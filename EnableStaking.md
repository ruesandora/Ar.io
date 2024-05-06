## Ar io Delegate stake etkinleştirme (Güncel versiyon)

```
cd ar-io-node 
rm -rf testnet-contract
git clone https://github.com/ar-io/testnet-contract
cd testnet-contract
yarn install
```

içerisine alttaki yazıyı yapıştırın girin
```
nano .env
```
``WALLET_FILE_PATH=/root/ar-io-node/testnet-contract/``

### Sonrasında (Önceden Ar.io Kuranlar yapmıştır, testnet-contract içerisinde key.json dosyanız yoksa bu adımı yapın.)
```
nano key.json 
```

### Nano komutundan sonra alttaki repodan oluşturduğumuz key.json içeriğini doldurucaz rues hoca anlatmış detaylı


https://github.com/ruesandora/Ar.io/blob/main/key.json.md


### Bundan sonra testnet-contract klasöründeyken (eğer değilseniz cd > cd ar-io-node/testnet-contract komutunu gir)
```
yarn update-gateway-settings
```

> Çoğu default olacak direk entere basın sadece Enable or disable auto staking ve delegates stakingi yes yapın
> 
> sonraki soruyu 10
> 
> ondan sonraki soruyu 100 yapın.
> 
> Sonra verdiğiniz bilgileri kontrol etmenizi isteyecek entera basın. Tx id verirse başarılıdır.

## Karşılıklı Stake Yapma Adımı
Tekrar testnet-contract içerisine girelim (cd > cd ar-io-node/testnet-contract)

```
yarn delegate-stake
```
> Enter the target gateway address you want to delegate to > STAKE YAPMAK İSTEDİĞİNİZ CÜZDAN
>
> Enter Stake Quantity (in IO) >  100 EĞER KARŞILIKLI YAPTIGINIZLA MİKTARI DEĞİŞTİRECEKSENİZ BU KISIMDAN DEĞİŞTİRİN
>
> CONFIRM DELEGATION DETAILS? {"target":"tncUYUIOfIib-izqoGbVVO12LiZTjzh6YQYNenD2kH0","qty":100} > (Y/n) BU KISIMDA YES DİYİP TX OLUSMASINI BEKLEYİN VE BİTTİ.

## Karşılıklı Stake yapmak isterseniz cüzdan adresim Telegram @enzifiri 
 <br> ``tncUYUIOfIib-izqoGbVVO12LiZTjzh6YQYNenD2kH0``

