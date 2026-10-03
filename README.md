# EnsariPOS — SambaPOS / AlfaPOS Restoran Yazılımları

**SambaPOS** ve **AlfaPOS** (SambaPOS tabanlı) ile çalışan restoran yazılımları: QR menü, self-servis kiosk, garson uygulaması, kurye ve paket servis, patron raporları, bulut lisans sunucusu. **Her ürün kendi deposundadır** — kodu, kurulumu ve katkı süreci ayrıdır. Bu sayfa hangi ürünün nerede olduğunu ve nasıl çalıştırılacağını anlatır.

> 🇬🇧 Open-source restaurant software for **SambaPOS / AlfaPOS**: QR menu, self-ordering kiosk, waiter app, courier & delivery, owner reports, cloud licensing. Each product lives in its own repository.

<p>
  <img src="https://raw.githubusercontent.com/yusuf631636/EnsariPOS-Kiosk/main/docs/ekran-goruntuleri/kiosk-menu.png" alt="Kiosk menü ekranı" width="230">
  <img src="https://raw.githubusercontent.com/yusuf631636/EnsariPOS-Kiosk/main/docs/ekran-goruntuleri/kiosk-qr-odeme.png" alt="Kiosk QR ile kart ödemesi" width="230">
  <img src="https://raw.githubusercontent.com/yusuf631636/EnsariPOS-Garson/main/docs/ekran-goruntuleri/garson-direkt-ayarlar.png" alt="Garson Direkt ayarlar" width="200">
</p>

## Ürünler

| Ürün | Ne yapar | Depo |
|---|---|---|
| **QR Menü** | Müşteri masadaki QR'ı okutur, menüyü görür, sipariş verir. Yönetim paneli, garson web ekranı, Android uygulamaları. | [EnsariPOS-QR-Menu](https://github.com/yusuf631636/EnsariPOS-QR-Menu) |
| **Kiosk** | Self-servis sipariş kioskı: dokunmatik menü, ürün seçenekleri ve not, masa seçimi, çoklu dil, QR ile kart ödemesi, kendi fiş yazıcısı. | [EnsariPOS-Kiosk](https://github.com/yusuf631636/EnsariPOS-Kiosk) |
| **Gelişmiş Kurye** | Paket siparişleri kuryelere dağıtır; kurye ekranı ve müşteriye canlı takip linki. | [EnsariPOS-Gelismis-Kurye](https://github.com/yusuf631636/EnsariPOS-Gelismis-Kurye) |
| **Ultra Paketçi** | Paket servis ve kurye yönetimi. | [EnsariPOS-Ultra-Paketci](https://github.com/yusuf631636/EnsariPOS-Ultra-Paketci) |
| **Patron Raporu** | İşletme sahibi için satış raporları: web paneli ve Android uygulaması. | [EnsariPOS-Patron-Raporu](https://github.com/yusuf631636/EnsariPOS-Patron-Raporu) |
| **Garson** | Garson uygulaması: web, Windows servisi, Android ve sunucusuz Garson Direkt. | [EnsariPOS-Garson](https://github.com/yusuf631636/EnsariPOS-Garson) |
| **Kurye Takip** | Kurye konum ve teslimat takibi. | [EnsariPOS-Kurye-Takip](https://github.com/yusuf631636/EnsariPOS-Kurye-Takip) |
| **Bulut** | Lisans ve aktivasyon, yönetici/bayi panelleri, restoranlara tünel, otomatik güncelleme. | [EnsariPOS-Bulut](https://github.com/yusuf631636/EnsariPOS-Bulut) |

## Nasıl çalıştırılır

Her deponun kendi **README** dosyasında adım adım anlatım vardır. Genel yol:

### 1. Hazırlık

- **Windows** bilgisayar.
- **SambaPOS V5** veya **AlfaPOS** kurulu ve **mesaj sunucusu** açık (varsayılan port `9000`, güvenlik duvarında izinli). Bulut hariç tüm ürünler SambaPOS'a buradan bağlanır.
- SambaPOS'ta **`EnsariGarson`** GraphQL istemci kaydı (ürünlerin kurulum paketi / hazırlık aracı otomatik ekler).
- SambaPOS'ta **Yönetici** rolünde bir kullanıcı ve bu kullanıcının **Şifre** alanı (PIN değil) dolu olmalı.
- Ürüne göre: **Node.js 18+** (Node.js sürümleri için) veya hiçbir şey (C# sürümleri Windows'un kendi derleyicisiyle derlenir).

### 2. Kodu indirin

```
git clone https://github.com/yusuf631636/EnsariPOS-QR-Menu.git
cd EnsariPOS-QR-Menu
```

(Depo adını çalıştırmak istediğiniz ürünle değiştirin. Git yoksa depo sayfasında **Code → Download ZIP**.)

### 3. Ayar dosyasını oluşturun

Şifre ve anahtarlar depoda **yoktur**. Her projede örnek ayar dosyası bulunur:

```
copy config.example.json config.json
```

`config.json` dosyasını açıp kendi SambaPOS adresinizi, kullanıcı adınızı ve şifrenizi yazın. Bu dosya GitHub'a gönderilmez.

### 4. Çalıştırın

**Node.js sürümleri** (`nodejs` klasörü olan depolar, Bulut, Kurye Takip):

```
npm install
node server.js
```

**C# sürümleri** (`csharp` klasörü, Kiosk, Garson servisi):

```
powershell -ExecutionPolicy Bypass -File derle.ps1
UrunAdiSrv.exe /console
```

`derle.ps1` programı derler (ör. `KioskSrv.exe`, `QRMenuSrv.exe`); `/console` ile servis kurmadan denersiniz.

**Android uygulamaları**: JDK 17, Android SDK ve Cordova gerekir; ilgili klasördeki `derle.ps1` adımları içerir.

**Kurulum paketleri**: `*.iss` dosyaları Inno Setup ile kurulum exe'si üretir.

## Katkı vermek

1. Katkı vermek istediğiniz ürünün deposunu **Fork**'layın.
2. Değişikliğinizi yapıp yerelde deneyin.
3. **Pull Request** açın: ne değişti, neden, nasıl test ettiniz.
4. Proje sahibi inceler; onaylanınca birleştirilir.

Kurallar her depodaki `CONTRIBUTING.md` dosyasında. Şifre, anahtar, müşteri verisi veya veritabanı dosyası göndermeyin; canlı bir SambaPOS'a test siparişi atmayın.

## Güvenlik

Açık bulursanız herkese açık issue açmayın; ilgili deponun **Security → Report a vulnerability** bölümünden gizli bildirin.

## Lisans

Tüm depolar **MIT** lisanslıdır.
