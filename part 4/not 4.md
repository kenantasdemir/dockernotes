docker container run -d --name myContainer ozgurozturknet/adanzyedocker /usr/bin/top -b
// container içerisinde /usr/bin/top komutu çalıştırılır. -b seçeneği ile bu işleme dair özet bilgiler görüntüler.

docker image pull ozgurozturknet/adanzyedocker --quiet

<b><mark>docker checkpoint create --leave-running myContainer myCustomCheckPoint</mark></b><br>
//myContainer adlı containera ait bir checkpoint oluşturur ve adını myCustomCheckPoint atar.<br>
//bu containerı çalışır durumda bırakır.<br>


<b><mark>docker checkpoint ls</mark></b><br>
//checkpointleri listeler.<br>

docker checkpoint rm myCustomCheckPoint
//myCustomCheckPoint adlı check pointi siler.


<b><mark>docker images --all </mark></b><br>
//bütün imajları görüntüler.(default olarak intermediate imajları saklar)<br>

<b><mark>docker images --digests</mark></b><br>
//imajlar hakkında özet bilgi görüntüler.<br>

<b><mark>docker images --quiet</mark></b><br>
//sade imaj idlerini görüntüler.<br>

<b><mark>docker rename myContainer myUpdatedContainer</mark></b><br>

<b><mark>docker search busybox</mark></b><br>
//adında busybox ifadesini içeren imajları görüntüler.<br>

<b><mark>docker search --filter stars=3 busybox</mark></b><br>
//adında busybox ifadesini içeren imajlardan yıldız sayısı 3 olanları görüntüler.<br>

<b><mark>docker port myContainer 80/tcp</mark></b><br>
//myContainer adlı bir Docker konteynerinin 80 numaralı TCP portunu yerel makinedeki ilişkili portla gösterir. <br>
//Bu, konteyner içinde çalışan bir uygulamanın, yerel makinede hangi portu dinlediğini gösterir. <br>

docker tag myimage:latest myregistry.com/myimage:v1.0
//docker tag komutu ile imajara tag eklenir


docker commit -c 'CMD ["java","uygulama"]' con1 kenant42/con1:v2.0
//imaj içine CMD ["java","uygulama"] komutu eklendi. bu imajdan bir container //oluşturulduğunda bu komut çalışacak


//Dockerfile dosyasında değişken tanımlamak istersek ARG kullanılır. sadece imaj yaratılma aşamasında geçerlidir.
docker image build -t x2 --build-arg VERSION=1.2.3 .


