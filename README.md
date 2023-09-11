# Ar.io

> TESTNETE BAŞLAMADAN ÖNCE, [Buradan](https://ar.io/testnet/) sayfayı biraz aşağıya kaydırıp FAQ kısmını okuyun arkadaşlar.

> Testnete katılmak için domain gerekmiyor ama ödül almak için gerekiyor, domainimi [Namecheap](https://www.namecheap.com/)'den aldım.

> ruesandora.xyz aldım 0.98$'a. sizde ucuza bir şey alın katılmak istiyorsanız, Namecheap'ı zaten bilmeyen yoktur.

# Kurulum

# Güncelleme ve gerekli paketler
sudo apt update -y && sudo apt upgrade -y && sudo apt install -y curl openssh-server docker-compose git certbot nginx sqlite3 build-essential && sudo systemctl enable ssh && curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && sudo apt-get update -y && sudo apt-get install -y yarn && curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash && source ~/.bashrc && sudo ufw allow 22 80 443 && sudo ufw enable

# nvm kurulumu
nvm install 16.15.1 && nvm use 16.15.1

# gerekli paketler ve portlar
sudo apt update -y && sudo apt upgrade -y

sudo ufw enable
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443

# ngix ve docker
sudo apt install nginx -y
sudo apt install git -y
sudo docker run hello-world

# cerbot'uda yükleyelim
sudo apt install certbot -y
sudo apt install openssh-server -y

# Birde manuel yükleyelim;

# yarn'ı yükleyelim
curl -sSL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update -y
sudo apt-get install yarn -y

# nvm'i yükleyelim
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source ~/.bashrc

# nodejs ve toolarımızı yükleyelim.
nvm install 16.15.1
sudo apt install build-essential
sudo apt install sqlite3 -y

# Node'u kuralım;

git clone https://github.com/ar-io/ar-io-node
cd ar-io-node





