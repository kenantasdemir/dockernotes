----------------------------------------------------------------------------------------

<b><mark>docker container run -d --memory=100m kenant42/ornekdocker</mark></b>
<br>
//kenant42/ornekdocker imajından bir container oluşturur. bu container 100MB bellek kullanımı kısıtı koyar.

<br>
<b><mark>docker container run -d --memory=100m --memory-swap=200m kenant42/ornekdocker</mark></b>
<br>

//--memory-swap=200m seçeneği kullanılarak konteynerın toplam bellek kullanımını en fazla 200 MB olarak sınırlandırır.

----------------------------------------------------------------------------------------

1.yöntem
<b><mark>docker container run -d --cpus="1.5" kenant42/ornekdocker</mark></b>
<br>

//"kenant42/ornekdocker" adlı bir Docker imajından yeni bir konteyner oluşturur ve 
//konteynerın maksimum CPU kaynağı kullanımını 1.5 çekirdek olarak sınırlandırır.

<br>

2.yöntem
<b><mark>docker container run -d --cpus="1.5" --cpuset-cpus="0,3" kenant42/ornekdocker</mark></b>
//--cpuset-cpus seçeneği, konteynerın hangi çekirdeklerin kullanılacağını belirtir. 
//Bu örnekte, --cpuset-cpus="0,3" seçeneği kullanılarak konteynerın sadece 0 ve 3 numaralı çekirdekleri kullanması sağlanır.

----------------------------------------------------------------------------------------
