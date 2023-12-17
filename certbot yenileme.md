ar-io kurulu sunucumaza giriş yaptıktan sonra

```console
cd ar-io-node
```
certbot sertifika tarihimizi kontrol edelim:
```console
sudo certbot certificates
```

cerbot sertifika süremiz dolmaya yakınsa yenileyelim: 
```console
sudo certbot certonly --manual --preferred-challenges dns --email youemail.com -d youdomain.com -d '*.youdomain.com'
```

Kurulumda yapmıştık bu işlemi. Certbot komutunda verilen TXT keyi record ekleyelim. [Domain'e Record Ekleme](https://github.com/ruesandora/Ar.io/blob/main/record-ekleme.md) Aşama 3- 4 ü tekrarlayın.


nginx resetleyelim: 
```console
sudo service nginx restart
```

cerbot sertifika tekrar süremizi kontrol edelim: 
```console
sudo certbot certificates
```
