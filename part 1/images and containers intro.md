docker image pull ozgurozturknet/app1
docker container run --name ilkcontainer ozgurozoturknet/app1
docker container run --name ikincicontainer ozgurozturknet/app2

docker version
docker info

docker image pull kenant42/app1
//kenant42/app1 adlı imajı çeker.

docker run kenant42/app1
docker container run kenant42/app1
//bu iki komut aynı anlama gelir

docker image --help
//docker image komutu hakkında yardım sayfası görüntüler.

docker image rm --help
docker image rm -f hello-world

docker image inspect ubuntu:latest
//ubuntu:latest imajı hakkında detaylı bilgi görüntüler

docker image prune
//kullanılmayan imajları siler.

docker image ls
//sistemde mevcut olan imajları listeler.

docker image history ubuntu:latest
//ubuntu:latest imajına ait geçmişi görüntüler.

<b><mark>docker image load --input fedora.tar</mark></b><br>
//fedora.tar içindeki dosyaları imaj olarak yükler.<br>

<b><mark>docker image load < fedora.tar</mark></b><br>
//yukarıdaki komutun alternatifidir. Bu komutta imajları STDIN kullanarak yükler.<br>

docker image rm --help
//docker image rm komutu hakkında yardım sayfası görüntüler.

docker image rm -f hello-world
////docker image rm -f komutu hakkında yardım sayfası görüntüler.

docker container --help
//docker container komutu hakkında yardım sayfası görüntüler.

docker container run --help
//docker container run komutu hakkında yardım sayfası görüntüler.

docker container run --name ilkcontainer kenant42/app1
//kenant42/app1 imajından ilkcontainer adlı bir container oluşturur.

docker container run --name ikincicontainer kenant42/app2
//kenant42/app2 imajından ikincicontainer adlı bir container oluşturur.


imageların saklandığı yerlere image registry denir

docker container ls
//çalışan containerları gösterir

docker container ls -a
//gizliler dahil olmak üzere bütün containerları gösterir


Her container imajında,o imajdan bir container yarattığımız
  zaman varsayılan olarak çalışması için ayarlanmış bir
                   uygulama vardır
   Bu uygulama çalıştığı sürece container ayakta kalır
  Uygulama çalışmayı bıraktığında container da kapatılır



Docker imajında birden fazla uygulama olabilir. Sadece tek bir uygulama içermesi kural değildir.
docker imajında birden fazla uygulama olabilir.

Docker container başlatıldığı zaman otomatik çalışması için tek bir uygulamanın ayarlanmasına izin verir.
//`docker container run ubuntu:latest ping 127.0.0.1` gibi

Docker container başlatıldığı zaman otomatik çalışması için 
tek bir uygulamanın ayarlanmasına izin verir fakat container içerisinde
daha sonra bu uygulamanın yanında başka uygulamalar da çalıştırılabilir.

Container yaratılırken hangi uygulamayı çalıştırmasını istediğimizi belirtebiliriz.

Çalışan bir container içerisinde başka bir uygulama çalıştırma:
//`docker container exec 12a793b3fec0 ping 127.0.0.1`


Container'ı detach modda ve shell bağlantısı ile oluşturma (dit):
//`docker container run -dit nginx:latest sh`


docker container run -p 80:80 kenant42/ornekdocker
//kenant42/ornekdocker adlı imajdan bir container oluşturur. 80 portunu containerın 80 portuna eşler.

docker container logs containerID
//ilgili containera ait log kayıtlarını verir.

docker container run --name denemecon kenant42/ornekdocker java app1
//imagın default uygulaması yerine belirttiğimiz uygulamayı çalıştırdık


docker container stop ShY65fh56ad
//idsi belirtilen containerı durdurur.

docker container run -d -p 80:80 kenant42/ornekdocker
//kenant42/ornekdocker imajından yeni bir container oluşturuldu.
// -d parametresi ile bu container arkaplanda çalışıyor. 
//son olarak -p parametresi ile 80 portu ile containerın 80 portu eşleştirildi.

docker ls = docker ps
docker ls -a = docker ps -a

docker container rm ShY65fh56ad g6sdf5sd65 k445f4dsdf4h
//id değerleri belirtilen containerları siler.

//çalışan container silinemez
docker container rm -f containerID
//bu şekilde çalışan container silinebilir.


docker run -p [host_port]:[container_port]/[protocol] [image_name]
docker run -p 80:80/udp myfirstimage


########################################################################################


docker container run --name websunucu -p 80:80 -d kenant42/ornekdocker
//kenant42/ornekdocker imajından detach olarak çalışan websunucu adlı bir container oluşturuldu.
//80 portu containerın 80 portu ile eşleştirildi.

docker ps
//çalışan containerları listeler.

docker container exec -it websunucu sh
//websunucu adlı containera interaktif olarak shell açıldı.

-it = --interactive --tty

exit
//shell bağlantısını kapatmak için exit komutu kullanılır.
//containerla bağlantıyı kopardık fakat container hala çalışıyor



echo "merhaba dunya" >> index.html
// index.html dosyasın "merhaba dunya" metni eklendi.


containerın ilk uygulaması durduğu anda container da durur.

docker container exec -it websunucu sh
//websunucu adlı containera interaktif olarak shell açıldı.

ps
//processleri listeler 

kill 1
//containerın ilk uygulamasının process id değeri 1 dir.
//kill 1 komutu ile de bu process durdurulur.

exit
//bu komut ile shell kapatıldı

docker ps
//websunucu adlı containerın ilk processi durdurulduğu için containerın da durduğu
//gözlemlenebilir.

docker start websunucu
//websunucu adlı container yeniden çalıştırıldı.

docker ps
//containerlar ve durumları hakkında bilgiler görüntülendi.

docker stop websunucu
//websunucu adlı container yeniden durduruldu.


docker container run --name websunucu2 -p 80:80 kenant42/ornekdocker

aynı imagedan istediğiniz kadar container oluşturulabilir
bu containerlar ayrı sanal makineler gibi birbirinden habersizdir.

containerın kendine ait yazılabilir katmanı olur bu değişiklikler orada tutulur.
docker image readonly olarak kalır

docker container prune
//çalışmayan containerları siler

docker image ls
//sistemde yüklü imajları listeler

docker image prune -a
//sistemde yüklü çalışmayan gizli imajları siler

docker image pull alpine
//alpine imajını çeker

docker image pull kenant42/ornekdocker
//kenant42/ornekdocker adlı imajı çeker



Docker kurulduğunda Docker daemon ve docker cli kurulur.
Docker cli ise enginele REST API üzerinden konuşur.
Daemon linuxta çalışır


Docker Version
Docker info
Docker

Docker run hello-world
Docker Container run hello-world

Docker image rm --help

Docker Container run --name ilkcontainer imageName
Container çalıştırıldığında Container Shelli client shelline bağlanır.

Docker Container ls 
#$çalışan containerları listeler

Docker Container ls -a
#$çalışan ve çalışmayan containerları listeler. 


Docker Container run -p 80:80 imageName

Docker Container Logs containerID

Docker Container stop ContainerinerID

ÇALIŞAN CONTAİNER SİLİNEMEZ

Docker Container rm -f containerID
#$ÇALIŞAN CONTAİNERI SİLMEYE ZORLAR


Docker Container run --websunucu -p 80:80 -d imageName 
Docker Container exec -it websunucu sh

Docker Container start containerID


Docker UNION FILE SYSTEM kullanır
Docker imajları mevcut Bir base imaj üzerine inşaa edilir.


Her containerın kendine ait yazılabilir katmanı vardır.
Tim değişiklikler Korda tutulur.
Imajlar read only olarak kalur.


Copy on Write

docker container prune
#çalışmayan tüm containerları siler

docker container kill -s
#çalışan tüm containerları siler. s parametresi ile sinyal gönderir.

Docker image prune -a

Docker image pull alpine

Docker Container run -it -v ilkvolume:/containericindekiKlasor alpine sh

Docker volume ls

Docker container run --rm -it imageName sh
#rm opsiyonuyla container kapatıldığında silinir.

#Exit ile containerla bağlantı kesilir.

docker volume create denemeVolume
 
































