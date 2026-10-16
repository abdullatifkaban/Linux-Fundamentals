# Paket Yönetimi

## 🎯 Bu Bölümde Ne Öğreneceğiz?

Bu bölümü bitirdiğinde şunları yapabileceksin:

- Paket, depo ve bağımlılık kavramlarını açıklayabileceksin.
- Paket listelerini güncellemenin neden gerekli olduğunu anlayacaksın.
- `apt` ile yazılım arayabilecek, kurabilecek, kaldırabilecek ve
  güncelleyebileceksin.
- Aynı işlemlerin `pacman` ve `dnf` karşılıklarını söyleyebileceksin.
- Gereksiz paketleri temizleyerek sistemi düzenli tutabileceksin.
- Paket yönetimi becerisini gerçek bir senaryoda, veri bilimi araçlarını
  kurarak uygulayabileceksin.

## 💡 Neden Bu Konuyu Öğreniyoruz?

Bir sistem kurduğunda yalnızca temel yazılımlar gelir. Zamanla yeni araçlar
kurman, eskileri güncellemen ve kullanmadıklarını kaldırman gerekir. Windows'ta
bunun için çoğu zaman tarayıcıdan dosya indirip çift tıklarsın. Linux'ta ise
işin büyük kısmı **paket yöneticisi (package manager)** denen araçla, terminal
üzerinden yapılır.

Paket yöneticisinin asıl üstünlüğü **bağımlılıkları** senin için çözmesidir.
Bir program kurduğunda, o programın ihtiyaç duyduğu diğer paketler otomatik
olarak bulunur ve kurulur. Bu, "eksik dosya" derdini büyük ölçüde ortadan
kaldırır. Ayrıca tüm güncellemeleri tek komutla, güvenilir depolar üzerinden
alırsın.

## 📌 Ön Bilgi

Bu bölüm, 5. bölümde öğrendiğin `sudo` yetkisine ve 6. bölümde tanıdığın
dağıtım ailelerine dayanır. Paket kurmak sistem geneline yazdığı için `sudo`
kullanacağız. Boru kullanımını (4. bölüm) da bir örnekte anımsayacaksın.

## 📖 Kavramlar

### Paket, depo ve bağımlılık

**Paket (package),** bir yazılımın kurulmaya hazır hâlidir; programın kendisi,
ayar dosyaları ve "neye ihtiyaç duyduğu" bilgisi bir arada bulunur. Debian
ailesinde paketler `.deb`, Fedora ailesinde `.rpm` uzantılıdır.

**Depo (repository),** paketlerin indirildiği güvenilir sunuculardır. Paket
yöneticisi, paketleri bu depolardan alır. Böylece her yazılımı ayrı ayrı
sitelerden indirmek zorunda kalmazsın.

**Bağımlılık (dependency),** bir paketin çalışmak için ihtiyaç duyduğu diğer
paketlerdir. Paket yöneticisi bu zinciri otomatik çözer.

### Paket listesi ve güncelleme

Paket yöneticisi, hangi paketin hangi sürümünün depoda olduğunu bir **paket
listesinden** öğrenir. Bu liste zaman zaman tazelenmelidir; aksi hâlde
kurulabilecek en güncel sürümleri göremez. Bu yüzden işe genellikle listeyi
güncellemekle başlanır.

```mermaid
flowchart LR
    A["Depo adresleri"] --> B["Paket listesi güncellenir"]
    B --> C["Paket aranır"]
    C --> D["Paket ve bağımlılıkları kurulur"]
    D --> E["Program kullanıma hazır"]
```

## 🔍 Birlikte Keşfedelim

Sisteminde yaklaşık olarak kaç paket kurulu olduğunu tahmin et. 100 mü, 1000 mi,
daha fazla mı?

Tahminini netleştirdikten sonra sisteminin hangi aileyi kullandığını
anımsayarak (6. bölümde `ID_LIKE=debian` görmüştün) şu komutu çalıştır:

```bash
apt list --installed | wc -l
```

Burada iki şey yapıyoruz: `apt` kurulu paketleri listeliyor, boru (`|`) ile
`wc -l` bu listenin satır sayısını, yani yaklaşık paket sayısını veriyor.
Muhtemelen beklediğinden çok daha fazla paket görürsün. Bu, bir Linux sisteminin
arkada ne kadar çok küçük bileşenden oluştuğunu gösterir.

## 🛠️ Uygulama

Aşağıdaki komutları Debian ailesinde, yani kendi Mint sisteminde
çalıştırabilirsin. Diğer ailelerin karşılıklarını birazdan karşılaştıracağız.

### 1. Adım: Paket listesini güncelle

```bash
sudo apt update
```

Bu komut paket kurmaz; yalnızca "depolarda neler var, hangi sürümler var?"
bilgisini tazeler. Çıktıda hangi depoların okunduğunu göreceksin. Hata değil,
bilgi mesajlarıdır.

### 2. Adım: Paket ara

```bash
apt search htop
```

`apt search`, adında ya da açıklamasında verdiğin kelime geçen paketleri
listeler. `htop`, sistem kaynaklarını gösteren küçük bir araçtır ve 8. bölümde
işimize yarayacak.

### 3. Adım: Paket kur

```bash
sudo apt install htop
```

Kurulum sırasında ekranda kurulacak ek paketler ve ne kadar yer kaplayacağı
yazar; onay istenirse `E` ya da `y` yazıp Enter'a bas. Ardından programı
çalıştır:

```bash
htop
```

`htop` ekranında çalışan süreçleri ve kaynak kullanımını görürsün. Çıkmak için
`q` tuşuna bas. (Bu programı 8. bölümde ayrıntılı kullanacağız.)

### 4. Adım: Paketi kaldır

```bash
sudo apt remove htop
```

`remove`, programı kaldırır ama ayar dosyalarını bırakabilir. Ayar dosyalarıyla
birlikte tamamen temizlemek için `purge` kullanılır:

```bash
sudo apt purge htop
```

### 5. Adım: Sistemi güncelle ve temizle

```bash
sudo apt upgrade
sudo apt autoremove
```

- `upgrade`, kurulu paketleri depodaki daha yeni sürümlere yükseltir.
- `autoremove`, artık hiçbir paketin ihtiyaç duymadığı bağımlılıkları temizler.

> [!TIP]
> Düzenli bir sistem için sıralama genellikle şöyledir: `sudo apt update`,
> ardından `sudo apt upgrade`, sonra ara sıra `sudo apt autoremove`. Bu üçlü,
> sistemi güncel ve temiz tutar.

### 6. Adım: Aileler arası karşılaştırma

Aynı işlerin diğer ailelerdeki karşılıkları şöyledir. Not: Bu komutları Mint'te
çalıştıramazsın, çünkü o paket yöneticileri sisteminde yok; tablo yalnızca
karşılaştırma içindir.

| İşlem | Debian (`apt`) | Arch (`pacman`) | Fedora (`dnf`) |
|---|---|---|---|
| Paket listesini güncelle | `sudo apt update` | `sudo pacman -Sy` | `sudo dnf check-update` |
| Paket ara | `apt search ad` | `pacman -Ss ad` | `dnf search ad` |
| Paket kur | `sudo apt install ad` | `sudo pacman -S ad` | `sudo dnf install ad` |
| Paket kaldır | `sudo apt remove ad` | `sudo pacman -R ad` | `sudo dnf remove ad` |
| Sistemi güncelle | `sudo apt upgrade` | `sudo pacman -Syu` | `sudo dnf upgrade` |

Bu tabloyu bir sözlük gibi kullanabilirsin: internette `pacman` komutu bulursan,
işin ne olduğunu anlayıp kendi `apt` karşılığına çevirebilirsin.

> [!CAUTION]
> Arch ailesinde tek başına `pacman -Sy` (listeyi güncelle) çalıştırıp hemen
> tek bir paket kurmak, parçalı güncelleme denen bir soruna yol açabilir.
> Arch'ta güncelleme genellikle tek adımda, `sudo pacman -Syu` ile yapılır. Bu,
> farklı ailelerin farklı güvenlik kuralları olduğunu gösteren iyi bir örnektir.

### 7. Adım: Veri bilimi araçlarını kuralım

Şimdiye kadar öğrendiğin beceri, tek bir pakete ya da tek bir işe bağlı değil.
Paket yönetimi, ihtiyaç duyduğun her yazılımı kurmanın genel yoludur. Bunu
somut bir örnekle taçlandıralım: veri bilimi ve analitik çalışmak için gereken
temel araçları kuralım.

Bu alanda en çok ihtiyaç duyulan araçlar ve işleri şunlardır:

| Araç | Ne işe yarar? |
|---|---|
| `python3` | Veri analizinin temel programlama dilidir |
| `pip` | Python paketlerini kuran paket yöneticisidir |
| `numpy` | Sayısal diziler ve matematiksel işlemler |
| `pandas` | Tablo (veri çerçevesi) işlemleri ve veri analizi |
| `matplotlib` | Grafik ve görselleştirme |
| `jupyterlab` | Kodu, notları ve görselleri bir arada tutan etkileşimli defter |

Bu araçları doğrudan sistem geneline kurmak yerine, işe Python'un temel
bileşenlerini kurmakla başlıyoruz:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

Buradaki `python3-venv`, birazdan kullanacağımız **sanal ortam (virtual
environment)** için gerekir. Sanal ortam, bir projeye ait Python paketlerini
sistemin geri kalanından ayıran izole bir klasördür. Böylece bir projedeki
paket sürümleri, başka bir projeyi ya da sistemi etkilemez.

Bir proje klasörü oluşturup içinde sanal ortamı kur:

```bash
mkdir -p ~/veri_bilimi
cd ~/veri_bilimi
python3 -m venv .venv
```

Şimdi veri bilimi paketlerini bu izole ortamın içine kuralım:

```bash
.venv/bin/pip install numpy pandas matplotlib jupyterlab
```

> [!NOTE]
> Burada pip'i sanal ortamın kendi yolundan çağırdık. Sanal ortamı
> "etkinleştirme" alışkanlığını ve `source` komutunu 11. bölümde kabuk
> konusunda göreceğiz; şimdilik programları yolunu vererek çalıştırmak
> yeterlidir. Ayrıca güncel sürümlerde sistemin kendi Python'una doğrudan
> `pip install` çalıştırmak "externally-managed-environment" hatasıyla
> engellenir; sanal ortam, bu sınırı aşmanın ve sistemi korumanın önerilen
> yoludur.

Kurulumun eksiksiz olduğunu doğrula:

```bash
.venv/bin/python -c "import numpy, pandas, matplotlib; print('Araclar hazir')"
```

Jupyter Lab'i başlatmak için:

```bash
.venv/bin/jupyter lab
```

Bu komut, tarayıcıda etkileşimli bir defter açar; ilk açılış birkaç saniye
sürebilir. Kapatmak için terminalde `Ctrl` + `C` tuşlarına bas.

> [!TIP]
> Aynı araçları sistem geneline yerleştirmek de mümkündür:
> `sudo apt install python3-numpy python3-pandas python3-matplotlib
> jupyter-notebook`. Ancak apt ile gelen sürümler genellikle daha eskidir ve
> paketler tüm sisteme yayılır. Öğrenme ve proje çalışmaları için sanal ortam
> daha düzenli ve güncel bir yol sunar; iki yöntemi karıştırmamaya çalış.

Bir projeyi tamamen kaldırmak istediğinde iş çok kolaydır; çünkü projeye ait her
şey tek bir klasörde toplanmıştır:

```bash
cd ~
rm -rf veri_bilimi
```

Yüzlerce paketi tek tek kaldırmak yerine, sanal ortamı barındıran klasörü
silmek yeterli olur. Bu, paketleri izole tutmanın pratikte neden bu kadar
değerli olduğunu somut olarak gösterir.

## 🧪 Deneyelim ve Gözlemleyelim

Küçük bir paket kurup paket yöneticisinin bağımlılıkları nasıl çözdüğünü
gözlemleyelim.

```bash
sudo apt install cowsay
cowsay "Paket yonetimi ogreniyorum"
```

Kurulum çıktısında, doğrudan istediğin paketin yanında birkaç ek paketin de
kurulduğunu görebilirsin; işte bunlar bağımlılıklardır. Programı çalıştırdığında
ekranda bir inek karakteri senin cümleni söyler. Şimdi paketi kaldır:

```bash
sudo apt remove cowsay
```

Kurulum ile kaldırma çıktılarını karşılaştır ve paket yöneticisinin ne kadar çok
işi senin yerine hallettiğini fark et.

## ⚠️ Bir Şeyler Ters Giderse

**Belirti:** `apt install` "Unable to locate package" (paket bulunamadı) hatası
veriyor.

**Olası neden:** Paket adını yanlış yazmışsın ya da paket listesi güncel değil.

**Ne yapmalısın:** Önce paket adını `apt search` ile doğrula. Ardından
`sudo apt update` çalıştırıp listeyi tazele ve tekrar dene.

**Belirti:** "Could not get lock /var/lib/dpkg/lock" gibi bir kilit hatası
alıyorsun.

**Olası neden:** Başka bir paket işlemi (örneğin açık bir güncelleme penceresi)
hâlâ çalışıyor.

**Ne yapmalısın:** Açık güncelleme yöneticisini kapat, birkaç saniye bekle ve
komutu tekrar dene. Kilidi zorla silmek son çaredir ve yanlış yapılırsa paket
veritabanını bozar.

**Belirti:** Kurulum yarıda kaldı ve sistem "broken packages" uyarısı veriyor.

**Ne yapmalısın:** `sudo apt --fix-broken install` komutu, yarım kalan
bağımlılıkları tamamlamaya çalışır. Sorun sürerse çıktıyı dikkatle oku ve
mesajın ne söylediğini anlamaya çalış.

## ✍️ Kendin Dene

**Görev:** Sisteminde kurulu olmayan küçük bir araç seç (örneğin `sl`, `figlet`
ya da `tree`). Önce `apt search` ile bul, sonra kur, çalıştır ve işin bitince
kaldır. Kurulum ve kaldırma arasındaki adımları kendi cümlelerinle not et.

<details>
<summary>İpucu göster</summary>

Aradığın paket adını bilmiyorsan `apt search anahtar_kelime` ile başla. Kurmadan
önce paketin açıklamasını okumak da iyi bir alışkanlıktır.

</details>

<details>
<summary>Örnek çözüm göster</summary>

```bash
apt search figlet
sudo apt install figlet
figlet "Merhaba"
sudo apt remove figlet
```

`figlet`, verdiğin metni büyük harflerle çizer. Sıralama her zaman aynıdır:
ara, kur, çalıştır, kaldır. Kurulumda bağımlılıkların otomatik geldiğini ve
kaldırmada nelerin gittiğini gözlemle.

</details>

## 🧠 Öğrendiklerini Kontrol Et

1. Paket yöneticisi kullanmak, yazılımı elle indirip kurmaktan neden daha
   güvenlidir?
2. Bağımlılık nedir ve kim çözer?
3. `apt update` ile `apt upgrade` arasındaki fark nedir?
4. `remove` ile `purge` arasındaki fark nedir?
5. Arch ailesinde bir paket kurmak için hangi komut kullanılır?

<details>
<summary>Cevapları göster</summary>

1. Çünkü paketler güvenilir depolardan gelir, imzalıdır ve bağımlılıklar
   otomatik çözülür. Ayrıca güncellemeler tek merkezden yönetilir.
2. Bir paketin çalışmak için ihtiyaç duyduğu diğer paketlerdir; paket yöneticisi
   bunları otomatik olarak bulup kurar.
3. `apt update` yalnızca paket listesini tazeler, hiçbir şey kurmaz.
   `apt upgrade` ise kurulu paketleri daha yeni sürümlere yükseltir.
4. `remove` programı kaldırır ama ayar dosyalarını bırakabilir; `purge` ayar
   dosyalarıyla birlikte tamamen kaldırır.
5. `sudo pacman -S paket_adi`.

</details>

## 🚀 Bağımsız Çalışma

1. **Araştırma görevi:** `apt` ile `dpkg` arasındaki farkı araştır. `dpkg`
   neden tek başına bağımlılıkları çözemez?
2. **Çeviri görevi:** İnternetten `dnf` için yazılmış bir paket kurma komutu
   bul. Bunu kendi sisteminde kullanacağın `apt` komutuna çevir.

Bu görevler, farklı dağıtımlarda karşılaşacağın komutları kendi sistemine
uyarlama becerisi kazandırır.

## 📚 Daha Fazlasını Öğrenmek

- Debian APT kullanım kılavuzu: <https://wiki.debian.org/Apt>
- Ubuntu paket yönetimi belgeleri: <https://help.ubuntu.com>
- Arch Wiki - pacman: <https://wiki.archlinux.org/title/pacman>
- Fedora DNF belgeleri: <https://docs.fedoraproject.org>
- Python resmî belgeleri: <https://docs.python.org/3/>
- pandas projesi: <https://pandas.pydata.org>
- Jupyter projesi: <https://jupyter.org>

## 📝 Kısa Özet

- Paketler güvenilir depolardan gelir; paket yöneticisi bunları kurar, günceller
  ve kaldırır.
- Bağımlılıklar paket yöneticisi tarafından otomatik çözülür.
- Debian ailesinde `apt`, Arch ailesinde `pacman`, Fedora ailesinde `dnf`
  kullanılır.
- İş akışı genellikle şöyledir: listeyi güncelle, ara, kur, güncelle, temizle.
- Paket yönetimi becerisi geneldir; aynı yaklaşımla veri bilimi gibi bir alanın
  tüm araç setini tek seferde kurabilirsin.
- Farklı ailelerin komutlarını karşılaştırmalı bilmek, internetteki çözümleri
  doğru uyarlamanı sağlar.

[Önceki bölüm: Dağıtım Aileleri ve Masaüstü Ortamları](06-Distributions-And-Desktops.md) | [İçindekiler](../README.md) | [Sonraki bölüm: Süreç ve Servis Yönetimi](08-Process-And-Services.md)
