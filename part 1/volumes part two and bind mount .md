Docker containerları, uygulama veya hizmetlerin çalıştırılmasında kullanılan yalıtılmış bir ortam sağlar. 
Ancak bu yalıtım, containerların birbirleri veya ana bilgisayar ile dosya paylaşımını kısıtlayabilir. 
Bu nedenle, verilerin containerlar arasında veya ana bilgisayar ile paylaşılması gerektiğinde, volume objeleri kullanılır.

Volume objeleri, Docker'da dosyaların containerlar arasında paylaşılması için kullanılan bir yöntemdir.
 Volume objeleri, containerlar arasında paylaşılan bir dosya sistemi sağlar ve verilerin disk üzerinde saklanmasını sağlar. 
Bu sayede, containerlar arasında veri paylaşımı daha kolay ve verimli bir şekilde yapılabilir.

Bununla birlikte, Docker'da volume objelerinin mount edileceği yöntemler farklı olabilir. 
<b><mark>Volume objeleri, host dosya sistemi tarafından sağlanan bir disk bölümüne veya uzaktan bir depolama alanına bağlanabilir.</mark></b><br>
 Bu nedenle, volume objelerinin nereye monte edileceği, 
containerların gereksinimlerine ve verilerin nerede saklanacağına bağlı olarak değişebilir.<br>

Docker'da, volume objeleri containerlar arasında dosya paylaşımını sağlamak için kullanılır 
ve bu nedenle containerlarla bir bağlantıları vardır. 
Volume objeleri, Docker hostu ve containerlar arasında bir köprü görevi görerek,
containerlardaki verilerin disk üzerinde saklanmasını sağlar.

Docker'da bir volume oluşturmak, Docker ana makinesinde bir dosya sistemi alanı ayırmak 
ve bunu bir veya daha fazla Docker konteynerine monte etmek anlamına gelir. 
Bu nedenle, <b><mark>bir konteynerle birlikte bir volume oluşturulduğunda, 
volume silinse bile konteyner içindeki dosyalar kalıcı olarak saklanır. </mark></b><br>
Ancak, volume oluşturulduğunda --name seçeneği ile adlandırılabilir ve böylece 
diğer konteynerlar da aynı volume'u kullanabilirler. 
Bu durumda, tüm konteynerlar volume'u paylaşır ve volume silinirse, 
tüm konteynerların içindeki dosyalar da silinir.


Docker'da volume objeleri, containerlarla birlikte oluşturulabilir veya daha sonra eklenebilir.
 Bu volume objeleri, containerlarla ilişkilendirilerek, containerların içindeki verilerin
 bu volume objeleriyle eşleştirilmesi sağlanır. Böylece, verilerin paylaşımı daha verimli bir şekilde yapılabilir.

Özetle, Docker'da volume objeleri, containerlarla yakından bağlantılıdır ve 
containerlar arasında dosya paylaşımını sağlamak için kullanılırlar.

docker volume create ilkvolume
//ilkvolume adında volume oluturuldu.

docker volume inspect ilkvolume
//ilkvolume adlı volmue hakkında bilgiler listelendi


docker container run -it --name my-container -v my-volume:/path/in/container alpine sh
//my-volume isimli volume nesnesi containera bağlandı.


docker container run -it -v ilkvolume:/uygulama alpine sh
Bu komut, alpine adlı bir Docker imajını kullanarak bir Docker konteyneri çalıştırır. 
Konteyner, it parametresi sayesinde etkileşimli modda başlatılır ve kullanıcı bir kabuk ortamına (sh) girer. 
Ayrıca -v parametresi, ilkvolume adlı bir Docker volumünü konteynere bağlar. 
Bu, /uygulama dizinindeki dosyaların ilkvolume adlı Docker volumünde saklanacağı anlamına gelir. 
Bu komut, Docker konteynerinde çalıştırılan bir uygulamanın, 
uygulamanın gerektirdiği dosyaları dışarıda (ana bilgisayar sistemde) tutmak için kullanılabilir.

<b><mark>çalışan containera volume bağlanabilir.</mark></b><br>
aşağıdaki gibi bir komutla çalışan bir containera volume bağlanabilir.<br>
docker container run --mount source=<volume-adı> target=<hedef-dizin> <container-adı veya ID'si><br>


container silinse bile volume silinmez. 
Volume nesnesi container'a bağlandıktan sonra bağımsız bir varlık 
olarak devam eder ve manuel olarak silinene kadar kalır. 
Bu, volume nesnesiyle bağlantısı kesilen yeni containerların oluşturulmasına olanak tanır.

Bunun için, docker volume rm komutu ile açıkça silinmesi gerekir. 
<b><mark>Ancak, bir volume, kullanılmayan bir container'ın silinmesi sırasında otomatik olarak silinebilir.</mark></b><br>
Bunu önlemek için, volume'u silmek yerine, docker volume prune komutunu kullanabilirsiniz, 
bu komut kullanılmayan tüm volumeleri siler. 


docker volume create --label app=my-app --label env=production my-volume
//my-volume adlı volume nesnesi oluşturuldu.
//bu nesneye app=my-app ve env=production olmak üzere iki label eklendi.

volumeleri containerlara mount ederiz
image içinde olmayan klasörede volume bağlayabiliriz


docker container run -it -v ilkvolume:/uygulama alpine sh
container içine bağlanacak klasör = uygulama
alpine = image

volumeleri containerlara mount ederiz

image içinde olmayan klasörede volume bağlayabiliriz

volumelerin containerlarla bir bağları yoktur

docker container run -it -v ilkvolume:/deneme3:ro centos sh

ro = readonly



docker container run -it -v ilkvolume:/deneme3:ro centos sh
//Bu komut, CentOS imajını kullanarak interaktif bir konteyner oluşturur. 
//Konteyner, ilkvolume adlı bir volume nesnesini /deneme3 dizinine bağlar. 
//:ro seçeneği, volume'un salt okunur (read-only) olarak bağlanmasını sağlar, 
//yani konteynerden bu dizindeki dosyaları yazamazsınız. 
//Bu seçenek, volume içindeki verilerin yanlışlıkla değiştirilmesini önlemek için kullanışlıdır. 
//Son olarak, sh komutu, konteynerda bir kabuk oturumu açar.


##########################################################################################

Boş-Dolu Volume Mount Edildiğinde Ne Olur?
1. Eğer bir volume mount edildiği klasör mevcut değilse bu klasörü yaratır.
  Ve o anda volume içerisinde hangi dosyalar varsa bu klasörde de o
  dosyaları görürsünüz. Boşsa boş görürsünüz.
2. Eğer bir volume imaj içerisinde bulunan mevcut bir klasöre mount edilirse:
A: Klasör boşsa o anda volume içerisinde hangi dosyalar varsa bu klasörde de
o dosyaları görürsünüz.
B: Klasörde dosya varsa ve volume boşsa bu sefer o klasördeki dosyalar
volume'e kopyalanır.
C: Klasörde dosya var ya da yok fakat volume'de dosyalar varsa yani volume
boş değilse, bu sefer siz o klasörün içerisinde volume'de ne dosya varsa onu
görürsünüz.


docker container run --rm -it kenant42/ornekdocker sh
//--rm seçeneği ile bu container kapatıldığında silineceği belirtildi.
exit
docker ps -a

docker volume create deneme1
//deneme1 adlı volume nesnesi oluşturuldu.

docker volume ls
//volume nesnelerini listeler.

docker volume inspect deneme1
//deneme1 adlı volume nesnesinin özelliklerini görüntüler.

docker volume prune
//kullanılmayan volume nesnelerini siler.

docker volume prune --filter "label=myLabel"
//kullanılmayan volume nesnelerinden sadece label değeri "myLabel" olanları siler.

docker volume rm volumeId1 volumId2 volumId3
//idleri belirtilen volume nesnelerini siler.

docker volume update
//bu komut sadece swarm modda çalışır.
--availability active pause drain



-----------------------------------------------


docker container run --rm -it -v deneme1:/test kenant42/ornekdocker sh
//test klasörü yoktur yeni oluşturulur içi boş bir şekilde
deneme1 isimli volumeü bu container içindeki test klasörüne mount ettik
exit


docker container run --rm -it -v deneme1:/usr/src/myapp kenant42/ornekdocker sh
//Bu komutla birlikte kenant42/ornekdocker adlı Docker imajından bir container oluşturulur. 
//Bu container, --rm parametresi sayesinde sonlandırıldığında otomatik olarak silinecektir. 
//Container oluşturulurken, -v deneme1:/usr/src/myapp komutu sayesinde deneme1 adlı bir volume, 
///usr/src/myapp dizinine mount edilir. 
//Bu komut ayrıca, -it parametresi sayesinde etkileşimli bir terminal açar ve sh komutu çalıştırarak bir shell oturumu başlatır. 
//Bu sayede kullanıcı, container içinde işlem yapabilir.

// /usr/src/myapp içindeki dosyalar volume kopyalanır
exit


docker container run --rm -it -v deneme1:/xyz alpine sh
//deneme1 adlı volume /xyz klasörü içindeki dosyaları kendine kopyalar.


-----------------------------------------------

docker container run --rm -it -v deneme1:/usr/src/myapp kenant42/ornekdocker sh
///usr/src/myapp dizinindeki dosyalar deneme1 adlı volume kaydedilir. 

dolu bir volumeü dolu bir klasöre mount ederseniz sadece volume içindeki dosyalar görünür

-----------------------------------------------

‼️ ciddi verilerle uğraşırken production gibi ortamlarda veri saklamak için sadece volume kullan

‼️  bind mounts production ortamında kullanılmamalıdır!!!

Host üstündeki bir klasör ya da dosyayı
  Container içerisine map edebiliriz.
      Buna Bind Mount denilir

Docker'da Bind Mount, Docker containerlarındaki dosya sistemleriyle Docker hostu arasında bir köprü görevi gören bir yöntemdir.
 Bind Mount, belirli bir host dosya sistemini bir Docker containerının dosya sistemi ile eşleştirmeyi sağlar.

Bind Mount'ın temel amacı, Docker containerlarının bir ana bilgisayarın dosya sistemine erişmesini sağlamaktır.
 Bu, Docker containerlarının dışarıya veri göndermesine veya almasına izin verir.
 Ayrıca, Docker containerlarının ana bilgisayarın dosya sistemine erişmesine izin vererek,
 containerların konfigürasyon dosyalarını ve log dosyalarını saklamasını sağlar.

Bind Mount'ın avantajı, Docker hostu ve containerlar arasındaki veri paylaşımını kolaylaştırmasıdır. 
Bind Mount, Docker containerlarında depolanan verilerin dışarıya aktarılmasını ve bu verilerin kalıcı hale getirilmesini sağlar. 
Böylece, Docker containerlarının veri saklama kapasitesi artar ve containerlar arasında veri paylaşımı daha verimli bir şekilde yapılabilir.

Bind Mount, Docker komut satırı aracılığıyla veya Dockerfile dosyaları aracılığıyla oluşturulabilir.
 Bind Mount oluştururken, belirli bir host dosya sistemine erişimi sağlamak için bir kaynak ve hedef belirtilir.
 Bu şekilde, Docker containerlarına erişilebilir bir dosya sistemi oluşturulur ve containerlar arasındaki veri paylaşımı daha kolay hale gelir.


docker container run -d -p 80:80 ozgurozturknet/adanzyedocker
docker ps -a

docker container run -d -p 88:80 -v C:\AdanzyeDocker\kisim3\bolum28\websitesi:/usr/share/nginx/html nginx
docker rm -f containerID



docker container run -d -p 80:80 --name ilkweb nginx
docker exec -it containerID sh
//containera bağlanıldı
exit

docker ps -a
//çalışan ya da çalışmayan tüm containerları listeler.

docker rm -f hfds4456sdhf4
//id değeri belirtilen containerı siler.
//normalde çalışan container ancak durdurulduktan sonra silinebilir.
//fakat -f seçeneği ile container durmaya zorlanır ve silinir.

docker container run -d -p 8080:80 --name myapp --mount type=bind, source=/path/to/myapp, target=/var/www/html my-image
Bu komut, /path/to/my-app dizinini Docker container'ının /var/www/html diziniyle eşleştirir. 
Bu sayede, Docker container'ında /var/www/html dizini, host'ta bulunan /path/to/my-app diziniyle aynı verilere sahip olacaktır.

Daha sonra, herhangi bir değişiklik yaptığınızda bu değişiklikler Docker container'ına da yansıyacaktır. 
Böylece, uygulamanızda yapılan değişiklikler Docker container'ına yansıyacak ve uygulamanız Docker container'ı içinde çalışmaya devam edecektir.

bind mount kendi sistemlerimizde development yaparken kullandığımız bir özellik


docker volume prune

Description
Remove all unused local volumes. Unused local volumes are those which are not referenced by any containers. 
By default, it only removes anonymous volumes.

Options
Option	Default	Description
-a, --all		API 1.42+ Remove all unused volumes, not just anonymous ones
--filter		Provide filter values (e.g. label=<label>)
-f, --force		Do not prompt for confirmation

docker volume create
docker volume inspect
docker volume ls
docker volume prune
docker volume rm
docker volume update

-----------------------------------------------


docker container run --rm -it -v deneme1:/test ozgurozturnet/adanzyedocker sh
//test klasörü yoktur yeni oluşturulur içi boş bir şekilde
deneme1 isimli volumeü bu container içindeki test klasörüne mount ettik
exit


docker container run --rm -it -v deneme1:/usr/src/myapp ozgurozturnet/adanzyedocker sh
ls
// /usr/src/myapp içindeki dosyalar volume kopyalanır
exit


docker container run --rm -it -v deneme1:/xyz alpine sh
cd /xyz
ls
exit
docker ps -a
docker volume ls

-----------------------------------------------

docker container run --rm -it -v deneme1:/usr/src/myapp ozgurozturnet/adanzyedocker sh
ls

dolu bir volumeü dolu bir klasöre mount ederseniz sadece volume içindeki dosyalar görünür

-----------------------------------------------
































