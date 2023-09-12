<h1 align="center">Ar.io</h1>

### TESTNETE BAŞLAMADAN ÖNCE OKUNMASI GEREKENLER

> [Buradan](https://ar.io/testnet/) sayfayı biraz aşağıya kaydırıp FAQ kısmını okuyun arkadaşlar.

> Testnete katılmak için domain gerekmiyor ama ödül almak için gerekiyor, domainimi [Namecheap](https://www.namecheap.com/)'den aldım.

> `ruesandora.xyz` aldım `0.98$`'a. sizde ucuza bir şey alın katılmak istiyorsanız, Namecheap'ı zaten bilmeyen yoktur.

> `Hosting satın almanıza gerek yok`, bazı firmalar dayatıyor buna gerek yok, ayrıca kullanmadığınız mevcut domain varsa o da olur.

<h1 align="center">Donanım ve İhtiyaçlar</h1>

> dolduracağım burayı

<h1 align="center">Kurulum</h1>

```console
# Güncelleme ve gerekli paketler
sudo apt update -y && sudo apt upgrade -y && sudo apt install -y curl openssh-server docker-compose git certbot nginx sqlite3 build-essential && sudo systemctl enable ssh && curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt-get update -y && sudo apt-get install -y yarn && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash && source ~/.bashrc && sudo ufw allow 22 80 443 && sudo ufw enable

# nvm kurulumu
nvm install 16.15.1 && nvm use 16.15.1

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

<h1 align="center">Gerekli paketler manuel</h1>

```console
# yarnı yükleyelim
curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update -y
sudo apt-get install yarn -y

# nvmi yükleyelim
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc

# nodejs ve toolarımızı yükleyelim.
nvm install 16.15.1
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

# Domain adresinizi yazın tırnakların arasına ve tırnakları kaldırın
GRAPHQL_HOST=arweave.net
GRAPHQL_PORT=443
START_HEIGHT=1000000
ARNS_ROOT_HOST=<domainadresiniz.xyz>

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

> Şimdiki aşamada 1 cüzdana ve `2 tip tokene` ihtiyacımız var, 1. `mainnet` 2. `Test token`

> Ben [ArConnect](https://www.arconnect.io/)'i seçtim ve Discord `testnet-kanalına` yukarıda search ettiğimiz `domainimizi` ve `cüzdan adresimizi` atıyoruz `TEST` ve `MAİN` tokeni için.

```
# tekrardan ar-io-node dizinindeyken .env'in içine girelim.
# Burada en alta AR_IO_WALLET= kısmı ekleyip karşısına cüzdanımızı girelim 
# Sonradan CTRL X Y ENTER ile çıkalım.

# Görselde gösterdim:
```

![image](https://github.com/ruesandora/Ar.io/assets/101149671/9ff234d0-c29f-4f77-bb07-95d5a175f9eb)

```console
# Yukarıda ki görseli gerçekleştirdiysen bunları yap
screen -r ar
sudo docker-compose down
sudo docker-compose up -d --build
sudo docker-compose logs -f --tail=0
```

<h1 align="center">Kontrat kurulumu</h1>

```console
# testnet-contract kurulumu:
git clone https://github.com/ar-io/testnet-contract

# dizine girip key.json'umuzu oluşturalım.
cd testnet-contract
nano key.json
```

> bu `key.json`'unun içine konulacak işlem [burada](https://github.com/ruesandora/Ar.io/blob/main/key.json.md) mevcut.

> `key.json`'u hallettiysek:

```console
# Buradaki paketleri yükleyelim
yarn install
npm install
npm install -g rimraf
npm install arg
sudo apt install ts-node -y
npm install -g ts-node
```

> YUKARIDAKİ PAKETLERİ YÜKLEDİYSEK `tools`'u halledelim:

> `key.json`'dan sonra `tools`'u ayarlamalıyız, [buradan](https://github.com/ruesandora/Ar.io/blob/main/tools.md) yapabilirsiniz.

> `tools`'u ayarladıysak devam:

<h1 align="center">2 tokenide temin ettiyseniz devam edin</h1>

```console
# tokeni aldıktan 15-20 dakika beklemenizi tavsiye ederim, başarlı TX alsanız bile ikisinden birisi gelmemiş olabilir

# toolsu ayarlayıp kaydedip çıktıysanız bu komutu çalıştıralım
yarn ts-node tools/join-network.ts
# Bu komut size TX id: null verirse tokeniniz eksiktir ya testnet ya mainnet. Uzun bir TX verirse başarılı!
```

> soon









