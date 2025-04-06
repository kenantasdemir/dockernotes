
Dockerfile kendine özgü kuralları olan bir dille yazılan
ve bizlerin Docker imajları oluşturmamızı sağlayan dosyalardır.

FROM oluşturulacak imaın hangi imajdan oluşturulacağı burada belirtilir. tanımlanması zorunludur.
Ör: FROM ubuntu:18.04

RUN imaj oluşturulurken shellde bir komut çalıştırmak isterseniz bu komutu kullanmalısınız.
COPY imaj içine dosya ya da klasör kopyalamak için kullanılır.
Ör: COPY /source /user/src/app

USER | gireceğimiz komutları hangi kullanıcı ile çalıştırmasını istiyorsak bu talimat ile onu seçebiliriz. 
Ör: USER poweruser

LABEL | İmaj metadata’sına key=value şeklinde değer çiftleri eklemek için kullanılır. Örneğin team=development şeklinde bir etiket eklenerek bu imajın development ekibinin kullanması için yaratıldığı belirtilebilir.
Ör: LABEL version:1.0.8

EXPOSE portNumber
Bu imajdan oluşturulacak containerların hangi portlar üstünden erişilebileceğini yani hangi portların yayınlanacağını bu talimatla belirtiriz.l

ADD kaynakyol hedefyol
COPY ile aynı işi yapar yani dosya ya da klasör kopyalarsınız.
fakat ADD bunun yanında dosya kaynağının bir url olmasına da izin verir.
ayrıca ADD ile kaynak olarak bir .tar dosyası belirtilirse bu dosya 
imaja .tar olarak sıkıştırılmış haliyle değil de açılarak kopyalanır.

//ADD https://wordpress.org/latest.tar.gz /temp

HEALTHCHECK
bu talimat ile dockera bir containerın hala çalışıp çalışadığını kontrol etmesini söyleyebiliriz.
docker varsayılan olarak container içerisinde çalışan ilk processi izler ve o çalıştığı sürece container çalışmaya devam eder. fakat process çalışşsa bile onun düzgün işlem yapıp yapmadığına bakmaz. Healtcheck ile
buna bakabilme imkanına kavuşuruz.

HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1

WORKDIR | cd xxx komutuyla ile istediğimiz klasöre geçmek yerine bu talimat kullanılarak istediğimiz klasöre geçer ve oradan çalışmaya devam ederiz. 
Ör: WORKDIR /usr/src/app


RUN | İmaj oluşturulurken shell’de bir komut çalıştırmak istersek bu talimat kullanılır. Örneğin apt-get install xxx ile xxx isimli uygulamanın bu imaja yüklenmesi sağlanabilir. 
Ör: RUN apt-get update

CMD 
Bu imajdan container yaratıldığı zaman varsayılan olarak çalıştırmasını istediğiniz komutu bu talimat ile belirtirsiniz.


SHELL | Dockerfile'ın komutları işleyeceği shell'in hangisi olduğunu belirtiriz. Linux için varsayılan shell ["/bin/sh", "-c"],Windows için ["cmd", "/S", "/C"]. Bunları SHELL talimatı ile değiştirebiliriz. 
Ör: SHELL ["powershell", "-command"]

ENTRYPOINT | Bu talimat ile bir containerın çalıştırılabilir bir uygulama gibi ayarlanabilmesini sağlarsınız.
Ör: ENTRYPOINT ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

EXPOSE | Bu imajdan oluşturulacak containerların hangi portlar üstünden erişilebileceğini yani hangi portların yayınlanacağını bu talimatla belirtirsiniz. 
Ör: EXPOSE 80/tcp

VOLUME | Imaj içerisinde volume tanımlanamızı sağlayan talimat. Eğer bu volume host sistemde varsa container bunu kullanır. Yoksa yeni volume oluşturur. 
Ör: VOLUME /myvol

ENV | Imaj içinde environment variable tanımlamak için kullanılır
Ör: ENV TEMP_FOLDER="/temp"

ARG | ARG ile de variable tanımlarsınız. Fakat bu variable sadece imaj oluşturulurken yani build aşamasında kullanılır. Imajın oluşturulmuş halinde bu variable bulunmaz. ENV ile imaj oluşturulduktan sonra da imaj içinde olmasını istediğiniz variable tanımlarsınız, ARG ile sadece oluştururken kullanmanız gereken variable tanımlarsınız.
Ör: ARG VERSION:1.0

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
