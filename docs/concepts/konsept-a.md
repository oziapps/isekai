# Konsept A — TAMGA: Adsızın Kaydı ("Sistem ve Kapılar")

> 2026-09-24 · Açı: **SİSTEM ve KAPILAR** (Solo Leveling ağırlıklı; DanMachi, Slime, Re:Zero ve Hades'ten ödünçlerle). Dayanak `docs/research/01–10`; [R03] ilgili raporu gösterir. Sayılar **tasarım hedefidir**, olgu değildir.

---

## 1. Künye

| Alan | Değer |
|---|---|
| **Çalışma adı** | **TAMGA: Adsızın Kaydı** · EN *TAMGA: Record of the Nameless* · JA 『タムガ ―名無しの記録―』 · ZH 《塔姆加：无名者之录》. Yedekler: *ADSIZ*, *Ninegate*. F0'da sınıf 9/41 marka taraması [R10] |
| **Tür** | Üçüncü şahıs anime aksiyon-RPG: hub şehir, instanced "Kapı" koşuları (roguelite-lite), Adlı toplama, şehir savunması |
| **Platform** | PC (Steam), Steam Deck Verified hedefi. Konsol 1.0+12–24 ay (W4 ya da port ortağı) [R08] |
| **Motor** | Godot 4.7.2, katı tipli GDScript; ilk 3 hafta "Anime Rendering Spike" kapısı, başarısızsa Unity 6.3 LTS [R08] |
| **Kamera** | Omuz üstü serbest üçüncü şahıs, yumuşak kilitlenme, ultimate ve bağ tekniklerinde cut-in kameraları; şehirde serbest keşif |
| **Hedef kitle** | A) 16–34 "Hunter" çekirdeği (Solo Leveling, manhwa, ARPG). B) 30+ "ikinci şans" yetişkinleri. C) Bağ ve hikâye odaklılar [R01]. PEGI 12/16, ESRB T |
| **Fiyat** | EA 19,99 $, 1.0 24,99 $ (artış 1.0'dan ≥30 gün önce) [R04]. Gacha, enerji, premium para, güç satışı yok |
| **Oturum** | 30–45 dk'lık "oyun günü": sabah şehir, 1–2 Kapı, Derleme, akşam sahnesi. Tek Kapı 10–25 dk, bölüm 5–8 saat |
| **EA dilleri** | Metin EN, JA, ZH-Hans, TR. Ses: EN insan kadro; Sistem sesi EN/JA/TR tasarlanmış, beyanlı AI sesi |
| **Takvim** | Next Fest Şubat 2028 → EA Mart–Nisan 2028 → 1.0 2029 1. yarı [R10] |

---

## 2. Logline ve "Neden Şimdi / Neden Biz"

**Logline:** *İstanbul'da son metroda açılan bir Kapı seni, tamgası olmayan herkesin "F" sayıldığı kervan şehri Dokuzkapı'ya fırlatır. Ölürken adını yazdığın anda, yalnızca senin duyduğun ve kendi hesabı olan bir Sistem uyanır. Yendiğin canavarlara ad verip onları ordun yap, Kapılar şehri yutmadan en zayıftan en güçlüye tırman ve sonunda Sistem'in senden istediği tek şeye karar ver: kendi adına.*

**Pazar boşluğu:**
- **Talep canlı, takvim bizden yana.** Solo Leveling Crunchyroll'un en çok izlenen animesi; S3 2027–28'e, film 2027'ye planlı [R01]. Next Fest ve EA bu dalgaya denk geliyor.
- **Lisanslı isekai oyunları çöktü.** DanMachi, KonoSuba, Re:Zero, SAO VS kapandı; premium lisanslılar Steam'de %52–71 olumlu. Ortak nedenler: oyuncu kendini oynamıyor, oynanış zayıf, monetizasyon agresif [R02].
- **Gacha yorgunluğu ölçülebilir.** Netmarble bile Overdrive'ı gacha'sız 39,99 $'a çıkardı (ilk hafta ~127 bin, Metacritic 64, "tekrar ve grind" şikâyeti); KARMA'yı roguelite yapıyor [R02]. "Bir kere al, isekai hayatını yaşa" tek başına farklılaştırıcı [R04].
- **Boşluk tablosu (R02 §6):** *Dünya'dan gelen oyuncunun kendisi*, *ana mekanik olarak Sistem*, *tepki veren dünya* ve *modern bilgi*yi birlikte kuran oyun yok. Bunlar sanattan çok sistem işi.

**Resmî Solo Leveling oyunlarından farkımız:** Jinwoo'yu değil kendini oynarsın. Sistem arayüz süsü değil, sesi ve gizli gündemi olan bir karakter. Düşmanlar "gölge çıkarma" ile değil **senin yazdığın adlarla** bağlanır. Kapılar gerçekten şehrine taşar. Dünya'daki mesleğin mekanik sonuç doğurur.

**Neden biz:** Oyunun kalbi (Sistem diyaloğu, Adlandırma, şehir tepkiselliği, Kapı üretimi) metin ve veri ağırlıklı; Claude Code'un headless Godot döngüsünde en verimli olduğu alan [R08]. Sanatı ağır kısımlar bilinçli olarak dar: tek hub, instanced Kapılar, az kahraman, CC0 animasyon temeli [R06]. Tam Türkçe yerel PR kaldıracı [R01].

---

## 3. Dünya ve Hikâye Tohumu

### 3.1 Dünya: Dokuzkapı ve Taşyol

- **Dokuzkapı**, Taşyol bozkırında dokuz kervan yolunun buluştuğu surlu ticaret şehri. 300 yıl önceki **Büyük Kırılma**'dan beri çevresinde **Kapılar** açılıyor.
- **Kapıların içi:** Her Kapı ölmüş bir dünyanın parçası. Canavarlar, adını yitirmiş sakinlerin **Yankı**ları. Kanamazlar, **mürekkep saçarlar** (stil, yaş derecesi ve ZH içerik hassasiyeti için).
- **Ekonomi:** Kapı Özü kristalleri şehri döndürür (DanMachi'nin büyü taşı döngüsü). Kapılar hem tehdit hem geçim.
- **Tamga ve rütbe:** Yerliler elinde doğuştan bir **tamga** (mühür izi) taşır; Eşikçiler Loncası rütbeyi (F→S) bundan ölçer. Dünya'dan gelen **Adsızlar** tamgasızdır, ölçülemez ve otomatik **F** sayılır.
- **Görsel kimlik:** Terrakota kerpiç, lapis çini, keçe-kilim, pirinç fenerler; jenerik Avrupa yerine İpek Yolu yüksek fantezisi [R01]. Kutsal figür kullanılmaz, tamgalar özgün tasarımdır, kültür danışmanı görüşü alınır [R09].

### 3.2 Varış (isekai anı)

İstanbul, gece yarısı, son metro. Karakter yaratma menüyle değil eşyalarla yapılır: çantadaki iş kartı, vagon camındaki yansıma. Peronda küçük bir Kapı yırtılır, mürekkep kürklü bir **Kapı Tazısı** çıkar. İlk dövüş mesleğe göre doğaçlama bir silahla yapılır (tava, yangın tüpü, kask). Telefona bildirim düşer: *"Sisteme kabul edildiniz. [Kabul] [Kabul]"*. Tazı seni içeri çeker. Kamyon klişesi yok [R01][R09].

### 3.3 Ana çatışma: Sistem'in gizli hesabı

- **Tanıtım:** Sistem kendini "SİSTEM" diye tanıtır: *"Bu kelimeyi senin zihninden aldım, tanıdık gelsin diye."* Oyunsu arayüzün kurgusal gerekçesi ve ilk manipülasyon ipucu budur.
- **Gerçek kimlik:** Adı **Kâtip**; yıkılmış bir kader bürokrasisinin, **Yazgı Divanı**'nın kayıt memuru. Divan her varlığa ad ve rütbe yazardı, tamgalar onun mirası. Divan çökünce kayıt çürüdü; Kapılar bu kayıttan düşen sayfalar.
- **Amaç:** Divan'ı yeniden kurmak. Bunun için binlerce yeni **Ad** ve kayıtta olmayan bir yazar (bir Adsız) gerekiyor. En son o yazara **kendi adını** yazdıracak.
- **Yöntem:** Faydacı. Kapıları bitirmek uğruna bazı mahallelerin taşmasına göz yumar, sayaçları hızlandırır.
- **Oyunun sorusu:** Kâtip yardımcın mı, yöneticin mi, yoksa senin yazacağın bir kişi mi? Cevabı iki görünür ölçü taşır: **Sistem Yakınlığı** (akşam Kâtip sohbetleri, Kalibrasyon, kabul edilen Kızıl Teklifler) ve **Şehir Güveni** (taşma savunması, icatlar, reddedilen Kızıl Teklifler).

### 3.4 Üç perdelik ana hat

| Perde | Rütbe | Özet | Kapanış |
|---|---|---|---|
| **1 "Kayıt"** (EA çıkışı) | F→C | Uyanış, Tazı'ya ad, F damgası, ilk taşmalar. Silinmişler Tarikatı yapay taşmalar tetikler; D→C sınavında arenada Mühürlü Kapı açılır | Boss **Mühürbozan**. Arıza: *"Önceki kayıt: Adsız #0417 — SİLİNDİ."* |
| **2 "Kırılma"** (EA güncellemeleri) | C→A | Osaka'lı Adsız Mei ve "eski sürüm" Sistemi; Muhafızlar alt mahalleleri feda etmek ister; Kâtip'in adı ve itirafı; Divan harabelerinde Kızıl Kapı | #0417: 1999'dan gelmiş, Kâtip'e ad vermeyi reddettiği için "silinmiş" **Hakan Erdem**. Yenip **adını geri verebilirsin**; Adlı olarak katılır |
| **3 "İmza"** (1.0) | A→S | Şehrin üstünde Dünya'ya açılan **Onuncu Kapı**; Kâtip adını ister | **Adlandır:** Kâtip tanrı olur, Kapılar biter, rütbeler sonsuza dek sabitlenir. **Sil:** Sistem'i kırarsın, güçlerini kaybedersin, şehir özgür. **Küçük Ad:** ona insan adı verirsin, sınırlı ve ölümlü bir yoldaşa dönüşür (yüksek *Sistem Yakınlığı* ve *Şehir Güveni* ister). Sonra: dön ya da kal |

"Sil" yolunun son boss'u arayüzün kendisi: pencereler mermiye dönüşür, HUD sahte ölüm ekranı gösterir.

### 3.5 Ana yoldaşlar

| Karakter | Profil | Oyun etkisi |
|---|---|---|
| **Tazı** (adını sen koyarsın) | Seni Dünya'dan çeken Kapı Tazısı, ilk Adlın. Mürekkep kürk, fener gözler; yalnızca hayvan sesi çıkarır, verdiğin ad seslendirmeyle çakışmaz | Öncü (tank/avcı); 1.0'da binek evrimi |
| **Yaren** (24), Yükçü | F rütbeli hamal; dili ve adetleri öğretir. Sırrı: bir Kapı'da donup kalmış, ekibi ölmüş | Destek (fener, kanca, tuzak). Bağ: Kapı başına bir "Kurtarış", taşıma kapasitesi, *Fener Zinciri* tekniği |
| **Ilgın Serdar** (31), Lonca Ölçeri | Seni F diye kaydeden memur; tamganı okuyamadığı için sana takılı. Kardeşi bir Mühürlü Kapı'da kayıp | Gizli modifier istihbaratı, sınav avantajı; Perde 1 sonunda zayıf nokta açan büyücü olarak sahada |
| **Doğan Usta** (60), tamga ustası | Sakat, eski A rütbeli; #0417'yi tanımış | Deterministik oyma, Adlı evrimleri; mentor |
| **Mei Arakawa** (28), Osaka'lı Adsız | Üç yıl önce gelmiş eski e-spor oyuncusu, A rütbeli ünlü; "eski sürüm" Sistemi onu araç gibi kullanıyor | Rakipten müttefike, parry odaklı bağ; JA pazarı kancası (Perde 2) |
| **Tolga Varan** (36), Sur kaptanı | F'lileri küçümseyen, "alt mahalleleri feda edelim" diyen pragmatist | Şehir Güveni'ne göre kalkanlı müttefik ya da rakip (1.0) |

Tüm yoldaşlar açıkça yetişkin. EA'da romans yok; 1.0'da iki yetişkinle isteğe bağlı, rızası açık rotalar. "Sevgi" satılmaz [R09].

### 3.6 Düşmanlar ve fraksiyonlar

| Fraksiyon | Rolü |
|---|---|
| **Yankılar** | Kapı sakinleri; biyom başına bir aile. Elit ve boss'lar Adlandırılabilir |
| **Silinmişler Tarikatı** | Kâtip'in kaydını yakmak isteyen, sahte tamgalı kültistler; yapay taşma tetikler. Lideri #0417 |
| **Sur Muhafızları** | Şehir savunması; taşma triyajında politik rakip |
| **Altın Kervan** | Kapı Özü tekeli peşindeki, hamalları sömüren tüccarlar; icatlarınla çatışır ya da ortak olur |
| **Eşikçiler Loncası** | Rütbe, sözleşme ve sınavların bürokratik hakemi |
| **Kâtip** | Dost da düşman da |

---

## 4. Tasarım Sütunları

| # | Sütun | Vaat | Tasarım testi |
|---|---|---|---|
| S1 | **Sistem Bir Karakterdir** | Arayüzün her satırı Kâtip'in sesidir. Kâtip soğuk bir memurdan kişiliği olan bir varlığa evrilir; arızaları gizemin ipuçlarıdır | Her yeni sistem, Kâtip'in bir repliği ya da görsel diliyle mi tanıtılıyor? |
| S2 | **Adın Güçtür** | Önce kendine, sonra yendiklerine ad verirsin. Yazdığın adlar dünyada kanonlaşır | Oyuncunun yazdığı bir ad dünyada görünür bir yerde yankılanıyor mu? |
| S3 | **En Zayıftan En Güçlüye, Herkesin Önünde** | Görünür ve hak edilmiş büyüme. Halka açık rütbe sınavları, aura anları, eski kâbusa dönüp onu ezmek | 30–45 dk sonunda bir sayı ya da rütbe değişti mi? |
| S4 | **Kapılar Beklemez** | Şehir yaşıyor ve tehdit altında. Triyaj, taşma, yeniden inşa var; ama gerçek zamanlı FOMO yok | Boşlanan bir Kapı'nın görünür ve telafi edilebilir bir sonucu var mı? |
| S5 | **Her Vuruş Bir Anime Karesi** | Hitstop, impact frame, cut-in, onomatope; hikâye bölüm formatında | 10 sn'lik bir klip sessiz izlendiğinde bile "anime" diye okunuyor mu? |
| S6 | **Dünya'dan Getirdiğin** | Eski meslek, anılar ve modern bilgi dövüşü de şehri de değiştirir | Eski hayat seçimi ölçülebilir bir fark yaratıyor mu? [R01 P1] |

---

## 5. Oyun Döngüleri ve Sistemler

### 5.1 Katmanlı döngü

| Katman | Süre | Oyuncu eylemi | Ödül ve kanca |
|---|---|---|---|
| **Saniye** | 0,3–5 sn | Kıl Payı kaçınma, Karşı Mühür (parry), kombo, yetenek, Adlı komutu | Hitstop, mürekkep sıçraması, onomatope, kalem cızırtısı ve mühür "tık"ı |
| **Dakika** | 1–5 dk | Oda temizle, **Sistem Teklifi** (3'lü güçlendirme) seç | Build çeşitliliği. **Kızıl Teklif:** büyük güç, karşılığında şehrin taşma sayacı hızlanır |
| **Oturum** | 30–45 dk | Şehir, Kapı panosu, koşu, Mühür Taşı'nda "çık ya da derine in", **Derleme töreni**, akşam bağ sahnesi, uyku | Seviye mühürlenir, malzeme gelir; uykuda gün ve sayaçlar ilerler. "Ertesi gün" doğal durma noktası |
| **Bölüm** | 5–8 saat | Hikâye arkı, yeni biyom, **halka açık rütbe sınavı** | Rütbe sinematiği, OP/ED, "Sonraki bölüm" önizlemesi |
| **Hafta** | 7 gün | İsteğe bağlı **Günlük Kalibrasyon** (5–10 dk), **Haftalık Anomali Kapısı** (sabit seed, liderlik tablosu) | En fazla 7 gün birikebilen bonus, kozmetik unvan; eski seed'ler arşivde |
| **Sezon** | 8–10 hafta | EA bölüm güncellemeleri (biyom, Adlı, hikâye) | Hedef hiç bırakmamak değil, her sezon geri gelmek [R03] |

### 5.2 Dövüş sistemi

Gamepad önceliklidir; klavye ve fare tam desteklenir. Oyun mantığı 60 Hz'de çalışır. Her aksiyon bir `ActionData` kaydıdır: startup, active ve recovery kareleri, iptal pencereleri, i-frame ve hitstop değerleri [R08].

| Girdi (pad / KB+M) | Eylem |
|---|---|
| □ / Sol tık | Hafif saldırı: 4–5 vuruşluk dizi, dallanan bitiriciler |
| △ / Sağ tık (basılı) | Ağır/şarjlı saldırı, havaya kaldırma, kısa hava kombosu |
| ○ / Shift | Kaçınma; tam zamanlanırsa **Kıl Payı** (0,4 sn ağır çekim ve karşı saldırı penceresi) |
| L1 / Q | **Karşı Mühür** (parry, ~150 ms, zorluğa bağlı): impact frame ve büyük Denge hasarı |
| R1 + yüz tuşu / 1–4 | 4 aktif yetenek (bekleme süresi ve "Öz") |
| L2 / Alt (basılı) | **Adlı komut çarkı**: odaklan, savun, geri çekil, bekle; kısa basış Öncü Saldırısı |
| R2 / R | **Tamga** (ultimate), cut-in ile |
| L1+R1 / F | **Bağ Tekniği**: yoldaşla ortak cut-in saldırısı |
| D-pad / Tab | Sarf malzemesi; hızlı Sistem penceresi zamanı %20'ye yavaşlatır (tam duraklatma ayarı var) |

- **Denge ve Kırılma:** Denge çubuğu kırılan düşman sersemler ve **Mühür Vuruşu** açılır (10 kare hitstop, 3 kare impact frame). Mühür Vuruşu Adlandırma şansının ana etkenidir (5.4); ustalık doğrudan koleksiyona bağlanır (P9).
- **Anime dili:** Özel hareketler 2'lerle "limited animation", smear kareleri, hız çizgileri, yerelleştirilmiş onomatopeler ("GÜM!", 「ドン」, 「砰」). Vokal müzik yalnızca aura anlarında. Impact frame'lere "flaş azaltma" ayarı zorunlu [R09].
- **Nam:** Sınavlarda ve taşma savunmalarında kalabalık izler. Stilli oyun (Kıl Payı, Karşı Mühür, çeşitlilik) **Nam** göstergesini doldurur; NPC tepkisi ve ödül artar. "Aura anı"nın sistemleşmiş hâli.

### 5.3 İlerleme

- **Seviye ve Derleme:** Kapıda kazanılan deneyim "ham" kalır. Şehirde ya da güvenli kattaki Mühür Taşı'nda Kâtip onu **derler**: *"Derleme tamamlandı."* DanMachi'nin Status töreninin Sistem kılığı; hub'a dönüşü ödül sahnesi yapar [R03]. Atlanabilir.
- **Status:** **Kuvvet, Çeviklik, Sezi, Dayanım, Kut** (Kut: Adlı kapasitesi ve şans). Her seviyede serbest puan. Seviye tavanı EA'da 40, 1.0'da 80.
- **Rütbe:** Lonca rütbesi (F→S) yalnızca halka açık **Rütbe Sınavı** ile yükselir: Ölçüm odaları, düello, hikâye sürprizi. Doruğunda **Maske seçimi**: gücünü gösterirsen aura sahnesi ve fraksiyon dikkati, gizlersen "zayıf F'li" yan görevleri (Eminence tipi yanlış anlaşılma komedisi).
- **Yetenekler:** Her silah arketipinin 10 aktif yetenekli bir ağacı var; aktifler kullanıldıkça seviye atlar, 3. ve 6. seviyede iki mutasyondan biri seçilir. Ayrıca **Tamga Sanatları** (sınıf) ve **Kut Düğümleri** (pasif). **Gizli sınıflar** keşifle açılır, asla satılmaz (ör. *Kıl Payı Dansçısı*: B rütbesinde hasar almadan 100 Kıl Payı).
- **Ekipman:** Silah, üç zırh, iki tamga yüzüğü. Loot yalnızca oynayarak ve kötü şans korumasıyla gelir. Doğan Usta'da **deterministik oyma**: seçilen affix bilinen malzemeyle yazılır (Last Epoch tipi) [R03].
- **Üç eksenli güç:** kalıcı istatistik, build (Teklif ve ekipman) ve satılamayan **bilgi** (Kodeks, boss notları, gizli koşullar). **Hatıra Kapıları**'nda eski rütbenin kâbus boss'u isteğe bağlı döner; tek vuruşta yenmek büyümeyi hissettirir.

### 5.4 Adlılar ve parti sistemi

- **Yankı ve Tanınma:** Yenilen elit ya da boss'tan bir **Yankı** kalır. Tanınma şansı nasıl kazandığına bağlı (Denge kırıldı mı, Mühür Vuruşu'yla mı bitti, Kızıl Teklif kullanıldı mı). Görünür bir **Tanınma Sayacı** en geç N denemede garanti verir. Bazı Yankılar özel koşul ister (bilgi ekseni, P9).
- **Adlandırma töreni:** Zaman durur, mürekkep dünyanın üstüne akar. Oyuncu adı yazar (en fazla 16 karakter; IME ve Deck ekran klavyesi), iki glif parçasını birleştirerek o Adlı'ya özel **tamgasını** çizer. Kâtip onaylar: *"Ad kabul edildi."*
- **Adlı'nın yapısı:** Rol (Öncü, Avcı, Destek, Taşıyıcı), 2 yetenek ve 1 pasif, bark ve saldırganlığı belirleyen bir **Mizaç**, bağ seviyesi ve evrim (EA'da 2, 1.0'da 3 aşama; model parçası, VFX ve palet değişir).
- **Kapasite:** Kut'a bağlı olarak sahada 1–3 aktif Adlı; kadro EA'da 12, 1.0'da 30. *Adlar Sancağı* ultimate'i tüm kadroyu birkaç saniye hayalet hücumla çağırır. Havuzlanmış düşük LOD spektral modeller kullanıldığı için animasyon bütçesi (PC ≤40) aşılmaz [R08].
- **Etik çerçeve:** Adlandırma köleleştirme değil **kimlik iadesi**: Yankı adını yitirmiş bir acıdır, ad ona benlik verir. Adlılar fikir beyan eder, **azat** edilebilir; veda sahnesinden sonra adları şehirdeki **Adlar Duvarı**'na kazınır. Kâtip'in bu adları kendi kaydına yazması Perde 2 geriliminin kaynağı.
- **İnsan yoldaşlar:** Kapıya bir insan yoldaş götürülür (EA'da Yaren ya da Ilgın). Basit davranış ağacı ve 2 yetenekle dövüşür, bağ göstergesi dolunca **Bağ Tekniği** cut-in'i yapar. Kamp ateşinde ikili sohbetler olur, bağ seviyeleri mekanik güç açar (Persona confidant modeli) [R03][R09].

### 5.5 Şehir ve yaşam katmanı

- **Bölgeler:** EA'da 3 bölge (Lonca Meydanı, Aşağı Çarşı, Sur Mahallesi); Yedi Fener Hanı, Doğan'ın demirhanesi ve Adlar Duvarı başlıca mekânlar.
- **Takvim:** Gün, Kapı koşusu ya da uykuyla ilerler, gerçek saatle değil. Hikâye Kapıları bekler; yan Kapıların taşma sayacı "gün" cinsinden işler.
- **Adlı görevleri:** Sur Nöbeti (taşma savunması), Hamal (malzeme), Ocak (dövme hızı), Bahçe (yemek), Keşif (Kapı ön bilgisi). Üretim oyun günüyle işler; "toplamazsan çürür" yok.
- **Dünya Bilgisi icatları:** Eski meslek ya da Anı Parçası, Kapı malzemesi ve bir usta (ya da Adlı) birleşince açılır. EA'da 8 icat: Triyaj Çadırı, Sabun Atölyesi, Kurutma/Konserve, Makara Sistemi, Işık Telgrafı (taşma uyarısı bir gün erken), Sigorta Sandığı (ölümde loot kaybı azalır), Izgara Harita, Pişmiş Tuğla Barikat. Her icat tabelada, NPC davranışında ve fiyatlarda görünür; Tensura IC'nin "yapılacaklar listesi" hatasına düşmemek için hepsi dövüşe ya da taşmaya bağlanır [R02].
- **Bağ ve ev:** Akşam sahneleri, buff veren Dünya tarifleri, zamanla dekore edilebilir bir eve dönüşen han odası (kozmetik gelir için doğal alan).
- **NPC hafızası:** Olay bayrakları ve ilişki vektörleri; LLM yok, ink ya da Dialogue Manager [R09]. *"Sen o gün Aşağı Çarşı'yı kurtaran F'liydin."*

### 5.6 Kapı yapısı ve prosedürel/el yapımı dengesi

- **Rütbe bantları:** E 3 kat (~10 dk), D 4–5, C 5–6 (ortada güvenli kat), B 7–8 kat (~25 dk). A ve S 1.0'da.
- **Kurgu:** Her biyomda el yapımı giriş, güvenli kat, 2–3 "landmark" oda ve boss arenası; yanında 20–25 **el yapımı kit oda**. `GateData` odaları seed ile dizer ve düşman bütçesini yerleştirir. Yani her oda el yapımı; prosedürel olan dizilim, popülasyon ve **Kapı Anomalileri** (karanlık, su baskını, ters yerçekimi). Her biyomun bir imza mekaniği var [R03][R08].
- **Özel Kapılar:** **Mühürlü Kapı** (boss ölene kadar çıkış kapalı, ödül ×3, ölüm cezası yüksek), **Arızalı Kapı** (Kâtip'in parmak izi, hikâye ipucu), **Aykırı işgal** (nadir elit istilacı; DanMachi'nin "irregular"ı).
- **Taşma:** Sayacı dolan Kapı bölgeye taşar; bölgenin instanced savunma haritasında dalgalar ve taşma boss'u gelir. Kaybedilirse dükkânlar geçici kapanır, fiyatlar artar, NPC'ler yaralanır; hasar görev ve Adlı emeğiyle onarılır. "Rahat Takvim" modunda taşma hasarı kapalı.

### 5.7 Ölüm ve başarısızlık

- **Kapıda ölüm = Yeniden Derleme:** Kâtip bedenini kayıttan yeniden kurar; Kapı eşiğinde ya da son Mühür Taşı'nda başlarsın. Derlenmemiş deneyim ve loot'un %50'si kaybolur (Sigorta Sandığı azaltır). Kodeks, boss notları ve Tanınma Sayacı korunur; bilgi asla kaybolmaz.
- **Anlatı ödülü:** Hades modeli; ölüm nedenine özel Kâtip replikleri ve Döngü sayacı [R03]: *"Bedenini 14. kez derledim. Artık yüzünü ezbere biliyorum."*
- Adlılar Kapıda dağılır, Derleme'de toplanır. Başarısız sınav ertesi gün ücretsiz tekrarlanır; başarısız taşma onarılabilir hasar bırakır.
- **Sistem Desteği:** Her ölümde hasar direnci artar (en fazla %60); başarımlar ayrı işaretlenir, utandırma yok [R03]. **Tek Kayıt** (isteğe bağlı): kalıcı ölüm, kalıcı Adlı ve taşma kaybı, ayrı tablo.

---

## 6. İlk 2 Saat (Steam iade penceresi: 14 gün ve <2 saat) [R03][R04]

| Dakika | Akış | Hedef his / telemetri |
|---|---|---|
| 0:00–0:01 | Siyah ekranda yanıp sönen mürekkep imleci, titreyen telefon. Kontrol hemen oyuncuda: gece yarısı son metro vagonu | Merak · `ftue_start` |
| 0:01–0:05 | **Son Gün:** Kilit ekranında ad alanı boş ("sonra"). İş kartıyla 5 meslekten biri, vagon camındaki yansımayla görünüş seçilir. Son mesajlardan seçilen "son saat" bir pişmanlık tohumu olur | "Bu benim hayatım" |
| 0:05–0:09 | Peronda Kapı yırtılır. **Kapı Tazısı**'na karşı mesleğe bağlı doğaçlama silahla dövüş: Kıl Payı, hafif/ağır saldırı, ilk hitstop ve onomatope. Kazanılamaz. "[Kabul] [Kabul]" bildirimi; Tazı seni içeri çeker | Dövüş iyi hissettiriyor · `prologue_fight` |
| 0:09–0:12 | Şehir uğultusu kulak çınlamasına, sonra sessizliğe döner. **Batık Fener** Kapısı'nda bir hamal ekibinin ortasında uyanırsın; altyazılar yabancı gliflerle akar | Yabancılık |
| 0:12–0:22 | Yaren'le jest tabanlı kelime öğrenme (su, kaç, kapı, ad). Hamal bıçağıyla zayıf Yankılar. Kâtip arızalı pencerelerle belirir: "[HATA] Kayıtsız varlık" | Merak · `lang_words` |
| 0:22–0:30 | **Mühürlü Kapı:** çıkış kapanır, Fener Bekçisi uyanır, ekibin C rütbeli avcısı düşer. Oyuncu zaman kazanır ve yere yığılır (senaryolu yakın ölüm) | Çaresizlik |
| 0:30–0:36 | **"ADINI YAZ_"**. Zaman durur, mürekkep dünyanın üstüne yazılır: *"Adsız varlık tespit edildi. Ad alanı: boş."* Oyuncu adını yazar: *"Ad kabul edildi."* Müzik girer, avuçta tamga yanar. Kâtip "SİSTEM" kelimesini açıklar; **Dil Kavrayışı Lv1** altyazıları oyuncunun diline çevirir. İlk puan dağıtımı, "Sınıf: [KİLİTLİ]" | Uyanış (90. dakikadan çok önce) · `system_awaken` |
| 0:36–0:45 | Rövanş: iki yeni yetenek, ilk Denge kırılması ve **Mühür Vuruşu** cut-in'i. Tazı'nın Yankısı seni tanır: **ilk Adlandırma**. Boss'un Yankısı reddeder ("her Yankı tanımaz") | Güç tersine dönüyor · `first_naming` |
| 0:45–0:55 | Kapıdan çıkış; vinç çekimiyle **Dokuzkapı** ve ana tema. Yaren'le bağ başlar | Hayranlık · `town_arrival` |
| 0:55–1:05 | **Lonca kaydı:** kristal boş kalır, **"F — Tamgasız"**, gülüşmeler. Kâtip fısıldar: *"Onların ölçeği benim ölçeğim değil."* | Küçük düşürülme · `guild_card` |
| 1:05–1:15 | Han odasında **ilk Derleme** (sayılar yükselir). %3 şarjlı Eski Telefon kristalle dolar, ilk fotoğraf. Avluda Tazı'yı sevme. Doğan'da silah seçimi: Çift Bıçak ya da Mızrak. İsteğe bağlı Günlük Kalibrasyon | Ev hissi · `first_seal` |
| 1:15–1:40 | Panodan ilk E Kapısı ("Taşmaya 3 gün"), yanında Yaren. İlk 3'lü Teklif ve ilk **Kızıl Teklif**; Mühür Taşı'nda "çık ya da derine in"; boss ve ikinci Adlı (Tuz Kertenkelesi) | Özerklik · `first_gate_clear` |
| 1:40–1:55 | **TAŞMA!** Giremediğin bir D Kapısı Aşağı Çarşı'ya taşar; Muhafızlar çaresiz. Adlılarla savunma, Taşkın Dev, ilk **Tamga** ultimate'i ve Nam patlaması. Tolga donakalır | **Aura anı** · `first_break` |
| 1:55–2:00 | Kâtip'in "sessiz" log satırı: *"[Taşma zamanlaması: düzeltildi]"*. ED şarkısı; Yaren ile Kâtip'in atıştığı "Sonraki bölüm: *F Rütbeli Kahraman*" önizlemesi. Kayıt, doğal durma noktası | "Bir bölüm daha" · `ep1_complete` |

**Next Fest demosu** bu 0:00–2:00 dilimidir ve istek listesi çağrısıyla biter. Fest'e yalnızca ana oyunun demosu katılabilir [R10].

---

## 7. Sürükleyicilik Özellikleri

1. **Kâtip = sesli karakter.** Perde 1'de bürokratik ve komik (TR: *"Sayın Adsız, ölümünüz kayda geçmiştir."*), Perde 2'de meraklı, Perde 3'te itiraf eden ya da yalvaran bir varlık. Dört dilde tasarlanmış AI sesi; insan olmadığı için kurgusal olarak meşru ve beyanlı [R07].
2. **Mürekkep-Mühür diegetik arayüzü.** Pencereler dünya uzayında görünmez bir kalemle **o an yazılır**, onaylar kırmızı mühürle basılır; mavi hologramdan belirgin biçimde farklı [R01].
3. **"Havayla konuşuyorsun" tepkileri.** NPC'ler boşluğa baktığını fark eder; hem mizah hem yalnızlık [R09].
4. **Son Gün prologu.** Eşyalarla karakter yaratma, mesleğe bağlı doğaçlama silah.
5. **"ADINI YAZ" uyanışı.** İlk ad, ölüm anında kendine verilir.
6. **Adlandırma ve Adlar Duvarı.** Yazdığın adlar NPC metinlerinde, görev panosunda ve duvarda yaşar; azat edilen Adlı için veda sahnesi.
7. **Eski hayat perk'leri ve pişmanlık görevleri.** EA'da 5 meslek (Aşçı, Yazılımcı, Sağlıkçı, Sporcu, Kurye). Yazılımcı, Kâtip'in arızalarını ve gizli modifier'ları okur, özel diyaloglar açar [R09].
8. **Dünya Bilgisi icatları.** Şehirde görünür, sistemik değişiklikler.
9. **Eski Telefon.** Kristalle şarj olur. Kamera fotoğraf modu (manga paneli filtresi), Notlar günlük, Müzik anı çalma listesi; arada Dünya'dan bozuk bildirimler düşer (P3 gizemi).
10. **Kısa, atlanabilir dil engeli.** Öğrenilen kelimeler şehir tabelalarında karşına çıkar.
11. **Halka açık rütbe sınavları.** Nam, kalabalık tepkisi, Maske seçimi.
12. **Taşma sirenleri.** Bölge hasarı ve yeniden inşa; şehir sensiz kötüleşebilir ama her şey telafi edilebilir.
13. **Kızıl Teklifler.** Kişisel güç ile şehrin güvenliği arasında ahlaki takas; Kâtip'in gündemi oynanışa sızar.
14. **Yeniden Derleme replikleri.** NPC'ler de hatırlar: *"Yine mi Mühür Taşı'ndan çıktın?"*
15. **Anime bölüm sunumu.** Başlık kartı, olay günlüğünden otomatik "Önceki bölümde…", OP/ED, seslendirilmiş önizleme [R01].
16. **Gerçek tarih sayacı (opt-in).** "Dünya'dan ayrılalı N gün" ve yıldönümü replikleri; asla cezalandırmaz [R09].
17. **Gerçek Dünya Görevi (opt-in).** 90 dakikadan sonra Kâtip: *"Uyku da bir istatistiktir."* [R09].
18. **Leitmotif haritası.** Soğuk synth'le başlayan Sistem teması ısınır; Adlandırma anında Dünya'nın piyano temasıyla birleşir.
19. **Ses imzası ve haptik.** Kalem cızırtısı ve mühür "tık"ı marka sesi; düşük HP'de kalp atışı titreşimi.
20. **Yayıncı modu.** Oyuncu ve Adlı adlarını gizler, telifsiz müzik çalar.

---

## 8. Endgame ve Uzun Vadeli Bağlılık (karanlık desen olmadan)

| Mod | İçerik | Koruma |
|---|---|---|
| **Sonsuz Eşik** | Her 10 katta yeni kural getiren sonsuz Kapı. Kalıcı ve sezonluk tablolar ayrı. EA'da ilk 30 kat | Güç satılmaz. Kalıcı ilerleme kaybolmaz |
| **Kapı Yeminleri** | Hades Heat benzeri gönüllü zorluk sözleşmeleri. Ödüller kozmetik ve unvan | Güç ödülü yok, ayrı tablo [R03] |
| **Haftalık Anomali** | Sabit seed ve Steam liderlik tablosu (kendi sunucumuz yok) | Katılmayana ceza yok. Arşiv seed'ler sonradan oynanabilir |
| **Adlı Kodeksi** | 16 türün (1.0'da 32) evrimleri, nadir Mizaçlar, özel Tanınma koşulları | Oranlar ve garanti sayacı görünür. Paralı hızlandırma yok |
| **Gizli sınıflar ve sırlar** | Dünyaya dağıtılmış ipuçları, "ilk keşfeden" topluluk kültürü | Asla satılmaz |
| **Şehrin yeniden doğuşu** | Bölge refahı, icatlar, Adlı iş gücü | Gerçek zamanlı üretim yok. Oyun günüyle, üst sınırlı |
| **Yeniden Kayıt (NG+)** | Kodeks ve bilgi taşınır. Kâtip'in farklı bir kişilik yolu ve diğer sonlar | — |
| **Tek Kayıt** | Kalıcı ölüm modu | İsteğe bağlı, ayrı tablo |

**Kurallar:** Günlük Kalibrasyon bonusu "dinlenmiş XP" gibi en fazla 7 gün birikir; aynı güç günlük yapmayana da açıktır. Seri cezası yok. Kaçırılan günler **Disiplin Kapısı**'nı açar: gönüllü, 4 dakikalık, yüksek ödüllü hayatta kalma; "ceza bölgesi"nin cezasız karşılığı [R01]. Geri dönen oyuncuya hızlandırma; suçluluk metni ve "seni özledim" bildirimi yok [R03].

---

## 9. Monetizasyon (EA → 1.0 → DLC)

| Faz | Ürün | Fiyat | İçerik ve kural |
|---|---|---|---|
| Çıkış öncesi | Ücretsiz demo (Bölüm 1) | 0 | Next Fest Şubat 2028 |
| EA (Mart–Nisan 2028) | Ana oyun | **19,99 $** | Perde 1 ve ücretsiz bölüm güncellemeleri (6–10 haftada bir). Steam'in bölgesel fiyat önerileri uygulanır |
| 1.0'dan ≥30 gün önce | Fiyat artışı | 24,99 $ | Steam kuralı gereği fiyat artışı 1.0 çıkış indiriminden en az 30 gün önce yapılır [R04] |
| 1.0 (2029 1. yarı) | Ana oyun | **24,99 $** | Tam hikâye ve üç son. Çıkış indirimi %10–15 |
| 1.0 ile birlikte | **Destekçi Paketi** | 9,99 $ | OST, dijital artbook, "Kâtip Mührü" arayüz teması, 2 kozmetik set, kredilerde isim. Oyun avantajı yok |
| 1.0 ile birlikte | OST (Steam, Bandcamp) | 7,99–9,99 $ | Content ID'ye kaydedilmez, yayıncılar serbest [R10] |
| 1.0 + 2–9 ay | Kozmetik DLC | 2,99–4,99 $ | "Dünya'dan gelen okul üniforması", tamga desen paketleri, Adlı kostümleri. İçerik satın almadan önce görülür, rastgele değil |
| 1.0 + 9–15 ay | **Genişleme "Kızıl Bozkır"** | 12,99–14,99 $ | Yeni bölge, 2 biyom, yeni yoldaş, Adlı türleri |
| Sonra | Complete Edition, konsol portu, fırsatçı mobil port, merch | — | Konsol için W4 ya da port ortağı [R08] |

**İlkeler:** Oyun içi mağaza yok; DLC'ler ana menüden Steam sayfasına bağlanır. Ücretli rastgelelik yok; kod düzeyinde ADR ile hiçbir ürün rastgele tabloya bağlanamaz [R04]. Slogan: *"Gacha yok. Enerji yok. Güç satılmıyor."*

**Gelir senaryoları** (24 ay, vergi öncesi net) [R04]: kötümser 5 bin kopya ~49 bin $, temel 50 bin ~515 bin $, iyimser 400 bin ~4,3 milyon $. Bütçe kötümser senaryoya göre kurulur.

---

## 10. Sanat ve Ses Yönü

### 10.1 Görsel hedef

- **Stil:** Modern TV animesi görünümünde cel-shaded 3D: iki tonlu ramp gölge, SDF yüz gölgesi, stencil outline, rim light, saç ve kumaşta spring bone, stilize post-process [R06][R08].
- **Referans üslup tarifi** (prompt'larda IP ya da sanatçı adı yok): *"temiz çizgi, iki tonlu gölge, yüksek kontrastlı aksiyon kareleri"*; *"terrakota, lapis çini, pirinç fenerli kervan şehri"*. Her Kapı kendi paletinde: Batık Fener yosun ve kehribar, Cam Kumlar kırık gökkuşağı, Kemik Koru kemik beyazı ve pas, Çarkhane bakır ve mürekkep.
- **Sistem arayüzü:** Yarı saydam, lake benzeri koyu panellerde altın mürekkep ve vermilyon mühür. Latin, kana ve Hanzi'yi kapsayan özgün kaligrafik-geometrik font.
- **Dövüş dili:** Guilty Gear Xrd tipi "2'lerde" özel hareketler, 2D illüstrasyon ve 3D karışımı cut-in panelleri.

### 10.2 AI destekli üretim hattı

| Varlık | Yöntem | İnsan payı |
|---|---|---|
| Key art, logo, capsule | Yalnızca referans | **%100 insan** (telif ve "AI slop" riski) [R10] |
| Kahraman tasarımları | Nano Banana Pro / Qwen-Image-Edit karakter sayfaları; Animagine XL 4.0 ya da Illustrious v1.x LoRA (NoobAI'siz) | Nihai çizimler insan illüstratörden [R05] |
| Kahraman 3D | VRoid gövde ve yüz, Blender'da özel saç ve kıyafet, VRM 1.0, godot-vrm | Yüz ve saç cilası [R06] |
| Oyuncu avatarı | CC0 Quaternius Base Characters ve parça sistemi (VRoid'in "karakter yaratıcı" yasağı) | — |
| Yankılar ve Adlılar | Konsept → Meshy/Tripo ücretli sprint ayı → retopo. **Aile başına tek rig**, evrimler parça ve VFX ile. Hunyuan yok | Retopo, imza boss hareketleri |
| Animasyon | UAL 1+2 ve KayKit (CC0), Mixamo; imza hareketler telefon mocap'i ve Rokoko/DeepMotion ücretli ayıyla, Blender ya da Cascadeur Indie'de stepped key cilası | Hold, smear, impact zamanlaması |
| VFX, arka plan | Effekseer ve shader VFX; arka plan ve ikonlar Gemini Batch (Vertex) ya da yerel ComfyUI | Rötuş |

Her varlığa bir **manifest** satırı (model, lisans, seed, insan düzenlemesi). Steam beyanı pazarlama materyallerini de kapsar. Kör testte "AI" şikâyeti ≤%10 bir kapı kriteri [R05][R10].

### 10.3 Ses ve seslendirme

- **Kâtip:** EN, JA ve TR'de Voice Design ile özgün ses (Gemini TTS ya da VoxCPM2), klon yok. Ton "resmî daire anonsu"; JA'da 事務的な敬語. Adlandırma anlarında ses kısa süre bozulur.
- **Ana kadro:** EN insan seslendirme: kilit sahneler, efor sesleri, imza replikler. Sözleşmelerde AI maddesi (klon ve model eğitimi yasak). JA çift dublaj 2. fazda, satışa bağlı [R07].
- **NPC bark'ları:** EA'da EN tasarlanmış AI sesi; JA, TR ve ZH'de metin (JA topluluğunun AI sese hassasiyeti) [R07].
- **Adlılar:** Yaratık SFX katmanları. Oyuncunun verdiği adlar seslendirilmez, seslendirmede unvan kullanılır ("Öncü").
- **Müzik:** Ana tema, vokalli OP ve ED insan besteciden (OST hakları sözleşmede). Döngü varyasyonları ACE-Step 1.5 (MIT) ya da Lyria ile üretilip insan eliyle düzenlenir. Adaptif yapı `AudioStreamInteractive/Synchronized`; vokal "drop" yalnızca aura anlarında.
- **SFX:** Kenney (CC0), Sonniss, ElevenLabs SFX'in ücretli bir ayı, Stable Audio Open.

---

## 11. Kapsam

### 11.1 İçerik sayıları

| Kalem | **EA (Mart–Nisan 2028)** | **1.0 (2029 1. yarı)** |
|---|---|---|
| Hub | 1 şehir, 3 bölge, ~40 isimli NPC | 5 bölge, ~70 isimli NPC |
| Kapı biyomu | 4 (Batık Fener, Cam Kumlar, Kemik Koru, Çarkhane) ve Dünya prologu | 7, Divan Harabeleri ve Onuncu Kapı |
| Oda kiti | ~100 kit oda, 12 landmark, 4 boss arenası, 3 taşma bölgesi haritası | ~175 kit oda, 21 landmark |
| Düşman | 20 temel tip, 10 elit varyant, 3 kültist | 35 temel tip, 25 varyant, 6 kültist |
| Boss | 6 (4 biyom, Mühürbozan, Taşkın Dev) ve 3 sınav rakibi | 14 ve final boss (sona göre 3 varyant) |
| Adlanabilir tür | 16 × 2 evrim, kadro 12 | 32 × 3 evrim, kadro 30 |
| Silah arketipi / yetenek | 2 (Çift Bıçak, Mızrak): 20 aktif, 8 Tamga Sanatı, 30 pasif, 4 ultimate | 4 (+ Ağır Kılıç, Tamga Zinciri): ~40 aktif, 60 pasif, 8 ultimate |
| Sistem Teklifi | 60 (8'i Kızıl) | 120 |
| Yoldaş | 3 insan (Yaren, Ilgın, Doğan) ve Tazı. Mei ilk EA güncellemesinde | 5 insan ve 2 hikâye Adlısı |
| Meslek / icat / gizli sınıf / sınav | 5 / 8 / 2 / 3 (F→C) | 8 / 20 / 6 / 6 (→S) |
| Diyalog | ~8.000 yazılı satır (~55 bin kelime); Kâtip ~1.500 satır × 3 dil (AI); insan EN ~1.200; AI bark ~1.500 (EN) | ~25.000 satır (~170 bin kelime); Kâtip ~4.000 × 4 dil; insan EN ~4.000; JA dublaj faz 2 |
| Müzik | ~25 parça (OP, ED dahil) | ~50 parça |
| Oynama süresi | 12–18 saat ana içerik ve tekrar oynanabilir Kapılar | 35–45 saat hikâye, 80+ saat tamamlama |

**Yapılmayacaklar (ADR):** Açık dünya yok. EA'da co-op yok. EA'da canlı LLM ya da runtime TTS yok. Kumarhane yok. Oyun içi mağaza yok [R10].

### 11.2 Yol haritası (temel senaryo, R10)

**F0** (Ekim 2026, 3–5 hafta): Rendering Spike, sanat bible'ı, marka taraması, ADR'ler → **F1 prototip** (Ocak 2027): gri kutu dövüş, Kâtip arayüzü, bir Kapı → **F2 dikey kesit** (Nisan 2027): Son Gün, uyanış, ilk Adlandırma, Batık Fener ve Fener Bekçisi; "1 kat = X gün" üretim hızı burada ölçülür → **Steam sayfası** Nisan–Mayıs 2027 → **Playtest** Temmuz–Eylül 2027 → **demo** Kasım–Aralık 2027 → **Next Fest** Şubat 2028 (fest öncesi ≥7–10 bin, EA kararı için ≥15–20 bin istek listesi) → **EA** Mart–Nisan 2028.

### 11.3 En riskli 5 teknik iş

1. **Godot'da anime render:** ramp, SDF yüz, outline, VRM spring bone ile hedef konsept karelere ulaşmak ve Deck'te ≥40 FPS. Önlem: F0 spike kapısı ve Unity 6.3 yedeği [R08].
2. **Dövüş hissi ve aksiyon durum makinesi:** kare verisi, iptal pencereleri, hitstop, impact frame, cut-in, root motion ve kilitlenmenin, 3 Adlı ve 1 yoldaş yapay zekâsıyla birlikte 60 Hz'de tutarlı çalışması. Önlem: veri güdümlü `ActionData`, simülasyon testleri, erken dış playtest.
3. **Runtime Adlı sistemi:** dört dilde oyuncu adı girişi (IME, Deck ekran klavyesi; GodotSteam'in bakım durumu belirsiz [R08]), Türkçe ek uyumu yardımcıları ("Karabaş'a", "Ayşe'ye"), çevrimdışı küfür filtresi, evrim parça değişimi, şehir iş gücü ve kayıt.
4. **Prosedürel Kapı birleştirme:** kit odaların navmesh'le dizilmesi, düşman bütçesi, liderlik tablosu için deterministik seed. Sınır PC'de ≤40, Deck'te ≤25 animasyonlu düşman; spektral ordu ultimate'i dahil.
5. **Şehir durumu ve tepkisellik:** taşma sayaçları, bölge hasarı ve onarımı, NPC hafıza bayrakları, şemalı JSON kayıt ve migrasyonlar; üstüne dört dilli yerelleştirme hattı ve pseudolocalization CI'ı [R08][R09].

---

## 12. Neden Bu Konsept Kazanır / Zayıf Yanları (dürüst)

**Neden kazanır:**
- **Boşluğu tam hedefliyor:** Dünya'dan gelen "ben", karakter olarak Sistem, tepki veren şehir ve modern bilgi başka hiçbir oyunda birlikte yok [R02].
- **Klip üreten kancalar:** Ölürken adını yazmak; seni Dünya'dan çeken canavarı adlandırıp köpeğin yapmak (oyuncular gerçek evcil hayvanlarının adını verecek); taşmada F'linin aura anı; boss olan arayüz [R10].
- **Premium ve adil model** gacha yorgunluğuna doğrudan cevap [R04]; çekirdeği Claude ajanları ve headless Godot'a en uygun sistem ve metin işi [R08]; Solo Leveling S3 dalgası ve TR/JA/ZH yerelleştirme pazarlamayı destekler.

**Zayıf yanlar ve riskler:**
- **"Solo Leveling kopyası" algısı.** Overdrive ve KARMA ile kıyaslanacağız. Özgün terim, UI dili ve ad teması tutmazsa hem hukuki hem itibar riski var [R01].
- **Kalite çıtası çok yüksek.** 3D anime aksiyon dövüşü tek kişilik ekip için en pahalı tür; Hades (~20 kişi) ve E33 (~33 kişi) cilasına yaklaşmak zor [R10].
- **Sistem sayısı fazla.** Adlılar, şehir simülasyonu, taşmalar, icatlar ve dört dil kapsam şişmesine açık. G2'deki üretim hızına göre biyom, Adlı ve icat sayısı kesilmeye hazır olunmalı.
- **Roguelite tekrarı.** Overdrive'ın "tekrarlayan görev ve grind" eleştirisi bizi de vurabilir; kit oda, anomali ve Teklif çeşitliliği yetmeli [R02].
- **AI damgası.** Kâtip'in AI sesi kurgusal olarak savunulabilir, ama tek bir kötü AI görseli kampanyayı batırabilir (Postal vakası) [R10].
- **Kültürel ve tonal riskler.** Türk-Orta Asya teması küresel kitleye niş görünebilir; JA kitlesi için 1.0'da bir Tokyo prolog varyantı düşünülebilir. Kâtip'in faydacı ahlakı ve "sabit rütbeler" sonu kötü yazılırsa vaaz gibi durur.
- **Gerçekçi beklenti.** Temel senaryo ~50 bin kopya. Hit için Next Fest'te üst %5'e (≥13 bin istek listesi) girmek gerekiyor; garanti değil [R04][R10].
