# 01. Linux Temellerine Giriş

> 🎯 **Bu Modülün Amacı:** Linux'in temel kavramlarını ve Windows/macOS ile farkı anlamak. Linux Mint dağıtımını (Cinnamon) sanal makine ortamında kurmak, sistem güncellemelerini gerçekleştirmek ve en yaygın sanal makine hatalarını nasıl araştırıp çözeceğinizi öğrenmek.

---

## 1. Teori ve Mantık

### Linux Nedir?

Linux, 1991'de Fin asıllı öğrenci Linus Torvalds tarafından başlatılan, tamamen ücretsiz ve açık kaynaklı bir **işletim sistemi çekirdeğidir (kernel)**. Linux'ta "Linux" terimi sadece çekirdeği değil, aynı zamanda çekirdek etrafında toplanmış tüm araçları, uygulamaları ve yazılımları da kapsayan tam paketleri ifade eder. Bu tam paketler bizlerin **Linux Dağıtımı (Linux Distribution / Distro)** dediğimiz şeydir.

**🎯 Önemli Ayrım:** Linux tek başına sadece bir çekirdektir, ancak halk arasında "Linux" dendiğinde aslında tam bir işletim sistemi paketini (çekirdek + araçlar + masaüstü ortamı) kastederiz. Tıpkı "araba" denince motorun değil, tekerlekleri, direksiyonu ve koltuklarıyla birlikte tam aracın anlaşılması gibi.

### Açık Kaynak ve Özgür Yazılım Felsefesi

**Açık Kaynak (Open Source):**
- Yazılımın kaynak kodunun herkese açık olması ve herkesin inceleyebilmesi, değiştirebilmesi, üzerinde çalışabilmesi demektir.
- Temel amaç, işbirliği ve topluluk temelli yazılım geliştirmektir.
- Kaynak koduna sahip olan herkes bir hatayı fark edip düzeltebilir, özellik ekleyebilir veya sistemi kendi ihtiyacına göre özelleştirebilir.

> [!TIP]
> Bir yazılımın "ücretsiz" olması, "açık kaynak" olması anlamına gelmez. Açık kaynak kodları herkese açıktır, bu da yazılımın kim olursa olsun üzerinde çalışabileceği anlamına gelir. Özgür yazılım, yazılımı kullanım, araştırma, değiştirme ve dağıtma özgürlüğü sağlar.

**Özgür Yazılım (Free Software):**
- Kullanıcıların yazılımı özgürce kullanabilmesi, inceleyebilmesi, değiştirebilmesi ve dağıtabilmesi hakkını savunur.
- "Özgür" kelimesi ücretsiz anlamından ziyade **özgürlük** ile ilgilidir.
- Linus Torvalds'ın da dediği gibi: "Linux'i özgür kıldığımdan değil, özgür yazılım olduğu için Linux'i sevdiğimi" belirtmiştir.

**GNU/Linux İsmi:** Richard Stallman'in başlattığı GNU projesi ile Linus Torvalds'ın çekirdeğinin birleşmesiyle oluşan sistemi çoğu zaman "GNU/Linux" olarak adlandırırız. GNU projesi Linux'in üzerine gerekli araçları (shell, derleyici, kütüphaneler vb.) sağlar.

> [!IMPORTANT]
> Linux tamamen ücretsiz ve açık kaynaklıdır. İster kişisel kullanım, ister ticari kullanım, isterse de bir şirkette kullanım olsun hiçbir lisans ücreti ödemek zorunda değilsiniz.

**GNU/Linux Terimleri:**
- **Kernel (Çekirdek):** Sistemin temelini oluşturan, donanımı yöneten en kritik parça.
- **Dağıtım (Distro):** Kernel'i, yazılımları ve araçları tek bir paket halinde bir araya getiren organizasyon (Örn: Linux Mint, Ubuntu, Fedora).
- **Desktop Environment (Masaüstü Ortamı):** Kullanıcı arayüzünü ve uygulamalarını sunan katman (Örn: Cinnamon, GNOME, KDE Plasma).

### Linux ve Diğer İşletim Sistemleri Arasındaki Temel Farklar

| Özellik | Windows | macOS | Linux |
|---------|---------|-------|-------|
| Lisans Tipi | Özel mülkiyet (proprietary) | Özel mülkiyet (proprietary) | Açık kaynak (open source) |
| Özelleştirme | Sınırlı | Çok sınırlı | Uçsuz bucaksız |
| Ücretsiz Yazılım | Hayır | Hayır (donanım ile birlikte gelir) | Evet |
| Komut Satırı Erişimi | Sınırlı (PowerShell / CMD) | Sınırlı (Terminal / Bash) | Tam erişim (Bash, Zsh vb.) |
| Uygulama Desteği | En geniş uygulama desteği | Uygulama kalitesi yüksek | Güçlü ama uygulama çeşitliliği daha az |
| Destek Modeli | Microsoft destek, ücretli | Apple destek, ücretli | Topluluk destekli (forumlar, wiki, dokümantasyon) |
| Güncelleme Kontrolü | Otomatik ve zorunlu olabilir | Genelde kullanıcı onaylı | Tamamen kullanıcı kontrolünde |

> [!NOTE]
> **Windows/macOS ile temel zihniyet farkı:** Windows ve macOS, "sistemi yönetme" konusunda genellikle kullanıcıdan çok şey beklemez, arka plan işlemleri otomatik olarak halledilir. Linux'ta ise siz sistemde daha fazla söz sahibisiniz — ne isterseniz o kadar kontrol sizdedir. Bir Windows/macOS kullanıcısı için Linux ilk başta "fazla teknik" gelebilir ama bu aslında Linux'un en büyük gücüdür: sistemde istediğiniz her şeyi yapabilirsiniz.

### Araba Motoru Analojisi: Kernel, Dağıtım ve Masaüstü Ortamı

Sistemi anlamak için en iyi benzetme bir otomobil örneğidir:

**🚗 Arabanın Motoru = Kernel (Çekirdek)**
- Tüm sistemin temelini oluşturan en önemli parçadır.
- Motorun kendisi; yakıtı yönetir, güç üretir, motor kontrol ünitesini kontrol eder, lastiklere güç gönderir.
- Motoru çalıştırabilmek için benzin (enerji), yağ ve soğutma sisteminin olması gerekir — tıpkı kernel'in çalışabilmesi için donanım sürücülerinin olması gibi.
- **Hız, yakıt tüketimi ve performans kontrolü motorun işidir.** Kernel de sistemin hızını, donanım erişimini ve kaynak yönetimini kontrol eder.

**🚗 Arabanın Gövdesi = Dağıtım (Distro)**
- Motorun etrafındaki tüm bileşenleri bir araya getiren sistemdir.
- Şasi, frenler, elektronik kontrol birimi, yakıt sistemi, ısıtma/soğutma — hepsi gövdede bir araya gelir.
- Aynı motoru (kernel) farklı gövdelere (dağıtımlara) takabilirsiniz: Spor araba gövdesi (hızlı ve hafif, örn: Arch Linux), aile araba gövdesi (rahat ve kararlı, örn: Linux Mint), kamyon gövdesi (güçlü ve iş odaklı, örn: Ubuntu Server).
- **Aracın tüm bileşenleriyle uyumlu çalışması gövdenin işidir.** Dağıtım da kernel'i, araçları, yazılımları ve masaüstü ortamını bir araya getirip size hazır bir sistem sunar.

**🚗 Arabanın İç Donanımı ve Kabin = Masaüstü Ortamı (Desktop Environment)**
- Kullanıcıya hizmet eden tüm iç mekan ve kontrol panelidir.
- Direksiyon, vites, koltuklar, klima, gösterge paneli, radyo — hepsi bu kısımdır.
- Farklı iç donanımlar aynı arabada kullanılabilir: Spor koltuklar (KDE Plasma - çok özelleştirilebilir), lüks deri koltuklar (GNOME - modern ve sade), ergonomik koltuklar (Cinnamon - Windows benzeri).
- **Kullanıcıyla doğrudan etkileşim kuran tüm araçlar buradadır.** Linux Mint'te Cinnamon seçtiğiniz için Windows benzeri bir iç donanım (başlat menüsü, görev çubuğu, sistem tepsisi) elde edersiniz.

> [!TIP]
> Bir sanal makinede öğrenme yaparken "Linux Mint (Cinnamon)" seçmeniz, Windows 10/11'e alışkın bir kullanıcı için en konforlu iç donanımı seçmeniz gibidir. Farklı masaüstü ortamlarını da deneyebilirsiniz ama ilk etapta Cinnamon size tanıdık gelecektir.

### Sanal Makine Nedir?

Bir **sanal makine (Virtual Machine - VM)**, fiziksel bir bilgisayara benzer ancak aslında sadece o fiziksel bilgisayarın içinde çalışan, izole bir sanal ortamdır. Sanal makineler, fiziksel makinenizin kaynaklarını (RAM, CPU, disk alanı) bölmek ve her birine ayrı bir işletim sistemi kurarak çalıştırmak için kullanılır. VirtualBox, VMware, KVM gibi sanal makine yazılımları bu işi sağlar.

Sanal makine içinde çalışan işletim sistemi, fiziksel makinenizden **izole** olduğu için:
- İçinde ne yaparsanız yapın ana bilgisayarınıza hiçbir zarar veremezsiniz.
- Kurulum sırasında yaptığınız hatalar sadece sanal makineyi etkiler.
- İstediğiniz zaman "snapshot" (anlık durum kayıt) alabilir ve istediğiniz an eski haline dönebilirsiniz.

> [!WARNING]
> Sanal makine içinde yapılan her şey sadece o sanal makineye aittir. Ana bilgisayarınızdaki hiçbir dosyaya, programa veya ayara erişemezsiniz — bu bir güvenlik özelliğidir, aynı zamanda bir öğrenme koludur!

### Sanal Makine Öğrenmeye Neden Daha Güvenlidir?

| Madde | Fiziksel Sistem (Direct Boot) | Sanal Makine |
|------|------------------|--------------|
| Risk | Yüksek — hatalı bir komut disk bölümlerini bozabilir, sisteminiz açılmaz | Sıfır — her şey sanal ortamda kalır, ana sisteminiz dokunulmaz |
| Kurulum | Karmaşık, disk bölüntüleme ve boot yönetimi gerektirir | Basit — ISO dosyası seçip "Oluştur" yeterli |
| Silme / Yeniden Kurma | Zor — zaman alır, veri kaybı riski vardır | Kolay — sanal makineyi silmek ve yeniden oluşturmak birkaç dakika |
| Portatif | Sınırlı — aynı bilgisayarda çalışır | Taşınabilir — sanal makine dosyaları başka bir bilgisayarda da çalışır |
| Hata Ayıklama | Zor — sistem açılmayabilir, kurtarma zor | Çok kolay — "Snapshot" ile bir tuşla geri dönebilirsiniz |
| Eşzamanlı Kullanım | Bir seferde bir işletim sistemi | Aynı anda Windows/macOS ve Linux birlikte çalışır |

> [!CAUTION]
> İlk aşamada kesinlikle **fiziksel bilgisayara Linux kurmayın**. Sanal makine ile öğreniminizi tamamlayana kadar fiziksel disk bölümleriyle, boot menüleriyle veya dağıtım dosyalarıyla denemeler yapmayın. Sanal makine, hatalarınız için güvenli bir deneme alanıdır.

> [!NOTE]
> Birçok deneyimli yazılımcı ve sistem yöneticisi de günlük işlerini sanal makine içinde yapar. Sanal makine sadece "yeni başlayanlar için güvenli alan" değil, profesyonellerin de vazgeçilmez bir aracıdır.

---

## 2. Adım Adım Uygulama ve Deneyim

### A. Gerekli Araçları İndirme 

#### 1. Sanal Makine Yazılımını İndir ve Yükle

Sanal makine yazılımı olarak **Oracle VM VirtualBox** kullanacağız. VirtualBox, tamamen ücretsizdir, hem Windows hem macOS hem de Linux ana bilgisayarlarında çalışır ve topluluk tarafından sürekli güncellenir.

1. **İndirme:**
   > **📷 Görsel İpucu:** [VirtualBox resmi sitesi (virtualbox.org) açılırken tarayıcı adres çubuğunda "https://www.virtualbox.org/wiki/Downloads" yazıyor, sayfa yüklenince soldaki menüde "Downloads" seçeneğinin vurgulandığı ve sağ tarafta "VirtualBox 7.x.x Extensions" ile birlikte "VirtualBox 7.x.x platform packages" başlığı altında "Windows hosts" yazan yeşil indirme butonunun göründüğü ekran görüntüsü]
   ```
   https://www.virtualbox.org/wiki/Downloads
   ```

   > [!TIP]
   > **İndirme ipucu:** Ana bilgisayarınız Windows ise "Windows hosts", macOS ise "macOS hosts" bağlantısına tıklayın. Bu bağlantı doğrudan kurulum dosyasını indirir.

2. **Yükleme:**
   > **📷 Görsel İpucu:** [VirtualBox kurulum dosyası (VirtualBox-7-x-x-Windows.exe) masaüstünde veya İndirilenler klasöründe çift tıklandıktan sonra açılan Kurulum Sihirbazı penceresi; "Next" butonunun vurgulandığı ve kurulumun ilk ekranının göründüğü ekran görüntüsü]
   - VirtualBox kurulum dosyasını çift tıklayarak çalıştırın.
   - Açılan pencerede **"Next"** butonuna tıklayın.
   - Lisans sözleşmesi ekranında **"I Accept"** kutusunu işaretleyin ve tekrar **"Next"**e tıklayın.
   - Kurulum yolu ekranında varsayılan yolu kabul edip **"Install"** butonuna tıklayın.
   - Güvenlik uyarısı çıkarsa Windows/Mac güvenlik onayını verin.
   - Kurulum tamamlandığında **"Finish"** düğmesine tıklayın.

   > [!IMPORTANT]
   > **Kurulum ipucu:** Kurulum sırasında "VirtualBox Network Interfaces" gibi ek seçenekler çıkabilir — bunları varsayılan haliyle kabul etmek yeterlidir. VirtualBox kurulumu bilgisayarınızı değiştirmeyecek, sadece sanal makine yazılımını yükleyecektir.

   > [!TIP]
   > **Arama ipucu:** VirtualBox kurulumu sırasında bir sorun yaşarsanız (örneğin "Windows Security" uyarısı), Microsoft Store'dan gelen bir uyarı olabilir. "More info" → "Run anyway" seçeneğine tıklayarak kurulumu devam ettirebilirsiniz.

#### 2. Linux Mint ISO Dosyasını İndir

ISO dosyası, bir işletim sistemi kurulum medyasının (CD/DVD'nin) dijital kopyasıdır. Sanal makine yazılımı, bu ISO dosyasını sanal bir CD sürücüsü gibi okuyarak işletim sistemini kurar.

1. **İndirme:**
   > **📷 Görsel İpucu:** [Linux Mint resmi indirme sayfası (linuxmint.com/download.php) açılırken tarayıcıda "https://linuxmint.com/download.php" adresinin göründüğü, sayfanın ortasında "Cinnamon" başlığı altında "Linux Mint 22 (Virginia) - Release Notes" yazan büyük yeşil "Direct Download" butonunun göründüğü ekran görüntüsü]
   ```
   https://linuxmint.com/download.php
   ```

2. **Seçenekler:**
   - **Cinnamon (Masaüstü):** Önerilen — Windows 10/11'e en çok benzeyen, kullanıcı dostu ve hızlı masaüstü ortamı.
   - **MATE / Xfce:** Daha düşük kaynak tüketen alternatif masaüstleri (Eski bilgisayarlar için).

   > [!NOTE]
   > **Dağıtım seçimi:** Linux Mint'in ana sürümleri Cinnamon, MATE ve Xfce'dir. İlk kez Linux kullanan biri için **Cinnamon** en iyi seçenektir çünkü Windows benzeri bir arayüz sunar (başlat menüsü, görev çubuğu, sistem tepsisi).

3. **İndirme Adımları:**
   > **📷 Görsel İpucu:** [Linux Mint 22 Cinnamon 64-bit ISO indirme sayfasında "Direct Download" butonuna tıklandıktan sonra tarayıcının indirme başlatması ve dosya adının "linuxmint-22-cinnamon-64bit.iso" şeklinde İndirilenler klasörüne kaydedildiğinin tarayıcı indirme çubuğunda göründüğü ekran görüntüsü]
   - "Cinnamon" sürümü için **"Direct Download"** butonuna tıklayın.
   - Tarayıcı ISO dosyasını otomatik olarak indirmeye başlayacak (boyut ~3 GB).
   - İndirme tamamlandığında dosyanın **İndirilenler (Downloads)** klasöründe olduğunu kontrol edin.

   > [!TIP]
   > **İndirme hızı:** ISO dosyası yaklaşık 3 GB olabilir ve Wi-Fi üzerinden biraz zaman alabilir. İndirme sırasında başka büyük dosya indirip indirmediğinize dikkat edin. İndirme tamamlandığında dosya boyutu 3 GB civarında olmalıdır.

   > [!NOTE]
   > **Linux Mint sürümü:** Bu rehber Linux Mint 22 (Cinnamon) üzerinden yazılmıştır. Daha yeni sürümler de olsa adımlar büyük ölçüde aynı olacaktır. ISO dosyasının adında "64-bit" olduğundan emin olun.

   > [!TIP]
   > **İndirme bittikten sonra:** İndirilen dosyanın sonunun `.iso` ile bittiğini kontrol edin. Eğer `.exe` veya başka bir uzantı ise, yanlış dosyayı indirmiş olabilirsiniz.

#### 3. Sanal Makineyi Ayarlama

1. **VirtualBox'ı Açma ve Yeni Makine Oluşturma:**
   > **📷 Görsel İpucu:** [VirtualBox uygulaması açıldıktan sonra ana pencerenin göründüğü, sol üst köşedeki soluk mavi "Yeni" (New) düğmesine mouse ile tıklandığında pencerenin kenarlığının hafifçe parladığı veya vurgulandığı ekran görüntüsü]

2. **Yeni Sanal Makine Sihirbazı:**
   > **📷 Görsel İpucu:** [VirtualBox "Yeni Sanal Makine" penceresi; sağ tarafta isim olarak "Linux Mint" yazan metin kutusu, tür olarak "Linux", sürüm olarak "Ubuntu (64-bit)" seçili, alt kısımda "Devam Et" butonunun göründüğü ekran görüntüsü]
   - **Ad:** `Linux Mint` yazın (veya sevdiğiniz bir isim).
   - **Tür:** `Linux` olarak kalsın.
   - **Sürüm:** `Ubuntu (64-bit)` seçin.
     > [!NOTE]
     > Neden "Ubuntu"? Linux Mint Ubuntu tabanlıdır ve VirtualBox'ın ön tanılı dağıtım listesinde Linux Mint adı geçmez. Ancak Ubuntu (64-bit) Linux Mint için gereken tüm özelliklere sahiptir — bu yüzden bu seçeneği kullanıyoruz.
   - **"Devam Et"** butonuna tıklayın.

3. **RAM Ayarlama:**
   > **📷 Görsel İpucu:** [VirtualBox "Anı (RAM)" ekranı; kaydırıcı 2048 MB konumunda ve sağdaki "2048 MB" yazısının yeşil alanda olduğu (ideal bölge), sol tarafta "Önerilen bellek 1024-2048 MB" yazısının göründüğü ekran görüntüsü]
   - RAM için **2048 MB** (2 GB) ayarlayın.
   - Kaydırıcıyı sola kaydırdığınızda sayıların **kırmızıya** döndüğünü göreceksiniz — bu, ayarlanan belleğin bilgisayarınızda yeterli olmadığı anlamına gelir.
   - Yeşil bölgede kalacak şekilde ayar yapın.

   > [!WARNING]
   > **RAM uyarısı:** Bilgisayarınızda 8 GB RAM varsa, sanal makineye 2-4 GB ayırmak güvenlidir. 16 GB veya daha fazla RAM'iniz varsa 4 GB bile ayırabilirsiniz. Ana işletim sisteminizin çalışması için en az 2-4 GB RAM ayırmayı unutmayın.

4. **Sanal Disk Oluşturma:**
   > **📷 Görsel İpucu:** [VirtualBox "Sanal Sabit Disk Dosyası" penceresi; "Yeni sanal sabit disk dosyası oluştur" seçeneğinin işaretli olduğu, "Hemen oluştur" butonunun göründüğü ve bir sonraki adıma yönlendiren ekran görüntüsü]
   - **"Hemen oluştur"** seçeneğinin işaretli olduğundan emin olun ve **"Sonraki"** butonuna tıklayın.

5. **Disk Tipi Seçimi:**
   > **📷 Görsel İpucu:** [VirtualBox "Sabit disk dosyası türü" ekranı; "VMDK - VMware Virtual Disk Format" seçili ve "Sonraki" butonunun göründüğü ekran görüntüsü]
   - Varsayılan olarak **VMDK** seçilidir. Bu, VMware uyumlu bir format olup VirtualBox ile mükemmel çalışır. **"Sonraki"** butonuna tıklayın.

6. **Disk Alanı Belirleme:**
   > **📷 Görsel İpucu:** [VirtualBox "Sanal disk boyutu" ekranı; kaydırıcı 20 GB konumunda, sağda "20 GB" yazısı yeşil alanda, altında "Önerilen disk boyutu 20 GB" yazısının göründüğü ekran görüntüsü]
   - Disk alanı olarak **20 GB** ayarlayın.
   - **Dinamik olarak ayrılmış** seçeneğinin işaretli olduğundan emin olun (bu, sanal makineyi ilk kullanmaya başlayana kadar tam 20 GB'ı değil, kullandıkça alan ayırmasını sağlar).
   - **"Oluştur"** butonuna tıklayın.

   > [!NOTE]
   > **Disk alanı:** 20 GB başlangıç için yeterlidir. Dinamik ayırma seçeneği, sanal makineyi ilk kullandığınızda diskte hemen 20 GB alan kaplamasın, kullandıkça artmasına izin verir.

7. **Sanal Makine Hazır:**
   > **📷 Görsel İpucu:** [VirtualBox ana penceresinde artık "Linux Mint" adında bir sanal makine kartının göründüğü ekran — kart üzerinde sanal makinenin adının, işletim sistemi ikonu (pencere ikonu) ve sağ tarafta yeşil "Başlat" butonunun göründüğü ekran görüntüsü]

   > [!TIP]
   > **Özet:** Sanal makine oluştururken dikkat ettiğiniz şeyler: İsim "Linux Mint", tür "Linux", sürüm "Ubuntu (64-bit)", RAM "2048 MB", disk "20 GB". Bunlar doğru ayarlanmışsa "Linux Mint" adında bir sanal makine kartı ana ekranda görünecektir.

### B. Linux Mint Kurulumunu Başlatma 

Sanal makineyi oluşturduktan sonra ilk kez işletim sistemini kuracağımız an geliyor. Sanal makine penceresi otomatik olarak açılacak ve Linux Mint kurulum sihirbazı başlayacaktır.

#### 1. İlk Açılış ve ISO Bağlama

1. **Sanal Makineyi Başlatma:**
   > **📷 Görsel İpucu:** [VirtualBox ana penceresinde sol tarafta "Linux Mint" sanal makinesinin seçili olduğu (mavi renkle vurgulandığı), üst kısımdaki yeşil üçgen "Başlat" (Start) butonuna mouse ile tıklanan anın göründüğü ekran görüntüsü]
   - Sol listede oluşturuğunuz `Linux Mint` sanal makinesine tıklayarak seçin.
   - Üst menüdeki yeşil üçgen **"Başlat" (Start)** butonuna tıklayın.
   - İlk açılışta VirtualBox, sanal makineye ISO dosyasını otomatik olarak bağlayacak ve Linux Mint kurulum ekranı görünecektir.

   > [!TIP]
   > **Başlatma ipucu:** Eğer sanal makine doğrudan Linux Mint yerine "boş" bir ekran gösteriyorsa, sanal makine ayarlarından "Depolama" sekmesine gidip sanal CD sürücüsüne indirdiğiniz ISO dosyasını manuel olarak bağlamanız gerekir. Bu, sonraki bölümlerde detaylıca anlatılacaktır.

2. **ISO Bağlama Kontrolü:**
   > **📷 Görsel İpucu:** [VirtualBox sanal makine penceresi başlık çubuğunda veya "Cihazlar" menüsünde "Optik Sürücüler" altında "linuxmint-22-cinnamon-64bit.iso" dosyasının bağlı olduğu ekran görüntüsü]
   - Sanal makine penceresinin üst menüsünden **"Cihazlar" → "Optik Sürücüler"** yolunu takip edin.
   - Listede indirdiğiniz ISO dosyasının (örneğin `linuxmint-22-cinnamon-64bit.iso`) seçili olduğundan emin olun.

#### 2. Dil Seçimi

1. **Dil Seçme:**
   > **📷 Görsel İpucu:** [Linux Mint kurulum sihirbazının ilk ekranında sol tarafta mavi kutucuğun içinde "Türkçe" seçeneğinin işaretli olduğu, sağ tarafta Türkçe çeviri başlıklarının (Kurulum, Linux Mint, Dil seçimi) göründüğü ekran görüntüsü]
   - Kurulum sihirbazı ilk ekranında sol taraftaki dil listesinden **"Türkçe"**yi seçin.
   - Sağ tarafta başlıkların Türkçe'ye çevrildiğini göreceksiniz.
   - **"Devam Et"** butonuna tıklayın.

   > [!NOTE]
   > **Dil seçimi:** Linux Mint kurulumu boyunca tüm menüler Türkçe olacak şekilde ayarlanacaktır. Kurulumdan sonra da dil seçebilirsiniz.

#### 3. Klavye Düzeni

1. **Klavye Seçimi:**
   > **📷 Görsel İpucu:** [Linux Mint kurulum sihirbazının klavye ekranında sol tarafta "Türkçe" klavye düzeninin seçili olduğu, sağ tarafta "Deneyin" kutusunda Türkçe karakterlerin (ğ, ü, ş, ı, ö, ç) test edildiği ekran görüntüsü]
   - Klavye düzeni ekranında **"Türkçe Q"** seçeneğini seçin.
   - **"Deneyin"** kutusuna `ğ ü ş ı ö ç` gibi Türkçe karakterleri yazarak klavyenizin doğru ayarlandığını test edin.
   - **"Devam Et"** butonuna tıklayın.

#### 4. Güncelleme ve Diğer Yazılımlar Seçimi

1. **Güncelleme Seçenekleri:**
   > **📷 Görsel İpucu:** [Linux Mint kurulum sihirbazının "Güncellemeler ve diğer yazılımlar" ekranında "Kurulum sırasında güncellemeler indir" ve "Bu yükleme sırasında üçüncü taraf yazılımları yükle" seçeneklerinin her iki kutusunun da işaretli olduğu ekran görüntüsü]
   - Kurulum sırasında **güncellemeleri indirmek** ve **üçüncü taraf yazılımları yüklemek** istiyorsanız her iki kutuyu da işaretleyin.
   - Bu seçenekler, kurulum sırasında biraz daha uzun sürmesine neden olabilir ancak kurulumdan sonra sisteminiz daha güncel olur.

   > [!NOTE]
   > **Güncelleme seçeneği:** Eğer sanal makine internete bağlıysa bu kutuları işaretleyebilirsiniz. Bağlantı yoksa veya hızlı kurulum istiyorsanız işaretlemeyin — daha sonra da güncellemeleri yapabilirsiniz.

2. **Disk Bölümleme Seçimi:**
   > **📷 Görsel İpucu:** [Linux Mint kurulum sihirbazının disk bölümleme ekranında "Sanal makineye göre disk alanını sil ve Linux Mint'i yükle" seçeneğinin işaretli olduğu ve aşağıda disk kullanımının gösterildiği ekran görüntüsü]
   - **"Sanal makineye göre disk alanını sil ve Linux Mint'i yükle"** seçeneğini işaretleyin.
   - Bu seçenek, sanal makine içindeki tüm alanı Linux Mint için kullanır ve otomatik olarak bölümlemeyi yapar.

   > [!WARNING]
   > **Disk bölümleme uyarısı:** Bu seçenek sadece sanal makine içindeki alanı kullanır. Ana bilgisayarınızda veya başka bir diskte herhangi bir veri silinmez. Sanal makine içindeki alanı kullanacağı için güvenli bir seçenektir.

#### 5. Kullanıcı Bilgileri

1. **Kullanıcı Oluşturma:**
   > **📷 Görsel İpucu:** [Linux Mint kurulum sihirbazının "Kimlik Bilgileri" ekranında "Adınız" kutusuna bir isim yazıldığı, "Bilgisayarın adı" kutusunun otomatik doldurulduğu, "Kullanıcı adı" kutusunun küçük harfle yazıldığı, "Şifre" ve "Şifreyi doğrulayın" kutularının doldurulduğu ekran görüntüsü]
   - **Adınız:** Gerçek adınızı veya istediğiniz bir ismi yazın (örneğin "Öğrenci" veya "Kullanıcı").
   - **Bilgisayarın adı:** Otomatik olarak doldurulacaktır. Linux Mint otomatik olarak üretir; değiştirebilirsiniz.
   - **Kullanıcı adı:** Küçük harflerden oluşan bir isim girin (örneğin "ogrenci" veya "kullanici"). Bu isim sistemde kullanıcı olarak kaydedilir.
   - **Şifre:** Güçlü bir şifre belirleyin (en az 8 karakter, büyük/küçük harf, rakam içeren).
   - **"Otomatik oturum açma"** seçeneğini işaretlemek isterseniz, her açılışta şifre girmenize gerek kalmaz.
   - **"Devam Et"** butonuna tıklayın.

   > [!TIP]
   > **Şifre ipucu:** Sanal makine için güçlü bir şifre belirlemenize gerek yok, ama alışkanlık kazanmak için iyi bir şifre kullanın. Şifrenizi unutmamanız gerekir, çünkü Linux Mint güncelleme yaparken veya bazı işlemleri yaparken şifre isteyebilir.

#### 6. Kurulumun Tamamlanması

1. **Kurulum Başlatma:**
   > **📷 Görsel İpucu:** [Linux Mint kurulum sihirbazının kurulumu başlatma ekranında ilerleme çubuğunun ilerlediği ve altında "Linux Mint yükleniyor..." yazan ekran görüntüsü]
   - Kurulum başlayacaktır. İşlem 10-20 dakika sürebilir.
   - İlerleme çubuğu dolduğunda kurulum tamamlanacaktır.

2. **Yeniden Başlatma:**
   > **📷 Görsel İpucu:** [Linux Mint kurulum sihirbazının kurulum tamamlandıktan sonra "Şimdi yeniden başlatın" butonunun göründüğü ve sanal makine penceresinde "Yeniden başlatılıyor..." ekranının göründüğü ekran görüntüsü]
   - Kurulum tamamlandığında **"Şimdi yeniden başlatın"** butonuna tıklayın.
   - Sanal makine yeniden başladığında Linux Mint masaüstünü göreceksiniz.

---

## 3. Balık Tutma Becerisi: Problem Çözme ve Araştırma

Linux öğrenirken en önemli beceri, komutları ezberlemek değil — **bir sorunla karşılaştığınızda kendi başınıza çözüm üretebilmektir.** Bu bölümde, sanal makine oluştururken karşılaşabileceğiniz en yaygın hatayı ve bunu nasıl araştırıp çözebileceğinizi öğreneceksiniz.

### En Yaygın Hata: Sanal Makine Açılmıyor — "Sanallaştırma devre dışı"

Sanal makine oluşturup "Başlat" butonuna tıkladığınızda, bilgisayarınızın sanallaştırma özelliği BIOS/UEFI'de açık değilse sanal makine açılmayabilir ve hata mesajı görebilirsiniz. Bu durum oldukça yaygındır ve çözümü nispeten basittir.

#### Hata Mesajını Tanıma

Sanal makine açılmadığında aşağıdaki hata mesajlarından birini görebilirsiniz:

> **⚠️ Karşılaşabileceğiniz hata mesajı:**
> ```
> VirtualBox Error: VT-x is disabled in the BIOS/UEFI settings or the host (your real machine) is running a hypervisor that has access to VT-x (i.e. Hyper-V) and cannot therefore provide VT-x to other hypervisors such as VirtualBox.
> ```
> **Türkçe çevirisi:** VT-x, BIOS/UEFI ayarlarında devre dışı bırakılmıştır veya ana makineniz Hyper-V gibi VT-x'e erişimi olan bir hipervizör üzerinde çalışıyor ve bu nedenle VT-x'i VirtualBox gibi diğer hipervizörlere sağlayamıyor.

veya daha kısa versiyonu:
> **⚠️ Alternatif hata mesajı:**
> ```
> VT-x is disabled in the BIOS settings
> ```
> **Türkçe çevirisi:** VT-x, BIOS ayarlarında devre dışı.

**Hata mesajını okumanın önemi:** Hata mesajı size sorunun ne olduğunu doğrudan söylüyor — bilgisayarınızın işlemcisi sanallaştırma teknolojisini (VT-x için Intel, AMD-V için AMD) kullanmıyor veya bu özellik BIOS'ta kapalı.

#### Sorunu Anlama

**Sanallaştırma (Virtualization) Nedir?**
Modern bilgisayar işlemcileri (Intel ve AMD), sanal makinelerin çalışması için "sanallaştırma" adında bir donanım özelliği içerir. Bu özellik BIOS/UEFI ayarlarında varsayılan olarak **kapalı** gelebilir, çünkü çoğu kullanıcı sanal makine kullanmaz. Linux Mint kurulumu sanal makine üzerinden çalıştığı için bu özelliğin açık olması gerekir.

> [!TIP]
> **Terim bilgisi:** Intel işlemcilerde bu özelliğe **VT-x** (Virtualization Technology), AMD işlemcilerde ise **AMD-V** adı verilir. Hangi işlemciye sahip olduğunuzu anlamak için Google'a "Intel processor name" veya "AMD processor name" yazarak modelinizi öğrenebilirsiniz.

#### Nasıl Çözülür? (Adım Adım)

1. **Bilgisayarı Yeniden Başlatma:**
   - Windows veya macOS bilgisayarınızı tamamen kapatın.
   - Bilgisayarınızı tekrar açın ve hemen **BIOS/UEFI** ayarlarını açmak için bir tuşa basın.
     - **Çoğu bilgisayar için:** `F2`, `F10`, `F12`, `Del` (Delete) veya `Esc` tuşları.
     - Laptoplar için genellikle `F2` veya `F10`.
   - Ekran kararıp marka logosu göründüğünde bu tuşlara hızlıca ve tekrar tekrar basın.

2. **BIOS/UEFI Ayarlarında Sanallaştırma Bulma:**
   - BIOS ekranında **"Advanced"**, **"Configuration"**, **"CPU Configuration"** veya **"Security"** gibi bir sekme/bölüm arayın.
   - Aradığınız seçenek genellikle şu isimlerden biridir:
     - **Intel:** `Intel Virtualization Technology`, `VT-x`, `Virtualization Technology (VT-x)`, `Vanderpool`
     - **AMD:** `AMD-V`, `SVM Mode`, `Secure Virtual Machine`
   - Seçeneği bulunca değeri **"Disabled"** ise **"Enabled"** olarak değiştirin.
     - Genellikle ok tuşlarıyla seçip `Enter`, sonra `+`/`-` veya `Space` tuşlarıyla değiştirilir.
   - Değişiklikleri kaydedip çıkın (genellikle `F10` ve `Y` — "Save and Exit").

3. **Doğrulama:**
   - Bilgisayar normal şekilde Windows/macOS'te açılmalı.
   - VirtualBox'ı tekrar açıp `Linux Mint` sanal makinesini başlatın.
   - Artık sanal makine açılmalı ve Linux Mint kurulumu başlamalı.

#### Sorunu Kendiniz Araştırma Becerisi

Şimdi size gerçek bir **araştırma pratiği** veriyorum. Aşağıdaki adımları izleyerek bu hatanın çözümüyle ilgili farklı kaynaklara ulaşmayı deneyin. Bu, Linux öğrenirken kendinizi geliştirmenizi sağlayacak en değerli becerilerden biridir.

1. **Google Araması:**
   > **📷 Görsel İpucu:** [Chrome/Edge tarayıcısında adres çubuğuna "VirtualBox VT-x is disabled in the BIOS settings" yazısı yazılmış, Enter tuşuna basılmış ve Google arama sonuçlarının listelendiği ekran görüntüsü]

   Google'a şu anahtar kelimeleri yazarak arama yapın:
   - `VirtualBox VT-x is disabled in the BIOS settings`
   - `enable virtualization in bios virtualbox`
   - `VirtualBox error "VT-x is disabled" how to fix`

   > [!TIP]
   > **Arama ipucu:** Arama yaparken sorununuzu İngilizce yazın. Linux topluluğu İngilizce içeriklerin çoğunluğuna sahiptir. Google, Türkçe yazsanız bile İngilizce sonuçlar önerebilir — bu normaldir.

2. **VirtualBox Forumu:**
   > **📷 Görsel İpucu:** [forum.virtualbox.org web sitesinde arama çubuğuna "VT-x is disabled" yazılmış ve forum konu başlıklarının listelendiği ekran görüntüsü]

   VirtualBox'ın resmi forumuna gidin: `https://forum.virtualbox.org/`
   - Arama çubuğuna `VT-x disabled` yazın.
   - Benzer sorunu yaşayan kullanıcıların çözümlerini okuyun.

3. **Stack Overflow ve Reddit:**
   - `https://stackoverflow.com/questions/tagged/virtualbox` — VirtualBox soruları
   - `https://www.reddit.com/r/virtualbox/` — VirtualBox topluluğu

   > [!NOTE]
   > **Kaynak güvenirligi:** Linux ve VirtualBox ile ilgili sorunları çözerken öncelikle resmi dokümantasyon (virtualbox.org), resmi forumlar ve Stack Overflow gibi topluluk kaynaklarını kullanın. YouTube videoları da yardımcı olabilir ama dokümantasyon her zaman daha güvenilir ve günceldir.

4. **Sanallaştırma Bilgilerini Kendiniz Kontrol Etme:**
   > [!NOTE]
   > İşletim sisteminizde sanallaştırma özelliğinin açık/kapalı olduğunu kontrol etmek için komut satırını kullanabilirsiniz (daha sonra öğreneceğiniz `--help` ve `man` komutlarıyla). Bilgisayarınızın modeline göre "how to check virtualization enabled windows" şeklinde arama yaparak komut satırından kontrol yöntemini bulabilirsiniz.

> [!TIP]
> **Troubleshooting taktiği:** Bir sorunla karşılaştığınızda izlemeniz gereken sıra:
> 1. **Hata mesajını dikkatlice okuyun** — çoğu zaman çözüm mesajın içinde ipucu vardır.
> 2. **Hata mesajının tam metnini Google'da arayın** (tırnak içine alarak: `"VT-x is disabled"`).
> 3. **Birden fazla kaynaktan yanıt alın** — tek bir kaynağa güvenmeyin.
> 4. **Çözümü uygulamadan önce ne yaptığını anlayın** — sadece komutu kopyalamayın, mantığını kavrayın.
> 5. **Başarılıysa, çözümün neden işe yaradığını not alın** — böylece bir dahaki sefere hatırlarsınız.

> [!IMPORTANT]
> **Not alma alışkanlığı:** Çözdüğünüz her sorunu bir not defterine (bilgisayarınızda veya fiziksel bir deftere) kaydedin. "X tarihinde Y hatası ile karşılaştım, çözüm: Z" şeklinde. Bir süre sonra bu notlar size büyük kolaylık sağlayacak ve benzer hatalarla hızlıca başa çıkmanızı sağlayacak.

---

## 4. Paket Yönetimi ve Uygulama Pratiği

### Update Manager ile İlk Güncelleme

Linux Mint kurulduktan sonra sistemdeki yazılım paketlerini güncellemek önemlidir. Linux Mint, bu işlemi hem grafik arayüz (Update Manager) hem de komut satırı (`apt`) üzerinden sağlar. İlk güncelleme işlemini grafik arayüz üzerinden yapacağız.

#### 1. Update Manager'ı Açma

1. **Bildirim Çubuğundan:**
   > **📷 Görsel İpucu:** [Linux Mint 22 Cinnamon görev çubuğunun sağ üst köşesinde sistem tepsisi (system tray) alanında kırmızı zemin üzerinde beyaz bir daire ikonu (güncelleme bildirimi) yanıp sönerken, mouse ile üzerine tıklandığında "Update Manager (Güncelleme Yöneticisi)" penceresinin açıldığı ekran görüntüsü]
   - Görev çubuğunun sağ üst köşesinde kırmızı zemin üzerinde beyaz bir daire ikonu göreceksiniz (bu, sisteminizdeki güncellemelerin olduğunu gösterir).
   - Bu ikona tıklayın ve **"Update Manager" (Güncelleme Yöneticisi)** seçeneğini seçin.

2. **Alternatif Yoldan:**
   > **📷 Görsel İpucu:** [Linux Mint 22 Cinnamon başlat menüsü (sol alt köşedeki menü butonu) tıklandıktan sonra açılan menüde "Uygulamalar" → "Yönetim" bölümünde "Update Manager (Güncelleme Yöneticisi)" seçeneğinin göründüğü ve mouse ile üzerine tıklandığı ekran görüntüsü]
   - Başlat menüsüne tıklayın.
   - **"Uygulamalar" → "Yönetim"** bölümünden **"Update Manager (Güncelleme Yöneticisi)"** seçeneğine tıklayın.

   > [!NOTE]
   > **İlk açılış:** Update Manager ilk açıldığında sistemdeki güncellemeleri kontrol etmek için birkaç saniye bekleyebilir. Bu sırada sistemdeki paket listesi güncellenir.

#### 2. Güncellemeleri İndirme ve Yükleme

1. **Güncelleme Kontrolü:**
   > **📷 Görsel İpucu:** [Linux Mint 22 Update Manager penceresi; üst kısımda "Sistem güncellemeleri bulundu" yazısı ve "Güncellemeleri indir ve yükle" yeşil butonu görünüyor, alt kısımda güncellenecek paketlerin listesi ve yanında "En son" ve "Değiştir" başlıklı sütunlar ile "Sık sık otomatik güncelleme denetimi" seçeneğinin işaretli olduğu ekran görüntüsü]
   - Update Manager penceresi açıldığında, eğer güncelleme varsa **"Güncellemeleri indir ve yükle"** yeşil butonunu göreceksiniz.
   - Eğer buton görünmüyorsa, üst menüden **"Görünüm → Güncellemeler" → "Güncellemeleri kontrol et"** yolunu izleyerek kontrolü manuel olarak başlatabilirsiniz.

2. **Lisans Sözleşmeleri:**
   > **📷 Görsel İpucu:** [Update Manager "Gelişmiş Lisans Sözleşmeleri" (Advanced License Agreements) penceresi; "GPG anahtarı" ve "Lisans" başlıklı lisans sözleşmelerinin listelendiği, "Kabul Et" butonunun göründüğü ekran görüntüsü]
   - Bazı güncellemeler için lisans sözleşmesi kabul etmeniz gerekebilir. **"Kabul Et"** butonuna tıklayın.

3. **Şifre Girme:**
   > **📷 Görsel İpucu:** [Update Manager "Yönetici parolasını girin" penceresi; "Parola" kutusuna şifre yazılan ve "Doğrula" butonunun göründüğü ekran görüntüsü]
   - Bazı güncellemeleri yüklemek için **yönetici parolanızı** girmeniz gerekecektir.
   - Kurulum sırasında belirlediğiniz kullanıcı şifresini girin ve **"Doğrula"** butonuna tıklayın.

   > [!TIP]
   > **Şifre ipucu:** Şifreyi yazarken ekranda karakterler görünmez. Yanlış yazdığınızdan emin olun, çünkü yanlış şifre girişinde "Doğrula" butonu hata verecektir.

4. **İndirme ve Yükleme:**
   > **📷 Görsel İpucu:** [Update Manager "Güncellemeler yükleniyor..." ilerleme çubuğu; alt kısımda güncellenen paket isimlerinin ve yükleme yüzdesinin göründüğü ekran görüntüsü]
   - Güncellemeler indirilmeye ve yüklenmeye başlayacaktır.
   - İşlem tamamlandığında bir mesaj göreceksiniz: **"Sistem güncellemeleri başarıyla yüklendi."**
   - **Tam güncelleme için bilgisayarınızı yeniden başlatın.**

#### 3. Yeniden Başlatma

1. **Sistemi Yeniden Başlatma:**
   > **📷 Görsel İpucu:** [Linux Mint 22 Cinnamon başlat menüsü tıklandıktan sonra açılan menünün sağ alt köşesinde "Güç Durumu" (Power) butonunun göründüğü ve üzerine tıklandığında "Yeniden Başlat" (Restart) seçeneğinin açıldığı ekran görüntüsü]
   - Güncellemeleri tam olarak yüklemek için bilgisayarınızı yeniden başlatın.
   - Başlat menüsünden **"Güç Durumu (Power) → Yeniden Başlat (Restart)"** yolunu izleyin.
   - Veya görev çubuğundaki güç butonuna tıklayarak da yeniden başlatabilirsiniz.

2. **İlk Oturum Açma:**
   > **📷 Görsel İpucu:** [Linux Mint 22 Cinnamon oturum açma ekranı; sol altta kullanıcı adının ve şifre kutusunun göründüğü, sağ altta güç butonunun ve dil seçiminin (TR/EN) göründüğü ekran görüntüsü]
   - Yeniden başladığınızda oturum açma ekranı görünecektir.
   - Kullanıcı adınızı seçin ve şifrenizi girerek oturum açın.
   - Artık Linux Mint masaüstünü kullanmaya hazırsınız!

---

## 5. Alıştırmalar ve Çözümleri (Exercises)

Bu modülde edindiğiniz bilgileri pekiştirmek için aşağıdaki alıştırmaları yapın. Alıştırmalar tamamen **grafik arayüz (GUI)** ve **sorun çözme araştırmaları** üzerine odaklanmıştır — henüz terminal komutlarına girmiyoruz.

### Challenge 1: VirtualBox Üzerinde Sanal Makine Yönetimi

**Görev:**
1. VirtualBox üzerinde Linux Mint için yeni bir sanal makine oluşturun.
2. Sanal makineyi başlatıp kurulum medyasını çalıştırın.
3. Sanal makineyi kapatın ve kullanmadığınız zamanlarda nasıl silebileceğinizi keşfedin.

<details>
<summary>Çözüm için tıklayın</summary>

```
1. Sanal Makine Oluşturma:
   - VirtualBox'ı açın, üst menüdeki "Yeni" (New) butonuna tıklayın.
   - İsim olarak "Linux Mint", Tür olarak "Linux", Sürüm olarak "Ubuntu (64-bit)" seçip 2048 MB RAM atayın.
   - Sabit disk oluşturun: 20 GB olacak şekilde ayarlayın.
   - Sanal disk formatı olarak VMDK seçin, sonra "Oluştur" düğmesine tıklayın.

2. Başlatma:
   - Sol listede oluşturduğunuz makineye tıklayın.
   - Üstteki yeşil "Başlat" (Start) butonuna basın.
   - Açılan pencerede indirdiğiniz .iso dosyasını seçin (Linux Mint 21.3 Cinnamon).
   - Kurulum sihirbazı başlayacaktır.

3. Kapatma/Silme:
   - Sanal makineyi kapatmak için menüden "Makine" → "Kapat" yolunu izleyin.
   - Sildiğinizde sol listede makineye sağ tıklayıp "Kaldır..." → "Tüm dosyaları sil" seçeneğini kullanın.
```
</details>

### Challenge 2: Linux Mint Kurulumu

**Görev:**
- Linux Mint kurulum sihirbazını tamamlayın.
- Türkçe dil seçeneğini aktif edin.
- Kurulumdan sonra masaüstünde dosya yöneticisini açın.

<details>
<summary>Çözüm için tıklayın</summary>

```
1. Kurulumu Tamamlama:
   - Dil ekranında "Türkçe" seçin.
   - Klavye düzeninizi kontrol edin.
   - Disk bölümleme ayarlarını kontrol edin.
   - Kullanıcı bilgilerinizi girin ve kurulumu başlatın.

2. Türkçe Dil Ayarı:
   - Kurulum tamamlandıktan masaüstünde "Sistem Ayarları" menüsünden "Diller"i açın.
   - Üstteki listede "Türkçe"yi ilk sıraya taşıın.
   - "Uygula" düğmesine tıklayın ve oturumu kapatıp açın.

3. Dosya Yöneticisi:
   - Masaüstünün sağ üst köşesindeki "Dosyalar" simgesine çift tıklayın.
   - Açılan pencerede /home/kullanıcı dizinini görebilirsiniz.
```
</details>

### Challenge 3: Sanal Makineye İlişkin Hata Araştırması

**Görev:**
- Sanal makine başlatılmadığında karşılaşabileceğiniz "VT-x is disabled" hatasıyla ilgili araştırma yapın.
- Bu hatanın çözümünü gösteren en az iki farklı kaynaktan bilgi edinin.
- Çözüm adımlarını kendi cümlelerinizle bir not defterine yazın.

<details>
<summary>Çözüm için tıklayın</summary>

```
1. Araştırma:
   - Google'da "VirtualBox VT-x is disabled in the BIOS settings" araması yapın.
   - En az iki farklı kaynaktan (örneğin VirtualBox forumu ve bir teknoloji blogu) çözüm okuyun.

2. Çözüm Adımları (kendi cümlelerinizle):
   - Bilgisayarı yeniden başlatın ve BIOS/UEFI ayarlarını açın (genellikle F2 veya Del tuşu).
   - BIOS'ta "Advanced" veya "CPU Configuration" bölümünü bulun.
   - "Intel Virtualization Technology" veya "AMD-V" seçeneğini bulun ve "Enabled" olarak değiştirin.
   - Değişiklikleri kaydedip çıkın (genellikle F10).
   - VirtualBox'ı tekrar açıp sanal makineyi başlatın.

3. Not Alma:
   - Çözüm adımlarını bir not defterine yazın.
   - Kaynakların linklerini de not edin.
```
</details>

---

## 6. Özet ve Hızlı İpuçları

| Özet |
|----------------|
| **Linux Nedir:** Ücretsiz, açık kaynaklı bir işletim sistemi çekirdeğidir; birçok dağıtımla birlikte kullanılır (Ubuntu, Debian, Linux Mint vb.) |
| **Kernel vs. Dağıtım vs. Masaüstü Ortamı:** Kernel araçları ve yazılımları bir araya getiren aracı bir parçadır; dağıtım kernel'i ve yazılımları bir araya getiren bir sistemdir; masaüstü ortamı kullanıcı arayüzünü ve uygulamalarını sağlar |
| **Sanal Makine:** Farklı işletim sistemlerini bir bilgisayarın içine yerleştiren bir sanal ortamdır; öğrenmek için en güvenli yoldur |
| **VirtualBox:** Sanal makineler oluşturmak, yönetmek ve başlatmak için kullanılır; 64-bit işletim sistemlerini, 2048 MB RAM'ı ve 20 GB diski destekler |
| **Linux Mint Kurulumu:** Başlangıç ekranı, dil seçimi, klavye ayarı, disk bölümleme, kullanıcı yaratma, güncellemeler, masaüstü ortamı |
| **Update Manager:** Güncellemeleri indirip yüklemek için kullanılan grafik arayüz aracı; ilk sisteme ilk güncellemeyi yapmanızı sağlar |
| **Troubleshooting:** Hata mesajını okuyun, Google'da arayın, birden fazla kaynaktan bilgi alın, çözümü not edin |
| **Önemli Araçlar:** Update Manager, VirtualBox GUI, Sistem Ayarları |
