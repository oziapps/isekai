# Konsept B — KORDAŞ: Kuyunun Közleri

> Açı: "Zindan Şehri ve Patron Tanrılar" (DanMachi ağırlıklı) · Hazırlanma: 2026-09-24 · Dayanak: `docs/research/01–10`
> Tüm isimler, terimler ve arayüz dili özgündür. Trope'lar serbesttir; Falna, Familia, Orario, "Arise" ve mavi pencere estetiği kullanılmaz (01 §9).

## 1. Künye

| Alan | Değer |
|---|---|
| Çalışma adı | **KORDAŞ** (EN: *KORDASH: Embers Below*; JP: 『コルダシュ ～深淵の残り火～』). "Kor" (köz) + "-daş" (yoldaş, kardeş): aynı közü paylaşanlar. Uydurma kelime; F0'da sınıf 9/41 marka taraması |
| Tür | Aksiyon-roguelite zindan inişleri + Persona ağırlığında şehir/ilişki simülasyonu; özgün IP anime isekai ARPG |
| Platform ve motor | PC (Steam, Windows/Linux), Steam Deck Verified hedefi; konsol 1.0 + 12–24 ay (W4 veya port ortağı). Godot 4.7.x, katı tipli GDScript. F0'da Anime Rendering Spike; başarısızsa Unity 6.3 LTS (karar 2027'ye kalırsa 6.7 LTS) |
| Kamera | Şehir: yakın 3. şahıs, sokak seviyesi. Kuyu: yüksek açılı 3/4 aksiyon kamerası (okunurluk, prosedürel oda). Diyalog: 2D anime portre; imza anlarda 3D cut-in |
| Hedef kitle | Birincil: Persona, Hades ve DanMachi seven 18–34 yaş oyuncu (01 raporu C + A segmentleri). İkincil: 30+ "ikinci şans ve inşa" oyuncusu (B). Harem yok |
| Fiyat | EA 19,99 $ → 1.0 24,99 $ (artış 1.0'dan ≥30 gün önce); bölgesel fiyat. Gacha, enerji ve premium para yok |
| Oturum | 1 oyun günü = 1 oturum = 30–45 dk (PC medyanı 32–33 dk). Doğal durma noktası gece Fincan Töreni. İnişsiz kısa gün 10–15 dk |
| Derece ve dil | PEGI 12/16, ESRB T. EA: EN, JA, ZH-Hans (insan LQA), TR (arayüz ve altyazı, Türkçe Defter sesi). 1.0: + KO, PT-BR, ES |
| Takvim | Next Fest Şubat 2028 → EA Mart–Nisan 2028 → 1.0 2029 1. yarı (10 raporu temel senaryo) |

## 2. Logline ve "Neden Şimdi / Neden Biz"

**Logline:** Dünya'da yıllardır eve gidemeyen sıradan biri, gece metrosunun kapısından unutulmak üzere olan küçük bir tanrıçanın son duasıyla çekilir: Eve Dönüşlerin İyesi **Sıla**. Onun batık çayhanesi, dipsiz **Kuyu**'nun ağzına kurulu kervan şehri **Bezirgân**'ın en yoksul ocağıdır. Gündüz şehirde çalışır ve bağ kurarsın, akşam Kuyu'ya inersin, gece tanrıçan fincanını okur ve gücünü mühürler. Unutulan tanrılar Kuyu'nun dibinde canavara dönüşür. Sıla'nın közü ise ancak ocağında yaşayanlar kadar yanar.

**Kanca:** "Tanrın seni her ölümde eve getirir. Sen de onu unutulmaktan kurtarırsın."

**Neden şimdi:**
- DanMachi S6 duyuruldu (Şubat 2026), ama DanMachi hayranının oynayacağı aktif oyun yok: Memoria Freese 2024'te, Battle Chronicle Eylül 2025'te kapandı. İkincisi için bile "hikâye ve ses harika, oynanış zayıf" denmişti (02).
- Formülün parçaları kanıtlı: Persona 3 Reload 3 milyon (Haziran 2026), Metaphor 2 milyon, Hades II 1.0 öncesi 2 milyon+, Fantasy Life i 1,5 milyon.
- Gacha yorgunluğu ölçülebilir (Duet Night Abyss, Ananta, Overdrive). "Gacha yok" artık bir satış argümanı.
- 02 raporunun boşluk tablosu: "oyuncunun kendi kimliği + mekanik olarak Sistem + tepki veren dünya + kalıcı bağlar + zindan" birleşimi hiçbir oyunda yok. Solo Leveling: KARMA F2P ve mobil öncelikli, raf farklı.

**Neden biz:**
- Kapadokya yeraltı şehirleri, kervansaray, ebru, kilim ve fincan falı isekai'de kullanılmamış bir palet. Türk geliştirici için otantik, küresel oyuncu için egzotik (01 #11).
- Türkçe anime kitlesi resmî platformlarda hizmet alamıyor. TR arayüz ve Türkçe Defter sesi ilk günden PR kaldıracı.
- Konseptin ağırlığı sanattan çok sistem ve veri işinde (tepkisel diyalog, prosedürel oda, takvim); Claude Code ajanları ve Godot headless CI tam burada verimli (08).

## 3. Dünya ve Hikâye Tohumu

### 3.1 Dünya
- **Bezirgân:** Tüfe oyulmuş peri bacası kuleler, teraslı çarşılar ve kervansaraylardan oluşan kervan şehri. Bütün servet Kuyu'dan gelir: canavar tortusu, ışık tuzu, Dünya'dan ve zamandan düşmüş eşyalar.
- **Kuyu:** Halk deyişindeki "yerin yedi kat dibi" burada gerçektir. Yedi **Kat** vardır; her biri basamaklardan, güvenli bir **Konak**'tan ve bir bekçiden oluşur. Kuyu haftada bir "nefes alır" ve iç düzenini değiştirir; prosedürel yapının kurgusal gerekçesi budur.
- **İyeler ve Ocaklar:** Tanrılar (halk inancındaki "iye" kavramının özgün yorumu) inananlarının közüyle yaşar. Bir İye'nin çevresindeki hane **Ocak**'tır. Üyeler ocağın **Kor**'unu besler, İye de onları Kuyu'da korur. Ocağı sönen İye unutulur, Kuyu'ya batar ve **Sönük**'e, yani katların acılı bekçi-tanrılarına dönüşür.
- **Divan:** Ocakları, ruhları ve iniş izinlerini kaydeden şehir bürokrasisi. Kaydı olmayan Kuyu'ya yasal olarak inemez.
- **Defter (Sistem):** Yalnızca oyuncunun gördüğü, ebru hareli parşömen ışığından sayfalar. Kuru bir kâtip diliyle konuşur, sana "Kayıtsız" der, görev (**Tezkire**) yazar, tortunu sayar. Sırrı Perde 2'de açılır.

### 3.2 Varış anı
Kamyon yok. Oyuncu gurbette yaşayan biridir. Son akşamında telefona "Bayramda geliyor musun?" mesajı düşer, oyuncu "Bu sefer de olmadı" yazar. Gece metrosunun kapısı açıldığında karşısında çay ve toz kokan ılık bir ışık vardır ve bir ses "Eve hoş geldin" der. Sıla'nın gücü yetmez; oyuncu çayhaneye değil, Kuyu'nun ilk katına düşer.

### 3.3 Ana çatışma
Şehrin en büyük ocağı, Bereket ve Ticaret İyesi **Zerrin**'in 3.000 kişilik hanesidir. Divan'ı, iniş asansörlerini ve aşevlerini o yönetir; halk onu sever. Zerrin küçük ocakların borçlarını satın alır, İyelerini sönmeye bırakır ve közlerini kendi ocağına katar. Ona göre bu merhamettir: "Tek büyük ocak herkesi doyurur." Sıla'nın ocağı 30.000 akçe borçlu ve listede sıradaki. Oyuncunun kişisel sorusu ise hiç değişmez: Kuyu'nun dibindeki eşik gerçekten eve açılıyorsa, dönecek misin?

### 3.4 Üç perdelik ana hat

| Perde | Katlar | Özet | Duygusal zirve |
|---|---|---|---|
| **1. Kayıtsız** (EA) | 1–3 | Varış, Sıla'nın ocağına kabul, Divan kaydı, borç. Oya, Dağhan ve Bilge ocağa katılır; ilk festival (Dilek Gecesi), rakip Ren. 3. Kat'ın Sönük'ü, Oya'nın ailesinin kayıp İye'si çıkar: ilk Ad Verme kararı | Oya'nın tanrısını eve getirmek ya da söndürmek; Sıla'nın ayaklarının ilk kez saydamlaşması |
| **2. Ocaklar** | 4–5 | Zerrin'in "Birleşme Fermanı", ocaklar arası festival yarışları, Ren'in Lütuf Sistemi'nden kopup ocağa sığınması, Aras'ın katılışı, Bilge'nin sahte kayıtları ifşa etmesi. **Sır:** Defter, Sıla'nın "hiç kaybolmayasın" diye kendinden kopardığı ilahi parçadır; her Derece onun közünden beslendi. Kuyu taşkınında Sıla bütün haneyi eve fırlatmak için son közünü harcar ve Kuyu'ya batar | "O bizi hep eve getirdi." Ocak soğur |
| **3. Yedi Kat Aşağı** | 6–7 | Hane Sıla'yı eve getirmeye ant içer. Yardım ettiğin şehir halkı geri döner: "Şehir hatırlar." Zerrin kendi açlığına yenilen trajik bir düşman olur. Yedinci Kat Dünya'nın aynasıdır: metro istasyonunun parçaları. Son dövüşte Defter'i Sıla'ya geri verirsin; arayüz söner, düşman işaretlerini kordaşların seslendirir. Sönük Sıla'ya adını geri verirsin | Üç son: **Dön** (Dünya), **Kal** (Bezirgân), **Eşiği Aç** (bağlar yüksekse Kuyu kayıp ruhların iki yönlü yolu olur). Hiçbir son parayla kilitlenmez |

### 3.5 Hane: patron ve kordaşlar (hepsi açıkça yetişkin)

| Karakter | Rol | Profil | Sır / kusur | Oynanış etkisi |
|---|---|---|---|---|
| **Sıla** | Patron İye: Eve Dönüşler ve Eşikler | Uzun boylu, pirinç anahtarlardan tacı ve yamalı kervan kaftanı var. Gururlu, beş parasız; kahvesi berbat, fal okuması kusursuz | Seni kahraman olduğun için değil, eve en çok hasret kalan ruh olduğun için çağırdı. Kendi közüyle yaşattığı Defter'i saklıyor | Fincan Töreni, Kor, Eşik çakma (kısayol), ölümde Eve Dönüş |
| **Oya** | İlk kordaş, yerli rehber | Ocaksız bir Kuyu hamalı. Sana dili ve gelenekleri öğretir, boş vakitlerinde oya işler | Ailesinin ocağı söndü, İye'si Kuyu'da. Kibirli ve borçlu | Tank ve destek; taşıma kapasitesi (ganimet sınırı +). Nakış motiflerini kaftanına o işler |
| **Dağhan** | Aşçı, ağır dövüşçü | Tüfken (taştan doğan halk). Borç tahsildarı olarak gelir, Sıla'nın kahvesini tadınca mutfağa yerleşir | Tüfkenler yaşlanınca taşa döner; o da dönmeye başladı | Kazan-kalkanla kalabalık kontrolü; canavar yemekleri ertesi güne buff verir |
| **Bilge** | Divan kâtibi | Seni "Kayıtsız" diye kaydeden titiz, alaycı memur. Geceleri gizlice iner | Kayıtların tanrı silmek için tahrif edildiğini biliyor. Kurala bağımlı, kaygılı | Mühür büyüsü: kontrol ve zayıflatma. Defter analizini derinleştirir |
| **Aras** (1.0) | Âşık (gezgin ozan) | Sazıyla festivalleri örgütleyen neşeli gezgin | Zerrin'in kaçak varisi | Ritim tabanlı buff ve ses dalgası; festival etkinlikleri |
| **Ren** (1.0) | Rakip yabancı | Dünya'dan çağrılmış eski profesyonel oyuncu. Zerrin'in verdiği **Lütuf** Sistemi rastgele kutsama çektirir | Çekiliş bağımlısı, tükenmiş, yalnız; Lütuf onu içten yiyor (gacha hicvi) | Yüksek riskli kritik saldırgan; Defter ile Lütuf arasında "iki Sistem" diyalogları |
| **Hatçe Nine** | Çayhanenin son müdavimi | Sıla'nın yaşayan son eski inananı, mahallenin dedikodu merkezi | Hafızası zayıflıyor | Söylenti sistemi, çayhane işleri |

### 3.6 Düşmanlar ve fraksiyonlar
- **Zerrin Ocağı:** Hayırsever görünümlü tekel. Muhafızlar, asansör loncası ve Lütuf şampiyonları.
- **Divan:** Tarafsız görünen, içeriden çürümüş kurum; hem engel hem müttefik adayı.
- **Sönükler:** Her katın bekçisi olan unutulmuş tanrılar. Her biri ocağının nasıl söndüğünü anlatan bir hikâye taşır.
- **Kuyu faunası:** Tortu, tuz ve kayıp eşyalardan doğan, avlanıp pişirilen ekolojik canavarlar.

## 4. Tasarım Sütunları

1. **Ocak güçtür.** Her sistem bir kordaşla an üretmeli ya da bağı mekanik güce çevirmeli. Test: Bu özellik sofrada konuşulacak bir şey doğuruyor mu?
2. **Her gün bir bölüm.** Sabah şehir, akşam iniş, gece tören ve "sonraki bölüm" kartı. Test: Her gün bir sayı ve bir sahneyle bitiyor mu?
3. **Hak edilmiş büyüme.** Nasıl dövüştüğün neyin güçleneceğini belirler. Güç satılmaz; bilgi ve kısayollar kalıcıdır.
4. **Bedel gerçek, ceza değil.** Ölüm Sıla'nın közünü harcar ama ilerlemeyi silmez. Son tarihler hikâyeyi dallandırır, oyunu bitirmez. FOMO yok.
5. **Burası başka bir dünya.** Diegetik arayüz, dil, kültür, hafızası olan NPC'ler ve Dünya'dan kalan izler.
6. **Aura anı.** Fincanın çatlaması, Ad Verme, nişan sınavında müfettişin donup kalması: kırpılıp paylaşılacak anime zirveleri.

## 5. Oyun Tasarımı

### 5.1 Döngüler

| Katman | Süre | İçerik | Ödül |
|---|---|---|---|
| Saniye | 0,3–5 sn | Kaçınma, karşılama (parry), kombo, Nakış yeteneği, kordaş tekniği | Hitstop, impact frame, Defter "tıkı", Alev göstergesi |
| Dakika | 1–5 dk | Oda temizle → kordaşlarının sunduğu 3 **Kıvılcım**'dan birini seç → ganimet | Koşu içi build, Tortu |
| Oturum | 30–45 dk | Bir oyun günü: sabah 1 şehir eylemi → akşam İniş (Konak'ta "eve dön ya da derine in") → gece Fincan Töreni ve Ocak Sofrası | Stat mühürleme, sofra sahnesi, sonraki bölüm önizlemesi |
| Hafta (oyun içi) | 7 gün, ~4–5 saat | Pazar günü, borç taksiti, NPC haftalık programları, Kuyu'nun nefesi | Borç ilerlemesi, bağ rütbesi, yeni oda düzenleri |
| Hafta (gerçek) | 7 gün | İsteğe bağlı **Yankı İnişi** (sabit tohum, liderlik tablosu) | Unvan ve kozmetik; kaçırana ceza yok |
| Sezon | Oyun içi mevsim; gerçekte 12 hafta | Mevsim festivali ve hikâye arkı. EA'da 12 haftada bir "anime sezonu" güncellemesi, OP/ED | Yeni kat, bağ rütbeleri, festival |

### 5.2 Dövüş
- **Kontroller (gamepad öncelikli):**
  - Sol çubuk hareket; B kaçınma (i-frame). Kusursuz kaçınmada kısa ağır çekim gelir: **Kapı Aralığı**.
  - X hafif, Y ağır/şarjlı saldırı.
  - LB **Karşıla**: 6 karelik kusursuz pencere düşmanın Denge'sini kırar ve Alev doldurur.
  - RB + yüz tuşları: 4 Nakış yeteneği. LT + yön: kordaş tekniği (cut-in). LT+RT: iki kordaşla **Ortak Ateş**.
  - R3: **Ocak Alevi**, Alev dolunca açılan aura/ultimate.
  - Select: Defter hızlı menüsü; zaman %20'ye yavaşlar, erişilebilirlik ayarında tam duraklatma var.
- **Kombo:** Silah başına 4–5 vuruşluk hafif zincir; bekletme ve gecikmeyle dallanan varyasyonlar, ağır bitirici, fırlatma, bazı silahlarda hava kombosu. İptal pencereleri kaçınma ve yeteneğe açıktır. Çerçeve verisi (startup/active/recovery) `ActionData` dosyalarındadır (08).
- **Silahlar:** EA'da Pala (hızlı, karşılama odaklı), Teber (menzil, süpürme) ve Yay + hançer (hareketli nişancı). 1.0'da Gürz (Denge kırıcı) ve Def (adaptif müziğin ritmine göre büyü) eklenir. Her silahın oyunla açılan 2–3 **Tavır** varyantı vardır.
- **Kıvılcım (koşu içi güçlendirme):** İnişe 2 kordaş götürürsün ve Kıvılcımları onlar sunar. Oya kalkan ve taşıma, Dağhan yanma ve ağırlık, Bilge mühür ve zaman temalıdır. Bağ rütbesi Kıvılcım nadirliğini yükseltir; iki kordaşın rütbesi yeterliyse **İkili Kıvılcım** çıkar. Şehirde kurduğun bağ, doğrudan Kuyu'daki gücündür.
- **Konuk İyeler:** Ad Verilen tanrılar 1–2 çağrı yuvasından kısa süreli yardımcı olarak çağrılır. Gölge ordusu trope'unun şefkatli, rızaya dayalı karşılığı.

### 5.3 İlerleme
- **Tortu → Status:** Dövüşte yaptığın şey ham **Tortu** biriktirir. Karşılama Çeviklik'i, darbe almak Dayanç'ı, ağır vuruş Kuvvet'i, isabetli atış İsabet'i, yetenek kullanımı Kut'u besler. Gece **Fincan Töreni**'nde Sıla fincanını okur ve telvedeki şekiller statlara mühürlenir. Her stat 0–100 arasıdır ve telve motifiyle gösterilir: Kum, Çakıl, Taş, Kaya, Dağ.
- **Derece (seviye):** Stat tavanını yalnızca bir **Büyük Tortu** kırar: bir Sönük'ü yenmek, bir kordaşı ölümün eşiğinden döndürmek, bir nişan sınavını kusursuz geçmek. O gece fincan çatlar, Derece atlar ve bir **Nakış** motifi seçersin. EA'da 6, 1.0'da 12 Derece var.
- **Kat Nişanı (rütbe):** Divan'ın seni hangi kata kadar yetkili saydığını gösterir: Nişansız'dan Yedinci Kat'a. **Nişan Sınavı**, müfettiş eşliğinde yapılan özel bir iniştir. Sonucu şehirde söylentiye dönüşür ve NPC tepkilerini değiştirir.
- **Kilim Tezgâhı (yetenek ağacı):** Oya'nın işlediği motif karolarını altıgen bir tezgâha dizersin. Komşu motifler "bordür" kurallarıyla sinerji kurar: 4–6 aktif yetenek ve pasifler. Tamamen deterministiktir, ücretsiz yeniden dokunur.
- **Ekipman:** Silah, kaftan ve 2 muska; demircide **deterministik zanaat**. Rastgele ganimet yalnızca oynayarak gelir, kötü şans korumalıdır.
- **Ocak Derecesi:** Çayhane-kervansarayın 6 odasını onarmak (mutfak, konuk odası, sunak, atölye, bahçe, gözlem kulesi) Sıla'nın gücünü, fincan okumasının derinliğini ve Eşik sayısını artırır.

### 5.4 Yoldaş ve parti sistemi
- İnişte oyuncu + 2 kordaş olur. Kordaşları yapay zekâ yönetir; basit emirler var: odaklan, koru, bekle, serbest. Kordaş başına 8–12 eylem vardır, tam hareket seti yalnızca oyuncudadır (animasyon kapsamı).
- Evde kalanlar **Ocak işleri**ne atanır: çayhane vardiyası, pazar tezgâhı, demirci çıraklığı, keşif. Akçe, Kor ve malzeme üretirler.
- **Bağ rütbesi 1–10:** Kıvılcım nadirliği, kordaş tekniği, Ortak Ateş, dengeyi değiştiren ödüllü kişisel görev ve şehir ayrıcalığı açar. Kordaşlar ikili sohbetlerle birbirleriyle de ilişki kurar.
- **Hafıza:** Verdiğin sözler, hediyeler, kimi Kuyu'da yaralı bıraktığın ve eski mesleğin olay bayraklarına yazılır. Ocak Sofrası ve bağ sahneleri bunlara atıf yapar. Tepkisellik yazılı ve deterministiktir (09 raporundaki K0+K1); canlı LLM yok.
- **Romans:** İsteğe bağlı; Oya, Bilge, Aras ve Ren için. Her karakterin kendi tercihleri var ve her oyuncu cinsiyetine en az iki seçenek düşer. Sıla ile bağ romans değil, aile bağıdır.

### 5.5 Şehir ve yaşam katmanı
- **Vakit:** Her gün Sabah, İkindi, Akşam ve Gece dilimlerinden oluşur. Kısa iniş 1, derin iniş 2 dilim harcar. Gece tören ve sofraya ayrılır; isteğe bağlı 1 bağ sahnesi eklenebilir.
- **Hüner (sosyal statlar):**
  - **Dil:** Başlangıçta sıfırdır. Kademeli çeviri ve yanlış anlama komedisi buradan doğar.
  - **Gönül**, **Maharet** ve **Nam:** Bağ sahnelerini ve diyalog seçeneklerini açar.
- **İşler:** 2–4 dakikalık mini oyunlar: çay demleme ritmi, hamal yük yerleştirme (ganimet paketlemeyi de öğretir), kâtiplik, fırın, kervan muhafızlığı, fener yapımı. Akçe, Hüner ve NPC hikâyeleri kazandırır.
- **Festivaller:** Her mevsim bir festival var. Dilek Gecesi (bahar; dilek ağacı, ateş üstünden atlama), Fener Alayı (yaz; peri bacalarının üstünde balon fenerler), Bağbozumu (sonbahar; Zerrin'in gövde gösterisi) ve Uzun Gece (kış; sabaha kadar hikâye ve nar). Festivalde tezgâh işletme, özel inişler ve seçtiğin kordaşla festival sahnesi var.
- **Borç:** Aylık taksitler Perde 1'in makro hedefidir. Kaçırılırsa oyun bitmez; Zerrin'in "merhamet teklifi" dalı açılır, Sıla'nın Kor'u düşer, kurtarma görevleri gelir.
- **Söylenti:** Hatçe Nine ve çarşı başarılarını abartarak yayar ("Kayıtsız, bir tanrıyı çıplak elle devirmiş"). Yanlış anlaşılma komedisi ve aura tepkileri buradan gelir.
- **Kor ekonomisi:** Ocağın ortak közüdür. Bağlar, festivaller, işler, Nam ve Konuk İyeler besler. Ölümde Eve Dönüş, fincan okumasının derinliği ve yeni Eşik çakmak Kor harcar. Her gün tabandan yenilenir; sosyal içerik bonus verir ama zorunlu grind değildir. Böylece şehir hayatı ile zindan tek bir döngü olur.

### 5.6 Kuyu yapısı: el yapımı ve prosedürel dengesi
- **El yapımı:** Kat temaları, Konak'lar (tüccar, kamp ateşi, yoldaş sahneleri), bekçi arenaları, hikâye katları ve her katın imza mekaniği:
  - 1. Kat: sarnıç sütunları ve yükselen su
  - 2. Kat: ışık tuzu ve mantar ekolojisi
  - 3. Kat: baş aşağı gömülmüş kervansaray (yerçekimi dönüşleri)
  - 4. Kat: Kül Çarşısı · 5. Kat: Kök Denizi · 6. Kat: Yankı Kütüphanesi (unutulmuş adlar) · 7. Kat: Dünya'nın aynası
- **Prosedürel:** Kat başına 40 el yapımı oda parçasından dizilim, düşman karışımları, **Nefes** kuralları, "Taşkın" olayları (irregular), ganimet ve Kıvılcım teklifleri.
- **Kalıcı kısayollar:** Yeni bir Konak'a ulaşınca Sıla oraya Kor ve malzeme karşılığında **Eşik** çakar; sonraki inişler oradan başlar. Hamallar Loncası'na yapılan yatırım ek halat ve asansör açar: şehirdeki yatırım zindanda yol olur.
- **Açgözlülük kararı:** Konak'ta "eve dön" ya da "×1,5 çarpanla derine in". Oya'nın taşıma kapasitesi bu kararı değiştirir.
- **Hatıra Kapısı:** Rütbe atlayınca eski bekçiler isteğe bağlı döner; eski kâbusu tek vuruşta yenmek görünür güç kontrolüdür.

### 5.7 Ölüm ve başarısızlık
- Ölünce Sıla seni en yakın Eşik'ten eve çeker (**Eve Dönüş**). Tortu ve bilgi korunur, kasaya konmamış ganimetin %50'si kaybolur, Kor harcanır. O gece Sıla yorgundur, avuçlarından kıvılcım saçılır; kordaşlar ölüm nedenine özel repliklerle tepki verir (Hades modeli). Defter "Dönüş #n" kaydı düşer.
- Kor sıfırsa Divan şifahanesinde uyanırsın, bir gün kaybedersin ve Sıla bir gün yatağa düşer. Düşen kordaş 1 gün yaralı kalır. Kalıcı kayıp ve kalıcı ölüm yoktur.
- İsteğe bağlı modlar: **Tek Kor** (Eve Dönüş yok, ayrı liderlik tablosu) ve Hades God Mode benzeri **Ocak Desteği** (her ölümde artan direnç).

## 6. İlk 2 Saat

İade penceresi 14 gün ve <2 saattir; EA'da oynanan süre de sayılır. Hizalanmış koşullar: ilk dövüş ≤10. dk, ilk yoldaş 15–30. dk, Uyanış ≤90. dk (03 ve 09).

| Dakika | Olay | Telemetri |
|---|---|---|
| 0–4 | **Son Gün:** Gurbetteki dairede kontrol hemen oyuncuda. Karakter yaratma eşyalarla yapılır: ayna görünüşü, iş kartı eski mesleği, telefon adı belirler. "Son bir saat" seçimi bir Anı Parçası ve pişmanlık görevi tohumu verir. ~3. dk'da Defter'in ilk hata mesajı: "Kayıt bulunamadı." | `ftue_prologue_done` |
| 4–6 | Metro kapısı. Ses önce çınlamaya, sonra sessizliğe döner. "Eve hoş geldin." | — |
| 6–12 | Kuyu 1. Kat'ta uyanış, paslı bir pala, **ilk dövüş** (tortu böcekleri). Hitstop, Defter tıkı, canlı sayan Tortu | `first_combat` |
| 12–28 | **Oya** gelir: sahipsiz bırakılmış bir hamal. Glif altyazılar, jest ve nesneyle kelime öğrenme. Kordaş tekniği eğitimi, ilk 3'lü Kıvılcım, 3 odalık mini iniş. ~25. dk'da Defter "Dil: Başlangıç" verir ve altyazı çözülür | `first_companion`, `lang_lv1` |
| 28–40 | Yüzeye çıkış: Bezirgân'ın alacakaranlıkta vinç çekimi, peri bacalarında fenerler. **Divan kaydı:** Bilge elini kristale koydurur; basılan tezkerede "Kayıtsız, Ocaksız, Nişansız" yazar. Zerrin Ocağı'nın devşiricisi güler | `guild_card` |
| 40–55 | Yağmurda Oya seni Ağız'daki yıkık çayhaneye götürür. Tezgâhta uyuyan kadın uyanır: "Geç kaldın. Seni üç gün önce çağırdım." **Sıla.** Ocağa kabul: berbat kahvesini içersin. **İlk Fincan Töreni:** Tortu statlara mühürlenir, telvede okunamayan bir motif belirir. 1. Kat Nişanı | `hearth_joined`, `first_seal` |
| 55–68 | Ertesi sabah Hatçe Nine ve çay demleme işi (ilk Vakit). Ardından Oya'yla iniş. Sarnıç Bekçisi'ne karşı büyük olasılıkla **ilk ölüm** ve **Eve Dönüş:** Sıla'nın avuçlarından kıvılcımlar, déjà vu replikleri | `first_death`, `first_return` |
| 68–80 | Sıla'nın çaktığı ilk Eşik'ten ikinci deneme. Bekçinin sinyalini öğrenmişsindir (bilgi ekseni) | `first_threshold` |
| 80–90 | **Uyanış:** Dövüşün doruğunda Defter arızalanır ve gizli bir unvan verir: **Eşik Yürüyen**, düşmanın içinden geçen eşik atılması. İlk Ocak Alevi sinematiği ve zafer. O gece fincan çatlar: ilk Derece ve Sıla'nın donan yüzü | `awakening_seen`, `first_rankup` |
| 90–105 | **Dağhan** borç tahsil etmeye gelir, kahveyi tadar ve mutfağa el koyar. Çarşıda **Ren:** "Sen de mi Dünya'dan? Senin çekiliş oranın kaç?" | `rival_met` |
| 105–120 | İlk **Ocak Sofrası** (4 kişi, günün olaylarına tepkili replikler), "Dilek Gecesi'ne 7 gün" afişi, Bölüm 1 bitiş kartı. Sıla ile Oya'nın atıştığı seslendirilmiş "sonraki bölüm" önizlemesi | `ep1_complete` |

Next Fest demosu ilk ~90 dakikadır ve istek listesi çağrısıyla biter.

## 7. Sürükleyicilik Özellikleri

1. **Defter bir karakterdir.** Dünya uzayında ebru hareli, yalnızca senin gördüğün sayfalar. Tasarlanmış, klonsuz bir AI sesiyle (EN/JA/TR) konuşur; soğuk kâtip dilinden sıcaklığa evrilir. Arızaları Sıla'nın sırrına ipucudur. NPC'ler "Yine havayla mı konuşuyorsun?" der.
2. **Fincan Töreni.** Statlar telvede fiziksel şekil olarak belirir. Bütün hanenin fincanı okunur, fal şakaları yapılır. Kısa, atlanabilir ve her gece küçük varyasyonlarla gelir.
3. **Son Gün prologu.** Menü yerine eşyalarla karakter yaratma. Gurbet ve "eve dönememe" duygusu bütün hikâyenin tohumudur.
4. **Eski hayat.** 8 meslek (EA'da 4: aşçı, yazılımcı, sağlıkçı, öğretmen) perk, iş, diyalog ve pişmanlık görevi açar. Yazılımcı Defter'in gizli değerlerini "debug" eder; sağlıkçı sunakta şifacılık işi alır.
5. **Dil edinimi.** Uydurma yazı ve tabelalar kelime öğrendikçe çözülür; atlanabilir, ana görevi kilitlemez.
6. **Eve Dönüş.** Ölümün bedeli Sıla'nın bedeninde görünür. Déjà vu ve ölüm nedenine özel replikler.
7. **Hafızası olan şehir.** 20 isimli NPC'nin (1.0'da 40) günlük programı ve kişisel arkı var; sözlerini, rütbeni ve iyiliklerini hatırlarlar. Karşılığı Perde 3'te gelir: "Şehir hatırlar."
8. **Söylenti ve aura.** Nam yükseldikçe fısıltılar, selamlar ve korkan tüccarlar. Nişan sınavında müfettişin kalemi elinden düşer.
9. **Eski Telefon.** Fotoğraf modu (manga paneli filtresi), günlük, Dünya'dan kalma çalma listesi ve Kuyu kristaliyle şarj edilen pil. Dünya'dan bozuk mesajlar gelir; annenin okunmamış mesajları ayarlardan kapatılabilir.
10. **Dünya'dan ayrılalı N gün.** Gerçek tarih sayacı, isteğe bağlı doğum günü ve mevsim eşlemesi. Hiçbir zaman ceza üretmez.
11. **Ad Verme.** Yenilen Sönük'e yazdığın adla eşik açılır. Zaman durur, vokal girer, Sıla'nın teması Dünya temasıyla birleşir; tanrı ocağına **Konuk İye** olarak yerleşir.
12. **Ocak Sofrası.** Her gece kimin evde olduğuna, günün olaylarına ve bağlara göre seçilen tepkisel sofra sohbetleri.
13. **Görünür dönüşüm.** Çayhane onarıldıkça Ağız mahallesi ışıklar ve müdavimlerle canlanır.
14. **Anime sunumu.** Bölüm başlık kartları, olay günlüğünden şablonla üretilen "önceki bölümde" özeti, sezon başına OP/ED, seslendirilmiş önizlemeler.
15. **Anime dövüş dili.** Hitstop, 2–4 karelik impact frame (flaş azaltma ayarıyla), kordaş cut-in'leri, yerelleştirilmiş onomatope.
16. **Oya'nın hamal haritası.** Elle not ve işaret bırakılır; 1.0 sonrası başka oyuncuların "kayıp ruh" notları eklenir.
17. **Modüler arayüz ve sönen Defter.** Oyuncu HUD parçalarını kaldırabilir. Son dövüşte arayüz hikâye gereği kaybolur ve düşman işaretlerini kordaşlar sesle bildirir.
18. **Gerçek Dünya Görevi (opt-in).** Uzun oturumdan sonra Sıla: "Senin dünyanda da gece oldu. Evine git, uyu."

## 8. Endgame ve Uzun Vadeli Bağlılık

- **Dipsiz:** Yedinci Kat'ın altında sonsuz iniş; her 5 katta yeni bir Nefes kuralı. Kalıcı ve sezonluk liderlik tabloları ayrı tutulur.
- **Ant sistemi:** Ocak başında gönüllü zorluk yeminleri içilir (Hades Heat benzeri). Ödüller kozmetik ve unvandır, güç vermez.
- **Yankı İnişi:** Haftalık sabit tohum ve sunucu tarafında basit doğrulama. Kaçırılan haftanın ödülleri sonradan da kazanılır.
- **Konuk İye koleksiyonu:** 30 tanrı (EA'da 8); her biri hikâye, sunak bonusu ve şehir hizmeti getirir, hiçbiri satılmaz.
- **İkinci Yıl:** Festival takvimi yeni varyasyonlarla döner; bağların "sonrası hikâyeleri" ve mahalle arkları eklenir.
- **Kötü desen yok:** Zorunlu günlük yok, seri cezası yok. Günlük eğitim en fazla 7 gün birikir, geri dönene catch-up verilir, sezon ödülleri kozmetik olarak kalır. Hedef "hiç bırakmasın" değil, "her sezon geri gelsin".

## 9. Monetizasyon

| Faz | İçerik | Fiyat |
|---|---|---|
| EA (Mart–Nisan 2028) | Perde 1, Kat 1–3, tam çekirdek döngü, 4 dil | 19,99 $ |
| Fiyat artışı | 1.0'dan ≥30 gün önce (Steam indirim kuralı) | 24,99 $ |
| 1.0 (2029 1. yarı) | Tam hikâye, 3 son, 7 dil; %10–15 çıkış indirimi | 24,99 $ |
| Destekçi Paketi | OST, dijital artbook, Sıla'nın çini fincan takımı, ebru arayüz teması, kredilerde isim. Oyun avantajı yok | 9,99 $ |
| OST | Steam Soundtrack + Bandcamp | 7,99–9,99 $ |
| Kozmetik DLC | Kordaş kıyafetleri, "Dünya'dan okul üniforması", ocak dekoru, fincan takımları, fotoğraf çerçeveleri. Sabit fiyat, önceden görülür | 2,99–4,99 $ |
| Genişleme (1.0 + 9–15 ay) | Yeni mahalle, Sekizinci Kat arkı, yeni kordaş | 12,99–14,99 $ |
| Sonrası | Complete Edition, konsol, fırsatçı manga ve merch | — |

- Oyun içi mağaza yok; DLC'ler ana menüden Steam'e bağlanır. Rastgele ödül ücretli ürüne bağlanamaz (ADR). Satış pop-up'ı ve "seni özledim" bildirimi yok.
- Romans ve kordaşlar asla satılmaz. Pazarlama cümlesi: "Gacha yok. Enerji yok. Güç satılmıyor. Ocağına sahip çık." Ren'in Lütuf Sistemi bu mesajın oyun içindeki hicvidir.
- Gelir senaryoları (04, 24 ay, vergi öncesi net): kötümser ~49 bin $, temel ~515 bin $, iyimser ~4,3 milyon $. Bütçe kötümser senaryoya göre kurulur; harcamalar istek listesi kapılarına bağlıdır (10 §4.4).

## 10. Sanat Yönü ve Ses Yönü

**Görünüm hedefi:** Güncel TV animesi key visual'ı kalitesinde cel-shaded 3D karakterler ve suluboya dokulu, el boyaması arka planlar. Palet: tüf okrası, kiremit, lapis mavisi, bakır, çini turkuazı. Kuyu'da indikçe renkler soğur; 7. Kat'ta Dünya'nın floresan beyazı belirir.

**Üslup tarifleri** (prompt'larda IP ve sanatçı adı yasak):
- Karakter: temiz ince çizgi, 2 tonlu ramp gölge, SDF yüz gölgesi, saçta ışık halkası, rim light, stencil outline.
- Mekân: peri bacası ve yeraltı şehri mimarisi, kilim ve çini motifleri, bakır fenerler, volumetrik toz.
- Arayüz: ebru hareleri ve geometrik rumi kenarlıklar. Defter pencereleri parşömen-altın ışıktır; arızada ebru dağılır.

**AI hattı:**
- **İnsan finali:** Logo, key art, capsule ve Sıla, oyuncu ile 5 kordaşın final tasarımları insan illüstratörden gelir. AI yalnızca keşif ve varyasyon içindir.
- **Kahramanlar:** VRoid gövde ve yüz → Blender'da özel saç ve kıyafet → VRM 1.0 → Godot'da özel toon shader. Oyuncu avatarı CC0 base mesh üzerine kurulur (VRoid karakter yaratıcı yasağı).
- **Canavar ve prop:** Ücretli bir ayda AI 3D (Tripo/Meshy) ve retopo. Hunyuan, NoobAI ve FLUX [dev] kullanılmaz.
- **Animasyon:** CC0 UAL1/UAL2 ve KayKit temeli; imza hareketler için ücretli bir ay mocap; anime zamanlaması Cascadeur Indie ya da Blender'da yapılır.
- **Diyalog portreleri:** İnsan finali ve AI destekli ifade varyantları. Nefes, göz kırpma ve ağız hareketi Godot Skeleton2D ile yapılır.
- **VFX:** Effekseer ve GDShader.
- **Kayıt:** Her varlık `PROVENANCE.csv`'ye yazılır, çıkış öncesi placeholder taraması yapılır. Steam beyanı somut olur: "Defter sesi, NPC bark'ları ve arka plan varyasyonları AI ile üretildi ve insan tarafından düzenlendi. Key art ve ana kadro sesleri insan eseridir."

**Müzik:**
- Ana tema, leitmotif'ler ve vokalli OP/ED insan besteciden gelir; OST'yi kapsayan telif devri alınır.
- Leitmotif haritası: Sıla (ney ve kanun), Defter (soğuk synth, zamanla ısınır), Dünya (piyano), festival (saz ve darbuka).
- Ortam döngüleri ACE-Step 1.5 (MIT) ya da Lyria ile üretilir ve insan elinden geçer.
- Adaptif yapı Godot'nun `AudioStreamInteractive` ve `AudioStreamSynchronized` sınıflarıyla kurulur. Vokal yalnızca aura anında girer. Uydurma dilde şarkı sözleri, öğrenilen kelimelerle kısmen anlaşılır hâle gelir. OST Content ID'ye kaydedilmez.

**Seslendirme:**
- EA'da insan EN VO: Sıla, Oya, Dağhan, Bilge ve Ren (kilit replikler ve efor sesleri).
- Defter, Gemini Voice Design ya da Chirp 3 HD ile tasarlanmış sentetik bir sestir (EN/JA/TR); kurgu gereği insan değildir ve beyan edilir. NPC bark'ları tasarlanmış AI sesleridir; gerçek kişi klonu yoktur.
- JA insan dublajı G5 kapısından sonra gelir (faz 2). TR altyazı EA'da; TR dublaj pazar karşılık verirse.
- Önce AI ile scratch VO yapılır, satırlar kilitlenince insan kaydına geçilir. Sözleşmelerde AI maddesi bulunur.

## 11. Kapsam

| İçerik | EA | 1.0 |
|---|---|---|
| Şehir | 1 şehir, 3 mahalle (Ağız, Çarşı, Divan Tepesi) + 6 odalı ocak | 5 mahalle (+ Kervan Kapısı, Fener Tarlası) |
| Kuyu | 3 Kat × 8 basamak + 3 Konak + 3 bekçi arenası; 120 oda parçası | 7 Kat (56 basamak), ~280 oda parçası + Dipsiz |
| Düşman | 24 tür + 6 elit + 2 Taşkın olayı | 56 tür + 14 elit + 5 Taşkın |
| Boss | 5 (3 Sönük, Sarnıç Bekçisi, Ren düellosu) | 12 (7 Sönük + Ren, Zerrin'in Eli, Zerrin, Sönük Sıla, Eşik) |
| Silah / Tavır | 3 / 6 | 5 / 15 |
| Yetenek | 18 Nakış, 4 Ocak Alevi, ~60 Kıvılcım, 24 kilim karosu | 48 Nakış, 8 Ocak Alevi, ~150 Kıvılcım, 60 karo |
| Kordaş | Sıla + 3 (bağ rütbesi 1–6) | Sıla + 5 (1–10) + Hatçe Nine |
| NPC / iş / festival | 20 / 5 / 2 | 40 / 8 / 4 |
| Eski meslek / Konuk İye | 4 / 8 | 8 / 30 |
| Diyalog | ~5.000 satır (~60 bin kelime): ~1.200 insan EN VO, ~800 Defter satırı × 3 dil, ~1.000 AI bark | ~15.000 satır (~180 bin kelime): ~4.000 insan EN VO; JA dublaj faz 2 |
| Müzik | 20 parça + OP | 50 parça + 2 OP/ED |
| Oynama süresi | Ana yol 10–12 sa; tamamlama 20–25 sa | Ana yol 35–45 sa; tamamlama 80–100 sa |

**Üretim takvimi (10 raporu temel senaryo):**
- F0 (Ekim–Kasım 2026): iki kamera modunda rendering spike (Sıla test modeli) ve marka taraması.
- F1: gri kutu dövüş, bir oyun günü ve Fincan Töreni.
- Dikey kesit (Nisan 2027): ilk 30 dk ve bir tam gün. "1 basamak = X gün, 1 bağ sahnesi = Y gün" üretim hızı ölçülür.
- Steam sayfası (Nisan–Mayıs 2027), Playtest (Temmuz–Eylül 2027), demo (Kasım–Aralık 2027), Next Fest (Şubat 2028), ardından EA.
- G2'de üretim hızı yetmezse kesme sırası bellidir: önce 3. Kat, sonra bir kordaş EA'dan çıkar.

**En riskli 5 teknik iş:**
1. **Godot'da iki kamera modunda anime görünüm:** ramp, SDF yüz, stencil outline (şeffaf geçiş sıralaması, saç ve yüz kesişimi); Deck'te ≥40 FPS. F0 kapısı; başarısızsa Unity yedeği.
2. **Dövüş hissi ve animasyon hattı:** CC0 ve mocap kliplerinin VRM iskeletlerine BoneMap ile retarget'ı, root motion, çerçeve verili aksiyon durum makinesi, hitstop ve iptal pencereleri. Oyuncunun önüne geçmeyen kordaş yapay zekâsı.
3. **Takvim, hafıza ve tepkisel diyalog:** Bayrak patlaması, Ocak Sofrası replik seçici ve kayıt migrasyonu. CI'da diyalog geçerlilik testleri ve deterministik gün simülasyonu şart.
4. **Prosedürel ve kalıcı Kuyu:** Oda parçası dikişi, Eşik kısayolu ve ganimet durumu, tohumlu Yankı İnişi'nin determinizmi ve basit hile doğrulaması, şehir ile Kuyu arasındaki sahne akışı.
5. **İçerik üretim hızı ve tutarlılık:** Karakter LoRA ve VRoid tutarlılığı, manifest, 60 bin kelimenin JA/ZH LQA'sı, scratch VO'dan insan VO'ya geçiş, Türkçe ek uyumu yardımcıları. Kör testte "AI slop" şikâyeti ≤%10 olmalı.

## 12. Neden Bu Konsept Kazanır / Zayıf Yanları

**Neden kazanır:**
- 02 raporunun boşluğunu en duygusal yerinden vurur: oyuncu bizzat isekai olur ve dünyaya bir **aile** üzerinden bağlanır. Görünür büyüme (Solo Leveling), tanrı-hane ilişkisi (DanMachi), "bağ güçtür" kuralı (Persona) ve "ölüm hikâyedir" döngüsü (Hades) tek bir ekonomide, Kor'da birleşir.
- Görsel kimlik tanınır: Türkiye'de güçlü PR, Japonya ve Çin'de "egzotik fantezi" çekiciliği.
- Kozmetik DLC kurguya doğal olarak uyar (ocak dekoru, fincan takımı, kıyafet). Gacha karşıtlığı hem ilke hem hikâye.

**Zayıf yanları (dürüst):**
- Üç oyunu birden yapıyor: aksiyon, roguelite ve yaşam simülasyonu. Yazım ve sistem yükü en yüksek konsept bu olabilir; tek kişilik ölçekte en büyük risk kapsam.
- Takvim ritmi saf aksiyon oyuncusunu, roguelite ölümleri de hikâye oyuncusunu yorabilir. "Sakin Gün" seçenekleri ve Ocak Desteği bunu hafifletir ama kitle yine bölünebilir.
- İki kamera modu sanat maliyetini artırır; spike başarısızsa şehir de "diorama" kameraya iner.
- Kültürel hassasiyet: Fincan falı bazı muhafazakâr kesimlerce hoş karşılanmaz; İye bir halk inancı kavramıdır. Kurgusal panteon, gerçek dinlere dokunmama ve kültür danışmanı şart.
- Sıla'nın sönmesi kötü yazılırsa manipülatif hissettirir; duygusal yük hak edilmeli.
- Türk kodlu dünya JA/ZH kitlesinde niş algılanabilir; anime sunum diliyle dengelenmeli.
