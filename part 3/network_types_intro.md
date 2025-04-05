volume driverları volume yaratıp kullanmanızı sağlar

Docker arka planda onlarca farklı servisten oluşması ve altyapısal olarak karmaşık
olmasına rağmen kullanımda yıllardır alıştığımız ve bildiğimizin dışında bir sistem
sunmaz.

Docker Network Driver Türleri
 Bridge
 Host
 Macvlan
 None
 Overlay



<b><mark>docker network ls</mark></b>
</br>
bridge hem bu driverın adı hemde dockerın default olarak oluşturduğu ilk networkede ayn isim verilir
yeni bir container oluşturulurken hangi networke bağlı olacağını belirtmezseniz default olarak bridge.
host networküne bağlayacağınız containerlar sanki bu makine üstüne çalışan bir process gibi davranır

</br>
<b><mark>docker network inspect bridge</mark></b>
//bridge adlı network objesinin özellikleri görüntülendi.
</br>


<b><mark>docker image ls</mark></b>
//tüm imajlar listelenir.
</br>

<b><mark>docker image inspect kenant42/ornekdocker</mark></b>
</br>
//kenant42/ornekdocker adlı imajın özellikleri görüntülendi.

</br>

<b><mark>docker container inspect fasd4fasd45</mark></b>
</br>
//fasd4fasd45 id değerine sahip containerın özelliklerini görüntüler.
</br>

<b><mark>docker network inspect bridge</mark></b>
</br>



docker container run -d kenant42/ornekdocker
</br>
//kenant42/ornekdocker imajından container oluşturur. bu container bridge networküne bağlıdır.
// -d seçeneği containerın detache modda çalışacağını belirtir.


docker exec -it fasd4fasd45 sh
//fasd4fasd45 id değerine sahip container içerisinde shell açar.

ifconfig
// ip = 172.17.0.2

docker engine kurulduğunda bridge host ve none 3 network objesi oluşturulur.
bridge o makine üstünde docker0 adlı sanal network interface oluşturur ona da 172.17.0.1/16 ip adresini verir.
docker bu containera 172.17.0.1/16 networkünden sıradaki boş ip adresini verir
default gateway olarak da docker0 interfaceinin adresini verir


<b><mark>docker container run -it --name deneme kenant42/ornekdocker sh</mark></b>
</br>


ping 172.17.0.2
//bağlantıyı kestiğimiz containerla hala haberleşebiliyoruz

<b><mark>docker container run -it --name deneme kenant42/ornekdocker sh</b></mark>
</br>
//exit ile yukarıda açtığımız shellden çıkarız.



-------------------------------------

<div align="center">
 hosta bağlı containerlar hiçbir network izolasyonu yoktur çalıştıkları networkün ağ altyapısını kullanırlar

</br>
<b><mark>docker container run -it --name deneme1 --net host kenant42/ornekdocker sh</mark></b>
<br>

</div>

-------------------------------------

docker container run -it --name denemecontainer --net none kenant42/ornekdocker sh
//kenant42/ornekdocker imajından denemecontainer adlı container oluşturur. none adlı networke bağlar.
//ardından sh parametresi sayesinde bu container içinde shell açar.


//none network objesine sahip containerlar networke bağlanamaz

Default bridgelar arasında DNS hizmeti yoktur.














