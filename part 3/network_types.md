
<div style="text-center;">
  <b><mark>Bridge</mark></b>
</div>
<br>
default olan driverdır. network objesi yaratılırken özellikle başka bir driver belirtilmezse bridge driver ile network yaratılır.

Her docker kurulu host üstünde bridge driver ile yaratılmış Bridge adında bir network bulunur ve container 
yaratıldığında aksi belirtilmediği takdirde varsayılan olarak buna bağlanır.
<br>

<center><b><mark>Host</mark></b></center>
<br>
Her sistemde host driver ile yaratılmış Host adında bir network bulunur.
Bu networkte bağlı containerda network izolasyonu olmaz.
Sanki o host üstünde çalışan bir process gibi hostun ağ kaynaklarını kullanır.



<center><b><mark>MacVLAN</mark></b></center>
<br>
Bu driver ile oluşturulan network objeleri sayesinde containerlar fiziksel ağlara kendi mac adreslerine
sahip birer fiziksel ağ adaptörüne sahipmişçesine bağlanabilirler.

<b><mark>None</mark></b>
<br>
Container hiçbir şekilde ağ bağlantısına sahip olmasın istenirse bu driver ile yaratılan networke bağlanır.


<b><mark>Overlay</mark></b>
<br>
Ayrı hostlar üstündeki containerların aynı ağda çalışıyormuş gibi çalışması istendiği zaman Overlay networkler devreye girer.


<b><mark>Kullanıcı Tanımlı Bridge</mark></b>
<br>
Containerlar arası network izolasyonu sağlamak istersek ayrı bridge networkler yaratarak bunu sağlayabiliriz.

Varsayılan dışında ip aralıkları tanımlanabilir.

Kullanıcı tanımlı bridge networke bağlı containerlar birbirleriyle isimler üzerinden haberleşebilir.
DNS çözümlemesi sağlarlar.

Container çalışır durumdayken de kullanıcı tanımlı bridge networklere bağlanıp bağlantıyı kesebilirler.
