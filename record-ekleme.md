<h1 align="center">Domain'e Record Ekleme</h1>

> Aşama 1: Domaninimizin manage panalıne giriyoruz:
>> `Domain list` ==> `Domain Manage` (domainin sağında olur) ==> `Advance DNS`

![image](https://github.com/ruesandora/Ar.io/assets/101149671/beaff9fc-da0b-4d73-b17e-ae2c8535d1e4)

> Aşama 2: `A` Record ekleme:
>> `ADD New Recod` ==> `Record tipi: A` ==> `Host: @` ==> `Value: Sunucunuzn IP'si`. 

![image](https://github.com/ruesandora/Ar.io/assets/101149671/2dcce3a4-dc48-4333-82c6-eb4dc6cafbb8)


> Aşama 3: `TXT` Record ekleme:
>> `ADD New Recod` ==> `Record tipi: TXT` ==> `Host: _acme-challenge` ==> `Value: Size certbot komutunda verilen TXT keyi`.

![image](https://github.com/ruesandora/Ar.io/assets/101149671/89e014e0-5d73-42c0-9501-c691f95b553b)

> Aşama 4: `2. TXT` Record ekleme: (`Not`, ilkini yaptıktan sonra sunucunuda ENTER'e tıklayın size 2.'sini verecek ve `sonra bekleyin`)
>> `ADD New Recod` ==> `Record tipi: TXT` ==> `Host: _acme-challenge` ==> `Value: Size certbot komutunda verilen 2. TXT keyi`.

![image](https://github.com/ruesandora/Ar.io/assets/101149671/fceeab84-cf51-4c4f-98f5-b38097fd138c)

> Aşama 5: `*` Record ekleme
>> `ADD New Recod` ==> `Record tipi: A` ==> `Host: *` ==> `Value: Sunucunuzn IP'si`. 

> GÖRSEL OLMASI GEREKEN SON HALİDİR:

![image](https://github.com/ruesandora/Ar.io/assets/101149671/df74737f-1b7d-4415-9cbc-bbb2ed0ac933)


> Şimdi [buradan](https://dnschecker.org/#TXT/_acme-challenge.ruesandora.xyz) `_acme-challenge.domaininiz.xyz` şeklinde kendi domaininizi aratın.

> Eğer İnternette yayılmaya başladı ve `tik sayınızda yeşiller` arttıysa (Genelde `10-20 DK` beklemeneizi tavsiye ederim) sunucuda `ENTER` diyebilirsiniz.

<h1 align="center">Notlar:</h1>

> `NOT`: Görselde ki gibi `2 TXT kaydınızda tikli` olacak

![image](https://github.com/ruesandora/Ar.io/assets/101149671/cdc2508a-7c52-4241-ac95-3dc3eaf6a875)

> Yukarıda karalamamamın nedeni benim değerlerimi girmeyin diye, yoksa sizde çalışmaz.

> www Record opsiyonel isterseniz eklersiniz görselde belirttim, value sunucunu IP'iniz.

