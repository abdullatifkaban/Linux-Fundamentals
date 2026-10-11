# Ağ Temelleri

## 🎯 Bu Derste Ne Öğreneceğiz?

Bu derste Linux sisteminde ağ bağlantısını, IP adresini ve temel ağ komutlarını (`ping`, `ip`, `ifconfig`/`ip addr`) öğreneceksiniz. Ayrıca ağ yapılandırmasının sistem çalışması üzerindeki etkisini gözlemleyeceksiniz.

## 💡 Neden Bu Konuyu Öğreniyoruz?

Veri biliminde veri transferi, sunucu erişimi ve harici kaynaklardan veri çekme sürekli yapılır. Ağ hatalarını anlamak ve temel ağ komutlarını kullanmak, sisteminizin bağlantı durumunu hızlıca kontrol etmenizi sağlar.

> [!NOTE]
> IP adresi, cihazın ağda tanınmasını sağlar. `127.0.0.1` her zaman kendi bilgisayarınızı temsil eder (döngüsel/localhost adresi).

## Ön Bilgi

Temel komutları (`ls`, `pwd`, `cd`) ve paket yönetimini (Hafta 6) bilmek yeterlidir.

## Kavramlar

### IP Adresi ve Ağ Arayüzü

Linux'ta ağ arayüzleri `lo` (loopback), `eth0`, `wlan0` gibi isimlerle tanımlanır.

### Temel Ağ Komutları

| Komut | Amaç |
|---|---|
| `ip addr` | Ağ arayüzleri ve IP'leri listele |
| `ping` | Bağlantı testi |
| `ip route` | Yönlendirme tablosu |

## 🔍 Birlikte Keşfedelim

1. `ip addr` çalıştırın; `lo` ve diğer arayüzleri not edin.
2. `ping -c 3 8.8.8.8` komutuyla Google DNS'e bağlanmayı test edin.
3. `ip route` ile varsayılan ağ geçidini gözlemleyin.

Tahmin edin: `ping` başarısız olursa sistemdeki sorun nerede olabilir?

## 🛠️ Uygulama

1. `ip addr show` ile IP'lerinizi yazın.
2. `ping google.com` çalıştırın.
3. `cat /etc/resolv.conf` ile DNS ayarlarını görüntüleyin.

## 🧪 Deneyelim ve Gözlemleyelim

- `ping -c 1 127.0.0.1` çalıştırın; `lo` arayüzünün kendi sisteminiz olduğunu doğrulayın.
- Ağ bağlantısını geçici olarak kapatıp (`ip link set lo down`) tekrar açın; dikkatli olun.

> [!WARNING]
> `ip link set` komutuyla aktif ağ arayüzünü kapatmak bağlantıyı keser; sadece `lo` ile deneyin.

## Bir Şeyler Ters Giderse

1. `ping 8.8.8.8` başarısızsa önce `ip addr` ile IP'nin var olduğunu kontrol edin.
2. DNS sorunu varsa `/etc/resolv.conf` içeriğini kontrol edin.
3. Ağ arayüzü yoksa `ip link` ile arayüz isimlerini listeleyin.

## Kendin Dene

1. `ip addr` çıktısını bir metin dosyasına yazın (`ip addr > /tmp/ag_bilgi.txt`);
2. `cat /tmp/ag_bilgi.txt` ile içeriği görüntüleyin.
3. `ping` ve `ip` komutlarını karşılaştırarak hangi komutun ne işe yaradığını açıklayın.

<details>
<summary>Cevapları göster</summary>

1. `/tmp/ag_bilgi.txt` oluşturulur.
2. Çıktı IP ve arayüz bilgilerini içerir.
3. `ping` bağlantı testi; `ip` arayüz/rota bilgisi verir.

</details>

## 🧠 Öğrendiklerini Kontrol Et

1. `ip addr` ne işe yarar?
2. `127.0.0.1` nedir?
3. `ping` başarısız olursa ilk kontrol ne olmalıdır?

<details>
<summary>Cevapları göster</summary>

1. Ağ arayüzleri ve IP adreslerini listeler.
2. Yerel döngüsel adres (localhost).
3. `ip addr` ile IP varlığı; ardından DNS (`/etc/resolv.conf`).

</details>

## Bağımsız Çalışma

- `ip addr` çıktısını kaydedin.
- Ağ bağlantısını `ping` ile test edin; sonuçları not edin.
- `ip route` ile varsayılan geçidi yazın.

## Daha Fazlasını Öğrenmek

- Linux Ağ Yönetimi: `man ip`
- Ağ yapısı kavramı: [`iproute2`](https://wiki.linuxfoundation.org/networking/iproute2)

## Kısa Özet

Ağ temellerini öğrendiniz: IP adresleri, arayüzler, `ping`, `ip` komutları. Bir sonraki derste disk bölümleme konularına geçeceğiz.

---

← [Paket Yönetimi](06-Package-Management.md) | [Disk Bölümleme →](08-Disk-Partitioning.md)
