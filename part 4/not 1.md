uygulamanın paketlenmiş hali bundan container oluşturuz
image registry --> dockerhub,azure container registry

docker image ls
//imajlar listelenir.

docker run kenant42/ornekdocker echo "test"
//kenant42/ornekdocker imajından bir container oluşturur ve bu container içerisinde  echo "test" komutunu çalıştırır.
//ekrana "test" yazar.

docker run 2b464g756H569F0 echo "test"
//idsi belirtilen container içerisinde echo "test" komutunu çalıştırır.


docker image pull kenant42/ornekdocker
//kenant42/ornekdocker imajını çeker.

docker image pull ubuntu

docker image pull gcr.io/google-containers/busybox
docker pull kenant42/ornekdocker:v1
//kenant42/ornekdocker imajının v1 taglı sürümünü çeker.


docker pull ubuntu:20.04
//ubuntu imajının 20.04 versiyonunu çeker.


aynı repo içinde birden fazla image tutulabilir

bir image'a birden fazla tag atılabilir
aynı id'ye birden fazla tag verilebilir<br>


<b><mark>docker run -dit --name=my_container ubuntu bash</mark></b><br>

<b><mark>docker wait my_container</mark></b><br>
//docker wait komutu, belirli bir Docker konteynerinin tamamlanmasını beklemek için kullanılır. <br>
//Bu komut, bir konteynerin çalışmasını bekler ve çıkış durumunu döndürür.<br>






