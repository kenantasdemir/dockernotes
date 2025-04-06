
Dockerfile kendine özgü kuralları olan bir dille yazılan
ve bizlerin Docker imajları oluşturmamızı sağlayan dosyalardır.

<b><mark>FROM</mark></b> oluşturulacak imaın hangi imajdan oluşturulacağı burada belirtilir. tanımlanması zorunludur.<br>
Ör: FROM ubuntu:18.04<br>

<b><mark>RUN</mark></b> imaj oluşturulurken shellde bir komut çalıştırmak isterseniz bu komutu kullanmalısınız.<br>
COPY imaj içine dosya ya da klasör kopyalamak için kullanılır.<br>
Ör: COPY /source /user/src/app<br>

<b><mark>USER</mark></b> | gireceğimiz komutları hangi kullanıcı ile çalıştırmasını istiyorsak bu talimat ile onu seçebiliriz. <br>
Ör: USER poweruser<br>

<b><mark>LABEL</mark></b> | İmaj metadata’sına key=value şeklinde değer çiftleri eklemek için kullanılır. Örneğin team=development şeklinde bir etiket eklenerek bu imajın development ekibinin kullanması için yaratıldığı belirtilebilir.<br>
Ör: LABEL version:1.0.8 <br>

<b><mark>EXPOSE</mark></b> portNumber
Bu imajdan oluşturulacak containerların hangi portlar üstünden erişilebileceğini yani hangi portların yayınlanacağını bu talimatla belirtiriz.<br>

<b><mark>ADD</mark></b> kaynakyol hedefyol<br>
COPY ile aynı işi yapar yani dosya ya da klasör kopyalarsınız.
fakat ADD bunun yanında dosya kaynağının bir url olmasına da izin verir.
ayrıca ADD ile kaynak olarak bir .tar dosyası belirtilirse bu dosya 
imaja .tar olarak sıkıştırılmış haliyle değil de açılarak kopyalanır.

//ADD https://wordpress.org/latest.tar.gz /temp

<b><mark>HEALTHCHECK</mark></b><br>
bu talimat ile dockera bir containerın hala çalışıp çalışadığını kontrol etmesini söyleyebiliriz.
docker varsayılan olarak container içerisinde çalışan ilk processi izler ve o çalıştığı sürece container çalışmaya devam eder. fakat process çalışşsa bile onun düzgün işlem yapıp yapmadığına bakmaz. Healtcheck ile
buna bakabilme imkanına kavuşuruz.

<b><mark>HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1</mark></b><br>

<b><mark>WORKDIR</mark></b> | cd xxx komutuyla ile istediğimiz klasöre geçmek yerine bu talimat kullanılarak istediğimiz klasöre geçer ve oradan çalışmaya devam ederiz. <br>
Ör: WORKDIR /usr/src/app<br>


<b><mark>RUN</mark></b> | İmaj oluşturulurken shell’de bir komut çalıştırmak istersek bu talimat kullanılır. Örneğin apt-get install xxx ile xxx isimli uygulamanın bu imaja yüklenmesi sağlanabilir.  <br>
Ör: RUN apt-get update<br>

<b><mark>CMD</mark></b><br> 
Bu imajdan container yaratıldığı zaman varsayılan olarak çalıştırmasını istediğiniz komutu bu talimat ile belirtirsiniz. <br>


<b><mark>SHELL</mark></b> | Dockerfile'ın komutları işleyeceği shell'in hangisi olduğunu belirtiriz. Linux için varsayılan shell ["/bin/sh", "-c"],Windows için ["cmd", "/S", "/C"]. Bunları SHELL talimatı ile değiştirebiliriz. <br>
Ör: SHELL ["powershell", "-command"]<br>

<b><mark>ENTRYPOINT</mark></b> | Bu talimat ile bir containerın çalıştırılabilir bir uygulama gibi ayarlanabilmesini sağlarsınız. <br>
Ör: ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]<br>

<b><mark>EXPOSE</mark></b> | Bu imajdan oluşturulacak containerların hangi portlar üstünden erişilebileceğini yani hangi portların yayınlanacağını bu talimatla belirtirsiniz. <br>
Ör: EXPOSE 80/tcp <br>

<b><mark>VOLUME</mark></b> | Imaj içerisinde volume tanımlanamızı sağlayan talimat. Eğer bu volume host sistemde varsa container bunu kullanır. Yoksa yeni volume oluşturur. <br>
Ör: VOLUME /myvol<br>

<b><mark>ENV</mark></b> | Imaj içinde environment variable tanımlamak için kullanılır <br>
Ör: ENV TEMP_FOLDER="/temp"<br>

<b><mark>ARG</mark></b> | ARG ile de variable tanımlarsınız. Fakat bu variable sadece imaj oluşturulurken yani build aşamasında kullanılır. Imajın oluşturulmuş halinde bu variable bulunmaz. ENV ile imaj oluşturulduktan sonra da imaj içinde olmasını istediğiniz variable tanımlarsınız, ARG ile sadece oluştururken kullanmanız gereken variable tanımlarsınız.<br>
Ör: ARG VERSION:1.0<br>

Exec Form
CMD ["java","uygulama"]

Shell Form
CMD java uygulama

Eğer komut shell formunda girilirse docker bu imajdan container yaratıldığı zaman bu komutu varsayılan shelli çalıştırarak onun içerisine girer. 
Bu neden containerda çalışan 1.process yani pid1 su shell processi olur.

Eğer komut exec formunda girildiyse docker herhangi bir shell çalıştırmaz ve komut direkt process olarak çalışır ve containerın pid1'i o process olur.

Exec formunda çalıştırılan komutlar herhangi bir shell processi çalışmadığı için Environment variable gibi bazı değerlere erişemez. 

Eğer ENTRYPOINT ve CMD birlikte kullanılacaksa Exec form kullanılmalıdır. shell formu kullanıldığında CMD'deki komutlar ENTRYPOINTE parametre olarak aktarılmaz.

Dockerfile isimli dosya oluştur(uzantı yok)

---

ENTRYPOINT RUNTIME'DA DEĞİŞTİRİLEMEZ!!!! 
CMD ILE GIRILEN KOMUT RUNTIME'DA DEGISTIRILEBILIR!!!!!
her docker containerında ya entrypoint ya da cmd olmalıdır.
her ikisi de olursa cmd komutu entrypointe parametre olarak eklenir
ENTRYPOINT ONCE GELIR!!!!!!!

---

1: Her Docker imajında bir CMD veya ENTRYPOINT talimatı
                  bulunmąlıdır
2: Her iki talimat da bu imajdan container yaratıldığında çalıştırılacak
           uygulamayı belirtmemizi sağlar
3: ENTRYPOINT ile girilen komut runtime'da yani container
çalıştırılırken değiştirilemez. CMD ile yazılan ise runtime'da
                  değiştirilebilir
4. ENTRYPOINT ve CMD aynı anda kullanılırsa CMD'de yazılan
ENTRYPOINT talimatında yazılana parametre olarak eklenir.

---

:x: EXEC FORMDA HERHANGI BIR SHELL PROCESS ÇALIŞMAZ!!!!!


---

EXEC FORMUNDA DIREKT OLARAK PROCESS CALISTIRABILIRSINIZ
CMD ["executable", "param1", "param2", ...]


SHELL FORMUNDA ISE SHELL ACIP ONU CALISTIRABILIRSINIZ
CMD command param1 param2 //SHELL FORM YAPISI



entrypoint ile cmd'yi aynı anda kullanıyorsanız shell kullanılamaz
ENTRYPOINT ILE CMD AYNI ANDA KULLANILACAKSA EXEC FORM KULLAN!!
Eğer böyle Bir senaryoda shell kullanılırsa cmd'deki komutlar entrypointe 
parametre olarak aktarılmaz.

---

Dockerfile talimatlarında değişebilecek şeyler en altta bulunması gerekirken 
değişmeyeceği öngörülen talimatlar üstte yer almalıdır.  
Çünkü docker talimatları uygularken önbellek kullanır. 
Değişiklik olmayan katmanda önbellek kullanırken 
değişiklik olan katmanı yeniden oluştutur.




EXEC FORM CMD ["java","uygulamaismi"]
SHELL FORM cmd java uygulama

Eğer kommt Shell formunda girilirse docker bu imajdan container yaratıldığı zaman 
bu komutu varsayılan shelli çalıştırarak onun içerisinde girer. 
Bu nedenle containerda çalışan 1.process yani pid1 bu shell processi olur.

Eğer kommt Executive formunda girildiyse docker herhangi bir shell çalıştırmaz ve 
komut direkt process olarak çalışır ve containerın pid1'i o process olur.

Exec formunda çalıştırılan komutlar ortam değişkenlerine erişemez.
 




