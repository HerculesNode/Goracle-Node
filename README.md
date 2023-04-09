# Merhaba Goracle Node Kurulum rehberi

 ## 🟢 Linkler:

 * [Hercules Telegram](https://t.me/HerculesNode)
 * [Hercules Twitter](https://twitter.com/Hercules4413)

 
 
  ## 1- Pera Wallet kurulumu

 * ilk yapılması gereken Algo üzerinde [PERA WALLET](https://web.perawallet.app/) hesabı açmanız gerekiyor. Daha sonra Setting kısmından ağı Testnete geçirin. 

![image](https://user-images.githubusercontent.com/101635385/230795905-2a576484-ab36-437e-8b6e-5acc79fe78d8.png)

  ## 2- Algo faucet

* Açmış olduğunuz Pera wallete Algo token almanız lazım aşağıdaki linkten alabildiğiniz kadar alın. 

[Faucet](https://bank.testnet.algorand.network/)

  ## 3- Goracle şifre 

* Goracle  [Discord](https://discord.gg/M7wSArcGDX) kanalına girip bir Ticket bilet oluşturun ve Node kurulumu için şifre isteyin. Size bir şifre verecek bu şifreyi saklayın ilerki adımlarda lazım olacak.

![image](https://user-images.githubusercontent.com/101635385/230796886-225cf1ed-b640-42d6-bc1c-cce0250d52e5.png)

  ## 4- Algo Node kurulumu

* Goracle Nodemizi çalıştırabilmek için Algo Testnet node kurulumu yapmamız gerekiyor adımları tek tek uygulayın ve senkronize olmasını bekleyin. Algo node kurulumu bitmeden Goracle node kurmayın. 

```shell
sudo apt-get update
```
```shell
sudo apt-get install -y gnupg2 curl software-properties-common
```
```shell
curl -o - https://releases.algorand.com/key.pub | sudo tee /etc/apt/trusted.gpg.d/algorand.asc
```
```shell
sudo add-apt-repository "deb [arch=amd64] https://releases.algorand.com/deb/ stable main"
```
```shell
sudo apt-get update
```
```shell
sudo apt-get install -y algorand-devtools
```
```shell
algod -v
```

* bu şekilde bir çıktı almanız gerekiyor. <br>

![image](https://user-images.githubusercontent.com/101635385/230796202-0efb78a4-5a77-4e07-9f89-27118a7df4df.png)

<hr>

* Node 8080 portunu kullanıyor eğer başka bir node kuruluysa shardeum gibi çakışacaktır bu yüzden port değiştirmeniz gerekiyor. Eğer port değiştirmeniz gerekiyorsa aşağıdaki adımı uygulayın. değiştirmeyecekseniz yapmanıza gerek yok.

```shell
cd /var/lib/algorand
```
```shell
cp config.json.example config.json
```

```shell
nano config.json
```

config dosyanızı açtığınızda aşağıdaki resimdeki gibi EndpointAdress kısmını bulun ve 127.0.0.1:8990 yazın por için istediğinizi yazabilirsiniz ben böyle yazdım. CTRL + X  yes ile kaydedin ve çıkın.

![image](https://user-images.githubusercontent.com/101635385/230798888-96d0025d-88ed-481e-8ecf-a19431de520d.png)

<hr>


* Nodeyi başlatalım <br>

```shell
cd
```

```shell
sudo systemctl start algorand
```

* Loglara bakalım.

```shell
goal node status -d /var/lib/algorand
```

* Şimdi Nodemizi hızlı senkronizasyon yapmamız lazım bunun için  [BURAYI TIKLAYIN](https://algorand-catchpoints.s3.us-east-2.amazonaws.com/channel/testnet/latest.catchpoint) 

* Açılan sayfada bir kod gelecek bu kodu kopyalayın.

* Kopyaladığınız kodu aşağıdaki alana yazın ve nodenize girin.

```shell
goal node catchup KODU-BURAYA-YAZIN -d /var/lib/algorand/
```

* Bu resimdeki gibi olacak

![image](https://user-images.githubusercontent.com/101635385/230796454-ac79a0a7-fd9f-4013-9bd6-561a808daa14.png)

* Şimdi tekrar loglara bakalım. Sync Tim 0.0s olduğu anda Algo nodeniz senkronize olmuş demektir. 

```shell
goal node status -d /var/lib/algorand
```

![image](https://user-images.githubusercontent.com/101635385/230797051-0a62c7a9-62b2-4291-9478-452b7278c921.png)


* Eğer kurduğunuz algo node Resimdeki gibi Testnet yazmıyorsa aşağıdaki adımları izleyin.

![image](https://user-images.githubusercontent.com/101635385/230797295-b9f00b6e-2c11-416f-91ec-4c90e2db6dc4.png)

```shell
sudo systemctl stop algorand
```
```shell
cd /var/lib/algorand/genesis/testnet
```
```shell
sudo cp genesis.json /var/lib/algorand/
```
```shell
sudo systemctl start algorand
```
```shell
goal node status -d /var/lib/algorand
```


  ## 5- Algo Node Token

* Şimdi Algo nodemizi kurduk senkronize olduktan sonra token alacağız. Aşağıdaki adımları izleyin ve çıkan ekranda bir token göreceksiniz bunu kopyalayın ve biryere yazın kaydedin.

```shell
cd /var/lib/algorand/
```
```shell
vim algod.token
```

* Bu resimdeki gibi bir token kaydettikten sonra sayfadan çıkmak için CTRL + C tuşuna basın ve :qa  yazıp enter tuşuna basın.

![image](https://user-images.githubusercontent.com/101635385/230797631-febc8173-f10f-4e0a-8a5c-e7da3c71a88d.png)


 ## 6- Goracle Node Kurulumu

* Artık Algo nodemizi kuruldu. Şimdi Goracle nodemizi kuralım. 

```shell
wget  -qP /usr/bin/ https://staging.dev.goracle.io/downloads/latest-staging/goracle &&  chmod u+x /usr/bin/goracle
```

*Aşağıdaki kodu girdiğinizde bir kaç işlem yapmamız gerekiyor.  

```shell
goracle init
```

Çıkan sorulara aşağıdaki gibi cevap verin. <br><br>
1- Y yazıp enter tuşuna basın<br>
2- Y yazıp enter tuşuna basın -  Ardından 5. Adımdaki aldığımız tokeni kopyalayıp yapıştırın.<br><br>

![image](https://user-images.githubusercontent.com/101635385/230797920-98e03ac3-8a61-4734-abdd-433eeebf55a7.png)

<br>
3- Ardından ilk adımda oluşturduğum Pera wallet adresini kopyalayın ve yapıştırıp enter tuşuna basın. Bu adresi Asla kaybetmeyin.

![image](https://user-images.githubusercontent.com/101635385/230798018-95544a1a-0570-49bf-8547-a9c6cb732721.png)

![image](https://user-images.githubusercontent.com/101635385/230797992-124909db-9a3f-46fb-8292-633227ec6cb0.png)

<br>

4- Daha sonra düğüm size bir adres verecek bu adresi kopyalayıp tarayıcınıza yapıştırın.

![image](https://user-images.githubusercontent.com/101635385/230798081-bbf432e3-c148-4477-8b05-590bbbd09be1.png)


5- Pera wallet ile bağlanın

![image](https://user-images.githubusercontent.com/101635385/230798155-14dc8581-08b7-4384-a3fc-2fa09806a0ae.png)

* Aşağıdaki gibi bir ekran açılacak Register butonuna basın. Pera Wallet ile onay verin.

![image](https://user-images.githubusercontent.com/101635385/230798189-0aa179e0-c93d-4846-8ea7-253bd7df05e3.png)

6 - Açılan sayfadan 3. Adımda discord üzerinden ticket açarak aldığımız şifreyi girerek GET TEST TOKEN diyoruz ve 11.000 Test token geliyor. 

![image](https://user-images.githubusercontent.com/101635385/230798467-adb8f269-b4d3-41de-a608-0464169fb576.png)

7 - Şimdi aldığımız test tokenleri Stake yapmamız gerekiyor. Aşağıdaki resimdeki gibi Stake işlemini yapın 10.000 adet stake yapın. Bu işlemleri yaparken Cüzdanınızda faucetten test algo olması gerekiyor. ilk adımlarda yapmıştık.

![image](https://user-images.githubusercontent.com/101635385/230798507-4fdfac1b-c955-40d1-b714-157ad2f4286c.png)

![image](https://user-images.githubusercontent.com/101635385/230798522-1a239855-786c-41e8-92ff-9124e03e58bb.png)

8 - Şimdi resimdeki adreste nodeniz size bir adres verdi bu adrese Test algo yollamanız gerekiyor günde 3-4 algo fee gidiyor biraz fazla algo yollayın ister faucetten ister kendi algo adresinizden yollayabilirsiniz. 

![image](https://user-images.githubusercontent.com/101635385/230798618-aa10345a-ba71-4637-80d3-f4cabafd6733.png)

<hr>

9- Şimdi nodemize geri dönelim ve enter tuşuna tekrar basalım. Aşağıdaki resimdeki gibi bir çıktı alacaksınız.

![image](https://user-images.githubusercontent.com/101635385/230798712-aa2baf3a-bfa4-4461-a1da-a7491dd34a88.png)

<hr>


  ## 6- .goracle dosyası

* Goracle dosyasını düzenleyelim. Aşağıdaki komutu girdikten sonra resimdeki gibi alanları düzeltin.

```shell
nano ~/.goracle
```

![image](https://user-images.githubusercontent.com/101635385/230799006-85e2790d-a0a1-45ec-b091-6b1f64f829d4.png)

Server kısmına "server": "http://127.0.0.1:PORT",  port adresini ne girdiyseniz onu yazın eğer hatırlamıyorsanız aşağıdaki komutu kullanıp port adresinize bakın. kaydedin çıkın

```shell
cd /var/lib/algorand
```
```shell
cat algod.net
```

![image](https://user-images.githubusercontent.com/101635385/230799082-03737669-9cc6-4157-81c1-294dfc86ff59.png)


<hr>

  ## 7- Goracle düğümünüzü başlatın.

```shell
goracle docker-start --background
```

* loglara bakın aşağıdaki resimdeki gibi ise nodeniz başlamıştır. 

```shell
docker logs -f goracle-nr
```


![image](https://user-images.githubusercontent.com/101635385/230799145-06ed3b7d-e3b5-4322-bdf6-42c43fe3d088.png)


