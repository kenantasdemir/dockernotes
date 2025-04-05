<b>mark>docker container run -it --env VAR1=deneme1 --env VAR2=deneme2 ubuntu bash</mark><b>
</br>
//ubunu imajından bir container oluşturur ve bu container interaktif olarak bash açar.
//bu container içinde VAR1 ve VAR2 olmak üzere 2 adet ortam değişkeni oluşturur.

printenv
//ortam değişkenlerinin hepsi görüntülenir.

echo $VAR1
//VAR1 adlı ortam değişkeni bastırıldı.

<b><mark>docker container run -it --env TEMP ubuntu bash  </mark></b>
</br>
//bir container olşturur. bu containera interaktif olarak bash açar. TEMP adlı bir ortam deişkeni ayarlar. 


<b><mark> docker container run -it --env-file .\env.list ubuntu bash</mark></b>
</br>
//--env-file seçeneği ile ortam değişkenlerini dosya içinden alır


<b><mark>docker container run --env veritabani=testveritabani.pizzadukkani.com kenant42/ornekdocker </mark></b>

</br>

<b><mark>docker container run --env veritabani=prod.pizzadukkani.com kenant42/ornekdocker </mark></b>

