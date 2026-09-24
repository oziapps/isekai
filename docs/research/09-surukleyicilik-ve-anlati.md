# 09 — Sürükleyicilik ve Anlatı: Oyuncuya "Gerçekten Başka Bir Dünyaya Düştüm" Dedirtmek

> Hazırlanma: 2026-09-24 · Kapsam: isekai "varış" tasarımı, diegetik "Sistem" arayüzü, isekai'ye özgü meta-sürükleyicilik, yoldaş/romans tasarımı, 2025–2026 yapay zekâ destekli NPC'ler, anime sinematik dili, ses, erişilebilirlik, yerelleştirme ve üç orijinal dünya tohumu.
>
> **Yöntem ve sınırlama notu (önemli):** Bu rapor yazılırken oturumun ortak WebSearch bütçesi (200/200) **tükenmişti**. Ayrıca egress proxy GitHub ve `*.googleapis.com` dışındaki alan adlarını engelliyor (Steam, PC Gamer, Wikipedia, GDC Vault, NVIDIA ve Inworld siteleri denendi: bağlantı reddedildi). Bu yüzden:
> - Araç, lisans ve donanım iddiaları **bu oturumda GitHub üzerinden birincil kaynaktan** (README, LICENSE, repo listeleri) doğrulandı → **[Y]**.
> - Pazar ve tepki verileri, kardeş raporların (01–07) önceki aramalarla doğruladığı kaynaklardan alındı. Bu URL'ler bu oturumda yeniden açılmadı → çoğunlukla **[O]**.
> - Oyun tasarımına dair nitel bilgiler (Dead Space'in arayüzü, Outer Wilds'ın döngüsü gibi) ve bazı rakamlar **bilgi tabanından** geliyor, bu oturumda web ile doğrulanamadı → **[BT]** etiketi ve güven düzeyi. Bunlar "Kaynaklar" bölümünün sonunda URL'siz olarak ayrıca listelendi. Doğrulama ekibinin öncelikle bu satırları kontrol etmesi gerekir.
>
> Güven notasyonu: **[Y]** yüksek · **[O]** orta · **[D]** düşük · **[BT]** bilgi tabanı (doğrulanamadı). Terimler (P1–P10 sütunları, Gate, Status mühürleme, "Son Gün" prologu) 01 ve 03 numaralı raporlarla uyumlu.

## Özet

- **Sürükleyicilik tek bir özellik değil, dört katmanın toplamı.** Duyusal katman (görüntü, ses, haptik), sistemik katman (dünya eylemlerine tepki veriyor), anlatısal/duygusal katman (kimlik, bağlar, bedel) ve isekai'ye özgü **meta katman** (oyuncunun gerçek hayatı kurguya sızıyor). Piyasadaki anime/isekai oyunları genelde yalnızca birinci katmana yatırım yapıyor. Bizim farkımız dördünü birlikte kurmak olmalı.
- **"Sistem" bir arayüz değil, bir karakter olmalı.** Status penceresi dünya içinde, yalnızca oyuncunun gördüğü holografik bir panel olarak konumlanmalı. Kendine özgü bir sesi ve kişiliği olmalı, zamanla "arıza" vermeli (P3 gizemi). Dead Space'in sırt üstü sağlık göstergesi ve Assassin's Creed'in Animus'u, arayüzü kurguyla meşrulaştırmanın iki bilinen örneği [BT, yüksek]. İsekai'de bu meşrulaştırma zaten türün içinde hazır.
- **Varış ilk 120 dakikada tamamen oynanabilir olmalı.** Steam'in iade kuralı (14 gün, 2 saatten az oynama) nedeniyle vaat ilk 2 saatte teslim edilmeli [21]. Önerilen akış: oynanabilir "Son Gün" (diegetik karakter yaratma) → geçiş anı → dilini bilmediğin bir dünyada uyanma → Lonca kaydı → Sistem uyanışı → ilk ölüm ve "Geri Yükleme" → ilk şehir → ilk yoldaş. **Düzeltme (24.09.2026):** İlk sürümde ilk gerçek dövüş 65. dakikaya, Uyanış olayı 105–120. dakikaya kalıyordu. Bu, 03 raporundaki hedeflerle (ilk dövüş ilk 5–10 dk, Uyanış ≤90. dk) çelişiyordu ve aksiyon oyununda iade riskini artırıyordu. Hizalanmış takvim §3'te: ilk dövüş ≤10. dk, ilk yoldaş (yerli rehber) 15–30. dk, Uyanış ≤90. dk.
- **Dil öğrenme, "yabancı" hissinin en ucuz ve en güçlü aracı.** Final Fantasy X'teki Al Bhed sözlükleri ve Chants of Sennaar tarzı kademeli çeviri, oyuncuya "burada yabancıyım" duygusunu mekanikle yaşatıyor [BT, yüksek]. Süresi kısa tutulmalı (20–40 dk) ve atlanabilir olmalı.
- **Ölüm döngüsü, roguelite yapıya anlatısal bir gerekçe sunuyor.** Hades'te ~21.000 seslendirilmiş replik var ve ölüm hikâyeyi ilerletiyor [22]. Bizde de ölüm "Geri Yükleme" olarak kurgulanmalı: NPC'lerin déjà vu replikleri ve Sistem kaydındaki "Döngü #n" ile, P4 sütununa uygun şekilde.
- **Eski hayat, sayısal bir fark yaratmalı (P1).** Oyuncunun seçtiği meslek başlangıç perk'ini, diyalog seçeneklerini ve bir "pişmanlık" görevini belirlemeli. Gerçek tarih/saat (Dünya'dan ayrılalı N gün, mevsim, isteğe bağlı doğum günü) düşük maliyetle güçlü bir meta-bağ kuruyor. Kişisel veriler yalnızca yerelde tutulmalı.
- **Yoldaşlar sürükleyiciliğin çekirdeği.** Persona'nın confidant yapısı (bağ = mekanik güç), Fire Emblem'in destek sohbetleri (yoldaşlar birbiriyle konuşur), BG3'ün onay ve tepki sistemi, Dragon's Dogma'nın pawn'ları iyi birer model [BT]. 4–6 derin yoldaş hedeflenmeli (02 raporu).
- **Romans talep görüyor ama mayınlı.** Harem ve rıza sorunları (Mushoku Tensei'nin Bilibili'den kaldırılması [36]) risk yaratıyor. Steam, Temmuz 2025'ten beri ödeme işlemcisi kurallarını ihlal edebilecek içeriği yasaklıyor [27]. Tüm romans edilebilir karakterler açıkça yetişkin olmalı. Romans ne satılmalı ne de gacha arkasına konmalı. Monetizasyon doğrudan satın alınan kozmetiklerle sınırlı kalmalı.
- **2025–2026'da LLM NPC'lerin karnesi karışık.** Where Winds Meet'in LLM NPC'leri ilgi çekti ama oyuncular onları kolayca manipüle etti. Uydurma sırlar ve döneme uymayan cevaplar sürükleyiciliği bozdu [23][24]. Inworld'ün GitHub vitrini artık oyun karakter SDK'ları yerine TTS/Realtime API ağırlıklı [9]. NVIDIA'nın yerel çıkarım SDK'sı (NVIGI) 8 GB+ VRAM'li bir NVIDIA GPU ve Windows istiyor [6][7].
- **Önerimiz: kritik yolda serbest metin LLM yok.** LLM'i üretim sırasında insan kontrollü replik varyasyonları üretmek için kullanmak, oyun içindeyse yalnızca **isteğe bağlı, yerel, gramerle kısıtlı ve lore'a bağlı** bir "Sistem'le konuş" deneyi sunmak doğru yol. Sistem zaten insan olmayan bir varlık olduğu için LLM tuhaflıkları kurgu içinde açıklanabilir. Canlı üretilen içerik Steam'de beyan edilmeli ve korumalarla birlikte sunulmalı [28][25].
- **Anime hissi kamera ve zamanlamadan gelir.** Hitstop, 2–4 karelik "impact frame", cut-in'ler, onomatope tipografisi ve kendimize ait bir "Arise" anı (öneri: **Ad Verme** töreni) en yüksek getirili yatırımlar. Impact frame'ler için flaş azaltma seçeneği şart (WCAG 2.3.1 [BT, yüksek]).
- **Ses kimliği:** Sistem bildirim sesi, karakter leitmotif'leri, uydurma dilde vokal parçalar (NieR örneği [BT]) ve Japonca dublaj seçeneği (faz 2, 07 raporu). Lip-sync için MIT lisanslı uLipSync, Rhubarb ve Audio2Face-3D SDK mevcut [19][8].
- **Üç orijinal dünya tohumu önerildi:** (1) *Kut Ağacı*: Türk kozmolojisinden ilham alan dikey dünya ağacı zindanı ve "Ocak" tanrıları, (2) *Kayıp Eşyalar Şehri*: Dünya'nın unuttuklarının vardığı şehir ve "Envanter" Sistemi, (3) *Eşik*: komadaki bedenin ve "derinleştikçe uyanırsın" ikilemi.
- **31 teknik önceliklendirildi (Bölüm 9).** Dikey dilim (P0) için 12 teknik yeterli. En yüksek etki/maliyet oranına sahip olanlar: Sistem'i karakter yapmak, imza bildirim sesi, Lonca kaydı töreni, eski hayat perk'leri ve NPC hafızası.

---

## 1. Çerçeve: "Oradaymış Gibi" Hissetmek Neden Olur?

Akademik literatürde sürükleyicilik genelde katmanlı ele alınıyor. Brown ve Cairns (2004) üç aşamadan bahseder: ilgi, kendini kaptırma ve tam sürüklenme. Ermi ve Mäyrä (2005) SCI modelinde duyusal, meydan okumaya dayalı ve imgesel sürüklenmeyi ayırır. Slater (2009) VR'da iki kavram önerir: "burada olma yanılsaması" (place illusion) ve "olanların gerçekten olduğu yanılsaması" (plausibility illusion) [BT, yüksek; bu oturumda metinlere erişilemedi]. Bu kavramları isekai'ye uyarlayan çalışma çerçevemiz şöyle:

| Katman | Soru | Kırılma anı (sürüklenmeyi bozan) | İsekai'deki fırsat |
|---|---|---|---|
| **Duyusal** | Dünya görünüyor, duyuluyor, hissediliyor mu? | Ucuz animasyon, sessiz vuruş, tutarsız sanat | Anime sinematik dili, imza sesler, haptik |
| **Sistemik (akla yatkınlık)** | Dünya benim eylemlerime tutarlı tepki veriyor mu? | NPC'nin az önce olanı bilmemesi, anlamsız görev | NPC hafızası, itibar, KCD2 tarzı gerçekçilik ayarları |
| **Anlatısal/duygusal** | Benim burada olmam bir şey ifade ediyor mu? | Karaktersiz harem, bedelsiz güç | Bedelli döngü, "dönüş mü kalış mı" ikilemi, derin yoldaşlar |
| **Meta (isekai'ye özgü)** | Buraya gerçekten *ben* mi geldim? | Hazır ve anlamsız bir kahraman | Oyuncunun adı, tarihi, eski hayatı ve telefonu kurgunun parçası |

**Temel ilke:** İsekai'de oyuncu ile karakterin durumu örtüşüyor. İkisi de bu dünyaya yeni geldi, ikisi de kuralları bilmiyor. Tutorial, arayüz, ölüm ve tekrar gibi normalde sürükleyiciliği bozan oyun sistemleri, isekai'de **kurgunun kendisi** olabilir. Bu tür avantajı en iyi .hack// serisi (oyun içinde sahte bir MMO, e-posta ve forum masaüstü) ve Sword Art Online'ın ölüm kuralı gibi eserlerde görülüyor [BT, yüksek].

---

## 2. Referans Oyunlardan Dersler

| Oyun | Sürükleyiciliği nasıl kuruyor | Bize aktarılacak ders | Uygulama maliyeti |
|---|---|---|---|
| **Dead Space** (2008) | Sağlık ve stasis göstergeleri karakterin sırtındaki RIG'de. Envanter ve harita oyunu durdurmadan hologram olarak açılıyor [BT, yüksek] | Status penceresi dünya-uzayında holografik bir panel olmalı. Savaşta açılırsa zaman durmasın (erişilebilirlik için "duraklat" seçeneği olsun) | Orta |
| **.hack//** (PS2, 2002–03) | Oyuncu, içinde MMO oynanan sahte bir işletim sisteminde e-posta, haber ve forum okuyor [BT, yüksek] | "Eski Telefon" diegetik menüsü: Dünya'dan gelen telefonun birkaç uygulaması hâlâ çalışıyor (Bölüm 4) | Orta |
| **Persona 3/5, Metaphor** | Takvim, gündüz sosyal bağ, gece zindan. Bağlar mekanik güç veriyor. P3 Reload Haziran 2026'da 3 milyonu geçti [31]. Metaphor 31 Mart 2025'te 2 milyona ulaştı [33] | DanMachi'deki şehir hayatı ile zindan döngüsü, takvim ve bağ ritmiyle kurulmalı | Yüksek |
| **Mount & Blade** | Hiç kimse olarak başlayıp lord ve kral olabiliyorsun. Lordlar seni hatırlıyor, itibar hissediliyor [BT, yüksek] | Fraksiyon itibarı ve "sıradan birinden hükümdarlığa" eğrisi (P7) | Yüksek |
| **Kingdom Come: Deliverance 1–2** | Açlık, yorgunluk, kirli ya da kanlı kıyafetin NPC tepkisine etkisi, sınırlı kayıt (Saviour Schnapps), tanık ve suç sistemi. KCD1'de okumayı öğrenmek gerekiyordu [BT, yüksek] | Kurgu içi "öğrenme" mekaniği ve isteğe bağlı bir "Gerçekçi Mod". Ana modda ceza hafif tutulmalı | Orta–Yüksek |
| **Baldur's Gate 3** | Yoldaş onayı, her şeye tepki veren replikler, köken karakterleri, sonuçları olan seçimler [BT, yüksek] | Az sayıda derin yoldaş. Her büyük olaya en az bir yoldaş tepkisi | Yüksek |
| **Elden Ring / Dark Souls** | İşaretsiz keşif, gizli NPC görevleri, diğer oyuncuların mesajları ve hayaletleri [BT, yüksek] | Asenkron "diğer isekai'lılar": başka oyuncuların bıraktığı notlar ve ölüm yankıları. MMO maliyeti olmadan kalabalık şehir hissi | Orta |
| **Outer Wilds** | 22 dakikalık döngü. İlerleme yalnızca **bilgiyle** oluyor. Gemi günlüğü ipuçlarını bağlıyor [BT, yüksek] | Ölümde bilgi kalıcı kalır (P4, P9). "Keşif Defteri" sırları birbirine bağlar | Orta |
| **Dragon's Dogma 1–2** | Oyuncunun yarattığı pawn başka oyuncuların dünyasına gidip bilgi ve hediyeyle dönüyor. DD2 31 Mart 2026 itibarıyla 4,2 milyon sattı [32] | Asenkron yoldaş ödünç verme (uzun vadeli, araştırılmalı). Yoldaş laf kalabalığı tekrara düşmemeli | Yüksek |
| **NieR:Automata** | HUD öğeleri takılıp çıkarılan çiplerle yönetiliyor (işletim sistemi çipini çıkarırsan ölürsün). E sonunda başkalarına yardım için kayıt dosyasını feda ediyorsun. Şarkılar uydurma dilde [BT, yüksek] | Sistem modülleri takılıp çıkarılan "yetenek çipleri" olabilir. Bir kez yapılabilen, gerçekten fedakârlık hissettiren meta seçim | Orta |
| **Final Fantasy X** | Tidus Spira'ya yabancı olarak geliyor ve anlatıcı o. Al Bhed dili, toplanan sözlüklerle harf harf çözülüyor [BT, yüksek] | Kademeli dil çevirisi ve yabancı anlatıcı bakışı | Orta |
| **Chants of Sennaar / Heaven's Vault** | Dil çözme oyunun ana mekaniği [BT, yüksek] | Glif sözlüğü. Kelime öğrendikçe altyazı açılır | Orta |
| **Morrowind** | Karakter yaratma, gümrük memurunun formu doldurmasıyla diegetik olarak yapılıyor [BT, yüksek] | Lonca kaydı töreninde memur Status kartını doldurur | Düşük |
| **Hades** | Ölüm anlatıyı ilerletiyor. ~21.000 replik, <20 kişilik ekip. Hypnos'un ölüm nedenine özel 75 repliği var [22] | Geri Yükleme sonrası özel replikler. NPC'lerde déjà vu | Orta–Yüksek |
| **Undertale / Doki Doki Literature Club** | Oyun, yeniden başlatmaları hatırlıyor ve dördüncü duvarı kırıyor [BT, yüksek] | Dozunda meta anlar (Sistem kaydı "bu döngüyü daha önce gördüm" der). Oyuncunun dosyalarını okumak **yok** | Düşük |
| **Animal Crossing / Pokémon G/S** | Gerçek saat ile mevsim ve bayram döngüsü [BT, yüksek] | Gerçek tarih entegrasyonu. Oyuncuyu **cezalandırmadan**, sürpriz olarak | Düşük |
| **Assassin's Creed (Animus)** | HUD'ın, "senkron kaybı"nın ve ölümün kurgusal gerekçesi [BT, yüksek] | Sistem, arayüzü ve yeniden doğuşu kurgu içinde açıklar | Düşük |

---

## 3. Isekai Varış Tasarımı: İlk 120 Dakikanın Senaryosu

03 raporundaki FTUE hedefleri (0–1 dk'da kontrol oyuncuda, 60–120 dk'da Uyanış olayı) korunarak sahne sahne öneri:

> **Hizalama notu (düzeltildi 24.09.2026):** Bu bölümün ilk sürümü 03 raporuyla çelişiyordu. İlk gerçek dövüş 65–85. dakikadaydı (03: ilk düşman 1–5. dk, "dövüş iyi mi" yargısı ilk 5 dk'da oluşur). İlk yoldaş 105–120. dakikadaydı (03: 5–15. dk). Uyanış olayı 105–120. dakikadaydı (03 Çıkarımlar #2: 90. dakikadan önce). İlk 65 dakikayı dövüşsüz geçiren bir aksiyon RPG, Steam'in 2 saatlik iade penceresinde gereksiz risk taşıyor. Sahnelerin içeriği korunarak dakikalar aşağıdaki gibi hizalandı. Alt başlıklardaki dakikalar bu tabloya göre güncellendi. Tüm değerler hedeftir, olgu değildir.
>
> | Dakika (hedef) | Olay | 03 raporundaki karşılığı |
> |---|---|---|
> | 0–5 | "Son Gün" prologu (kısaltılmış), ~3–5. dk'da ilk Sistem "hata mesajı" | 0–1 dk kontrol oyuncuda |
> | 5–7 | Geçiş anı | 1–5 dk varış |
> | 7–15 | Yeni dünyada uyanış + **ilk dövüş** (hayatta kalma karşılaşması, hit-stop, Sistem "ding"i). Dil segmenti başlar, dövüş ve keşifle iç içe ilerler | 1–5 dk ilk düşman |
> | 15–30 | **İlk yoldaş (a: yerli rehber)**, ilk mini-Gate, ilk 3'lü Sistem önerisi, ilk seviye atlama. "Dil Kavrayışı Lv1" ~25–40. dk | 5–15 dk |
> | 30–45 | Lonca kaydı, F-rank damgası, Sistem'in kısmi uyanışı (günlük görev) | 5–15 dk F-rank |
> | 45–65 | İlk boss, ilk ölüm ve "Geri Yükleme", déjà vu replikleri | 15–60 dk |
> | 65–80 | İlk şehir, ilk Status mühürleme töreni, ilk kasaba yapısı | 15–60 dk |
> | 80–90 | **Uyanış olayı:** gizli sınıf, ilk Aura anı, eski boss'a rövanş | 60–120 dk, "90. dakikadan önce" |
> | 90–120 | Meta katmanların önizlemesi, rakip yabancı (b) ile tanışma, Bölüm 1 sonu ve "sonraki bölüm" önizlemesi | 60–120 dk |

### 3.1 "Son Gün" prologu: modern dünya, diegetik karakter yaratma (0–5 dk; ilk sürümde 0–8 dk, düzeltildi 24.09.2026)

- **Kurgu:** Oyuncunun Dünya'daki son akşamı. Kontrol ilk saniyeden itibaren oyuncuda. Uzun logo ve açıklama yok.
- **Karakter yaratma menüsü yok, eşyalar var:**
  - Masadaki iş kartı, dolaptaki forma ya da önlük, telefondaki son mesajlar mesleği ve hobiyi belirler (Morrowind'in gümrük formu mantığı [BT]).
  - Ayna, görünüşü belirler.
  - Telefondaki bir form (hastane randevusu, iş başvurusu ya da oyun hesabı), oyuncunun adını kurgu içinde sorar.
- **"Son bir saatini ne yaparsın?" seçimi:** Anneni ara, işi bitir, arkadaşlarla buluş, oyun oyna, spora git. Seçim üç şeyi belirler:
  - Bir **Anı Parçası** (ileride bir flashback açar)
  - Bir başlangıç eğilimi
  - Bir **pişmanlık** (kişisel görev tohumu)
- **Gerçek zaman:** Prolog, sistem saatine göre akşam ya da gece geçer. Pencereden görünen mevsim cihazın tarihine uyar. İsteğe bağlı. Dünya'daki son günün tarihi, oyuncunun oyunu ilk açtığı tarih olur ve kayda yazılır.

**Eski hayat → başlangıç tablosu (P1, örnek; dikey dilimde 3, çıkışta 8 meslek):**

| Eski meslek | Başlangıç perk'i | Diyalog/dünya etkisi | Pişmanlık görevi tohumu |
|---|---|---|---|
| Aşçı | "Tat Analizi": yemek buff'ları, zehri tanıma | Han ve pazarda özel seçenekler | Açamadığı lokanta |
| Yazılımcı | "Hata Ayıklama": Sistem arızalarını ve gizli istatistikleri görme | Sistem'le özel diyaloglar (P3 ipuçları) | Bitmemiş proje ya da ekip |
| Sağlıkçı | Sahada ilk yardım, triyaj | Tapınak ve şifacılarla güven | Kurtaramadığı hasta |
| Öğretmen | Dil öğrenme hızı +, yoldaş bağı + | Çocuklar ve lonca eğitmenleri | Mezun göremediği sınıf |
| Mühendis / inşaatçı | Kasaba yapıları için indirim, tuzak kurma | Kasaba inşası (P7) seçenekleri | Yarım kalan köprü |
| Sporcu | Dayanıklılık, kaçınma | Arena ve lonca sınavları | Kaçırılan final |
| Kurye / şoför | Harita ezberi, hızlı seyahat | Kervanlar ve tüccarlar | Teslim edilmemiş paket (gizem) |
| "Oyuncu" (gamer) | "Meta Bilgi": düşman HP barını erken görme | NPC'lerin "bu yabancı neden her şeyi biliyor?" tepkileri (P9) | Söz verip gidemediği buluşma |

### 3.2 Geçiş anı (5–7 dk; ilk sürümde 8–10 dk, düzeltildi 24.09.2026): Truck-kun yok

- Kamyon klişesi hayranların bıktığı ilk trope (01 raporu [37]).
- **Alternatifler:**
  - Metro istasyonunda açılan bir Gate.
  - Telefona gelen bildirim: "Sisteme kabul edildiniz. [Kabul] [Kabul]". Her iki buton da kabul. Hem komik hem ürkütücü.
  - Uyurken çalan bir alarm.
- **Ses tasarımı en önemli araç:** Şehir uğultusu, kulak çınlamasına ve sonra tam sessizliğe dönüşür. İlk ses, yeni dünyanın rüzgârı ve yabancı bir kuş olur. Ekran kararırken yalnızca Sistem metni kalır.

### 3.3 Uyanış ve dil (7–40 dk, dövüşle iç içe; düzeltildi 24.09.2026)

- Yakın kamera ve kısa bir duyusal aşırı yüklenme: iki ay, yabancı bir koku, bitki dokusu.
- **İlk dövüş burada, en geç 10. dakikada gelir (düzeltildi 24.09.2026):** Uyanıştan hemen sonra kısa bir hayatta kalma karşılaşması, hit-stop ve Sistem "ding"i. Oyuncu dil bilmeden de savaşabilir. "Bu oyunun dövüşü iyi" yargısı ilk dakikalarda oluşur (03 raporu).
- **İlk yoldaş (a: yerli rehber) 15–30. dakikada katılır:** Dili ve gelenekleri öğreten yerli karakter, kademeli çevirinin doğal taşıyıcısıdır (§3.8).
- İlk NPC konuşur ve altyazı **uydurma bir yazıyla** görünür.
- **Kademeli çeviri:**
  - Oyuncu işaret, jest ve nesne-kelime eşleştirmesiyle kelime öğrenir (FFX Al Bhed, Chants of Sennaar [BT]).
  - Altyazıda bilinen kelimeler oyuncunun diline geçer.
  - 20–40 dakika sonra Sistem ilk ödül olarak **"Dil Kavrayışı Lv1"** verir ve çeviri tamamlanır.
  - Bu an, Sistem'in "sana yardım ediyorum" diyerek oyuncunun güvenini kazandığı ilk andır.
- **Erişilebilirlik ve sabır:** "Dil engelini atla" seçeneği olmalı. Ana görev hiçbir zaman dil bulmacasına kilitlenmemeli. Öğrenilen kelimeler şehirde tabelaları okumak gibi sonraki sürprizlerde işe yarar.

### 3.4 Gelenekler ve Lonca kaydı (30–45 dk; ilk sürümde 40–55 dk, düzeltildi 24.09.2026)

- **Küçük kültürel kurallar:** selamlaşma biçimi, sağ elle yeme, "gerçek adını söylemek güç verir" tabusu. Bu tabu, Ad Verme mekaniğine bağlanır (Bölüm 8.1).
- **Lonca kaydı töreni:**
  - Memur, oyuncunun elini bir kristale koydurur. Status kartı dünyada fiziksel bir nesne olarak basılır.
  - Rütbe "F" çıkar ve memurun yüzünde acıma ifadesi görülür. Bu, 03 raporundaki "F-rank damgası" duygusal kancasıdır.
  - Memur, DanMachi'deki lonca danışmanı rolünün orijinal bir karşılığıdır. İleride bir yoldaş ya da bağ adayı olabilir.

### 3.5 Sistem uyanışı (ilk 5 dk'da tohum, 30–45 dk'da kısmi uyanış, 80–90 dk'da gizli sınıf; düzeltildi 24.09.2026)

- İlk Sistem penceresi 3–5. dakikada kısa bir "hata mesajı" olarak görünür. Kayıttan sonra günlük görev ve ceza kuralı açılır. **Gizli sınıf** ve ilk Aura anı, 03 raporundaki "90. dakikadan önce" hedefiyle uyumlu olarak 80–90. dakikadaki Uyanış olayına ayrılır (düzeltildi 24.09.2026).
- **Günlük görev, etik tasarım (03 raporundaki kırmızı çizgilerle uyumlu):**
  - Günlük "Eğitim" küçük ama görünür bir kazanç sağlar (P2).
  - Kaçırılırsa ceza kaybettirmez. Bunun yerine "Telafi Zindanı" adında eğlenceli bir hayatta kalma görevi açılır. Solo Leveling'deki ceza bölgesi trope'unun orijinal ve cezasız karşılığı budur.
  - Seri (streak) kaybı yok. Kaçırılan günler 03 raporuyla uyumlu olarak en fazla 7 gün biriktirilebilir (ilk sürümde 3 gün yazıyordu; düzeltildi 24.09.2026).

### 3.6 İlk boss, ilk ölüm ve "Geri Yükleme" (45–65 dk; ilk sürümde "ilk dövüş" 65–85 dk idi, düzeltildi 24.09.2026)

- İlk boss dövüşü kaybedilebilir, hatta kaybedilmesi beklenir. (İlk sıradan dövüş artık §3.3'te, ≤10. dakikada.)
- Ekran donar ve Sistem der ki: *"Kritik hata. Son kararlı duruma geri yükleniyor… Döngü #1 kaydedildi."*
- **Re:Zero trope'unun orijinal yorumu:** Geri Yükleme'nin bedeli var (bir "Yıpranma" göstergesi, bir anı kaybı). Kimseye anlatılamıyor, anlatmaya çalışınca Sistem sesi bozuluyor.
- **NPC tepkisi:**
  - Geri Yükleme'den sonra bazı NPC'ler "Seni daha önce görmüş gibiyim" gibi déjà vu replikleri söyler (Hades modeli [22]).
  - Bu replikler olay bayraklarıyla tetiklenir, yazılı ve seslendirilmiş olur. LLM gerekmez.

### 3.7 İlk şehir (65–80 dk; ilk sürümde 85–105 dk, düzeltildi 24.09.2026)

- Varış sinematiği: vinç çekimi, şehrin leitmotif'i, kalabalık NPC rutinleri, satıcı bağırışları ve tapınak çanı.
- Oyuncunun öğrendiği kelimeler tabelalarda karşısına çıkar (ödül).
- İlk hanın odası "ev" hissinin tohumudur. Daha sonra dekore edilebilir (kozmetik gelir için doğal bir alan).

### 3.8 Yoldaşlar ve Bölüm 1 sonu (yerli rehber 15–30 dk, rakip yabancı ve bölüm sonu 90–120 dk; ilk sürümde 105–120 dk, düzeltildi 24.09.2026)

- İlk yoldaş, oyuncunun **en zayıf anında** gelmeli. Hizalanmış takvimde bu an, uyanıştan hemen sonraki ilk hayatta kalma dövüşüdür (düzeltildi 24.09.2026).
- **Önerilen iki arketip:**
  - (a) Oyuncuya dili ve gelenekleri öğreten yerli biri. Doğal bir tutorial olur. 15–30. dakikada katılır.
  - (b) Başka bir "Sistem"e sahip, rakip bir yabancı. Uyanış olayından sonra (90–120. dk) tanıtılır.
- Bölüm 1, "sonraki bölüm" önizlemesiyle biter (P10).

| Dakika (hizalanmış; düzeltildi 24.09.2026) | Olay | Hedef his | Telemetri (03 raporuyla uyumlu) |
|---|---|---|---|
| 0–5 | Son Gün, eşyalarla karakter yaratma | "Bu benim hayatım" | `ftue_prologue_done` |
| 5–7 | Geçiş | Ürperti | — |
| 7–15 | Uyanış, **ilk dövüş**, dil başlangıcı | Yabancılık, merak, "dövüş iyi" | `first_combat` |
| 15–30 | İlk yoldaş (yerli rehber), ilk mini-Gate, ilk seviye | Güven, yetkinlik | `first_companion`, `lang_lv1` (~25–40. dk) |
| 30–45 | Lonca kaydı, F-rank, Sistem'in kısmi uyanışı | Küçük düşürülme, gizem | `guild_card`, `system_awaken` |
| 45–65 | İlk boss, ilk ölüm ve Geri Yükleme | Şok, sonra "anladım" | `first_death`, `first_restore` |
| 65–80 | İlk şehir, ilk Status mühürleme | Hayranlık | `town_arrival`, `first_seal` |
| 80–90 | Uyanış olayı: gizli sınıf, ilk Aura anı | "Bende bir şey var" | `awakening_seen` |
| 90–120 | Rakip yabancı, meta önizleme, Bölüm 1 sonu | Bağ, "bir bölüm daha" | `ep1_complete` |

---

## 4. Isekai'ye Özgü Meta-Sürükleyicilik

| Fikir | Uygulama | Risk / sınır | Maliyet |
|---|---|---|---|
| **Gerçek tarih/saat** | Kayıtta "Dünya'dan ayrılalı N gün" sayacı. Mevsim ve gün-gece isteğe bağlı olarak gerçek saate bağlanır. Oyun içi yıldönümlerinde yoldaşlar "Buraya geleli bir yıl oldu" der | Oyuncuyu **cezalandırmamalı**. Kaçırılan gün kayıp değildir. Saat hilesi serbest | Düşük |
| **Oyuncunun adı** | Metinde her yerde kullanılır. Seslendirmede Fallout 4'teki Codsworth yaklaşımı [BT, orta]: sık kullanılan isimlerin ön kaydı, olmayanlar için unvan ("Yabancı", "Kayıtsız") | Anında TTS ile isim eklemek ton uyumsuzluğu yaratır, dikkatli test edilmeli. Yayıncı modunda gerçek isim gizlenmeli | Orta |
| **Eski hayat anıları** | Meslek, hobi ve pişmanlık → perk, diyalog ve görev (3.1). Toplanan **Anı Parçaları** Dünya'daki sahneleri açan flashback'ler olur | Kişisel veri sorulmaz, oyuncu **seçer** | Orta |
| **"Eski Telefon" diegetik hub** | Dünya'dan gelen telefonun birkaç uygulaması hâlâ çalışır. Kamera fotoğraf modu olur, Notlar günlük, Müzik prologdaki anılara bağlı çalma listesi. Pil kıt bir kaynaktır ve mana kristaliyle şarj edilir. Dünya'dan bozuk mesajlar gelir (P3 gizemi) | Ana menünün yerine geçmez, yanında durur | Orta |
| **Geri Yükleme (ölüm döngüsü)** | Roguelite yeniden doğuşun kurgusal gerekçesi. Sistem kaydında "Döngü #n" tutulur. NPC'lerde déjà vu | Bedeli olmalı, yoksa ölüm anlamsızlaşır (P4) | Orta–Yüksek |
| **Seni hatırlayan NPC'ler** | Olay bayrakları, ilişki vektörü ve "anı" kayıtları. NPC bir önceki buluşmaya ve verilen sözlere atıf yapar | Warner Bros.'un **Nemesis System** patenti (ABD, 2021'de verildi [BT, orta]) hiyerarşik düşman-hafıza mekaniğini kapsıyor. Birebir benzer bir "ork kaptanı" yapısından kaçınılmalı, hukuk kontrolü yapılmalı | Orta |
| **Değişen dünya** | Fraksiyon itibarı, kasaba büyümesi (P7), görünür değişim (afişler, NPC kıyafetleri, yeniden inşa edilen köprü) | İçerik maliyeti yüksek, az ama görünür değişimler seçilmeli | Yüksek |
| **"Önceki bölümde…" özeti** | Olay günlüğünden otomatik anime özeti: bölüm başlık kartı ve sonraki bölüm önizlemesi (P10) | Şablon tabanlı yapılmalı. LLM kullanılacaksa yalnızca yeniden ifade için | Orta |
| **Dönüş mü, kalış mı?** | Ana hikâyenin sonunda Dünya'ya dönme imkânı ve bunun bedeli: bağlar. Birden çok son | Anlatı yükü yüksek ama duygusal zirve için en güçlü soru | Orta |
| **Tek Hayat / Sistemsiz mod** | Kalıcı ölüm (Geri Yükleme yok) ya da Sistem yardımı olmadan oynama | Niş bir kitle için. Başarımlar ayrı işaretlenir | Düşük |
| **Gerçek Dünya Görevi (opt-in)** | 90 dakikalık oturumdan sonra Sistem der ki: "Uyku da bir istatistiktir. Dinlenme bonusu hazır." Opt-in "su iç, esne" görevleri | Anti-bağımlılık ve olumlu PR. Asla zorunlu olmamalı ya da ödül kesmemeli | Düşük |
| **Dördüncü duvar anları** | Sistem nadiren "Bu döngüyü daha önce gördüm" der. Tek seferlik bir fedakârlık seçimi (NieR [BT]) | Oyuncunun dosyalarını, kullanıcı adını ya da konumunu **okumamalı**. KVKK/GDPR ve güven | Düşük |

**Kişisel veri notu:** Oyuncunun adı, doğum günü ve mesleği yalnızca **yerel kayıtta** tutulmalı. Telemetriye gönderilmemeli, bulut kaydı açıksa şifreli olmalı. KVKK ve GDPR riski minimumda tutulmalı. Bunun için ayrıca hukuki kontrol gerekli [D].

---

## 5. Diegetik Arayüz: "Sistem" Bir Karakterdir

1. **Görsel dil:** Arayüz, dünyada yüzen yarı saydam paneller olarak tasarlanmalı. Solo Leveling'in mavi pencerelerinin birebir kopyası olmamalı (01 raporundaki "look and feel" riski). Önerilen renk ve form dünya tohumuna göre değişir (Bölüm 10).
2. **Kimse görmez:** NPC'ler oyuncunun boşluğa baktığını fark eder ("Yine mi havayla konuşuyorsun?"). Bu hem mizah hem yalnızlık hissi yaratır.
3. **Ses kişiliği:** Sistem en çok duyulan "karakter". Replik havuzu en özenli seslendirmeyi gerektiriyor.
   - Kurguda insan olmayan bir varlık olduğu için, tasarlanmış (klonlanmamış) bir yapay zekâ sesi burada tematik olarak meşru.
   - 07 raporundaki hibrit modelle uyumlu: ana kadro insan, Sistem ve kalabalık AI.
   - Beyan şeffaf olmalı [25].
4. **Evrim:** Sistem ilk başta soğuk ve bürokratik konuşur. Bağ kurdukça kişilik kazanır, bazen şaka yapar, bazen arızalanır. Arıza anları P3 gizeminin ipuçlarıdır ("Yönetici erişimi reddedildi").
5. **Modüler yetenek çipleri:** NieR'deki HUD çipleri gibi [BT]. İsteyen oyuncu hasar sayılarını ve mini haritayı "kaldırıp" daha sade bir görünüm seçebilir. Bu aynı zamanda erişilebilirlik ve sade oyun seçeneğidir.
6. **Gerçek zamanlı ama güvenli:** Dövüş sırasında hızlı erişim menüsü zamanı %20'ye yavaşlatır (Dead Space'in gerilimi ile erişilebilirlik arasında bir orta yol). Tam duraklatma bir ayar olarak sunulur.
7. **Bildirim hiyerarşisi:** Kritik bildirimler (seviye, uyanış, görev) tam ekran ve sesli olur. Rutin bildirimler (ganimet) köşede ve sessizdir. Bildirim yorgunluğu, sürüklenmeyi bozan en yaygın sorunlardan biri.

---

## 6. Karakterler, Bağlar ve Romans

### 6.1 Yoldaş tasarım ilkeleri

| Model | Ne alıyoruz | Nasıl |
|---|---|---|
| Persona confidant [31] | Bağ = mekanik güç | Her bağ seviyesi bir dövüş ya da kasaba yeteneği açar. Son seviyede ortak **"bağ ultimate"** sinematiği |
| Fire Emblem destekleri [BT] | Yoldaşlar birbiriyle ilişki kurar | Kamp ateşinde ikili sohbetler. Yoldaşlar arası dostluk ve çatışma |
| BG3 onay sistemi [BT] | Dünya ve kararlar yoldaşın gözünden | Her büyük seçime en az bir yoldaş tepkisi. Onay, görevleri açar ya da kapatır |
| Dragon's Dogma pawn [32] | Oyuncunun yarattığı yoldaş | Uzun vadede asenkron ödünç verme (araştırma kalemi) |
| Hades ilişkileri [22] | Ölüm ve döngü sonrası özel replikler | Geri Yükleme ve déjà vu replikleri |

**Her yoldaşta olmalı:**
- Kendi hedefi, bir sırrı ve bir kusuru
- Oyun dengesine etki eden kişisel görev (P5)
- Oyuncunun eski hayatına bir tepki ("Aşçı mıydın? Bana o yemeği yap")

Hedef 4–6 derin yoldaş (02 raporu). Karaktersiz harem en çok eleştirilen trope'lardan biri (01 raporu [37]).

### 6.2 Romans

- **Talep:** Anime kitlesinde ilişki rotaları güçlü bir motivasyon. Otome/villainess alt türü kadın kitleyi çekiyor [37]. Karakter yaratmada cinsiyet seçimi ve farklı romans rotaları kitleyi genişletir (01 raporu).
- **Tuzaklar ve kurallar:**
  - Tüm romans edilebilir karakterler **açıkça yetişkin** olmalı. Yaşları kanonik olarak belirtilmeli, görsel tasarımları da yetişkin olmalı. "1000 yaşında ama çocuk görünümlü" kalıbı kesinlikle olmamalı.
  - Rıza açık olmalı, reddetme seçeneği her zaman bulunmalı. Yoldaş, oyuncuya "mekanik ödül" olarak sunulmamalı.
  - Romans oyuncunun seçimine göre açılmalı ama karakter bütünlüğü korunmalı. Herkesin her oyuncuyla romans yaşadığı "playersexual" tasarım eleştiri alıyor [BT, orta].
  - Platform ve derecelendirme: Steam'in Temmuz 2025 kuralı ödeme işlemcisi standartlarını ihlal edebilecek içeriği yasaklıyor [27]. (Doğrulandı 24.09.2026: kural ~16 Temmuz 2025'te Steamworks kurallarına 15. madde olarak eklendi. Kaldırılan oyunların çoğu ensest, kölelik ve rıza dışı temalı "Adults Only" oyunlardı. PEGI 12/16 ve ESRB T hedefli romans bu kuralın kapsamı dışında kalır, ama "köle harem" gibi trope'lar doğrudan risk alanında.) Hedef PEGI 12/16 ve ESRB T (04 raporu). Mushoku Tensei'nin Bilibili'den kaldırılması gibi vakalar itibar riskini gösteriyor [36].
- **Monetizasyon ("waifu/husbando" çekiciliği, yırtıcılık olmadan):**
  - İzinli: yoldaş kıyafetleri **doğrudan ve sabit fiyatla** satılır, fotoğraf modu pozları, herkesin aynı fiyata alabildiği hikâye DLC'leri ("Festival Günü" bölümü), OST ve artbook.
  - Yasak:
    - Romans ya da yoldaşı gacha arkasına koymak
    - Parayla alınan "sevgi hediyeleri"
    - Yalnızlığı sömüren bildirimler ("Seni özledim, geri dön")
    - Güç satmak
  - Bu kurallar 03 ve 04 raporlarındaki kırmızı çizgilerle uyumlu.
  - **LLM'li "sanal sevgili" riski:** AI companion uygulamalarına yönelik düzenleyici baskı artıyor. İtalya'nın Replika'ya verdiği ceza ve Kaliforniya'nın SB 243 companion chatbot yasası buna örnek [BT, orta]. SB 243'te, yalnızca oyun konularıyla sınırlı oyun içi botlar için bir istisna olduğu biliniyor [BT, düşük–orta]. **Romans yoldaşlarında serbest LLM sohbeti kullanılmamalı.**

---

## 7. Yapay Zekâ Destekli NPC'ler (2025–2026)

### 7.1 Yayımlanmış ve duyurulmuş örnekler

| Oyun / proje | Ne yapıyor | Tepki / durum | Ders | Güven |
|---|---|---|---|---|
| **Where Winds Meet** (NetEase, 14 Kas 2025) | Açık dünyada LLM ile sohbet eden NPC'ler. Oyun Steam'de 251.008 eşzamanlı oyuncuya ulaştı (23 Kas 2025; doğrulandı 24.09.2026) | Oyuncular NPC'leri manipüle etti (PC Gamer başlığı: "karakterimin ondan hamile olduğuna inandırdım"). NPC uydurma hamileliği sorgulamadı, ilişki seviyesi yine de yükseldi. Oyuncular "Solid Snake yöntemi" ile NPC'leri kandırıp yan görevleri atlattı, yani LLM oynanış kurallarını da delebildi (eklendi 24.09.2026). Uydurma sırlar ve dönem hataları sürükleyiciliği bozdu | Serbest sohbet, lore tutarlılığı ve güvenlik için büyük risk. Viral ilgi ile kalite algısı ters yönde işleyebilir | [O] [23][24][34] |
| **inZOI** (Krafton, EA Mart 2025) | "Smart Zoi": NVIDIA ACE tabanlı, cihazda çalışan küçük dil modeliyle NPC davranışı. İsteğe bağlı ve RTX gerektiriyor | Yenilik olarak ilgi gördü | Yerel SLM'ler ticari bir oyunda çalışıyor, ama donanım bağımlılığı var | [BT, orta] |
| **PUBG Ally** (Krafton × NVIDIA, CES 2025'te duyuruldu) | Sesle komut alan, cihazda çalışan "birlikte oynanabilir karakter" | Yayın durumu ve tarihi bu oturumda doğrulanamadı | Takım arkadaşı yapay zekâsı dar görev alanında daha güvenli | [BT, düşük–orta] |
| **Mecha BREAK** (Amazing Seasun) | NVIDIA ACE demosunda sesle konuşulan mekanik NPC | Çıkış sürümünde bulunup bulunmadığı doğrulanamadı | Demo ile çıkış sürümü arasında fark olabilir | [BT, düşük] |
| **Whispers from the Star** (Anuttacon) | Oyuncu, uzayda mahsur kalan bir karakterle sesli ya da yazılı konuşuyor. Oyunun kendisi bu sohbet | Kabul ve satış verileri doğrulanamadı | LLM'in **oyunun konusu** olduğu durumda tuhaflıklar tolere ediliyor | [BT, düşük–orta] |
| **Suck Up!** (Proxima) | Vampir, ev sahiplerini ikna edip içeri girmeye çalışıyor | Yayıncılar arasında viral oldu | LLM kısa ve kapalı bir oyun döngüsünde ve komedi türünde iyi çalışıyor | [BT, orta] |
| **Vaudeville** (Bumblebee, 2023) | Serbest sesli sorgulama yapılan dedektif oyunu | Karışık tepki (tutarsızlık) | Uzun anlatıda LLM tutarlılığı zayıf | [BT, orta] |
| **Dead Meat** (Meaning Machine) | Serbest metinle şüpheli sorgulanan cinayet oyunu | Çıkış durumu doğrulanamadı | Dar senaryo ve net kurallarla daha kontrollü | [BT, düşük] |
| **LLM for Unity kullanan oyunlar** | Steam ve itch'te küçük ölçekli örnekler var (Verbal Verdict, Case Closed, Love and Lie, CielChan Anime Desktop AI Companion vb.) | Çoğu niş ya da deneysel | Yerel LLM entegrasyonu indie ölçeğinde uygulanabilir | [Y] [3] |

### 7.2 Araçlar (bu oturumda GitHub'dan doğrulandı)

| Araç | Tür | Lisans | Motor/platform | Önemli notlar | Kaynak |
|---|---|---|---|---|---|
| **llama.cpp** | Yerel LLM çıkarımı (C/C++) | MIT | Hepsi | Diğer eklentilerin çoğunun temeli | [1] |
| **NobodyWho** | Yerel LLM, STT, TTS (Rust) | EUPL-1.2. README: "proprietary ve ticari projelerde ücretsiz". Yalnızca NobodyWho kodunda yapılan değişiklikler açılmak zorunda | Godot (masaüstü + Android; **iOS ve web yok**), Python, Flutter, RN | Model boyutunun ~1,5 katı boş RAM gerekiyor. Başlangıç için Qwen3 0.6B (~330 MB) öneriliyor. Gramerle tip güvenli araç çağrısı, Kokoro/Pocket TTS/Supertonic TTS, Whisper STT | [2] |
| **LLM for Unity** | Yerel LLM ve RAG | Apache-2.0 | Unity 2021 LTS–Unity 6. PC, Android, iOS, VR | GBNF gramer ve fonksiyon çağırma, ANN tabanlı RAG, uzak sunucu seçeneği | [3] |
| **Llama-Unreal** | Yerel LLM eklentisi | MIT | UE5 (5.7 derleme notları) | Windows'ta varsayılan Vulkan. CUDA'ya göre ~%3 fark olduğu belirtiliyor | [4] |
| **NVIDIA NVIGI** (v1.7.0) | Oyun içi çıkarım SDK'sı (LLM, ASR, TTS, embedding) | Godot eklentisi Apache-2.0. Modeller ayrı lisanslı | **Windows 10/11, AVX2, NVIDIA GPU 8 GB+ VRAM (12 GB+ öneriliyor)**. Eklentiler RTX 30x0 ve üstünü istiyor, bazıları yalnızca RTX 40x0+ | Resmî Godot GDExtension (Mayıs 2026). Godot 4.5+, 4.7 ile doğrulanmış. Chatterbox TTS 23 dil | [6][7] |
| **NVIDIA ACE** | Dijital insan mikroservisleri (NIM) | Repo Apache-2. NIM'ler NVIDIA AI Enterprise lisansıyla | Bulut/PC | README'ye göre NIM'ler değerlendirme lisansıyla alınıyor. "Nemotron-3 4.5B SLM" erken erişimde (README eski olabilir) | [5] |
| **Audio2Face-3D** | Sesten yüz animasyonu | SDK ve UE5 eklentisi (v2.5, UE 5.5/5.6) MIT. Eğitim framework'ü Apache. NIM NVIDIA lisanslı | UE5, Maya | Gerçekçi yüzlere yönelik. Anime karakterde viseme tabanlı basit lip-sync daha uygun olabilir | [8] |
| **Inworld** | Artık ağırlıkla TTS ve Realtime API | TTS eğitim kodu MIT | — | GitHub org'da 24 public repo var: `tts`, `inworld-api-examples`, ElevenLabs'ten ses klonu taşıma aracı. "Runtime" şablonlarının çoğu Temmuz 2026'da arşivlendi. **Public listede Unity/Unreal karakter SDK'sı yok.** Çıkarım: oyun karakter motoru odağından uzaklaşmış [O] | [9] |
| **Convai** | Bulut tabanlı konuşan NPC | SDK açık (lisans ayrıca kontrol edilmeli) | Unreal (V4 eklentisi Ekim 2025), Unity WebGL | Unreal SDK repo'su aktif (son güncelleme 2026-09-19). Bilgi tabanı, eylemler, lip-sync. README'de uzun süreli hafıza "yakında" görünüyor. Fiyat doğrulanamadı | [10] |
| **Qwen3 / Qwen3.5** | Açık ağırlıklı LLM | Qwen3 README: "tüm açık ağırlıklı modeller Apache 2.0". Qwen3.5 lisansı HF'deki dosyaya yönlendiriyor, model kartında teyit edilmeli | — | Qwen3.5-0.8B/2B/4B/9B 2026-03-02'de çıktı. README 201 dil ve lehçe iddia ediyor. Qwen3.8 (Ağustos 2026) büyük modeller | [11][12] |
| **Gemma 4 / Gemma 3n / Gemma 3 270M** | Açık ağırlıklı LLM | **Lisans bu oturumda doğrulanamadı** | — | Gemma 4: E2B, E4B, 26B A4B ve 31B boyutları. Gemma 3 270M fonksiyon çağırma için ince ayar örneğine sahip | [13] |
| **Qwen3Guard** | Moderasyon modeli | Lisans README'de görülemedi (Qwen'in genel Apache beyanı var) | — | 0.6B, 4B ve 8B boyutları. "Gen" ve akış için "Stream" varyantları. 1,19 milyon etiketli örnekle eğitilmiş, 119 dil | [14] |
| **Llama Guard 3 (1B/8B), Prompt Guard** | Moderasyon ve prompt enjeksiyonu tespiti | Llama 3.2 Community License | — | Lisansın atıf ve kullanım koşulları ayrıca okunmalı | [15] |
| **ink / Yarn Spinner / Dialogue Manager / Dialogic** | Dallanan diyalog yazımı | Hepsi MIT | ink: Unity ve genel. Yarn: Unity/Godot. Dialogue Manager ve Dialogic: Godot | Tepkisel diyalog için temel araçlar (LLM gerektirmez) | [16][17][18] |

### 7.3 Maliyet ve gecikme

- **Yerel model:**
  - Oyuncu başına ek maliyet 0. Sunucu yok, çevrimdışı çalışır.
  - **Bedeli:** VRAM ve RAM rekabeti. Oyunun kendi render yükü zaten VRAM kullanıyor, NVIDIA bu yüzden 12 GB öneriyor [6][7]. CPU'ya düşüldüğünde yavaşlar.
  - Model boyutunun ~1,5 katı RAM kuralı var [2].
  - Oyuncu kitlesinin GPU dağılımı, ilk token gecikmesi ve Türkçe/Japonca kalitesi **hedef donanımda ölçülmeli**. Bu container'da GPU yok ve model indirme (Hugging Face) engelli, bu yüzden ölçüm yapılamadı.
- **Bulut model (örnek hesap, gerçek fiyat değil):**
  - Varsayım: girdi 0,10 $/1M token, çıktı 0,40 $/1M token.
  - Tek bir konuşma: 1.500 girdi token'ı (kişilik + lore RAG + geçmiş) ve 80 çıktı token'ı ≈ 0,00018 $.
  - Oyuncu başına 200 konuşma ≈ 0,04 $. 100 bin oyuncuda ≈ 3.700 $.
  - Tutar küçük ama **süresiz ve değişken bir yükümlülük**. Premium (tek seferlik satış) modelde bu, sonsuz bir sunucu borcu demek. Ayrıca oyunu çevrimiçi olmaya zorlar ve kişisel veri (KVKK/GDPR) konusunu açar.
  - Gerçek fiyatlar sağlayıcının güncel sayfasından alınmalı. Bu oturumda doğrulanamadı.

### 7.4 Güvenlik, moderasyon, beyan ve mevzuat

- **Tehdit modeli:** Prompt enjeksiyonu (WWM örneği [23]), lore dışı ya da uydurma bilgi, müstehcen veya nefret içerikli çıktı, yaş derecesinin aşılması, telifli metnin tekrar üretilmesi.
- **Korumalar (katmanlı):**
  1. Kişilik ve lore için sabit sistem istemi ve yalnızca onaylı lore kartlarından RAG
  2. **GBNF/JSON gramerle kısıtlı çıktı**: niyet, duygu, en fazla 2 cümle ve izinli eylem listesi [2][3]
  3. Girdi ve çıktıda moderasyon (Qwen3Guard-Stream-0.6B ya da Llama Guard 3-1B [14][15])
  4. Kara liste ve konu filtresi. Romans, sağlık ve siyaset konuları kapalı
  5. Başarısızlıkta el yazımı yedek replik ("Sistem: Bu sorgu yetkiniz dışında.")
  6. Hız sınırı ve oturum başına kota
  7. Loglar yalnızca yerelde tutulur
- **Steam:**
  - Ocak 2024'ten beri önceden üretilmiş ve **canlı üretilen** yapay zekâ içeriğinin beyanı gerekiyor. Canlı üretimde korumaların açıklanması isteniyor [28, erişilemedi; 05 raporu].
  - Form, oyuncunun tükettiği içeriğe odaklanacak şekilde güncellendi [26].
  - 2025 çıkışlarının ~%20'si yapay zekâ beyan etti [25].
- **AB AI Act md. 50 (şeffaflık):** Yapay zekâyla etkileşime girdiğini bilmeyen kişiyi bilgilendirme yükümlülüğü var. **Düzeltme (24.09.2026):** Md. 50, 2 Ağustos 2026'dan beri uygulanıyor. Digital Omnibus yüksek riskli sistemlerin tarihlerini 2027–2028'e erteledi, ama md. 50'yi ertelemedi. Tek istisna: 2 Ağustos 2026'dan önce piyasaya sürülmüş sistemler için md. 50(2) makinece okunabilir işaretleme yükümlülüğüne 2 Aralık 2026'ya kadar geçiş süresi var. Bu nedenle LLM'li her karakter için "AI" bildirimi bugünden zorunlu kabul edilmeli. Pratik çözüm: LLM'li her karakterde görünür bir "AI" rozeti ve ayarlarda açıklama.
- **Seslendirme sanatçısı hakları:** SAG-AFTRA 2025 Interactive Media sözleşmesi dijital kopya için rıza ve ücret şartı getiriyor [30]. Japonya'daki "NO MORE 無断生成AI" kampanyası (07 raporu) ile birlikte düşünüldüğünde, gerçek bir sanatçının sesiyle **anlık** üretim yapılmamalı.

### 7.5 Oyuncu tepkisi

- **Olumlu:**
  - Yenilik ve yayıncılar arasında viral olma (Suck Up! [BT]).
  - Mekanik açıkça "LLM ile konuşmak" olduğunda tolerans yüksek (Whispers from the Star [BT]).
- **Olumsuz:**
  - Büyük ve yazılı bir dünyada tutarsızlık hemen fark ediliyor (WWM [23][24]).
  - "AI slop" damgası anime kitlesinde güçlü. Clair Obscur'un Indie Game Awards ödüllerini kaybetmesi buna örnek [35]. (Nüans, 24.09.2026: ödüller 20 Aralık 2025'te geri alındı; neden, çıkış sürümünde kalan AI ile üretilmiş geçici dokular ve başvurudaki "gen AI yok" beyanıydı. Ders: placeholder varlıklar da izlenmeli ve beyan eksiksiz olmalı.)
  - Beyanlı oyunların daha az ilgi gördüğüne dair iddialar var, ama nedensellik kanıtlanmadı [25].
- **Sonuç:** LLM, ana anlatının taşıyıcısı olmamalı. Kurguda tuhaflığı açıklanabilen tek bir karakterde (Sistem) sınırlı bir deney olarak kalmalı.

### 7.6 Öneri: dört katmanlı ve güvenli kullanım

| Katman | Ne | Ne zaman | Risk |
|---|---|---|---|
| **K0 — Geliştirmede LLM (önerilen, çekirdek)** | Claude Code ile bark ve varyasyon taslakları, NPC rutin metinleri, olay→özet şablonları. **Hepsi insan editörden geçer**, dosyalara yazılır, "önceden üretilmiş" olarak beyan edilir | Hemen | Düşük |
| **K1 — Deterministik tepkisellik** | ink/Yarn/Dialogue Manager ile olay bayrakları, ilişki vektörü ve hafıza kayıtları. Déjà vu, yoldaş yorumları, "önceki bölümde" | Dikey dilim | Düşük |
| **K2 — Sınırlı yeniden ifade** | Yerel küçük model (ör. Qwen3.5-0.8B/2B ya da Gemma 4 E2B, lisans teyidinden sonra) **yalnızca** önceden yazılmış anlamı farklı kelimelerle söyler (Kronik ve bark çeşitliliği). Gramer kısıtlı, yeni bilgi üretmez | Çıkış sonrası, A/B testi | Orta |
| **K3 — "Sistem'le Konuş" (opt-in, deneysel)** | Oyuncu Sistem'e serbest metin yazar. Sistem lore RAG'ı ve niyet gramerleriyle cevap verir, gerekirse "yetkiniz dışında" der. Varsayılan olarak kapalıdır, AI rozeti vardır, Steam'de canlı üretim beyanı yapılır | Canlı operasyon deneyi | Orta–Yüksek |

**Motor notu:**
- Godot'da: NobodyWho [2]. RTX'li oyuncular için isteğe bağlı olarak NVIGI [7].
- Unity'de: LLM for Unity [3].
- Unreal'da: Llama-Unreal [4].
- NVIGI yalnızca NVIDIA/Windows'ta çalıştığı için **tek arka uç olamaz**.

---

## 8. Görsel-İşitsel Sürükleyicilik

### 8.1 Anime sinematik yönetimi

- **Zamanlama:**
  - Vuruşta hitstop (3–8 kare), ağır vuruşta 2–4 karelik **impact frame** (negatif, siyah-beyaz ya da tek renkli flaş) ve kısa kamera sarsıntısı.
  - Guilty Gear Xrd'nin yöntemi: 3D modelleri 2'ler ve 3'lerle "limited animation" gibi oynatmak, elle ayarlanmış normaller, hareket bulanıklığı yok (GDC 2015 konuşması [BT, yüksek]).
- **Kamera dili:** Eğik açılar, hız çizgileri, smear kareleri, poz tutma, kısa dolly-zoom. Ultimate'larda Persona/ZZZ tarzı karakter **cut-in**'leri [BT].
- **Tipografi:** Vuruş anında dünyada beliren onomatopeler ("GÜM!", "ドン"). Oyuncunun diline göre yerelleştirilir.
- **İmza an, bizim "Arise"ımız: Ad Verme töreni.**
  - Yenilen bir canavar, düşmüş bir ruh ya da kurtarılan bir köy oyuncunun verdiği adla bağlanır. Slime'daki isim verme trope'unun orijinal bir yorumu (01 raporu).
  - Sinematik akış: zaman durur, Sistem "Ad kabul edildi" der, vokal parça girer, bağlanan varlık yeni formuna geçer.
  - Oyuncunun **kendi yazdığı** isim kurgusal otorite kazanır (meta-sürüklenme).
  - Her dünya tohumu için ayrı bir sözel çağrı önerildi (Bölüm 10).
- **Rütbe atlama töreni:** 03 raporundaki "Status mühürleme" tapınak sahnesi. Kısa, atlanabilir ve her seferinde küçük bir varyasyonla.
- **Flaş güvenliği:** Impact frame'ler için "Flaş azaltma" ayarı olmalı: süre ve kontrast kısılır. WCAG 2.3.1'deki "saniyede 3 flaş" eşiği referans alınmalı [BT, yüksek].

### 8.2 Müzik

- **Leitmotif haritası:** Sistem (soğuk synth ile başlayıp zamanla sıcaklaşan tema), her yoldaş, her fraksiyon, zindan katmanları ve "Dünya/eski hayat" teması (piyano). Ad Verme anında Dünya teması ile Sistem teması birleşir.
- **Adaptif müzik:**
  - Dikey katmanlama: keşif → tehlike → dövüş.
  - Yatay geçişler: boss fazları.
  - Vokal girişi yalnızca "aura anı"nda (Sawano tarzı "drop"ta vokal).
- **Uydurma dilde şarkılar:** NieR'in "chaos language"ı [BT, yüksek]. Dünyanın dilinde yazılmış şarkı sözleri, oyuncunun öğrendiği kelimelerle kısmen anlaşılır hâle gelir. Dil mekaniğine bağlanır.
- **OP/ED:** Her "sezon" bir açılış ve kapanış jeneriği (P10). Üretim: 07 raporuna göre AI (ACE-Step 1.5, MIT) taslağı ve insan beste/düzenleme.

### 8.3 Ses, seslendirme ve lip-sync

- **Hibrit model (07 raporu):** Ana kadro insan sesi, geniş kadro ve Sistem tasarlanmış AI sesi. Hiçbir gerçek kişinin sesi klonlanmaz.
- **Japonca dublaj:** Anime kitlesi için güçlü bir özgünlük sinyali. 07 raporunda faz 2 olarak önerildi. Oyuncunun adı Japonca VO'da katakana ön kayıtlarıyla ya da unvanla söylenir.
- **Efor sesleri** (nefes, vuruş bağırışları) ve **Sistem replikleri** en sık duyulan sesler. Kalite bütçesi önce bunlara ayrılmalı.
- **Lip-sync:**
  - Anime stilinde viseme tabanlı ağız şekilleri yeterli ve stile uygun: uLipSync (Unity, MIT) [19], Rhubarb (motordan bağımsız ön işleme, MIT) [19].
  - Gerçekçi yüz gerekirse Audio2Face-3D SDK ve UE5 eklentisi (MIT) [8].

### 8.4 Arayüz ses tasarımı ve haptik

- **İmza ses seti:** Sistem bildirimi (tek ve tanınabilir bir "çınlama"), seviye atlama stinger'ı, görev tamamlama, uyarı ve arıza (bozuk/glitch versiyonu). Solo Leveling'in bildirim sesi gibi bir **marka sesi** hedeflenmeli ama birebir taklit edilmemeli.
- Diegetik arayüz sesleri 3D uzamsal olarak panelin konumundan gelir. Diyalog sırasında müzik ve SFX kısılır (ducking).
- **Haptik:** Düşük HP'de kalp atışı titreşimi, şarjlı saldırılarda DualSense adaptif tetik, Sistem bildiriminde kısa bir "tık". Steam Input üzerinden sunulur, desteklenmeyen cihazlarda rumble'a düşer [BT, orta].

### 8.5 Fotoğraf modu

- Eski Telefon'un kamerası oyun içinde fotoğraf modunu açar (diegetik).
- Özellikler: anime pozları ve ifadeleri, "manga paneli" ve "anime ekran görüntüsü" (altyazı çubuğu) filtreleri, çerçeveler, yoldaşları kadraja davet etme.
- Paylaşım, organik pazarlama için önemli (03 raporu, mekanik #21).

### 8.6 Erişilebilirlik (P0 paketi)

- Altyazı: boyut, arka plan, konuşan adı, yön göstergesi
- Tam tuş atama, tek elle oynama önayarları
- Renk körlüğü modları
- Kamera sarsıntısı, flaş ve hareket bulanıklığı ayarları
- Zorluk yardımı ("Sistem Desteği", 03 raporu)
- Dil engelini atlama ve diegetik arayüzde duraklatma seçeneği
- Menüler için ekran okuyucu: Godot'da AccessKit tabanlı destek var (4.7 changelog'unda AccessKit ve ekran okuyucu düzeltmeleri [20]). Unity ve Unreal'da ayrıca araştırılmalı.
- Kıyas noktası: The Last of Us Part II'nin 60'ı aşkın erişilebilirlik seçeneği [BT, yüksek].

### 8.7 Yerelleştirme

- **Sıra (02 raporu):** İngilizce → Japonca → Basitleştirilmiş Çince → Korece → Türkçe → PT-BR → İspanyolca.
- **Kültürelleştirme:**
  - Dünyanın uydurma yazısı ve dili **bilinçli olarak çevrilmez** (mekanik).
  - Onomatopeler, sayfa ve font (CJK) desteği, metin uzaması (Almanca/Türkçe ~%30) dikkate alınmalı.
  - Oyuncu adının çekim ekleri (Türkçe ünlü uyumu: "Ahmet'e / Ayşe'ye") için ek-yardımcı fonksiyonlar gerekir. Türkçe'de sık yapılan bir hata.
- **Dublaj:** EN ve JA. Türkçe'de önce altyazı, pazar karşılık verirse dublaj (07 raporu).

---

## 9. Önceliklendirilmiş 31 Sürükleyicilik Tekniği

Öncelik: **P0** dikey dilimde olmalı · **P1** çıkışta olmalı · **P2** çıkış sonrası · **P3** deneysel. Maliyet: Düşük/Orta/Yüksek (tek geliştirici ve Claude Code ölçeğinde görece). Etki: sürüklenme ve bağlılığa beklenen katkı (tasarım yargısı, olgu değil).

| # | Teknik | Maliyet | Etki | Öncelik |
|---|---|---|---|---|
| 1 | **Sistem = karakter**: kişilik, ses, evrim, arıza anları (§5) | Orta | Çok yüksek | P0 |
| 2 | **İmza Sistem bildirim sesi** ve haptik "tık" seti (§8.4) | Düşük | Yüksek | P0 |
| 3 | **Oynanabilir "Son Gün"** ve eşyalarla diegetik karakter yaratma (§3.1) | Orta | Çok yüksek | P0 |
| 4 | **Eski meslek → perk, diyalog ve pişmanlık görevi** (dikey dilimde 3 meslek) | Orta | Yüksek | P0 |
| 5 | **Lonca kaydı töreni**, fiziksel Status kartı ve F-rank damgası (§3.4) | Düşük | Yüksek | P0 |
| 6 | **Dünya-uzayında holografik Status paneli** (dövüşte yavaşlatma, isteğe bağlı duraklatma) | Orta | Yüksek | P0 |
| 7 | **Geri Yükleme döngüsü**, bedeli ve déjà vu replikleri (§3.6) | Orta–Yüksek | Çok yüksek | P0 |
| 8 | **NPC hafızası**: olay bayrakları, ilişki vektörü, hatırlama replikleri (K1) | Orta | Yüksek | P0 |
| 9 | **Anime dövüş dili**: hitstop, impact frame, cut-in, onomatope | Orta | Çok yüksek | P0 |
| 10 | **İmza an: Ad Verme töreni** sinematiği ve vokal parça | Orta–Yüksek | Çok yüksek | P0 |
| 11 | **Yoldaş bağı**: ikili sohbetler, bağ yeteneği, ortak ultimate (dikey dilimde 2 yoldaş) | Yüksek | Çok yüksek | P0 |
| 12 | **Erişilebilirlik P0 paketi** (flaş azaltma dahil) | Orta | Yüksek | P0 |
| 13 | **Kademeli dil edinimi** ve glif sözlüğü, atlanabilir (§3.3) | Orta | Yüksek | P1 |
| 14 | **Eski Telefon diegetik hub**: kamera, notlar, müzik, pil, bozuk mesajlar | Orta | Yüksek | P1 |
| 15 | **"Önceki bölümde…" özeti**, başlık kartı ve sonraki bölüm önizlemesi (P10) | Orta | Yüksek | P1 |
| 16 | **Leitmotif haritası ve adaptif müzik**, OP/ED | Orta | Yüksek | P1 |
| 17 | **Takvim ve şehir rutinleri** (Persona ritmi, NPC programları) | Yüksek | Yüksek | P1 |
| 18 | **Fraksiyon itibarı ve görünür dünya değişimi** (kasaba büyümesi, afişler) | Yüksek | Çok yüksek | P1 |
| 19 | **Keşif Defteri**: bilgiye dayalı ilerleme (Outer Wilds) | Orta | Yüksek | P1 |
| 20 | **Gerçek tarih entegrasyonu**: gün sayacı, mevsim, doğum günü (opt-in) | Düşük | Orta | P1 |
| 21 | **Fotoğraf modu** (telefon kamerası, manga paneli) | Orta | Orta–Yüksek | P1 |
| 22 | **Haptik profil** (kalp atışı, adaptif tetik) | Düşük–Orta | Orta | P1 |
| 23 | **Gerçek Dünya Görevi** ve dinlenme önerisi (opt-in) | Düşük | Orta (PR) | P1 |
| 24 | **Yayıncı modu** (gerçek isim gizleme, telifsiz müzik) | Düşük | Orta | P1 |
| 25 | **Asenkron "diğer isekai'lılar"**: notlar ve ölüm yankıları (Elden Ring) | Orta | Yüksek | P2 |
| 26 | **İsmin seslendirilmesi** (ön kayıtlı isim listesi ve unvan) | Orta | Orta | P2 |
| 27 | **Japonca dublaj ve çift ses seçeneği** | Yüksek | Yüksek (anime kitlesi) | P2 |
| 28 | **Gerçekçi Mod** (açlık, yorgunluk, kirli kıyafet, NPC tepkisi; KCD tarzı) | Orta | Orta | P2 |
| 29 | **Tek Hayat / Sistemsiz mod** | Düşük | Orta (niş) | P2 |
| 30 | **Pawn benzeri asenkron yoldaş ödünç verme** (Dragon's Dogma) | Yüksek | Orta–Yüksek | P3 |
| 31 | **"Sistem'le Konuş"**: yerel, gramer kısıtlı, opt-in LLM (K3) | Orta–Yüksek | Belirsiz | P3 |

**En yüksek etki/maliyet oranına sahip beş teknik:** #2 imza ses, #5 Lonca kaydı, #1 Sistem karakteri, #4 eski meslek, #8 NPC hafızası.

---

## 10. Orijinal IP: Üç Dünya Tohumu

> Üç tohum da Solo Leveling tarzı görünür Sistem ilerlemesini, DanMachi tarzı "zindan üstü şehir hayatını" ve isekai'nin duygusal bedelini birleştiriyor. İsimler, terimler ve görsel kimlik orijinal. Trope'lar serbest, ama ifade korunuyor (01 raporu). Nihai isimler için marka taraması gerekli.

**Tohum A — *Kut Ağacı* (Türk-Orta Asya kozmolojisinden serbest ilham):** Ölümle yaşam arasında kalan oyuncu, gökten yeraltına uzanan dev bir dünya ağacının köklerine kurulmuş kervan şehri **Otağkent**'te uyanır. Ağacın dalları gök katlarına, kökleri karanlık yeraltı katlarına iner. Şehirde her biri bir koruyucu ruhun yönettiği **Ocak**'lar var. Ocaklar, maceracıları himaye eden ailelerdir ve ruhları insan kılığında sokaklarda dolaşan, kaprisli, yarı unutulmuş varlıklardır. Oyuncunun Sistem'i **Kut Defteri** adında, talihini ölçen bir defterdir. Her gün "Kut görevleri" yazar, her kat inişte oyuncunun rütbesini mühürler. Defterin son sayfası boştur ve söylentiye göre oraya yazılan kişi eve dönebilir. Bedeli şudur: her derin iniş, eski hayattan bir anıyı defterden siler. Dünya'daki annesinin yüzünü unutmaya başlayan oyuncu, anılarını korumak ile güçlenmek arasında seçim yapar. İmza çağrı olarak Ad Verme'de *"Kut'um tanıktır: adın ___!"* önerilir. Görsel kimlik keçe, kilim motifleri, bozkır gökyüzü ve kervansaray kubbelerinden oluşur. 01 raporunun işaret ettiği, isekai'de neredeyse hiç kullanılmamış bir palet. Mitolojik öğeler public domain folklordan özgün yorumla alınmalı. Kutsal figürler birebir kullanılmamalı ve kültürel hassasiyet için danışman görüşü alınmalı [D].

**Tohum B — *Kayıp Eşyalar Şehri*:** Dünya'da kaybolan her şey (şemsiyeler, eşleri kaybolmuş çoraplar, söylenmemiş sözler, unutulmuş şarkılar) bu dünyanın kıyısına vurur. Onlardan örülmüş rengârenk şehir **Bulunmuş** da böyle doğmuştur. İnsanlar da buraya aynı yolla gelir: Dünya'da herkes seni unuttuğunda. Oyuncu da bir sabah burada uyanır, yani bir yerde herkes onu unutmuştur. Sistem, evrenin **Envanter**'idir ve oyuncuyu bir eşya gibi kataloglar. Rütbeler Sıradan'dan Efsanevi'ye nadirlik seviyeleridir. Günlük görevler "sayım"dır, ceza ise "hurdaya ayrılma" korkusudur. Şehrin altında sonsuz raflardan oluşan bir arşiv zindanı olan **Depo** vardır. Canavarları, sahipsiz kalıp çürüyen anılardır. Maceracılar, sahibine eşya ulaştıran **Bulucular Loncası**'nda çalışır. Oyuncu kayıp eşya dükkânı işletir, anılara ev bulur. Duygusal soru şudur: seni kim, neden unuttu? Dünya'da seni hatırlayan tek kişiyi bulursan geri dönebilir misin? İmza an, bir eşyaya ya da ruha **yeniden ad vermek**tir. Adsız kalan her şey Depo'da canavara dönüşür. Nostalji ağırlıklı, sıcak ve melankolik bir ton, Solo Leveling'in karanlığı ile DanMachi'nin şehir sıcaklığı arasında özgün bir yer tutuyor.

**Tohum C — *Eşik*:** Oyuncu Dünya'da bir kazadan sonra komada. Bu dünyadaki her gün, hastane yatağında geçen bir gecedir. Kayıttaki "Dünya'dan ayrılalı N gün" sayacı burada bir **nabız** göstergesine dönüşür. Uyandığı şehir **Eşik**, dipsiz bir zindanın ağzına kurulmuştur. Buradaki herkes "yarım kalmış" insanlardır. Zindanda ne kadar derine inersen Dünya'daki bedenin o kadar uyanmaya yaklaşır. Yani kazanmak, sevdiğin yoldaşlardan ayrılmak demektir. Sistem'in günlük görevleri tuhaf biçimde fizyoterapi egzersizlerine benzer: "100 adım", "nefesini say". Arıza anlarında hastane monitörünün sesi duyulur. Sistem gerçekten bir yaşam destek arayüzü mü, yoksa seni burada tutmak isteyen bir şey mi (P3)? Geri Yükleme, Dünya'da bedenin kalp krizini atlatmasıdır ve her döngü nabzı zayıflatır (P4 bedeli). Takvim, Persona'nın gündüz şehir hayatı ile gece zindan ritmini anlamlandırır. Final seçimi "uyan ya da kal"dır ve birden çok son vardır. İmza çağrı *"Kalbim atıyor: ___, ayağa kalk!"* olabilir. Ton ağır olduğu için mizahi yoldaşlar ve sıcak şehir hayatıyla dengelenmeli. Sağlık temaları duyarlı yazılmalı, uzman görüşü alınmalı [D].

| Kriter | A: Kut Ağacı | B: Kayıp Eşyalar | C: Eşik |
|---|---|---|---|
| Görsel ayırt edicilik | Çok yüksek (bozkır ve kilim paleti) | Yüksek (eklektik obje şehri) | Orta (modern ve fantezi karışımı) |
| Sistem'in kurgusal gerekçesi | Talih defteri | Evrenin envanteri | Yaşam destek arayüzü (gizem) |
| Duygusal bedel | Anı kaybı | Unutulmuş olmak | Uyanmak = ayrılmak |
| Meta-sürüklenme uyumu | Orta | Yüksek (ad verme, eşya) | Çok yüksek (gerçek gün sayacı = nabız) |
| TR pazarında PR kaldıracı | Çok yüksek | Orta | Orta |
| Risk | Kültürel hassasiyet | Ton dengesi | Ağır tema, derecelendirme |

---

## Oyunumuz İçin Çıkarımlar

1. **Tasarım belgesine bir "sürüklenme sözleşmesi" ekle.** Her özellik Bölüm 1'deki dört katmandan en az birine hizmet etmeli. "Sürükleyiciliği bozan an" listesi QA kontrol listesine girmeli (bildirim yorgunluğu, NPC'nin bilmemesi gereken şeyi bilmesi, dördüncü duvarın yanlış kırılması).
2. **Dikey dilimde 12 P0 tekniği bulunmalı.** Bölüm 3'teki 120 dakikalık akış, 03 raporundaki telemetri hunisine bağlanmalı. Steam Next Fest demosu da bu dilim olabilir. İade eşiği 2 saat [21].
3. **Sistem'i ilk gün bir karakter olarak yaz.** Ses tasarımı, replik havuzu, evrim eğrisi ve arıza ipuçları P3 gizemiyle birlikte planlanmalı. Sistem sesi için tasarlanmış AI sesi kullanılabilir ve beyan edilmeli. Ana kadroda insan sesi olmalı (07 raporu).
4. **Tepkiselliği LLM'siz kur.** ink, Yarn Spinner ya da Godot Dialogue Manager (hepsi MIT) ile olay bayrakları, ilişki vektörü ve hafıza kayıtları [16][17][18]. Claude Code bu dosyaları şablonlarla toplu üretebilir, insan editör onaylar (K0 + K1).
5. **Canlı LLM'i ertele.** Çıkışta serbest metin LLM olmamalı. Çıkıştan sonra K2 (yeniden ifade) A/B testi, ardından opt-in K3 "Sistem'le Konuş" denenebilir. Motor seçimine göre NobodyWho, LLM for Unity ya da Llama-Unreal kullanılabilir [2][3][4]. NVIGI yalnızca RTX'li oyuncular için hızlandırıcı olabilir [6][7]. Bulut LLM'e bağımlı bir premium oyun yapılmamalı.
6. **Model lisanslarını tek tek teyit et.** Qwen3.5 küçük modellerinin HF lisans dosyası ve Gemma 4'ün kullanım şartları incelenmeli. Moderasyon için Qwen3Guard-Stream-0.6B ya da Llama Guard 3-1B'nin lisans koşulları okunmalı [11]–[15].
7. **Eski hayat sistemi veri modeli olarak ilk sprintte kurulmalı.** Meslek, hobi, pişmanlık ve "son saat" seçimleri perk, diyalog ve görev tablolarına bağlanmalı. Dikey dilimde 3, çıkışta 8 meslek. Kişisel veriler yalnızca yerelde tutulmalı.
8. **Geri Yükleme'yi hem roguelite döngüsünün hem anlatının omurgası yap.** Döngü sayacı, bedel (Yıpranma/anı), NPC déjà vu replikleri, ölüm nedenine özel replikler (Hades modeli [22]).
9. **İmza anı (Ad Verme) ve bildirim sesini marka varlığı olarak ele al.** Fragman, mağaza sayfası ve kısa videolarda tekrar kullanılacak. Impact frame'lerde flaş azaltma seçeneği zorunlu.
10. **Romans kuralları:** Tüm romans karakterleri yetişkin, rıza açık. Gacha ve sevgi satışı yok, romans yoldaşlarında serbest LLM yok. Hedef PEGI 12/16 ve ESRB T. Steam'in Temmuz 2025 kuralı dikkate alınmalı [27].
11. **Dünya tohumu seçimi:** Türk kitlesinde PR kaldıracı ve görsel ayırt edicilik için **A (Kut Ağacı)**, meta-sürüklenme gücü için **C (Eşik)** öne çıkıyor. İkisi birleştirilebilir: Kut Ağacı dünyasında Eşik'in "komadaki beden" gerekçesi ve gün sayacı kullanılabilir. Karar, 01–03 raporlarındaki sütunlarla birlikte konsept yarışmasında verilmeli.
12. **Diegetik "Eski Telefon"** fotoğraf modunu, günlüğü ve P3 gizemini tek bir tanıdık nesnede toplar. Düşük sanat maliyetiyle yüksek kimlik değeri sağlar ve P1'de öne alınmalı.
13. **Erişilebilirlik ve yerelleştirme ilk günden olmalı.** Türkçe ek uyumu yardımcı fonksiyonları, CJK font altyapısı, altyazı ve flaş ayarları dikey dilimde bulunmalı. Godot seçilirse AccessKit tabanlı ekran okuyucu desteği değerlendirilmeli [20].
14. **Şeffaflık:** Steam AI beyanı dürüst ve ayrıntılı olmalı. LLM'li karakterlerde "AI" rozeti olmalı (AB AI Act md. 50; 2 Ağustos 2026'dan beri yürürlükte, ertelenmedi; düzeltildi 24.09.2026). Kredilerde AI kullanımı açıkça yazılmalı (07 raporu).

---

## Belirsizlikler ve Riskler

- **Doğrulama boşluğu (en büyük risk):** WebSearch bütçesi tükendiği ve alan adları engellendiği için şu iddialar **[BT]** olarak kaldı ve doğrulama ekibi tarafından kontrol edilmeli:
  - inZOI, PUBG Ally, Mecha BREAK, Whispers from the Star, Suck Up!, Vaudeville ve Dead Meat ayrıntıları
  - KCD2, BG3, Dead Space, .hack//, Outer Wilds, NieR, FFX ve Morrowind tasarım ayrıntıları
  - WCAG 2.3.1, Nemesis patenti, SB 243, Replika cezası (AI Act md. 50 tarihi 24.09.2026'da doğrulandı: 2 Ağustos 2026'dan beri yürürlükte)
  - The Last of Us Part II'nin erişilebilirlik seçeneği sayısı
- **LLM teknolojisi hızla değişiyor:** Inworld'ün yeniden konumlanması GitHub vitrininden çıkarıldı [9], şirketin resmî açıklaması görülmedi [O]. Convai fiyatları ve veri politikası doğrulanamadı. NVIDIA ACE README'si güncel olmayabilir [5].
- **Donanım:** Yerel LLM'in hedef kitlenin GPU ve RAM dağılımında çalışıp çalışmayacağı ölçülmedi. NVIGI 8 GB+ VRAM'li NVIDIA ve Windows istiyor [6][7]. Oyunun kendi VRAM bütçesiyle çakışabilir. Türkçe ve Japonca kalitesi küçük modellerde düşük olabilir.
- **Hukuki:**
  - Nemesis tarzı düşman hafızası patent riski taşıyor (hukukçu kontrolü gerekli).
  - Solo Leveling'in mavi pencere estetiği ve "Arise" söylemine fazla benzerlik, "look and feel" riski yaratıyor (01 raporu).
  - Tohum A'da kültürel ve dinî figürlerin kullanımı hassas.
  - KVKK/GDPR: isim ve doğum günü yerelde tutulmalı.
- **"AI slop" algısı:** Anime kitlesi AI kullanımına karşı hassas [35]. Sistem sesi için AI kullanımı tematik olarak savunulabilir, ama ana kadroda AI ses ciddi itibar riski taşıyor (07 raporu).
- **Meta-sürüklenmenin ters tepmesi:** Gerçek tarih ya da "Dünya'dan bozuk mesajlar" bazı oyuncular için rahatsız edici veya manipülatif hissettirebilir. Hepsi kapatılabilir olmalı ve günlük geri dönüşü **cezalandırmamalı** (03 raporundaki kırmızı çizgiler).
- **Kapsam:** 31 tekniğin tamamı tek geliştirici için çok fazla. P0 listesi dışındaki her şey ancak dikey dilim test verisiyle (oturum süresi, iade oranı, "bir bölüm daha" oranı) önceliklendirilmeli.
- **Ağır temalar:** Tohum C'nin koma teması ve Geri Yükleme'deki "Yıpranma" göstergesi, akıl sağlığı ve ölüm konularını duyarlı ele almayı gerektiriyor. Derecelendirme ve mağaza sayfası uyarıları gerekebilir.

---

## Kaynaklar

**A. Bu oturumda doğrudan erişilen birincil kaynaklar (GitHub README, LICENSE ve repo listeleri, 2026-09-24)**

1. llama.cpp (README, MIT): https://github.com/ggml-org/llama.cpp
2. NobodyWho (README; LICENSE EUPL-1.2; platform ve bellek notları): https://github.com/nobodywho-ooo/nobodywho
3. LLM for Unity (README; LICENSE Apache-2.0; kullanan oyunlar listesi): https://github.com/undreamai/LLMUnity
4. Llama-Unreal (README; LICENSE MIT): https://github.com/getnamo/Llama-Unreal
5. NVIDIA ACE (README; lisans tablosu): https://github.com/NVIDIA/ACE
6. NVIDIA In-Game Inferencing (v1.7.0) ve eklenti donanım gereksinimleri: https://github.com/NVIDIA-RTX/NVIGI ve https://github.com/NVIDIA-RTX/NVIGI-Plugins
7. NVIGI Godot Extension (Apache-2.0; gereksinimler): https://github.com/NVIDIA-RTX/nvigi_godot_extension
8. NVIDIA Audio2Face-3D (bileşen lisans tablosu): https://github.com/NVIDIA/Audio2Face-3D
9. Inworld GitHub organizasyonu (GitHub arama API'si ile repo listesi) ve TTS README: https://github.com/inworld-ai ve https://github.com/inworld-ai/tts
10. Convai Unreal SDK (README) ve V4 eklentisi: https://github.com/Conv-AI/Convai-UnrealEngine-SDK ve https://github.com/Conv-AI/Convai-UnrealEngine-SDK-V4
11. Qwen3 README (Apache 2.0 beyanı): https://github.com/QwenLM/Qwen3
12. Qwen3.5 / 3.6 / 3.8 README (sürüm tarihleri ve küçük modeller): https://github.com/QwenLM/Qwen3.5
13. Gemma Cookbook README (Gemma 4 boyutları, Gemma 3 270M) ve gemma paketi: https://github.com/google-gemini/gemma-cookbook ve https://github.com/google-deepmind/gemma
14. Qwen3Guard README: https://github.com/QwenLM/Qwen3Guard
15. PurpleLlama (Llama Guard 3 ve Prompt Guard lisans tablosu): https://github.com/meta-llama/PurpleLlama
16. ink (LICENSE.txt MIT): https://github.com/inkle/ink
17. Yarn Spinner (LICENSE MIT): https://github.com/YarnSpinnerTool/YarnSpinner
18. Godot Dialogue Manager (MIT) ve Dialogic (MIT): https://github.com/nathanhoad/godot_dialogue_manager ve https://github.com/dialogic-godot/dialogic
19. uLipSync (MIT) ve Rhubarb Lip Sync (MIT): https://github.com/hecomi/uLipSync ve https://github.com/DanielSWolf/rhubarb-lip-sync
20. Godot CHANGELOG (4.7, 2026-06-18; AccessKit ve ekran okuyucu girdileri): https://github.com/godotengine/godot/blob/master/CHANGELOG.md

**B. Kardeş raporların doğruladığı kaynaklar (bu oturumda yeniden açılmadı)**

21. Steam iade politikası (03 raporu [7]): https://store.steampowered.com/steam_refunds/
22. Hades diyalog verileri (03 raporu [20]): https://www.gamedeveloper.com/audio/dive-into-the-dialogue-of-i-hades-i-at-gdc-2021 ve https://gamerant.com/hades-developer-infographic-dialogue-breakdown/
23. PC Gamer, Where Winds Meet'in AI sohbet NPC'leri (02 raporu [41]): https://www.pcgamer.com/games/rpg/wuxia-mmo-where-winds-meet-is-full-of-ai-chatbot-npcs-and-people-are-doing-all-the-standard-obscene-stuff-to-them-i-made-him-think-that-my-character-was-pregnant-with-his-child/
24. Where Winds Meet (02 raporu [76]): https://en.wikipedia.org/wiki/Where_Winds_Meet
25. VGC ve Totally Human, Steam AI beyanları (02 raporu [64]): https://www.videogameschronicle.com/news/steam-games-disclosing-generative-ai-use-are-up-800-this-year/ ve https://www.totallyhuman.io/blog/games-with-ai-disclosures-have-grossed-an-estimated-660m-on-steam
26. PC Gamer, Steam AI beyan formu güncellemesi (02 raporu [65]): https://www.pcgamer.com/software/ai/steam-updates-ai-disclosure-form-to-specify-that-its-focused-on-ai-generated-content-that-is-consumed-by-players-not-efficiency-tools-used-behind-the-scenes/
27. Steamworks onboarding, Temmuz 2025 ödeme işlemcisi kuralı (04 raporu [47]): https://partner.steamgames.com/doc/gettingstarted/onboarding
28. Steam AI içerik politikası duyurusu, Ocak 2024 (05 raporu [41], orada da erişilemedi): https://store.steampowered.com/news/group/4145017/view/3862463747997849618
29. Kardeş raporlar (terim, FTUE, kırmızı çizgiler, ses ve yerelleştirme planları): /home/user/isekai/docs/research/01-isekai-anime-analizi.md, 02-pazar-ve-rakip-analizi.md, 03-oynanis-ve-baglilik-tasarimi.md, 04-monetizasyon-ve-regulasyon.md, 07-ai-ses-muzik-seslendirme.md
30. SAG-AFTRA Interactive Media Agreement (07 raporu): https://www.sagaftra.org/contracts-industry-resources/contracts/interactive-media-video-game-agreement
31. Persona 3 Reload 3 milyon ve P5R confidant rehberi (03 raporu [29]): https://www.gematsu.com/2026/06/persona-3-reload-shipments-and-digital-sales-top-three-million ve https://hardcoregamer.com/features/persona-5-royal-confidant-guide/370507/
32. Dragon's Dogma 2 satışları (02 raporu [48]): https://finalweapon.net/2026/05/21/capcom-platinum-titles-march-2026/ ve https://www.capcom.co.jp/ir/english/business/million.html
33. Metaphor: ReFantazio satışları (02 raporu [50]): https://personacentral.com/metaphor-sales-update/
34. SteamDB, Where Winds Meet eşzamanlı oyuncu zirvesi (02 raporu [41]): https://steamcommunity.com/groups/SteamDB/announcements/detail/604172916311982119
35. Engadget, Indie Game Awards ve Clair Obscur (05 raporu [44]): https://www.engadget.com/gaming/the-indie-game-awards-snatches-back-two-trophies-from-clair-obscur-over-its-use-of-generative-ai-164730842.html
36. Mushoku Tensei'nin Bilibili'den kaldırılması (01 raporu [69]): https://www.cbr.com/mushoku-tensei-hard-to-ignore-problem/
37. İsekai trope yorgunluğu ve otome isekai (01 raporu [61][39]): https://www.cbr.com/annoying-isekai-anime-tropes/ ve https://www.cbr.com/otome-isekai-sub-genre-villainess/

**C. Bilgi tabanı iddiaları ([BT], bu oturumda web ile doğrulanamadı, URL verilmedi)**

- Brown & Cairns (2004), Ermi & Mäyrä (2005, SCI modeli), Slater (2009, place ve plausibility illusion)
- Dead Space RIG arayüzü; .hack// sahte işletim sistemi; Morrowind gümrük formu; FFX Al Bhed sözlükleri; Chants of Sennaar ve Heaven's Vault; Outer Wilds'ın 22 dakikalık döngüsü; NieR:Automata HUD çipleri, E sonu ve "chaos language"; KCD1 okuma öğrenme ve KCD2 sistemleri; BG3 onay sistemi; Elden Ring mesajları; Animal Crossing ve Pokémon G/S gerçek saat; Assassin's Creed Animus; Undertale ve DDLC meta anları; Fallout 4 Codsworth isim seslendirmesi
- Guilty Gear Xrd GDC 2015 sanat yönetimi konuşması; WCAG 2.3.1; The Last of Us Part II'nin 60'tan fazla erişilebilirlik seçeneği
- inZOI Smart Zoi (NVIDIA ACE SLM), PUBG Ally, Mecha BREAK ACE demosu, Whispers from the Star, Suck Up!, Vaudeville, Dead Meat
- Warner Bros. Nemesis System patenti (2021); Kaliforniya SB 243; İtalya Garante'nin Replika cezası; AB AI Act md. 50'nin uygulama tarihi

---

## Doğrulama Notları (24.09.2026)

> Bağımsız doğrulama turu (adversarial fact-check). Karar etkisi yüksek iddialar ve 03 raporuyla iç tutarlılık kontrol edildi. [BT] etiketli tasarım betimlemelerinin (Dead Space, NieR vb.) çoğu bu turda yeniden aranmadı; karar etkileri düşük.

| İddia | Sonuç | Düzeltme/Not | Kaynak |
|---|---|---|---|
| İlk 120 dakika takvimi (§3) 03 raporundaki FTUE hedefleriyle uyumlu | Düzeltildi (iç çelişki) | İlk sürümde ilk dövüş 65–85. dk, ilk yoldaş ve Uyanış olayı 105–120. dk idi. 03'te ilk düşman 1–5. dk, ilk yoldaş 5–15. dk, Uyanış "90. dakikadan önce". Takvim hizalandı: ilk dövüş ≤10. dk, yerli rehber 15–30. dk, Uyanış 80–90. dk | 03 raporu §7 ve Çıkarımlar #2 (iç referans) |
| Günlük görevde kaçırılan günler "en fazla 3 gün" birikir | Düzeltildi (iç çelişki) | 03 raporu 7 gün diyor; 7 güne hizalandı | 03 raporu §8.3 (iç referans) |
| Steam iadesi: 14 gün içinde ve 2 saatten az oynama | Doğrulandı | 23 Nisan 2024'ten beri Early Access ve Advanced Access süresi de 2 saate sayılıyor; ön siparişte 14 gün çıkış gününden başlıyor. İade penceresi 03 ile tutarlı | https://store.steampowered.com/steam_refunds/ · https://gameworldobserver.com/2024/04/24/steam-refund-changed-playtime-counts-in-advanced-access |
| Where Winds Meet: 14 Kas 2025, Steam zirvesi 251.008, LLM NPC'leri manipüle edildi | Doğrulandı | Zirve 23 Kas 2025. "Hamilelik" vakası (PC Gamer, TheGamer) ve yan görevleri atlatan "Solid Snake yöntemi" LLM'in oynanış kurallarını da delebildiğini gösteriyor | https://steamcommunity.com/groups/SteamDB/announcements/detail/604172916311982119 · https://www.pcgamer.com/games/rpg/wuxia-mmo-where-winds-meet-is-full-of-ai-chatbot-npcs-and-people-are-doing-all-the-standard-obscene-stuff-to-them-i-made-him-think-that-my-character-was-pregnant-with-his-child/ · https://www.aol.com/news/where-winds-meet-players-using-115622558.html |
| Steam, Temmuz 2025'ten beri ödeme işlemcisi kurallarını ihlal edebilecek içeriği yasaklıyor | Doğrulandı | ~16 Temmuz 2025'te 15. kural olarak eklendi; özellikle "certain kinds of Adults Only content". Kaldırılan oyunların çoğu ensest/kölelik temalı. PEGI 12/16 romans hedefi etkilenmiyor | https://automaton-media.com/en/news/steam-rules-updated-to-prohibit-content-that-violates-rules-set-forth-by-payment-processors-and-banks/ · https://www.gamingonlinux.com/2025/07/valve-gets-pressured-by-payment-processors-with-a-new-rule-for-game-devs-and-various-adult-games-removed/ |
| AB AI Act md. 50'nin uygulama tarihi 2 Ağustos 2026, erteleme tartışması var [BT] | Düzeltildi | Md. 50 2 Ağustos 2026'dan beri yürürlükte; Digital Omnibus onu ertelemedi (yalnızca yüksek riskli sistemler 2027–28'e kaydı). Md. 50(2) işaretleme için eski sistemlere 2 Aralık 2026'ya kadar geçiş süresi var | https://www.goodwinlaw.com/en/insights/publications/2026/08/alerts-technology-dpc-eu-ai-act-transparency-obligations-now-in-force · https://artificialintelligenceact.eu/transparency-rules-article-50/ |
| Clair Obscur Indie Game Awards ödüllerini kaybetti | Doğrulandı (nüans eklendi) | 20 Ara 2025'te geri alındı. Neden: çıkış sürümünde kalan AI placeholder dokular (5 günde yamalandı) + "gen AI yok" beyanı | https://www.engadget.com/gaming/the-indie-game-awards-snatches-back-two-trophies-from-clair-obscur-over-its-use-of-generative-ai-164730842.html |
| 2025 Steam çıkışlarının ~%20'si gen AI beyan etti | Doğrulandı | Totally Human; tüm kütüphanede 7.818 oyun (%7) | https://www.tomshardware.com/video-games/pc-gaming/1-in-5-steam-games-released-in-2025-use-generative-ai-up-nearly-700-percent-year-on-year-7-818-titles-disclose-genai-asset-usage-7-percent-of-entire-steam-library |
| Godot 4.7, 2026-06-18'de yayımlandı | Doğrulandı | Resmî CHANGELOG: "4.7 - 2026-06-18". 08 raporundaki 2026-06-17 etiket commit tarihi; fark 1 gün | https://raw.githubusercontent.com/godotengine/godot/master/CHANGELOG.md |
| Hades ~21.000 replik, <20 kişilik ekip | Doğrulandı (önceki kaynaklar) | Bu turda yeniden aranmadı; 03 raporunun GDC tabanlı kaynaklarıyla tutarlı | https://www.gamedeveloper.com/audio/dive-into-the-dialogue-of-i-hades-i-at-gdc-2021 |

**Karar etkisi:** FTUE hizalaması bir tasarım kararını değiştiriyor. Dikey dilim ve Next Fest demosu artık ilk 10 dakika içinde dövüş, 30. dakikaya kadar ilk yoldaş ve 90. dakikadan önce Uyanış olayı içermeli. Dil öğrenme segmenti ayrı bir 30 dakikalık blok değil, dövüş ve keşifle iç içe bir katman. AI Act md. 50 artık "tartışmalı tarih" değil, yürürlükte bir yükümlülük; K3 "Sistem'le Konuş" deneyinde AI bildirimi zorunlu.
