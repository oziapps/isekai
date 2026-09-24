# 03 — Oynanış Döngüleri, Bağlılık ve Elde Tutma Tasarımı (Etik ama Etkili)

> Hazırlanma: 2026-09-24 · Yöntem: 24 hedefli WebSearch. Oturumun ortak arama bütçesi bu raporun ortasında doldu. WebFetch ile Steam, SteamSpy, GameAnalytics ve Wikipedia'ya doğrudan erişim egress proxy tarafından engellendi. Sayılar arama özetlerinden ve bu özetlerin işaret ettiği birincil/ikincil kaynaklardan alındı.
> Güven notasyonu: **[Y]** yüksek (hakemli makale, resmî kurum veya şirket sayfası), **[O]** orta (saygın sektör basını, rapor özetleri), **[D]** düşük (ikincil blog, tek kaynak ya da arama özetinin belirsiz olduğu durum). Köşeli parantezdeki sayılar `## Kaynaklar` listesine referanstır.
> **"Hedef"** diye işaretlenen değerler bizim tasarım hedeflerimizdir, olgu değildir. Oyun terimleri (P1–P10 sütunları, Gate, Status mühürleme vb.) 01 numaralı raporla uyumludur.

## Özet

- **PC ile mobil farklı platformlar.** GameAnalytics'in 2026 raporuna göre PC "alışkanlıkla değil derinlikle" oynanıyor. Oyuncular ayda daha az gün geliyor ama daha uzun kalıyor. PC'de medyan günlük oyun süresi 32–33 dk, üst %25'te 70 dk, üst %10'da 120 dk [3][4]. Mobilde medyan günlük süre 22 dk, medyan oturum 5–6 dk [1][2]. **Sonuç:** Çekirdek oturumumuz 30–45 dk olmalı ve doğal durma noktaları içermeli.
- **Elde tutma çok zor.** Mobilde medyan D7 %3,4–3,9. Projelerin %75'inin D28 değeri %3'ün altında [1][2]. PC'de üst %25'in D1 değeri yalnızca %15–16 [4]. Premium PC oyununda belirleyici eşik **Steam iade kuralı**: satın almadan sonra 14 gün içinde ve 2 saatten az oynanmışsa iade mümkün [7]. Bu yüzden oyunun vaadinin tamamı **ilk 2 saatte** hissedilmeli.
- **En sağlam teorik temel Self-Determination Theory (SDT).** Özerklik, yetkinlik ve ilişkililik ihtiyaçları oyundan alınan keyfi ve oyuna geri dönmeyi **birbirinden bağımsız olarak** öngörüyor [8]. Her sistem bu üç ihtiyaçtan en az birine hizmet etmeli.
- **"Bir tur daha" hissi iki kanıtlı mekanizmaya dayanıyor.** Birincisi goal-gradient: insanlar ödüle yaklaştıkça daha çok çaba harcıyor [11]. İkincisi Ovsiankina etkisi: yarım kalan işe geri dönme eğilimi. Popüler "Zeigarnik etkisi"nin hafıza tarafı (yarım işi daha iyi hatırlamak) 2025 meta-analizinde **doğrulanmadı**. Geri dönme eğilimi ise doğrulandı [12]. Bu yüzden tasarımı "unutturmama" hilelerine değil, **"kaldığın yerden kolayca devam et"** ilkesine kurmalıyız.
- **Hades modeli başarısızlığı anlatıyla ödüllendiriyor.** Oyunda yaklaşık 21.000 seslendirilmiş replik ve 300 bin kelime var. Oyunu 20 kişiden küçük bir ekip yaptı [20]. Tek bir yan karakterin (Hypnos) ölüm nedenine özel 75 repliği var [20]. Bu yaklaşım isekai'deki "ölüm bilgi bırakır" (Re:Zero, P4) sütunuyla birebir örtüşüyor.
- **Kaliteli roguelite'lar çok satıyor.** Hades II 1.0 (25 Eylül 2025) Steam'de 112.947 eşzamanlı oyuncuya ulaştı. Bu, ilk oyunun 54.240'lık zirvesinin iki katı [22]. Balatro çıkışından (20.02.2024) yaklaşık 11 ay sonra 5 milyon satışa ulaştı [23].
- **Endgame'i zayıf çıkmak ölümcül olabiliyor.** Monster Hunter Wilds'ın Steam'deki eşzamanlı oyuncu sayısı 1,38 milyondan birkaç ay içinde zirvenin yaklaşık %1'ine düştü. Başlıca şikâyetler performans ve zayıf endgame [25].
- **Sezon dalgaları normal.** PoE2'de lig başlangıcından sonraki aylarda %60–70'lik aylık düşüşler tekrar tekrar görülüyor [27]. Diablo IV yılda 2 sezondan 5 sezona çıktı [26]. **Sonuç:** Hedef "oyuncu hiç bırakmasın" değil, **"her sezon geri gelsin"** olmalı.
- **Değişken ödül güçlü bir araç, ama gerçek parayla birleşince hukuki ve etik mayına dönüşüyor.** Loot box harcaması ile problem kumar arasındaki meta-analitik korelasyon r = .27 [13]. FTC, HoYoverse'e 20 milyon $ ceza verdi ve 16 yaş altına ebeveyn onayı olmadan satışı yasakladı [15]. Epic Games dark pattern'ler için 245 milyon $ ödedi [16]. Brezilya 17 Mart 2026'dan itibaren reşit olmayanlara ücretli loot box'ı yasakladı [19]. AB'nin CPC ilkeleri (21 Mart 2025) fiyatların gerçek parayla gösterilmesini istiyor [17]. AB'nin Digital Fairness Act önerisinin 2026'nın ikinci yarısında gelmesi bekleniyor [18].
- **Önerilen mimari 6 katmanlı:**
  1. Saniye: dövüş hissi
  2. Dakika: oda/kat ve güçlendirme seçimi
  3. Oturum: Gate veya iniş koşusu, ardından şehirde "Status mühürleme" töreni
  4. Bölüm: 5–15 saatlik anime bölümü ve rank sınavı
  5. Hafta: isteğe bağlı eğitim ve haftalık Anomali Gate
  6. Sezon: 8–12 haftalık "anime sezonu" güncellemesi
- **Güç eğrisi üç eksenli olmalı:** kalıcı istatistik, koşu veya sezon build'i ve **oyuncunun öğrendiği bilgi**. Bunlara düzenli "eski kâbusuna geri dönüp tek vuruşta yenme" anları eklenmeli. Solo Leveling hissini bu anlar veriyor.
- **Temel kural:** Rastgelelik yalnızca oynayarak kazanılan ödüllerde olur. Gerçek parayla satılan her şey deterministiktir (ne alacağın bellidir) ve kozmetik ya da içeriktir. Aşağıda 22 somut mekanik ve 14 kırmızı çizgi var.

---

## 1. Kıyas Verileri (Benchmark)

### 1.1 Elde tutma ve oturum süreleri

| Metrik | Değer | Kapsam | Kaynak | Güven |
|---|---|---|---|---|
| Mobil D1 (üst %25) | %26,5–27,7. iOS üst %25: %31–33, Android: %25–27 | 2024 sonu, 11.600 mobil oyun, 16 tür | [1][2] | O |
| Mobil D7 | Medyan %3,42–3,94 (2023'te %4–5). Üst %25: %7–8. Alt %25: ~%1,5 | 2024 | [1][2] | O |
| Mobil D28 | Projelerin %75'i %3'ün altında | 2024 | [1][2] | O |
| Mobil günlük oyun süresi | Medyan 22 dk | 2024 | [1][2] | O |
| Mobil oturum uzunluğu | Medyan 5–6 dk. Üst %25: 8–9 dk | 2024 | [1][2] | O |
| Tür farkı (mobil) | RPG, strateji ve simülasyon yavaş başlayıp uzun kuyruk yapıyor. Aksiyonda D30 ~%2,1, hiper-casual'da ~%1,4 | 2025 | [6] | D |
| PC D1 | Üst %25: %15–16. Üst %1: %50–60. Medyan (P50) ~%7, alt %25 ~%3 (eklendi 24.09.2026). Örneklem: en az 100 MAU'lu 3.582 PC oyunu | 2025 | [3][4][5] | O |
| PC D7 | Medyan ~%1,7–1,8 (arama özetinde mobil ve PC verisi karışık, dikkatli kullanılmalı) | 2025 | [4] | D |
| PC günlük oyun süresi | Medyan 32–33 dk. Üst %25: 70 dk. Üst %10: 120 dk | 2025 | [3][4] | O |
| Steam iade kuralı | Satın almadan sonra 14 gün içinde **ve** 2 saatten az oynama. 23 Nisan 2024'ten beri Early Access ve Advanced Access'te oynanan süre de 2 saate sayılıyor (eklendi 24.09.2026) | Güncel politika | [7] | Y |

**Yorum:**
- GameAnalytics verisi SDK'yı entegre eden projelerden geliyor ve bunların çoğu küçük ve orta ölçekli. Premium Steam oyunlarını tam temsil etmeyebilir. Bu bizim değerlendirmemiz, kaynakta yazmıyor.
- Premium bir PC oyununda D1/D7 yerine şu KPI'lar daha anlamlı:
  1. İade oranı
  2. 2. saate ulaşan oyuncu oranı
  3. İlk "bölümü" bitirme oranı
  4. Medyan toplam oynama süresi
  5. Steam inceleme puanı
  6. Her içerik güncellemesinden sonra geri dönen oyuncu oranı
- Bu KPI'lar için sektör ortalamalarına ulaşılamadı (**doğrulanamadı**).
- **Steam'de başarılı roguelite ve ARPG'lerin medyan oynama süresi:** SteamSpy ve Steam API'ye erişilemediği, arama sonuçları da sayı vermediği için **doğrulanamadı**. Tek bulunan ikincil tahmin şu: Hades II'de tüm içerik, başarımlar ve hikâye varyasyonları için yaklaşık 65 saat, odaklı bir oynanış için yaklaşık 35 saat [31] (**[D]**). Bu değerler hedef belirlerken yalnızca kaba bir çapa olarak kullanılmalı.

### 1.2 Vaka verileri

| Oyun | Veri | Ders | Kaynak | Güven |
|---|---|---|---|---|
| Hades II | 1.0 çıkışı 25.09.2025. Steam zirvesi 112.947 eşzamanlı oyuncu (28.09.2025). İlk oyunun zirvesi 54.240. Üçüncü taraf tahmini: Steam'de ~5,2 milyon kopya ve ~93,5 milyon $ (Raijin; iki değer birbiriyle tutarsız, resmî rakam yok. Doğrulanmış alt sınır: 1.0 öncesi 2 milyon+; düzeltildi 24.09.2026) | Erken erişim, anlatı ödülü ve meta ilerleme birlikte çok güçlü bir satış motoru | [22] | O (satış: D) |
| Balatro | Çıkış 20.02.2024. 5 milyon satış açıklaması 21.01.2025 | Tek mekaniğin derinliği ve kısa koşular | [23] | Y |
| Monster Hunter Wilds | Eşzamanlı oyuncu 1,38 milyondan (1.384.608, 1 Mart 2025) Haziran 2025'te zirvenin ~%1–2'sine indi. Satışlar da aynı eğriyi izledi: ilk ayda 10 milyon, sonraki 12 ayda (FY2026) yalnızca 1,32 milyon (eklendi 24.09.2026). Forbes başlığına göre son incelemelerin %82'si olumsuz | Endgame ve performans çıkışta hazır olmalı | [25] | O |
| Path of Exile 2 | Erken erişim zirvesi 578.569 (08.12.2024). 0.4 ligi ~240 bin. Lig başlangıcından sonraki aylarda %60–70 düşüş | Sezon dalgası doğal, planlanmalı | [27] | O |
| Diablo IV | Yılda 2 sezondan (2023) 5 sezona (2025). Sezon süreleri 48–105 gün arasında değişti. Liderlik tabloları 2026 yol haritasında | Daha sık sezon = daha fazla içerik yükü ve yorgunluk riski | [26] | D |
| Last Epoch | Season 2 (Nisan 2025) güçlü bir geri dönüş yarattı | Her sezonda anlamlı bir yenilik geri getiriyor | [28] | O |
| Persona 3 Reload | İlk haftada 1 milyon. Haziran 2026'da 3 milyonu aştı | Takvim, sosyal bağlar ve zindan birlikte çalışıyor | [29] | Y |
| Stardew Valley | Aralık 2024 itibarıyla 41 milyondan fazla (26 milyondan fazlası PC) | Rahat döngü ve ilişki sistemi on yıla yakın satıyor | [30] | Y |

---

## 2. Oyuncu Psikolojisi: Ne Kullanıyoruz, Nasıl, Hangi Sınırla

| İlke | Kanıt | Oyunumuzda uygulama | Etik sınır |
|---|---|---|---|
| **SDT: Yetkinlik** | Oyun içinde algılanan yetkinlik, keyfi ve oyunun iyi oluşa etkisini öngörüyor [8] | Okunabilir düşman tell'leri, net hasar geri bildirimi. Ölümden sonra "neden öldün" özeti gösteren Sistem penceresi | Zorluk yapay olarak şişirilip "kolaylaştırıcı" satılmaz |
| **SDT: Özerklik** | Özerklik keyfi ve gelecekte oynamayı ayrı ayrı öngörüyor [8] | Build seçimi. Hangi Gate'e gideceğine oyuncu karar verir. Patron tanrı seçimi, rota seçimi | Zorunlu günlük görevler özerkliği zedeler, isteğe bağlı olmalı |
| **SDT: İlişkililik** | Çok oyunculu oyuncularda ilişkililik ayrı bir öngörücü [8] (Çalışma 4) | Yoldaş bağları, Familia/lonca, eşzamansız paylaşım (hayalet koşular) | Sosyal baskı yok: lonca cezası, "arkadaşını hayal kırıklığına uğrattın" yok |
| **Flow** | Beceri ile zorluk dengelenmeli. Chen'e göre dinamik zorluk ayarı (DDA), oyuncunun seçimleriyle bilinçaltından yapılabilir [9][10] | Yemin/Heat tipi gönüllü zorluk sözleşmeleri. Hades'in God Mode'u gibi bir erişilebilirlik modu (%20 hasar direnci, her ölümde +%2, en fazla %80) [21] | Gizli DDA ile ödül manipülasyonu yapılmaz. DDA yalnızca zorluğa dokunur, düşme oranlarına dokunmaz |
| **Goal-gradient** | Kahve kartında ödüle yaklaşan müşteri daha sık alışveriş yapıyor. "Yanıltıcı ilerleme" (önceden damgalı kart) de çabayı hızlandırıyor [11] | Koşu sonu ekranında "sonraki kilit %87". Status mühürleme töreninde bir sonraki eşiğin gösterilmesi. Koleksiyon sayaçları | İlerleme çubukları dürüst olur. Parayla hızlandırma "son %10'da" satılmaz |
| **Ovsiankina (devam etme eğilimi)** | 2025 meta-analizi: yarım kalan işi hatırlama avantajı yok (oran ≈0,99), ama sürdürme eğilimi var [12] | Oturum bir "sonraki bölüm önizlemesi" ile kapanır. Kayıt noktası net olur. Tek tuşla "kaldığın yerden devam et" | Oyuncunun çıkışı engellenmez. Çıkış ekranında suçluluk metni yok |
| **Değişken oranlı ödül** | Kumar psikolojisinin çekirdeği. Vampire Survivors'ın sandık açma sunumu slot makinesi estetiğinden esinlendi [24] | Loot drop'ları, nadir "Irregular" olaylar, gizli sınıf keşfi. Bunlar oynayarak kazanılır ve "kötü şans koruması" vardır | **Gerçek para ile asla birleşmez** (bkz. §11). Loot box ile problem kumar arasında r = .27 [13] |
| **Anlatı ödülü** | Hades, ölümleri reaktif diyalogla ödüllendiriyor [20] | Her ölümden sonra Sistem'den, yoldaştan veya tanrıdan ölüme özel bir replik ve yeni bir hikâye kırıntısı | Yok (saf pozitif) |
| **Koleksiyon ve tamamlama** | Koleksiyonu tamamlama isteği güçlü bir motivasyon (bu raporda genel bilgi, sayısal kanıt aranmadı) | Bestiary, gölge ordusu (01 raporu satır 7), tarif ve harita kodeksi | Koleksiyon parçaları paralı rastgele paketlerle satılmaz |
| **Sosyal kanıt** | Topluluk keşfi ve wiki kültürü (01 raporu satır 8, 31) | "İlk keşfeden" unvanı, haftalık seed'li Gate liderlik tablosu | Sahte sosyal kanıt yok ("şu an 5.000 kişi aldı" gibi) |

**Önemli not:** Vampire Survivors'ın geliştiricisi Luca Galante kumar sektöründe çalışmış. Ancak kendi ifadesine göre oyun tasarımında değil, sistem tarafında çalışmış [24]. Oyunun sandık sunumu gerçek para içermediği için bir "juice" örneği olarak kabul edilebilir. Aynı sunumu **paralı** bir sisteme bağlamak ise kırmızı çizgidir.

---

## 3. Referans Oyunlardan Döngü Dersleri

Aşağıdaki tasarım betimlemeleri yaygın bilinen mekanikler. Sayı içermeyenler bu raporda ayrıca kaynakla doğrulanmadı.

| Oyun | Çekirdek döngü | "Yapışkanlık" mekanizması | Bizim için ders |
|---|---|---|---|
| **Hades / Hades II** | Koşu → rastgele boon seçimi → ölüm veya zafer → evde meta harcama ve diyalog | Ölüm = yeni hikâye. God Mode [21]. Heat/Pact (gönüllü zorluk) | Hub'a dönüş bir ceza değil, **ödül sahnesi** olmalı. Bizde bu şehirdeki Status töreni |
| **Dead Cells** | Koşu → kalıcı kilitler ("hücre" harcama) → yeni rota ve silahlar | Metroidvania kısayolları. Bir sonraki biyomu merak ettirme | Kalıcı kısayollar ve yeni rotalar keşif hissini canlı tutar |
| **Vampire Survivors** | Yaklaşık 30 dk'lık koşu → seviye atlama seçimi → sandık → meta altın | Güç fantezisinin ekranı doldurması, sandık sunumu [24] | "Aura anı"nın görsel doruğu. Sürüleri bir anda silme hissi |
| **Balatro** | Kısa el ve blind turları → joker sinerjileri → ante artışı | Kombinasyon keşfi. "Bir el daha" | Az sayıda ama birbiriyle çarpışan kural içeren build sistemi |
| **Diablo IV** | Zindan → loot → Paragon/Aspect → sezon mekaniği | Sezon mekaniği, Pit/Helltide, sezon yolculuğu | Sezonluk "tema mekaniği" ekleme modeli. Yorgunluk riski [26] |
| **Path of Exile 2** | Harita/Atlas → para birimi ekonomisi → craft | Derin pasif ağaç, lig sıfırlaması | Derinlik çekirdek kitleyi tutar, ama ilk saatlerde karmaşıklık gizlenmeli |
| **Last Epoch** | Monolith echo'ları → her yeteneğin kendi uzmanlık ağacı → deterministik craft | Craft güvenilirliği, loot filtresi | **Deterministik craft** oyuncunun zamanına saygı gösterir. Bizde "ruh taşı damıtma" |
| **Monster Hunter** | Av → parça toplama → silah/zırh craft → daha büyük av | Desen öğrenme ve "bir av daha" | İyi bir çekirdek, ince bir endgame'i kurtarmıyor [25] |
| **Persona (Tartarus / Mementos)** | Takvim → gündüz sosyal bağ → gece zindan | Confidant'lar dövüş ve füzyon avantajı veriyor. P5R'de 23 confidant var [29] | Sosyal bağ **mekanik güç** vermeli (01 raporu satır 11). Tekdüze kat dizaynından (Tartarus eleştirisi) kaçınılmalı |
| **Etrian Odyssey** | Katman katman labirent → harita çizme → FOE'lar (dolaşan güçlü düşmanlar) | Oyuncunun kendi haritasını çizmesi | "Kendi haritanı yap" bir sahiplenme mekaniğine dönüşebilir |
| **Genshin / Zelda** | Açık dünya merakı: tepeden görünen işaretler, bulmacalar, sandıklar | Görsel "merak işaretleri" | Açık dünya yerine **yoğun hub + Gate dünyası**. Tek kişilik geliştirici için ölçek riski |
| **Palworld / Enshrouded** | Keşif → yaratık veya zanaatkâr toplama → üs inşa ve otomasyon | Üs, oyuncu yokken de "çalışıyor" | Tensura tipi ulus kurma: isim verilen canavarlar kasabada meslek edinir (01 raporu satır 22–23) |
| **Stardew Valley** | Gün döngüsü → çiftlik → hediye ve kalp seviyeleri | Rahat ritim, sabırla gelişen ilişki | Savaş dışı "nefes alma" katmanı: yemek, bahçe, yoldaşlarla akşam yemeği sahneleri |
| **Solo Leveling: ARISE** (02 raporundan) | Gacha ve story stage'ler | IP gücüyle hızlı zirve, ardından hızlı düşüş | Mağaza ve ara sahne çakışması sürükleyiciliği öldürür (02 raporu) |

---

## 4. Güç Eğrisi: En Zayıftan En Güçlüye

### 4.1 Üç eksenli büyüme

1. **Kalıcı güç (vertical):** Seviye, istatistik ve Status mühürleme. Daima görünür ve geri alınamaz. P2 sütununa hizmet eder.
2. **Build gücü (horizontal):** Koşu içi Sistem önerileri ve sezonluk ekipman. Çeşitlilik ve yeniden oynanabilirlik sağlar.
3. **Bilgi gücü:** Boss desenleri, gizli sınıf koşulları ve ölüm döngüsünün öğrettikleri. P4 ve P9 sütunlarına hizmet eder. Hiçbir zaman satılamaz. Bu yüzden "hak edilmiş" hissi en güçlü olan eksen.

### 4.2 Aşamalar (hedef süreler, olgu değil)

| Aşama | Süre (hedef) | Oyuncu hissi | Tasarım aracı |
|---|---|---|---|
| **"En zayıf"** | 0–60 dk | Aşağılanma ve kırılganlık | F-rank damgası. İlk boss'ta kaybetmek neredeyse kaçınılmaz ama anlatıyla ödüllendirilir |
| **Uyanış** | 60–120 dk | "Bende bir şey var" | Gizli Sistem'in açılması, ilk "Aura anı" sinematiği. **İade penceresi kapanmadan** gerçekleşir [7] |
| **Yükseliş** | 2–20 saat | Her oturumda daha güçlü | Rank sınavları (E→D→C). Her 20–40 dk'da bir güç sıçraması (hedef) |
| **Aura** | 20–60 saat | Dünya bana tepki veriyor | NPC tepki sistemi. Eski bölgelere dönüp eski boss'u tek vuruşta yenme ("güç kontrolü") |
| **Hükümdar** | 60 saat ve sonrası | Ustalık ve ifade | Sonsuz Derinlik, Yemin sözleşmeleri, sezon ligleri, ulus yönetimi |

### 4.3 Kurallar

- **Görünür sıçramalar:** Düz bir %2'lik artış yerine, eşiklerde nitel değişiklikler (yeni hareket, yeni aura, yeni yoldaş formu). Solo Leveling'in "yeniden değerlendirme" anları buna örnek.
- **Geriye dönük tatmin:** Her yeni rank'ta, önceki rank'ın en zor düşmanı haritada isteğe bağlı bir "hatıra Gate'i" olarak yeniden belirir. Oyuncu farkı hisseder.
- **Seviye ölçeklemesi yok, rank ölçeklemesi var:** Dünya oyuncuyla birlikte güçlenmez. Gate rank'ları (E–S) zorluk bantlarını belirler. Oyuncunun güçlendiğini hissetmesi için eski içeriğin kolaylaşması şart.
- **Güç enflasyonunu sezonla yönetme:** Kalıcı karakter ("Ebedî") ile sezonluk karakter ("Sezon Avcısı") birbirinden ayrılır. Sezon güç sistemleri sezon sonunda Ebedî karaktere **kozmetik ve koleksiyon** olarak geçer, güç olarak geçmez. Bu model Diablo ve PoE'nin sezon/lig yapısından uyarlandı.

---

## 5. Önerilen Katmanlı Döngü Mimarisi

```
SEZON (8–12 hf) ── "Anime Sezonu N": yeni ark, yeni Gate tipi, sezon mekaniği, lig
  └─ HAFTA ─────── Haftalık Anomali Gate (sabit seed + liderlik tablosu), dünya olayı
      └─ BÖLÜM (5–15 sa) ── Hikâye arkı, rank sınavı, yeni bölge, bağ arkı, kasaba tier'ı
          └─ OTURUM (30–45 dk) ── Gate/iniş koşusu → çıkış → Status mühürleme → harca → sahne
              └─ DAKİKA (1–5 dk) ── Oda/kat karşılaşması → 3'lü Sistem önerisi → loot
                  └─ SANİYE (0,3–5 sn) ── Kaçın/parry/beceri/kritik → hit-stop + Sistem sesi
```

| Katman | Süre | Oyuncu eylemi | Ödül | İhtiyaç (SDT) / Sütun | Ölçülecek KPI |
|---|---|---|---|---|---|
| **Saniye** | 0,3–5 sn | Kaçınma, parry, beceri kombosu | Hit-stop, kamera sarsıntısı, Sistem "ding"i, hasar sayıları | Yetkinlik / P2, P8 | Ölüm başına süre, parry başarı oranı |
| **Dakika** | 1–5 dk | Oda veya kat temizleme | 3'lü Sistem önerisi (boon benzeri), loot, kat ilerlemesi | Özerklik / P9 | Seçim dağılımı (ölü seçenek var mı?) |
| **Oturum** | 30–45 dk (hedef, PC medyanı 32–33 dk [3]) | Gate'e gir → güvenli katta "çık ya da derine in" kararı → çıkış | **Status mühürleme töreni** (ham XP'nin istatistiğe dönüşmesi), kasabaya malzeme, hikâye sahnesi | Yetkinlik ve ilişkililik / P2, P5, P10 | Oturum sonu "devam" oranı, oturum uzunluğu dağılımı |
| **Bölüm** | 5–15 saat | Hikâye arkı, rank sınavı boss'u, yeni bölge | Rank atlama sinematiği, yeni yoldaş, kasaba tier'ı, "sonraki bölüm" önizlemesi | Hepsi / P1, P3, P8, P10 | Bölüm bitirme oranı (her bölüm ayrı bir huni) |
| **Hafta** | 7 gün | İsteğe bağlı günlük eğitim (5–10 dk), haftalık Anomali Gate | Birikebilir haftalık ödüller, liderlik sırası, kozmetik unvan | Yetkinlik ve ilişkililik / P2, P6 | Haftalık aktif oyuncu, Anomali katılımı |
| **Sezon** | 8–12 hafta | Yeni ark, sezon mekaniği, lig | Yeni hikâye, sezon yolculuğu (ücretsiz), isteğe bağlı kozmetik pass | Özerklik / P6, P10 | Sezon başında geri dönen eski oyuncu oranı |
| **Yıl** | 12 ay | Ücretli genişleme ("Sezon 2" arkı, yeni bölge veya sınıf) | Yeni fantezi katmanı (ör. ulus → krallık) | Hepsi | Genişleme bağlanma oranı |

**Ritim ilkesi:** Her katmanın sonu bir üst katmanın ilerleme çubuğunu doldurur (goal-gradient [11]). Oturum sonu her zaman bir **doğal durma noktası** sunar: şehre dönüş, tören, "sonraki bölüm" kartı. Oyuncu burada ya huzurla çıkar ya da "bir Gate daha" der. Oyunu kapatmak bir kayıp gibi hissettirilmez.

---

## 6. Zindan ve Kat Yapısı (DanMachi × Tartarus × Etrian)

- **Dikey mega-zindan ("Derinlik"):** 10 katlık katmanlar. Her 10 katta bir **güvenli kat-kasaba** var: tüccar, kamp ateşi, yoldaş sahneleri. DanMachi'deki güvenli kat kasabalarından esinlendi (01 raporu satır 12).
- **Kısayollar:** Katman boss'u yenilince açılan "geçit taşı" ile sonraki girişlerde o katmandan başlanır. Dead Cells ve Metroidvania kısayol hissi buradan gelir.
- **Açgözlülük kararı (extraction-lite):** Güvenli katta seçim yapılır. "Kasaya koy ve dön" ya da "×1,5 çarpanla derine in". Ölümde yalnızca **kasaya konmamış** ganimetin bir kısmı kaybolur. Kalıcı ilerleme (XP ve bilgi) kaybolmaz. P4 sütunu (gerçek risk) ile oyuncunun emeğine saygı arasındaki dengeyi bu sağlar.
- **Katmanların el yapımı iskeleti, prosedürel içi:** Katman temaları, set-piece'ler ve boss'lar el yapımı olur. Oda dizilimi, düşman karışımları ve Irregular olaylar prosedürel olur. Persona 3'teki Tartarus'un tekdüzelik eleştirisinden (genel bilgi) kaçınmak için her katmanda en az bir benzersiz mekanik (su baskını, karanlık, yerçekimi vb.) bulunmalı.
- **Harita sahiplenmesi:** Etrian'dan esinle oyuncu haritaya not ve işaret bırakabilir. Bu notlar isteğe bağlı olarak arkadaşlarla paylaşılabilir (eşzamansız ilişkililik).
- **Yüzey Gate'leri (Solo Leveling):** Şehir haritasında zamanlayıcılı ve rank'lı Gate'ler açılır. Temizlenmeyen Gate "dungeon break" olayına dönüşür (01 raporu satır 4). Bu, Derinlik'in yanında ikinci, kısa oturumluk (10–20 dk) içerik kaynağıdır.

---

## 7. İlk Deneyim (FTUE): İlk 5 / 15 / 60 / 120 Dakika

Steam iade kuralı (<2 saat, 14 gün) [7] nedeniyle **ilk 2 saat ürünün kendisidir**. Aşağıdaki süreler bizim hedeflerimiz.

> **Hizalama notu (24.09.2026):** 09 raporunun ilk sürümündeki "ilk 120 dakika" senaryosu bu tabloyla çelişiyordu (ilk dövüş 65. dk, Uyanış 105–120. dk). 09 raporu §3 bu tabloya göre düzeltildi: ilk dövüş ≤10. dk, ilk yoldaş (yerli rehber) 15–30. dk, Lonca kaydı/F-rank 30–45. dk, ilk boss ve ölüm 45–65. dk, Uyanış 80–90. dk. İki rapor arasındaki kalan fark (bu tablo F-rank damgasını 5–15. dakikaya koyuyor, 09 ise dil ve kayıt sahneleri nedeniyle 30–45. dakikaya) dikey dilim testinde ölçülerek kapatılmalı. Değişmez koşullar: ilk dövüş ilk 10 dakikada, Uyanış 90. dakikadan önce.

| Zaman | Olması gereken | Neden |
|---|---|---|
| **0–1 dk** | Kontrol oyuncuda. "Son Gün" prologu (01 raporu): Dünya'daki son an, oynanabilir. Uzun logo ve ara sahne yok | Yetkinlik hissi hemen başlamalı |
| **1–5 dk** | Varış, ilk Sistem penceresi (seslendirilmiş), ilk düşman, hit-stop ve "ding". Eski hayat anketi (P1) 3 soru, ayrıntılısı sonra | "Bu oyunun dövüşü iyi" yargısı ilk 5 dk'da oluşur |
| **5–15 dk** | İlk mini-Gate, ilk 3'lü Sistem önerisi, ilk seviye atlama, ilk yoldaşla tanışma. **F-rank damgası** ile aşağılanma sahnesi | Build özerkliğini tanıtır. Duygusal kanca: "en zayıf" |
| **15–60 dk** | İlk boss'ta muhtemel ölüm, ardından anlatı ödülü (özel replik) [20]. Şehre dönüş, ilk Status mühürleme töreni, ilk kasaba yapısı | "Ölüm = ilerleme" sözleşmesi öğretilir. Hub bir ödül sahnesi olur |
| **60–120 dk** | **Uyanış olayı:** gizli Sistem sınıfı, ilk "Aura anı" sinematiği, eski boss'a rövanş ve zafer. Meta katmanların (bağlar, kasaba, Gate haritası) önizlemesi. Bölüm 1 bitişi ve "Sonraki bölüm" önizlemesi | İade penceresi kapanmadan ana vaat teslim edilir. Ovsiankina kancası kurulur [12] |

**Onboarding kuralları:**
- Bir seferde tek yeni sistem.
- Menü öğretisi yerine oynayarak öğretme.
- Karmaşık sistemler (craft, ulus, lig) 3. saatten sonra açılır. PoE2'nin derinliği çekirdek kitleyi tutar, ama yeni oyuncuyu ilk saatlerde boğmamalı.
- Her adım telemetriyle huniye bağlanır: `ftue_step_n`, `first_death`, `first_seal`, `awakening_seen`, `ep1_complete`.

---

## 8. Endgame ve Canlı Operasyon Ritmi

### 8.1 Endgame modelleri

| Model | Referans | Güçlü yanı | Zayıf yanı | Bizde |
|---|---|---|---|---|
| Zamanlı, ölçeklenen anahtarlar | WoW Mythic+ | Sonsuz beceri tavanı, grup oyunu | Toksisite, grup bulma zorunluluğu | "Anomali Gate": solo veya co-op, zamanlı, rank'lı |
| Sonsuz kule veya çukur | D4 Pit, SAO kulesi | Basit, liderlik tablosuna uygun | Tekdüze olabilir | **Sonsuz Derinlik:** her 10 katta yeni kural (modifier) |
| Harita atlası | PoE2 Atlas, Last Epoch Monolith | Oyuncu kendi endgame rotasını seçer | Karmaşık | Sezonluk "Gate Takımyıldızı" haritası (ORV esinli) |
| Gönüllü zorluk sözleşmesi | Hades Heat/Pact | Oyuncu zorluğu kendisi ayarlar (flow [9]) | Ödül eğrisi dikkat ister | **Yemin sistemi:** tanrıya yemin et, zorluk artsın, kozmetik ödül ve unvan kazan |
| Liderlik tablosu | D4 (2026 yol haritası) [26] | Sosyal kanıt, yayıncı içeriği | Hile ve baskı riski | Haftalık sabit seed, sınıf başına ayrı tablo, sunucu tarafında doğrulama |
| Dünya olayı | Dungeon break (Solo Leveling) | Canlı dünya hissi (P6) | Kaçırma kaygısı (FOMO) yaratabilir | Olaylar tekrarlanır. Kaçırılan olayın ödülü sonra da kazanılabilir |

### 8.2 İçerik ritmi (hedef)

- **4–6 haftada bir** küçük yama: denge, QoL, 1 yeni Irregular olayı veya boss varyantı.
- **8–12 haftada bir** "Anime Sezonu": yeni ark bölümü, sezon mekaniği, yeni Gate tipi, OP/ED jeneriği ve sezon ligi. Diablo IV'ün sezon sürelerinin 48–105 gün arasında dalgalanması ve yılda 5 sezona çıkması [26], tek kişilik veya küçük bir ekip için **12 haftanın** daha gerçekçi bir alt sınır olduğunu düşündürüyor. Bu bizim çıkarımımız.
- **Yılda bir** ücretli genişleme.
- **Beklenti yönetimi:** PoE2'de lig ayından sonraki aylarda %60–70 düşüş olağan [27]. KPI olarak "sezon başında geri dönen oyuncu" izlenmeli. Aylık düşüşe panikle agresif günlük sistemler eklenmemeli.
- **MH Wilds dersi:** Çıkışta **en az 1 derin endgame modu** (Sonsuz Derinlik ve Yemin) hazır olmalı. İnce endgame ve performans sorunları bir araya gelince yorumlar ve oyuncu sayısı çöküyor [25].

### 8.3 Günlük ve haftalık sistemler: yorgunluk karşıtı tasarım

- **Günlük eğitim tamamen isteğe bağlı** ve 5–10 dk sürer. Kaçırılan günler **birikir**, en fazla 7 güne kadar (rested bonus mantığı). Seri kırılınca ödül sıfırlanmaz.
- **Haftalık tavan:** Haftalık ödüllerin büyük kısmı ilk 2–3 saatlik oyunda toplanır. Sonrası "istersen oyna" alanıdır.
- **Geri dönüş yakalama (catch-up):** Sezona geç başlayan oyuncuya hızlandırılmış ilerleme verilir. Geri dönen oyuncu cezalandırılmaz.
- Bu ilkelerin retention'a etkisine dair sayısal kanıt bulunamadı (**doğrulanamadı**). Dayanakları SDT'nin özerklik bulgusu [8] ile 02 raporundaki ARISE ve Blue Protocol tepkileri.

---

## 9. Co-op ve Çok Oyunculu Modun Bağlılığa Etkisi

- **Kanıt:** SDT'nin 4. çalışmasında ilişkililik, keyif ve gelecekte oynamanın bağımsız bir öngörücüsü [8]. "Co-op, retention'ı X% artırır" türünden güvenilir, güncel bir sayı bulunamadı (**doğrulanamadı**).
- **Maliyet gerçeği:** Gerçek zamanlı co-op; netcode, sunucu, hile önleme ve eşleştirme demek. Bu, tek kişilik bir geliştirici ve Claude Code iş akışı için en pahalı risk kalemlerinden biri. Motor seçimi raporuyla birlikte değerlendirilmeli.
- **Önerilen aşamalama:**
  1. **Çıkışta eşzamansız sosyallik:** hayalet koşular, paylaşılan harita notları, haftalık seed liderlik tabloları, "Familia" panosu (üye katkıları), yoldaş paylaşımı (arkadaşının yoldaşını AI ile kiralamak).
  2. **Çıkıştan sonra veya 1.0'da 2–4 kişilik drop-in co-op**, yalnızca Gate ve Anomali içeriğinde. Hikâye solo kalır.
  3. **PvP:** yalnızca isteğe bağlı, kozmetik ödüllü "War Game" etkinlikleri. Güç eşitlenir.

---

## 10. "Saatlerce Oynatan" 22 Somut Mekanik (Dark Pattern'siz)

| # | Mekanik | Nasıl çalışır | Neden işe yarar | Koruma (guardrail) |
|---|---|---|---|---|
| 1 | **Status Mühürleme Töreni** | Koşuda "ham" XP birikir. Tapınakta tanrı eşliğinde sinematik bir törenle istatistiğe mühürlenir | Hub'a dönüşü bir ödül ritüeline çevirir. Goal-gradient [11] | Tören atlanabilir veya hızlandırılabilir |
| 2 | **Ölüm Kırıntıları** | Her ölüm nedenine özel replik ve yeni bir lore parçası (Hades'te Hypnos'un 75 repliği gibi [20]) | Başarısızlığı ilerlemeye çevirir (P4) | Yok |
| 3 | **Sistem Önerisi (3'lü seçim)** | Oda sonunda 3 güçlendirme, sinerji etiketli | Özerklik ve build keşfi (Balatro/Hades tipi) | "Yeniden çek" hakları oynayarak kazanılır |
| 4 | **Açgözlülük Kararı** | Güvenli katta "kasaya koy ya da derine in" | Kendi seçtiği risk ve "bir kat daha" hissi | Kalıcı ilerleme hiç kaybolmaz |
| 5 | **Rank Sınavı** | Bölüm sonlarında E→S rank için özel bir sınav boss'u | Anlamlı kilometre taşı (DanMachi'de seviye atlama için "büyük başarı") | Tekrar denemesi ücretsiz |
| 6 | **Hatıra Gate'i (güç kontrolü)** | Eski kâbus boss'u yeni rank'ta isteğe bağlı olarak geri döner | Görünür güç büyümesi (P2, P8) | Yok |
| 7 | **Gizli Sınıf Koşulları** | Keşifle açılan, ipuçları dünyaya dağıtılmış sınıflar | Topluluk dedektifliği ve paylaşım (P9) | Asla satılmaz |
| 8 | **Gölge/Ruh Ordusu Koleksiyonu** | Elitler belirli bir şansla bağlanır. Kötü şans koruması garanti sağlar | Koleksiyon ve değişken ödül, yalnızca oynayarak | Görünür "garanti sayacı". Paralı hızlandırma yok |
| 9 | **Yoldaş Bağ Arkları** | Bağ seviyesi mekanik bir yetenek açar (P5R'deki confidant faydası [29]) | İlişkililik (SDT [8]) | Kaçırılamaz. Takvim baskısı yok |
| 10 | **Yemek ve Kamp Sahneleri** | Dünya tarifleri, buff'lar, yoldaşlarla sohbet | Nefes alma ritmi (Stardew tipi) | Buff'lar zorunlu değil |
| 11 | **Kasaba ve Ulus İnşası** | İsim verilen canavarlar vatandaş olur ve meslek edinir. Üretim oyuncu yokken de sürer | Uzun vadeli sahiplenme (P7). Palworld tipi otomasyon | Çevrimdışı birikim üst sınırlı ama cezasız. "Toplamazsan çürür" yok |
| 12 | **Yemin (gönüllü zorluk)** | Tanrıya yemin: düşman kuralları zorlaşır, ödüller kozmetik ve unvan olur | Flow ve beceri tavanı [9] | Güç ödülü yok, liderlik tablosu ayrı |
| 13 | **Sonsuz Derinlik** | Sınırsız katlar, her 10 katta yeni modifier | Hardcore endgame | Sezonluk ve kalıcı tablolar ayrı |
| 14 | **Haftalık Anomali Gate** | Sabit seed, herkese aynı zindan, liderlik tablosu | Sosyal kanıt ve yayın içeriği | Katılmayana ceza yok |
| 15 | **Dungeon Break Olayları** | Temizlenmeyen Gate şehre taşar, NPC'ler etkilenir | Yaşayan dünya (P6) | Hasar geri alınabilir. Kalıcı kayıp yalnızca "Hardcore" modda |
| 16 | **Eski Hayat Perk'leri** | Mühendis, aşçı, oyuncu gibi eski meslekler diyalog ve perk açar | Yeniden oynanabilirlik (P1) | Bütün perk'ler dengeli |
| 17 | **Kodeks ve Bestiary** | Düşman zayıflıkları öğrenildikçe dolar. Tamamlama bonusu kozmetik | Tamamlama ve bilgi gücü | Güç bonusu çok küçük |
| 18 | **"Sonraki Bölüm" Önizlemesi** | Oturum veya bölüm sonunda seslendirilmiş anime önizlemesi | Devam etme eğilimi [12] ve anime sunumu (P10) | Çıkışı engellemez |
| 19 | **Sezon Yolculuğu (ücretsiz)** | Sezon hedefleri ağacı. Ödüller sezon mekaniğini öğretir | Yön duygusu, goal-gradient | Sezon sonunda ödüller kaybolmaz, kozmetik olarak kalır |
| 20 | **Deterministik Craft** | Ruh taşı damıtma: ne alacağın bellidir (Last Epoch tipi) | Zamanına saygı, planlama keyfi | Craft malzemesi satılmaz |
| 21 | **Fotoğraf ve Aura Modu** | Anime kompozisyonlu fotoğraf modu, paylaşım | Sosyal paylaşım, organik pazarlama | Yok |
| 22 | **Rahat Mod / Sistem Desteği** | God Mode benzeri artan direnç [21] | Erişilebilirlik ve daha geniş kitle | Başarımlar ayrı işaretlenir, oyuncu utandırılmaz |

---

## 11. Kırmızı Çizgiler (Asla Yapmayacaklarımız)

| # | Dark pattern | Neden yasak | Kaynak ve dayanak |
|---|---|---|---|
| 1 | **Paralı rastgele ödül** (gacha, loot box, paralı sandık) | Problem kumarla orta düzeyde ilişkili (r = .27) [13]. Katılımcıların ~%19,6'sı loot box'ların sonradan kumara geçişi etkilediğini bildirdi [14]. Brezilya'da reşit olmayanlara yasak (17.03.2026) [19]. FTC yaptırımı [15] | Hukuki ve etik |
| 2 | **Gerçek fiyatı gizleyen premium para** (tuhaf paket miktarları, artık bakiye) | CPC ilkelerine göre fiyatın gerçek parayla gösterilmesi ve para birimi satın almaya zorlamama beklentisi var [17] | AB tüketici hukuku |
| 3 | **Kafa karıştırıcı satın alma butonları, tek tık satın alma** | Epic'e 245 milyon $ yaptırım [16] | FTC |
| 4 | **Ebeveyn kontrolsüz reşit olmayan satışı** | HoYoverse'e 20 milyon $, 16 yaş altına onaysız satış yasağı [15] | FTC ve COPPA |
| 5 | **Güç satmak (pay-to-win)** | "Hak edilmiş büyüme" (P2) sütununu çiğner. ARISE ve Blue Protocol tepkileri (02 raporu) | İtibar |
| 6 | **Enerji veya stamina ile oyunu kesip hızlandırma satmak** | Özerkliği zedeler [8]. Premium PC kitlesinin beklentisine aykırı | SDT |
| 7 | **Seri (streak) cezası** (bir gün kaçırınca her şey sıfırlanır) | Kaygıyla elde tutma. Refah yerine zorunluluk | Etik ve DFA'nın gündemi [18] |
| 8 | **Güç veren, zamanı sınırlı ve bir daha gelmeyen içerik (FOMO)** | Kıtlık baskısı. DFA "bağımlılık yaratan tasarım"ı hedefliyor [18] | Kozmetikler geri döner (rotasyon) |
| 9 | **Ara sahneye veya ölüm ekranına teklif pop-up'ı** | Sürükleyiciliği öldürür (ARISE eleştirisi, 02 raporu) | Mağaza yalnızca hub'da, oyuncu isteyince açılır |
| 10 | **Yapay grind ile hızlandırıcı satmak** | Güven kaybı. Oyuncu zamanını düşmana çevirir | Tasarım ilkesi |
| 11 | **Parayla bağlantılı near-miss manipülasyonu** ("az kalsın!" animasyonu) | Kumar tekniği (Vampire Survivors analizi [24]) | Oynayarak kazanılan loot'ta bile sahte near-miss yok |
| 12 | **Sosyal zorunluluk** (lonca cezası, "arkadaşın seni bekliyor" bildirimi) | İlişkililiği baskıya çevirir | SDT [8] |
| 13 | **Confirmshaming ve çıkışı zorlaştırma** ("Gerçekten güçsüz kalmak mı istiyorsun?") | Manipülatif arayüz. DFA hedefinde [18] | Etik |
| 14 | **Gizli oranlar veya gizli DDA ile ödül manipülasyonu** | Oranlar ve bu tür hesaplar şeffaf olmalı [15][17] | FTC ve CPC |

---

## Oyunumuz İçin Çıkarımlar

1. **Oturum 30–45 dk, bölüm 5–15 saat, sezon 12 hafta.** PC'nin "derinlik platformu" oluşu [3][4] ile uyumlu bir ritim. Mobil sürüm düşünülürse ayrıca 5–10 dk'lık yüzey Gate'leri ana mobil döngü olur [1].
2. **İlk 2 saat = demo + iade penceresi.** Uyanış olayı ve ilk Aura anı **90. dakikadan önce** gelmeli [7]. Steam Next Fest demosu da bu ilk 60–90 dakikayı kullanmalı.
3. **Hub'a dönüş bir ödül olmalı, ceza değil.** Status mühürleme töreni (DanMachi) ve ölüm kırıntıları (Hades [20]) sayesinde her ölüm "bir sonraki koşuya sebep" olur. Seslendirme bütçesi reaktif repliklere öncelik vermeli: az ama bağlama duyarlı satır, uzun ara sahneden daha değerli.
4. **Üç eksenli güç eğrisi:** kalıcı istatistik, build ve bilgi. Bilgi ekseni satılamaz. Oyunun en "hak edilmiş" hissi buradan gelir.
5. **Çıkışta endgame hazır olmalı:** Sonsuz Derinlik, Yemin ve Haftalık Anomali Gate. MH Wilds dersi [25].
6. **Canlı operasyon kapasitesi gerçekçi olmalı.** Tek kişilik ekip ve Claude Code için 12 haftalık sezon ve 4–6 haftalık yama ritmi. Diablo IV'ün sıklaştırma deneyimi [26] daha fazla sezonun daha fazla yük demek olduğunu gösteriyor. İçerik üretim hattı (AI asset'leri) bu ritme göre boyutlandırılmalı.
7. **Rastgelelik oyunda, determinizm mağazada.** Mağaza yalnızca kozmetik, genişleme ve isteğe bağlı kozmetik sezon pass satar. Her fiyat gerçek parayla gösterilir [17]. Paralı gacha tamamen dışarıda kalır. Bu hem Brezilya/AB/ABD hukuku [15][17][19] hem de 02 raporundaki "adil para kazanma" konumlanması için şart.
8. **Günlük sistemler isteğe bağlı ve birikimli olmalı.** Seri cezası yok. Geri dönen oyuncuya catch-up verilir. Hedef, "her sezon geri dönen oyuncu".
9. **Co-op aşamalı gelmeli:** çıkışta eşzamansız sosyallik, sonra Gate'lerde 2–4 kişilik co-op. Netcode riski motor seçim raporunda ayrıca ele alınmalı.
10. **Telemetri ilk günden kurulmalı.** FTUE hunisi, oturum sonu "devam" oranı, bölüm bitirme oranları, seçim dağılımları, sezon dönüş oranı. Kıyas için GameAnalytics'in PC ve mobil verileri [1][3] kullanılabilir. Premium KPI'lar (iade oranı, 2. saat oranı) kendi hedef tablomuzla izlenmeli.
11. **Anime sunum katmanı döngünün parçası olmalı.** "Sonraki bölüm" önizlemesi [12], sezon OP/ED'leri ve rank sınavı sinematikleri döngüyü kapatan birer ödül. Bu yüzden kozmetik değil, çekirdek tasarım (01 raporu, P10).
12. **Erişilebilirlik bir büyüme kaldıracı.** God Mode benzeri bir "Sistem Desteği" modu [21] rahat oyuncuyu da içeri alır. Zorluk tavanı Yemin sistemiyle sınırsız kalır.

---

## Belirsizlikler ve Riskler

- **Benchmark temsiliyeti:** GameAnalytics verisi SDK kullanan projelerden geliyor. Premium ve büyük Steam oyunlarını temsil etmeyebilir. 2026 PC özetinde mobil ve PC sayıları karışmış olabilir (PC medyan D7 değeri **[D]**) [3][4].
- **Steam medyan oynama süreleri doğrulanamadı** (SteamSpy ve Steam API erişilemedi). Hades II için yalnızca ikincil bir "65 saat" tahmini var [31].
- **Co-op'un retention'a etkisi** için güvenilir, güncel bir sayı bulunamadı. Aynı şekilde "isteğe bağlı günlükler retention'ı nasıl etkiler" sorusunun da sayısal kanıtı yok. Bunlar bizim testlerimizle ölçülmeli.
- **Diablo IV sezon verileri** ikincil kaynaktan (**[D]**) [26]. Last Epoch'un 2025–2026 sayıları arama özetlerinde çelişkili olduğu için bilinçli olarak kullanılmadı.
- **Hades II satış sayısı** üçüncü taraf bir tahmin (Raijin), resmî değil [22].
- **Hukuk hızla değişiyor.** AB Digital Fairness Act önerisi 2026'nın ikinci yarısında bekleniyor, kabulü muhtemelen 2027'den önce değil [18]. Brezilya'daki 9 Haziran 2026 loot box kararı (toplam ~333 milyon BRL) [19] temyize gidebilir. Brezilya yasasındaki tanım ödemeyi şart koşuyor ama yasak maddesi "sunmak" (offered) fiilini kullanıyor; **ücretsiz, oynayarak kazanılan rastgele ödüllerin** kapsama girip girmediği hukuken henüz net değil. "Rastgelelik yalnızca oyunda" kuralımız doğru yön, ama Brezilya'da yaşa göre derecelendirme ve hukuki görüş gerekli (eklendi 24.09.2026). Türkiye'de oyun içi satın alma ve loot box düzenlemesi bu raporda **araştırılamadı**. Monetizasyon raporunda ele alınmalı.
- **Tek kişilik geliştirici riski:** 22 mekaniğin hepsi çıkışa sığmaz. Önceliklendirme şöyle olmalı:
  - **Çıkış (MVP):** 1–6, 9, 12, 13, 18
  - **1. sezon:** 11, 14, 15
  - **Sonrası:** co-op, PvP
- **Etik tasarım ile ticari başarı dengesi:** Etik döngülerin premium PC'de daha iyi yorum ve satış getirdiği görüşü vaka verilerine dayanıyor (Hades II, Balatro, Stardew) [22][23][30]. Nedensellik kanıtlanmış değil.
- **Zeigarnik ve Ovsiankina bulgusu** tek bir meta-analize dayanıyor [12]. Pratik tasarım sonucu (kaldığın yerden devam etmeyi kolaylaştırmak) zaten risksiz.

---

## Kaynaklar

1. https://www.gameanalytics.com/reports/2025-mobile-gaming-benchmarks
2. https://gamedevreports.substack.com/p/gameanalytics-mobile-gaming-benchmarks
3. https://www.gameanalytics.com/reports/2026-mobile-pc-gaming-benchmarks
4. https://gamedevreports.substack.com/p/gameanalytics-mobile-and-pc-game
5. https://www.gamigion.com/2026-mobile-pc-gaming-benchmarks-report-by-gameanalytics/
6. https://segwise.ai/blog/mobile-gaming-app-user-retention-strategies
7. https://store.steampowered.com/steam_refunds/
8. https://selfdeterminationtheory.org/SDT/documents/2006_RyanRigbyPrzybylski_MandE.pdf ve https://link.springer.com/article/10.1007/s11031-006-9051-8
9. https://cacm.acm.org/opinion/flow-in-games-and-everything-else/ ve https://www.jenovachen.com/flowingames/p31-chen.pdf
10. https://en.wikipedia.org/wiki/Flow_(video_game)
11. https://journals.sagepub.com/doi/abs/10.1509/jmkr.43.1.39 ve https://home.uchicago.edu/ourminsky/Goal-Gradient_Illusionary_Goal_Progress.pdf
12. https://www.nature.com/articles/s41599-025-05000-w
13. https://journals.sagepub.com/doi/10.1177/14614448211027175
14. https://pubmed.ncbi.nlm.nih.gov/35397261/
15. https://www.ftc.gov/news-events/news/press-releases/2025/01/genshin-impact-game-developer-will-be-banned-selling-lootboxes-teens-under-16-without-parental ve https://consumer.ftc.gov/consumer-alerts/2025/01/ftc-settlement-order-bans-sales-genshin-impact-loot-boxes-kids-under-16-without-their-parents
16. https://www.ftc.gov/news-events/news/press-releases/2023/03/ftc-finalizes-order-requiring-fortnite-maker-epic-games-pay-245-million-tricking-users-making , https://www.ftc.gov/news-events/news/press-releases/2022/12/fortnite-video-game-maker-epic-games-pay-more-half-billion-dollars-over-ftc-allegations ve https://www.ftc.gov/enforcement/refunds/fortnite-refunds
17. https://commission.europa.eu/document/download/8af13e88-6540-436c-b137-9853e7fe866a_en?filename=Key+principles+on+in-game+virtual+currencies.pdf ve https://connectontech.bakermckenzie.com/european-consumer-protection-network-issues-new-key-principles-on-in-game-virtual-currencies-impact-for-gaming-and-gambling-entities-in-belgium-the-eu-and-beyond/
18. https://www.freshfields.com/en/our-thinking/blogs/technology-quotient/the-eus-proposed-digital-fairness-act-a-game-developers-guide-to-potential-imp-102ltio ve https://chambers.com/articles/digital-fairness-act-what-the-public-consultation-tells-the-video-game-industry
19. https://www.mayerbrown.com/en/insights/publications/2026/04/enforcement-of-brazils-eca-digital-introduces-new-obligations-for-companies ve https://www.lickslegal.com/articles/brazil-s-first-loot-box-ruling-key-takeaways-for-digital-companies/
20. https://www.gamedeveloper.com/audio/dive-into-the-dialogue-of-i-hades-i-at-gdc-2021 , https://www.gamedeveloper.com/design/how-supergiant-weaves-narrative-rewards-into-i-hades-i-cycle-of-perpetual-death ve https://gamerant.com/hades-developer-infographic-dialogue-breakdown/
21. https://hades.fandom.com/wiki/God_Mode ve https://www.gamesradar.com/hades-god-mode-achievements/
22. https://www.gamespot.com/articles/hades-2-passes-110000-concurrent-players-on-steam-doubling-all-time-peak-for-original/1100-6535081/ , https://en.wikipedia.org/wiki/Hades_II ve https://raijin.gg/app/1145350/Hades_II/sales-revenue
23. https://www.playstack.com/news/balatro-5-million-copies-sold/ ve https://www.gamedeveloper.com/business/balatro-sells-5-million-copies-after-end-of-year-spike
24. https://theconversation.com/vampire-survivors-how-developers-used-gambling-psychology-to-create-a-bafta-winning-game-203613 ve https://www.androidpolice.com/vampire-survivors-developer-interview/
25. https://www.forbes.com/sites/paultassi/2025/06/21/monster-hunter-wilds-collapses-with-1-of-launch-players-82-negative-reviews/ ve https://www.gamespot.com/articles/monster-hunter-wilds-on-pc-is-seeing-fewer-players-than-world-as-negative-reviews-continue/1100-6532587/
26. https://ggseason.com/blog/diablo-4-all-seasons-dates/ ve https://www.tweaktown.com/news/104518/diablo-4s-first-roadmap-is-here-new-seasons-ip-crossover-events-expansions-and-more/index.html
27. https://steamcharts.com/app/2694490 , https://www.exitlag.com/blog/path-of-exile-2-player-count/ ve https://dedicatedgameservers.net/articles/path-of-exile-2-roadmap-2026-1-0-window/
28. https://www.forbes.com/sites/paultassi/2025/04/18/last-epoch-season-2-blasts-off-with-massive-player-retention/
29. https://www.gematsu.com/2026/06/persona-3-reload-shipments-and-digital-sales-top-three-million , https://x.com/Atlus_West/status/1755397306697077107 ve https://hardcoregamer.com/features/persona-5-royal-confidant-guide/370507/
30. https://www.gamingonlinux.com/2025/01/stardew-valley-hits-over-41-million-sales-with-millions-sold-during-2024/
31. https://space4games.com/en/games-en/hades-2-playtime-how-many-hours-youll-spend-in-the-dark-roguelike/
32. İç referanslar: `docs/research/01-isekai-anime-analizi.md` (P1–P10 sütunları, mekanik çeviri tablosu) ve `docs/research/02-pazar-ve-rakip-analizi.md` (ARISE ve Blue Protocol tepkileri, konumlandırma)

---

## Doğrulama Notları (24.09.2026)

> Bağımsız doğrulama turu (adversarial fact-check). Karar etkisi yüksek kıyas verileri ve 09 raporuyla iç tutarlılık kontrol edildi. Akademik kaynaklar (SDT, goal-gradient, Zeigarnik meta-analizi, Spicer vd.) bu turda yeniden aranmadı.

| İddia | Sonuç | Düzeltme/Not | Kaynak |
|---|---|---|---|
| GameAnalytics 2026: PC medyan günlük süre 32–33 dk, üst %25 70 dk, üst %10 120 dk; PC üst %25 D1 %15–16, üst %1 %50–60 | Doğrulandı | Ek: PC medyan D1 ~%7, alt %25 ~%3. Örneklem: en az 100 MAU'lu 3.582 PC oyunu ve 16 binden fazla mobil oyun. Küçük oyun ağırlıklı; premium Steam hitlerini temsil etmeyebilir | https://gamedevreports.substack.com/p/gameanalytics-mobile-and-pc-game · https://www.gameanalytics.com/reports/2026-mobile-pc-gaming-benchmarks |
| Steam iadesi: 14 gün içinde ve <2 saat | Doğrulandı | 23 Nisan 2024'ten beri Early Access ve Advanced Access süresi de 2 saate sayılıyor. Early Access planlanıyorsa ilk 2 saat kuralı EA sürümü için de geçerli | https://store.steampowered.com/steam_refunds/ · https://gameworldobserver.com/2024/04/24/steam-refund-changed-playtime-counts-in-advanced-access |
| Hades II 1.0 (25 Eyl 2025) zirvesi 112.947, Hades I zirvesi 54.240 | Doğrulandı | Zirve 28 Eyl 2025 | https://store.steampowered.com/news/group/4777282/view/4169846932066328202 · https://www.gamespot.com/articles/hades-2-passes-110000-concurrent-players-on-steam-doubling-all-time-peak-for-original/1100-6535081/ |
| Hades II ~5,2 milyon kopya, ~93,5 milyon $ | Doğrulanamadı (yalnızca tahmin) | Raijin tahmini, resmî değil, iki değer birbiriyle tutarsız. Doğrulanmış alt sınır: 1.0 öncesi Steam'de 2 milyon+ | https://wnhub.io/news/analytics/item-48907 |
| MH Wilds: 1,38 milyon zirveden Haziran 2025'te ~%1'e düşüş | Doğrulandı | Zirve 1.384.608 (1 Mar 2025). Haziran 2025'te ~%98 kayıp. Satış: 11,4 milyon toplam, FY2026'da yalnızca 1,32 milyon | https://www.forbes.com/sites/paultassi/2025/06/21/monster-hunter-wilds-collapses-with-1-of-launch-players-82-negative-reviews/ · https://gamerant.com/monster-hunter-wilds-player-count-decline-steam-users-report/ · https://www.pushsquare.com/news/2026/05/monster-hunter-wilds-sales-really-have-fallen-off-a-cliff |
| Brezilya Lei 15.211/2025, 17 Mar 2026'dan beri reşit olmayanlara ücretli loot box yasak | Doğrulandı (nüans eklendi) | Yasak maddesi "sunmak" fiilini kullanıyor; ücretsiz rastgele mekaniklerin kapsamı hukuken net değil. 9 Haziran 2026 kararı (~333 milyon BRL) bu turda yeniden doğrulanmadı | https://factotumcom.substack.com/p/brazil-digital-eca-bans-loot-boxes · https://www.pcgamer.com/gaming-industry/brazils-president-has-signed-a-ban-on-selling-loot-boxes-to-minors-as-part-of-a-larger-online-child-safety-law/ |
| FTUE takvimi (§7) 09 raporuyla tutarlı | Düzeltildi (iç çelişki) | 09'un ilk sürümünde ilk dövüş 65. dk, Uyanış 105–120. dk idi. 09 §3 bu raporun hedeflerine göre hizalandı (ilk dövüş ≤10. dk, Uyanış ≤90. dk). F-rank sahnesinin dakikası (5–15 ↔ 30–45) dikey dilim testinde belirlenecek | 09 raporu §3 (iç referans) |
| Günlük görevde kaçırılan günler en fazla 7 gün birikir (§8.3) | Doğrulandı (iç tutarlılık) | 09 raporundaki "3 gün" bu rapora göre 7 güne düzeltildi | 09 raporu §3.5 (iç referans) |

**Karar etkisi:** Oturum, bölüm ve sezon ritmi önerileri değişmiyor. FTUE'de "ilk dövüş ilk 10 dakikada, Uyanış 90. dakikadan önce" artık iki raporun ortak, değişmez koşulu. Brezilya notu, oynayarak kazanılan rastgele ödüller için de yaşa göre derecelendirme ve hukuki görüş gerektiriyor.
