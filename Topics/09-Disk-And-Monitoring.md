# Disk, Donanım ve Sistem İzleme

## 🎯 Bu Bölümde Ne Öğreneceğiz?

Bu bölümü bitirdiğinde şunları yapabileceksin:

- Disk, bölüm (partition), dosya sistemi ve bağlama (mount) kavramlarını
  açıklayabileceksin.
- `df` ve `du` ile disk kullanımını inceleyebileceksin.
- `lsblk` ve `mount` ile diskleri ve bağlı dosya sistemlerini listeleyebileceksin.
- `free` ile bellek, `uname` ve `lscpu` ile sistem ve işlemci bilgilerini
  okuyabileceksin.
- `lspci` ve `lsusb` ile donanımı tanıyabileceksin.
- `journalctl` ve `/var/log` ile sistem günlüklerini inceleyebileceksin.

## 💡 Neden Bu Konuyu Öğreniyoruz?

Bir sistemin sağlığını anlamak için üç sorunun cevabını bilmen gerekir: Disk
doluyor mu, bellek yetiyor mu, donanım tanınıyor mu? Bu soruların cevabı yoksa,
"bilgisayar yavaşladı" ya da "program açılmıyor" gibi şikâyetler havada kalır.

Bir de günlükler var: Sistem, olan biteni sessizce bir yere kaydeder. Bir hata
çıktığında o kayıtlar, sorunun gerçek nedenini gösteren en iyi ipucudur. Bu
bölüm, sistemi "önce gözlemle, sonra karar ver" yaklaşımıyla incelemeni sağlar.

## 📌 Ön Bilgi

Bu bölüm, 8. bölümdeki süreç ve servis bilgisine dayanır; bir servisin sorununu
bu kez günlükler üzerinden inceleyeceğiz. Ayrıca 4. bölümdeki boru ve `grep`
kullanımı, günlükleri süzerken çok işine yarayacak.

## 📖 Kavramlar

### Disk, bölüm ve dosya sistemi

Fiziksel bir **disk (disk)**, veriyi saklayan donanımdır. Bu disk, **bölümlere
(partition)** ayrılabilir; her bölüm bağımsız bir alan gibi davranır. Bir
bölümün kullanılabilmesi için üzerine bir **dosya sistemi (file system)**
kurulur. Dosya sistemi kurulduktan sonra bölüm, dizin ağacındaki bir noktaya
**bağlanır (mount)**. Örneğin kök dosya sistemin (`/`) bir bölüme bağlıdır.

```mermaid
flowchart LR
    A["Fiziksel disk"] --> B["Bölümler"]
    B --> C["Dosya sistemi"]
    C --> D["Bağlama noktası (/, /home ...)"]
```

Bu zincir, "diskteki boş alan" ile "kullanabildiğin klasör" arasındaki yolu
gösterir. `/home` ayrı bir bölüme bağlıysa, kişisel dosyaların farklı bir fiziksel
alandadır.

### Günlük (log)

**Günlük (log),** sistemin ve servislerin yaptıkları işleri, uyarıları ve
hataları kaydettiği metinlerdir. Modern sistemlerde günlükler genellikle
`/var/log` altında ya da systemd'nin günlük aracıyla (journal) tutulur.

## 🔍 Birlikte Keşfedelim

Sence kök dosya sisteminin ne kadarı dolu? Yüzde 20 mi, yüzde 50 mi, yüzde 80
mi?

Tahminini netleştirdikten sonra şu komutu çalıştır:

```bash
df -h
```

`df` (disk free), bağlı dosya sistemlerinin kullanımını gösterir; `-h` seçeneği
sonucu insan okuyabilir biçimde (GB, MB) yazar. Çıktıda `Use%` sütununa bak:
kök dosya sisteminin doluluk oranını görürsün.

Sistemin **tüm diski değil, bağlı dosya sistemlerini** gösterdiğine dikkat et.
Yani bir disk birden çok satırda görünebilir. Şimdi disklerin ham hâline bak:

```bash
lsblk
```

`lsblk`, diskleri ve bölümlerini ağaç biçiminde listeler. `df` "kullanımdaki
alanı", `lsblk` ise "disklerin yapısını" gösterir; ikisi farklı sorulara cevap
verir.

## 🛠️ Uygulama

### 1. Adım: Disk kullanımını ölç

```bash
df -h
du -sh ~
du -sh ~/linux_deneme
```

- `df -h`, tüm bağlı dosya sistemlerinin durumunu özetler.
- `du -sh ~`, ev dizininin toplam boyutunu verir. `-s` özet (summary), `-h`
  okunabilir boyut demektir.

Belirli bir dizinde en çok yer kaplayan ögeleri bulmak için bir boru hattı
kurabiliriz:

```bash
du -h ~ --max-depth=1 | sort -h
```

Bu komut, ev dizinindeki alt dizinlerin boyutlarını hesaplar ve küçükten büyüğe
sıralar. Böylece diskini en çok tüketen klasörü hızlıca bulabilirsin.

### 2. Adım: Bellek ve işlemci bilgisini oku

```bash
free -h
uname -a
lscpu
```

- `free -h`, belleğin ne kadarının kullanıldığını gösterir.
- `uname -a`, çekirdek sürümü ve mimari gibi sistem bilgilerini verir.
- `lscpu`, işlemcinin çekirdek sayısı, mimarisi gibi ayrıntılarını listeler.

### 3. Adım: Donanımı tanı

```bash
lspci
lsusb
```

- `lspci`, PCI veri yoluna bağlı donanımları (ekran kartı, ağ kartı, ses kartı)
  listeler.
- `lsusb`, USB cihazlarını listeler.

Bir cihazın tanınıp tanınmadığını anlamak istediğinde bu iki komut ilk
başvurduğun araçlardır.

### 4. Adım: Günlükleri incele

```bash
journalctl -b
```

`journalctl -b`, sistemin **bu açılıştan bu yana** ürettiği günlükleri gösterir.
Çıktı uzun olabilir; sayfa sayfa gezinmek için boşluk tuşunu, çıkmak için `q`
kullan. Yalnızca hata düzeyindekileri görmek için:

```bash
journalctl -b -p err
```

Günlükleri boru ve `grep` ile süzmek de mümkündür:

```bash
journalctl -b | grep -i "error"
```

Klasik günlük dosyalarına da bakabilirsin:

```bash
ls /var/log
tail -n 20 /var/log/syslog
```

`tail`, dosyanın son satırlarını gösterir; bir günlüğün en yeni kayıtları
genellikle en sonda olduğu için `tail` sık kullanılır.

> [!TIP]
> Bir hata aldığında önce tam olarak ne zaman olduğunu not et; sonra
> `journalctl` çıktısını o zamana yakın satırlarda incele. Günlükler, "ne
> oldu?" sorusunun en dürüst cevabını verir.

## 🧪 Deneyelim ve Gözlemleyelim

Disk ile bellek kullanımının birbirinden bağımsız olduğunu gözlemleyelim.

```bash
free -h
df -h /
```

Şimdi birkaç program aç (tarayıcı, metin düzenleyici) ve iki komutu tekrar
çalıştır. Bellek kullanımının arttığını, ama disk doluluğunun büyük ölçüde aynı
kaldığını göreceksin.

Sistemi yeniden başlatıp `free -h` çıktısını bir daha incele. Bellek kullanımı
önemli ölçüde düştü mü? Bu, bellek kullanımının geçici olduğunu, diskin ise
kalıcı olduğunu gösterir. "Bilgisayarım yavaşladı" dendiğinde bu ikisinin
hangisinin dolu olduğunu ayırt etmek kritik olur.

## ⚠️ Bir Şeyler Ters Giderse

**Belirti:** Kök dosya sistemin (`/`) neredeyse tamamen dolu (yüzde 90'ın
üzerinde).

**Olası neden:** Büyük dosyalar, biriken günlükler ya da temizlenmeyen geçici
dosyalar (`/tmp`, önbellekler).

**Ne yapmalısın:** `du -h --max-depth=1 /` ile hangi üst dizinin yer
kapladığını bul. Genellikle ev dizini, önbellekler ya da günlükler baş sorumludur.
Silmeden önce ne olduğunu mutlaka anla.

**Belirti:** `lspci` ya da `lsusb` bir cihazı listelemiyor; cihaz çalışmıyor.

**Olası neden:** Cihaz tanınmamış ya da sürücüsü yüklü değil.

**Ne yapmalısın:** Cihazın adını not et ve sürücü durumunu araştır. Sanal
makinede çalışıyorsan bazı cihazlar sanal olarak sunulmaz; bu normaldir.

**Belirti:** `journalctl` çok uzun çıktı veriyor, aradığını bulamıyorsun.

**Ne yapmalısın:** Zaman aralığı ve önem düzeyi filtrelerini kullan
(`-p err`, `--since "10 min ago"` gibi) ya da çıktıyı `grep` ile süz.

## ✍️ Kendin Dene

**Görev:** Ev dizinindeki en büyük üç klasörü boyutlarıyla birlikte bul. Sonra
kök dosya sistemindeki hata düzeyindeki günlükleri listeleyip bunlardan birini
cümlelerinle açıkla.

<details>
<summary>İpucu göster</summary>

Klasörleri boyuta göre sıralamak için `du -h ~ --max-depth=1 | sort -h`
komutunu kullanabilirsin. Hata günlükleri için `journalctl -b -p err`.

</details>

<details>
<summary>Örnek çözüm göster</summary>

```bash
du -h ~ --max-depth=1 | sort -h | tail -n 4
journalctl -b -p err
```

İlk komut, ev dizinindeki ögeleri boyuta göre sıralayıp en büyük üçünü (artı
toplam satırı) gösterir. İkinci komut, bu açılışta üretilen hata düzeyindeki
günlükleri listeler. İkinci komutun çıktısında çıkan bir satırı seçip "bu satır
şu servisin şu sorununu anlatıyor" diye kendi cümlelerinle özetle.

</details>

## 🧠 Öğrendiklerini Kontrol Et

1. Disk, bölüm ve dosya sistemi kavramlarını birbirinden ayır.
2. `df` ile `du` arasındaki fark nedir?
3. `free -h` ve `uname -a` ne tür bilgiler verir?
4. Bir USB cihazının sistem tarafından tanınıp tanınmadığını hangi komutla
   kontrol edersin?
5. `journalctl` ne işe yarar ve bir sorunu incelerken neden faydalıdır?

<details>
<summary>Cevapları göster</summary>

1. Disk fiziksel saklama aygıtıdır; bölüm disk üzerindeki ayrılmış alandır;
   dosya sistemi ise o bölümün nasıl düzenlendiğini tanımlayan yapıdır.
2. `df` bağlı dosya sistemlerinin kullanım oranını/boş alanını gösterir; `du`
   belirli dosya ya da dizinlerin kapladığı alanı hesaplar.
3. `free -h` bellek kullanımını; `uname -a` çekirdek sürümü ve mimari gibi
   sistem bilgilerini verir.
4. `lsusb`.
5. `journalctl`, systemd tarafından tutulan sistem günlüklerini gösterir.
   Sorunun ne zaman ve hangi serviste oluştuğunu ortaya koyduğu için sorun
   gidermede çok değerlidir.

</details>

## 🚀 Bağımsız Çalışma

1. **Gözlem görevi:** `lsblk` çıktısındaki bölümleri incele. Kök dosya sistemi
   hangi bölümde? Ev dizinin ayrı bir bölümde mi, yoksa kökle aynı bölümde mi?
   `df -h` çıktısıyla karşılaştırarak cevapla.
2. **Araştırma görevi:** `journalctl` komutunun `--since` seçeneğini araştır ve
   "son 10 dakikadaki günlükleri" listeleyen bir komut yaz.

Bu görevler, sistemi bütüncül okuma ve günlüklerden sonuç çıkarma becerisi
kazandırır.

## 📚 Daha Fazlasını Öğrenmek

- GNU coreutils kılavuzu (df, du): <https://www.gnu.org/software/coreutils/manual/>
- util-linux (lsblk, mount): <https://en.wikipedia.org/wiki/Util-linux>
- systemd journal belgeleri: <https://www.freedesktop.org/wiki/Software/systemd/journal/>
- Ubuntu man sayfaları: <https://manpages.ubuntu.com>

## 📝 Kısa Özet

- Disk, bölüm, dosya sistemi ve bağlama noktası bir zincir oluşturur.
- `df` ve `du` disk kullanımını farklı açılardan ölçer; `lsblk` disk yapısını
  gösterir.
- `free`, `uname` ve `lscpu` sistem ile bellek bilgilerini verir.
- `lspci` ve `lsusb` donanımı tanır.
- `journalctl` ve `/var/log` günlükleri sunar; sorun gidermenin en güvenilir
  kaynağıdır.

[Önceki bölüm: Süreç ve Servis Yönetimi](08-Process-And-Services.md) | [İçindekiler](../README.md) | [Sonraki bölüm: Ağ Temelleri](10-Networking-Basics.md)
