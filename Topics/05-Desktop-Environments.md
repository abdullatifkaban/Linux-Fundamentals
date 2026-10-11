# Masaüstü Ortamları

## 🎯 Bu Derste Ne Öğreneceğiz?

Bu derste, Linux'ta kullanılan başlıca masaüstü ortamlarını — GNOME, KDE Plasma, XFCE, Cinnamon, LXQt, MATE gibi — tanıyacak; ancak bu derste sadece GNOME, KDE Plasma ve XFCE'yi detaylı olarak ele alacağız. Her birinin arayüz tasarımı, kaynak kullanımı ve kullanıcı deneyimi açısından farklarını gözlemleyeceksiniz. Ayrıca mevcut sisteminizde farklı bir masaüstü ortamını kurup kısa süreli deneyimleyerek bu farkları doğrudan yaşayacaksınız.

## 💡 Neden Bu Konuyu Öğreniyoruz?

Veri biliminde çalışırken, görsel araçları ve not defterlerini kullanmak için rahat bir arayüz önemlidir. Bazı kullanım senaryolarında hafif bir masaüstü (XFCE) daha hızlı yanıt verir; bazı durumlarda zengin özellikli bir ortam (GNOME, KDE) daha verimlidir. Bu dersteki deneyim, hangi ortamın sizin çalışma tarzınıza daha uygun olduğunu anlamanızı sağlar.

> [!NOTE]
> Masaüstü ortamı (desktop environment), pencere yönetimi, uygulama başlatıcıları, sistem ayarları ve görsel öğeleri bir araya getiren bir yazılım katmanıdır. Linux çekirdeği tek başına görsel bir arayüz sunmaz; masaüstü ortamı bu eksikliği tamamlar.

## Ön Bilgi

Bu dersi takip etmek için önceki haftalarda öğrenilen temel kavramlar (dosya sistemi, komutlar) yeterlidir. Ayrıca paket kurulumu (Hafta 6) hakkında kısa bilgi sahibi olmak faydalıdır; çünkü farklı masaüstü ortamlarını kurmak için paket yöneticisi kullanacağız.

## Kavramlar

### GNOME

GNOME, modern ve sade bir tasarıma sahip, dokunmatik cihazlar için optimize edilmiş bir masaüstü ortamıdır. Varsayılan olarak Ubuntu'da kullanılır.

### KDE Plasma

KDE Plasma, yüksek özelleştirilebilirlik sunan, zengin görsel efektleri olan bir ortamdır. Fedora gibi dağıtımlarda alternatif olarak bulunur.

### XFCE

XFCE, eski donanımlarda bile hızlı çalışabilen hafif bir masaüstü ortamıdır. Kaynak tüketimi düşüktür; sunucu veya eski sistemler için uygundur.

### Karşılaştırma Tablosu

| Özellik | GNOME | KDE Plasma | XFCE |
|---|---|---|---|
| Ağırlık | Orta | Orta-yüksek | Hafif |
| Özelleştirme | Orta | Çok yüksek | Orta |
| Varsayılan dağıtım | Ubuntu | Kubuntu, Fedora (alt) | Xubuntu |
| Kaynak kullanımı | Orta | Yüksek | Düşük |

## 🔍 Birlikte Keşfedelim

Sisteminizde mevcut masaüstü ortamını gözlemleyin:

1. `echo $XDG_CURRENT_DESKTOP` komutunu çalıştırın. Çıktıyı not edin.
2. Çalışan masaüstü uygulamalarını listelemek için `ls /usr/share/applications/ | head -n 10` komutunu kullanın.
3. Diğer iki masaüstü ortamını kurun (mevcut hangisi olursa olsun):
   - `sudo apt install xfce4` (XFCE) — Ubuntu/Mint
   - `sudo apt install kde-plasma-desktop` (KDE) — Ubuntu/Mint (veya `sudo dnf install @kde-desktop` Fedora)
   - `sudo apt install cinnamon` (Cinnamon) veya `sudo dnf install @cinnamon-desktop`

Tahmin edin: XFCE ile GNOME arasında açılış hızı açısından fark olacak mı? Neden?

Şimdi `echo $XDG_CURRENT_DESKTOP` çıktısını gözlemleyin ve mevcut ortamı yazın.

## 🛠️ Uygulama

Aşağıdaki görevleri sırayla tamamlayın:

1. `sudo apt install xfce4` (Ubuntu/Debian) veya `sudo dnf install @xfce-desktop` (Fedora) ile XFCE'yi kurun. Ayrıca `sudo apt install kde-plasma-desktop` veya `sudo dnf install @kde-desktop` ile KDE'yi kurun. Üç ortamı da kurup giriş ekranında seçin.
2. Kurulum tamamlandığında oturumu kapatın ve giriş ekranında XFCE oturumunu seçin.
3. XFCE masaüstünde bir pencere açın ve `ls` komutuyla dosyaları listeleyin.
4. Masaüstü arka planını değiştirin; ayarlar menüsünden bir görsel seçin.

> [!TIP]
> Farklı bir masaüstü kurulumu yaptıktan sonra orijinal ortamınıza geri dönmek için giriş ekranında session seçeneğini değiştirebilirsiniz.

## 🧪 Deneyelim ve Gözlemleyelim

Deneyleri yapın:

1. **Açılış hızı:** XFCE'ye giriş yaptıktan sonra bir terminal açın; `time ls` komutuyla basit bir komutun ne kadar sürede çalıştığını gözlemleyin.
2. **Kaynak kullanımı:** `top` veya `htop` komutuyla mevcut süreçleri listeleyin; RAM kullanımını karşılaştırın (GNOME vs XFCE).
3. **Özelleştirme:** XFCE'de paneli sağ tıklayıp yeni öğe ekleyin; GNOME'de ise ayarlardan "Karanlık Mod" veya "Büyük Metin" gibi seçenekleri deneyin.

> [!WARNING]
> Aynı anda çok sayıda masaüstü kurmak sistem kaynaklarını tüketebilir. Deney için en az 2 GB RAM ayırın; düşük sistemlerde sadece bir ek ortam kurun.

## Bir Şeyler Ters Giderse

Farklı masaüstü kurulumunda sorunlar:

1. **Giriş ekranında yeni seçenek görünmüyor:** `sudo systemctl restart display-manager` komutuyla giriş yöneticisini yeniden başlatın.
2. **Ekran çözünürlüğü yanlış:** Masaüstü ayarlarında ekran çözünürlüğünü manuel ayarlayın.
3. **Kurulum başarısız:** Paket yönetimi hatasını (`apt` veya `dnf`) kontrol edin; internet bağlantısını doğrulayın.

## Kendin Dene

Aşağıdaki görevleri tamamlayın:

1. Kendi sisteminizde `echo $XDG_CURRENT_DESKTOP` çıktısını yazın.
2. `ls /usr/share/applications/` ile kurulu uygulamaları listeleyin; en az 5 uygulama adını not edin.
3. Bir arkadaşıyla (veya kendi notlarınızla) GNOME ve XFCE arasındaki farkları üç maddeyle özetleyin.

<details>
<summary>Cevapları göster</summary>

1. Çıktı mevcut ortamı gösterir (örneğin `GNOME`, `XFCE`).
2. Çıktı uygulama adı listesi verir (örneğin `firefox.desktop`, `org.gnome.Terminal.desktop`).
3. Özet: GNOME daha modern ve dokunmatik uyumlu; XFCE daha hafif ve hızlı; GNU daha özelleştirilebilir.

</details>

## 🧠 Öğrendiklerini Kontrol Et

1. GNOME, KDE Plasma ve XFCE arasındaki en belirgin fark nedir?
2. XFCE'nin hangi durumlarda tercih edilmesi gerekir?
3. `echo $XDG_CURRENT_DESKTOP` komutu ne işe yarar?

<details>
<summary>Cevapları göster</summary>

1. GNOME modern/sade; KDE yüksek özelleştirme; XFCE hafif/hızlı.
2. Eski donanım, düşük RAM, sunucu veya hızlı yanıt gerektiren senaryolar.
3. Mevcut masaüstü ortamının adını yazdırır.

</details>

## Bağımsız Çalışma

Kendi Linux sisteminizde bu bağımsız çalışmayı tamamlayın:

- Mevcut masaüstü ortamınızı belirleyin (`echo $XDG_CURRENT_DESKTOP`).
- Eğer mümkünse, `sudo apt install xfce4` (veya eşdeğeri) ile XFCE kurun; giriş ekranından XFCE oturumunu seçin.
- XFCE'de bir terminal açın (`Ctrl + Alt + T`) ve `ls -la` komutunu çalıştırın; sonuçları önceki GNOME deneyiminizle karşılaştırın (pencere boyutu, hız, menü düzeni).
- Çalışmayı tamamladığınızda orijinal oturuma geri dönün.

## Daha Fazlasını Öğrenmek

- GNOME: [https://www.gnome.org/](https://www.gnome.org/)
- KDE Plasma: [https://kde.org/plasma-desktop/](https://kde.org/plasma-desktop/)
- XFCE: [https://www.xfce.org/](https://www.xfce.org/)

## Kısa Özet

Bu derste GNOME, KDE Plasma ve XFCE masaüstü ortamlarını karşılaştırdınız. Her birinin ağırlığı, özelleştirme oranı ve hedef kitlesi arasındaki farkları gözlemlediniz. Bir sonraki derste paket yönetimi (apt, dnf, snap) konularını öğreneceğiz.

---

← [Farklı Dağıtımlar](04-Distributions.md) | [Paket Yönetimi →](06-Package-Management.md)
