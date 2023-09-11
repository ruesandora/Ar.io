# DOMAİNİMİZE RECORD EKLEME 

> Aşama 1: Domaninimizin manage panalıne giriyoruz:
>> `Domain list` ==> `Domain Manage` (domainin sağında olur) ==> `Advance DNS`

![image](https://github.com/ruesandora/Ar.io/assets/101149671/d34cd3a7-c3e3-41f2-b10e-10d34cddf784)

> Aşama 2: `A` Record ekleme:
>> `ADD New Recod` ==> `Record tipi: A` ==> `Host: @` ==> `Value: Sunucunuzn IP'si`. 

![image](https://github.com/ruesandora/Ar.io/assets/101149671/287ac28b-338a-41c5-bff8-dc40eef7eeff)

> Aşama 3: `TXT` Record ekleme:
>> `ADD New Recod` ==> `Record tipi: TXT` ==> `Host: _acme-challenge` ==> `Value: Size certbot komutunda verilen TXT keyi`.

![image](https://github.com/ruesandora/Ar.io/assets/101149671/b93e5d5b-b96e-473f-aeaf-dad2b6f1f6c0)

> Aşama 4: `2. TXT` Record ekleme: (`Not`, ilkini yaptıktan sonra sunucunuda ENTER'e tıklayın size 2.'sini verecek ve `sonra bekleyin`)
>> `ADD New Recod` ==> `Record tipi: TXT` ==> `Host: _acme-challenge` ==> `Value: Size certbot komutunda verilen 2. TXT keyi`.

![image](https://github.com/ruesandora/Ar.io/assets/101149671/b93e5d5b-b96e-473f-aeaf-dad2b6f1f6c0)

> Şimdi [buradan](https://dnschecker.org/#TXT/_acme-challenge.ruesandora.xyz) `_acme-challenge.domaininiz.xyz` şeklinde kendi domaininizi aratın.

> Eğer İnternette yayılmaya başladı ve `tik sayınızda yeşiller` arttıysa (Genelde `10-20 DK` beklemeneizi tavsiye ederim) sunucuda `ENTER` diyebilirsiniz.

> `NOT`: Görselde ki gibi `2 TXT kaydınızda tikli` olacak

![image](https://github.com/ruesandora/Ar.io/assets/101149671/50866698-bfd1-4427-a627-24b49151d3ee)

> Yukarıda karalamamamın nedeni benim değerlerimi girmeyin diye, yoksa sizde çalışmaz.

> www Record opsiyonel isterseniz eklersiniz görselde belirttim, value sunucunu IP'iniz.

