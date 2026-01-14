1. PC ve Wi-Fi Güncellemeleri
Bilgisayarı hazırlar, güncellemeleri yapar ve gerekli (non-free) sürücü kaynaklarını ekler.

Sistem Güncellemesi:

``` Bash
sudo apt update
sudo apt upgrade
```

Açıklama: Güncellemeleri kontrol eder ve yükler.

Kaynak Listesini Düzenleme (Non-Free Ekleme):

```Bash

sudo nano /etc/apt/sources.list
```
Açıklama: Editör açıldığında satır sonlarına şunları ekleyin: main contrib non-free non-free-firmware

Wi-Fi Sürücü Kurulumu ve Kontrolü:

```Bash

sudo apt install firmware-b43-installer
sudo reboot
```
Açıklama: Sürücüyü yükler ve bilgisayarı yeniden başlatır.

(Bilgisayar açıldıktan sonra)

```Bash

nmcli radio wifi
nmcli radio wifi on
```
Açıklama: Wi-Fi durumunu kontrol eder, kapalıysa açar.

2. Magic Mirror Kurulumu
Gerekli araçları (Git, Node.js) indirir ve MagicMirror dosyasını kurar.

Ön Hazırlık (Git ve Curl):

```Bash

sudo apt install git curl
```
Açıklama: Git ve Curl araçlarını yükler.

Node.js ve NVM Kurulumu:

```Bash

curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```
Açıklama: NVM (Node Version Manager) kurulum betiğini indirir ve çalıştırır.
(Terminali kapatıp yeniden açmanız gerekebilir)

```Bash

nvm install 24
nvm use 24
```
Açıklama: Node.js 24 sürümünü indirir ve aktif eder.

Versiyon Kontrolleri (İsteğe bağlı):

```Bash

nvm --version
node -v
npm -v
```
MagicMirror İndirme ve Yükleme:

```Bash

git clone https://github.com/MagicMirrorOrg/MagicMirror
cd MagicMirror
npm install
```
Açıklama: Dosyaları indirir, klasöre girer ve kurulumu yapar. (Notunda node --run yazıyordu ancak standart kurulum npm install komutudur, bunu kullanman daha garantidir.)

Örnek Ayar Dosyasını Kopyalama:

```Bash

cp config/config.js.sample config/config.js
```
Açıklama: Örnek ayar dosyasını kopyalar, böylece kendi ayarlarını yapabilirsin.

3. Magic Mirror Konfigürasyonu
Ayarları değiştirmek için dosyayı açma işlemi.

```Bash

nano config/config.js
```
Açıklama: Bu komut dosyayı açar. Word dosyasındaki veya elindeki hazır kodları buraya yapıştırıp kaydedebilirsin.

4. Magic Mirror Çalıştırma
Kurulum bittikten sonra programı başlatmak için.

```Bash

cd ~/MagicMirror
npm start
```
Açıklama: MagicMirror klasörüne gidip programı başlatır.

5. Magic Mirror Otomatik Başlatma (PM2)
Cihaz açıldığında MagicMirror'ın otomatik gelmesi için.

PM2 Yükleme:

```Bash

sudo npm install -g pm2
pm2 startup
```
Açıklama: pm2 startup yazdıktan sonra terminal sana bir kod verecek, o kodu kopyalayıp yapıştırman gerekir.

Script Oluşturma ve Kaydetme: (Bu kısım görselde yoktu ama otomatik başlatma için gereklidir, ek bilgi olarak veriyorum)

```Bash

cd ~
echo 'cd ~/MagicMirror && npm start' > mm.sh
chmod +x mm.sh
pm2 start mm.sh
pm2 save
```
Açıklama: MagicMirror'ı başlatan bir script oluşturur, çalıştırır ve pm2'ye kaydeder.
