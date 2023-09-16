## NOT: EKİP TAVSİYESİ HER ZAMAN 100000 bloktan başlamanızdır, bunuda belirteyim altını çizerek.

### 1- Disk hakkında yapmanız gereken şeyler aslında çok basit.

### 2- Bir kaç yöntem var ama testlerimde en doğru çalışan aşağıda ki anlatım.

##

> Yeni sunucunuza repomda ki normal kurulumu birebir aynı işlemleri gerçekleştiriyorsunuz

> Tek fark kurulum esnasında `.env`'de `1000000` yerine `1250000` yazıyorsunuz bu şekilde kuruyorsunuz
```
GRAPHQL_HOST=arweave.net
GRAPHQL_PORT=443
START_HEIGHT=1250000
ARNS_ROOT_HOST=<domainadresiniz.xyz>
```
##

### Mevcut node'u yapsam peki? Maalesef olmuyor yeni sunucuya taşımak gerekiyor.

### Son olarak eskisinden tek farkı domaininizi arattığınızda biraz geç düşüyor.

##

### Dünden beri yaptığım testler sonucunda bu şekilde çözdüm disk krizini.

![image](https://github.com/ruesandora/Ar.io/assets/101149671/1d0e0ab3-43c4-418a-a57c-e6c244e8568a)

