# Konsept C · DEVRAN: Yeniden, Yeniden Doğmak ("Reenkarnasyon ve Dönüş")

> 2026-09-24 · Açı: **REENKARNASYON VE DÖNÜŞ** (Re:Zero, Mushoku Tensei, Tensura; Solo Leveling, DanMachi ve Hades'ten ödünçler). Dayanak `docs/research/01–10`; [R03] ilgili raporu gösterir. Sayılar **tasarım hedefidir**. Terimler özgündür; başka eserlerin adları, terimleri ve UI'ı kopyalanmaz [R01].

---

## 1. Künye

| Alan | Değer |
|---|---|
| **Çalışma adı** | **DEVRAN** · TR alt başlık *Yeniden, Yeniden Doğmak* · EN *DEVRAN: Born Again, Again* · JA 『デヴラン ―もう一度、生まれ直す―』 · ZH 《轮转：再一次重生》. Yedekler: *MİHENK*, *Sekizinci Kemer*. "Devran" yaygın kelime (ayırt edicilik riski); F0'da sınıf 9/41 marka taraması [R10] |
| **Tür** | Üçüncü şahıs anime aksiyon-RPG: roguelite "Girdap" koşuları, zaman döngülü hikâye "Düğüm"leri, hub şehir, orta oyundan itibaren yerleşim (Yurt) |
| **Platform / motor** | PC (Steam), Steam Deck Verified hedefi; konsol 1.0+12–24 ay (W4 ya da port ortağı). Godot 4.7.2, katı tipli GDScript; ilk 3 haftada "Anime Rendering Spike" kapısı, geçemezse Unity 6.3 LTS (2027'de 6.7 LTS) [R08] |
| **Kamera / perspektif** | Orta mesafeli serbest üçüncü şahıs; yumuşak kilitlenmede omuz üstü; ultimate, Ad Çağrısı ve Dönüş'te sinematik cut-in; hub'da geniş açı |
| **Hedef kitle** | A) 16–34 yaş "Hunter" çekirdeği (aksiyon, aura anları). B) 30+ yaş "ikinci şans" yetişkinleri: inşa ve aile temaları (Japonya'da 35–64 yaş erkeklerde 24 dizinin 21'i isekai). C) Dram, ilişki ve hikâye oyuncuları [R01]. PEGI 12/16, ESRB T |
| **Fiyat** | EA 19,99 $, 1.0 24,99 $ (artış 1.0'dan ≥30 gün önce), bölgesel fiyat. Gacha, loot box, enerji, premium para, güç satışı yok [R04] |
| **Oturum süresi** | **1 oturum = 1 oyun günü:** sabah 3–5 dk, Girdap 15–25 dk, Akşam Mühürü ve Sofra 5–8 dk; toplam 30–45 dk (PC medyanı 32–33 dk [R03]). Düğüm (bölüm) 4–7 saat |
| **Diller** | EA metni EN, TR, JA, ZH-Hans (JA/ZH insan LQA, G4 kapısına bağlı). Ses: ana kadro EN insan; Sistem EN/JA/TR tasarlanmış, beyanlı AI sesi. 1.0: +KO, PT-BR, ES; JA dublaj faz 2 [R07][R10] |
| **Takvim** | Dikey kesit Nisan 2027 → Next Fest Şubat 2028 → EA Mart–Nisan 2028 → 1.0 2029'un ilk yarısı [R10] |

---

## 2. Logline ve "Neden Şimdi / Neden Biz"

**Logline:** *Sel basan bir alt geçitte bir yabancıyı kurtarmak için aynı son dakikayı üç kez yaşar ve ölürsün. Zamanı dev bir su çarkının döndürdüğü Çarkbent'te yeniden doğarsın; 16 yaşında eski hayatın geri gelir. Artık her ölümünde dünya o günün şafağına sarılır: sen her şeyi hatırlarsın, dünya yalnızca hafifçe. Sevdiklerini kurtarmak için aynı günleri yeniden yaşa, dışlanmış canavarlara ve sürgünlere ad ver, onlarla yurdunu kur; sonunda karar ver: devranı döndürmeye devam mı, yoksa zamanı akmaya mı bırakacaksın?*

**Neden şimdi:**
- **Açının üç kaynağı aynı anda gündemde:** Re:Zero S4 (Nisan 2026), Mushoku S3 (Temmuz 2026), Slime S4 (5 cour). Re:Zero S3 2025 ve 2026'da "Best Isekai" aldı; Solo Leveling S3 (2027–28) EA'ya denk [R01].
- **Başarısız olan fantezi değil, lisanslı uygulamalar.** Re:Zero Witch's Re:surrection ~9 ayda kapandı; Mushoku QoM %61, Tensura IC %52 ("şehir kurma yapılacaklar listesi") [R02]. Ortak sorun: oyuncu kendini oynamıyor, oynanış zayıf.
- **Mekaniğin ataları kanıtlı:** Hades II (roguelite + anlatı ödülü, 1.0 öncesi 2 milyon+), Outer Wilds (bilgiyle ilerleme) [R02][R09]. Ama "ölüm bilgi bırakır, dünya hafifçe hatırlar, yurt kalıcıdır" üçlüsünü anime isekai'de sistemik kuran oyun yok (R02 boşluk tablosu).
- **Doğrudan rakip riski düşük:** KARMA roguelite ama F2P, mobil ve önce KR/JP; premium Steam rafında çakışma sınırlı [R02].

**Farklılaştırıcılar:**
1. **Dünya nasıl öldüğünü hatırlar:** seni öldüren saldırılar sonraki denemede ebru hayaletleriyle önceden belirir (Önsezi).
2. **Adlar zamana direnir:** ad verdiğin varlık geri sarılan döngüde de seni tanır.
3. **İki yaşam, iki karakter yaratma:** Dünya'daki yüzün ve 16 yaşındaki yeni yüzün.
4. **Senin dilin gizli bir yazıdır:** önceki Dönenler'in Türkçe, İngilizce ya da Japonca duvar notlarını yalnızca sen okursun.
5. **Ege-Anadolu yüksek fantezisi:** su çarkları, sukemerleri, ebru, rüzgâr gülü; isekai'de neredeyse hiç görülmemiş bir palet [R01].

**Neden biz:** Döngü tasarımı **içerik verimlidir**: aynı gün, farklı bilgiyle yeniden oynandığında da anlamlıdır; içerik başına oynama süresi katlanır. Oyunun kalbi durum, koşul ve diyalog verisi; Claude Code bunları headless Godot'ta "1.000 döngü" simülasyonlarıyla doğrulayabilir [R08]. Anadil Türkçe olduğu için TR yerelleştirmesi ucuz, yerel PR kaldıracı güçlü [R01].

---

## 3. Dünya ve Hikâye Tohumu

### 3.1 Dünya: Devran ve Çarkbent

- **Devran**, zamanın nehir gibi aktığı bir dünya. Nehrin ağzında, kimin kurduğu bilinmeyen 1.000 yıllık **Büyük Çark** döner; halk, çark durursa zamanın da duracağına inanır.
- **Çarkbent**, çarkın çevresindeki baraj ve liman şehri: badanalı taş evler, turkuaz kepenkler, yel değirmenleri, zeytin ve servi. Üstünden sekiz kemerli dev bir sukemeri geçer; efsaneye göre her kemeri bir "Dönen" kurmuştur. Yedisi ayakta, **sekizincisi yıkık**.
- **Girdaplar:** Nehirde açılan zaman burgaçları; içlerinde geçmişin ve olası geleceklerin tortusu birikir (batık çarşı, saat mekanizmalı orman, tuz ve cam mağaraları). Canavarları **Çökeltiler**'dir, "hiç yaşanmamış olayların anıları". Kan değil, parlayan kum saati kumu saçarlar (yaş derecesi ve ZH hassasiyeti için). Kum para birimidir.
- **Mihenkler:** Çarkın parmaklıklarına ve eski taşlara işlenmiş hafıza taşları; dünya kendini bunlara "kaydeder".
- **Gelenler ve Dönenler:** Dünya'dan gelen ruhlar **Gelen**'dir, eski hayatlarını hatırlar; pek azı **Dönen** olur ve ölünce Mihenk'e sarılır. **Dünya Kahvesi**'nde farklı ülke ve dönemlerin Gelenleri kahve, mayonez, radyo icat etmeye çalışır: mizah ve "modern bilgi" görevleri.

### 3.2 Varış: "Son Dakika" ve ikinci doğum

İsimsiz, yağmurlu bir metropol; tabelalar oyunun diline göre değişir (ucuz doku değişimi, her pazarda "benim şehrim" hissi). Karakter yaratma eşyalarla yapılır: iş kartı, ayna, telefondaki son mesajlar [R09]. 23.58'de sel basan bir alt geçitte kırmızı yağmurluklu bir kadın mahsur kalır. Oyuncu onu kurtarırken ölür, **son 60 saniye geri sarılır**, telefonda *"Dönüş 1/3"* yazar. Üçüncü denemede kadın kurtulur, oyuncuyu su alır. Kadının gözlerinde ebru desenleri: *"Sekizinci."* Kamyon klişesi yok; döngü kuralı ilk 5 dakikada oynanarak öğretilir.

Ardından bebek gözünden yeni anne **Meltem** (emekli Kılavuz) ve yabancı bir ninni. **7 yaşında** mahalleye Girdap taşar; çocuk kürekle kız kardeşi **Su**'yu korur (ilk dövüş). **16 yaşında**, Kemer Yaşı sabahı eski hayat tamamen döner; oyuncu nehre bakıp yeni yüzünü seçer.

### 3.3 Ana çatışma

- **Mühürdarlar** (Bent Divanı'nın muhafız tarikatı) Dönenleri avlar: 90 yıl önce bir Dönen'in döngüleri şehrin yarısını sular altında bırakmıştı. Her büyük geri sarma bir **İz** (nehir kokusu) bırakır ve Mühürdarlar onu izler.
- **Durgunlar** Büyük Çark'ı durdurup zamanı "kusursuz bir günde" dondurmak ister. Başlarında **Selvi** var: alt geçitteki kırmızı yağmurluklu kadın, **İlk Dönen**. Yüzyıllardır kızını kurtarmak için aynı yılı yaşıyor; oyuncuyu bu dünyaya o çekti. Ritüeli, Dönen'lerin büyük geri sarmalarıyla beslenir.
- **Sistem'in sırrı:** Ebru desenli arayüzün sesi yedi sesin üst üste binmesidir: önceki yedi Dönen'in tortulaşmış anıları. Sekizinci kemer tamamlanırsa çark serbest kalacağı için sana yardım eder; ama seslerden biri Selvi'nin. Bölüm 1 sonunda senden bir ad ister (varsayılan **"Ebru"**).

### 3.4 Üç perdelik ana hat

| Perde | Özet | Duygusal zirve |
|---|---|---|
| **1. Dönen** (EA) | Döngüler, aile, Lonca, Mühürdar baskısı, ilk ad verme. Durgunlar'ın saldırısında sekizinci kemerin yıkıntısında **Yurt** kurulur; kırmızı yağmurluklu kadının Selvi olduğu anlaşılır | Su'yu kurtarmak için beşinci deneme |
| **2. Yurt** | Yurt büyür, sürgünler ve canavarlar yurttaş olur, Divan'la diplomasi başlar, kemerlerin sırrı açılır. Orta noktada Selvi Mihenk'i kilitler: Tuna ölür ve **geri sarılamaz**; kurtarmak için geçmişe açılan bir Girdap'a inilir | Umutsuzluk, kırılma |
| **3. Devran** | Oyuncunun ulusu Serbest Kemer, fraksiyonlarla Çark için savaşır. Son iniş **"Tek Nefes"**: geri sarma yok, yalnızca bilgi var. Üç son: Çarkı durdur (sonsuz döngü), serbest bırak (zaman akar, güç kaybolur), Dünya'ya dön (alt geçit anı; bu kez ikiniz de yaşarsınız) | "Dönüş mü, kalış mı?" |

### 3.5 Ana yoldaşlar (6)

Romans edilebilenlerin hepsi kanonik olarak yetişkin; rıza açık, "herkes herkesle" tasarımı yok [R09].

| Yoldaş | Rol / silah | Hedef · sır · kusur | Döngüyle ilişkisi | Bağ gücü |
|---|---|---|---|---|
| **Tuna** (K, 19) | Kayıkçı kızı, çocukluk arkadaşı, rehber; sırıkla sıçrama | Kendi teknesiyle denize açılmak · ilk döngülerde üç kez ölür · pervasız iyimserlik | Rüyalarında döngüleri görür | "Akıntı": kusursuz kaçınma Geri Al şarjı verir |
| **Haru** (E, 23) | Japonya'dan gelmiş bir Gelen, Mühürdar çavuşu; zincirli fener | Dönen'leri yakalayıp "felaketi önlemek" · geri sarılamaz, bunu kıskanır · kibir | Yankıları hafifçe görür, şüphelenir | "Fener": Önsezi hayaletlerini 2 sn uzatır |
| **Kerpiç** (adı oyuncu koyar) | Çamurdan Çökelti; kalkan-tank, Yurt'ta inşaatçı | Bir ev · 90 yıl önceki selde boğulan bir çocuğun anısı · huysuz | İlk ad verilen varlık; döngüde de hatırlar | Evrim; savunma ve Ad Çağrısı çekirdeği |
| **Ilgaz** (K, 34) | Mühürdar yüzbaşısı; ağır arbalet, mühür tuzakları | Kardeşini alan felaketin sorumlusunu bulmak · önceki döngülerin "hayalet karelerini" hisseder · katılık | Önce en tehlikeli düşman, sonra kritik müttefik | "Mühür": düşmanlar için zamanı yavaşlatır |
| **Firuz** (E, 27) | Gezgin âşık; sazla ritim tabanlı destek | Dönen'lerin destanını bitirmek · Durgun muhbiri, taraf değiştirir · kompulsif yalancı | Lore'u uydurma dilde şarkılarla taşır | Ritim buff'ları, Rüzgâr yeniden çekme |
| **Nar Hatun** (K, ~40 görünümlü) | Yılan soyundan sürgünlerin şifacı önderi (Anadolu halk anlatılarından özgün yorum); zehir ve şifa | Soyunu avcılardan korumak · soyu bütün Dönen'lerin anılarını miras alır · alaycılık | Perde 2'de Yurt'un veziri | Şifahane, iyileştirme ağacı |

### 3.6 Fraksiyonlar ve düşmanlar

- **Kılavuzlar Loncası:** Girdap dalgıçları; F→S rütbeler (Tayfa'dan Efsane'ye denizci unvanları), rütbe sınavları, Kum ekonomisi.
- **Bent Divanı ve Mühürdarlar:** Şehri ve su haklarını yöneten oligarşi ve Dönen avcıları; Şüphe/İz baskısı, pusular, mahkeme Düğüm'ü.
- **Rüzgâr Evleri:** Değirmen ve tüccar klanları; ticaret, fiyatlar, Yurt'un tanınması.
- **Kıyıdışılar:** Sazlıktaki sürgünler ve ad almamış canavarlar; Yurt'un yurttaş havuzu.
- **Durgunlar:** Selvi'nin tarikatı; suikastlar, Girdap taşkınları, boss'lar.
- **Çökeltiler:** Biyoma göre ekolojisi değişen Girdap canavarları; 6 aile (Silt, Mercan, Cam, Çark, Pus, Tuz).

---

## 4. Tasarım Sütunları

1. **Ölüm öğretir.** Her ölüm bilgi, Tortu ve hikâye kırıntısı bırakır; öğrenilen hiçbir şey kaybolmaz [R03].
2. **Dünya hatırlar, ama hafifçe.** Döngüler arası sistemik kalıntı: Yankı, Şüphe, İz, Mühür. Her sistem "geri sarınca ne kaldı?" sorusuna cevap vermeli.
3. **İkinci hayat bir kez yaşanır.** Eski hayat mekanik ve duygusal fark yaratır: Anı Defteri, aile, pişmanlık görevleri [R01 P1].
4. **Her dövüş bir anime kesiti.** Okunabilir, hızlı ve şık bir dövüş: hitstop, impact frame, Geri Al ve Önsezi [R09].
5. **Kurduğun yurt, verdiğin ad.** Kurulan aile yurda, yurt ulusa dönüşür; bağlar güçtür ama oyun şehir simülatörü olmaz [R01].

**Koruyucu kural:** Döngünün temposunu oyuncu belirler; gerçek zamanlı baskı, seri cezası ve FOMO yok [R03].

---

## 5. Oyun Döngüleri ve Sistemler

### 5.1 Katmanlı döngü

| Katman | Süre | Eylem | Ödül |
|---|---|---|---|
| **Saniye** | 0,3–5 sn | Kombo, kaçınma, savuşturma, Geri Al | Hitstop, impact frame, Sistem çınlaması |
| **Dakika** | 1–5 dk | Girdap odası | 3'lü **Rüzgâr** (koşu içi güçlendirme), ganimet |
| **Oturum (Gün)** | 30–45 dk | Sabah → Girdap → Akşam Mühürü → Sofra | Status mühürleme, bağ sahnesi |
| **Düğüm (bölüm)** | 4–7 sa | 3–7 günlük, son tarihli kriz; döngülerle çözülür | Rütbe sınavı, yoldaş/yurttaş, "sonraki bölüm" |
| **Hafta** | 7 gün | İsteğe bağlı Sabah Talimi, haftalık **Aynı Gün** | Kozmetik, unvan, liderlik tablosu |
| **Sezon** | 12 hafta | Ücretsiz "Devir Mevsimi" | Yeni ark, Girdap tipi, OP/ED |

**Dönem ritmi:** **Düğüm dönemlerinde** takvim ve son tarih var (Re:Zero gerilimi). **Serbest Dönemler**de son tarih yok: sınırsız Girdap, Yurt, bağ sahneleri. Sonraki Düğüm'ü oyuncu başlatır; günler yalnızca uyuyunca ilerler.

### 5.2 Zamanın kuralları: üç kalıcılık katmanı

| Katman | Ne tutar | Ne zaman sıfırlanır |
|---|---|---|
| **Hafıza** (oyuncuda) | Keşif Defteri, boss desenleri, açılmış diyalog seçenekleri, tarifler, Önsezi verisi | Hiçbir zaman |
| **Tortu** (dünyada, hafif) | Meta para birimi; NPC'lerin déjà vu bayrakları; güven değerinin %30'u; ad verilmiş varlıkların hatırası | Hiçbir zaman (birikir) |
| **Mühür** (kesinleşmiş gerçeklik) | Yurt binaları, fraksiyon durumları, kurtarılan karakterler, Status | Son Mihenk'ten sonrası geri sarılır |

- **Küçük Dönüş:** Girdap'ta ölürsen **o günün şafağına** dönersin; mühürlenmemiş ganimet kaybolur, ham deneyimin yarısı Tortu olur. Tekrar yaşanan sabah **"Aynı sabahı atla"** ile 10 saniyede geçilir.
- **Büyük Dönüş:** Düğüm'ün felaket saati dolarsa **Düğüm'ün ilk şafağına** dönersin. Bedeli: bir Emanet Anı "sisler" (§5.4) ve **İz** artar (Mühürdar pusuları sıklaşır).
- **Söyleyemezsin:** Döngüyü anlatmaya çalışırsan mürekkep ağzını mühürler; bilgiyi dolaylı kullanmalısın. Aşırı "geleceği bilmek" **Şüphe**'yi doldurur ("Bunu nereden biliyorsun?").
- **Adlar zamana direnir:** Başarısız döngüde ad verdiğin yurttaş, sonraki döngüde anında geri gelir: *"Adımı sen vermiştin."*

### 5.3 Dövüş sistemi

Gamepad öncelikli, tam klavye-fare desteği. Mantık sabit 60 Hz; her aksiyon startup/active/recovery verili bir `ActionData` kaynağı [R08].

| Girdi | İşlev |
|---|---|
| Hafif / Ağır | Silah başına 4–5 vuruşluk kombo, 3 dallanma; şarjlı ağır saldırı dengeyi kırar |
| **Kaçınma** | 0,2 sn i-frame; **kusursuz kaçınma** 0,5 sn "Akış" yavaşlaması ve karşı saldırı açar |
| **Savuşturma** | 8 karelik pencere; kusursuzu Denge barını kırıp sersemletir |
| **Geri Al** | Son 1,5 sn'yi (konum, can, durum) geri sarar; hasardan sonraki 0,6 sn içinde basılırsa hasar da silinir. 1 Devir şarjı (başta 1, en fazla 3); boss faz geçişleri geri alınamaz |
| Anı Teknikleri (4 slot) | Silaha ve eski mesleğe bağlı yetenekler |
| Ad Çağrısı (ultimate) | Ad verdiğin 1–3 yurttaş savaşa iner: oyunun "aura anı" |
| Bağ Tekniği | Aktif yoldaşa komut ya da ikinci yoldaşın destek hamlesi |

- **Önsezi (imza mekanik):** Seni daha önce öldüren saldırılar sonraki denemede 0,4 sn önceden ebru hayaletiyle belirir (boss başına en fazla 3; "Ayak Taşı" ile kapatılır). Ölüm ders olur, zorluk tavanı korunur.
- **Silahlar (EA'da 3):** **Gönder** (sırık-mızrak: menzil, süpürme, sıçrama), **Çift Kanca** (hızlı; çekme, tutunma), **Çapa** (ağır; zincirle fırlatıp çekme, yere çarpma). 1.0: **Ebru Fırçası** (menzilli mürekkep büyüsü), **Zincirli Fener**.
- **Anime hissi:** 3–8 kare hitstop, 2–4 kare impact frame (flaş azaltmalı), cut-in'ler, dile göre yerelleşen onomatopeler ("ŞAK!", "ドン") [R06][R09].

### 5.4 İlerleme

- **Status:** Güç, Çeviklik, Dayanım, Akıl, Sezgi (Önsezi ve ganimeti etkiler). Deneyim gün boyu "ham" birikir, akşam Meltem'in su aynası ritüeliyle (Perde 2'den itibaren Yurt Mihenk'inde) **mühürlenir**; eşiklerde yeni hareket açılır [R01].
- **Rütbe F→S:** Düğüm sonundaki **Rütbe Sınavı** boss'uyla atlanır, Girdap kademelerini (I–VII) açar. Seviye ölçekleme yok; eski içerik kolaylaşır, **Hatıra Rövanşı**'nda eski kâbus tek vuruşta düşer [R03].
- **Yetenek ağaçları (3):** **Kılavuz** (silah ustalığı), **Devir** (Geri Al şarjları, Önsezi, kısa zaman durdurma), **Yurt** (Ad Çağrısı ve yoldaş ortak ultimate'leri).
- **Anı Defteri (Emanet Anılar):** 6 yuva (meslek, hobi, pişmanlık, "son saat"). Her anı bir perk, diyalog seçenekleri ve Yurt'ta bir **Dünya Bilgisi** icadı verir. Büyük Dönüş bir anıyı "sisler", perk zayıflar; **Hatırlama** göreviyle (annenin yemeğini yoldaşlarla pişirmek gibi) geri gelir, hatta güçlenir. Bedel kalıcı güç kaybı değil, içeriktir. 1.0'da 8 meslek: aşçı, yazılımcı, sağlıkçı, öğretmen, mühendis, sporcu, kurye, "oyuncu" [R09].
- **Tortu → Devir Çarkı:** 8 kol × 5 düğüm meta ağaç (+1 Geri Al şarjı, yeniden çekme, şişe yuvası, başlangıç güçlendirmesi).
- **Ekipman:** 1 silah, 3 zırh, 2 **Nazarlık** (düşman ailesine karşı koruma). Zanaat deterministik: Çökelti parçaları, sonucu önceden görünen **Ebru Deseni** yuvalarına işlenir (Last Epoch tipi). Rastgele ganimet yalnızca oynayarak kazanılır, kötü şans korumalıdır [R03][R04].

### 5.5 Yoldaş ve parti sistemi

- Girdap'a **1 aktif yoldaş** (AI) ve **1 destek yoldaşı** (bekleme süreli Bağ Tekniği); kapsam bilinçli olarak dar.
- **Bağ seviyesi 1–5:** her seviye mekanik bir yetenek açar (Persona modeli); 5'te ortak ultimate cut-in'i [R09].
- Sofra'da ikili sohbetler; her büyük karara en az bir yoldaş tepkisi; eski hayata tepki ("Aşçı mıydın? O çorbayı yap").
- **Ölüm riski yalnızca Düğüm içinde;** kalıcı ölüm yalnızca isteğe bağlı "Tek Hayat" modunda.

### 5.6 Şehir ve yaşam katmanı: Çarkbent ve Yurt

- **Çarkbent (EA'da 4 mahalle):** Kemeraltı (Lonca, çarşı, Dünya Kahvesi), Değirmen Sırtı (ev, aile), Mühürhane, Sazlık Kıyısı (Yurt'a geçiş); sade NPC rutinleri ve söylenti panosu.
- **Sofra:** İsteğe bağlı akşam yemeği; eski hayattan bir tarif buff verir ve bağ sohbetini açar.
- **Yurt (Perde 1 sonunda):** Sekizinci kemerin yıkıntısında, adını oyuncunun verdiği yerleşim.
  - **Sabit parseller**, serbest şehir kurma yok (EA 6, 1.0 16): Ocak, Tersane-Demirci, Şifahane, Değirmen, Ebru Atölyesi, Nöbet Kulesi.
  - **Adlılar:** 1 meslek ve 1 savaş rolü; bağ olaylarıyla **Ad Derinliği** artar, evrimleşirler (2 görsel form).
  - Üretim oyuncu yokken sürer ama üst sınırlıdır; "toplamazsan çürür" yok.
  - **Dünya Bilgisi icatları** (sabun, dişli su çarkı, pusula-saat) şehre yayılır: fiyatlar, afişler, NPC replikleri değişir [R02].
  - **Taşkın:** Planlı, tekrarlanabilir savunma olayları; Girdap Yurt'a taşar, yurttaşlarla savunursun.
  - Akşam başına **3–8 dakikalık** hafif menü; "yapılacaklar listesi" hatasına düşmemek için her yapının savaşta ya da hikâyede görünür karşılığı olmalı [R02].

### 5.7 Girdap yapısı: prosedürel ve el yapımı dengesi

- **Girdap = 3 katman × 4–6 oda + ara boss + boss.** Katman aralarındaki **Kıyı** güvenli odasında **Şişeye Koy** kararı: ganimeti şişeyle eve yolla ya da ×1,5 çarpanla derine in (extraction-lite) [R03 §6].
- **El yapımı:** biyom teması, oda parçaları, set-piece'ler, boss'lar, Düğüm Girdapları. **Prosedürel:** oda dizilimi, düşman karışımı, "Ters Akıntı" elit olayları, Rüzgâr havuzu. Kurgusal gerekçe: zaman tortusu her girişte yeniden dizilir.
- Her biyomun bir mekaniği var: Batık Çarşı'da gelgit, Saat Ormanı'nda dönen platformlar, Tuz Mağaraları'nda yansıyan ışınlar.
- **Rüzgârlar** (5 aile): **Poyraz** (dondurma), **Lodos** (yanma), **Karayel** (itme, kritik), **İmbat** (kalkan, iyileşme), **Gündoğusu** (hız, yeniden çekme).

### 5.8 Ölüm ve başarısızlık tasarımı

- Her Dönüş'te atlanabilir **ebru girdabı sinematiği** ve **"Döngü #n"** sayacı; ölüm nedenine özel Sistem, yoldaş ya da aile replikleri (Hades modeli, ~600 replik) [R03].
- **Asla kaybolmaz:** Hafıza, Tortu, mühürlü Status, adlar. **Kaybolur:** mühürlenmemiş ganimet ve o günün olayları.
- **Kilitlenme önleyici:** Aynı Düğüm'de 3 Büyük Dönüş'ten sonra Sistem, Keşif Defteri bağlantılarını ipucu olarak önerir. **"Sistem Desteği"** modu her ölümde %2 hasar direnci ekler (en fazla %80); başarımlar ayrı işaretlenir, oyuncu utandırılmaz [R03].

---

## 6. İlk 2 Saat (Steam iade penceresi: 14 gün ve <2 saat; EA'da oynanan süre de sayılır) [R03][R09]

| Dakika | Olay | Hedef his | Telemetri |
|---|---|---|---|
| 0–3 | **Son Dakika:** daire, eşyalarla karakter yaratma, "son saatini ne yaparsın" (ilk Emanet Anı, pişmanlık) | "Bu benim hayatım" | `ftue_prologue_done` |
| 3–6 | Alt geçit: ölüm, **ilk Sistem hatası "Dönüş 1/3"**, iki geri sarma, kurtarma, "Sekizinci" | Şok; "bilgi kalır" | `earth_loop_done` |
| 6–8 | Doğum (ninni, uydurma dilde altyazı), 7 yaş vinyeti | Merak | — |
| 8–12 | **İlk dövüş:** çocuk kürekle Su'yu korur (*"Önceki hayattan refleks aktarıldı"*), Meltem Çapa'yla gelir | "Dövüş iyi" | `first_combat` |
| 12–14 | Zaman atlaması ve **OP jeneriği**, "Bölüm 1: İkinci Kez Doğmak" (atlanabilir) | Anime hissi | — |
| 14–24 | 16. yaş, nehirde ikinci yüz; **Tuna katılır** (rehber); Dünya Kahvesi'nde kendi dilinde duvar notu | "Yabancıyım ama yalnız değilim" | `first_companion`, `secret_script_seen` |
| 24–34 | **Lonca kaydı:** su aynası bozulur, "ölçülemez"; rütbe **F (Tayfa)**, fiziksel Status kartı; Ilgaz "nem kokusu" alır | Küçük düşürülme, gizem | `guild_card`, `suspicion_seed` |
| 34–48 | **İlk Girdap** (Batık Çarşı): ilk Rüzgâr seçimi, ilk seviye, Şişeye Koy | Yetkinlik, özerklik | `first_girdap` |
| 48–58 | D0 "Tuna'nın Üçüncü Günü": limanda **Kör Dümenci**; **ilk ölüm** (büyük olasılıkla) | "Haksızlık!" | `first_boss`, `first_death` |
| 58–74 | **İlk Dönüş:** şafak, déjà vu, Önsezi hayaletleri; bilgiyi dolaylı kullanma (*mürekkep ağzını mühürler*), rövanş | "Anladım" | `first_return`, `onsezi_seen` |
| 74–82 | **İlk Akşam Mühürü:** Meltem'in ritüeli, Status sıçraması; Sofra'da eski hayattan tarif | Sıcaklık, büyüme | `first_seal` |
| 82–90 | **Uyanış olayı:** Durgun baskını, Tuna'ya ölümcül darbe; **Geri Al** uyanır, gizli sınıf "Dönen" açılır; Kör Dümenci'nin gölgesi vokal müzikle tek vuruşta düşer (**Hatıra Rövanşı**) | "Bende bir şey var" | `awakening_seen` |
| 90–105 | Sukemerinde kırmızı yağmurluklu siluet: *"Hoş geldin, Sekizinci."* Haru'yla tanışma, sekizinci kemerde ışık (Yurt habercisi), Kerpiç peşinden gelir | Gizem, rekabet | `rival_met` |
| 105–120 | Sistem ad ister (**Ebru**); isteğe bağlı bir Girdap; **ED** ve Tuna ile Sistem'in **"Sonraki bölüm"** önizlemesi | "Bir bölüm daha" | `system_named`, `ep1_complete` |

Vaadin tamamı (reenkarnasyon, döngü, dövüş, Sistem, aile, aura anı, gizem, Yurt habercisi) 90. dakikadan önce teslim edilir; Next Fest demosu bu ilk 90–120 dakikadır [R10].

---

## 7. Sürükleyicilik Özellikleri (16)

1. **Sistem = karakter (Ebru):** Soğuk bildirimlerle başlar, kişilik kazanır; arızaları gizemin ipuçlarıdır; yedi katmanlı sesi yavaşça teke iner; adını oyuncu verir [R09 #1].
2. **Diegetik ebru arayüzü:** Paneller dünyada, su yüzeyinde yüzer; bildirimde yüzey dalgalanır. Solo Leveling'in mavi pencerelerine benzemez [R01 §9].
3. **Son Dakika:** Dünya'da oynanan mini döngü; eşyalarla karakter yaratma, dile göre yerelleşen tabelalar.
4. **İkinci yüz:** 16 yaşında nehir aynasında ikinci karakter yaratma. Avatar CC0 base mesh üzerine kurulur, çünkü VRoid lisansı oyun içi editörü yasaklıyor [R06].
5. **Anı Defteri:** Meslek, hobi ve pişmanlık perk, diyalog ve göreve dönüşür; sislenen anılar Hatırlama görevleriyle döner.
6. **Önsezi (Yankı hayaletleri):** Dünya seni nasıl öldürdüğünü hatırlar.
7. **Déjà vu hafızası:** NPC'ler olay bayraklarıyla "seni tanıyor gibiyim" der; güvenin %30'u döngüler arasında taşınır. LLM değil, yazılı ve seslendirilmiş replikler (K1) [R09 §7.6].
8. **Söyleyemezsin ve Şüphe:** Mürekkep ağzını mühürler; geleceği bilmek sosyal bir risktir.
9. **İz:** Büyük geri sarmalar Mühürdarlar'ın izlediği bir nehir kokusu bırakır; pusu ve gizlenme olayları doğar.
10. **Gizli yazı:** Oyuncunun gerçek dili bu dünyada bir şifredir: önceki Dönenler'in duvar notları, Dünya Kahvesi menüsü, lore avı.
11. **Akşam Mühürü ve Sofra:** Aile ritüeli ve Dünya tarifleri; merkeze dönüş ceza değil ödül sahnesidir [R03].
12. **Dönüş sinematiği ve "Döngü #n":** Ebru girdabı, ters çalan ney ve saz; tanınır bir marka sesi.
13. **Adlar zamana direnir:** Oyuncunun yazdığı ad kurgusal otorite kazanır; yurttaş döngüler arasında seni tanır.
14. **Gerçek zaman (isteğe bağlı):** "Son gecenden bu yana N gün" sayacı, yıldönümü anma sahnesi, "Uyku da bir Mihenk'tir" hatırlatması; hiçbiri cezalandırmaz [R09].
15. **Anime sunumu:** Bölüm kartları, OP/ED, olay günlüğünden "Önceki bölümde…", seslendirilmiş "Sonraki bölüm" [R01].
16. **Su Aynası foto modu** (yansımadan kadraj, manga paneli filtresi), yayıncı modu ve P0 erişilebilirlik: flaş azaltma, tuş atama, altyazı ayarları, ekran okuyucu (AccessKit) [R09].

Kritik yolda canlı LLM yok; replik varyasyonları geliştirmede üretilir, insan editörden geçer ve "önceden üretilmiş" olarak beyan edilir [R09][R10].

---

## 8. Endgame ve Uzun Vadeli Bağlılık (karanlık desen olmadan)

- **Dipsiz Burgaç:** Sonsuz Girdap, her 10 katta yeni kural; sezonluk ve kalıcı tablolar ayrı. Çıkışta hazır olacak (MH Wilds dersi) [R03].
- **Ayak Taşları:** Gönüllü zorluk (Heat tipi). "Düşman da hatırlar" taşıyla boss'lar desenlerine uyum sağlar. Ödül kozmetik ve unvan, güç değil.
- **Aynı Gün:** Her hafta herkes aynı seed'li günü yaşar; başkalarının ölüm yerleri **ebru lekeleri** olarak görünür. Katılmayana ceza yok.
- **Yeni Devir (NG+):** 9. Dönen olarak yeniden başlarsın; Anı Defteri ve Tortu'nun bir kısmı taşınır, NPC'ler önceki devri hatırlar, Düğüm'ler karışır, yeni sonlar açılır. İçerik yeniden kullanıldığı için ucuzdur.
- **Serbest Kemer:** Yurt 5. seviyede ulus olur; diplomasi ve son savaştaki fraksiyon desteği buradan gelir.
- **Devir Mevsimi:** 12 haftada bir ücretsiz güncelleme (Düğüm, Girdap tipi, yurttaşlar, OP), 4–6 haftada bir yama. Hedef **"her sezon geri gelsin"** [R03].
- **Koruyucu kurallar:** İsteğe bağlı 5–10 dk Sabah Talimi, kaçırılan günler 7 güne kadar birikir; seri cezası, "seni özledim" bildirimi ve çürüme yok; geç kalana yetişme bonusu; kozmetikler rotasyonla döner.

---

## 9. Monetizasyon (EA → 1.0 → DLC)

| Faz | Ürün | Fiyat |
|---|---|---|
| Duyurudan itibaren | Ücretsiz demo (ilk 90–120 dk), Next Fest Şubat 2028 | 0 |
| **EA** (Mart–Nisan 2028) | Perde 1, tam çekirdek döngü, Dipsiz Burgaç | **19,99 $** |
| 1.0'dan ≥30 gün önce | Fiyat artışı (1.0'da %10–15 çıkış indirimi mümkün kalır) | → 24,99 $ |
| **1.0** (2029 1. yarı) | Tam hikâye, 3 son, Yeni Devir | **24,99 $** |
| 1.0 ile | **Destekçi Paketi:** OST, artbook, 3 kozmetik set, 2 ebru arayüz paleti, kredilerde isim; oyun avantajı yok | 9,99 $ |
| 1.0 ile | **OST** (Steam, Bandcamp; Content ID kaydı yok) | 7,99–9,99 $ |
| 1.0 + 2–9 ay | Kozmetik DLC: kıyafetler ("Dünya'dan okul forması"), Yurt süsleri, ebru arayüz desenleri; önceden görülür, rastgele değil | 2,99–4,99 $ |
| 1.0 + 9–15 ay | **Genişleme "Karşı Kıyı":** yeni bölge, Düğüm arkı, 1 yoldaş, 1 silah | 12,99–14,99 $ |
| Sonra | Complete Edition; konsol (W4 veya port ortağı); fırsat çıkarsa mobil premium, manga ve merch | — |

- **Kurallar:** Oyun içi mağaza yok; DLC'ler ana menüden Steam'e bağlanır; fiyatlar gerçek parayla; ücretli rastgelelik, premium para, enerji ve güç satışı yok (kod düzeyinde ADR) [R04].
- **Beklenti (24 ay, vergi öncesi net) [R04]:** kötümser ~49 bin $ (5 bin kopya), temel ~515 bin $ (50 bin), iyimser ~4,3 milyon $ (400 bin). Bütçe kötümser senaryoya göre; harcamalar istek listesi kapılarına (G2–G5) bağlı [R10].

---

## 10. Sanat Yönü ve Ses Yönü

### 10.1 Görsel hedef

- **Karakterler:** 3D cel-shading: iki tonlu ramp, SDF yüz gölgesi, stencil outline (gerekirse ters kabuk), saçta "angel ring", rim light, spring bone. Hareket 60 fps, kilit pozlar 2'ler ve 3'lerle "limited animation" [R06][R08].
- **Dünya:** Suluboya dokulu boyanmış gökler; palet Ege turkuazı, badana beyazı, nar kırmızısı, servi yeşili; zaman öğeleri ebru mermer dokusunda. Dinî sembol yok, kültür danışmanı görüşü alınır [R09].
- **Üslup tarifi** (prompt'ta IP ya da sanatçı adı yasak): *"Yüksek kontrastlı cel-shading, iki tonlu gölge, incelip kalınlaşan kontur, suluboya zemin, ebru dokusu, eğik kamera."*

### 10.2 AI destekli üretim hattı

1. **Stil bible'ı ve karakter sayfaları:** Nano Banana Pro/2 (Vertex, 300 $ kredi) ya da yerel Animagine XL 4.0 / Illustrious v1.x. **NoobAI, FLUX [dev] ve Hunyuan yasak** [R05].
2. **İnsan eli:** Key art, logo, capsule ve 6 yoldaşın son tasarımları (telif koruması ve "AI slop" riski) [R10].
3. **3D:** Kahramanlar VRoid gövdesi + Blender'da (VRM Add-on) özel saç ve kıyafet → VRM 1.0 → godot-vrm. Canavar ve prop'lar: bir aylık ücretli Meshy/Tripo sprint'i ve TripoSR; retopo Instant Meshes ile [R06].
4. **Animasyon:** CC0 UAL1/2 ve KayKit temel seti; imza hareketler Rokoko/DeepMotion ücretli planı + Cascadeur Indie ya da Blender'da anime zamanlaması [R06].
5. **VFX:** Effekseer ve GDShader; ebru girdabı tek bir yeniden kullanılabilir shader.
6. **Kayıt:** bpy + Godot headless "asset fabrikası", her varlığa `PROVENANCE.csv`, çıkış öncesi placeholder taraması (E33 dersi); AI beyanı pazarlamayı da kapsar [R02][R10].

### 10.3 Ses ve seslendirme

- **İnsan ses (EN):** yoldaşlar (EA'da 4, 1.0'da 6), Meltem, Selvi; kahramanın efor sesleri ve ~150 kilit repliği (2 ses seçeneği). Sözleşmelerde AI maddesi: klonlama ve model eğitimi yasak [R07].
- **Sistem Ebru:** Voice Design ile tasarlanmış ses (Gemini TTS ya da VoxCPM2), klon değil; EN/JA/TR, yedi katmanlı işleme. Kurgusal olarak meşru ve beyanlı [R07][R09].
- **NPC bark'ları** Voice Design AI sesi. **JA dublaj** G5 kapısından sonra; TR'de önce altyazı ve TR Sistem sesi. Kayıttan önce AI geçici ses (scratch VO) [R07].
- **Müzik:** Ana tema "Devran" (uydurma dilde vokalli OP) ve 6 leitmotif insan besteci işi; varyasyonlar ACE-Step 1.5 (MIT) ya da Lyria + insan düzenlemesi. Adaptif müzik `AudioStreamInteractive` ve `AudioStreamSynchronized` ile; vokal yalnızca aura anlarında [R07].
- **Marka sesleri:** Sistem çınlaması ve Dönüş motifi (ters ney ve saz, su damlası).

---

## 11. Kapsam

### 11.1 İçerik sayıları

| Kalem | **EA** | **1.0** |
|---|---|---|
| Hub / bölge | Çarkbent (4 mahalle) ve Yurt (seviye 1–2) | 6 mahalle, Yurt (seviye 5), Karşı Kıyı (DLC) |
| Girdap biyomu | 3 (Batık Çarşı, Tuz ve Cam Mağaraları, Saat Ormanı) | 6 |
| Oda parçası | 72 (biyom başına 24) ve 6 set-piece | 150 |
| Düğüm (bölüm) | 5 (D0 eğitim, Çamurun Adı, Değirmen Yangını, Mühürhane, Sekizinci Kemer) | 14 |
| Düşman tipi | 18 ve 6 elit varyant | 40 ve 12 elit |
| Ara boss / boss | 3 / 4 (Rütbe Sınavı dahil) | 8 / 11 (Selvi dahil) |
| Silah | 3 | 5 |
| Yetenek | 24 aktif, 36 pasif, 30 Rüzgâr, 40 Devir Çarkı düğümü | 45 aktif, 70 pasif, 60 Rüzgâr |
| Yoldaş | 4 tam (Tuna, Haru, Kerpiç, Ilgaz) ve Firuz NPC olarak | 6 tam |
| Adlı yurttaş | 8 | 24 |
| Eski meslek | 6 | 8 |
| Metin | ~70 bin kelime (EN) | ~160 bin kelime |
| Seslendirilmiş replik | 2.200 insan (EN), Sistem 1.500×3 dil, 2.000 AI bark | 6.000 insan (EN; JA faz 2), Sistem 3.500×3 dil |
| Oynama süresi | 10–15 sa ana içerik ve sonsuz mod | 30–40 sa, NG+ ve sonsuz mod |

Kapsam kuralı: G2'de ölçülen üretim hızı ("1 oda parçası = X gün") yetmezse önce biyom ve yurttaş, en son Düğüm sayısı kesilir [R10].

### 11.2 En riskli 5 teknik iş

1. **Godot'da anime görünümü:** SDF yüz, stencil outline'ın şeffaf geçiş sıralaması ve saç-yüz kesişimi, ebru shader'ı, Deck'te ≥40 fps. Rendering Spike kapısı; gerekirse Unity [R08].
2. **Döngü ve dünya durumu mimarisi:** Hafıza/Tortu/Mühür katmanlarının JSON anlık görüntüleri ve diff'leri, Mihenk'e geri sarma, döngüler arası NPC bayrakları, kayıt migrasyonu. Kombinasyon patlamasına karşı veri güdümlü durum makineleri ve headless "1.000 döngü" fuzz testi.
3. **Geri Al ve Önsezi:** 90 karelik halka tampon (dönüşüm, animasyon durumu, can, efektler), hitstop ve AI uzlaşması, deterministik 60 Hz; öldüren saldırıların kaydedilip hayalete dönüştürülmesi.
4. **Prosedürel Girdap:** El yapımı parçalardan birleştirme, navmesh, karşılaşma bütçesi, set-piece garantisi; Deck'te ≤25 animasyonlu düşman [R08 §8].
5. **Tepkisel anlatı ve yerelleştirme:** Döngüye duyarlı diyalog koşulları (Dialogue Manager), 4 dil, CJK fontları, **oyuncunun koyduğu adlarda Türkçe ek uyumu** (Kerpiç'e / Ebru'ya), ses satırı yönetimi [R09 §8.7].

---

## 12. Neden Bu Konsept Kazanır / Zayıf Yanları (dürüst)

**Neden kazanır:**
- Açı, 2026'nın en güçlü isekai sinyallerine ve kanıtlanmış formüllere (Hades II, Outer Wilds) oturuyor.
- **Klip dostu:** ebru geri sarma, Önsezi hayaletleri, "adımı sen vermiştin", Tek Nefes finali; kısa videoda keşfedilmeye hazır anlar [R10].
- **İçerik verimliliği:** Döngüler içeriği anlamlı biçimde yeniden kullanır.
- **Etik model satış argümanıdır:** gacha yok, FOMO yok, çevrimdışı [R04].
- TR anadili ve Ege-Anadolu kimliği yerel PR kaldıracı; "senin dilin gizli yazı" fikri her pazarda merak uyandırır.

**Zayıf yanları:**
- **Aynı günleri yaşamak bıktırabilir.** "Aynı sabahı atla", kısa Düğüm'ler, Serbest Dönemler şart; dikey kesitte ölçülmeli.
- **Üç katmanlı kalıcılığı anlatmak zor.** İlk saatte yalnızca "bilgi kalır, gün geri sarılır"; gerisi kademeli.
- **Kapsam gerilimi:** Aksiyon, döngü anlatısı ve Yurt bir arada; Yurt EA'da ince.
- **Re:Zero karşılaştırması kaçınılmaz.** Hukuki risk düşük, algı riski var; pazarlama "dünyanın seni hatırladığı oyun" diye yapılmalı.
- **Hassas temalar:** Sel ve boğulma (Türkiye'de yaşanmış afetler), ölüm, kayıp; grafik olmayan sunum ve uyarı metni şart.
- **Motor riski:** Godot'da anime kalitesi kanıtlanmadı; geçiş ancak kapı erken konursa ucuz.
- **AI damgası:** Anime kitlesi hassas; insan eliyle key art, şeffaf beyan ve kayıt disiplini şart [R02][R10].
