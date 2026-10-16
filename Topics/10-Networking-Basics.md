# Ağ Temelleri

## 🎯 Bu Bölümde Ne Öğreneceğiz?

Bu bölümü bitirdiğinde şunları yapabileceksin:

- IP adresi, arayüz, ağ geçidi ve DNS kavramlarını açıklayabileceksin.
- `ip` komutuyla ağ arayüzlerini ve yollarını inceleyebileceksin.
- `ping` ve `tracepath` ile bağlantıyı test edebileceksin.
- `hostname` ve `/etc/hosts`, `/etc/resolv.conf` dosyalarının işlevini
  anlayacaksın.
- Kablosuz ağ bağlantısını arayüz üzerinden yönetmeyi görebileceksin.
- "İnternete bağlanamıyorum" sorununa yöntemli biçimde yaklaşabileceksin.

## 💡 Neden Bu Konuyu Öğreniyoruz?

Bugün neredeyse her şey ağ üzerinden çalışır: güncellemeler, web, dosya
paylaşımı. Ağ kesildiğinde bir kullanıcı genellikle tamamen çaresiz kalır.
Oysa sorunun nerede olduğunu adım adım bulmak mümkündür: kablo mu, arayüz mü,
ağ geçidi mi, yoksa isim çözümleme (DNS) mı?

Ağ temellerini bilmek, seni "modemi kapat aç" düzeyinden çıkarıp sorunu
gerçekten teşhis eden bir kullanıcı hâline getirir. Bu, Linux becerilerinin en
pratik kazanımlarından biridir.

## 📌 Ön Bilgi

Bu bölüm, 9. bölümde öğrendiğin sistem inceleme yaklaşımına dayanır: önce
gözlemlersin, sonra karar verirsin. Ayrıca `/etc` altındaki yapılandırma
dosyalarını (3. bölüm) okuyacağız; bunun için `cat` komutunu kullanacağız.

## 📖 Kavramlar

### Arayüz ve IP adresi

Bir bilgisayarın ağa katılması için bir **ağ arayüzüne (network interface)**
ihtiyacı vardır. Kablolu ağ için `eth0` benzeri, kablosuz için `wlan0` benzeri
adlar kullanılır. Her arayüzün ağdaki adresi **IP adresidir**. Yaygın biçim
`192.168.1.42` gibi dört sayıdır. Ayrıca `127.0.0.1` özel bir adrestir ve
"bilgisayarın kendisi" anlamına gelir; buna **localhost** denir.

### Ağ geçidi ve yönlendirme

Kendi ağının dışına (örneğin internete) çıkmak için bir **ağ geçidine
(gateway)** ihtiyaç vardır. Genellikle modem ya da router bu görevi üstlenir.
Bilgisayarın "bu adrese nasıl giderim?" sorusuna **yönlendirme tablosu (routing
table)** cevap verir.

### DNS ve isim çözümleme

Biz `www.ornek.com` gibi **isimler** kullanırız; ama ağ, adresleri kullanır. Bu
isimleri IP adreslerine çeviren sisteme **DNS (Domain Name System)** denir.
DNS çalışmazsa, internet bağlantın var olsa bile siteleri isimle açamazsın.

```mermaid
flowchart LR
    A["www.ornek.com yazdın"] --> B["DNS sunucusu sorulur"]
    B --> C["IP adresi bulunur"]
    C --> D["Sunucuya bağlanılır"]
```

Internet bağlantısının çalışıp çalışmadığını test etmek için genellikle
`ping` kullanılır; bu komut hedefe küçük paketler gönderip yanıt bekler.

## 🔍 Birlikte Keşfedelim

Sence bilgisayarının kendi içindeki adresi var mı? Yani bilgisayarın kendisiyle
"konuşabilir" mi?

Tahminini netleştirdikten sonra şu komutları çalıştır:

```bash
ip a
ping -c 4 127.0.0.1
```

`ip a` ağ arayüzlerini ve adreslerini listeler. `ping -c 4 127.0.0.1` ise
bilgisayarın kendisine dört paket gönderir. Yanıt geliyorsa, ağ yığınının temel
katmanı çalışıyor demektir; çünkü bilgisayar kendi kendine ulaşabiliyor.

Şimdi kendi ağ geçidini bul ve onu test et:

```bash
ip route
ping -c 4 <ag_gecidi_ip>
```

`ip route` çıktısındaki `default via` satırı ağ geçidini gösterir. Bu adresi
`ping` ile test ettiğinde, yerel ağın çalıştığını doğrulamış olursun. Bu iki
adım, "sorun yerel ağda mı, yoksa dışarıda mı?" sorusunu ayırt etmenin temelidir.

## 🛠️ Uygulama

### 1. Adım: Ağ arayüzlerini incele

```bash
ip a
```

Her arayüzün yanında `state UP` ya da `state DOWN` yazısını, altında da
`inet` ile başlayan IP adresini göreceksin. `lo` arayüzü, localhost'u temsil eden
özel arayüzdür.

### 2. Adım: Yönlendirme tablosunu oku

```bash
ip route
```

`default via ...` satırı, dışarı çıkış kapını (ağ geçidini) gösterir. Diğer
satırlar yerel ağla ilgili bilgilerdir.

### 3. Adım: Bağlantıyı test et

```bash
ping -c 4 8.8.8.8
ping -c 4 linuxmint.com
```

İlki bir IP adresine, ikincisi bir isme ping atar. İkisi arasındaki fark bize
DNS'i test etme imkânı verir. Ardından yolu izle:

```bash
tracepath linuxmint.com
```

`tracepath`, hedefe giden yol üzerindeki durakları (router'ları) listeler.
Bazı sistemlerde bu araç `traceroute` adıyla bulunur. Amaç, paketin hangi
noktalardan geçtiğini görmektir.

### 4. Adım: İsim çözümleme dosyalarını incele

```bash
hostname
cat /etc/hosts
cat /etc/resolv.conf
```

- `hostname`, bilgisayarının ağdaki adını verir.
- `/etc/hosts`, elle tanımlanmış isim-adres eşleşmelerini içerir; DNS'ten önce
  buraya bakılır.
- `/etc/resolv.conf`, hangi DNS sunucularının kullanılacağını gösterir.

### 5. Adım: Kablosuz bağlantıyı yönet

Linux Mint'te kablosuz ağları çoğunlukla sağ alttaki ağ simgesinden yönetirsin.
Terminalden yönetmek için `nmcli` (NetworkManager komut satırı aracı)
kullanılabilir:

```bash
nmcli device status
nmcli connection show
```

İlk komut, aygıtların bağlantı durumunu; ikincisi tanımlı bağlantı profillerini
listeler. Bu araç, arayüzü olmayan ortamlarda (örneğin bir sunucuda) ağ
yönetmenin yoludur.

> [!TIP]
> Bir ağ sorununu araştırırken şu sırayı izle: 1) `ip a` ile arayüz ayakta mı?
> 2) `ping` ile ağ geçidine ulaşabiliyor musun? 3) IP adresine ping atabiliyor
> musun? 4) İsme ping atabiliyor musun? Bu sıra, sorunun hangi katmanda
> olduğunu hızla daraltır.

## 🧪 Deneyelim ve Gözlemleyelim

DNS ile IP bağlantısını ayırt edelim.

```bash
ping -c 2 8.8.8.8
ping -c 2 ornek-olmayan-site.test
```

İlk komut, IP adresine doğrudan ulaşmaya çalışır; genellikle çalışır. İkinci
komut ise var olmayan bir isme ulaşmaya çalışır ve "isim çözümlenemedi"
benzeri bir hata verir. Bu, "internetim var ama siteler açılmıyor" durumunun
genellikle bir DNS sorunu olduğunu gösterir.

Şimdi `/etc/hosts` dosyasına geçici bir satır ekleyerek isim çözümlemenin
önceliğini gözlemleyebilirsin (bu değişikliği sonra geri al):

```bash
sudo nano /etc/hosts
# sona şu satırı ekle:  127.0.0.1 kendi_sitem.test
```

Kaydedip çıktıktan sonra `ping -c 2 kendi_sitem.test` komutunu dene ve
`127.0.0.1`e gittiğini gör. `/etc/hosts`, DNS'ten önce okunduğu için isim artık
yerel olarak çözümlenir. İşin bitince eklediğin satırı silmeyi unutma.

## ⚠️ Bir Şeyler Ters Giderse

**Belirti:** Hiçbir site açılmıyor.

**Ne yapmalısın:** Sırayla test et: `ip a` ile arayüz ayakta mı, `ip route` ile
ağ geçidi var mı, `ping` ile ağ geçidine ulaşıyor musun, `ping 8.8.8.8` çalışıyor
mu, `ping linuxmint.com` çalışıyor mu? Bu sıra, sorunu adım adım daraltır.

**Belirti:** IP adreslerine ulaşabiliyorsun ama isimler çözümlenmiyor.

**Olası neden:** DNS sorunu. `/etc/resolv.conf` boş ya da yanlış sunucu
gösteriyor olabilir.

**Ne yapmalısın:** `/etc/resolv.conf` içeriğini kontrol et. Kablosuz bağlantıyı
yöneten araç genellikle bu dosyayı otomatik doldurur; elle değiştirdiysen geri
al.

**Belirti:** Sanal makinede internet yok ama ana makinede var.

**Olası neden:** Sanal makinenin ağ ayarı yanlış olabilir (örneğin NAT yerine
"not attached" seçili).

**Ne yapmalısın:** Sanal makine ayarlarında "Network" bölümünü kontrol et;
genellikle "NAT" ya da "Bridged Adapter" seçili olmalıdır.

## ✍️ Kendin Dene

**Görev:** İnternet bağlantını üç katmanlı bir testle doğrula: yerel arayüz,
ağ geçidi ve dış dünya. Her katman için bir komut seç ve çıktısını yorumla.

<details>
<summary>İpucu göster</summary>

Katmanlar: `ip a` (arayüz), `ping <ag_gecidi>` (yerel ağ), `ping 8.8.8.8` (dış
IP), `ping linuxmint.com` (DNS). Son iki adımın farkı DNS'i sınar.

</details>

<details>
<summary>Örnek çözüm göster</summary>

```bash
ip a                 # arayüz ayakta mı? IP aldı mı?
ip route             # ağ geçidi nedir?
ping -c 4 8.8.8.8    # dışarıya IP ile ulaşabiliyor musun?
ping -c 4 linuxmint.com   # isimleri çözümleyebiliyor musun?
```

Dördü de başarılıysa ağ sağlıklıdır. Yalnızca son komut başarısızsa sorun
DNS'tedir. Bu tür bir testi ezberlemek yerine mantığını kavramak, her ağ
sorununda işine yarar.

</details>

## 🧠 Öğrendiklerini Kontrol Et

1. IP adresi nedir ve `127.0.0.1` neyi ifade eder?
2. Ağ geçidi ne işe yarar?
3. DNS nedir ve çalışmadığında ne olur?
4. `ping 8.8.8.8` çalışıp `ping linuxmint.com` çalışmıyorsa sorun nerededir?
5. `/etc/hosts` ile `/etc/resolv.conf` arasındaki fark nedir?

<details>
<summary>Cevapları göster</summary>

1. IP adresi, bir arayüzün ağdaki sayısal adresidir. `127.0.0.1` ise
   bilgisayarın kendisini (localhost) temsil eden özel adrestir.
2. Ağ geçidi, yerel ağın dışına çıkışı sağlayan cihazdır (genellikle modem ya
   da router).
3. DNS, alan adlarını IP adreslerine çevirir. Çalışmazsa IP ile ulaşabilsen de
   siteleri isimle açamazsın.
4. Sorun DNS'tedir; çünkü IP ile dış dünyaya ulaşabiliyorsun ama isim
   çözümlenemiyor.
5. `/etc/hosts` elle tanımlanmış isim-adres eşleşmelerini içerir ve DNS'ten
   önce okunur; `/etc/resolv.conf` ise hangi DNS sunucularının kullanılacağını
   belirtir.

</details>

## 🚀 Bağımsız Çalışma

1. **Gözlem görevi:** `ip a` çıktısındaki her arayüz için "bu hangi amaçla
   kullanılıyor?" sorusuna bir cümle yaz (`lo`, kablolu, kablosuz arayüzler).
2. **Araştırma görevi:** Yerel ağındaki başka bir cihazın IP adresini bulmayı
   dene (örneğin modem arayüzünden) ve ona `ping` at. Yerel ağ ile dış ağ
   arasındaki farkı deneyimle.

Bu görevler, ağ kavramlarını soyut bilgi olmaktan çıkarıp kendi ortamında
gözlemlemene yardımcı olur.

## 📚 Daha Fazlasını Öğrenmek

- Linux Mint ağ belgeleri: <https://linuxmint.com/documentation.php>
- NetworkManager projesi: <https://networkmanager.dev>
- Ubuntu man sayfaları (ip, ping, tracepath): <https://manpages.ubuntu.com>

## 📝 Kısa Özet

- Her arayüzün bir IP adresi vardır; `127.0.0.1` bilgisayarın kendisidir.
- Ağ geçidi, yerel ağın dışına çıkışı sağlar; `ip route` ile bulunur.
- DNS, isimleri IP adresine çevirir; bozulduğunda siteler isimle açılmaz.
- `ping` bağlantıyı, `tracepath` yolu, `nmcli` kablosuz bağlantıyı yönetir.
- Ağ sorunlarını katman katman (arayüz, ağ geçidi, dış IP, DNS) test etmek
  sorunu hızla daraltır.

[Önceki bölüm: Disk, Donanım ve Sistem İzleme](09-Disk-And-Monitoring.md) | [İçindekiler](../README.md) | [Sonraki bölüm: Ortam Değişkenleri, PATH ve Kabuk Yapılandırması](11-Environment-And-Path.md)
