# 04 — Monetizasyon Modelleri, Kıyaslar ve Regülasyon (2025–2026)

> Hazırlanma: 2026-09-24 · Kapsam: PC-first (Steam), sonra konsol/mobil; Türkiye merkezli solo/indie geliştirici.
>
> **Yöntem ve doğrulama notu (önemli, okuyun):** Bu rapor başladığında oturumun WebSearch kotası (200 arama) diğer araştırmacılar tarafından tüketilmişti. WebFetch ve curl ise Steam, FTC, AB, GİB, Resmî Gazete gibi alan adlarında egress proxy tarafından engellendi. Bu yüzden her iddia aşağıdaki etiketlerden biriyle işaretlendi:
> - **[C] Canlı doğrulandı:** Bu oturumda birincil kaynaktan açılıp okundu. Erişilebilen birincil kaynaklar developer.apple.com ve GitHub oldu.
> - **[R] Kardeş rapor:** `02-pazar-ve-rakip-analizi.md` raporunda WebSearch ile doğrulanmış; kaynak URL'si oradan aktarıldı.
> - **[B] Bilgi tabanlı:** Model bilgisine (Haziran 2026'ya kadar) dayanıyor; verilen URL bu oturumda açılamadı. **Doğrulayıcı (fact-checker) önce bunlara bakmalı.**
> - Güven düzeyi: **Y** yüksek, **O** orta, **D** düşük veya doğrulanamadı.

## Özet

- **Önerilen ana model premium (tek seferlik satın alma, B2P).** Fiyat 1.0'da 24,99 $, Early Access'te 19,99 $. Gelir; destekçi paketi, OST, deterministik (rastgele olmayan) kozmetik DLC ve yılda bir ücretli genişleme ile büyütülür. **Ücretli rastgele öğe hiç olmayacak:** gacha, loot box ve bunlara dönüşebilen premium para birimi yok.
- **Steam'in payı ömür boyu brüt gelirin ilk 10 milyon $'ında %30'dur.** 10–50 milyon $ arası %25, 50 milyon $ üstü %20 [1] [B/Y]. Steam Direct ücreti oyun başına 100 $'dır ve oyun 1.000 $ gelir yapınca geri ödenir [2] [B/Y]. Gerçekçi senaryolarımızın hepsi %30 diliminde kalıyor.
- **Mobilde Apple'ın Small Business Program'ı önceki yılda ≤1 milyon $ hasılat yapan geliştiriciden %15 komisyon alır** [8] [C/Y]. Google Play de her yılın ilk 1 milyon $'ına %15 uygular [9] [B/O].
- **Loot box regülasyonu sıkılaşıyor ve parçalı bir yapıda:**
  - Brezilya'da ECA Digital (Kanun 15.211/2025) 17 Mart 2026'da yürürlüğe girdi. Reşit olmayanların erişebildiği oyunlarda ücretli loot box yasak; ceza 50 milyon BRL'ye veya Brezilya gelirinin %10'una kadar çıkabiliyor [29][30] [R/Y].
  - Apple, loot box içeren uygulamalara Brezilya'da 18+ [24][23], Avustralya'da 18 Haziran 2026'dan itibaren 16+ yaş sınırı veriyor [25] [C/Y].
- **ABD'de FTC, Ocak 2025'te HoYoverse'e (Genshin Impact) 20 milyon $ ceza verdi.** Şirketin 16 yaş altına ebeveyn izni olmadan loot box satması yasaklandı; olasılıkları ve sanal para biriminin gerçek para karşılığını göstermesi zorunlu hâle geldi [33] [B/Y].
- **Güney Kore'de ücretli olasılıklı öğelerin oranlarını açıklamak 22 Mart 2024'ten beri yasal zorunluluk.** İspat yükünü yayıncıya geçiren ve kasıtlı ihlalde 3 kata kadar tazminat getiren değişiklik Aralık 2024'te Meclis'ten geçti, Ocak 2025'te kabul edildi ve **1 Ağustos 2025'te yürürlüğe girdi** (düzeltildi 24.09.2026) [31] [R/Y].
- **Japonya'da "kompu gacha" 2012'den beri yasak** [40] [B/Y].
- **Belçika 2018'den beri ücretli loot box'ı lisanssız kumar sayıyor,** ama uygulama zayıf [35][36] [B/O].
- **Hollanda'da Danıştay (Raad van State) 2022'de EA'ya kesilen 10 milyon €'luk cezayı bozdu** [37] [B/O].
- **İngiltere yasa yerine sektörün öz-düzenlemesini seçti** (Ukie ilkeleri, 2023) [38][39] [B/O].
- **AB'de loot box'a özel bir yasa henüz yok, ama baskı artıyor.** Tüketici Koruma İşbirliği (CPC) ağı Mart 2025'te oyun içi sanal para birimleri için ilkeler yayımladı (Star Stable vakası) [41] [B/O]. Digital Fairness Act teklifi **24 Eylül 2026 itibarıyla henüz yayımlanmadı**; Komisyon'un 2026 çalışma programı teklifi 2026'nın 4. çeyreğine (Ekim–Aralık) koyuyor. Avrupa Parlamentosu (Kasım 2025, bağlayıcı değil) DFA'nın reşit olmayanların erişebildiği oyunlarda loot box'ı yasaklamasını istedi (düzeltildi 24.09.2026) [42].
- **PEGI, Haziran 2026'dan itibaren yeni başvurulara "etkileşimli risk" kriterleri uyguluyor** (düzeltildi 24.09.2026): ücretli rastgele öğe → en az **PEGI 16**; süreli veya adet sınırlı satın alma teklifi → en az **PEGI 12**; NFT/blokzincir → **PEGI 18**; engelleme, raporlama ve filtre aracı olmayan sınırsız çevrimiçi iletişim → **PEGI 18** [44].
- **Türkiye'de loot box'a özel bir düzenleme bulunamadı** (bu oturumda yalnızca model bilgisiyle kontrol edilebildi) [B/D]. Ancak çocuk koruma gerekçeli erişim engelleri (Roblox, Ağustos 2024) iklimin sertleştiğini gösteriyor [52] [B/Y].
- **Türkiye'de Dijital Hizmet Vergisi %7,5'ten %5'e indi.** Apple, Türkiye satışlarında bu vergiyi geliştirici hasılatından düşüyor ve oranı 29 Ocak 2026'da %5 olarak güncelledi [27] [C/Y]. Oran 10767 sayılı Cumhurbaşkanı Kararı ile 1 Ocak 2026'dan itibaren %5, **1 Ocak 2027'den itibaren %2,5** (düzeltildi 24.09.2026).
- **Steam, Kasım 2023'ten beri Türkiye'de TL değil USD ile fiyatlandırıyor** [49] [B/Y]. Apple da Türkiye fiyatlarını kur nedeniyle defalarca güncelledi (Aralık 2024, Kasım 2025) [72][73] [C/Y].
- **Türk geliştirici Steam'de vergi mülakatını dolduruyor:** şahıs olarak W-8BEN, şirket olarak W-8BEN-E. ABD–Türkiye çifte vergilendirme anlaşmasına göre telif ödemelerinde stopaj %10'dur [53][54][56] [B/O]. Kickstarter'da proje sahibi olarak Türkiye desteklenmiyor [63] [B/O].
- **Gerçekçi gelir beklentisi düşük.** 2025'te Steam'e çıkan oyunların ~%40'ı 100 $ bile kazanamadı, yalnızca ~%8'i 100 bin $ brüt geliri aştı [13] [R/O]. 24,99 $'lık oyun için 24 aylık senaryolarımız (vergi öncesi net):
  - Kötümser (5 bin kopya): ~49 bin $
  - Temel (50 bin kopya): ~515 bin $
  - İyimser (400 bin kopya): ~4,3 milyon $

---

## 1. Platform Ücretleri, Gelir Payları ve Motor Telifleri

| Platform / Motor | Kesinti / Telif | Not | Etiket | Kaynak |
|---|---|---|---|---|
| **Steam** | Ömür boyu brüt gelirin ilk 10 milyon $'ında %30; 10–50 milyon $ arası %25; 50 milyon $ üstü %20 | Oyun, DLC ve oyun içi satışlar birlikte sayılır. Değişiklik Kasım 2018'de duyuruldu | B/Y | [1] |
| **Steam Direct** | Ürün başına 100 $ | Oyun 1.000 $ düzeltilmiş brüt gelire ulaşınca geri ödenir. Ücreti ödedikten sonra ilk çıkış için 30 gün beklenir. "Coming Soon" sayfası çıkıştan en az 2 hafta önce yayında olmalıdır | B/Y | [2] |
| **Steam DLC / OST** | Ek başvuru ücreti yok | DLC ve soundtrack ayrı mağaza sayfası olarak açılır. Gelir payı %30 | B/O | [3] |
| **Epic Games Store** | 88/12. Haziran 2025'ten itibaren uygulama başına yılda ilk 1 milyon $'da %0 | EGS gelirine Unreal telifi uygulanmaz | B/O | [4][11] |
| **GOG** | Standart 70/30 | Seçici küratörlük var | B/O | [5] |
| **itch.io** | Varsayılan %10, geliştirici değiştirebilir | Demo, prolog ve destek (donation) kanalı olarak kullanılabilir | B/Y | [7] |
| **Konsollar (PS/Xbox/Nintendo)** | Genelde %30 | Sözleşmeler gizli (NDA). Port için partner veya yayıncı gerekir | B/O | — |
| **Apple App Store** | %30. Small Business Program ile %15 | Önceki takvim yılında ≤1 milyon $ hasılat yapanlar ve yeni geliştiriciler %15 öder. Yıl içinde eşik aşılırsa standart orana dönülür, bir sonraki yıl yeniden hak kazanılabilir | **C/Y** | [8] |
| **Google Play** | Her yılın ilk 1 milyon $'ına %15, üstüne %30. Aboneliklerde %15 | ABD'de Epic v. Google sonrası ödeme kuralları değişiyor (detay doğrulanamadı) | B/O | [9] |
| **Godot** | Telif yok (MIT lisansı) | Lisans GitHub'da doğrulandı | **C/Y** | [10] |
| **Unreal Engine** | Ürün başına ömür boyu ilk 1 milyon $ brütten sonra %5 | "Launch Everywhere with Epic" programında %3,5. EGS gelirine telif yok | B/O | [11] |
| **Unity** | Runtime Fee Eylül 2024'te iptal edildi. Personal sürüm ~200 bin $ gelir sınırına kadar ücretsiz | Pro/Enterprise lisansı yıllık ücretli | B/O | [12] |

**Yorum:** Motor seçimi bu raporun konusu değil. Ancak gelir açısından Godot'nun telifsiz olması, Unreal'ın %5'lik telifinin (1 milyon $ sonrası) iyimser senaryoda ~150–200 bin $ fark yaratabileceğini gösteriyor. Bu fark, motorun iş akışına kattığı değerle birlikte tartılmalı.

---

## 2. Monetizasyon Modelleri: Solo ve Indie İçin Karşılaştırma

| Model | Gelir potansiyeli (solo/küçük ekip) | Operasyon yükü | Yasal risk | Topluluk riski | Bizim için |
|---|---|---|---|---|---|
| **Premium (B2P), 19,99–29,99 $** | Hit olursa çok yüksek, medyan çok düşük [13] | Düşük: çıkış ve yamalar | Çok düşük | Düşük | **ANA MODEL** |
| **Early Access** | Geliştirme sürerken gelir ve geri bildirim sağlar. Hades II EA → 1.0 başarısı [20] | Orta: düzenli güncelleme sözü | Düşük (Steam EA kuralları var) | Orta: "bitmeyen EA" algısı | **Önerilir** (koşullu, bkz. §7) |
| **Premium + kozmetik DLC / genişleme / OST / artbook** | Temel gelire +%5–20 (D, sektör sezgisi) | Orta | Düşük (PEGI "in-game purchases" etiketi gelebilir [44]) | Kozmetikse düşük; oyun "kesilip satılmış" görünürse yüksek | **İKİNCİL** |
| **Destekçi paketi (Supporter / Deluxe)** | Küçük ama yüksek marjlı | Düşük | Çok düşük | Güç (stat) içermezse çok düşük | **Önerilir** |
| **F2P + battle pass + kozmetik** | Ölçek gerektirir. Payer dönüşümü sektörde tipik olarak %1–5 (D) | **Çok yüksek**: canlı operasyon, içerik takvimi, sunucu | Orta: AB'nin sanal para ilkeleri, çocuk koruma [41] | Yüksek (FOMO) | Önerilmez |
| **Gacha / loot box** | Üst segmentte çok yüksek; ekip 500+ kişi [R] | Çok yüksek | **Yüksek**: Brezilya yasağı, Kore, Belçika, FTC, yaş derecelendirmesi [29][31][33][24] | **Çok yüksek**: ARISE ve BP:SR tepkileri [67][68] | **Kesinlikle hayır** |
| **Abonelik / Game Pass tipi anlaşma** | Tek seferlik anlaşma olarak cazip olabilir (tutarlar gizli, D) | Düşük | Düşük | Düşük | Hit sinyali sonrası fırsatçı değerlendirilmeli |
| **B2P + live service** (sezonluk içerik) | Orta–yüksek | Yüksek | Düşük–orta | Orta | Yalnızca "ücretsiz güncellemeler + yıllık genişleme" biçiminde |
| **Kitle fonlaması** (Kickstarter/Patreon) | Kickstarter: pazarlama ve ön satış. Patreon: küçük, düzenli gelir | Orta: ödül teslimatı | Kickstarter'da Türkiye desteklenmiyor [63] | Teslim edemezsen ağır itibar kaybı | Kickstarter hayır; Patreon/Ko-fi yalnızca devlog için |
| **Yayıncı anlaşması** | Avans + pazarlama + port + Asya yerelleştirmesi | Düşük (yayıncı üstlenir) | Sözleşme riski (IP, süre) | Düşük | Konsol/Asya için **seçici** (bkz. §6.5) |

**Kritik gözlem (02 raporundan):** Aynı IP'de bile model değişiyor. Netmarble, gacha'lı Solo Leveling: ARISE'dan sonra PC için gacha'sız, 39,99 $'lık premium Overdrive'ı çıkardı [21] [R]. Duet Night Abyss çıkıştan hemen önce karakter ve silah gacha'sını kaldırdı [69] [R]. ARISE'ın sinematiklerin üstüne açılan teklifleri ve çoklu abonelikleri sert eleştiri aldı [67] [R]. Bizim hedefimiz olan **"isekai'yi yaşama" hissi, satış pop-up'larıyla doğrudan çelişiyor.**

---

## 3. Kıyas Verileri (Benchmarks)

| Metrik | Değer | Etiket | Kaynak |
|---|---|---|---|
| Steam 2025 çıkış sayısı | 19 binden fazla | R/O | [13] |
| 2025 çıkışlarında gelir dağılımı | ~%40'ı 100 $ altında, ~%8'i 100 bin $ brüt üstünde | R/O | [13] |
| Indie payı (Steam 2025) | Gelirin ~%25'i (~4,4 milyar $) | R/O | [13] |
| İstek listesi → ilk hafta satış | GameDiscoverCo (Eylül 2024–Eylül 2025 çıkışları): 25 bin+ istek listeli oyunlarda medyan **0,15×**, **10 $ üstü oyunlarda medyan 0,10×**. Oyunlar arasında 10 kattan fazla fark var. 19,99–24,99 $'lık oyunumuz için gerçekçi taban ~%10; %15–20 iyi senaryo (düzeltildi 24.09.2026) | R/O | [14][16] |
| "Popular Upcoming" görünürlüğü | Eski ~7 bin rehberi **geçersiz**. Valve Haziran 2026'daki mağaza değişikliğiyle bu rafı algoritmik yaptı; Zukowski'nin tahminine göre artık ~100 bin (başka tahminler ~80–120 bin) istek listesi gerekiyor. Indie için asıl raf kişiselleştirilmiş **Personal Calendar** (resmî eşik yok) (düzeltildi 24.09.2026) | R/O | [14] |
| Boxleiter çarpanı (inceleme × çarpan ≈ satış) | Tarihsel aralık 20–60. 2026 çıkışları için medyan ~30× (çalışma aralığı 20–40×), yıllar içinde yavaşça düşüyor (Gamalytic/VG Insights özetleri). Ucuz ve niş oyunlarda sapma büyük (düzeltildi 24.09.2026) | R/O | [15][16] |
| Steam iade politikası | Satın almadan sonraki 14 gün içinde ve 2 saatten az oynanmışsa iade | B/Y | [17] |
| Tipik iade oranı | ~%5–12 (sektör sezgisi; doğrulanamadı) | D | — |
| Next Fest | Yılda 3 kez (Şubat, Haziran, Ekim) | B/Y | [19] |
| İndirim kuralları | İndirimler arasında bekleme süresi var. Fiyat artışından sonra belirli süre indirim yapılamaz. Valve'ın sezonluk indirimleri ayrı kurallara tabi | B/O | [18] |
| Net gelir sezgisi | "Satış × liste fiyatı"nın ~%35–50'si geliştiriciye kalır (bölgesel fiyat, indirim, KDV, iade, Steam payı sonrası). Bizim modelimizde ~%37 (bkz. §8) | D | — |
| DLC bağlanma oranı (attach rate) | Kozmetik DLC ~%5–15, OST ~%2–8 (sezgisel; doğrulanamadı) | D | — |
| F2P payer dönüşümü | ~%1–5; ARPPU türe göre çok değişken | D | — |
| Early Access örneği | Hades II: EA Mayıs 2024 → 1.0 25 Eylül 2025. 1.0 öncesi 2 milyon+ satış. Ağustos 2026'da Steam'de ~5,2 milyon kopya (tahmin) | R/O | [20] |
| IP'li premium örneği | Solo Leveling: ARISE OVERDRIVE (39,99 $): ilk hafta ~127 bin (tahmin), Metacritic 64 | R/O | [21] |

**Fiyat bandı referansı (02 raporundan):** Anime ARPG'lerde 39,99–44,99 $ fiyatlar IP'li ve vasat oyunlarda "Mixed" puanla birleşince satışı sınırladı (Overdrive, Mushoku QoM) [R]. Özgün bir indie için **19,99–29,99 $** hem "AAA değilim" dürüstlüğünü hem de indirim alanını koruyor.

---

## 4. Ücretli Rastgele Öğe (Loot Box / Gacha) Regülasyonu: Ülke Ülke

| Yargı alanı | Kural | Tarih / Durum | Bize etkisi (ücretli rastgelelik YOKSA) | Etiket | Kaynak |
|---|---|---|---|---|---|
| **Belçika** | Kansspelcommissie: ücretli loot box, 1999 Kumar Kanunu'na göre lisanssız şans oyunudur | Nisan 2018 raporu. Uygulama zayıf; akademik çalışmalar yasağa rağmen yaygın loot box buldu | Yok | B/O | [35][36] |
| **Hollanda** | KSA 2018'de transfer edilebilir ödüllü paketleri kumar saydı. Danıştay 9 Mart 2022'de EA'ya kesilen 10 milyon €'luk cezayı bozdu (ECLI:NL:RVS:2022:690) | Hükümet AB düzeyinde yasak için çalışıyor | Yok | B/O | [37][36] |
| **Birleşik Krallık** | DCMS (Temmuz 2022): yasa yok, sektörün öz-düzenlemesi. Ukie'nin 11 ilkesi (Temmuz 2023): 18 yaş altına ebeveyn onayı olmadan satış engeli (teknik kontrol), olasılık açıklaması vb. | Uyum düzeyi tartışmalı | Yok | B/O | [38][39] |
| **Brezilya** | ECA Digital (Kanun 15.211/2025): reşit olmayanlara yönelik veya onların erişebildiği oyunlarda ücretli loot box yasak. Ceza 50 milyon BRL'ye veya Brezilya gelirinin %10'una kadar. Yaş doğrulama ve ebeveyn araçları gibi geniş yükümlülükler de getiriyor | İmza Eylül 2025, **yürürlük 17 Mart 2026** | Loot box yoksa asıl risk ortadan kalkar. Genel çocuk koruma yükümlülükleri (yaş doğrulama/ebeveyn araçları) Brezilya çıkışı öncesi hukukçuya kontrol ettirilmeli | R/Y | [29][30] |
| **Brezilya (Apple)** | Yaş derecelendirme anketinde loot box beyan eden uygulama Brezilya mağazasında **18+ (A18)** olur | 24 Şubat 2026 | Mobil sürüm için önemli | **C/Y** | [24][23] |
| **Avustralya** | Sınıflandırma kuralı: ücretli loot box'lı oyunlar en az **M**, simüle kumar içeren oyunlar **R18+** alır | 22 Eylül 2024 | **Simüle kumar ücretsiz olsa bile R18+.** Kasabadaki "kumarhane" mini oyunu bu yüzden risk | B/Y | [32] |
| **Avustralya (Apple)** | Loot box → 16+ (18 Haziran 2026'dan itibaren; önceden 15+). Simüle kumar → R18+ | 2024 / 2026 | Mobil sürüm için önemli | **C/Y** | [25][26][23] |
| **Çin** | Olasılıkları açıklama zorunluluğu (Kültür Bakanlığı genelgesi) | Yürürlük 1 Mayıs 2017. Aralık 2023'te NPPA harcama ve ödül sınırları taslağı yayımladı, piyasa tepkisi sonrası geri çekildi veya revize edildi (kesin durum D) | Çin'de resmî yayın için ayrıca ISBN lisansı gerekir. Global Steam üzerinden satış bu kapsamda değil (D) | B/O | [36] |
| **Japonya** | "Kompu gacha" (set tamamlama gacha'sı), Tüketici İşleri Ajansı yorumuyla Haksız Primler ve Yanıltıcı Beyanlar Kanunu kapsamında yasak. JOGA öz-düzenlemesi ile olasılık gösterimi | 2012 | Yok | B/Y | [40] |
| **Güney Kore** | Oyun Endüstrisi Kanunu değişikliği: olasılıklı öğelerin oranlarını oyunda, web sitesinde ve reklamlarda açıklamak zorunlu. GRAC denetliyor. İspat yükünü yayıncıya geçiren ve 3 kata kadar tazminat getiren değişiklik Ocak 2025'te kabul edildi, 1 Ağustos 2025'te yürürlüğe girdi (düzeltildi 24.09.2026). KFTC Ocak 2024'te Nexon'a ~11,6 milyar ₩ ceza verdi (B/O) | 22 Mart 2024 | Yok. Apple Kore'de GRAC numarasıyla yaş sınıfı geçersiz kılmaya izin veriyor [28] | R/Y | [31][28] |
| **AB – CPC ağı** | Oyun içi sanal para birimleri için ilkeler: fiyatlar gerçek para karşılığıyla açıkça gösterilmeli, gereksiz para birimi alımına zorlanmamalı, çocuklara doğrudan satın alma çağrısı yapılmamalı vb. Star Stable'a karşı koordineli eylem | Mart 2025 | Premium para birimi kullanmazsak etkisi yok | B/O | [41] |
| **AB – Digital Fairness Act** | Karanlık desenler (dark patterns), bağımlılık yaratan tasarım, sanal para birimi ve loot box'ı kapsaması beklenen yasa teklifi. Kamuoyu danışması Temmuz–24 Ekim 2025 | **24 Eylül 2026 itibarıyla teklif yayımlanmadı.** Komisyon 2026 çalışma programı: 2026'nın 4. çeyreği (düzeltildi 24.09.2026) | Yok ya da düşük | R/O | [42] |
| **AB – Parlamento** | Reşit olmayanların çevrimiçi korunması raporunda, reşit olmayanlar için loot box ve kumar benzeri mekaniklerin yasaklanması çağrısı (Kasım 2025, bağlayıcı değil) | — | Yok | B/D | — |
| **ABD – FTC v. HoYoverse (Cognosphere)** | 20 milyon $ ceza. 16 yaş altına ebeveyn izni olmadan loot box satışı yasak. Olasılıklar ve sanal para biriminin gerçek para karşılığı açıklanmalı. COPPA ihlali nedeniyle çocuk verileri silinmeli | 17 Ocak 2025 | Yok. COPPA (13 yaş altı verisi) yine geçerli | B/Y | [33] |
| **ABD – FTC v. Epic** | Toplam 520 milyon $ (275 milyon $ COPPA cezası + 245 milyon $ karanlık desen iadesi) | Aralık 2022 | Satın alma arayüzünde karanlık desen kullanılmamalı | B/Y | [34] |
| **Apple** | 3.1.1: Rastgele sanal öğe satan uygulamalar, satın almadan önce her öğe türünün olasılığını göstermek zorunda | Kılavuz son güncelleme 8 Haziran 2026 | Yok | **C/Y** | [22] |
| **Google Play** | Ödeme politikası: rastgele öğe satan uygulamalar olasılıkları satın almadan önce ve satın alma anına yakın göstermeli | Yürürlükte | Yok | B/O | [9] |
| **Steam** | Global bir olasılık açıklama kuralı bilinmiyor (D). Blokzincir/NFT/kripto oyunlar yasak (Ekim 2021). Temmuz 2025'ten beri "ödeme işlemcilerinin ve kart ağlarının kurallarını ihlal edebilecek" içerik (özellikle bazı yetişkin içerikler) yasak | 2021 / 2025 | Fan servisi dozu, ödeme işlemcisi kuralına göre ayarlanmalı | B/O | [47] |
| **PEGI / ESRB / USK** | PEGI ve ESRB 2020'den beri "In-game Purchases (includes random items)" etiketini kullanıyor. USK, Ocak 2023'ten beri gençlik koruma kanunu (JuSchG) gereği etkileşim risklerini (satın alma, rastgele öğe) değerlendirip yaş sınırını yükseltebiliyor. **PEGI, Haziran 2026'dan itibaren yeni başvurularda:** ücretli rastgele öğe → en az PEGI 16; süreli/adet sınırlı satın alma teklifi → en az PEGI 12; NFT/blokzincir → PEGI 18; engelleme/raporlama/filtre olmadan sınırsız çevrimiçi iletişim → PEGI 18. Eski dereceler yeniden derecelendirilmez (düzeltildi 24.09.2026) | 2020 / 2023 / Haziran 2026 | DLC varsa yalnızca "In-game purchases". Oyun içinde süreli teklif olmaması ve (ileride co-op gelirse) sohbette engelleme/raporlama aracı bulunması PEGI 12/16 hedefini korur. Konsolda dijital satış için IARC derecelendirmesi ücretsiz (B/O) | B/O; PEGI 2026: R/Y | [44][45][46] |
| **Türkiye** | Loot box'a özel kural bulunamadı (D). Kumar ve şans oyunları için 7258 sayılı Kanun ve TCK md. 228 var. Roblox'a Ağustos 2024'te, Discord'a Ekim 2024'te çocuk koruma gerekçesiyle erişim engeli getirildi. Çocuklar ve sosyal medya için yaş sınırı tartışmaları sürüyor (D) | — | Ücretli rastgelelik ve kumarhane teması olmazsa risk düşük. Sosyal ve çevrimiçi özelliklerde çocuk koruma önlemleri alınmalı | B/O–D | [50][51][52] |

**Sonuç:** Ücretli rastgele öğe sunmamak, bu tablodaki 15'ten fazla yargı alanındaki riskin neredeyse tamamını tek kararla ortadan kaldırıyor. Bu kararla Brezilya'da 18+ ve Avustralya'da 16+/M etiketi almaktan, Kore'deki olasılık yükümlülüğünden ve FTC tipi davalardan kaçınılıyor. Pazarlamada **"Gacha yok. Enerji yok. Güç satılmıyor."** bir satış argümanına dönüşüyor.

---

## 5. Türkiye'ye Özgü: Fiyatlandırma, Vergiler ve Yasal İklim

| Konu | Bilgi | Etiket | Kaynak |
|---|---|---|---|
| **Steam Türkiye fiyatlandırması** | Valve, 20 Kasım 2023'ten itibaren Türkiye (ve Arjantin) için yerel para birimi desteğini kaldırdı. Türkiye "MENA – USD" bölgesine geçti; oyunlar USD ile fiyatlanıyor | B/Y | [49] |
| **Bölgesel fiyat önerisi** | Steam her para birimi ve bölge için önerilen fiyat tablosu sunuyor. MENA-USD önerisi ABD fiyatının belirgin biçimde altında (tam oran bu oturumda doğrulanamadı) | B/D | [49] |
| **Apple Türkiye fiyatları** | Apple, Türkiye mağazası fiyatlarını kur nedeniyle defalarca güncelledi (Aralık 2024, 17 Kasım 2025) | **C/Y** | [72][73] |
| **Dijital Hizmet Vergisi (DHV)** | 7194 sayılı Kanun ile getirildi (%7,5). Apple bildirimine göre **oran %5'e indi** ve Apple 29 Ocak 2026'dan itibaren geliştirici hasılatını buna göre düzeltiyor. 10767 sayılı CK: 1 Ocak 2026'dan itibaren %5, 1 Ocak 2027'den itibaren %2,5. Eşikler: Türkiye hasılatı 20 milyon TL ve küresel hasılat 750 milyon € (düzeltildi 24.09.2026). Vergiyi büyük platformlar öder; küresel ciro eşikleri nedeniyle indie geliştiriciyi doğrudan ilgilendirmez. Steam'in bunu geliştiriciye yansıtıp yansıtmadığı D | C/Y (oran), B/O (eşikler) | [27][50] |
| **KDV** | Türkiye'de genel oran %20 (Temmuz 2023'ten beri). Steam, KDV'yi toplayan taraf olarak raporlarda satıştan düşüyor (B/O) | B/O | [58] |
| **Kumar mevzuatı** | 7258 sayılı Kanun ve TCK md. 228. Oyun içi ücretli şans mekaniğine özel emsal bulunamadı (D) | B/O | [51] |
| **Çocuk koruma ve erişim engeli** | Roblox (7 Ağustos 2024) ve Discord (Ekim 2024) erişim engelleri → sosyal ve UGC özellikleri olan oyunlar için ölçülebilir bir risk | B/Y | [52] |

**Çıkarım:** Türkiye pazarı gelirden çok **topluluk, PR ve yerel basın** için önemli. Steam'in USD bazlı önerilen bölgesel fiyatı kullanılmalı, ama TL alım gücü nedeniyle Türkiye'den gelen gelir sınırlı kalacak. Türkçe tam dublaj yerine kaliteli altyazı ve yerelleştirme yeterli (02 raporuyla uyumlu).

---

## 6. Türkiye Merkezli Indie İçin İş Kurulumu

### 6.1 Steamworks kurulum adımları

1. Steamworks hesabı açılır, tüzel veya şahıs kimliği girilir, banka bilgisi eklenir.
2. **Vergi mülakatı (tax interview)** doldurulur:
   - Şahıs için **W-8BEN**, şirket (Ltd/AŞ) için **W-8BEN-E**.
   - Formda Türk vergi kimlik numarası (TCKN veya VKN) ve ABD–Türkiye anlaşması beyan edilir.
   - Bu yapılmazsa Valve ABD kaynaklı ödemelerde %30 stopaj uygular [55][56] [B/Y].
3. **Anlaşma oranı:** ABD–Türkiye Çifte Vergilendirmeyi Önleme Anlaşması (1996, yürürlük 1997), md. 12 telif ödemeleri. Endüstriyel, ticari veya bilimsel ekipman kirası için %5, **diğer telifler için %10**. Valve, Steam gelirini telif olarak ele alıyor ve stopajı yalnızca ABD'deki satışlara uyguluyor [53][54][56] [B/O].
4. **Kimlik doğrulama → Steam Direct ücreti (100 $) → 30 günlük bekleme → Coming Soon sayfası (en az 2 hafta) → yayın** [2] [B/Y].
5. **Ödemeler:**
   - Aylık yapılır, ay kapanışından yaklaşık 30 gün sonra, 100 $ eşiği aşılınca.
   - USD olarak banka havalesiyle (SWIFT) gelir. Türk bankasında USD hesabı (IBAN) gerekir; hesap adı, Steamworks'teki kişi veya şirket adıyla aynı olmalı [57] [B/O].
   - Gelen SWIFT masrafları ve (varsa) döviz dönüşüm kuralları bankayla teyit edilmeli (D).

### 6.2 Şahıs şirketi mi, Limited mi?

| Kriter | Şahıs şirketi | Limited şirket |
|---|---|---|
| Kuruluş maliyeti ve süresi | Düşük, hızlı | Daha yüksek. **Asgari sermaye 50.000 TL** (2024'ten beri) [58] B/O |
| Gelir/kurumlar vergisi | Artan oranlı gelir vergisi **%15–40** [58] B/Y | **Kurumlar vergisi %25** (7456 sayılı Kanun, 2023) [58] B/Y + dağıtılan kâr payında **%15 stopaj** (Aralık 2024'ten beri) [58] B/O. 2025'ten itibaren %10 yurt içi asgari kurumlar vergisi (B/O) |
| Sorumluluk | Sınırsız (kişisel varlıklar) | Sermaye ile sınırlı |
| Teşvik erişimi | Genç girişimci istisnası (GVK mük. md. 20: 29 yaş altı, ilk kez işe başlayanlara 3 yıl, tarifenin 2. dilim tutarına kadar; **2026 için 400.000 TL**). Genç girişimcinin Bağ-Kur prim desteği (5510 md. 81/1-k), 1 Ocak 2026'dan sonra işe başlayanlar için 7566 sayılı Kanun'la **kaldırıldı** (düzeltildi 24.09.2026) [58] | **Teknokent** (4691 sayılı Kanun) muafiyetleri, TÜBİTAK ve yatırımcı/yayıncı anlaşmaları için daha uygun [59][60] B/O |
| Yayıncı ve platform anlaşmaları | Mümkün, ama bazı taraflar şirket ister | Tercih edilir |
| Ne zaman? | Gelir öncesi veya ilk yıl, düşük gelirde | Yıllık kâr üst gelir dilimlerine yaklaştığında, yatırımcı/yayıncı/teknokent planlandığında |

**Vergi notları (hepsi mali müşavirle teyit edilmeli):**
- **Hizmet ihracatı:** Valve'a verilen lisans veya hizmet için KDV istisnası (KDVK 11/1-a) uygulanabilir. Yurt dışına verilen yazılım hizmetlerinde kazanç indirimi (GVK 89/13, KVK 10/1-ğ) oranı 2025'te %80 idi; 11257 sayılı Cumhurbaşkanı Kararı (Nisan 2026) ile **1 Ocak 2026'dan başlayan dönemler için %100**. Şartlar: hizmetten münhasıran yurt dışında yararlanılması, faturanın yurt dışındaki müşteri adına kesilmesi, kazancın beyanname tarihine kadar Türkiye'ye getirilmesi. Steam'deki oyun satışının (Valve'a telif/lisans) "yazılım hizmeti" sayılıp sayılmayacağı **belirsiz; mali müşavir/özelge gerekir** (düzeltildi 24.09.2026) [58].
- **GVK md. 18 (eser satışı / serbest meslek kazancı istisnası):** Bilgisayar programcılarının eserlerini satış, devir ve kiralamasından elde ettikleri hasılatı kapsar. **Tutar sınırı var:** istisna kapsamındaki gelir, gelir vergisi tarifesinin 4. dilim tutarını (**2026: 5.300.000 TL**) aşarsa beyan edilir. Ticari organizasyonla yapılan satışta kazanç ticari kazanç sayılabildiği için Steam gelirine uygulanabilirliği **mali müşavir ve özelgeyle** netleştirilmeli (düzeltildi 24.09.2026) [58].
- **ABD'de kesilen %10 stopaj**, Türkiye'de hesaplanan vergiden mahsup edilebilir (GVK md. 123 / KVK md. 33, sınırları dahilinde) [58] B/O.
- **Faturalama:** Valve'a aylık ödemeler için e-Arşiv veya ihracat faturası düzenleme yöntemi mali müşavirle belirlenmeli (D).

### 6.3 Olası Türkiye teşvikleri

| Program | Özet | Etiket | Kaynak |
|---|---|---|---|
| **Teknoloji Geliştirme Bölgeleri (Teknokent)** | Bölgede geliştirilen yazılım ve Ar-Ge kazancına gelir/kurumlar vergisi istisnası (**31.12.2028'e kadar**), Ar-Ge personeli ücretlerinde gelir vergisi ve SGK teşvikleri, belirli yazılım satışlarında KDV istisnası. Şirket ve proje onayı gerekir. Oyunların kapsama nasıl alındığı teknokente göre değişir (D) | B/O | [59] |
| **TÜBİTAK 1512 BiGG** | Aşamalı bireysel girişim programı; hibe + iş planı desteği. Güncel tutar D | B/O | [60] |
| **KOSGEB Girişimcilik Destek Programı** | Uygulamalı Girişimcilik Eğitimi sertifikası → yeni girişimci/iş kurma desteği. Güncel tutar D | B/O | [61] |
| **Ticaret Bakanlığı – Hizmet ihracatı destekleri** | Bilişim ve dijital oyun firmalarına pazarlama, tanıtım, yerelleştirme ve fuar katılımı gibi harcama destekleri (kapsam ve oranlar D) | B/D | [62] |
| **Kalkınma ajansları ve oyun hızlandırıcıları** | Dönemsel çağrılar (D) | D | — |

### 6.4 Kitle fonlaması

- **Kickstarter:**
  - Platform ücreti %5, ödeme işleme ücreti ~%3–5 [63] B/Y.
  - **Proje sahibi olarak Türkiye desteklenen ülkeler arasında değil** [63] B/O. Yabancı bir tüzel kişilik veya ortak olmadan kullanılamaz.
  - Ayrıca Kickstarter'da başarı, zaten var olan bir topluluğa bağlı.
- **Patreon:**
  - Türkiye'den kullanılabiliyor.
  - Ağustos 2025'ten sonra katılan yeni içerik üreticileri için standart platform ücreti %10, artı ödeme işleme ücreti [64] B/O.
  - Devlog, sanat ve beta erişimi için küçük ve düzenli gelir sağlar. **Ana finansman olarak görülmemeli.**

### 6.5 Yayıncı anlaşması: kontrol listesi

Tipik yapı: geri ödenebilir avans + gelir paylaşımı. Avans geri ödendikten sonra geliştiriciye ~%50–70 kalır (sektör sezgisi, D). Masaya oturmadan önce şunlar netleşmeli:

- IP sahipliği mutlaka **geliştiricide** kalmalı.
- Süre ve bölge sınırlı olmalı (ör. 5–7 yıl, yalnızca konsol ya da yalnızca Asya).
- Devam oyunu ve uyarlama hakları kapsam dışı tutulmalı.
- Denetim (audit) hakkı sözleşmede yer almalı.
- Pazarlama taahhüdü yazılı ve rakamla belirtilmeli.
- Kilometre taşı (milestone) ödemeleri tanımlanmalı.
- Yayıncı geri çekilirse hakların geri dönüşü güvenceye alınmalı.

**Öneri:** Steam PC sürümünü kendin yayımla. Yayıncı veya port partnerini **konsol + Japonya/Çin yerelleştirme ve pazarlaması** için, istek listesi verisi elindeyken, güçlü pozisyondan seç.

---

## 7. Önerilen Monetizasyon Stratejisi

### 7.1 İlkeler

1. **Ücretli rastgelelik yok, güç satışı yok, enerji/stamina yok, premium para birimi yok.** Oyun içindeki rastgele ödüller ("Sistem Ödül Kutusu", zindan loot'u) yalnızca oynayarak kazanılır ve hiçbir ücretli kaynağa bağlanmaz.
2. **Satış anı oyun dışında olur.** Mağaza ve DLC sayfası ana menüde durur. Hikâye, zindan veya ara sahne içinde asla teklif gösterilmez; isekai sürükleyiciliği korunur.
3. **Oynama süresi = inceleme = satış.** Tutundurma, "Sistem" günlük görevleri (FOMO'suz, kaçırılan görev telafi edilebilir), meta ilerleme, ilişki sistemleri ve ev dekorasyonu ile sağlanır. Bu tutundurma paraya çevrilmez, Steam algoritmasına ve ağızdan ağıza yayılmaya yakıt olur.

### 7.2 Gelir akışları ve zaman çizelgesi

| Faz | Zaman | Birincil / ikincil | İçerik | Fiyat (ABD) |
|---|---|---|---|---|
| 0 | Çıkıştan 12–18 ay önce | — | Steam sayfası, istek listesi, ücretsiz demo veya "Prolog: Varış Günü", Next Fest (Şubat/Haziran/Ekim). Not: Next Fest'e yalnızca ana oyun, bir kez ve EA/çıkıştan önce katılabilir; ayrı uygulama olarak yayımlanan prolog/"Bölüm 1"/kısa önizleme Next Fest'e kabul edilmez (düzeltildi 24.09.2026) | Ücretsiz |
| 1 | EA çıkışı | **Birincil** | Perde 1 + tam çekirdek döngü (zindan/Kapı + şehir + Sistem). Ana hikâye sonu EA'da verilmez. EA süresi 9–15 ay | **19,99 $** |
| 2 | 1.0 | **Birincil** | Tam hikâye. EA alıcıları en iyi fiyatı almış olur. **Steam kuralı: herhangi bir fiyat artışından sonraki 30 gün hiçbir indirim yapılamaz; bu 1.0 çıkış indirimini (launch discount) de kapsar ve istisnası yok.** Bu yüzden fiyat 24,99 $'a 1.0'dan **en az 30 gün önce** yükseltilmeli, 1.0'da %10–15 çıkış indirimi (7–14 gün, en fazla %40) yapılmalı. Alternatifler: 1.0'da fiyatı artırıp indirim yapmamak ya da 1.0'da eski fiyatla indirim yapıp fiyatı 30 gün sonra artırmak (düzeltildi 24.09.2026) | **24,99 $** |
| 2 | 1.0 ile birlikte | İkincil | **Destekçi Paketi / Deluxe**: OST + dijital artbook + 2–3 kozmetik set + "Sistem" arayüz teması + kredilerde isim. **Oyun avantajı yok** | +9,99 $ (paket halinde) |
| 2 | 1.0 ile birlikte | İkincil | **OST** (Steam Soundtrack; ayrıca Bandcamp ve dijital müzik dağıtımı) | 7,99–9,99 $ |
| 3 | 1.0 + 2–9 ay | İkincil | **Kozmetik DLC**: kıyafet setleri (ör. "Dünya'dan getirilen okul üniforması"), ev/lonca dekorları. İçerik önceden görülür, rastgele değil | 2,99–4,99 $ |
| 3 | Sürekli | — | **Ücretsiz güncellemeler**: yeni zindan katları, etkinlikler, yaşam kalitesi iyileştirmeleri. İncelemeleri ve algoritmayı canlı tutar | Ücretsiz |
| 4 | 1.0 + 9–15 ay | **İkincil (en büyük)** | **Ücretli genişleme**: yeni kıta, yeni "Kule/Kat" arkı, yeni yoldaş | 12,99–14,99 $ |
| 4 | Genişleme ile | — | **Complete Edition** paketi, indirimlerde "Complete the set" | Paket |
| 5 | 1.0 + 12–24 ay | İkincil | **Konsol** (PS5/Xbox/Switch 2) port partneri veya yayıncıyla. Steam Deck Verified hedefi ilk günden | Konsol fiyatı |
| 5 | Hit sinyalinden sonra | Fırsatçı | Mobil premium port (Apple/Google %15 [8][9]), fiziksel sürüm ve merch (partner), manga/webtoon lisansı | — |
| — | Sürekli | Küçük | Patreon/Ko-fi (devlog, erken sanat), itch.io destek sayfası | — |

**Early Access koşulu:** EA ancak çekirdek döngü tek başına eğlenceliyse ve ilk 2–3 saatte "isekai'ye düştüm" hissi tam veriliyorsa açılmalı. Aksi hâlde doğrudan 1.0 + güçlü demo tercih edilmeli. EA'da vaat edilen her özellik yazılı yol haritasında olmalı (Steam EA kuralları) [B/O].

**Fiyat mekaniği:**
- Steam'in önerdiği bölgesel fiyatlar kullanılmalı (Türkiye, LATAM, BDT, Güney/Güneydoğu Asya).
- EA→1.0 fiyat artışı, bir sonraki indirim takvimi Steam'in bekleme kurallarına uygun olacak şekilde planlanmalı [18]. Steam kuralları: çıkıştan (EA ve 1.0 ayrı ayrı) sonraki 30 gün indirim yok (tek istisna önceden ayarlanan çıkış indirimi); fiyat artışından sonraki 30 gün **hiçbir** indirim yok, çıkış indirimi ve sezonluk indirimler dahil; iki indirim arasında 30 gün (sezonluk indirimler bu kuraldan muaf). Fiyat artışı 1.0'dan en az 30 gün önce yapılmalı ve sezonluk indirim takvimiyle çakıştırılmamalı (düzeltildi 24.09.2026).
- Tüm mağazalarda fiyat ve içerik eşitliği korunmalı (Steam anahtar kuralları) [B/O].

---

## 8. Gelir Senaryoları (24,99 $ premium PC oyunu, ilk 24 ay)

### 8.1 Varsayımlar (hepsi varsayımdır, ölçülmüş veri değildir)

| # | Varsayım | Değer | Dayanak |
|---|---|---|---|
| A1 | ABD liste fiyatı | 24,99 $ | §7 |
| A2 | Gerçekleşen ortalama birim hasılat (bölgesel fiyat, indirimler ve KDV/satış vergisi sonrası) | Liste fiyatının %60'ı = **14,99 $** | Sektör sezgisi, D |
| A3 | İade oranı | %8 | D |
| A4 | Steam payı | %30 (10 milyon $ altında kalınıyor) | [1] |
| A5 | ABD stopajı | Satışların ~%30'u ABD'den × %10 = toplamda ~%3 | [53][56], D |
| A6 | DLC + OST + destekçi paketi ek geliri | Temel oyun netinin %5 / %10 / %15'i | D |
| A7 | Kapsam dışı | Pazarlama, seslendirme, yerelleştirme ve port maliyetleri; Türkiye vergileri; kur farkı | — |

**Birim başına geliştiriciye kalan:** 24,99 × 0,60 × 0,92 × 0,70 × 0,97 ≈ **9,37 $** (liste fiyatının ~%37'si).

### 8.2 Senaryo tablosu

| Senaryo | Çıkışta istek listesi | İlk hafta satış (istek listesinin %10–20'si; 10 $ üstü oyunlarda medyan %10, yani alt sınır medyan, üst sınır iyimser — düzeltildi 24.09.2026) | 24 ayda toplam satış | Steam hasılatı (A2 bazında) | Temel oyundan net | Ek gelir | **Toplam net (vergi öncesi)** | Beklenen inceleme sayısı (Boxleiter 30–40×) |
|---|---|---|---|---|---|---|---|---|
| Başarısız (Steam medyanı civarı [13]) | < 2 bin | < 300 | < 1.000 | < 15 bin $ | < 9,4 bin $ | ~0 | **< 10 bin $** | < 30 |
| **Kötümser** | ~10 bin | 1–2 bin | **5.000** | ~75 bin $ | ~46,8 bin $ | +%5 ≈ 2,3 bin $ | **~49 bin $** | ~125–170 |
| **Temel** | ~75 bin | 7,5–15 bin | **50.000** | ~750 bin $ | ~468 bin $ | +%10 ≈ 47 bin $ | **~515 bin $** | ~1.250–1.700 |
| **İyimser** | ~350 bin | 35–70 bin | **400.000** | ~6,0 milyon $ | ~3,75 milyon $ | +%15 ≈ 562 bin $ | **~4,3 milyon $** | ~10–13 bin |

**Fiyat duyarlılığı** (talep esnekliği yok sayılarak, temel senaryo 50 bin kopya):
- 19,99 $ → birim başına ~7,49 $ → ~375 bin $
- 29,99 $ → birim başına ~11,24 $ → ~562 bin $

**Bağlam:**
- Temel senaryo (50 bin kopya), 2025 Steam çıkışlarının kabaca üst %5–8'lik dilimine denk geliyor [13].
- Dünyanın en büyük isekai IP'si ile yapılan 39,99 $'lık Overdrive ilk hafta ~127 bin (tahmin) sattı [21].
- İyimser senaryo, Hades II veya MiSide tipi bir "özgün hit" gerektirir [R]. Planlama ve bütçe **kötümser senaryoda bile batmayacak** şekilde yapılmalı.
- 02 raporundaki aralıklarla (5–20 bin / 50–150 bin / 500 bin+) uyumlu, biraz daha muhafazakâr noktalar seçildi.

---

## 9. Yapılmaması Gerekenler

1. **Ücretli loot box, gacha veya "gizemli kutu" DLC'si satmak.** Ücretli para birimiyle rastgele öğe almak da buna dahil. Sonuç: Brezilya yasağı, Kore yükümlülükleri, Belçika riski, Apple'da 18+/16+ yaş sınırı [24][25][29][31][35].
2. **Premium para birimi, uyumsuz paket boyları, gerçek fiyatı gizlemek.** Bunlar AB CPC ilkelerine ve FTC HoYoverse kararına aykırı [33][41].
3. **Premium oyunda enerji veya stamina, "hızlandırıcı" satışı, XP/stat boost satışı.** Pay-to-win algısı incelemeleri öldürür.
4. **Ara sahnelerin veya zindanın ortasında satış pop-up'ı, süreli FOMO teklifleri, çocuklara doğrudan "satın al" çağrısı** [67][41].
5. **Kumarhane, rulet veya slot mini oyunu.** Ücretsiz olsa bile Avustralya'da R18+ derecesi getirir [26][32]. İsekai kasabasındaki "kumarhane" klişesinden kaçınılmalı.
6. **NFT, kripto veya blokzincir öğeleri.** Steam'de yasak [47].
7. **Ödeme işlemcisi kurallarını zorlayan cinsel içerik.** Temmuz 2025 Steam kuralı [47]. Fan servisi dozu yaş derecesi hedefiyle (PEGI 12/16) uyumlu tutulmalı.
8. **Üretken yapay zekâ kullanımını beyan etmemek** (Steam formu) [48].
9. **İçeriği belirsiz sezon bileti veya ön sipariş satmak, EA'da tutulamayacak vaatler vermek.**
10. **Sahte indirim ya da indirim öncesi fiyat şişirmek, mağazalar arasında Steam aleyhine fiyat veya içerik farkı yaratmak** [18].
11. **Tek oyunculu içerik için sürekli çevrimiçi zorunluluğu veya sunucu bağımlılığı koymak.** Oyunun "kapanma" (end-of-service) riski doğar ve AB'deki "Stop Killing Games" vatandaş girişimi ile uyumsuz düşer [43].
12. **Teşvikli (ödüllü) inceleme istemek, inceleme manipülasyonu yapmak.**
13. **Türkiye'den doğrudan Kickstarter açmaya çalışmak** (desteklenmiyor) veya demo olmadan kitle fonlaması yapmak [63].
14. **IP'yi devreden ya da süresiz, dünya çapında tüm hakları veren yayıncı sözleşmesi imzalamak.**
15. **Vergi mülakatını ertelemek.** Bu durumda %30 stopaj uygulanır [56].

---

## Oyunumuz İçin Çıkarımlar

1. **Model kararı (kesin):** Premium B2P. EA 19,99 $ → 1.0 24,99 $ (fiyat artışı 1.0'dan en az 30 gün önce yapılmalı, yoksa 1.0 çıkış indirimi uygulanamaz; düzeltildi 24.09.2026). İkincil gelir: Destekçi Paketi (9,99 $), OST (7,99–9,99 $), deterministik kozmetik DLC (2,99–4,99 $), 1.0'dan 9–15 ay sonra ücretli genişleme (12,99–14,99 $). Gacha, loot box, enerji, premium para birimi ve güç satışı yok.
2. **Tasarım ekibine gereksinim:**
   - "Sistem Ödül Kutusu" ve zindan loot'u yalnızca oyun içi eylemle kazanılır. Kod düzeyinde hiçbir mağaza ürünü rastgele tabloya bağlanamaz.
   - Bu kural bir **ADR** (Architecture Decision Record, mimari karar kaydı) olarak yazılmalı.
3. **Yaş derecesi hedefi:** PEGI 12/16 ve ESRB T.
   - Kumarhane mini oyunu yok.
   - Fan servisi ölçülü; açık cinsellik yok.
   - Sonuç: DLC için yalnızca "In-game purchases" etiketi gelir [44].
4. **Satış arayüzü:**
   - Oyun içi mağaza yok; DLC'ler ana menüden Steam sayfasına link verir.
   - Tüm fiyatlar gerçek para biriminde gösterilir.
   - Çocuklara yönelik çağrı dili kullanılmaz (AB CPC uyumu) [41].
5. **Çevrimdışı oynanabilirlik ve sunucusuz tek oyunculu mod** varsayılan olmalı. Co-op varsa P2P ya da Steam Networking kullanılmalı; oyunun ömrü sunucuya bağlanmamalı [43].
6. **İş kurulumu:**
   - Gelir öncesi dönemde **şahıs şirketi** yeterli: genç girişimci istisnası (2026: 400.000 TL; Bağ-Kur prim desteği 2026'da yeni başlayanlar için kalktı), GVK 18 (2026 sınırı 5.300.000 TL) ve %100 hizmet ihracatı kazanç indiriminin Steam gelirine uygunluğu mali müşavirle incelenmeli (düzeltildi 24.09.2026).
   - Steamworks'te W-8BEN ile %10 anlaşma oranı beyan edilmeli.
   - EA/1.0 gelirleri 100 bin $'ı aşma eğilimi gösterdiğinde **Limited + teknokent** yapısına geçiş planlanmalı.
7. **Kitle fonlaması:** Kickstarter yok. Patreon/Ko-fi yalnızca devlog ve topluluk için. Finansmanın asıl kaynakları: kişisel bütçe, TÜBİTAK BiGG/KOSGEB (başvuru uygunsa), ileride konsol ve Asya için yayıncı veya port partneri.
8. **Pazarlama mesajı:** "Gacha yok, enerji yok, satın alınabilir güç yok; bir kere al, isekai hayatını yaşa." 2025–2026'daki gacha yorgunluğu ortamında bu, farklılaştırıcı bir vaat [69][R].
9. **Yerelleştirme ve bölge:**
   - Brezilya (Portekizce) gelir için anlamlı, ama ECA Digital'in yaş doğrulama ve ebeveyn araçları yükümlülükleri çıkış öncesi hukuken kontrol edilmeli [29].
   - Kore ve Japonya'da ücretli rastgelelik olmadığı için ek yük yok.
10. **Finansal planlama:** Bütçe **kötümser senaryoya (~50 bin $ net)** göre kurulmalı. Temel senaryo (~500 bin $) tam zamanlı devam ve genişleme için yeterli; iyimser senaryo stüdyolaşmayı mümkün kılar.
11. **Motor seçimine etkisi:** Telif açısından Godot 0, Unity Personal 0 (~200 bin $ gelir sınırına kadar), Unreal %5 (1 milyon $ sonrası). İyimser senaryoda Unreal telifi ~150–200 bin $ eder. Bu kalem motor kararında (başka rapor) dikkate alınmalı [10][11][12].

## Belirsizlikler ve Riskler

- **Doğrulama açığı:** Bu raporun büyük kısmı [B] etiketli. Steam, FTC, AB, GİB ve Resmî Gazete sayfaları bu oturumda açılamadı ve arama kotası bitmişti. Canlı doğrulanabilenler Apple kaynakları [C] ve 02 raporundan aktarılanlar [R] ile sınırlı. **Doğrulayıcı öncelik sırası:**
  1. Steam gelir payı ve Direct ücreti
  2. ABD–Türkiye telif stopaj oranı
  3. GVK 18 ve hizmet ihracatı istisnaları
  4. Kickstarter'ın Türkiye durumu
  5. Epic'in ilk 1 milyon $'da %0 kuralı
  6. DFA'nın durumu
- **AB Digital Fairness Act:** Teklifin kapsamı ve tarihi belirsiz. Bizi etkileyebilecek başlıklar abonelik iptali, kişiselleştirilmiş fiyatlandırma ve bağımlılık yaratan tasarım. Premium modelde etkinin düşük olması beklenir.
- **Brezilya ECA Digital'in geniş kapsamı:** Loot box dışında yaş doğrulama, ebeveyn denetimi ve varsayılan gizlilik yükümlülükleri, "reşit olmayanların erişebileceği" her dijital ürüne uygulanabilir. Uygulama yönetmelikleri ve yaptırım pratiği izlenmeli [29].
- **Türkiye vergi detayları:** GVK 18 tutar sınırı, hizmet ihracatı indirim oranı, genç girişimci istisnası tutarı, teknokentte oyunun kapsama girip girmediği, döviz dönüşüm kuralları ve Valve'a fatura yöntemi **doğrulanamadı**. Mali müşavir ve teknokent yönetimiyle görüşülmeli.
- **Türkiye'de çocuk koruma ve dijital düzenleme iklimi:** Erişim engelleri ve olası yaş sınırı yasaları, sosyal, UGC veya sohbet özellikleri içeren oyunları etkileyebilir. Tek oyunculu ve moderasyonsuz sohbet içermeyen tasarım bu riski azaltır.
- **Kıyas verilerinin oynaklığı:** İstek listesi dönüşümü, Boxleiter çarpanı ve iade ile DLC oranları türe ve fiyata göre 2–3 kat sapabilir. Senaryo tablosu karar desteği içindir, tahmin değildir.
- **Kur riski:** Gelir USD, giderler kısmen TL. Apple'ın Türkiye fiyatlarını sık güncellemesi TL oynaklığını gösteriyor [72][73].
- **Platform politika değişiklikleri:**
  - Steam'in Temmuz 2025 içerik kuralı gibi ani değişiklikler olabiliyor [47].
  - Yapay zekâ beyan formu güncellenebiliyor [48].
  - AB AI Act'in şeffaflık yükümlülükleri (md. 50) 2 Ağustos 2026'dan itibaren uygulanıyor. Digital Omnibus (Tüzük 2026/1744, yürürlük 27 Temmuz 2026) md. 50'yi ertelemedi; yalnızca 2 Ağustos 2026'dan önce piyasaya sürülmüş sistemlere md. 50(2) işaretleme için 2 Aralık 2026'ya kadar süre verdi (düzeltildi 24.09.2026) [71]. Ayrıntı 10 raporu §6.4'te.
- **"Stop Killing Games" girişimi:** 1.294.188 doğrulanmış imzayla 26 Ocak 2026'da Komisyon'a sunuldu. Komisyon 16 Haziran 2026 yanıtında oyunları ticari destek bitince oynanabilir tutma yönünde **yasal zorunluluk önermedi**; 2026 sonuna kadar sektörle gönüllü bir "oyun ömrü sonu" davranış kuralları süreci başlatacak (düzeltildi 24.09.2026) [43]. Kısa vadede yasal yükümlülük yok, ama çevrimdışı tasarım tavsiyesi geçerli.
- **Yayıncı ve konsol anlaşmalarının koşulları gizli.** Rakamlar sektör sezgisidir.

## Kaynaklar

Etiketler: **[C]** bu oturumda açılıp okundu · **[R]** 02 raporunda arama ile doğrulandı · **[B]** bu oturumda açılamadı, model bilgisine dayalı referans.

1. [B] Steam Dağıtım Sözleşmesi gelir payı değişikliği (30 Kasım 2018): https://steamcommunity.com/groups/steamworks/announcements/detail/1697191267930157838
2. [B] Steam Direct ücreti: https://partner.steamgames.com/doc/gettingstarted/appfee
3. [B] Steamworks DLC: https://partner.steamgames.com/doc/store/application/dlc
4. [B] Epic Games Store dağıtım koşulları: https://store.epicgames.com/en-US/distribution
5. [B] GOG geliştirici başvurusu: https://www.gog.com/indie
6. (kullanılmadı)
7. [B] itch.io creator FAQ (open revenue sharing): https://itch.io/docs/creators/faq
8. [C] Apple App Store Small Business Program: https://developer.apple.com/app-store/small-business-program/
9. [B] Google Play hizmet ücretleri: https://support.google.com/googleplay/android-developer/answer/112622 ; Ödeme politikası (loot box olasılıkları): https://support.google.com/googleplay/android-developer/answer/9858738
10. [C] Godot LICENSE (MIT): https://raw.githubusercontent.com/godotengine/godot/master/LICENSE.txt
11. [B] Unreal Engine lisansı: https://www.unrealengine.com/en-US/license
12. [B] Unity fiyatlandırma ve Runtime Fee iptali: https://unity.com/pricing ; https://unity.com/blog/unity-is-canceling-the-runtime-fee
13. [R] Steam 2025 gelir dağılımı ve indie payı: https://gameworldobserver.com/2025/12/22/indie-projects-generated-a-quarter-of-the-total-game-revenue-on-steam-by-the-end-of-2025-analytics ; https://game-developers.org/2025-steam-game-revenue-distribution
14. [B] Chris Zukowski, istek listesi rehberleri: https://howtomarketagame.com/
15. [B] VG Insights, Steam satış tahmini yöntemi: https://vginsights.com/insights/article/how-to-estimate-steam-video-game-sales
16. [B] GameDiscoverCo bülteni: https://newsletter.gamediscover.co/
17. [B] Steam iade politikası: https://store.steampowered.com/steam_refunds/
18. [B] Steamworks indirim kuralları: https://partner.steamgames.com/doc/marketing/discounts
19. [B] Steam Next Fest: https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest
20. [R] Hades II satış ve EA verisi: https://wnhub.io/news/analytics/item-48907 ; https://raijin.gg/app/1145350/Hades_II/sales-revenue
21. [R] Solo Leveling: ARISE OVERDRIVE satış tahmini: https://gamerant.com/solo-leveling-arise-overdrive-player-count-steam-sales-estimate/
22. [C] Apple App Review Guidelines 3.1.1 (son güncelleme 8 Haziran 2026): https://developer.apple.com/app-store/review/guidelines/
23. [C] Apple yaş derecelendirme değerleri ve tanımları (loot box; Brezilya A18, Avustralya 16+/R18+): https://developer.apple.com/help/app-store-connect/reference/app-information/age-ratings-values-and-definitions
24. [C] Apple, Brezilya/Avustralya/Singapur yaş gereklilikleri (24 Şubat 2026; loot box → Brezilya 18+): https://developer.apple.com/news/?id=f5zj08ey
25. [C] Apple, Avustralya ve Vietnam yaş derecesi değişikliği (loot box 15+ → 16+, 18 Haziran 2026): https://developer.apple.com/news/?id=yrrb45pw
26. [C] Apple, Avustralya ve Fransa bölgesel derecelendirmeleri (simüle kumar → R18+, Eylül 2024): https://developer.apple.com/news/?id=4mfp130q
27. [C] Apple fiyat ve vergi güncellemesi (Türkiye DHV %7,5 → %5, 29 Ocak 2026): https://developer.apple.com/news/?id=gvnljl3f
28. [C] Apple, Kore yaş derecesi güncellemesi (GRAC RCN ile geçersiz kılma, 12 Ağustos 2026): https://developer.apple.com/news/?id=oj3r9pvw
29. [R] Mayer Brown, Brezilya ECA Digital yürürlüğü (Nisan 2026): https://www.mayerbrown.com/en/insights/publications/2026/04/enforcement-of-brazils-eca-digital-introduces-new-obligations-for-companies
30. [R] Pixelkin, Brezilya loot box yasağı: https://pixelkin.org/2025/09/29/brazil-becomes-latest-country-to-ban-loot-boxes-targeted-at-minors/
31. [R] Shin & Kim, Kore olasılık açıklama ve ispat yükü: https://www.shinkim.com/eng/media/newsletter/3206
32. [B] Avustralya Sınıflandırma Kurulu, oyun ve kumar içeriği için zorunlu asgari sınıflandırmalar (22 Eylül 2024): https://www.classification.gov.au/
33. [B] FTC, Genshin Impact geliştiricisi ile uzlaşma (17 Ocak 2025): https://www.ftc.gov/news-events/news/press-releases/2025/01/genshin-impact-game-developer-will-be-banned-selling-lootboxes-teens-under-16-without-parental-consent-pay-20-million-fine
34. [B] FTC, Epic Games uzlaşması (Aralık 2022): https://www.ftc.gov/news-events/news/press-releases/2022/12/fortnite-video-game-maker-epic-games-pay-more-half-billion-dollars-over-ftc-allegations
35. [B] Belçika Kansspelcommissie (loot box raporu, Nisan 2018): https://www.gamingcommission.be/
36. [B] Loot box, ülke düzenlemeleri özeti (ikincil): https://en.wikipedia.org/wiki/Loot_box
37. [B] Raad van State, Electronic Arts kararı (ECLI:NL:RVS:2022:690, 9 Mart 2022): https://www.raadvanstate.nl/
38. [B] DCMS, loot box çağrısına hükümet yanıtı (Temmuz 2022): https://www.gov.uk/government/consultations/loot-boxes-in-video-games-call-for-evidence/outcome/government-response-to-the-call-for-evidence-on-loot-boxes-in-video-games
39. [B] Ukie, loot box ilkeleri (Temmuz 2023): https://ukie.org.uk/loot-boxes
40. [B] Gacha oyunları ve kompu gacha yasağı (ikincil özet): https://en.wikipedia.org/wiki/Gacha_game
41. [B] Avrupa Komisyonu basın odası, CPC ağının oyun içi sanal para birimi ilkeleri ve Star Stable eylemi (Mart 2025): https://ec.europa.eu/commission/presscorner/
42. [B] Digital Fairness Act girişim sayfası: https://ec.europa.eu/info/law/better-regulation/have-your-say/initiatives/14622-Digital-Fairness-Act_en
43. [B] Avrupa Vatandaş Girişimi "Stop Destroying Videogames": https://citizens-initiative.europa.eu/initiatives/details/2024/000007_en
44. [B] PEGI etiketleri: https://pegi.info/what-do-the-labels-mean
45. [B] ESRB derecelendirme rehberi: https://www.esrb.org/ratings-guide/
46. [B] USK: https://usk.de/
47. [B] Steamworks onboarding, Steam'de yayımlanamayacak içerikler (blokzincir/NFT; ödeme işlemcisi kuralı, Temmuz 2025): https://partner.steamgames.com/doc/gettingstarted/onboarding
48. [R] PC Gamer, Steam yapay zekâ beyan formu güncellemesi: https://www.pcgamer.com/software/ai/steam-updates-ai-disclosure-form-to-specify-that-its-focused-on-ai-generated-content-that-is-consumed-by-players-not-efficiency-tools-used-behind-the-scenes/
49. [B] Steamworks desteklenen para birimleri ve bölgesel fiyatlandırma (Türkiye → MENA-USD, Kasım 2023): https://partner.steamgames.com/doc/store/pricing/currencies
50. [B] 7194 sayılı Kanun (Dijital Hizmet Vergisi): https://www.mevzuat.gov.tr/mevzuat?MevzuatNo=7194&MevzuatTur=1&MevzuatTertip=5
51. [B] 7258 sayılı Kanun (bahis ve şans oyunları): https://www.mevzuat.gov.tr/mevzuat?MevzuatNo=7258&MevzuatTur=1&MevzuatTertip=5
52. [B] Reuters, Türkiye'nin Roblox'a erişim engeli (7 Ağustos 2024): https://www.reuters.com/technology/turkey-blocks-access-roblox-2024-08-07/
53. [B] IRS vergi anlaşması tabloları: https://www.irs.gov/individuals/international-taxpayers/tax-treaty-tables
54. [B] IRS, ABD–Türkiye anlaşma belgeleri: https://www.irs.gov/businesses/international-businesses/turkey-tax-treaty-documents
55. [B] IRS Form W-8BEN / W-8BEN-E: https://www.irs.gov/forms-pubs/about-form-w-8-ben ; https://www.irs.gov/forms-pubs/about-form-w-8-ben-e
56. [B] Steamworks vergi SSS: https://partner.steamgames.com/doc/finance/taxfaq
57. [B] Steamworks ödemeler ve satış raporları: https://partner.steamgames.com/doc/finance/payments_salesreporting
58. [B] Gelir İdaresi Başkanlığı (GVK md. 18, mük. 20, 89/13, 123; KVK; 7456 sayılı Kanun; KDV oranları): https://www.gib.gov.tr/
59. [B] Sanayi ve Teknoloji Bakanlığı, Teknoloji Geliştirme Bölgeleri (4691 sayılı Kanun): https://www.sanayi.gov.tr/
60. [B] TÜBİTAK 1512 BiGG: https://tubitak.gov.tr/tr/destekler/sanayi/ulusal-destek-programlari/1512
61. [B] KOSGEB destek programları: https://www.kosgeb.gov.tr/
62. [B] Ticaret Bakanlığı, ihracat ve hizmet ihracatı destekleri: https://ticaret.gov.tr/
63. [B] Kickstarter ücretleri ve desteklenen ülkeler: https://www.kickstarter.com/help/fees ; https://help.kickstarter.com/
64. [B] Patreon fiyatlandırma: https://www.patreon.com/pricing
65. (kullanılmadı)
66. [R] Kardeş rapor: /home/user/isekai/docs/research/02-pazar-ve-rakip-analizi.md
67. [R] Screen Rant, Solo Leveling: ARISE gacha eleştirisi: https://screenrant.com/solo-leveling-arise-review-gacha-mechanics-gameplay/
68. [R] Automaton, Blue Protocol: Star Resonance para kazanma tepkisi: https://automaton-media.com/en/news/blue-protocol-star-resonance-is-peaking-at-more-than-90000-concurrent-players-but-steam-reviews-are-mixed-due-to-server-issues-and-aggressive-monetization/
69. [R] Automaton, Duet Night Abyss gacha'yı kaldırıyor: https://automaton-media.com/en/news/duet-night-abyss-decides-to-abolish-gacha-systems-just-before-launch-we-ask-the-devs-what-happens-to-the-games-monetization/
70. (kullanılmadı)
71. [B] AB Yapay Zekâ Yasası (Tüzük 2024/1689): https://eur-lex.europa.eu/eli/reg/2024/1689/oj
72. [C] Apple fiyat güncellemesi (Türkiye dahil, 17 Kasım 2025): https://developer.apple.com/news/?id=nomqoqfm
73. [C] Apple fiyat ve vergi güncellemesi (Japonya ve Türkiye fiyatları, Aralık 2024): https://developer.apple.com/news/?id=onjo01rj

## Doğrulama Notları (24.09.2026)

Bağımsız doğrulama; Steamworks belgeleri `SteamTracking/SteamworksDocumentation` GitHub aynasından (raw.githubusercontent.com) birincil metin olarak, diğerleri WebSearch ile farklı sorgu ve kaynaklardan kontrol edildi. ftc.gov, eur-lex, irs.gov, kickstarter.com, classification.gov.au bu oturumda doğrudan açılamadı; bunlar için arama sonuçlarındaki resmî sayfa başlıkları ve hukuk bürosu özetleri kullanıldı.

| İddia | Sonuç | Düzeltme/Not | Kaynak |
|---|---|---|---|
| Steam gelir payı %30 / %25 (10 M $ üstü) / %20 (50 M $ üstü); oyun başına, DLC ve oyun içi satış dahil; Kasım 2018 duyurusu | Doğrulandı | 1 Ekim 2018 sonrası gelirlere uygulanıyor, 30 Kasım 2018'de duyuruldu | https://variety.com/2018/gaming/news/valve-revenue-split-changes-1203078700/ |
| Steam Direct 100 $, 1.000 $ düzeltilmiş brüt gelirde mahsup, iade yok; ödemeden sonra 30 gün bekleme | Doğrulandı | — | https://partner.steamgames.com/doc/gettingstarted/appfee ; https://partner.steamgames.com/doc/gettingstarted/onboarding (GitHub aynası) |
| EA→1.0 fiyat 1.0'da artar + %10 çıkış indirimi | **Düzeltildi** | Fiyat artışından sonraki 30 gün çıkış indirimi dahil hiçbir indirim yapılamıyor. Fiyat 1.0'dan ≥30 gün önce artırılmalı (§7.2) | https://partner.steamgames.com/doc/marketing/discounts ; https://partner.steamgames.com/doc/store/pricing |
| Brezilya ECA Digital (Kanun 15.211/2025) 17 Mart 2026'da yürürlükte; reşit olmayanların erişebildiği oyunlarda ücretli loot box yasak; ceza 50 M BRL veya Brezilya gelirinin %10'u | Doğrulandı | İmza 17 Eylül 2025 | https://www.mayerbrown.com/en/insights/publications/2026/04/enforcement-of-brazils-eca-digital-introduces-new-obligations-for-companies ; https://www.hrw.org/news/2025/09/17/brazil-passes-landmark-law-to-protect-children-online |
| FTC v. HoYoverse/Cognosphere (Ocak 2025): 20 M $, 16 yaş altına ebeveyn izni olmadan loot box yasak, olasılık ve sanal para kuru açıklaması, 13 yaş altı veri silme | Doğrulandı | — | https://www.ftc.gov/news-events/news/press-releases/2025/01/genshin-impact-game-developer-will-be-banned-selling-lootboxes-teens-under-16-without-parental |
| FTC v. Epic: 520 M $ (275 M $ COPPA + 245 M $ karanlık desen iadesi), Aralık 2022 | Doğrulandı | 245 M $'lık emir Mart 2023'te kesinleşti | https://www.ftc.gov/news-events/news/press-releases/2022/12/fortnite-video-game-maker-epic-games-pay-more-half-billion-dollars-over-ftc-allegations |
| Güney Kore olasılık açıklaması 22 Mart 2024; "Ocak 2025'te ispat yükü yayıncıya geçti" | **Düzeltildi** | Açıklama zorunluluğu doğru. İspat yükü ve 3 kat tazminat değişikliği Ocak 2025'te kabul edildi, **1 Ağustos 2025'te** yürürlüğe girdi | https://www.shinkim.com/eng/media/newsletter/3206 ; https://gameworldobserver.com/2024/07/08/266-games-violated-loot-box-rules-south-korea |
| Belçika Kumar Komisyonu Nisan 2018: ücretli loot box lisanssız şans oyunu; uygulama zayıf | Doğrulandı | Rapor 25 Nisan 2018; 2022'de en çok hasılat yapan 100 iPhone oyununun %82'si hâlâ loot box satıyordu | https://online.ucpress.edu/collabra/article/9/1/57641/195100/Breaking-Ban-Belgium-s-Ineffective-Gambling-Law |
| Hollanda Danıştayı 9 Mart 2022'de EA'nın 10 M €'luk cezasını bozdu | Doğrulandı | Gerekçe: paketler beceri oyununun parçası, kendi başına şans oyunu değil | https://cms-lawnow.com/en/ealerts/2022/03/dutch-court-rules-fifa-loot-boxes-not-a-game-of-chance-revokes-ea-penalty |
| Avustralya (22 Eylül 2024): ücretli şans mekaniği → en az M; simüle kumar → R18+ | Doğrulandı | Yalnızca bu tarihten sonra sınıflandırılan oyunlara uygulanır | https://www.classification.gov.au/about-us/media-and-news/news/new-classifications-for-gambling-content-video-games |
| Apple: Brezilya'da loot box → 18+; Avustralya'da 18 Haziran 2026'dan itibaren 15+ kalkıyor | Doğrulandı | — | https://developer.apple.com/news/?id=f5zj08ey ; https://developer.apple.com/news/?id=yrrb45pw |
| AB CPC ağı, Mart 2025 oyun içi sanal para ilkeleri + Star Stable eylemi | Doğrulandı | 7 ilke; ana mesaj: her satın almanın gerçek para karşılığı gösterilmeli | https://commission.europa.eu/news-and-media/news/european-commission-hosts-stakeholders-talks-application-cpc-networks-key-principles-games-virtual-2025-06-03_en |
| AB Digital Fairness Act: "Eylül 2026 durumu doğrulanamadı" | **Düzeltildi** | Teklif henüz yayımlanmadı; Komisyon 2026 çalışma programı: 4. çeyrek 2026 | https://www.europarl.europa.eu/legislative-train/theme-protecting-our-democracy-upholding-our-values/file-digital-fairness-act |
| PEGI'nin ücretli rastgele öğe için asgari sınıfı (açık soru) | **Düzeltildi (yeni bilgi)** | Haziran 2026'dan itibaren yeni başvurularda ücretli rastgele öğe → en az PEGI 16; süreli teklif → en az PEGI 12; NFT → PEGI 18; sınırsız iletişim → PEGI 18 | https://pegi.info/news/pegi-expands-age-rating-criteria-interactive-risk-categories ; https://www.videogameschronicle.com/news/all-games-with-loot-boxes-in-them-will-be-rated-minimum-pegi-16-starting-this-summer/ |
| Türkiye DHV %7,5 → %5 | Doğrulandı + ek | 10767 sayılı CK: 2026'da %5, **1 Ocak 2027'den itibaren %2,5** | https://taxnews.ey.com/news/2026-0117-turkiye-revises-digital-service-tax-rate-for-2026-and-2027 |
| Steam, 20 Kasım 2023'ten beri Türkiye'de USD (MENA-USD) | Doğrulandı | Steamworks para birimi sayfasında Türkiye "USD_MENA" listesinde | https://steamdb.info/blog/steam-turkey-argentina-usd/ ; https://partner.steamgames.com/doc/store/pricing/currencies |
| ABD–Türkiye anlaşması md. 12: telif stopajı %10 (ekipman %5); Valve Steam gelirini telif sayıyor, stopaj yalnızca ABD kaynaklı satışlara | Doğrulandı | Anlaşma 28 Mart 1996'da imzalandı, 19 Aralık 1997'de yürürlüğe girdi | https://www.congress.gov/congressional-report/105th-congress/executive-report/6/1 ; https://partner.steamgames.com/doc/finance/taxfaq |
| Kickstarter'da proje sahibi olarak Türkiye desteklenmiyor | Doğrulandı | Uygun ülke listesinde Türkiye yok | https://updates.kickstarter.com/who-is-eligible-to-use-kickstarter/ |
| Hizmet ihracatı kazanç indirimi %50 (oran D) | **Düzeltildi** | 2025'te %80; 11257 sayılı CK ile 2026'dan itibaren **%100**. Steam gelirine uygulanabilirliği mali müşavirle teyit edilmeli | https://www.alomaliye.com/2026/04/20/yurt-disi-mukimlere-verilen-hizmetlerde-kazanc-indirimi/ |
| GVK 18 tutar sınırı doğrulanamadı | **Düzeltildi** | 2026 sınırı 5.300.000 TL (tarifenin 4. dilimi); Steam gelirine uygulanabilirliği mali müşavir/özelge ile netleşmeli | https://www.alomaliye.com/2026/09/03/gelir-vergisi-madde-18-serbest-meslek-kazanclari-telif-kazanclari-istisnasi/ |
| Genç girişimci istisnası tutarı D | **Düzeltildi** | 2026: 400.000 TL. Bağ-Kur prim desteği 1 Ocak 2026'dan sonra işe başlayanlar için kaldırıldı (7566 sayılı Kanun) | https://vergiselboyut.com/2026-genc-girisimci-vergi-tesviki/ ; https://www.bbdas.com.tr/bbdas-07-01-2026-15-7566-sayili-kanun-ile-yapilan-sgk-ve-diger-duzenlemeler-g-2894 |
| Teknokent, TÜBİTAK BiGG, KOSGEB tutarları | Doğrulanamadı | Mali müşavir ve teknokent yönetimiyle teyit edilmeli | — |
| İstek listesi → ilk hafta satış ~%10–20 | **Düzeltildi** | GameDiscoverCo: 25 bin+ istek listeli oyunlarda medyan 0,15×, 10 $ üstü oyunlarda 0,10×. 10–20 aralığının alt sınırı medyan | https://newsletter.gamediscover.co/p/the-state-of-steam-wishlist-conversions |
| Popular Upcoming eşiği ~5–10 bin | **Çürütüldü** | Haziran 2026'dan beri tahminen ~80–120 bin (Zukowski ~100 bin); resmî değil | https://howtomarketagame.com/2026/06/25/how-the-steam-personal-calendar-affects-your-launch/ ; https://www.pcguide.com/news/steams-new-100000-wishlist-rule-means-many-indie-devs-will-have-to-rely-on-a-different-feature-to-be-discovered/ |
| Boxleiter çarpanı ~30–40 | Kısmen doğrulandı | 2026 çıkışları için medyan ~30× (aralık 20–40×); ikincil kaynak | https://www.steampageanalyzer.com/blog/boxleiter-method-explained |
| Next Fest yılda 3 kez; bir oyun yalnızca bir kez | Doğrulandı | Prolog, "Bölüm 1" ve kısa önizlemeler kabul edilmez; EA çıkışı "çıkış" sayılır | https://partner.steamgames.com/doc/marketing/upcoming_events/nextfest |
| Epic Games Store 88/12, Haziran 2025'ten beri yılda uygulama başına ilk 1 M $'da %0; Unreal %5 (1 M $ sonrası), "Launch Everywhere with Epic" %3,5 | Doğrulandı | — | https://store.epicgames.com/en-US/news/epic-games-store-updates-revenue-share-keep-100-of-the-first-1m-per-product-per-year ; https://www.unrealengine.com/license |
| Unity Runtime Fee iptal (Eylül 2024), Personal sınırı 200 bin $ | Doğrulandı | — | https://unity.com/blog/unity-is-canceling-the-runtime-fee |
| Steam'de blokzincir/NFT ve reklam tabanlı model yasak; ödeme işlemcisi kuralına aykırı içerik yasak | Doğrulandı | — | https://partner.steamgames.com/doc/gettingstarted/onboarding |
| "Stop Killing Games": kesin sayı ve Komisyon yanıtı D | **Düzeltildi** | 1.294.188 imza, 26 Ocak 2026'da sunuldu. Komisyon 16 Haziran 2026'da yasal zorunluluk önermedi; gönüllü davranış kuralları süreci başlatacak | https://citizens-initiative.europa.eu/news/european-commission-replies-stop-destroying-videogames-initiative-2026-06-16_en |
| AB AI Act md. 50, 2 Ağustos 2026'dan beri uygulanıyor; erteleme D | **Düzeltildi** | Digital Omnibus (2026/1744) md. 50'yi ertelemedi; md. 50(2) için yalnızca eski sistemlere 2 Aralık 2026'ya kadar süre | https://www.hunton.com/privacy-and-cybersecurity-law-blog/eu-digital-omnibus-on-ai-enters-into-force |

**Karar etkisi:** Ana model (premium, ücretli rastgelelik yok) değişmiyor; PEGI 2026 değişikliği bu kararı güçlendiriyor. Değişen tek uygulama kararı **EA→1.0 fiyat artışının zamanlaması** (1.0'dan en az 30 gün önce). Türkiye vergi teşvikleri (%100 indirim, GVK 18, genç girişimci) şahıs şirketi önerisini destekliyor, ama Steam gelirine uygulanabilirliği mali müşavirle teyit edilmeden bütçeye yazılmamalı.
