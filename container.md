docker container containerID
docker container rename actualContainerName containerNewName

docker commit old_container new_image
docker rm old_container
docker run --name new_container -d new_image


docker run -d --label app=webserver --label owner=ahmet nginx

<b><mark>docker export red_panda_container > latest.tar</mark></b><br>

<b><mark>docker export --output="latest.tar" red_panda_container</mark></b><br>

docker container diff containerID

docker container pause red_panda_container

docker container unpause red_panda_container

docker update --restart=on-failure:3 abebf7571666 hopeful_morse

docker update --memory 512m --cpus 1.5 --restart=always my-container

docker update --blkio-weight 500 my-container
Bu komut, konteynerin disk I/O önceliğini orta düzeyde (500) ayarlar.

docker update --cpu-quota 50000 my-container
Bu komut, konteynerin CPU kullanımını %50 ile sınırlar (50000 / 100000).

docker update --cpu-period 100000 my-container
Bu komut, konteynerin CPU zaman dilimini 100 ms olarak sınırlar.

docker update --cpus 2 --memory 1g --pids-limit 100 --restart=always my-container
Bu komut:
Konteynerin en fazla 2 CPU çekirdeği kullanmasını sağlar.
Bellek kullanımını 1 GB ile sınırlar.
Maksimum 100 işlem (PID) oluşturmasına izin verir.
Konteyneri her durumda yeniden başlatır.

docker update --memory-swap 2g my-container
Bu komut, konteynerin bellek + swap kullanımını 2 GB ile sınırlar.

<b><mark>docker update --memory-reservation 512m my-container</mark></b><br>
Bu komut, konteyner için 512 MB bellek rezervasyonunu garanti eder.

docker update --memory 1g my-container
Bu komut, konteynerin en fazla 1 GB bellek kullanmasına izin verir.



docker update --cpuset-cpus 0,1 my-container
Bu komut, konteynerin yalnızca CPU 0 ve 1 üzerinde çalışmasına izin verir.

docker update --cpus 2 my-container
Bu komut, konteynerin en fazla 2 CPU çekirdeği kullanmasına izin verir.

<b><mark>docker update --cpu-rt-runtime 80000 my-container</mark></b><br>
Bu komut, gerçek zamanlı çalışmayı 80 ms ile sınırlar.


docker update --cpu-rt-period 950000 my-container
Bu komut, konteynerin gerçek zamanlı CPU süresini 950 ms olarak ayarlar.

docker update --cpu-shares 512 my-container
CPU önceliği, bir bilgisayar sisteminde çalışan farklı işlemlere (process) 
CPU kaynaklarının nasıl tahsis edileceğini belirleyen bir mekanizmadır. 
Yüksek öncelikli işlemler, CPU'ya daha hızlı erişir ve düşük öncelikli 
işlemlerden daha önce çalıştırılır. Bu, sistemin daha kritik işlemleri 
daha hızlı ve daha verimli bir şekilde tamamlamasına olanak tanır.

Bellek Düğümleri Nedir?
Bellek düğümleri (memory nodes), NUMA (Non-Uniform Memory Access) mimarisine sahip sistemlerde fiziksel belleğin (RAM) gruplandırıldığı birimlerdir. 
NUMA sistemlerinde, CPU ve bellek fiziksel olarak gruplandırılmıştır, ve bu gruplar "düğüm" olarak adlandırılır. 
Her düğüm kendi CPU'larına ve RAM'ine sahiptir.

NUMA ve Bellek Düğümleri
NUMA mimarisi, yüksek performanslı sistemlerde CPU'ların belleğe erişimini hızlandırmak için kullanılır.
Her CPU kendi yerel belleğine (düğüm belleği) daha hızlı erişebilirken, diğer düğümlerdeki belleklere erişim daha yavaş olabilir.

docker update --cpuset-mems 0 my-container
Bu komut, konteynerin yalnızca bellek düğümü 0'ı kullanmasını sağlar.
