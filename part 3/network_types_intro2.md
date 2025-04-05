<b><mark>docker container run -d --publish 8080:80 imageName</b></mark>
<br>

<b><mark>docker container run -d --publish 8080:80 -p 8043:443 imageName</mark></b>
<br>
//containerı detach olarak oluşturur. 8080 portu ile containerın 443 portu ile eşleştirir. 

<br>
<b><mark>docker container run -d --publish 8080:80 -p 53:53/udp imageName</mark></b>
//container oluşturur ve Docker host'un 53 numaralı UDP portunu konteynerın 53 numaralı UDP portuna yönlendirir.

<br>
<b><mark>docker container run -d --publish 8080:80 kenant42/ornekdocker</mark></b>
//kenant42/ornekdocker imajından bir container oluşturur. 8080 portu ile containerın 80 portunu eşler.

<br>

:x: default bridge ile bağlı containerlar arasında DNS hizmeti yoktur

<br>

<b><mark> docker container run -d --name websunucu1 kenant42/ornekdocker</mark></b>
<br>

<b><mark>docker container run -it -d --name database1 kenant42/ornekdocker sh</mark></b>
//kenant42/ornekdocker imajından database1 adlı container oluşturur ve bu container içinde shell açar

<br>
-d (detached mode):
Bu parametre, Docker container'ını arka planda çalıştırmak için kullanılır. Eğer -d parametresi eklenmezse, container terminale bağlanır ve çıktı terminalde görünür, ancak -d kullanıldığında, container arka planda çalışır ve terminali serbest bırakır.


<br>
-it (interactive + TTY):
-i (interactive): Container'ın etkileşimli modda çalışmasını sağlar. Bu, container içinde komut girmeyi ve çalıştırmayı mümkün kılar.

-t (TTY): Terminal (TTY) için bir bağlantı sağlar, yani komutları yazmak ve çıktı almak için terminal benzeri bir ortam yaratır.
Genellikle, -it kombinasyonu, kullanıcıların container ile etkileşimde bulunabilmesi için kullanılır. Örneğin, bir terminal açıp içine komut girebilmek için bu parametreler kullanılır.

<br>


docker ps -a
//çalışan ya da çalışmayan tüm containerları listeler.

docker container rm -f hfda5ad56had56hf hgfsja99afdsag5v12
//id değerleri belirtilen 2 containerı siler
//-f seçeneği ise bu containerların çalışması durumunda silmeye zorlar.

docker run --rm --network host nginx

// bir sistemde sadece 1 adet host türünde network objesi bulunabilir
//docker network create --driver bridge kopru2
//host network oluşturdu

docker network create kopru1
//kopru1 adlı network nesnesi oluşturuldu.

docker network create mycustomnet --driver host
//hata

docker network ls
//network objelerini listeler.

docket network inspect kopru1
//kopru1 adlı network objesininin özelliklerini görüntüler.



docker container run -dit --name websunucu --net kopru1 kenant42/ornekdocker sh

docker container run -dit --name database --net kopru1 kenant42/ornekdocker sh
//kenant42/ornekdocker imajından database adlı container oluşturur. bu containerı kopru1 adlı networke bağlar.
//-dit = -d -it
//d parametresi u containerın detach modda çalışaağı belirtilir.
//-it parametresi bu containera interaktif bir şekilde bağlanacağını belirtir.
//son olarak sh parametresi ile bu container içinde shell açar

docker ps

docker network inspect kopru1
//kopru1 adlı network nesnesinin özelliklerini görüntüler.

docker attach websunucu
//websunucu adlı docker konteynerının çalışma zamanı konsoluna bağlanmak için kullanılır.


:heavy_exclamation_mark: user tanımlı bridge'e bağlı olan containerlar arasında DNS hizmeti vardır

---------------------------------------------------------------------------------------------------------------------------------------


user tanımlı bridge'e bağlı olan containerlar arasında 
DNS hizmeti vardır


docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 kopru2
docker network ls

docker network inspect kopru2

---------------------------------------------------------------------------------------------------------------------------------------

kullanıcı tanımlı köprülerin önemli bir özelliği
containerlar çalışırken bunlara bağlanabilir
default bridge'te bu özellik yok

read escape sequence
docker network connect kopru2 database
//database adlı containerı kopru2 adlı network objesini bağlar

docker attach database
//database adlı docker konteynerının çalışma zamanı konsoluna bağlanmak için kullanılır.


bir container aynı anda birden fazla bridge bağlanabilir.

docker network disconnect kopru2 database
//containerla köprü bağlantısını kestik

docker network inspect kopru2



//eğer bir köprü bir containera bağlı ise bu köprü silinemez


docker network rm kopru2
//kopru2 adlı network objesini siler.

docker container rm -f websunucu database
//websunucu ve database adlı 2 containerı siler.

docker network rm kopru1




default bridge netwrk objesi
bu network nesnesine bağlı containerlar birbirleriyle haberleşebilir
fakat DNS yani isim çözümleme yoktur.
çalışan containerlara bağlanamazlar.

kullanıcı tanımlı bridge nesnelerinde ise
DNS vardır. çalışan containerlara bağlanabilirler.

read escape sequence
docker network connect kopru2 database
bir Docker konteynerini mevcut bir Docker ağına bağlamak için kullanılır. 
Bu komut, bir konteyneri yeni bir ağa bağlayarak, 
ağ üzerinde farklı konteynerlerle iletişim kurmasını sağlar.
docker attach database
çalışmakta olan bir Docker konteynerine bağlanmanıza olanak tanır. 
Bu komut, konteynerin standart giriş (stdin), 
standart çıkış (stdout) ve standart hata (stderr) akışlarını, 
yani konteynerin terminal çıktısını görmenizi ve etkileşime geçmenizi 
sağlar.



docker run -dit --network=kopru2 myContainer
//bir container başlatırken network nesnesi bağlandı.


docker network connect --ip 10.10.36.122 kopru2 mySecondContainer
//mySecondContainer adlı containerı kopru2 network objesine bağlandı.
//kopru2 ağı içerisinde kullanması için spesifik id atandı.

docker network disconnect kopru2 mySecondContainer
//mySecondContainer adlı containerın kopru2 nesnesiyle bağlantısı sonlandırıldı.

docker network prune --force --filter until=5m
//sistemdeki oluşturulma zamanı 5 dakikadan fazla olan network objelerini siler.
//--force seçeneği ile onay istemeden silinmeleri sağlanır.


docker network rm networkID kopru2
//id değeri ve ismi belirtilen network objelerini siler.

docker network rm kopru2
docker container rm -f websunucu database
docker network rm kopru1


Docker container Logs containerID
Docker logs --details containerName









































