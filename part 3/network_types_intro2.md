<b><mark>docker container run -d --publish 8080:80 imageName</b></mark>
<br>

<b><mark>docker container run -d --publish 8080:80 -p 8043:443 imageName</mark></b>
<br>
//containerı detach olarak oluşturur. 8080 portu ile containerın 443 portu ile eşleştirir. 

<br>
<b><mark>docker container run -d --publish 8080:80 -p 53:53/udp imageName</mark></b>
<br>
//container oluşturur ve Docker host'un 53 numaralı UDP portunu konteynerın 53 numaralı UDP portuna yönlendirir.
<br>

<br>
<b><mark>docker container run -d --publish 8080:80 kenant42/ornekdocker</mark></b>
<br>
//kenant42/ornekdocker imajından bir container oluşturur. 8080 portu ile containerın 80 portunu eşler.
<br>

:x: default bridge ile bağlı containerlar arasında DNS hizmeti yoktur

<br>

---------------------------------------------------------------------------------------------------------------------------------------
<b><mark> docker container run -d --name websunucu1 kenant42/ornekdocker</mark></b>
<br>

<b><mark>docker container run -it -d --name database1 kenant42/ornekdocker sh</mark></b>
<br>
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

---------------------------------------------------------------------------------------------------------------------------------------

<b>docker ps -a</b>
<br>
//çalışan ya da çalışmayan tüm containerları listeler.
<br>

<b>docker container rm -f hfda5ad56had56hf hgfsja99afdsag5v12</b>
<br>
//id değerleri belirtilen 2 containerı siler
<br>
//-f seçeneği ise bu containerların çalışması durumunda silmeye zorlar.
<br>

<b><mark>docker run --rm --network host nginx</mark></b>
<br>

<div>
  // bir sistemde sadece 1 adet host türünde network objesi bulunabilir
//docker network create --driver bridge kopru2
//host network oluşturdu
</div>
<br>

---------------------------------------------------------------------------------------------------------------------------------------


<b><mark>docker network create kopru1</mark></b>
<br>
//kopru1 adlı network nesnesi oluşturuldu.

<b><mark>docker network create mycustomnet --driver host</mark></b>
<br>
//hata

<b><mark>docker network ls</mark></b>
<br>
//network objelerini listeler.

<b><mark>docker network inspect kopru1</mark></b>
<br>
//kopru1 adlı network objesininin özelliklerini görüntüler.

---------------------------------------------------------------------------------------------------------------------------------------

<b><mark>docker container run -dit --name websunucu --net kopru1 kenant42/ornekdocker sh</mark></b>
<br>

<b><mark>docker container run -dit --name database --net kopru1 kenant42/ornekdocker sh</mark></b>
<br>
//kenant42/ornekdocker imajından database adlı container oluşturur. bu containerı kopru1 adlı networke bağlar.<br>
//-dit = -d -it  <br>
//d parametresi u containerın detach modda çalışaağı belirtilir. <br>
//-it parametresi bu containera interaktif bir şekilde bağlanacağını belirtir. <br>
//son olarak sh parametresi ile bu container içinde shell açar <br>

<br>
docker ps
<br>


<b><mark>docker network inspect kopru1</mark></b><br>
//kopru1 adlı network nesnesinin özelliklerini görüntüler.
<br>

<b><mark>docker attach websunucu</mark></b><br>
//websunucu adlı docker konteynerının çalışma zamanı konsoluna bağlanmak için kullanılır.

<br>
:heavy_exclamation_mark: user tanımlı bridge'e bağlı olan containerlar arasında DNS hizmeti vardır

---------------------------------------------------------------------------------------------------------------------------------------

✅ user tanımlı bridge'e bağlı olan containerlar arasında DNS hizmeti vardır


<b><mark>docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 kopru2</mark></b><br>
<b><mark>docker network ls</mark></b><br>

<b><mark>docker network inspect kopru2</mark></b>

---------------------------------------------------------------------------------------------------------------------------------------

<div align="center">
  kullanıcı tanımlı köprülerin önemli bir özelliği
containerlar çalışırken bunlara bağlanabilir
default bridge'te bu özellik yok
</div>
<br>


<b><mark>docker network connect kopru2 database</mark></b>
<br>
//database adlı containerı kopru2 adlı network objesini bağlar<br>
<br>
<b><mark>docker attach database</mark></b><br>
//database adlı docker konteynerının çalışma zamanı konsoluna bağlanmak için kullanılır.


✅ bir container aynı anda birden fazla bridge bağlanabilir.
<br>

<b><mark>docker network disconnect kopru2 database</mark></b>
<br>
//containerla köprü bağlantısını kestik
<br>

<b><mark>docker network inspect kopru2</mark></b>
<br>



:x: eğer bir köprü bir containera bağlı ise bu köprü silinemez

---------------------------------------------------------------------------------------------------------------------------------------

<b><mark>docker network rm kopru2</mark></b>
<br>
//kopru2 adlı network objesini siler.

<b><mark>docker container rm -f websunucu database</mark></b>
<br>
//websunucu ve database adlı 2 containerı siler.

<b>docker network rm kopru1</b>
<br>



<div >
  default bridge netwrk objesi
bu network nesnesine bağlı containerlar birbirleriyle haberleşebilir
fakat DNS yani isim çözümleme yoktur.
çalışan containerlara bağlanamazlar.

kullanıcı tanımlı bridge nesnelerinde ise
DNS vardır. çalışan containerlara bağlanabilirler.

</div>
<br>

---

<br>
<b><mark>docker network connect kopru2 database</mark></b>
<br>

<div>
  bir Docker konteynerini mevcut bir Docker ağına bağlamak için kullanılır. 
Bu komut, bir konteyneri yeni bir ağa bağlayarak, 
ağ üzerinde farklı konteynerlerle iletişim kurmasını sağlar.<br>
<br><b><mark>docker attach database</mark></b>
<br>
çalışmakta olan bir Docker konteynerine bağlanmanıza olanak tanır. 
Bu komut, konteynerin standart giriş (stdin), 
standart çıkış (stdout) ve standart hata (stderr) akışlarını, 
yani konteynerin terminal çıktısını görmenizi ve etkileşime geçmenizi 
sağlar.
</div>
<br>



<b><mark>docker run -dit --network=kopru2 myContainer</mark></b><br>
<br>
//bir container başlatırken network nesnesi bağlandı.<br>
<br>

<b><mark>docker network connect --ip 10.10.36.122 kopru2 mySecondContainer</mark></b><br>
<br>
//mySecondContainer adlı containerı kopru2 network objesine bağlandı.<br>
<br>
//kopru2 ağı içerisinde kullanması için spesifik id atandı.<br>
<br>
<b><mark>docker network disconnect kopru2 mySecondContainer</mark></b><br>
<br>
//mySecondContainer adlı containerın kopru2 nesnesiyle bağlantısı sonlandırıldı.<br>

<b><mark>docker network prune --force --filter until=5m</mark></b><br>
<br>
//sistemdeki oluşturulma zamanı 5 dakikadan fazla olan network objelerini siler.<br>
<br>
//--force seçeneği ile onay istemeden silinmeleri sağlanır.<br>

---------------------------------------------------------------------------------------------------------------------------------------
<b><mark>docker network rm networkID kopru2</mark></b><br>
//id değeri ve ismi belirtilen network objelerini siler.
<br>
<b><mark>docker network rm kopru2</mark></b><br>
<br>

<b><mark>docker container rm -f websunucu database</mark></b>
<br>

<b><mark>docker network rm kopru1</mark></b>
<br>













































