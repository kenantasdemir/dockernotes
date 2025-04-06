<b><mark>docker logout</mark></b><br>
// Docker Hub veya diğer Docker imaj kaynaklarına yapılmış olan oturum açma işlemini sonlandırır ve kullanıcının kimlik bilgilerini siler.<br>


<b><mark>docker login</mark></b><br>
//docker imaj kaynağında oturum açar.<br>


‼️ Aksi belirtilmediği takdirde docker default olarak latest tagını kullanır.


<b><mark>docker image tag mysql:5 kenant42/ornekdocker:latest</mark></b><br>
//mysql:5 adlı Docker imajını kenant42/ornekdocker:latest adlı yeni bir imaj olarak etiketler.<br>

<b><mark>docker image ls</mark></b><br>
//imajları listeler.<br>

<b><mark>docker image push kenant42/ornekdockerdeneme:latest</mark></b><br>
//kenant42/ornekdockerdeneme:latest adlı imajı repoya yollar<br>

<b><mark>docker image pull kenant42/ornekdockerdeneme:latest</mark></b><br>
//kenant42/ornekdockerdeneme imajının latest tagını çeker.<br>


---


docker image build -t kenant42/ornekdocker -f Dockerfile . 
docker container run kenant42/ornekdocker
docker image history kenant42/ornekdocker


---

docker image history kenant42/ornekdocker
//Bu komut, kenant42/ornekdocker adlı imajın geçmişini görüntülemeye yarar. 
//Bu komut ile, imajın oluşturulması için kullanılan katmanlar, her katmanın boyutu, 
//hangi komutların çalıştırıldığı ve ne kadar süreyle çalıştığı gibi bilgiler elde edilebilir.

docker image history ubuntu:18.04

docker image push kenant42/ornekdocker
//kenant42/ornekdocker adlı imajı repoya gönderir.

docker imageları layerlar halinde tutar


---



docker image build -t kenant42/py .
//mevcut dizinde bulunan Dockerfile adlı dosyadan bir imaj oluşturur.

docker tag kenant42/py kenant42/py:v1.0
//kenant42/py adlı imaja v1.0 tagını ekler.


docker container run --rm -p 80:5000 kenant42/py:v1.0
//kenant42/py:v1.0 adlı imajdan bir container oluşturur.
// --rm parametresi ile container durduğu anda silinir.
//80 portu ile containerın 5000 portunu eşler.


docker ps
//çalışan containerları listeler.

docker stop hadf4ds56H4sh
//idsi belirtilen containerı durdurur.

docker image build -t ozgurozturknet/node .
docker container run -d -p 80:8080 node2




---



ls ; date
//tek satırda birden fazla komut çalıştırmamıza izin verir

cat abc.txt && echo "dosya bulundu"
cat def.txt || echo "dosya bulunamadı" 

---

#sistemin düzgün çalıştığını ve nginx daemon'ının web sitesini publish etmekte bir sorun yaşamadığını test ediyoruz
HEALTHCHECK --interval=30s --timeout=10s --start-period=5s --retries=3 CMD curl -f http://localhost/ || exit1

docker image build -t kenant42/hello-docker .
//kendi imajlarımızı oluşturmak istediğimi docker image build komutunu kullanırız.
//bu örnekte oluşturacağımız imajın konfiguraasyonları Dockerfile isimli dosyadan alınır.
//eğer dosya adı belirtilmezse docker default olarak Dockerfile isimli dosya arar.
//. parametresi ile Dockerfile adlı dosyanın mevcut dizinde olduğu belirtilir.
//-t parametresi ile imaja tag atanır. bu tag Dockerfile içinde belirtilir.

docker container run -d --name hellodocker -p 80:80 kenant42/ornekdocker
//kenant42/ornekdocker imajından hellodocker adlı bir container oluşturulur. bu container detach olarak çalışır.
//80 portu ile containerın 80 portu eşlenir.


tek bir run komutu içinde birden fazla işlem yapılabilir
\ ile komutlarımızı daha okunaklı hale getirmek için bölmemizi sağlar

docker container run -d -p 80:80 --name hd2 -e KULLANICI="Kenan TASDEMİR" kenant42/ornekdocker
//kenant42/ornekdocker imajından hd2 adlı bir container oluşturuldu. bu containerda KULLANICI adlı ortam değişkeni oluşturuldu.
//bu ortam değişkeninin değerini görmek için aşağıdaki komutlar çalıştırılmalıdır.

docker exec -it hd2 sh
//hd2 adlı containerda shell açıldı.

echo $KULLANICI
//ortam değişkeni ve değeri yazdırıldı.
exit
//shellden çıkıldı.

docker image inspect kenant42/ornekdocker
//kenant42/ornekdocker adlı imajın özellikleri görüntülendi.

kullandığınız base imagedaki değerler sizin imageınıza inherit edilir

---

docker image build -t addcopy .
//mevcut dizinde bulunan Dockerfile adlı dosyayı kullanarak addcopy adlı bir imaj oluşturur.
//. parametresi Dockerfile adlı dosyanın mevcut dizinde olduğunu belirtir.


docker run -it addcopy sh
//addcopy adlı imajdan bir container oluşturur ve bu containerda shell açar.

uzak sunucudan alındığında add fonksiyonu ilgili sıkıştırılmış dosyayı açmaz direk atar

---

docker image build -t javaimaj .
//Bu komut, mevcut dizindeki Dockerfile'ı kullanarak javaimaj adlı bir Docker imajı oluşturur.
//-t veya --tag parametresi, oluşturulan imaja bir etiket eklemek için kullanılır.

docker run javaimj
//Bu komut, javaimaj adlı Docker imajını çalıştırır ve 
//varsayılan olarak imajın CMD veya ENTRYPOINT direktifinde belirtilen komutu çalıştırır. 
//Bu örnekte Dockerfile'da bir CMD direktifi belirtilmemiş, 
//bu nedenle Docker imajı varsayılan olarak çalıştırılmak üzere hazır hale getirilir.

docker run javaimj ls
//Bu komut, javaimaj adlı Docker imajını çalıştırır ve ls komutunu çalıştırarak imajın içindeki dosya listesini gösterir. 



docker image build -t pingimaj -f .\Dockerfile.Centos .
//Dockerfile.Centos dosyasını kullanarak pingimaj adlı bir Docker imajı oluşturur. 
//-t veya --tag parametresi, oluşturulan imaja bir etiket eklemek için kullanılır. 
//-f veya --file parametresi, Dockerfile dosyasının adını ve yolunu belirler.

docker run pingimaj
//pingimaj adlı imajdan bir container oluşturur.



---

docker image build -t ozgurozturknet/hello-docker .

tek bir run komutu içinde birden fazla işlem yapılabilir
\ ile komutlarımızı daha okunaklı hale getirmek için bölmemizi sağlar


docker image build -t myfirstimaj .
//mevcut dizinde bulunan Dockerfile adlı dosyayı kullanarak myfirstimaj adlı yeni bir imaj oluşturur.

docker container run --name firstcon myfirstimaj
//myfirstimaj adlı imajdan firstcon adlı yeni bir container oluşturur.



docker container run --name shellcontainer myfirstimaj
//myfirstimaj adlı imajdan shellcontainer adlı yeni bir container oluşturur.

FROM centos:latest
ENV TEST-"Bu bir denemedir"
CMD echo STEST




---

Multi-stage image build 
imaj yaratma aşamasını kademelere bölmemize ve ilk kademede yarattığımız imaj içerisindeki dosyaları
bir sonraki kademede oluşturacağımız imaja kopyalayabilmemize imkan sağlar. bu sayede nihai imaj boyutumuzun küçülmesine imkan tanıyor.


---

docker image build -t uygulama:3.7.6 .
//mevcut dizinde bulunan Dockerfile adlı dosyayı kullanarak yeni bir imaj oluşturur.
//bu imajın ismi uygulama olacaktır. tagı ise 3.7.6 şeklindedir.



docker image build -t x1 --build-arg VERSION=3.7.1 .
//Bu komut, . dizinindeki Dockerfile dosyasını kullanarak bir Docker imajı oluşturur. 
//Oluşturulan imajın adı x1 olarak belirlenir. 
//Ayrıca, --build-arg parametresi ile Dockerfile içinde tanımlı olan VERSION değişkenine 3.7.1 değeri atanır.


docker image build -t x2 --build-arg VERSION=3.8.1 .

ARG ile oluşturulan değişkenler sadece image yaratılma aşamasında geçerli olur
ARG ile tanımlanan değişken bu imajdan yaratılan container içerisinden erişilemez

---




docker container run -it --name con1 ubuntu:latest bash
//ubuntu:latest imajından con1 adlı yeni bir container oluşturur.
//bu containerda interaktif olarak bash açar.

apt-get update
mkdir /temp
cd /temp
apt-get install wget
wget https://wordpress.org/latest.tar.gz
//wordpress son sürümü indirildi.
exit
clear

docker image oluşturma yöntem 2(containerdan image oluşturma)

docker commit con1 kenant42/con1:latest
//kenant42/con1:latest tagli image haline geldi
//Bu komut, bir Docker container'dan yeni bir image oluşturur ve bu image'ı belirtilen ad ve etiketle (kenant42/con1:latest) kaydeder. 
//Bu, container'ın mevcut durumunu kaydederek ve bu duruma dayalı bir image oluşturarak container'ı "dondurmayı" sağlar. 
//Bu, özellikle bir container'ı hızlı bir şekilde kurtarmanız veya başka bir ortama taşımanız gerektiğinde yararlı olabilir.


docker run -it --name con2 kenant42/con1:latest bash
//kenant42/con1:latest adlı containerın imajından con2 adlı yeni bir container oluşturur.
//bu container içerisinde interaktif olarak bash açar.


docker commit -c 'CMD ["java","uygulama"]' con1 kenant42/con1:ikinci
//komutu, bir Docker container'dan yeni bir image oluşturur ve bu image'ı belirtilen ad ve etiketle (kenant42/con1:ikinci) kaydeder.
//-c parametresi, yeni image'ın oluşturulması sırasında geçerli olan Dockerfile komutlarını belirler. 
//Burada CMD komutu, oluşturulan image çalıştırıldığında otomatik olarak yürütülecek olan komutu belirtir. 
//Bu örnekte, CMD ["java","uygulama"] komutu, uygulama adlı bir Java uygulamasını başlatır. 

docker image inspect kenant42/con1:ikinci
//kenant42/con1:ikinci adlı imajın özelliklerini görüntüler.



---


<b><mark>docker save kenant42/con1:latest -o con1imaj.tar</mark></b><br>
//docker save komutu docker imajını kaydetmek için kullanılır.<br>
//kenant42//con1:latest kaydedilecek docker imajının adı ve etiketini belirtir.<br>
// -o con1imaj.tar parametresi docker imajının kaydedileceği yolu belirtir.<br>
//kenant42//con1:latest adlı imajı con1imaj.tar olarak kaydeder. yani sıkıştırır.<br>


<b><mark>docker load -i con1imaj.tar</mark></b><br>
//bu komut ile docker imajı bir arşiv dosyasından yüklenir.<br>





---
				---MULTISTAGE 1 --

docker container run --name javauygulama javasdk

docker cp javauygulama:/usr/src/uygulama .
cd uygulama
cd ..


docker image build -t javajre -f .\Dockerfile.jre .


	---MULTISTAGE 2 --

docker image build -t javason .
docker image ls


---

docker image build -t uygulama:3.7.6 .
//İMAJA TAG ATANDI
docker image build -t uygulama:3.8.1 .


docker image build -t x1 --build-arg VERSION=3.7.1 .
docker image build -t x2 --build-arg VERSION=3.8.1 .

ARG ile oluşturulan değişkenler sadece image yaratılma aşamasında geçerli olur
ARG ile tanımlanan değişken bu imajdan yaratılan container içerisinden erişilemez

---

docker image oluşturma yöntem 2(containerdan image oluşturma)


docker container run -it --name con1 ubuntu:latest bash
apt-get update
mkdir /temp
cd /temp
apt-get install wget
wget https://wordpress.org/latest.tar.gz
exit
clear

docker commit con1 ozgurozturknet/con1:latest
//ozgurozturknet/con1:latest tagli image haline geldi

docker commit -a "kenant42" -m "Hello World" b33container be33imaj
docker commit --change='CMD ["python", "app.py"]' my-container new-image:latest
docker commit \
  --change='ENV APP_ENV=production' \
  --change='CMD ["node", "server.js"]' \
  my-container new-image:latest




docker run -it --name con2 ozgurozturknet/con1:latest bash
cd /temp
ls

docker commit -c 'CMD ["java","uygulama"]' con1 ozgurozturknet/con1:ikinci
docker image inspect ozgurozturknet/con1:ikinci


---

docker image ls
mkdir image
cd image
ls
clear

docker save ozgurozturknet/con1:latest -o con1imaj.tar
//docker imajını con1imaj.tar olarak dışarı aktardık

ls
docker load -i .\con1imaj.tar
// ozgurozturknet/con1:latest isimli imaj oluşturdu




---
























