<h1 align="center">Ar.io</h1>

### TESTNETE BAŞLAMADAN ÖNCE OKUNMASI GEREKENLER

> YAZMASI ve ANLATMASI günler sürdü/sürecek sizin okumanız maks 15 dakika `tüm notlarımı okuyunuz lütfen`. 

> Hocam şunla şu yan yana olur mu gibi sorular hep yarım kaldığı için bu tarz soruları sormayın cevaplamayacağım.

> Şu anda aktif 247 Gateway bulunuyor. Eskiden katılmak için 50k tARIO olan alt limit 10k tARIO'ya düşürüldü. Gateway olmak istiyorsanız cüzdanınızda bu miktarın bulunması şart.

> Devam etmek isteyenler öncelikle tARIO temin etmeli. Bunun için de cüzdanınızdaki AR tokenleri [buradan](https://aox.xyz/#/beta) AO'ya geçirip [Permaswap](https://www.permaswap.network/#/ao/WAR-TARIO?tab=swap) üzerinden alabilirsiniz. Bridge işlemi bazen uzun sürebiliyor.

> Testnete katılmak için domain gerekmiyor ama ödül almak için gerekiyor, domainimi [Namecheap](https://www.namecheap.com/)'den aldım.

> `ruesandora.xyz` aldım `0.98$`'a. sizde ucuza bir şey alın katılmak istiyorsanız, Namecheap'ı zaten bilmeyen yoktur.

> `Hosting` satın almanıza `gerek yok`, bazı firmalar dayatıyor buna gerek yok, ayrıca kullanmadığınız mevcut domain varsa o da olur.

> TOPLULUK KANALLARI: [Sohbet Kanalımız](https://t.me/RuesChat) - [Duyurular ve Gelişmeler](https://t.me/RuesAnnouncement) - [Ar.io Discord](https://discord.com/invite/HGG52EtTc2)

<h1 align="center">Donanım ve İhtiyaçlar</h1>

> Güzel bir internete ihtiyacınız var Contabo sorun çıkarır TR sunucusu asla, [Hetzner](https://hetzner.cloud/?ref=gIFAhUnYYjD3) kullandım, şaşmaz.

```
> Sadece AR.IO varsa sunucunuzun diski minimum 80 GB olsun.
> 80 GB SSD'nin getirdiği CPU ve RAM yeterli. (Genel firamlar için, kıytırık firmaları bilmiyorum)
```

<h1 align="center">Kurulum</h1>

```console
# Güncelleme ve gerekli paketler
sudo apt update -y && sudo apt upgrade -y && sudo apt install -y curl openssh-server docker-compose git certbot nginx sqlite3 build-essential && sudo systemctl enable ssh && curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt-get update -y && sudo apt-get install -y yarn && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash && source ~/.bashrc

# nvm kurulumu
nvm install 20.11.1 && nvm use 20.11.1

# gerekli paketler ve portlar
sudo apt update -y && sudo apt upgrade -y

# y diyip enterleyin enable komutunda.
sudo ufw enable
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443

# ngix ve docker
sudo apt install nginx -y
sudo apt install git -y
sudo docker run hello-world

# cerbotuda yükleyelim
sudo apt install certbot -y
sudo apt install openssh-server -y
```

<h1 align="center">Gerekli paketler Güncelleme</h1>

```console
# yarnı yükleyelim
curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor -o /usr/share/keyrings/yarn-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/yarn-archive-keyring.gpg] https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list > /dev/null
sudo apt-get update -y
sudo apt-get install yarn -y

# nvmi yükleyelim
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc

# nodejs ve toolarımızı yükleyelim.
nvm install 20.11.1
sudo apt install build-essential
sudo apt install sqlite3 -y
```

<h1 align="center">ar-io'yu kuralım</h1>

```console
# repoyu klonlayalım
git clone https://github.com/ar-io/ar-io-node
cd ar-io-node

# içine girelim
nano .env
# İsterseniz 2(Observer - Owner), isterseniz tek cüzdan kullanabilirsiniz ben tek cüzdan kullanıyorum.
# Arconnect kullanıyorsanız generate butonun basıp ikinci cüzdanınızı kurabilirsiniz.
# Domain adresinizi ve cüzdan adreslerinizi yazın tırnakların arasına ve tırnakları kaldırın

GRAPHQL_HOST=arweave.net
GRAPHQL_PORT=443
START_HEIGHT=1000000
RUN_OBSERVER=true
ARNS_ROOT_HOST=<domain-adresiniz.xyz>
AR_IO_WALLET=<Cüzdan adresiniz>
OBSERVER_WALLET=<Tek cüzdan kullanıyorsanız üsttekiyle aynı adres>

# nodeumuzu calıstıralım:
screen -S ar
sudo docker-compose up -d --build
sudo docker-compose logs -f --tail=0

# ipimizi teyit edelim ve ping atalım
curl ipinfo.io/ip
ip addr show | grep -w inet | awk '{print $2}' | awk -F'/' '{print $1}'
```

<h1 align="center">ÇOKOMELLİ BURASI!</h1>

```console
# CERTBOTTA YAPACAĞIMIZ BU İŞLEM EN ÖNEMLİ KISIM
# Tırnakların arasını doldurup tırnakları kaldırın
sudo certbot certonly --manual --preferred-challenges dns --email <mailAdresiniz@gmail.com> -d <domainadresiniz.xyz> -d '*.<domainadresiniz.xyz>'
```

> Bize bu kommuttan sonra bir kaç kez `Agree` , `Yes` diyecek bunları geçiyoruz `AMA`, 
>> Bunları geçtikten sonra `"Please deploy a DNS TXT record"` kısmında duruyoruz.

> Açıklamada bize verdiği `_acme-challenge`'ı ve `private key`'e benzeyen `TXT keyimizi` Record ekleyeceğiz, peki ya nasıl yaparız?

![image](https://github.com/ruesandora/Ar.io/assets/101149671/7916af9f-dcb8-4e1d-b6b7-78e2816eed17)


> [Buradan](https://github.com/ruesandora/Ar.io/blob/main/record-ekleme.md) Recordlarınızı ekleyebilirisiniz. TEK TEK GİDİN OKUYUN PLS

> Yaptıktan sonra aşağıdan devam:

```console
# Şimdi bu klasöre girelim ve içinde ki her şeyi CTRL + K ile silelim.
sudo nano /etc/nginx/sites-available/default
```

> İçine bu kodu yapıştıralım `AMA` yapıştırmadan önce tam `6 yerde` ki tırnakların içini `doldurup` tırnakları kaldırın.

```console
# Force redirects from HTTP to HTTPS
server {
    listen 80;
    listen [::]:80;
    server_name <domainin> *.<domainin>;

    location / {
        return 301 https://$host$request_uri;
    }
}

# Forward traffic to your node and provide SSL certificates
server {
    listen 443 ssl;
    listen [::]:443 ssl;
    server_name <domainin> *.<domainin>;

    ssl_certificate /etc/letsencrypt/live/<domainin>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domainin>/privkey.pem;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
    }
}
```
``` console
# Daha sonra nginx konfigrasyonu ayarlayalım ve resetleyelim:
sudo nginx -t
sudo service nginx restart
```

> Domaininizi internette search edince şöyle bir çıktı alırsınız


![image](https://github.com/ruesandora/Ar.io/assets/101149671/90b8bc7f-554c-470d-8728-f212e6d1a27b)

<h1 align="center">İnternette gözüktüysek devam edelim</h1>

```console
# Yukarıda ki görseli gerçekleştirdiysen bunları yap
screen -r ar
sudo docker-compose down
sudo docker-compose up -d --build
sudo docker-compose logs -f --tail=0
```

<h1 align="center">Cüzdan kurulumu</h1>

```console
# NOT: 2 CÜZDAN KULLANANLAR OBSERVER WALLET İÇİN DE AYNI İŞLEMİ YAPMALI
cd /ar-io-node/wallets

# dizine girip cüzdanadresi.json umuzu oluşturalım.

nano cüzdanadresi.json
```

> bu `cüzdanadresi.json`'unun içine konulacak işlem [burada](https://github.com/ruesandora/Ar.io/blob/main/cuzdanadresi.json.md) mevcut.

> `cüzdanadresi.json`'u hallettiysek:

```console
# Son kez kapatıp açıyoruz ve loglarımıza bakıyoruz. Arada girip loglarınızı kontrol edebilirsiniz.
sudo docker-compose down -v
sudo docker-compose up -d --build
screen -r ar
sudo docker-compose logs -f --tail=0
ctrl A+D

# Observer logları için bir screen açalım
screen -S observer
sudo docker-compose logs -f observer
ctrl A+D
```

> YUKARIYI HALLEDİNCE [siteye](https://network-portal.app) geçelim:

> Cüzdan bağlayıp soldan Gateways'e geçiyoruz. My Gateway kısmında bir eksik varsa (Observer-Owner wallet) .env dosyasındaki aynı bilgileri girin.

> Otomatik stake açmak istiyorsanız Reward Auto Stake'i enabled yapabilirsiniz. Manuel stake etmenize gerek kalmaz.

> https://domainAdresiniz/ar-io/healthcheck kısmını `düzenleyin`, `Search` edin ve `Uptime` her `F5` yaptığınızda artması gerekiyor.

> https://domainAdresiniz/ar-io/observer/info kısmında cüzdan adresiniz görünmeli. `INVALID` yazısı görüyorsanız `cüzdanadresiniz.json` dosyasında bir hata yapmışsınız demektir.

> Son olarak `My Gateway` kısmında sağ üstte `Observe` seçeneğine basıp kontrol edebilirsiniz. Hepsi `PASSED` ise tebrikler, rica ederim.

<h1 align="center">Güncelleme Kodları</h1>

```console
# Güncelleme geldiğinde kodları sırasıyla kullanın
cd ar-io-node
sudo docker-compose down -v
git checkout main
git pull  
sudo docker-compose up -d --build
screen -r ar
sudo docker-compose logs -f --tail=0
ctrl A+D
screen -r observer
sudo docker-compose logs -f observer
ctrl A+D
```
<h1 align="center">Disk Temizleme</h1>

```console
# df -h ile diskin doluluk durumuna bakın. Dolmaya yakınsa:
cd ar-io-node
sudo docker-compose down -v
sudo docker system prune -a
rm -rf /root/ar-io-node/data/headers/partial-blocks
rm -rf /root/ar-io-node/data/headers/partial-txs
rm -rf /root/ar-io-node/data/redis
rm -rf /root/ar-io-node/data/contiguous
rm -rf /root/ar-io-node/data/sqlite
sudo docker-compose up -d --build
# Tekrar screenleri açıp logları kontrol edebilirsiniz.
```
