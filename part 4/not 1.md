uygulamanın paketlenmiş hali bundan container oluşturuz
image registry --> dockerhub,azure container registry

<b><mark>docker image ls</mark></b><br>
//imajlar listelenir.

<b><mark>docker run kenant42/ornekdocker echo "test"</mark></b><br>
//kenant42/ornekdocker imajından bir container oluşturur ve bu container içerisinde  echo "test" komutunu çalıştırır.<br>
//ekrana "test" yazar.

<b><mark>docker run 2b464g756H569F0 echo "test"</mark></b><br>
//idsi belirtilen container içerisinde echo "test" komutunu çalıştırır.


<b><mark>docker image pull kenant42/ornekdocker</mark></b><br>
//kenant42/ornekdocker imajını çeker.

<b><mark>docker image pull ubuntu</mark></b><br>

<b><mark>docker image pull gcr.io/google-containers/busybox</mark></b><br>
<b><mark>docker pull kenant42/ornekdocker:v1</mark></b><br>
//kenant42/ornekdocker imajının v1 taglı sürümünü çeker.


<b><mark>docker pull ubuntu:20.04</mark></b><br>
//ubuntu imajının 20.04 versiyonunu çeker.


aynı repo içinde birden fazla image tutulabilir

bir image'a birden fazla tag atılabilir
aynı id'ye birden fazla tag verilebilir<br>


<b><mark>docker run -dit --name=my_container ubuntu bash</mark></b><br>

<b><mark>docker wait my_container</mark></b><br>
//docker wait komutu, belirli bir Docker konteynerinin tamamlanmasını beklemek için kullanılır. <br>
//Bu komut, bir konteynerin çalışmasını bekler ve çıkış durumunu döndürür.<br>






