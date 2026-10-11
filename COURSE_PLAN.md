# Linux Temelleri — Kurs Planı

Son güncelleme: 9 Ekim 2026

## Kurs Profili

- **Kurs adı:** Linux Temelleri
- **Eğitim seviyesi:** 3. sınıf lisans
- **Bölüm:** Veri bilimi ve analitiği
- **Hedef kitle:** Daha önce hiç Linux tecrübeleri olmayan öğrenciler
- **Süre:** 14 hafta, haftada 3 saat
- **Teori/Pratik:** Dengeli (~50 / ~50)
- **Komut satırı ağırlığı:** Çok fazla değil; kavramlar, görseller ve ortamlar da kapsanır
- **Adres formu:** Siz
- **Sözde kod:** Kullanılmayacak
- **Görsel:** İhtiyaç halinde ekran görüntüleri / görseller kullanılacak; görsel stili onaylanacak
- **Başlangıç:** İlk hafta basit Linux kurulumu + temel kavramlar
- **İlerleyiş:** Temel kullanım / komutlar → farklı dağıtım ve masaüstü ortamları → ileri kurulum (disk bölümleme, ext/btrfs, Timeshift)
- **Kurs türü:** Sistem / teknik (Linux) — kavram → çevre → keşif → görev → sorun giderme → bağımsız görev

## Onaylanmış Öğrenme Çıktıları

1. Linux işletim sisteminin temel kavramlarını açıklayabilir.
2. Temel dosya ve dizin yapısını yorumlayabilir.
3. Temel komutları doğru kullanarak dosya işlemleri gerçekleştirebilir.
4. Farklı Linux dağıtımlarını karşılaştırıp avantajlarını değerlendirebilir.
5. Farklı masaüstü ortamlarını deneyimleyip farklarını gözlemleyebilir.
6. Disk bölümleme (partitioning), dosya sistemleri (ext4, btrfs) ile ilgili temel farkları açıklayabilir.
7. İleri kurulum ve yedekleme araçlarını (örneğin Timeshift) kullanarak sistem bakımını gerçekleştirebilir.
8. Hata ayıklama ve sistem izleme yöntemlerini uygulayabilir.
9. Linux ortamında veri biliminde kullanılabilecek temel araçları kurup çalıştırabilir.

## Onaylanmış Haftalık Plan (14 hafta)

| Hafta | Konu | Alt Konular | Çıktı | Pratik | İlişki |
|---|---|---|---|---|---|
| 1 | Linux Kurulumu ve Temel Kavramlar | Kurulum, çekirdek, kabuk, dosya sistemi | 1, 2 | Kurulum | Başlangıç |
| 2 | Temel Komutlar ve Dosya Sistemi | ls, cp, mv, rm, pwd, cd, cat | 2, 3 | Dosya işlemleri | H1 sonrası |
| 3 | Kullanıcı Yönetimi ve İzinler | chmod, chown | 3 | İzin değiştirme | H2 sonrası |
| 4 | Farklı Dağıtımlar | Ubuntu, Fedora, Debian | 4 | Dağıtım yükleme | Temel kavramlardan sonra |
| 5 | Masaüstü Ortamları | GNOME, KDE, XFCE | 5 | Masaüstü değiştirme | H4 sonrası |
| 6 | Paket Yönetimi | apt, dnf, snap | 1, 3 | Paket kurma | Temel komutlardan sonra |
| 7 | Ağ Temelleri | IP, yapılandırma | 8 | Ağ bağlantısı | Temel sistemden sonra |
| 8 | Disk Bölümleme ve Dosya Sistemleri | ext4, btrfs | 6 | Disk bölümleme | H3, H2 sonrası |
| 9 | İleri Kurulum ve Çoklu Önyükleme | Çoklu önyükleme | 6, 7 | İleri kurulum | H8 sonrası |
| 10 | Shell Betikleri ve Otomasyon | bash, temel betik | 3, 8 | Otomasyon | Temel komutlardan sonra |
| 11 | Sistem İzleme ve Hata Ayıklama | top, dmesg, loglar | 8 | İzleme | H7, H10 sonrası |
| 12 | Veri Bilimi Araçları Kurulumu | Python, Jupyter | 9 | Araç kurulum | Temel sistemden sonra |
| 13 | Yedekleme ve Kurtarma | Timeshift, yedekleme | 7, 9 | Yedekleme | H8, H9 sonrası |
| 14 | Bütünleşik Proje ve İnceleme | Tüm konular | Tüm | Proje sunumu | Tüm haftalardan sonra |

## Depo Yapısı (Onaylanmış)

```text
Linux-Temelleri/
├── README.md
├── COURSE_PLAN.md
└── Topics/
    ├── 01-Linux-Basics.md
    ├── 02-File-Operations.md
    ├── 03-User-Management.md
    ├── 04-Distributions.md
    ├── 05-Desktop-Environments.md
    ├── 06-Package-Management.md
    ├── 07-Network-Basics.md
    ├── 08-Disk-Partitioning.md
    ├── 09-Advanced-Install.md
    ├── 10-Shell-Scripting.md
    ├── 11-System-Monitoring.md
    ├── 12-Data-Science-Tools.md
    ├── 13-Backup-Timeshift.md
    └── 14-Integrated-Project.md
```

## Terim Kararları

- dosya sistemi (file system)
- disk bölümleme (disk partitioning)
- paket yöneticisi (package manager)
- masaüstü ortamı (desktop environment)
- çoklu önyükleme (dual/multi boot)
- yedekleme (backup)
- sistem izleme (system monitoring)
- hata ayıklama (debugging / troubleshooting)
- çekirdek (kernel)
- kabuk (shell)

## Görsel Stili (Öneri — onay bekleniyor)

Düz, sade ekran görüntüsü stili veya basit vektör ilustrasyon; arka plan açık, yazı yok, Türkçe karakter içermeyen görseller tercih edilir. Görsel sadece ihtiyaç halinde eklenir.

## İçerik Şablonu (Onaylanacak — Gate 5)

Her hafta için:
- Başlık (H1) — Türkçe konu başlığı
- 🎯 Bu Derste Ne Öğreneceğiz?
- 💡 Neden Bu Konuyu Öğreniyoruz?
- Ön Bilgi
- Kavramlar
- 🔍 Birlikte Keşfedelim (keşif döngüsü: soru → tahmin → deney → açıklama)
- 🛠️ Uygulama
- 🧪 Deneyelim ve Gözlemleyelim
- Bir Şeyler Ters Giderse (hata ayıklama / sorun giderme)
- Kendin Dene
- 🧠 Öğrendiklerini Kontrol Et
- Bağımsız Çalışma
- Daha Fazlasını Öğrenmek
- Kısa Özet
- Navigasyon (önceki / sonraki hafta bağlantıları)

Mermaid diyagramları kavram akışı için kullanılır (örneğin disk bölümleme akışı, paket kurulum akışı). Emoji yalnızca başlıklarda; başlık başına en fazla bir emoji.

## İçerik Üretim Durumu

- [x] Kurs profili (Gate 1)
- [x] Öğrenme çıktıları (Gate 2)
- [x] Haftalık plan (Gate 3)
- [x] Depo yapısı / README taslağı (Gate 4)
- [x] İçerik şablonu (Gate 5)
- [x] 01-Linux-Basics.md
- [x] 02-File-Operations.md
- [x] 03-User-Management.md
- [x] 04-Distributions.md
- [x] 05-Desktop-Environments.md
- [x] 06-Package-Management.md
- [x] 07-Network-Basics.md
- [x] 08-Disk-Partitioning.md
- [x] 09-Advanced-Install.md
- [x] 10-Shell-Scripting.md
- [x] 11-System-Monitoring.md
- [x] 12-Data-Science-Tools.md
- [x] 13-Backup-Timeshift.md
- [x] 14-Integrated-Project.md
