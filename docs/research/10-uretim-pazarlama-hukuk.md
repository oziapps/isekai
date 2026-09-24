# 10 — Üretim Planlaması, Pazara Çıkış (Go-to-Market) ve Hukuk

> Hazırlanma: 2026-09-24 · Kapsam: Türkiye'de yaşayan, Claude Code'u ana geliştirici olarak kullanan tek kişilik bir geliştiricinin özgün, 3D anime isekai aksiyon-RPG'si. Motor önerisi 08 raporunda Godot 4.7; iş modeli 04 raporunda premium (B2P) + Early Access.
>
> **Yöntem ve doğrulama notu (önemli):** Bu rapor yazılırken oturumun WebSearch kotası (200/200) dolmuştu. partner.steamgames.com, howtomarketagame.com, copyright.gov, eur-lex, turkpatent.gov.tr gibi alan adları egress proxy tarafından engellendi. Bunun yerine üç yol kullanıldı:
> 1. **Steamworks belgeleri**, Steam belgelerini otomatik izleyen `SteamTracking/SteamworksDocumentation` GitHub aynasından (son commit 2026-09-24 09:38 UTC) doğrudan okundu. Bu, fiilen birincil metindir.
> 2. **Makale ve düzenleme özetleri**, GitHub'daki üçüncü taraf araştırma notlarından (orijinal URL'yi ve tarihi veren) okundu. Orijinal sayfa açılamadı.
> 3. Model bilgisi (Haziran 2026'ya kadar).
>
> **Etiketler:**
> - **[C]** Canlı doğrulandı: birincil metin bu oturumda okundu (Steamworks aynası, GitHub dosyaları).
> - **[G]** GitHub-ikincil: orijinal URL'yi ve tarihi veren üçüncü taraf GitHub notundan. Orijinal açılamadı.
> - **[R]** Kardeş rapor (01–08). Oradaki kaynak aktarıldı.
> - **[B]** Model bilgisi. Verilen URL bu oturumda açılamadı. **Doğrulayıcı önce bunlara bakmalı.**
> - Güven düzeyi: **Y** yüksek · **O** orta · **D** düşük veya doğrulanamadı.

## Özet

- **Takvim gerçeği [C/Y]:** Ekim 2026 Next Fest'in kaydı 31 Ağustos 2026'da kapandı. Önümüzdeki Next Fest'ler:
  - 22 Şubat – 1 Mart 2027 (kayıt son günü 10 Ocak 2027)
  - 14–21 Haziran 2027 (kayıt son günü 25 Nisan 2027)
  - Bir oyun Next Fest'e **yalnızca bir kez** katılabilir [1][3][4]. Prolog, "Bölüm 1" ve başka bir oyunun kısa önizlemeleri Next Fest'e kabul edilmez; EA'ya çıkan oyun "çıkmış" sayılır ve artık katılamaz (düzeltildi 24.09.2026) [1].
  - Bizim için gerçekçi pencereler **Ekim 2027** (agresif senaryo) veya **Şubat 2028** (temel senaryo). Bu iki etkinliğin tarihleri henüz ilan edilmedi. Valve'ın Haziran 2027 sayfası bir sonraki fest'in **Ekim 2027'de planlandığını** yazıyor; Şubat 2028 ise yılda üç kez Şubat/Haziran/Ekim örüntüsünden çıkarım (düzeltildi 24.09.2026) [1][4].
- **Kapsam gerçeği:** Tek kişilik hit'lerin neredeyse hepsi ya küçük kapsamlı ve düşük varlık maliyetli (Megabonk, Schedule I, Buckshot Roulette, Vampire Survivors) ya da çok yıllık (Stardew ~4 yıl, Blue Prince ~8 yıl). **Listede tek kişilik 3D anime ARPG yok.** Bu yüzden kapsam hub şehir + instanced "Kapı" zindanları + az ama derin yoldaş ile sınırlanmalı (08 raporuyla uyumlu) [G][R].
- **Önerilen temel yol haritası (bugünden itibaren):**
  - Dikey kesit ~7. ay (Nisan 2027)
  - Steam "Coming Soon" sayfası ~6.–7. ay
  - Herkese açık demo ~13.–14. ay
  - Next Fest Şubat 2028
  - Early Access Mart–Nisan 2028 (~18. ay)
  - 1.0 2029'un ilk yarısı
  - Her fazın sonunda sayısal go/no-go kapısı var (§3).
- **Steam'in "Popular Upcoming" rafı artık indie için fiilen kapalı [G/O]:** Zukowski'ye göre Valve Haziran 2026'da eşiği ~7 bin istek listesinden **~100 bin**e çıkardı (resmî olmayan tahmin). Yerine gelen **Personal Calendar** kişiselleştirilmiş çalışıyor [21]. Valve'ın kendi belgesi, istek listesinin (bu raf dışında) algoritmik görünürlükte "çoğunlukla" etken olmadığını söylüyor [14][C].
- **İstek listesi kıyasları (2025–2026) [G/O]:**
  - Next Fest'te zayıf pazarlanmış oyun ≤1 bin, orta 2–3 bin, üst %95'lik dilim ~15 bin, "süper viral" 30–45 bin istek listesi topluyor [19]. Düzeltme: Şubat 2026 anketinde (3.500+ demo) **medyan oyun ~800** istek listesi kazandı; üst %5 medyanın 16 katından fazlasını, yani ~13 bin+ aldı. "Orta 2–3 bin" medyanın üstünde, iyi pazarlanmış bir oyun için geçerli (düzeltildi 24.09.2026) [19].
  - Fest öncesi istek listesi sayısı, fest kazancının en güçlü göstergesi (Spearman r≈0,825; bu değer Şubat 2026 verisinden [19], Mart 2025 makalesinden değil — düzeltildi 24.09.2026).
  - Demo oyuncusundan istek listesine dönüşüm medyanı %19,3 [22].
  - 10 $ üstü oyunlarda istek listesinden ilk hafta satışa dönüşüm medyanı **~0,10×** [75].
- **Steam'in AI beyan kuralı [C/Y]:** İçerik anketi, oyuncunun tükettiği içeriği (sanat, ses, anlatı, yerelleştirme) iki başlıkta soruyor: **Önceden Üretilmiş** ve **Canlı Üretilen** (canlı üretimde koruma önlemleri de isteniyor). Kod asistanı gibi verimlilik araçları "odak değil" [7]. 16 Ocak 2026 form güncellemesini aktaran haberlere göre (Slashdot, KitGuru, TechPowerUp) beyan kapsamına **mağaza sayfası varlıkları, Steam topluluk varlıkları ve pazarlama materyalleri** (fragman, capsule vb.) de giriyor; Steamworks belge sayfası yalnızca "oyunla gelen" içerikten söz ediyor. İhtiyaten pazarlamadaki AI kullanımı da beyan edilmeli (düzeltildi 24.09.2026). Buna karşın çekirdek Steam kitlesinin %56'sı Claude Code gibi kodlama araçlarının da beyan edilmesini istiyor [27][G/O].
- **Oyuncu tepkisi karışık ama yönetilebilir [G/O]:**
  - GameDiscoverCo anketi (25 Haziran–2 Temmuz 2026, ~4.000 çekirdek Steam fanı): AI beyanlı oyunu almakta %43 sorun görmüyor, ~%26 nötr, %31 olumsuz, %8,1 hiçbir koşulda oynamam diyor (düzeltildi 24.09.2026: "%43 kayıtsız" yerine "sorun görmüyor"). Oyuncuların yalnızca %17'si geliştiricilerin AI kullanımını tam beyan ettiğine inanıyor [27].
  - Haziran 2026 Next Fest demolarının %26,5'i AI beyanı taşıyordu [25].
  - Sonuç: risk "AI kullanmak"tan çok **"gizlemek" ve "AI görünümlü" key art**.
- **AB Yapay Zekâ Yasası md. 50 [G/O]:**
  - Şeffaflık yükümlülükleri **2 Ağustos 2026'dan beri uygulanıyor**.
  - Digital Omnibus (Tüzük 2026/1744), yüksek riskli sistemleri Aralık 2027 ve Ağustos 2028'e erteledi ama md. 50'yi ertelemedi.
  - 2 Ağustos 2026'dan önce piyasaya sürülmüş üretken sistemlerin sağlayıcılarına md. 50(2) için 2 Aralık 2026'ya kadar süre tanındı [52].
  - Kurgusal ve sanatsal eserlerde deepfake beyanı, "eserden alınan keyfi bozmayacak" şekilde sınırlı tutulabiliyor [51].
- **Telif [G/O]:**
  - ABD Telif Ofisi (29 Ocak 2025): yalnızca prompt yazmak yazarlık sayılmıyor [56].
  - ABD Yüksek Mahkemesi 2 Mart 2026'da Thaler v. Perlmutter'da temyizi reddetti; insan yazarlık şartı kesinleşti [57].
  - Sonuç: saf AI çıktısını başkası kopyalayabilir. **Logo, key art ve ana karakter tasarımları insan eliyle üretilmeli ya da belgelenmiş biçimde dönüştürülmeli.**
- **Marka tescil ücretleri:**
  - TÜRKPATENT 2026: başvuru 1. sınıf 2.820 TL, 2. sınıf +2.820 TL, 3. ve sonraki her sınıf +3.150 TL; tescil ücreti 7.010 TL [60][G/O].
  - EUIPO: 850 € (1 sınıf) + 50 € (2. sınıf) [63][G/B].
  - USPTO: sınıf başına 350 $ (18 Ocak 2025'ten beri) [62][G/O].
  - Oyun için temel sınıflar 9 (indirilebilir oyun yazılımı) ve 41 (eğlence ve oyun hizmetleri).
- **Bütçe (EA'ya kadar ~18 ay, geliştiricinin geçim gideri hariç; kalemlerin çoğu tahmin/D):** asgari ~6 bin $, temel ~52 bin $, ideal ~175 bin $ (§4.3). En büyük kalemler yerelleştirme, insan sanatı ve seslendirme. Bu kalemler **istek listesi kapılarına bağlanarak** harcanmalı.
- **Yerelleştirme önceliği:**
  - Steam kullanıcılarının %60'tan fazlası Steam'i İngilizce dışında bir dilde kullanıyor [17][C/Y].
  - Sıralama: EN → JA → ZH-Hans → KO → TR → PT-BR → ES (02 raporu).
  - JA ve ZH için AI ön çeviri + **mutlaka insan LQA** (dil kalite kontrolü).
- **Hukuki asgari set:**
  - Serbest çalışan sözleşmelerinde yazılı ve hak hak sayılmış devir (FSEK md. 52) [B/O]
  - AI maddesi (klonlama ve model eğitimi yasağı, AI kullanım beyanı)
  - Besteciyle OST dahil tam devir ve yayıncılara Content ID çıkmaması
  - Hesapsız, çevrimdışı tek oyunculu tasarım (KVKK/GDPR yükünü minimuma indirir)
  - Steam içerik anketinin dürüst doldurulması (Almanya'da yaş derecesi 15 Kasım 2024'ten beri zorunlu) [8][C/Y]

---

## 1. Gerçekçi Kapsam: Tek Kişi + AI Ajanları

### 1.1 Küçük ekip hit'leri: ekip boyutu ve süre

| Oyun | Ekip | Süre / Takvim | Sonuç | Bizim için ders | Etiket |
|---|---|---|---|---|---|
| Stardew Valley | 1 kişi | ~4 yıl; çıkış Şubat 2016 | Aralık 2024'te 41 milyon+ | Tek kişi uzun soluklu olabilir, ama 2D ve sistem ağırlıklı | [42][R/Y], süre [G/O] |
| Vampire Survivors | 1 kişi (başlangıçta) | Mart 2021'de itch.io'da ücretsiz; varlık harcaması ~1.100 £ | Türünü yarattı | Önce minik ve ucuz prototip, sonra motor değişimi | [69][G/O] |
| Balatro | 1 kişi | ~2,5 yıl | Ocak 2025'te 5 milyon | Tek mekaniğin derinliği | [40][R/Y] |
| Hollow Knight | 3 kişilik çekirdek ekip | 2014 Kickstarter → Şubat 2017 | Kült hit | Küçük ekip + güçlü sanat yönetimi | [48][B/O] |
| Hades | ~20 kişi | EA Aralık 2018 → 1.0 Eylül 2020 | GOTY düzeyi | EA, düzenli içerik ve tam seslendirme | [B/Y] |
| Hades II | Supergiant | EA Mayıs 2024 → 1.0 25 Eylül 2025 | Steam'de ~5,2 milyon (tahmin) | EA → 1.0 modeli | [R/O] |
| Schedule I | 1 kişi | EA Mart 2025 | 459 bin zirve CCU: tek geliştirici rekoru | Sistemik simülasyon + co-op + viral klipler | [36][G/O] |
| Megabonk | 1 kişi | Çıkış 18 Eylül 2025, 9,99 $ | 2 haftada 1 milyon+, zirve ~117 bin CCU | Kanıtlanmış tür + güçlü "juice" | [37][G/O] |
| PEAK | Aggro Crab + Landfall ortak ekibi | ~1 aylık jam, maliyet <200 bin $ | 2 milyon → 10 milyon+ | Co-op klip ekonomisi | [38][G/O] |
| R.E.P.O. | Küçük ekip (semiwork) | EA Şubat 2025 | İstek listesi dönüşümünde medyanın 68 katı | Co-op korku, yayıncı klipleri | [75][G/O], ekip [B/D] |
| Buckshot Roulette | 1 kişi | ~2 ay | ~6 milyon | Mikro kapsam, güçlü kanca | [39][G/O] |
| MiSide | 2 kişi | — | İlk ay 25 milyon $+ (tahmin) | Anime estetiği + güçlü kanca | [R/O] |
| Blue Prince | Çok küçük ekip | ~8 yıl; çıkış Nisan 2025 | Eleştirmen hit'i | Tasarım derinliği uzun sürer | [49][B/O] |
| Clair Obscur: E33 | ~33 kişi, <10 milyon $ | — | 8 milyon | "AAA hissi" 30+ kişiyle mümkün; AI ifşası sonrası ödül kaybı | [R/Y] |
| Palworld | Pocketpair (ekip boyutu doğrulanamadı) | EA Ocak 2024 → 1.0 2026 | ~30,5 milyon | Sistemik dünya + yaratık toplama | [R/O] |

**Çıkarımlar:**
- Tablodaki tek kişilik başarıların ortak noktaları: **dar kapsam, düşük varlık maliyeti** (2D, low-poly, tekrar kullanılabilir), **klipe uygun anlar** ve çoğunlukla **kanıtlanmış bir tür**.
- 3D anime kalitesinde sunum, Hades (~20 kişi) ve E33 (~33 kişi) sınıfında ekiplerle görülüyor.
- Yapay zekâ bu açığı kısmen kapatabilir, ama kapsamı kısmak zorunlu:
  - 1 hub şehir
  - EA'da 3–4 Kapı biyomu
  - 4–6 derin yoldaş
  - Açık dünya yok
  - Co-op en erken 1.0 sonrası

### 1.2 AI destekli geliştirme vakaları (2025–2026)

| Vaka | Ne oldu | Ders | Etiket |
|---|---|---|---|
| fly.pieter.com | Oyun geliştirme deneyimi olmayan bir girişimci Cursor + Claude ile tarayıcı uçuş oyunu yaptı. İddiaya göre 17 günde 1 milyon $ yıllık gelir hızına ulaştı (Mart 2025) | Dağıtım (kurucunun kitlesi) koddan önemli. Premium Steam oyunu için tekrarlanabilir değil | [33][G/O] |
| Relu Games, "Magic Girl Lulupping" | 3 kişi, üretken AI ile 1 ayda Steam'e çıktı (Seul SBA programı) | AI ile hız mümkün. Kalite ve satış verisi yok | [34][G/D] |
| Claude Code "5 ajanlı stüdyo" | Paralel ajanlar bir oturumda 17 görevin 9'unu bitirdi | Görev bölme işe yarıyor, ama küçük oyunlarda | [G/D] |
| **Başarısızlık:** "Claude bütün RTS kodunu yazsın" (Godot) | Geliştirici kodu anlamayı bıraktı, proje terk edildi | **Kod sahipliği insanda kalmalı.** Mimari kararlar, testler ve kod okuma şart | [35][G/O] |
| **Başarısızlık:** Postal: Bullet Paradise | AI sanat suçlamalarıyla duyurudan 1 gün sonra iptal edildi | Görsel pazarlama materyalinde AI izi ölümcül olabiliyor | [32][G/O] |
| Clair Obscur: E33 | Indie Game Awards ödülleri, üretken AI kullanımı nedeniyle geri alındı (Aralık 2025) | Başarılı oyunda bile itibar riski | [R/Y] |
| Steam geneli | 2025 çıkışlarının ~1/5'i AI beyan etti; toplam 7.818 oyun, kütüphanenin ~%7'si. Haziran 2026 Next Fest demolarının %26,5'i beyanlı | AI yaygınlaştı, tek başına ayırt edici ya da öldürücü değil | [31][25][G/O] |
| Geliştirici duygusu (GDC 2026) | Geliştiricilerin %36'sı işte GenAI kullanıyor; %52'si AI'ı sektör için olumsuz görüyor (2025'te %30) | Serbest sanatçı bulurken "AI'lı proje" damgası bir maliyet kalemi | [30][G/O] |
| Godot'nun yükselişi | Haziran 2026 Next Fest demolarında Godot payı %9,2'den %12,6'ya çıktı | Godot ile ticari indie artık olağan | [25][G/O] |

### 1.3 Ne kadar sürede ne yapılabilir? (1 kişi + Claude Code + AI varlık hattı)

| Süre | Gerçekçi çıktı | Gerçekçi değil |
|---|---|---|
| **6 ay** | Oynanabilir prototip + **20–30 dk'lık cilalı dikey kesit** (varış prologu, hub'dan bir parça, 1 Kapı katı, 1 boss, 1 seslendirilmiş yoldaş). Steam sayfası, duyuru fragmanı, Discord | Demo veya EA. Birden fazla biyom. Co-op |
| **12 ay** | 60–90 dk'lık demo (03 raporu: ilk 60–90 dakika). 2–3 biyom, 2–3 boss, 3 yoldaş, Sistem görev döngüsü. Steam Playtest ile kapalı test. 7–10 bin istek listesi hedefi | Tam hikâye. 5+ dil |
| **18 ay** | **Early Access**: Perde 1 (8–15 saat tekrar oynanabilir içerik), EN+JA+ZH-Hans metin, EN'de kilit seslendirme, Steam Deck uyumu | 1.0, konsol |
| **24 ay** | EA'da 2–3 büyük güncelleme, Perde 2, KO/TR/PT-BR, konsol veya yayıncı görüşmeleri | 1.0 cilası |
| **30–36 ay** | 1.0 + Destekçi Paketi + OST (04 raporu) | — |

**Tampon kuralı:** Tahminlere **+%30–50** eklenmeli. Tek kişilik projelerde hastalık, motor sürprizleri ve AI araç değişiklikleri kritik yolu doğrudan etkiliyor.

### 1.4 Dikey kesit (vertical slice) yaklaşımı

- **Tanım:** Oyunun **nihai kalite çıtasındaki** küçük bir dilimi. Bütün katmanlar bu dilimde son hâlinde olmalı:
  - Sanat, animasyon, VFX, ses, UI
  - Savaş hissi, performans, bir parça anlatı
- **Amaç:** Beş soruya evet ya da hayır yanıtı almak:
  1. Çekirdek döngü eğlenceli mi?
  2. AI hattı hedef görünümü tutarlı üretebiliyor mu?
  3. Motor performansı yetiyor mu?
  4. Bir içerik birimi (1 kat, 1 boss, 1 yoldaş sahnesi) kaç günde üretiliyor?
  5. Oyuncular "istek listesine eklerim" diyor mu?
- **Kritik çıktı üretim hızı ölçümüdür.** Örnek: "1 Kapı katı = X gün". Bu ölçüm EA kapsamını ve tarihini matematiksel olarak belirler.

### 1.5 Kilometre taşları ve "bitti" tanımı (Definition of Done)

| Kilometre taşı | "Bitti" tanımı (hepsi sağlanmalı) |
|---|---|
| **Prototip** | Gri kutu (graybox) savaş + Sistem penceresi + 1 Kapı koşusu baştan sona oynanıyor. 60 fps hedef donanımda. En az 10 dış test oyuncusu. Kayıt/yükleme çalışıyor. CI'da headless testler yeşil (08 raporu) |
| **Dikey kesit** | 20–30 dk nihai kalite. Sanat bible'ı kilitli. İçerik birimi üretim süresi ölçülmüş. 50+ kör test. Crash'siz oturum oranı ≥%99. AI varlık manifesti eksiksiz (model, lisans, insan düzenlemesi) |
| **Steam sayfası (Coming Soon)** | İnsan elinden çıkmış capsule/logo. Önce oynanış (gameplay-first) fragmanı. En az 5 ekran görüntüsü. Doğru etiketler. Kısa açıklama EN+JA+ZH. İçerik anketi ve AI beyanı taslağı. Discord ve basın kiti linki |
| **Demo** | 60–90 dk. Kendi başına anlamlı bir sonu var ve "istek listesine ekle" çağrısıyla bitiyor. Ayarlar, kontrolcü desteği, Steam Deck'te oynanabilir. EN+JA+ZH arayüz. Demo derlemesi Steam incelemesinden geçmiş |
| **Next Fest** | Demo fest'ten **en az 1 ay önce** yayında [19]. Kayıt son gününde fragman ve mağaza varlıkları güncel [1]. Yayıncı/VTuber listesine anahtar ve rehber gönderilmiş |
| **Early Access** | Perde 1 tamam. EA S&C (Soru-Cevap) bölümü yazılı yol haritasıyla dolu [15]. Crash oranı düşük. İade gerekçeleri izleniyor. İlk 2 saat cilalı (iade penceresi). Hotfix hattı hazır |
| **1.0** | Tam hikâye, bütün diller + LQA, başarımlar, erişilebilirlik ayarları, Destekçi Paketi ve OST sayfaları |

---

## 2. Takvim: Doğrulanmış Steam Tarihleri ve Önerilen Senaryolar

**Doğrulanmış Steam etkinlikleri [C/Y] [1]–[5]:**

| Etkinlik | Tarih | Önemli son günler |
|---|---|---|
| Next Fest Ekim 2026 | 19–26 Ekim 2026 | Kayıt 31 Ağustos 2026'da kapandı. **Bizim için kaçtı** |
| Sonbahar İndirimi 2026 | 1–8 Ekim 2026 | — |
| Kış İndirimi 2026 | 17 Aralık 2026 – 4 Ocak 2027 | — |
| **Next Fest Şubat 2027** | 22 Şubat – 1 Mart 2027 | Kayıt 10 Ocak · basın önizlemesi için demo 25 Ocak · zorunlu öğeler 8 Şubat · basın önizlemesi 11 Şubat |
| İlkbahar İndirimi 2027 | 18–25 Mart 2027 | — |
| **Next Fest Haziran 2027** | 14–21 Haziran 2027 | Kayıt 25 Nisan · fragman çekimi 3 Mayıs · basın önizlemesi için demo 17 Mayıs · zorunlu öğeler 31 Mayıs |
| Yaz İndirimi 2027 | 24 Haziran – 8 Temmuz 2027 | — |
| Next Fest Ekim 2027 / Şubat 2028 | **Tarihler ilan edilmedi.** Valve'ın Haziran 2027 sayfası "bir sonraki edisyon Ekim 2027'de planlanıyor" diyor (düzeltildi 24.09.2026). Örüntü: Ekim ve Şubat | Son üç fest'te kayıt, fest'ten ~6–7 hafta önce kapandı |

**Diğer fuarlar [G/O] [70]:**
- Tokyo Game Show 2026: 17–21 Eylül 2026. TGS 2027: 16–20 Eylül 2027.
- Digital Games Expo (デジゲー博, Japon indie fuarı): 8 Kasım 2026.
- gamescom 2026: 26–30 Ağustos.
- Steam'in 2026–2027 temalı fest takviminde **anime temalı resmî bir fest yok** [5][C]. Örneğin Party-Based RPG Fest 14–21 Eylül 2026'da yapıldı.

**Senaryolar (bugün = 0. ay, Eylül 2026):**

| Adım | Agresif | **Temel (önerilen)** | Muhafazakâr |
|---|---|---|---|
| Rendering spike + ön üretim | Ekim 2026 | Ekim 2026 | Ekim–Kasım 2026 |
| Dikey kesit | Mart 2027 | **Nisan 2027** | Haziran 2027 |
| Steam sayfası + duyuru | Mart 2027 | **Nisan–Mayıs 2027** | Temmuz 2027 |
| Steam Playtest (kapalı) | Haziran 2027 | **Temmuz–Eylül 2027** | Ekim 2027 |
| Herkese açık demo | Ağustos 2027 | **Kasım–Aralık 2027** | Mart 2028 |
| Next Fest | Ekim 2027 | **Şubat 2028** | Haziran 2028 |
| Early Access | Kasım 2027 – Ocak 2028 | **Mart–Nisan 2028** | Temmuz–Eylül 2028 |
| 1.0 (EA + 9–15 ay) | 2028 sonu | **2029 1. yarı** | 2029 2. yarı |

Notlar:
- Haziran 2027 Next Fest ana oyunla **kullanılmamalı**, çünkü tek hak var ve EA'ya çok uzak kalıyor. O dönem Steam Playtest ile veri toplanmalı [18].
- Zukowski'nin önerisi: Next Fest, çıkıştan önceki "son büyük etkinlik" olsun; demo fest'ten aylar önce yayında olsun [19].

---

## 3. Faz Bazlı Yol Haritası Şablonu (süre, çıktı, KPI, go/no-go)

| Faz | Süre | Ana çıktılar | KPI (hedef) | Go/No-Go kapısı |
|---|---|---|---|---|
| **F0 Ön üretim** | 3–5 hafta | Tasarım sütunları, sanat bible'ı, **anime rendering spike** (08), AI karakter tutarlılık testi, isim ve marka ön araştırması, şahıs şirketi kararı | Test karakteri hedef görünüme ulaşıyor (kör karşılaştırmada ≥3/5). 20 aday isimden ≥3'ü sınıf 9/41'de TR, EU ve US'de temiz | **G0:** Görünüm tutmazsa motor veya stil değişikliği (Unity yedeği, 08). İsim temiz değilse sayfa açılmaz |
| **F1 Prototip** | 8–12 hafta | Gri kutu savaş, Sistem UI, 1 Kapı koşusu, kayıt sistemi, CI | ≥10 dış test oyuncusu. Savaş eğlencesi ≥4/5. ≥%50 "tekrar oynarım". Gönüllü oturum ≥20 dk | **G1:** Başarısızsa 4 hafta iterasyon. İkinci başarısızlıkta çekirdek döngü pivotu |
| **F2 Dikey kesit** | 10–14 hafta | 20–30 dk nihai kalite, üretim hızı ölçümü, duyuru fragmanı | ≥50 kör test. Tamamlama ≥%70. "İstek listesine eklerim" ≥%40. "AI slop" şikâyeti ≤%10. Hedef donanımda 60 fps | **G2:** Üretim hızı EA kapsamını 12 ayda çıkarmaya yetmiyorsa **kapsam kesilir** (biyom/yoldaş sayısı) |
| **F3 Duyuru + üretim** | 4–6 ay | Steam sayfası, Discord, kısa video (Shorts/TikTok) devlog ritmi, Steam Playtest, içerik üretimi | İlk 3 ayda 3–5 bin istek listesi (organik ≥30/gün). Discord ≥500. İstek listesi/takipçi oranı izlenir [28] | **G3:** 3 ayda <1.000 istek listesiyse demo öncesi **konumlandırma yenilenir** (capsule, kanca, fragman). Ücretli işler ertelenir |
| **F4 Demo** | 8–12 hafta | 60–90 dk demo + yayıncı kiti | Demo→istek listesi ≥%15–20 (medyan %19,3 [22]). Medyan demo süresi ≥30 dk. Demo incelemeleri ≥%85 olumlu | **G4:** Fest'e girerken ≥7–10 bin istek listesi. Altındaysa fest bir sonraki pencereye kaydırılır |
| **F5 Next Fest** | 1 hafta (+6 hafta hazırlık) | Canlı yayın (isteğe bağlı), güncel fragman | Fest'te +5–15 bin istek listesi (~13 bin+ ≈ üst %5, medyan ~800 [19]; düzeltildi 24.09.2026) | **G5 (EA kararı):** Toplam ≥15–20 bin → EA. 7–15 bin → EA yapılır ama gelir beklentisi ve harcama düşürülür. <7 bin → 3–6 ay erteleme ve yeniden pazarlama |
| **F6 Early Access** | 9–15 ay | Perde 1, 6–10 haftalık güncelleme ritmi | İlk hafta dönüşümü ≥%10 [75]. İnceleme ≥%80 olumlu. İade ≤%10. Medyan oynama süresi ≥4 saat. Oyuncuların ≥%50'si 2. saate ulaşıyor | **G6 (EA +30 gün):** İnceleme <%70 ise yeni içerik dondurulur, 4 haftalık düzeltme sprinti yapılır |
| **F7 1.0** | 3–4 ay cila | Tam hikâye, yerelleştirme ve LQA, Destekçi Paketi, OST | Yeniden istek listesi e-postası [13]. İnceleme ≥%85 | **G7:** Konsol ve Asya yayıncısı görüşmesi için 1.0 verileri kullanılır |

**Kapıların arkasındaki veri:**
- Next Fest'in sonucu büyük ölçüde fest öncesi istek listesine bağlı:

| Fest öncesi istek listesi | Fest'te kazanılan (medyan) [20] |
|---|---|
| 0–999 | 322 |
| 1.000–9.999 | 1.006 |
| 10.000–99.999 | 5.215 |

  (Doğrulama notu 24.09.2026: Bu kademe medyanları bağımsız olarak doğrulanamadı; ikincil özetlerde 1.000 altı için 462 gibi farklı değerler geçiyor. Güçlü korelasyon (r≈0,825) ve "fest ivmeyi büyütür" sonucu doğrulandı.)

- Steam'e göre inceleme puanı %40'ın üstünde kaldıkça görünürlüğü etkilemiyor [14][C].
- Ancak ilk 7 günde "Mixed" (%67) inceleme alan oyunlar istek listesini zayıf satışa çeviriyor [75][G].
- 2025 verisinde sayfası çıkıştan çok önce açılan oyunlar (medyan 411 gün) daha zayıf dönüştü (üst 20'de medyan 214 gün) [75][G/O]. Valve ise erken sayfanın bir dezavantajı olmadığını söylüyor [11][C].
- Uzlaştırma: Sayfa **sanat yönü kesinleşince** açılmalı ve çıkışa kadar sürekli yeni haberle beslenmeli.

---

## 4. Bütçe

### 4.1 Birim maliyetler

| Kalem | Değer | Etiket |
|---|---|---|
| Steam Direct | Uygulama başına **100 $**. İade edilmez; uygulama 1.000 $ düzeltilmiş brüt gelire ulaşınca mahsup edilir. Ödemeden sonra 30 gün bekleme var | [9][10][C/Y] |
| Demo, Playtest, OST sayfası | Playtest, Valve'ın ifadesiyle "ücretsiz" bir alt uygulama [18][C/Y]. Demo belgesinde ayrı bir ücretten söz edilmiyor (demo ana oyuna bağlı alt uygulama) [C/O]. OST/DLC için ek başvuru ücreti yok [R/O] | [18][C]; [R] |
| TÜRKPATENT 2026 | Başvuru: 1. sınıf 2.820 TL + 2. sınıf 2.820 TL + 3. ve sonraki her sınıf 3.150 TL. Tescil ücreti 7.010 TL. **Sınıf 9 + 41 için toplam ≈12.650 TL** | [60][G/O] |
| EUIPO | 850 € (1 sınıf, online) + 50 € (2. sınıf) + 150 € (3. ve sonraki her sınıf) | [63][G/B-O] |
| USPTO | Sınıf başına 350 $ temel başvuru (18 Ocak 2025'ten beri). Eksik bilgi sunulursa ek ücret | [62][G/O] |
| Yerelleştirme (kelime başı) | EN→JA/ZH/KO ~0,10–0,20 $; EN→ES/PT-BR/FR/DE ~0,08–0,14 $; EN→TR/RU ~0,06–0,12 $; LQA için +%10–20. **Bu oturumda doğrulanamadı.** 3 teklif alınmalı | [B/D] |
| İnsan seslendirme | Sendikasız EN: karakter veya paket başına düşük yüzler–birkaç yüz $. SAG-AFTRA: 4 saatlik oturum ~1.000 $+. Japon seiyuu: ajans teklifi gerekir | [R 07][D] |
| İnsan sanatı | Key art 500–3.000 $; Steam capsule seti 300–2.000 $; oyuna hazır 3D anime karakter 1.500–6.000 $. **Doğrulanamadı** | [B/D] |
| AI araçları | Görsel ~30 $/ay ile ~900 görsel (Gemini Batch). 3D/animasyon 30–80 $/ay. Sesin küçük bütçe paketi 1,5–6 bin $ | [R 05/06/07] |

**Yerelleştirme formülü:** kaynak kelime × kelime başı ücret × (1 + LQA oranı).
- Örnek: 50 bin kelime × 0,12 $ × 1,15 ≈ **6.900 $/dil** (D).
- EA'da yalnızca UI + ana hikâye çevrilirse kelime sayısı düşer. Yazım aşamasında **kelime bütçesi** konmalı.

### 4.2 AI neyi ikame eder, insan nerede şart?

| Alan | AI'ın payı | İnsanın zorunlu payı | Gerekçe |
|---|---|---|---|
| Kod | Yüksek (Claude Code) | Mimari, kod okuma ve inceleme, oyun hissi ayarı | RTS vakası [35] |
| Konsept ve fikir | Çok yüksek | Seçme, bible'a uygunluk | — |
| **Key art, logo, capsule** | Yalnızca referans | **Tamamen insan** | Telif korunabilirliği [56], marka, "AI slop" riski [32] |
| Karakter sayfaları | Taslak | Temizlik, tutarlılık, son çizim | 05 raporu |
| 3D (prop, canavar) | Yüksek | Retopo, temizlik | 06 raporu |
| Kahraman karakterleri | Orta (VRoid + AI) | Yüz ve saç cilası | 06 raporu |
| Animasyon | Temel hareketler (video veya metinden harekete) | İmza hareketler, zamanlama | 06 raporu |
| Metin ve anlatı | Taslak, varyasyon | Ses tonu, ana hikâye, tutarlılık | 09 raporuyla uyumlu |
| Yerelleştirme | Ön çeviri | **JA ve ZH için insan LQA** | Anime kitlesi çeviri kalitesine çok hassas |
| Seslendirme | "Sistem" sesi (kurgu gereği sentetik), NPC bark'ları | Ana kadro | 07 raporu, SAG-AFTRA 2025 |
| Müzik | Ortam varyasyonları | Ana tema, leitmotif'ler | OST satışı için telif sahibi olunan müzik gerekir |
| QA | Otomatik test, görsel regresyon | Oynanış testi | 08 raporu |
| Pazarlama | Metin taslağı, planlama | **Geliştiricinin yüzü ve sesi**, topluluk ilişkisi | Özgünlük, "Dave the Diver modeli" [G] |
| Hukuk | Taslak | Avukat ve mali müşavir onayı | — |

### 4.3 Bütçe tablosu (USD, EA'ya kadar ~18 ay, geliştiricinin geçimi hariç)

| Kalem | Asgari | Temel | İdeal | Not |
|---|---|---|---|---|
| Steam Direct | 100 | 100 | 100 | [9] |
| Claude / LLM aboneliği ve API | 0 (mevcut plan/kredi) | 1.800 | 3.600 | 100–200 $/ay varsayımı [D] |
| AI üretim araçları (görsel, 3D, ses, video) | 450 | 1.800 | 4.500 | 25 / 100 / 250 $/ay [R] |
| Yerel üretim için GPU'lu donanım | 0 | 1.200 | 3.000 | [D] |
| İnsan sanatı (key art, capsule, karakter son çizimleri, UI) | 1.000 | 6.000 | 20.000 | [D] |
| 3D/animasyon temizliği ve mocap | 0 | 3.000 | 12.000 | [D] |
| Müzik (besteci: tema + leitmotif) | 300 | 3.000 | 10.000 | [D] |
| Seslendirme (EN ana kadro, sonra JA) | 300 | 4.000 | 15.000 | [R 07] |
| Yerelleştirme (EA dilleri) | 500 (AI + topluluk kontrolü) | 12.000 (JA + ZH profesyonel) | 35.000 (6 dil + LQA) | [D] |
| Fragman ve çekim | 0 | 1.500 | 8.000 | [D] |
| Pazarlama (reklam testi, anahtar dağıtım aracı, festival, PR) | 200 | 3.000 | 15.000 | [D] |
| Hukuk ve marka | 400 (TR marka + şablonlar) | 3.500 (TR + EU + US + sözleşme incelemesi) | 10.000 (+ Madrid/JP/CN, sürekli danışmanlık) | [60][62][63] |
| Mali müşavir ve şirket giderleri | 1.800 | 2.700 | 5.400 | [D] |
| Fuar ve seyahat | 0 | 1.000 | 8.000 | [D] |
| Playtest teşvikleri ve dış QA | 0 | 500 | 3.000 | [D] |
| **Ara toplam** | **5.050** | **45.100** | **152.600** | |
| Beklenmeyen giderler (%15) | 758 | 6.765 | 22.890 | |
| **Toplam** | **~5,8 bin $** | **~52 bin $** | **~175 bin $** | |

**Karşılaştırma:** 04 raporunun kötümser senaryosu (5 bin kopya) ~49 bin $ net gelir öngörüyordu. Temel bütçe bu tutara denk geliyor. Bu yüzden:

### 4.4 Harcama kapıları (bütçeyi istek listesine bağlamak)

- **G2'ye kadar** (dikey kesit) yalnızca asgari sütun harcanır. Tek istisna: capsule ve logo (~1–2 bin $).
- **G3 sonrası** (≥3–5 bin istek listesi): besteci ana tema, fragman.
- **G4 sonrası** (≥7–10 bin): JA+ZH profesyonel yerelleştirme, EN ana kadro seslendirme.
- **G5 sonrası** (≥15–20 bin): ideal sütuna doğru genişleme (KO/PT-BR/ES, JA dublaj, fuar standı).
- Konsol ve JP/CN pazarlaması için **yayıncı veya port partneri**, veri elde edildikten sonra ve güçlü pozisyondan seçilir (04 raporu).

---

## 5. Pazarlama ve Pazara Çıkış

### 5.1 Steam mekaniği: doğrulanmış kurallar [C/Y]

| Kural | Kaynak |
|---|---|
| Coming Soon sayfası çıkıştan **en az 2 hafta** önce yayında olmalı. İnceleme 3–5 iş günü sürüyor; en az 7 iş günü önce gönderilmeli | [11][12] |
| Valve: "İki yıl önce istek listesine ekleyen, iki hafta önce ekleyen kadar satın almaya yatkın olabilir" (oyun çok değişmezse) | [11] |
| İstek listesine e-posta gider: çıkışta, EA→1.0 geçişinde ve **≥%20, >8 saat** süren indirimlerde. Aynı uygulama için 2 hafta bekleme süresi var | [13] |
| Demo çıkınca istek listesine **bir kez** bildirim gönderilebilir (demo çıkışından sonraki 2 hafta içinde, geliştirici tetikler) | [13] |
| İstek listesi, Popular Upcoming dışında algoritmik görünürlükte "çoğunlukla" etken değil. Sayfa trafiği ve dönüşüm oranı etken değil. İnceleme puanı ≥%40 oldukça etken değil | [14] |
| Next Fest'in ilk günlerinde yerleşim rastgele, sonra davranışa göre kişiselleştiriliyor. Etiketler ve 1–2 ana kategori sıralamayı belirliyor | [1] |
| Fest fragmanına seçilmek için kayıt son gününde herkese açık bir fragman ve güncel varlıklar gerekiyor | [1] |
| Fest sırasında Playtest açık tutulmamalı: oyuncuları böler | [1] |
| Fragman: ilk fragman **oynanış** olmalı. Oyuncuyu yakalamak için "10 saniyeden az" zaman var. Mikro fragman ilk videodan otomatik üretiliyor. 1920×1080 çözünürlük | [16] |
| EA: fiyat artışından sonraki 30 gün içinde indirim yapılamıyor; bu **1.0 çıkış indirimini de kapsıyor**, yani EA→1.0 fiyat artışı 1.0'dan en az 30 gün önce yapılmalı (düzeltildi 24.09.2026). EA'da kalıcı indirim yasak. Gelecek için somut vaat verilmemeli | [15] |
| Reklam tabanlı iş modeli ve blokzincir/NFT Steam'de yasak. Ödeme işlemcisi kurallarını ihlal eden yetişkin içerik de yasak | [10] |

### 5.2 İstek listesi hedefleri: 2026 gerçeği

- **Popular Upcoming:**
  - Eski rehber: çıkışta ~7 bin istek listesi (Zukowski, 2023) [24][G].
  - Haziran 2026'dan beri eşik tahminen ~100 bin [21][76][G/O]. **Bizim hedefimiz değil.**
- **Personal Calendar:** Kişiye göre öneriyor. Zukowski indie için olumlu görüyor [21].
- **Çıkış hedefi (temel):** ≥20 bin istek listesi.
  - 10 $ üstü oyunlarda ilk hafta dönüşüm medyanı 0,10× [75] → ~2.000 ilk hafta satışı. 04 raporundaki birim net (EA 19,99 $ için ~7,5 $) ile ~15 bin $ ilk hafta neti.
  - Dönüşüm oyunlar arasında **10–20 kat** değişebiliyor [75].
- **İstek listesi/takipçi oranı:** Aşırı yüksek oran (ör. 35×) viral ama doğrulanmamış ilgiye; ~12× istikrarlı hayran kitlesine işaret ediyor [28][G/O].
- **Demo CCU:** Demo zirve CCU'dan çıkış CCU'suna medyan çarpan **~3×** (2.569 oyunluk örneklem) [26][G/O]. Demo gerçek zamanlı izlenmeli.

### 5.3 Next Fest stratejisi

1. **Tek hak:** Çıkıştan hemen önceki son büyük etkinlik olarak planlanmalı [19].
2. Demo fest'ten **1–3 ay önce** yayında olmalı. "Gölge çıkış" (shadow drop; fest başlarken habersiz demo) veriyle desteklenmiyor [19].
3. Fest öncesi istek listesi en güçlü gösterge (r≈0,825; Şubat 2026 verisi) [19]. Fest yalnızca var olan ivmeyi büyütüyor. Demosunu fest'ten aylar önce yayımlayan oyunlar, demoyu fest sırasında açanlara göre medyanda ~2,5 kat istek listesi kazandı (ikincil özet, düzeltildi 24.09.2026).
4. Haziran 2026'da demo sayısı %66 arttı (4.382). Üst %10'un fest'teki takipçi kazancı %25 düştü [25]. Rekabet artıyor; **net bir "kanca" ve doğru etiketler** şart.
5. Fest'te günlük geliştirici yayını isteğe bağlı [1]. Asıl kaldıraç yayıncılar ve VTuber'lar (§5.5).

### 5.4 Kanallar

| Kanal | Nasıl | Not |
|---|---|---|
| **TikTok / YouTube Shorts / Reels** | Haftada 2–3 klip: "Sistem bildirimi" anı, rütbe yeniden değerlendirme sahnesi, boss aura patlaması. Gerçek oynanış, altyazılı | Kısa video artık yeni oyunları keşfettirmenin birinci sürücüsü (Dear Passengers: tek fragmanla 3 günde 1 milyon istek listesi, uç vaka) [28][G/O] |
| **X (Twitter)** | Japonya'da ana kanal. #indiedev, #ゲーム制作, #screenshotsaturday | [B/O] |
| **Reddit** | r/isekai, r/manhwa, r/sololeveling, r/LitRPG, r/progressionfantasy, r/JRPG, r/ARPG, r/roguelites, r/IndieDev, r/indiegaming. **Her alt forumun tanıtım kuralı okunmalı**; r/anime ve r/gamedev tanıtım konusunda sıkı | Üye sayıları doğrulanamadı [B/D]. Önerilen tutum: "Dave the Diver modeli", yani Reddit'e az ama değerli katkı [G] |
| **Discord** | Geliştiricinin doğrudan yanıt verdiği sunucu: devlog, playtest rolü, JA/ZH kanalları | Dave the Diver: yapamadıklarını ve takvimi şeffafça açıklama [G/O] |
| **Bilibili / Weibo** (ZH) | Oynanış videoları ve Çince açıklama | Basitleştirilmiş Çince Steam'in ilk iki dilinden biri [R] |
| **Steam etkinlikleri** | Üçüncü taraf festivaller: 2019'dan bu yana 470 festival, 31.285 oyun. 2020 sonrası çıkan oyunların ~%31'i en az bir festivalde yer aldı; medyan 2 kez [23][G/O] | Anime/JRPG/ARPG küratörlerine başvurulmalı |

### 5.5 Yayıncı ve VTuber'lara ulaşma

- **Yayıncı sayısı, izlenme süresinden önemli:**
  - Gamesight (PvP FPS örneklemi): 3. gündeki aktif yayıncı sayısı uzun vadeli tutunmayı %72 isabetle öngördü [29][G/O].
  - Tek oyunculu oyunlara genellenmesi belirsiz. Yine de "çok sayıda küçük yayıncı" stratejisini destekliyor.
- **VTuber'lar (JA/EN):**
  - Japon ajansları ve yayıncılar genelde net bir **yayın ve para kazanma izni rehberi** (配信ガイドライン) istiyor [B/O].
  - Mağaza sayfasında ve sitede EN/JA "Yayın serbest, para kazanma serbest, spoiler sınırı: X" metni olmalı.
- **Uygulama:** Anahtar dağıtım platformları (Keymailer, Lurkit gibi; [B/O]), benzer oyunları oynamış yayıncıların listesi, kişiselleştirilmiş e-posta. Takipçi sayısı yerine türe yakınlık esas alınmalı [G].
- **Müzik:** OST'yi Content ID'ye **kaydetmeyin**. Yayıncılara telif talebi gelirse pazarlama zarar görür [B/O].

### 5.6 Fuarlar ve konvansiyonlar

| Etkinlik | Tarih | Değer | Etiket |
|---|---|---|---|
| TGS 2027 | 16–20 Eylül 2027 | JP basını ve yayıncılar. Indie bölgesi | [70][G/O] |
| デジゲー博 (Digital Games Expo) | 8 Kasım 2026 (2027 tarihi ilan edilmedi) | Japon indie topluluğu | [70][G/O] |
| INDIE Live Expo | Yılda 2 kez, çevrim içi | JP odaklı indie vitrin, ücretsiz başvuru dönemleri var | [70][G], ücret [B/D] |
| BitSummit (Kyoto) | Genelde Temmuz | JP indie | [B/D] |
| gamescom | Ağustos sonu | Batı basını ve yayıncılar | [70][G/O] |
| Türkiye: Kimicon (Bursa, ~10 bin katılımcı), Comic Con İstanbul ve 80+ anime/cosplay etkinliği | Değişken | Yerel topluluk ve TR basını; düşük maliyet | [R 01][D] |

### 5.7 Japonya, Çin, Kore ve yerelleştirme önceliği

- **Neden bu diller:**
  - Anime gacha harcamasının %41–44'ü Japonya'dan geliyor [R].
  - Basitleştirilmiş Çince, Steam'in ilk iki dilinden biri [R].
  - Steam kullanıcılarının %60'tan fazlası İngilizce dışı dil kullanıyor [17][C].
- **Sıra:**
  - EA: EN + JA + ZH-Hans
  - 1.0: + KO + TR + PT-BR + ES (RU isteğe bağlı)
  - Mağaza sayfası ve kısa açıklama, sayfa açılışında en az EN/JA/ZH olmalı.
- **Japonya:** JA ses (dual audio) 2. fazda. JA metinde oyun terimleri sözlüğü (Sistem, rütbe, beceri adları) insan tarafından kilitlenmeli. X ve TGS/デジゲー博/INDIE Live Expo kanalları kullanılmalı.
- **Çin:**
  - Global Steam satışı ISBN kapsamında değil; yalnızca Çin'e resmî yayında ISBN gerekiyor [R/D].
  - Bilibili'de erken varlık gösterilmeli.
  - İçerik (iskelet, kan, siyasi semboller) bilinçli seçilmeli [B/O].
- **Kore:** Solo Leveling'in anavatanı, "hunter/gate" terimleri tanıdık. KO yerelleştirme 1.0'da.
- **Türkiye:** Gelir değil, topluluk ve PR pazarı (04). TR arayüz ve altyazı iyi yapılırsa belirgin bir farklılaştırıcı olur (01).

### 5.8 Basın kiti ve fragman

- **Basın kiti:** `presskit.html` (presskit()'in statik site versiyonu, npm'de `presskit`) [71][C].
  - İçerik: kısa ve uzun açıklama, bilgi tablosu, logo (PNG/SVG), 10+ ekran görüntüsü, GIF, fragman linki, geliştirici hikâyesi.
  - **AI kullanım beyanı** (Steam formundakiyle tutarlı) ve iletişim bilgisi.
- **Fragman sırası:**
  1. Duyuru fragmanı: 60–75 sn, ilk 5 sn'de oynanış ve kanca.
  2. Oynanış fragmanı: mağazada ilk sırada [16].
  3. Next Fest ve EA fragmanları: mevcut görüntülerin yeniden kurgusu [G].
- İlk saniyelerde logo veya stüdyo kartı gösterilmemeli [G][16].

---

## 6. Hukuk ve Politika

> Bu bölüm genel bilgidir, hukuki görüş değildir. Sözleşmeler ve marka tescili için avukat, vergi için mali müşavir gerekir.

### 6.1 Fikrî mülkiyet: trope serbest, ifade korunur

- **Serbest olanlar:** Fikirler, sistemler ve mekanikler telif konusu değil. Durum penceresi, rütbe, zindan katları, kamyon klişesi kullanılabilir. İsimler ve kısa ifadeler de telifle korunmaz, **ama marka olabilir** [R 01, Circular 33].
- **Kaçınılacaklar:** "Look and feel" birebir kopyalanmamalı (Tetris v. Xio) [R 01]. Solo Leveling pencere tasarımı, "Arise", "Shadow Monarch", "Familia/Falna", "Orario" kullanılmamalı.
- **İsim araştırması (F0'da):**
  - TÜRKPATENT araştırması: e-Devlet ile ücretsiz [61][G]
  - EUIPO eSearch veya TMview, USPTO Trademark Search, WIPO Global Brand Database [B]
  - Steam'de aynı ya da benzer ad
  - Alan adı ve sosyal medya kullanıcı adları
- **İsim seçimi:** "Isekai" gibi tanımlayıcı kelime tek ayırt edici öğe olmamalı. Fonetik benzerlik de itiraz sebebi olabilir [61].

### 6.2 AI çıktılarının telifi

| Yargı alanı | Durum | Etiket |
|---|---|---|
| ABD | Telif Ofisi Part 2 raporu (29 Ocak 2025): yalnızca prompt yazmak yeterli değil. İnsanın ifade katkısı (düzenleme, seçme, dönüştürme) vaka bazında korunabilir [56]. D.C. Circuit Thaler kararı (18 Mart 2025) [58], Yüksek Mahkeme temyizi reddetti (2 Mart 2026, dosya 25-449) [57] | G/O |
| AB | Özgünlük için "yazarın kendi entelektüel yaratımı" (CJEU içtihadı) gerekiyor. Saf AI çıktısı büyük olasılıkla korunmuyor | B/O |
| Türkiye | FSEK, "sahibinin hususiyetini taşıyan" insan yaratımı arıyor. Saf AI çıktısının korunmaması muhtemel. Emsal bu oturumda doğrulanamadı | B/D |

**Uygulama:**
- Her varlık için bir manifest tutulmalı: model, lisans, prompt/seed, insan düzenlemesinin açıklaması, tarih (05 ve 07 raporları).
- Logo, key art ve kahraman tasarımları **insan eseri** olmalı. Koruma ve marka için bu gerekli.

### 6.3 Steam AI beyanı (resmî metin, [7][C/Y])

- Anket üç bölümden oluşuyor: genel içerik (bölgesel yaş derecelerini üretir), olgun içerik, **üretken AI içeriği**.
- Kapsam: "oyunla birlikte gelen ve oyuncunun tükettiği" sanat, ses, anlatı, yerelleştirme. Geliştirme ortamındaki verimlilik araçları "odak değil". 16 Ocak 2026 form güncellemesini aktaran haberlere göre mağaza sayfası, Steam topluluk varlıkları ve pazarlama materyallerindeki AI içeriği de serbest metin alanında anlatılmalı; fragman, capsule veya ekran görüntüsünde AI kullanıldıysa beyana eklenmeli (düzeltildi 24.09.2026).
- **Önceden Üretilmiş:** Diğer içerikle aynı incelemeden geçer (yasa dışı veya ihlal edici içerik yok; pazarlama ile oyun tutarlı).
- **Canlı Üretilen:** Buna ek olarak yasa dışı içerik üretimini engelleyen **koruma önlemleri** anlatılmalı. Canlı AI ile "Adult Only" cinsel içerik kabul edilmiyor.
- Oyun yayınlandıktan sonra anketin bazı alanları ancak Steam Destek üzerinden değiştirilebiliyor.
- **Öneri:** Beyan somut ve dürüst olmalı. Örnek: "Arka plan varyasyonları ve NPC bark sesleri AI ile üretildi, insan tarafından düzenlendi. Ana karakterler, key art ve ana kadro sesleri insan eseridir. Kod geliştirmede Claude Code kullanıldı." Son cümle zorunlu değil, ama kitlenin %56'sı bu bilgiyi istiyor [27].

### 6.4 AB Yapay Zekâ Yasası: md. 50 bizim için ne demek?

| Durum | Yükümlülük | Etiket |
|---|---|---|
| Takvim | Md. 50, 2 Ağustos 2026'dan beri uygulanıyor. Digital Omnibus (Tüzük 2026/1744; AB Resmî Gazetesi 24 Temmuz 2026, yürürlük 27 Temmuz 2026) Ek III yüksek risk kurallarını 2 Aralık 2027'ye, Ek I kurallarını 2 Ağustos 2028'e erteledi; md. 50'ye dokunmadı. 50(2) için eski sistemlere 2 Aralık 2026'ya kadar süre var | [52][53][G/O] |
| Önceden üretilmiş AI sanatı ve sesi (bizim ana kullanımımız) | Md. 50(2)'deki makinece okunabilir işaretleme yükümlülüğü **üretken AI sağlayıcısına** ait (Google vb.). Md. 50(4), kullanıcının (deployer) yükümlülüğü ve **deepfake** ile sınırlı. Kurgusal ve sanatsal eserlerde beyan, "eserin sunumunu ve keyfini bozmayacak" şekilde yapılabiliyor (ör. künye, mağaza sayfası) | [51][G/Y metin] |
| Canlı LLM NPC veya Sistem sohbeti (ileride) | Md. 50(1): doğal kişilerle doğrudan etkileşen AI sistemlerinde, durum açık değilse kişiler AI ile etkileşimde olduklarını bilmeli → oyun içi bildirim ve ayar | [51][G/O] |
| Yaptırım | Md. 50 ihlalinde 15 milyon €'ya veya küresel cironun %3'üne kadar ceza. KOBİ'lerde ikisinden düşük olan uygulanır (md. 99(6)) | [55][G/O]; KOBİ [B/O] |
| Rehberlik | Komisyon'un md. 50 kılavuzu (taslak 8 Mayıs 2026) ve AI içerik işaretleme uygulama kuralları (Code of Practice) süreci devam ediyor | [54][G/O] |

**Sonuç:** Önceden üretilmiş içerikle giden tek oyunculu bir oyun için yük hafif. Künye ve mağaza sayfasındaki AI beyanı Steam ile AB'yi birlikte karşılar. **EA'da canlı LLM özelliği olmaması** bu riski de sıfırlar.

### 6.5 KVKK / GDPR

- **Tasarım ilkesi:** Hesap yok, çevrim dışı tek oyunculu oyun, ödeme Steam'de. Bu durumda işlenen kişisel veri çok az.
- **Yine de kapsamdakiler:** Bülten e-postası, playtest başvuru formu, Discord moderasyonu, analitik ve crash raporları (IP, cihaz kimliği).
- **KVKK:**
  - md. 10 aydınlatma metni gerekli. Ticari e-posta için açık onay ve İYS kaydı gerekebilir [B/O].
  - 7499 sayılı Kanun değişikliğiyle (yürürlük 1 Haziran 2024) yurt dışı aktarım "uygun güvence" rejimine geçti. Standart sözleşme imzadan sonra **5 iş günü içinde** Kurum'a bildirilmeli [64][G/O]. Yabancı analitik ve e-posta servisleri bu kapsamda.
  - VERBİS kaydı: çalışan sayısı <50 ve yıllık bilanço <100 milyon TL ise (ana faaliyet özel nitelikli veri işlemek değilse) muafiyet [65][G/O].
- **GDPR:**
  - AB'deki kişilere hizmet sunuluyor veya davranışları izleniyorsa uygulanır (md. 3(2)) [B/Y].
  - AB temsilcisi (md. 27) şartı, arızi ve düşük riskli işlemede istisna tanıyor [B/O].
- **Öneri:**
  - Telemetri ve crash raporu **varsayılan kapalı, isteğe bağlı** (opt-in) olsun.
  - E-posta listesi çift onaylı (double opt-in) olsun.
  - Sitede EN/TR gizlilik politikası ve aydınlatma metni bulunsun.
  - Çocuklara yönelik (13 yaş altı) pazarlama yapılmasın (COPPA).

### 6.6 Yaş derecelendirme

- **Steam [C/Y]:** Steam'in içerik anketi bölgesel yaş dereceleri üretiyor [7].
  - **Almanya:** 15 Kasım 2024'ten beri yaş derecesi olmayan oyun gösterilmiyor. USK derecesi ya da Valve'ın kendi derecelendirmesi kabul ediliyor [8].
  - **Endonezya:** Benzer bir zorunluluk yolda (IGRS/Komdigi) [8b].
  - Başka mağazada IARC ile alınmış USK/IGRS derecesi Steam'e **girilmemeli** [8].
- **Diğer mağazalar:** Konsol ve mobil dijital mağazalarda IARC anketi geliştiriciye ücretsiz [B/O]. Fiziksel veya perakende sürümde PEGI/ESRB ücretli; yayıncıya bırakılmalı [B/D].
- **Hedef:** PEGI 12/16, ESRB T. Kumarhane mini oyunu yok (04 raporu).
- **PEGI Haziran 2026 değişikliği (düzeltildi 24.09.2026):** Yeni başvurularda ücretli rastgele öğe → en az PEGI 16; süreli/adet sınırlı satın alma teklifi → en az PEGI 12; NFT/blokzincir → PEGI 18; engelleme, raporlama veya filtre aracı olmayan sınırsız çevrimiçi iletişim → PEGI 18. İleride co-op ve sohbet eklenirse engelleme/raporlama aracı zorunlu tasarım gereksinimi olmalı; aksi hâlde konsol sürümü PEGI 18 alır.

### 6.7 EULA ve gizlilik politikası

- Steam Abone Sözleşmesi temel çerçeveyi sağlıyor [10]. Özel EULA kısa tutulmalı ve şunları içermeli:
  - Lisans kapsamı
  - Mod politikası
  - Yayın ve para kazanma izni
  - AI beyanına atıf
  - Veri işleme (varsa)
- Mağaza sayfasında "online gerekmez" bilgisi belirtilmeli.

### 6.8 Müzik lisansı

- **Besteciyle sözleşme:** Eser sahipliği veya münhasır lisans; kapsamı oyun, OST satışı, dijital müzik dağıtımı, fragman ve sinkronizasyon. Besteci bir meslek birliği (MESAM/MSG, JASRAC vb.) üyesiyse yönetim durumu sözleşmede açıkça yazılmalı [B/D].
- **Content ID:** Yayıncıların önünü açmak için beyaz liste ya da hiç kayıt olmaması tercih edilmeli [B/O].
- **AI müzik:** Yalnızca ticari lisansı net araçlar (07 raporu). Suno ve Udio'dan kaçınılmalı.

### 6.9 Serbest çalışan (freelancer) sözleşmeleri

- **Türkiye (FSEK):**
  - Mali hakların devri **yazılı olmalı ve devredilen haklar tek tek sayılmalı** (md. 52) [67][B/O-Y].
  - Manevi haklar devredilemez; değişiklik ve isim konusunda muvafakat alınmalı [B/O].
- **ABD:** Siparişle yaptırılan eser, ancak yazılı sözleşme varsa ve 9 kategoriden birine giriyorsa (ör. görsel-işitsel eserin parçası) "work made for hire" sayılıyor [68][B/O]. Buna ek olarak **yedek devir maddesi** (assignment) konmalı.
- **Zorunlu maddeler:**
  - Tam devir ve lisans
  - Özgünlük garantisi ve üçüncü kişi hakkı ihlal etmeme taahhüdü
  - **AI maddesi:** Serbest çalışan hangi AI'ları kullandığını beyan eder. Bizim materyallerimiz model eğitiminde kullanılmaz. **Ses klonlama yalnızca ayrı yazılı rıza ve ek ücretle** yapılır (07 raporu, SAG-AFTRA 2025)
  - Gizlilik, künyede isim, çıkıştan sonra portföy hakkı
  - Ödeme kilometre taşları, uygulanacak hukuk

### 6.10 Marka tescili

- **TÜRKPATENT:**
  - Süreç 6–12 ay: şekli inceleme → mutlak ret incelemesi → bültende yayın, ardından **2 aylık itiraz süresi** → tescil [61][G/O].
  - Koruma 10 yıl, yenilenebilir.
  - 2026 ücretleri §4.1'de [60].
- **Sıra:**
  1. Steam sayfası açılmadan önce TR başvurusu (sınıf 9 ve 41)
  2. EA'dan önce EUIPO ve USPTO (ya da Madrid Protokolü üzerinden) [B/O]
  3. İleride JP/CN/KR (yayıncıyla birlikte)

### 6.11 Türkiye'ye özgü iş ve vergi notları (ayrıntı 04 raporunda)

- Gelir öncesi dönemde şahıs şirketi yeterli.
- **2026 değişiklikleri (mali müşavirle teyit edilmeli) [69][G/D]:**
  - Genç girişimci kazanç istisnası üst sınırı 400.000 TL
  - Bağ-Kur prim desteği 1 Ocak 2026'dan itibaren kaldırıldı (7566 sayılı Kanun)
  - Yurt dışına verilen yazılım hizmetlerinde kazanç indirimi %100'e çıktı (gelirin Türkiye'ye getirilmesi şartıyla). Doğrulandı: 11257 sayılı Cumhurbaşkanı Kararı (Nisan 2026), 1 Ocak 2026'dan başlayan dönemler için %80'den %100'e. Steam oyun satışının "yazılım hizmeti" sayılıp sayılmayacağı belirsiz (24.09.2026)
  - Genç girişimci 400.000 TL ve Bağ-Kur desteğinin kaldırılması (7566 sayılı Kanun, 1 Ocak 2026'dan sonra işe başlayanlar için) doğrulandı. GVK 18 eser satışı istisnasında 2026 sınırı 5.300.000 TL (24.09.2026)
- Steam vergi mülakatında W-8BEN ile ABD stopajı %10 (04 raporu).

---

## 7. En Büyük 15 Üretim Riski ve Önlemleri

| # | Risk | Olasılık / Etki | Önlem |
|---|---|---|---|
| 1 | **Kapsam şişmesi** (açık dünya, co-op, çok yoldaş) | Y / Y | Hub + instanced Kapı yapısı. EA kapsamı G2'de ölçülen üretim hızına göre hesaplanır. Co-op 1.0 sonrasına kalır. "Yapılmayacaklar listesi" ADR olarak yazılır |
| 2 | **Anime 3D görünümün Godot'da tutmaması** | O / Y | F0 rendering spike kapısı. Unity yedek planı (08) |
| 3 | **AI varlık tutarsızlığı ve "AI slop" algısı** | Y / Y | Sanat bible'ı, karakter LoRA'ları, insan rötuşu. Key art, capsule ve logo %100 insan eseri. Kör testte "AI" şikâyeti ≤%10 kapısı |
| 4 | **AI tepkisi veya ifşa krizi** (E33 ve Postal örnekleri) | O / Y | Önceden, somut ve tutarlı beyan (Steam + basın kiti + SSS). Beyanı "AI'sız" şartı olan ödül ve fonlara başvurmamak. Kanıt için manifest |
| 5 | **Kodun anlaşılmaz hâle gelmesi** (ajan kod borcu) | O / Y | Katı tipli GDScript, CI testleri, PR bazında Claude + insan incelemesi, mimari belgeleri. "Anlamadığın kodu birleştirme" kuralı [35] |
| 6 | **Pazarlama başarısızlığı / düşük istek listesi** | Y / Y | Sayfa G2'de açılır. Haftalık kısa video ritmi. Festivaller. G3/G4 kapılarında yeniden konumlandırma. Harcama kapıları (§4.4) |
| 7 | **Görünürlük yapısının değişmesi** (Popular Upcoming 100 bin, Next Fest kalabalığı) | Y / O | Personal Calendar, yayıncılar ve tür küratörlerine odaklanmak. Next Fest'i doğru zamanlamak [21][25] |
| 8 | **Rakip çıkışları** (Solo Leveling: KARMA, Echoes of Aincrad, büyük anime ARPG'ler) | O / O | Farklılaştırıcılar: varış anı, karakter olarak Sistem, tepki veren dünya. Tarih seçiminde büyük çıkışlardan ve indirim festivallerinden kaçınmak [R 02][25] |
| 9 | **Hukuki IP ihlali iddiası** (Solo Leveling ve DanMachi benzerliği) | D / Y | Trope/ifade kontrol listesi (01). İsim ve marka araştırması. Özgün terimler ve UI dili |
| 10 | **Korunamayan varlıklar** (saf AI çıktısı kopyalanır) | O / O | Kilit varlıklarda insan yazarlığı, manifest, marka tescili |
| 11 | **Yerelleştirme kalitesi** (JA/ZH makine çevirisi eleştirisi) | O / Y | Terim sözlüğü, insan LQA, pseudolocalization (08). Topluluk geri bildirim kanalı |
| 12 | **Seslendirme maliyeti ve etik sorunlar** | O / O | Sistem sesi kurgu gereği sentetik. Ana kadro insan. Sözleşmede AI maddesi. Önce AI ile geçici ses (scratch VO) (07) |
| 13 | **Tükenmişlik ve "otobüs faktörü"** (tek kişi) | Y / Y | Haftalık sürdürülebilir tempo. Her faz sonunda 1 hafta tampon. Yedekleme ve depo disiplini. Yazılı yol haritası |
| 14 | **Finansal pist ve kur riski** (gelir USD, gider TRY) | O / Y | Asgari bütçeyle ilerleme, harcama kapıları, TÜBİTAK/KOSGEB başvuruları (04), EA geliri. Konsol ve Asya için yayıncı |
| 15 | **Platform ve regülasyon değişiklikleri** (Steam içerik kuralları, yaş derecesi, TR erişim engelleri, AB md. 50) | O / O | Gacha ve kumarhane yok (04). Ölçülü fan servisi. Canlı AI yok. Belgeleri üç ayda bir yeniden okuma |

---

## Oyunumuz İçin Çıkarımlar

1. **Takvim kararı:**
   - Temel senaryo: dikey kesit Nisan 2027, Steam sayfası Nisan–Mayıs 2027, demo Kasım–Aralık 2027, **Next Fest Şubat 2028**, **EA Mart–Nisan 2028**, 1.0 2029'un ilk yarısı.
   - Ekim 2026 ve Şubat 2027 fest'leri gerçekçi değil.
   - Haziran 2027 fest'i ana oyunla kullanılmamalı; onun yerine Steam Playtest.
2. **İlk 5 hafta (F0) somut iş listesi:**
   - Rendering spike
   - Sanat bible'ı
   - 20 aday isimle marka ön araştırması
   - Şahıs şirketi ve vergi mülakatı hazırlığı
   - AI manifest şablonu
   - ADR'ler: "gacha yok", "canlı AI yok (EA)", "co-op yok (EA)"
3. **Ölçülebilir kapılar:** Bu belgedeki G0–G7 eşikleri proje panosuna (ör. GitHub Projects) ve `docs/` altına **karar kaydı** olarak yazılmalı. Her kapıda "devam / kes / ertele" kararı tarihli olarak kaydedilmeli.
4. **Bütçe:** Temel sütun (~52 bin $) hedeflenmeli, ama harcama **istek listesine bağlı** açılmalı. G2'ye kadar asgari sütun. Tek istisna insan eliyle capsule ve logo.
5. **Pazarlama motoru:** Haftada 2–3 kısa klip, aylık devlog, Discord. Sayfa açılınca hedef ilk 3 ayda 3–5 bin, fest öncesinde 7–10 bin, EA'da ≥20 bin istek listesi.
6. **Mağaza varlıkları:** İlk fragman oynanış, ilk 5 saniye kanca. Capsule ve logo insan eseri. Kısa açıklama EN/JA/ZH. Etiketler: Action RPG, Anime, Roguelite, Dungeon Crawler, Singleplayer, Fantasy. **Oyun içinde karşılığı olmayan etiket kullanılmamalı.**
7. **Yerelleştirme:** EA'da EN+JA+ZH-Hans metin (insan LQA ile). TR arayüz ve altyazı mümkünse EA'da (yerel PR kaldıracı, maliyeti düşük). KO/PT-BR/ES 1.0'da.
8. **AI şeffaflık metni:** Steam formu + basın kiti + web SSS'de aynı cümleler. İçinde "Claude Code ile kodlandı; oyuncunun gördüğü X ve Y'de AI kullanıldı, şunlar insan eseri" beyanı olmalı. Fragman, mağaza görselleri ve diğer pazarlama materyallerinde AI kullanıldıysa bu da beyana eklenmeli (düzeltildi 24.09.2026).
9. **Hukuki şablonlar (F0–F2):** Serbest çalışan sözleşmesi (FSEK 52 uyumlu, AI maddeli), besteci sözleşmesi (OST dahil), seslendirme sözleşmesi (klon yasağı), gizlilik politikası ve aydınlatma metni, yayın izni metni (EN/JA). Bir avukata **tek seferlik paket** olarak inceletilmeli.
10. **Marka:** Sayfa açılmadan TÜRKPATENT'e sınıf 9 ve 41 başvurusu (~12.650 TL). EA'dan önce EUIPO (~900 €) ve USPTO (~700 $).
11. **Yayıncılar:** Mağaza sayfasında ve sitede EN/JA yayın ve para kazanma serbestliği metni olmalı. OST Content ID'ye kaydedilmemeli. Demo çıkışında 200–500 kişilik türe yakın yayıncı listesine anahtar ve rehber gönderilmeli.
12. **Plan B (isteğe bağlı):** Pazarlama becerisini ve kitleyi erken test etmek için aynı evrende 2–3 aylık küçük bir 2D "Sistem" mini oyunu çıkarılabilir (ayrı oyun, ayrı Next Fest hakkı). Dikkat: Valve prolog, "Bölüm 1" ve başka bir oyunun kısa önizlemelerini Next Fest'e kabul etmiyor; mini oyun ana oyunun önizlemesi değil, kendi başına bir oyun olarak konumlanmalı (düzeltildi 24.09.2026). Ana projeyi geciktirme riski yüzünden **yalnızca G3 başarısız olursa** değerlendirilmeli.

## Belirsizlikler ve Riskler

- **Doğrulama açığı:**
  - Steamworks belgeleri bu oturumda GitHub aynasından birincil metin olarak okundu [C].
  - Zukowski, GameDiscoverCo, AB AI Act takvimi, Thaler kararı, TÜRKPATENT ve USPTO ücretleri, KVKK ayrıntıları ise **GitHub'daki üçüncü taraf özetlerden** [G] alındı. Orijinal sayfalar açılamadı.
  - Doğrulayıcı öncelik sırası:
    1. Popular Upcoming ~100 bin iddiası
    2. Next Fest kıyasları
    3. Digital Omnibus tarihleri
    4. TÜRKPATENT 2026 tarifesi
    5. Thaler temyiz reddi
    6. Genç girişimci ve yazılım ihracatı 2026 değişiklikleri
- **Doğrulanamayanlar [D]:**
  - Yerelleştirme kelime ücretleri, sanat ve 3D dış kaynak ücretleri, seslendirme ücretleri
  - Reddit alt forumlarının büyüklükleri
  - Türk anime etkinliklerinin güncel tarihleri
  - BitSummit ve INDIE Live Expo 2027 tarihleri
  - Palworld, R.E.P.O. ve Blue Prince ekip boyutları
  - Blue Prince'in geliştirme süresi
  - Bütçe tablosu bu yüzden **planlama varsayımıdır**. Karar öncesinde her kalemde 3 teklif alınmalı.
- **Next Fest Ekim 2027 ve Şubat 2028 tarihleri ilan edilmedi.** Senaryolar geçmiş örüntüye dayanıyor.
- **Kıyasların tür uyumu:** Zukowski ve GameDiscoverCo verileri tüm türleri karıştırıyor. Co-op "friendslop" oyunları istatistiği şişiriyor [19][75]. Gamesight verisi yalnızca PvP FPS [29]. Tek oyunculu anime ARPG'de dönüşüm farklı olabilir.
- **Popular Upcoming ve kişiselleştirme:** Valve eşik açıklamıyor. Zukowski ve topluluk tahminleri farklı (~80–120 bin). Kurallar yeniden değişebilir.
- **AB AI Act:** Md. 50 kılavuzu ve uygulama kuralları kesinleşmedi. Oyunların "deepfake" tanımına ne ölçüde girdiği uygulamayla netleşecek. Türkiye'de AI'a özgü bir yasa bulunamadı (D).
- **Tahmin hatası:** Tek kişilik projede üretim hızı ölçülmeden (G2) EA tarihi yalnızca bir hipotez. %30–50 kayma olasılığı yüksek.
- **Üslup:** Bu rapor yol haritası ve iş planı önerileri içeriyor. Hukuk bölümleri avukat onayı olmadan uygulanmamalı.

## Kaynaklar

Etiketler: [C] bu oturumda okundu · [G] GitHub'daki üçüncü taraf özetten, orijinal açılamadı · [R] kardeş rapor · [B] model bilgisi, açılamadı. Steamworks sayfaları GitHub aynasında `https://github.com/SteamTracking/SteamworksDocumentation/blob/master/docs/<yol>.html` adresiyle okunabilir (son commit 2026-09-24).

1. [C] Steam Next Fest (genel): https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest
2. [C] Next Fest Ekim 2026: https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest/2026october
3. [C] Next Fest Şubat 2027: https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest/feb_2027
4. [C] Next Fest Haziran 2027: https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest/june_2027
5. [C] Upcoming Steam Events (indirim ve fest takvimi): https://partner.steamgames.com/doc/marketing/upcoming_events ; temalı fest kuralları: https://partner.steamgames.com/doc/marketing/upcoming_events/themed_sales
6. (kullanılmadı)
7. [C] Content Survey (AI beyanı dahil): https://partner.steamgames.com/doc/gettingstarted/contentsurvey
8. [C] Almanya'da zorunlu yaş derecesi: https://partner.steamgames.com/doc/gettingstarted/contentsurvey/germany ; 8b. Endonezya: https://partner.steamgames.com/doc/gettingstarted/contentsurvey/indonesia
9. [C] Steam Direct ücreti: https://partner.steamgames.com/doc/gettingstarted/appfee
10. [C] Onboarding (30 gün bekleme, içerik kuralları): https://partner.steamgames.com/doc/gettingstarted/onboarding
11. [C] Coming Soon: https://partner.steamgames.com/doc/store/coming_soon
12. [C] Review Process: https://partner.steamgames.com/doc/store/review_process
13. [C] Wishlists: https://partner.steamgames.com/doc/marketing/wishlist
14. [C] Visibility on Steam: https://partner.steamgames.com/doc/marketing/visibility
15. [C] Early Access: https://partner.steamgames.com/doc/store/earlyaccess
16. [C] Trailers: https://partner.steamgames.com/doc/store/trailer
17. [C] Localization: https://partner.steamgames.com/doc/store/localization
18. [C] Steam Playtest: https://partner.steamgames.com/doc/features/playtest
19. [G] Zukowski, "Making sense of the February 2026 Steam Next Fest" (13 Nisan 2026): https://howtomarketagame.com/2026/04/13/making-sense-of-the-february-2026-steam-next-fest/ (özet: https://github.com/ginzadaddy-png/my-wiki/blob/main/wiki/sources/zukowski-next-fest-strategy.md)
20. [G] Zukowski, "Benchmarks: How many wishlists can I get from Steam Next Fest" (Mart 2025): https://howtomarketagame.com/2025/03/26/benchmarks-how-many-wishlists-can-i-get-from-steam-next-fest/ (özet: https://github.com/ginzadaddy-png/my-wiki/blob/main/wiki/concepts/launch-metrics.md)
21. [G] Zukowski, "How the Steam Personal Calendar affects your launch" (25 Haziran 2026): https://howtomarketagame.com/2026/06/25/how-the-steam-personal-calendar-affects-your-launch/
22. [G] Zukowski, "Nobody plays demos and that is OK" (30 Haziran 2026): https://howtomarketagame.com/2026/06/30/nobody-plays-demos-and-that-is-ok/
23. [G] Zukowski, "The state of virtual 3rd party festivals 2026" (11 Ağustos 2026): https://howtomarketagame.com/2026/08/11/the-state-of-virtual-3rd-party-festivals-2026/
24. [G] Zukowski, "Should you do Early Access?" (27 Temmuz 2023): https://howtomarketagame.com/2023/07/27/should-you-do-early-access/ (özet: https://github.com/eiaserinnys/seosoyoung-blog/blob/HEAD/content/digest/zukowski-should-you-do-early-access-2023.md)
25. [G] GameDiscoverCo, "Who 'won' June 2026's Steam Next Fest?" (23 Haziran 2026): https://newsletter.gamediscover.co/p/who-won-june-2026s-steam-next-fest
26. [G] GameDiscoverCo, "Does your Steam demo CCU predict...?" (8 Eylül 2026): https://newsletter.gamediscover.co/p/does-your-steam-demo-ccu-predict
27. [G] GameDiscoverCo, "What do Steam fans really think about AI?" (7 Temmuz 2026): https://newsletter.gamediscover.co/p/what-do-steam-fans-really-think-about
28. [G] GameDiscoverCo, "What 1 million (immediate!) wishlists for Dear Passengers says about discovery" (17 Temmuz 2026): https://newsletter.gamediscover.co/p/what-1-million-immediate-wishlists
29. [G] GamesIndustry.biz, Gamesight: yayıncı sayısı en iyi başarı göstergesi (30 Temmuz 2026): https://www.gamesindustry.biz/gamesight-creators-are-best-predictor-for-a-games-success-not-viewership
30. [G] GDC 2026 State of the Game Industry: https://gdconf.com/article/gdc-2026-state-of-the-game-industry-reveals-impact-of-layoffs-generative-ai-and-more/ (özet: https://github.com/lucasbrandao4770/claude-code-gamedev/blob/HEAD/notes/research/ai-gamedev-community-2026.md)
31. [G] Tom's Hardware, 2025 Steam çıkışlarının 1/5'i GenAI kullandı: https://www.tomshardware.com/video-games/pc-gaming/1-in-5-steam-games-released-in-2025-use-generative-ai-up-nearly-700-percent-year-on-year-7-818-titles-disclose-genai-asset-usage-7-percent-of-entire-steam-library
32. [G] GameRant, Postal: Bullet Paradise AI tepkisiyle iptal: https://gamerant.com/steam-ai-art-game-canceled-postal-bullet-paradise-explained/
33. [G] 404 Media, fly.pieter.com: https://www.404media.co/this-game-created-by-ai-vibe-coding-makes-50-000-a-month-yours-probably-wont/
34. [G] Seul SBA / Relu Games: https://indiegame.com/en/archives/22797
35. [G] "Building an RTS in Godot — What if Claude writes ALL code?": https://dev.to/datadeer/part-1-building-an-rts-in-godot-what-if-claude-writes-all-code-49f9
36. [G] TweakTown, Schedule I 459 bin zirve: https://www.tweaktown.com/news/104474/schedule-hits-459k-peak-players-the-most-by-solo-developer-in-steam-history/index.html
37. [G] Game Developer, Megabonk 2 haftada 1 milyon: https://www.gamedeveloper.com/business/indie-hit-megabonk-moves-over-a-million-copies-in-two-weeks
38. [G] Game Developer, PEAK <200 bin $ ile 2 milyon: https://www.gamedeveloper.com/production/how-co-op-climbing-hit-peak-achieved-2-million-sales-for-less-than-200-000- ; TweakTown 10 milyon: https://www.tweaktown.com/news/107179/peak-confirmed-to-have-sold-more-than-10-million-copies/index.html
39. [G] GamesRadar, Buckshot Roulette: https://www.gamesradar.com/games/horror/he-made-a-viral-horror-game-in-2-months-it-sold-6-million-copies-and-now-he-can-make-whatever-he-wants-for-the-rest-of-his-life-my-final-theory-is-that-gambling-is-very-fun/
40. [R] Balatro 5 milyon: https://www.gamedeveloper.com/business/balatro-sells-5-million-copies-after-end-of-year-spike
41. (kullanılmadı)
42. [R] Stardew Valley 41 milyon: https://www.gamingonlinux.com/2025/01/stardew-valley-hits-over-41-million-sales-with-millions-sold-during-2024/ ; ~4 yıl tek kişi: https://github.com/playhunterhq/playhunter.dev/blob/HEAD/scout/data/comparables.json [G]
43–47. [R] Hades II, Clair Obscur, MiSide, Palworld: bkz. `02-pazar-ve-rakip-analizi.md` kaynaklar 43, 44, 53, 54
48. [B] Hollow Knight Kickstarter: https://www.kickstarter.com/projects/11662585/hollow-knight
49. [B] Blue Prince (Raw Fury): https://rawfury.com/
50. (kullanılmadı)
51. [G] AB AI Act md. 50 metni (Tüzük 2024/1689): https://eur-lex.europa.eu/eli/reg/2024/1689/oj (metin kopyası: https://github.com/lawve-ai/awesome-legal-skills/blob/HEAD/skills/eu-ai-act-knowledge-base-oliver-schmidt-prietz/references/core/regulation-title-IV-transparency.md)
52. [G] Digital Omnibus on AI, Tüzük (AB) 2026/1744: http://data.europa.eu/eli/reg/2026/1744/oj (özet: https://github.com/AISDLC/curriculum/blob/HEAD/briefs/2026-08-02-eu-ai-act-application-status.md)
53. [G] Avrupa Komisyonu md. 50 SSS: https://digital-strategy.ec.europa.eu/en/faqs/transparency-obligations-under-article-50-ai-act
54. [G] Avrupa Komisyonu md. 50 kılavuzu: https://digital-strategy.ec.europa.eu/en/library/guidelines-transparency-obligations-providers-and-deployers-ai-systems
55. [G] Bratby Law, md. 50 yaptırımları: https://bratby.law/ai-act-transparency-obligations-2026/
56. [G] ABD Telif Ofisi, Copyright and AI Part 2 (29 Ocak 2025): https://www.copyright.gov/ai/Copyright-and-Artificial-Intelligence-Part-2-Copyrightability-Report.pdf
57. [G] Holland & Knight, Yüksek Mahkeme Thaler temyizini reddetti (Mart 2026): https://www.hklaw.com/en/insights/publications/2026/03/the-final-word-supreme-court-refuses-to-hear-case-on-ai-authorship ; IPWatchdog: https://ipwatchdog.com/2026/03/02/supreme-court-denies-thalers-latest-attempt-register-copyright-ai-generated-image/
58. [G] D.C. Circuit, Thaler v. Perlmutter (18 Mart 2025): https://media.cadc.uscourts.gov/opinions/docs/2025/03/23-5233.pdf
59. [R] ABD Telif Ofisi Circular 33: https://www.copyright.gov/circs/circ33.pdf
60. [G] TÜRKPATENT marka işlem ücretleri (yürürlük 1 Ocak 2026): https://www.turkpatent.gov.tr/marka-islem-ucretleri (anlık görüntü 2026-09-01: https://github.com/parkerhancock/patent-client-agents/blob/HEAD/coverage/fees-snapshot/TURKPATENT-trademark.json)
61. [G] TÜRKPATENT tescil süreci rehberi (Ağustos 2026): https://github.com/soylemezz33/markala/blob/HEAD/docs/TURKPATENT-MARKA-TESCIL-REHBERI.md
62. [G] USPTO ücretleri (sınıf başına 350 $, 18 Ocak 2025): https://www.uspto.gov/trademarks/fees-payment-information (özet: https://github.com/ericrisco/rsc-harness/blob/HEAD/skills/ip-trademark/SKILL.md)
63. [G/B] EUIPO ücretleri: https://www.euipo.europa.eu/en/trade-marks/before-applying/fees-payable-direct-filings
64. [G] KVKK yurt dışına aktarım rehberi: https://kvkk.gov.tr/Icerik/8142/Kisisel-Verilerin-Yurt-Disina-Aktarilmasi-Rehberi ; 6698 sayılı Kanun: https://www.mevzuat.gov.tr/mevzuat?MevzuatNo=6698&MevzuatTur=1&MevzuatTertip=5
65. [G] KVKK VERBİS istisna kriteri duyurusu: https://www.kvkk.gov.tr/Icerik/7646/Kamuoyu-Duyurusu-Veri-Sorumlulari-Siciline-Kayit-Yukumlulugune-Iliskin-Istisna-Kriterinde-Degisiklik-Yapilmasi-Hakkinda-
66. [B] GDPR (Tüzük 2016/679): https://eur-lex.europa.eu/eli/reg/2016/679/oj
67. [B] 5846 sayılı FSEK: https://www.mevzuat.gov.tr/mevzuat?MevzuatNo=5846&MevzuatTur=1&MevzuatTertip=3
68. [B] 17 U.S.C. §101 (work made for hire): https://www.law.cornell.edu/uscode/text/17/101
69. [G] Türkiye'den solo indie için 2026 vergi notları ve Vampire Survivors verisi: https://github.com/bekirmfr/Emberwatch/blob/HEAD/docs/compass-research.md
70. [G] Oyun endüstrisi etkinlik takvimi (TGS 2026/2027, デジゲー博, gamescom, INDIE Live Expo): https://github.com/norimichitakesue2/game-industry-tracker/blob/HEAD/md/14-events.md ; TGS 2026: https://events.nikkeibp.co.jp/tgs/2026/en/ ; TGS 2027: https://news.denfaminicogamer.jp/news/2609203w
71. [C] presskit.html: https://github.com/pixelnest/presskit.html
72. [R] Kardeş raporlar: `docs/research/01` … `08`
73. (kullanılmadı)
74. (kullanılmadı)
75. [G] GameDiscoverCo, "The state of Steam wishlist conversions" (17 Ekim 2025): https://newsletter.gamediscover.co/p/the-state-of-steam-wishlist-conversions (özet: https://github.com/ginzadaddy-png/my-wiki/blob/main/wiki/sources/carless-wishlist-conversions-2025-10.md)
76. [G] PCGuide, Popular Upcoming için 100 bin istek listesi eşiği: https://www.pcguide.com/news/steams-new-100000-wishlist-rule-means-many-indie-devs-will-have-to-rely-on-a-different-feature-to-be-discovered/

## Doğrulama Notları (24.09.2026)

Bağımsız doğrulama; Steamworks belgeleri `SteamTracking/SteamworksDocumentation` GitHub aynasından (raw.githubusercontent.com) yeniden indirilip okundu, diğerleri WebSearch ile farklı sorgu ve kaynaklardan kontrol edildi. howtomarketagame.com, pcgamer.com, gamedeveloper.com, eur-lex ve turkpatent.gov.tr bu oturumda doğrudan açılamadı; bunlar için arama sonuçları ve ikincil hukuk/sektör özetleri kullanıldı.

| İddia | Sonuç | Düzeltme/Not | Kaynak |
|---|---|---|---|
| Next Fest Şubat 2027: 22 Şubat–1 Mart 2027; kayıt 10 Ocak; basın önizlemesi demosu 25 Ocak; zorunlu öğeler 8 Şubat; basın önizlemesi 11 Şubat | Doğrulandı | — | https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest/feb_2027 |
| Next Fest Haziran 2027: 14–21 Haziran 2027; kayıt 25 Nisan; zorunlu öğeler 31 Mayıs | Doğrulandı | Basın önizlemesi 3 Haziran. Sayfa, bir sonraki edisyonun Ekim 2027'de planlandığını yazıyor | https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest/june_2027 |
| Next Fest Ekim 2026: 19–26 Ekim; kayıt 31 Ağustos 2026'da kapandı | Doğrulandı | — | https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest/2026october |
| Bir oyun yalnızca bir Next Fest'e katılabilir; yılda 3 kez (Şubat/Haziran/Ekim) | Doğrulandı + ek | Prolog, "Bölüm 1" ve kısa önizlemeler kabul edilmez; EA çıkışı "çıkış" sayılır. Plan B mini oyun bağımsız oyun olmalı | https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest |
| Steam Direct 100 $, 1.000 $ AGR'de mahsup, iade yok; 30 gün bekleme | Doğrulandı | — | https://partner.steamgames.com/doc/gettingstarted/appfee ; https://partner.steamgames.com/doc/gettingstarted/onboarding |
| Coming Soon ≥2 hafta; inceleme 3–5 iş günü, ≥7 iş günü önce gönder | Doğrulandı | — | https://partner.steamgames.com/doc/store/coming_soon ; https://partner.steamgames.com/doc/store/review_process |
| İstek listesi e-postası ≥%20 ve >8 saat indirimde; demo bildirimi bir kez | Doğrulandı | — | https://partner.steamgames.com/doc/marketing/wishlist |
| Görünürlük: istek listesi "çoğunlukla" etken değil; trafik/dönüşüm etken değil; inceleme ≥%40 iken etken değil | Doğrulandı | — | https://partner.steamgames.com/doc/marketing/visibility |
| EA: fiyat artışından sonra 30 gün indirim yok | Doğrulandı + ek | Kural 1.0 çıkış indirimini de kapsıyor; istisnası yok | https://partner.steamgames.com/doc/marketing/discounts ; https://partner.steamgames.com/doc/store/pricing |
| Steam indirim takvimi (Sonbahar 1–8 Ekim 2026, Kış 17 Aralık–4 Ocak, İlkbahar 18–25 Mart 2027, Yaz 24 Haziran–8 Temmuz 2027) | Doğrulandı | — | https://partner.steamgames.com/doc/marketing/upcoming_events |
| Steam kullanıcılarının %60'tan fazlası İngilizce dışı dil kullanıyor | Doğrulandı | — | https://partner.steamgames.com/doc/store/localization |
| Steam AI beyanı: oyunla gelen ve oyuncunun tükettiği içerik; verimlilik araçları odak değil; Önceden Üretilmiş / Canlı Üretilen; canlı AI ile Adult Only cinsel içerik yok | Doğrulandı + ek | 16 Ocak 2026 güncellemesini aktaran haberlere göre mağaza sayfası, topluluk varlıkları ve pazarlama materyalleri de kapsamda; pazarlamadaki AI da beyan edilmeli | https://partner.steamgames.com/doc/gettingstarted/contentsurvey ; https://games.slashdot.org/story/26/01/19/1735231/valve-has-significantly-rewritten-steams-rules-for-how-developers-must-disclose-ai-use |
| Popular Upcoming eşiği Haziran 2026'da ~7 binden ~100 bine çıktı (Zukowski) | Doğrulandı (tahmin) | Resmî değil; başka kaynaklar ~80 bin–120 bin diyor | https://howtomarketagame.com/2026/06/25/how-the-steam-personal-calendar-affects-your-launch/ ; https://www.pcguide.com/news/steams-new-100000-wishlist-rule-means-many-indie-devs-will-have-to-rely-on-a-different-feature-to-be-discovered/ |
| Next Fest kademeleri (Şubat 2026): zayıf ≤1 bin, orta 2–3 bin, üst %5 ~15 bin | **Düzeltildi** | Medyan ~800; üst %5 medyanın 16 katından fazla (~13 bin+) | https://howtomarketagame.com/2026/04/13/making-sense-of-the-february-2026-steam-next-fest/ |
| Fest öncesi istek listesi en güçlü gösterge (r≈0,825) | Doğrulandı, kaynak düzeltildi | Değer Şubat 2026 verisinden [19]; kademe medyanları (322/1.006/5.215) doğrulanamadı | https://howtomarketagame.com/2026/04/13/making-sense-of-the-february-2026-steam-next-fest/ |
| Demo oyuncusu → istek listesi medyanı %19,3 | Doğrulandı (yaklaşık) | "Medyan oyunda her 5 demo oyuncusundan ~1'i" | https://howtomarketagame.com/2026/06/30/nobody-plays-demos-and-that-is-ok/ |
| İstek listesi → ilk hafta satış: 25 bin+ istek listeli oyunlarda 0,15×, 10 $ üstünde 0,10×; 10–20 kat fark | Doğrulandı | Örneklem: Eylül 2024–Eylül 2025 çıkışları | https://newsletter.gamediscover.co/p/the-state-of-steam-wishlist-conversions |
| Haziran 2026 Next Fest: 4.382 demo (+%66), %26,5 AI beyanı, Godot %9,2 → %12,6 | Doğrulandı | Tüm etkinlikte (~8.700 giriş) AI beyan oranı ~%20 | https://newsletter.gamediscover.co/p/who-won-june-2026s-steam-next-fest |
| GameDiscoverCo AI anketi: %43 kayıtsız, %31 olumsuz, %8 reddediyor | **Düzeltildi** (ifade) | %43 "sorun görmüyor", ~%26 nötr, %31 olumsuz, %8,1 hiçbir koşulda oynamaz | https://newsletter.gamediscover.co/p/what-do-steam-fans-really-think-about ; https://www.gamesradar.com/games/survey-finds-only-31-percent-of-steam-users-have-a-problem-with-ai-in-games-with-43-percent-totally-fine-with-it/ |
| AB AI Act md. 50, 2 Ağustos 2026'dan beri uygulanıyor; Digital Omnibus (2026/1744) 24 Temmuz'da yayımlandı, 27 Temmuz 2026'da yürürlüğe girdi; Ek III → 2 Aralık 2027, Ek I → 2 Ağustos 2028; md. 50(2) için eski sistemlere 2 Aralık 2026 | Doğrulandı | md. 50(2) geçiş süresi yalnızca 2 Ağustos 2026'dan önce piyasaya sürülen sistemler için | https://www.hunton.com/privacy-and-cybersecurity-law-blog/eu-digital-omnibus-on-ai-enters-into-force ; https://www.whitecase.com/insight-alert/eu-ai-omnibus-enters-force-amending-ai-act |
| ABD Telif Ofisi Part 2 (29 Ocak 2025): yalnızca prompt yazarlık için yetmez | Doğrulandı | — | https://www.copyright.gov/ai/Copyright-and-Artificial-Intelligence-Part-2-Copyrightability-Report.pdf ; https://ipwatchdog.com/2025/01/29/part-two-copyright-office-ai-report-says-creative-prompting-doesnt-constitute-authorship/ |
| Yüksek Mahkeme 2 Mart 2026'da Thaler v. Perlmutter (No. 25-449) temyiz başvurusunu reddetti | Doğrulandı | D.C. Circuit'in insan yazarlık kararı yürürlükte kaldı | https://www.scotusblog.com/cases/thaler-v-perlmutter/ ; https://www.mayerbrown.com/en/insights/publications/2026/03/supreme-court-denies-review-in-ai-authorship-case |
| TÜRKPATENT 2026: başvuru 2.820 TL, 2. sınıf +2.820 TL, 3.+ sınıf +3.150 TL, tescil 7.010 TL (9+41 ≈ 12.650 TL) | Doğrulandı | Resmî ücretler; vekil ücreti ve KDV hariç | https://www.turkpatent.gov.tr/marka-islem-ucretleri |
| EUIPO: 850 € (1 sınıf) + 50 € (2.) + 150 € (3.+) | Doğrulandı | — | https://www.euipo.europa.eu/en/trade-marks/before-applying/fees-payable-direct-to-the-euipo |
| USPTO: sınıf başına 350 $ (18 Ocak 2025'ten beri) | Doğrulandı | ID Manual dışı serbest tanım için sınıf başına +200 $, eksik bilgi için +100 $ | https://www.uspto.gov/trademarks/fees-payment-information |
| Megabonk 2 haftada 1 milyon+; Schedule I 459 bin zirve CCU (tek geliştirici rekoru) | Doğrulandı | Schedule I zirvesi 459.075 (6 Nisan 2025) | https://www.gamedeveloper.com/business/indie-hit-megabonk-moves-over-a-million-copies-in-two-weeks ; https://steamdb.info/app/3164500/charts/ |
| 2026 vergi: genç girişimci 400 bin TL; Bağ-Kur desteği kaldırıldı (7566); yazılım ihracatı indirimi %100 | Doğrulandı | %100 oran 11257 sayılı CK ile (Nisan 2026) 1 Ocak 2026'dan itibaren; Steam gelirine uygulanabilirliği mali müşavirle teyit edilmeli | https://www.alomaliye.com/2026/04/20/yurt-disi-mukimlere-verilen-hizmetlerde-kazanc-indirimi/ ; https://vergiselboyut.com/2026-genc-girisimci-vergi-tesviki/ |
| PEGI (rapor §6.6'da yoktu) | **Eklendi** | Haziran 2026'dan itibaren ücretli rastgele öğe → PEGI 16+, süreli teklif → PEGI 12+, sınırsız iletişim → PEGI 18 | https://pegi.info/news/pegi-expands-age-rating-criteria-interactive-risk-categories |

**Karar etkisi:** Takvim (Next Fest Şubat 2028, EA sonrası), bütçe ve marka önerileri geçerliliğini koruyor. Değişen uygulama noktaları: (1) AI beyanı pazarlama materyallerini de kapsamalı; (2) EA→1.0 fiyat artışı 1.0'dan en az 30 gün önce yapılmalı; (3) Plan B mini oyun ana oyunun prologu/önizlemesi gibi konumlanırsa Next Fest'e giremez; (4) Next Fest'te "medyan" beklenti ~800 istek listesi, bu yüzden G4/G5 kapıları iddialı hedef olarak okunmalı.
