# Sei-Node-Kurma ve Validatör Olma

Sei Network validatör kurulum rehberi


Sei Ağı, sipariş defterine özgü ilk L1 blok zinciridir. Zincir, her şeyden önce güvenilirliği, güvenliği ve yüksek verimi vurgulayarak, üstüne inşa edilmiş ultra yüksek performanslı DeFı ürünlerinin tamamen yeni bir kademesini mümkün kılıyor. Sei'nin zincir içi CLOB ve eşleştirme motoru, tüccarlar ve uygulamalar için derin likidite ve fiyat-zaman öncelikli eşleştirme sağlar. Seı üzerine kurulu uygulamalar, yerleşik sipariş defteri altyapısından, derin likiditeden ve tamamen merkezi olmayan bir eşleştirme hizmetinden yararlanır. Kullanıcılar, MEV koruması ile birlikte işlemlerinin fiyatını, boyutunu ve yönünü seçme yeteneği ile bu değişim modelinden yararlanır.


Validator Node Gereksinimleri
Sistem Gereksinimleri :

Bellek	Cpu	Disk	Ağ
4GB	Quad-Core	250GB	1Gbps/100Mbps
Yazılım Gereksinimleri :

Gereksinim	Not	İşletim Sistemi
Go Sürümü	1.17+	Ubuntu 20.04
Oto Kurulum
Öncelikle Sunucumuza baglanalım, bir pencere açalım ve işlemlere başlayalım.

  #Screen Kuralım
  apt install screen
  #Yeni bir screen açalım
  screen -S node
  #Oto kurulumu başlatalım
  wget -q -O sei-kur.sh https://api.rues.info/sei-kur.sh && chmod +x sei-kur.sh && sudo /bin/bash sei-kur.sh
  #Node ismi isteycektir girin ve Enter basın işlemin bitmesini bekleyin
Şuan Node'unuz kuruldu ve Servis dosyası oluştu. Node Pencerisi içine Node Loglarımızı açalım.

 journalctl -u seid -f
CTRL + A + D ile pencerimizi kapatalım. Eşleşme Tamamlandıktan sonra validatör açmanız gerek...

 screen -S validator
 #"<wallet-ismi>" degiştirin ve cüzdan oluşturun
 seid keys add <wallet-ismi>
 
 #Oluşan Cüzdan kayıt edin ve Token alın. "<wallet-ismi>" degiştirin.
 
 PUBKEY=$(seid tendermint show-validator)
 seid tx staking create-validator \
    --amount=1000000usei \
    --pubkey=$PUBKEY \
    --moniker=$MONIKER \
    --chain-id=sei-testnet-2 \
    --from=<wallet-ismi> \
    --commission-rate="0.10" \
    --commission-max-rate="0.20" \
    --commission-max-change-rate="0.01" \
    --min-self-delegation="1" \
    --yes
 #"CTRL + A + D" screen kapatın.
1.0.3b Güncellemesi
Node Pencerinize girin, "systemctl stop seid" ile durdurun. Güncellemeye devam edin..

 Update 1.0.3b

//oto kurulum için
cd
rm $HOME/sei -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.3beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
mv $HOME/sei-chain $HOME/sei
systemctl restart seid
journalctl -fu seid -o cat

//manuel kurulum için
cd
rm $HOME/sei-chain -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.3beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
systemctl restart seid
journalctl -fu seid -o cat
1.0.4b Güncellemesi
//oto kurulum için
cd
rm $HOME/sei -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.4beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
mv $HOME/sei-chain $HOME/sei
systemctl restart seid
journalctl -fu seid -o cat

//manuel kurulum için
cd
rm $HOME/sei-chain -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.4beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
systemctl restart seid
journalctl -fu seid -o cat
1.0.5b Güncellemesi
//oto kurulum için
cd
rm $HOME/sei -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.5beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
mv $HOME/sei-chain $HOME/sei
systemctl restart seid
journalctl -fu seid -o cat

//manuel kurulum için
cd
rm $HOME/sei-chain -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.5beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
systemctl restart seid
journalctl -fu seid -o cat
1.0.6b Güncellemesi
//oto kurulum için
cd
rm $HOME/sei -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.6beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
mv $HOME/sei-chain $HOME/sei
systemctl restart seid
journalctl -fu seid -o cat

//manuel kurulum için 
cd
rm $HOME/sei-chain -rf
git clone https://github.com/sei-protocol/sei-chain.git && cd $HOME/sei-chain
git checkout 1.0.6beta
make install
go build -o build/seid ./cmd/seid
chmod +x ./build/seid && sudo mv ./build/seid /usr/local/bin/seid
mv ~/go/bin/seid /usr/local/bin/seid
systemctl restart seid
journalctl -fu seid -o cat
//UnJail seid tx slashing unjail --broadcast-mode=block --from=wallet chain-id=sei-testnet-2

Sei Network Discord Kanalı Linki: https://discord.gg/aRYdu6Y3

Hesaplarım;

https://medium.com/@birgaripbeserr
https://twitter.com/birgaripbeserr

