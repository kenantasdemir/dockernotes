

docker compose up
#$ bulunduğu dizinde docker compose .yaml uzantılı dosya arar.
docker-compose -f dockerfile.yaml up
docker compose -f dockerfile1.yaml -f dockerfile2.yaml up

docker-compose down
//servisleri durdurur ve siler

<b><mark>docker-compose config</mark></b><br>

<b><mark>docker-compose images</mark></b><br>
//servislerin hangi imajdan oluştuğunu görüntüler<br>

<b><mark>docker-compose logs</mark></b><br>

docker-compose exec webservis ls -a
//servis içerisinde komut çalıştırdık.

docker-compose up -d

docker-volume rm volumeName

docker-compose build

Docker-compose production ortamında kullanılmaz. Geliştirme ya da
Test ortamında kullanılmalıdır.


Docker swarm init
Komutu çalıştırıldğında engine moddan swarm moda geçilir
Arkaplanda etcd adı verilen key-value replikası devreye alınır
Cluster ile ilgili verliert Burda şifrelenmiş olarak tutulur.
Swarm bunun yanında bir de Certificate Authority Kurar ve sertifkalar yayınlar
Bu sertifikalar Cluster eklenen Tüm nodelara dağıtılır. Bu sayede
Swarm managerlar ve nodelar arasındajki tüm iletişim TLS Protokoll kullanılarak
Yetkilendirilir ve şifrelenir.

Ayrıca iki adet random token üretilir. Biri worker eklemek için diğeri de Manager eklemek için.
Docker info

Docker swarm init --advertise-addr 192.168.0.13


Docker swarm join-token worker
Docker swarm join-token Manager 

Docker node ls

Docker service Create --name test --replicas=5 -p 8080:80 nginx
Docker service ps test

Varsayılan olarak Managerlarda birer worker olarak çalışır fakat production ortamında
Bu istenmeyen bir durumdur.

docker service create --help

Docker service Create --name test nginx

Docker service Logs test
Docker service scale test=3
Docker service scale test=2

Docker service rm test

Docker service Create --name glb --node=global nginx

Docker service create --name web --network over-net -p 8080:80 --replicas=3 imajName

Docker service update --help

Docker service update --detach --update-delay 5s --update-parallelism 2 --image imajName webservisim 

Docker service Rollback --detach webservisisim

Docker Secret Create user_name .\\user_name.txt

Docker service Create -d --name secretornek --secret user_name imajName
Secretlar silinemez

Docker service update --secret-rm user_name --secret-add kullanici_adi secretornek

Docker stack deploy -c .\\docker-compose.yml ilkstack
Docker stack ls
Docker stack Services ilkstack

Stackler bilden fazla Servisi tek bir configürasyon dosyası altında oluşturmamıza
Imkan deren docker objesidir.

Docker stack rm ilkstack
