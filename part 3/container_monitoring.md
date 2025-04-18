docker container run -d --name appbir kenant42/app1<br>
//kenant42/app1 imajından appbir adlı container oluşturur. bu container detach olarak çalışır.<br>
docker logs appbir
//appbir adlı containerın loglarını görüntüler.

docker stop $(docker ps -q)
//çalışan tüm containerları durdurur.

docker container run -d --name con1 -p 80:80 nginx
</br>
docker ps

docker logs containerName
</br>
docker exec -it con1 sh
</br>


docker exec -it con1 sh
//con1 adlı containerda interaktif şekilde shell bağlantısı yapıldı.
cd /var/log/nginx
ls
access.log error.log
nginx daemonı stdout ve stderr çıkışlarına yazmaz
nginx erişimleri access.log dosyasına hataları error.log dosyasına yazar



###########################################################################

docker logs con1
</br>
//con1 adlı containerın loglarını görüntüler

docker logs --help
</br>
//docker logs komutu hakkında yardım görüntüler.

docker container run -d --name con1 -p 80:80 nginx
</br>
docker logs con1/containerID
</br>

//container silinene kadar bu loglara erişilebilir
##
<mark>docker logs --details con1</mark>
</br>
//con1 adlı containerın detaylı loglarını görüntüler.

<b><mark>docker logs -t con1</mark></b>
</br>
// "con1" adlı bir Docker konteynerının log dosyalarını görüntülemek için kullanılır. 
//Bu komut, konteynerın log dosyalarını sırayla gösterirken, her bir log satırının önünde zaman damgası (timestamp) ekler.



docker logs --until 1652061353 con1
</br>
//con1 adlı container için 1652061353 ile belirtilen timestamp değerine kadar olan logları görüntüler.

docker logs --since timeStamp1 con1
</br>
//con1 adlı containerın 1652061353 ile belirtilen timestamp değerinden itibaren olan logları görüntüler.



docker logs --tail 3 con1
</br>
//con1 adlı containerın loglarından son 3 logu görüntüler.


docker logs -f con1
</br>
//"con1" adlı bir Docker konteynerının log dosyalarını takip etmek için kullanılır. 
//Bu komut, log dosyalarını sürekli olarak takip eder ve yeni log girdileri eklenir eklenmez gösterir.


docker container run --log-driver splunk nginx
</br>
//"splunk" adlı bir log yönetim sistemi kullanarak "nginx" adlı bir Docker imajından yeni bir konteyner oluşturur.

//--log-driver seçeneği, Docker tarafından sağlanan log yönetim sistemlerinden birini belirlemek için kullanılır. 
//Bu seçenek, Docker konteynerının log dosyalarının nereye gönderileceğini belirler. 
//Bu örnekte, "splunk" log yönetim sistemi kullanılarak log dosyaları yönetilir.

###########################################################################333333

<b><mark>docker top con1</mark></b>
</br>
//docker top komut containerın içine girmeye gerek kalmadan container içindeki processleri görmemizi sağlar
//bu örnek con1 adlı containerın içindeki processler görüntülendi.

<b><mark>docker stats</mark></b>
</br>
//sistemde çalışan containerların kullandığı ram ve cpu, network i/o gibi bilgilerini verir

<b><mark>docker stats con1</mark></b>
<br/>
//con1 adlı containerın kullandığı ram ve cpu, network i/o gibi bilgilerini verir






























