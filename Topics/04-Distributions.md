# Farklı Dağıtımlar

## 🎯 Bu Derste Ne Öğreneceğiz?

Bu derste, Linux dünyasındaki başlıca dağıtımları — Debian, Fedora ve Arch — tanıyacak; her birinin paket yönetimi, güncelleme politikası, masaüstü ortamı ve hedef kitle açısından farklarını karşılaştıracaksınız. Ayrıca sanal makine veya canlı USB ile en az bir dağıtımı deneyimleyerek bu farkları doğrudan gözlemleyeceksiniz.

## 💡 Neden Bu Konuyu Öğreniyoruz?

Veri biliminde çalışırken, sunucu ortamı olarak genellikle Debian veya Ubuntu tabanlı sistemler tercih edilir; ancak geliştirme ortamı için Fedora gibi daha güncel paketlerin bulunduğu dağıtımlar da kullanılır. Farklı dağıtımların avantajlarını bilmek, doğru ortamı seçmenizi sağlar ve ilerleyen haftalarda sistem bakımı görevlerinde size esneklik kazandırır.

> [!NOTE]
> Dağıtım (distribution), Linux çekirdeği üzerine kurulmuş bir işletim sistemi paketidir. Çekirdek aynıdır; fark, paketlerin seçimi, yapılandırması ve yönetim araçlarında ortaya çıkar.

## Ön Bilgi

Bu dersi takip etmek için önceki haftalarda öğrenilen temel kavramlar (çekirdek, kabuk, dosya sistemi, komutlar) yeterlidir. Sanal makine veya canlı USB kullanarak deneme yapacağınız için kurulum adımlarını (Hafta 1) hatırlamanız faydalı olur.

## Kavramlar

### Distribüsyon Karşılaştırması

| Özellik | Debian (Stable) | Fedora | Arch Linux |
|---|---|---|---|
| Paket yöneticisi | apt | dnf | pacman |
| Güncelleme sıklığı | Kararlı, yavaş | 6 ay | Sürekli (rollingg) |
| Masaüstü varsayılan | Açık seçenek | GNOME | Açık seçenek |
| Hedef kitle | Sunucu, kurumsal | Geliştirici | İleri kullanıcı |
| Açık kaynak desteği | Geniş | Geniş | Geniş |

> [!TIP]
> Linux Mint, Ubuntu tabanlı bir dağıtım olmasına rağmen ek araçlar ve daha kullanıcı dostu bir arayüz sunar. Karşılaştırma yaparken sadece paket yöneticisini değil, kullanıcı deneyimini de göz önünde bulundurun.

## 🔍 Birlikte Keşfedelim

Sanal makinenizi veya canlı USB'nizi başlatın. Her biri için aşağıdaki gözlemleri yapın:

1. **Linux Mint (Debian tabanlı):** Linux Mint, Debian tabanlı bir dağıtım olduğundan `lsb_release -a` çıktısında Debian kökeni görünebilir. Menüyü gözlemleyin; `cat /etc/os-release` ile sürüm bilgilerini not edin.
2. **Fedora:** Paket yöneticisi (`dnf`) hangi komutlarla çalışıyor? `dnf list installed | head -n 5` ile kurulu paketleri listeleyin.
3. **CachyOS (Arch Linux tabanlı):** CachyOS, Arch Linux tabanlı bir dağıtım olduğundan `/etc/os-release` dosyasında `rollingg release` notunu gözlemleyin; `pacman -S` komutuyla paket kurulumu deneyin.

Tahmin edin: Üç dağıtım arasında aynı komut (`ls`, `pwd`) çalıştığında sonuç aynı mı olacaktır? Neden?

Şimdi her üç sistemde (veya en az birinde) `ls -la /` komutunu çalıştırın ve çıktıları karşılaştırın.

## 🛠️ Uygulama

Aşağıdaki görevleri sırasıyla tamamlayın:

1. Sanal makinenize yeni bir dağıtım ISO'su bağlayın (örneğin Fedora veya Debian).
2. Kurulumu başlatın; disk yapılandırmasında "Otomatik bölümleme" seçeneğini tercih edin.
3. Kurulum tamamlandığında terminal açın ve `uname -a` ile çekirdek sürümünü not edin.
4. `cat /etc/os-release` ile dağıtım bilgilerini kaydedin.
5. Her bir sistemde bir dosya oluşturun (`touch fark.md`) ve `ls -l fark.md` ile izinleri karşılaştırın.

## 🧪 Deneyelim ve Gözlemleyelim

Deneyleri yapın ve sonuçları not edin:

1. **Paket kurulum farkı:** Linux Mint (Debian tabanlı) `sudo apt install curl`, Fedora `sudo dnf install curl`, CachyOS (Arch tabanlı) `sudo pacman -S curl` komutlarını deneyin. Her iki komutun da başarıyla çalışıp çalışmadığını gözlemleyin.
2. **Güncelleme farkı:** `sudo apt update` (Ubuntu/Debian) ve `sudo dnf upgrade` (Fedora) komutlarını çalıştırın. Çıktılardaki farklılıkları not edin.
3. **Masaüstü farkı:** Her sistemde açık olan uygulamaları (`ls /usr/share/applications/` veya menüden) listeleyin; ortak olanları işaretleyin.

> [!WARNING]
> Farklı dağıtımları aynı fiziksel diske kurarken dikkatli olun. Yanlış bölümleme veri kaybına neden olabilir. Bu deney için sanal makine kullanmanız en güvenli yöntemdir.

## Bir Şeyler Ters Giderse

Farklı dağıtım kurulumunda karşılaşabileceğiniz sorunlar:

1. **ISO bağlanmıyor:** Sanal makine ayarlarında "Depolama" bölümünü kontrol edin (Hafta 1'deki VirtualBox adımlarına bakın).
2. **Kurulum ekranı gelmiyor:** UEFI/BIOS ayarlarında güvenli önyükleme (Secure Boot) kapatılabilir veya ISO dosyasının bütünlüğü kontrol edilebilir.
3. **Ağ bağlantısı yok:** Sanal makine ağ ayarının "NAT" veya "Köprü" modunda olduğundan emin olun.

> [!TIP]
> Bir dağıtım kurulumunda hata alırsanız, hata mesajını arama motorunda aramak yerine önce `man` komutuyla ilgili aracı kontrol edin; bu hem öğrenmenizi hem de sorun giderme becerinizi geliştirir.

## Kendin Dene

Aşağıdaki görevleri tamamlayın:

1. Üç dağıtım arasında bir karşılaştırma tablosu oluşturun; her birinin paket yöneticisi, varsayılan masaüstü ve hedef kitlesini yazın.
2. Kendi sisteminizde `lsb_release -a` (veya `cat /etc/os-release`) komutuyla hangi dağıtımı kullandığınızı belirleyin.
3. `sudo apt list --installed` (Ubuntu/Debian) veya `dnf list installed` (Fedora) ile kurulu paket sayısını karşılaştırın.

<details>
<summary>Cevapları göster</summary>

1. Karşılaştırma tablosu: Linux Mint (Debian tabanlı: apt, kararlı, sunucu/başlangıç), Fedora (dnf, GNOME, geliştirici), CachyOS (Arch Linux tabanlı: pacman, rolling, ileri kullanıcı).
2. Çıktı kendi sisteminizin dağıtım adını gösterir.
3. Paket sayısı sistemden sisteme değişir; sadece göreli bir karşılaştırma yapın.

</details>

## 🧠 Öğrendiklerini Kontrol Et

1. Ubuntu ile Fedora arasındaki temel paket yönetimi farkı nedir?
2. Debian Stable'in güncelleme politikası neden daha yavaştır?
3. Sanal makine kullanmanın avantajı nedir?

<details>
<summary>Cevapları göster</summary>

1. Ubuntu `apt`, Fedora `dnf` kullanır; komut sözdizimi biraz farklıdır.
2. Debian Stable, kararlılık için yeni özellikleri geciktirir; güncellemeler güvenlik düzeltmeleri ile sınırlıdır.
3. Sanal makine, gerçek diski etkilemeden deneme yapmanızı sağlar; veri kaybı riski yoktur.

</details>

## Bağımsız Çalışma

Kendi sisteminizde bu bağımsız çalışmayı yapın:

- Mevcut Linux sisteminizde `cat /etc/os-release` ile dağıtım bilgilerini not edin.
- `lsb_release -d` komutuyla dağıtım açıklamasını öğrenin (varsa).
- Bir sanal makine kurup, bu derste karşılaştırılan üç dağıtımdan birini yükleyin. Kurulum sonrası `uname -a`, `cat /etc/os-release` ve `ls -l /etc` komutlarını çalıştırın; sonuçları defterinize yazın.

## Daha Fazlasını Öğrenmek

- Debian Wiki — Dağıtım karşılaştırması: [https://wiki.debian.org/Choosing](https://wiki.debian.org/Choosing)
- Fedora projesi: [https://fedoraproject.org/](https://fedoraproject.org/)
- Ubuntu: [https://ubuntu.com/](https://ubuntu.com/)

## Kısa Özet

Bu derste üç başlıca Linux dağıtımını karşılaştırdınız: Linux Mint (Debian tabanlı: apt, kararlı, sunucu), Fedora (dnf, güncel, geliştirici) ve CachyOS (Arch Linux tabanlı: pacman, sürekli güncelleme, ileri kullanıcı). Her birinin paket yöneticisi (`apt`, `dnf`, `pacman`), güncelleme politikası ve hedef kitlesi arasındaki farkları anladınız. Bir sonraki derste masaüstü ortamlarını (GNOME, KDE, XFCE) deneyimleyeceğiz.

---

← [Kullanıcı Yönetimi ve İzinler](03-User-Management.md) | [Masaüstü Ortamları →](05-Desktop-Environments.md)
