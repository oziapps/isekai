# 06 — AI ile 3D Model, Anime Karakter, Rig ve Animasyon Hattı + Motor/DCC MCP Sunucuları

> Araştırma tarihi: 2026-09-24 · Hazırlayan: araştırma alt-ajanı (Claude) · Kapsam: anime 3D karakterler (VRoid/VRM), AI 3D üretimi, otomatik rig, animasyon ve mocap, yüz animasyonu ve lip sync, ücretsiz kütüphaneler, anime dövüş VFX'i ve Claude'un DCC/motor sürmesini sağlayan MCP sunucuları.

**Yöntem notu (önemli):** Bu oturumda WebSearch kotası (200/200) dolmuştu. Konteynerin ağ politikası da GitHub, PyPI ve npm dışındaki alan adlarını engelliyor (vroid.com, meshy.ai, tripo3d.ai, adobe.com, huggingface.co ve diğerleri denendi, erişilemedi). Bu yüzden kaynakların güvenilirliğini üç seviyede işaretledim:
- **[A] Birincil:** Lisans dosyası, README veya kaynak kod GitHub/PyPI'dan doğrudan okundu. Yıldız sayıları GitHub arama API'sinden, son commit tarihleri `git clone --depth 1` ile alındı. Konteyner testlerini de kendim çalıştırdım.
- **[B] Tarihli ikincil:** Başka bir projenin, canlı sayfadan tarih vererek alıntıladığı bilgi. Çoğu 2026-07 ile 2026-09 arası (örneğin TMHSDigital/Free-Game-Dev-Assets kataloğu, calesthio/generative-media-skills).
- **[C] Doğrulanamadı:** Eğitim bilgime dayanıyor ya da tarihsiz ikincil kaynaktan geliyor. Güven düşük.

Yıldız sayıları ve son commit tarihleri 2026-09-24 itibarıyla geçerli.

---

## Özet

1. **Anime kahramanları için en sağlam ve ücretsiz temel VRoid Studio + VRM.** pixiv'in yönergeleri, VRoid ile yapılan modellerin ve preset parçaların oyunlarda ticari kullanımına açıkça izin veriyor. İki şart var: içerik CC0 değil, ve **VRoid mesh'lerinden model üreten bir "karakter yaratıcı" uygulama yapmak ayrı lisans gerektiriyor** [B][1]. Yani oyun içi karakter editörümüzü VRoid mesh'leri üzerine kuramayız.
2. VRM formatı motor bağımsız ve olgun. İçe aktarıcılar Unity'de UniVRM (MIT, 3.388★), Godot'ta godot-vrm (MIT, VRM 1.0 içe/dışa aktarım, MToon, spring bone) ve Unreal'da VRM4U (MIT, UE 5.8 desteği). Blender'da VRM Add-on (Blender 2.93–5.2) var [A][4–7]. VRM 1.0'da hazır ifadeler (happy/angry/sad…), dudak şekilleri (aa/ih/ou/ee/oh) ve blink/look ifadeleri tanımlı. Bu, lip sync'i ucuza getiriyor [A][3].
3. **Üçüncü taraf VRM modellerinde (VRoid Hub, Booth) tuzak var.** VRM meta alanında `allowExcessivelyViolentUsage` varsayılan olarak `false`, `commercialUsage` da varsayılan olarak `personalNonProfit` [A][2]. Dövüş oyununda başkasının modelini bu bayraklar açık değilse kullanamayız.
4. **"Ücretsiz ve sınırsız" bir AI 3D SaaS yok.** Meshy'nin ücretsiz planı 100 kredi/ay veriyor ve çıktılar **CC BY 4.0** lisanslı, atıf zorunlu [B][8][10]. Tripo'nun ücretsiz Basic planı yaklaşık 300 kredi/ay; çıktılar herkese açık ve CC BY 4.0 [B][11]. Rodin'in ücretsiz katmanında dışa aktarım hakkı yok, bu hak Creator planında (30 $/ay) başlıyor [B][10]. Ticari oyun için ya ücretli bir ay ya da açık ağırlıklı model gerekiyor.
5. **Gerçekten ücretsiz ve sınırsız yol, açık ağırlıkları kendi GPU'nda çalıştırmak.** TRELLIS.2 **MIT** lisanslı (4B parametre, PBR, ≥24 GB VRAM) [A][16]. TripoSR (MIT, ~6 GB) ve TripoSG (MIT, ≥8 GB) daha hafif seçenekler [A][17]. Bulut konteynerimizde GPU yok ve huggingface.co engelli, dolayısıyla bu yol ancak kullanıcının kendi PC'sinde (ya da kiralık GPU'da) mümkün.
6. **Hunyuan3D 2.x ve HY-Motion'ın lisansı AB, Birleşik Krallık ve Güney Kore'yi hariç tutuyor.** Kısıtlama yalnızca modeli değil, **çıktıyı da** kapsıyor: "must not use… display… Output… outside the Territory" [A][13][33]. Türkiye bölge içinde. Ancak Steam'de AB'ye satılacak bir oyunda Hunyuan çıktısı kullanmak ciddi hukuki risk. Hunyuan3D 2.5/3.0/3.1 ve PolyGen ise kapalı, yalnızca API üzerinden erişiliyor [B][15].
7. **Otomatik rig artık standart bir hizmet.** Mixamo ücretsiz ve video oyunlarında telifsiz kullanılabiliyor, ama yalnızca iki ayaklı insansılar için [B][24]. Meshy'de rig 5 kredi, animasyon 3 kredi [B][8]. Tripo'da rig 25 kredi, hazır hareket başına retarget 10 kredi [B][11]. Açık kaynak tarafında UniRig ve SkinTokens (MIT, `.vrm` girişini destekliyor) var [A][22].
8. **CC0 animasyon temeli çok güçlü.** Quaternius Universal Animation Library 1 (120+ klip) ve 2 (130+ klip; yakın dövüş kombo, parkur), ayrıca KayKit Character Animations (161 klip) tamamen CC0 [B][27][28]. Prototipin locomotion ve temel dövüş setini 0 $'a karşılıyorlar.
9. **Açık metinden-harekete (text-to-motion) modeller 2026'da ciddi seviyeye geldi, ama lisans ve GPU şartları ağır.** NVIDIA Kimodo'nun kodu Apache-2.0, SOMA ağırlıkları NVIDIA Open Model License altında. 700 saatlik ticari kullanıma uygun mocap ile eğitilmiş ve yaklaşık 17 GB VRAM istiyor (metin kodlayıcı CPU'ya alınırsa 3 GB'ın altına iniyor) [A][34]. Tencent HY-Motion 1.0 (1B, 26 GB) bölge kısıtlı [A][33]. Popüler video→mocap modeli GVHMR **ticari kullanıma kapalı** [A][37].
10. **Yüz animasyonu ve lip sync için ücretsiz yığın tamam.** Seçenekler: VRM ifadeleri, Rhubarb (MIT), uLipSync (MIT, Unity, VRM uyumlu) ve NVIDIA Audio2Face-3D. Audio2Face-3D 2025'te açıldı; SDK MIT, modeller NVIDIA Open Model License altında, UE5 eklentisi de MIT [A][39][40].
11. **MCP olgunluğu (yıldızlar):** Blender MCP (ahujasid, 29.284★), Unity MCP (CoplayDev, 14.461★), Godot MCP (Coding-Solo, 5.811★; hi-godot/godot-ai, 2.581★) ve Unreal MCP (chongdashu, 2.085★; ama son commit 2025-04, yani bakımsız) [A][45–50]. Resmî tarafta Unity 6 `com.unity.ai.assistant` ile yerleşik MCP sunuyor, Epic de UE 5.8'de deneysel bir MCP eklentisi çıkardı [B][49][50].
12. **Bulut konteynerde fiilen doğruladıklarım (2026-09-24):** Godot 4.7.2 `--headless` modunda çalışıyor, GitHub release indirmesi de açık. **PyPI'daki `bpy` 5.2.2 (Blender Python modülü) kuruluyor.** Mesh işleme, glTF/FBX dışa aktarma ve **Cycles CPU render** çalışıyor (256², 16 örnek ≈0,9 sn). EEVEE ve Workbench ise `libEGL` eksik olduğu için çalışmıyor. download.blender.org engelli. Unity ve Unreal editörleri konteynerde çalıştırılamaz, bunlar için MCP ancak kullanıcının kendi PC'sinde kullanılabilir.
13. **Ekosistem derinliği:** Anime toon shader tarafında en zengin ekosistem Unity'de. UniVRM/MToon, lilToon (MIT), Unity Toon Shader (Unity Companion License), Genshin tarzı açık NPR örnekleri ve uLipSync hep orada. Godot'ta MToon ve birkaç cel shader var, Unreal'da ücretsiz anime NPR seçeneği az [A][44]. Bu durum motor kararında bir girdi olmalı.
14. **AI'ın hâlâ zayıf olduğu yerler:** Topoloji (üçgen çorbası), eller ve parmaklar, anime yüz düzlemleri, saç kütleleri, dokuya gömülü ışık, kıyafet skin'i ve anime zamanlaması (hold/smear/impact frame). Önerilen çözüm hibrit bir hat: kahraman karakterlerin gövde ve yüzü VRoid'den, zırh/silah/prop/canavarlar AI'dan, animasyonun iskeleti CC0 veya mocap'ten, anime "hissi" ise el ile cilalanıyor.

---

## 1. Anime 3D Karakter Temeli: VRoid Studio ve VRM Ekosistemi

### 1.1 VRoid Studio lisansı (pixiv)

Aşağıdaki alıntıları TMHSDigital kataloğu 2026-09-23'te canlı `vroid.com/en/studio/guidelines` ve pixiv Kullanım Koşulları sayfalarından almış [B][1]:
- "Any individual or corporation may sell or use for commercial purposes any mesh, texture, or preset item provided by VRoid Studio… provided that no special clauses are indicated in the license." İzin verilen ticari kullanımlar arasında "games, applications, software" sayılıyor.
- "All content provided by pixiv, including the base models… is not CC0." Sıfırdan yaptığımız doku ve saç mesh'leri bizim olur. Temel gövde mesh'i ve preset'ler ise pixiv'in lisansı altında kalır.
- **Kritik kısıt:** "You cannot create an application that can generate or output 3D models, avatars, or items consisting of deformed or combined meshes and textures that were created in VRoid Studio." Oyun içi karakter oluşturucuyu VRoid mesh'lerinden türetemeyiz. Oyuncunun özelleştireceği avatar için kendi base mesh'imiz (ya da CC0 Quaternius Universal Base Characters [B][27]) gerekiyor.
- Atıf zorunlu değil (Madde 13: "for (1) any purpose and (2) any use").

**Kalite tavanı [C]:** VRoid modelleri temiz, deforme olabilen topoloji, hazır humanoid iskelet, spring bone ve 50'yi aşkın yüz blendshape'iyle geliyor. Ancak siluetler birbirine benziyor, yani tanınır bir "VRoid görünümü" var. Profesyonel kaliteye çıkmak için şunlar gerekir: Blender'da (VRM Add-on) özel saç kartları, özel kıyafet ve zırh mesh'leri, el boyaması dokular, yüz için özel normal ya da SDF gölge haritası ve özel shader.

### 1.2 VRM meta lisans alanları: üçüncü taraf modellerde tuzak

VRM 1.0 spesifikasyonuna göre her model meta verisinde kendi lisansını taşıyor [A][2]:

| Alan | Varsayılan | Bizim için anlamı |
|---|---|---|
| `commercialUsage` | `personalNonProfit` | Şirket olarak kullanabilmek için değerin `corporation` olması gerekiyor |
| `allowExcessivelyViolentUsage` | `false` | Dövüş oyunu için `true` olmalı |
| `modification` | `prohibited` | Modeli düzenleyemeyiz |
| `allowRedistribution` | `false` | Oyun dosyasında dağıtmak sorunlu olabilir |
| `creditNotation` | `required` | Krediye yazmak zorunlu |

**Sonuç:** VRoid Hub ve Booth modelleri varsayılan olarak ticari dövüş oyunu için kullanılamaz. Booth'ta yaygın olan VN3 lisansı bile tipik olarak "kurumsal kullanım için hak sahibiyle iletişime geçin" diyor [C][54]. Kural basit: **yalnızca kendi ürettiğimiz ya da CC0 modelleri kullanacağız.**

### 1.3 VRM araç zinciri (doğrulandı)

| Araç | Motor/DCC | Lisans | ★ | Son commit | Not |
|---|---|---|---|---|---|
| UniVRM [4] | Unity | MIT | 3.388 | 2026-09-24 | Referans uygulama, çalışma zamanında yükleme |
| godot-vrm [5] | Godot 4.1+ | MIT | 471 | 2026-07-08 | VRM 0.0/1.0 içe aktarım ve 1.0 dışa aktarım, MToon ✅, springBone ✅ ("needs optimization"), node constraint + retarget "buggy" |
| VRM4U [6] | UE 4.20–5.8 | MIT | 1.983 | 2026-09-24 | MToon benzeri materyal, UE 5.8 resmî desteği |
| VRM Add-on for Blender [7] | Blender 2.93–5.2 | MIT veya GPL-3.0 | 1.709 | 2026-09-23 | Düzenleme ve yeniden dışa aktarım için şart |
| three-vrm | Web | MIT | 2.183 | — | Tanıtım sitesi veya web demosu için |

VRM 1.0 hazır ifadeleri şunlar [A][3]: happy, angry, sad, relaxed, surprised; dudak için aa, ih, ou, ee, oh; göz için blink, blinkLeft, blinkRight, lookUp/Down/Left/Right. Lip sync ve duygu sistemi bu isimlere doğrudan bağlanabilir.

### 1.4 Ticari anime oyunları toon karakteri nasıl yapıyor (Genshin tarzı hat)

Açık kaynak NPR projelerinde belgelenen, Genshin ve Honkai tipi karakter hattının bileşenleri şöyle [A][44]:
- **ILM/Light map (RGBA):** Kanallar gölge eğilimini, specular maskesini ve malzeme ID'sini tutuyor.
- **Ramp dokusu:** Half-Lambert değeri ramp dokusundan örneklenerek 2–3 tonlu, "boyanmış" bir gölge elde ediliyor ("Diffuse Warp", ilk kez Team Fortress 2'de kullanıldı).
- **Yüz için SDF gölge eşik haritası:** Işık açısına göre yüzde her zaman temiz, anime tarzı bir gölge çizgisi veriyor. Yüz normalleri bu yüzden ayrıca düzenleniyor.
- **Diğer katmanlar:** Ters çevrilmiş kabuk (inverted hull) outline'ları, kalınlığı vertex color ile kontrol edilir. Saçta "angel ring" specular, rim light ve bloom.

Motorlara göre kaynaklar şöyle:
- **Unity:** GenshinCelShaderURP (MIT; ancak örnek modeller miHoYo'ya ait ve ticari kullanım yasak), lilToon (MIT, 1.570★), MToon (MIT), UnityURPToonLitShaderExample (MIT, 7.793★) ve Unity Toon Shader (Unity Companion License, yalnızca Unity projelerinde).
- **Godot:** godot-vrm'deki MToon, EXPWorlds/Godot-Cel-Shader (245★), FlexibleToonShaderGD (201★) ve gdquest godot-shaders (kod MIT).
- **Unreal:** Ücretsiz seçenekler zayıf. VRM4U'nun MToon materyali ve motor fork'u gerektiren cel shading projeleri (ashtonland, 105★) var.

**Değerlendirme:** Anime tarzı en az özel geliştirmeyle Unity'de elde edilir. Godot'ta shader'ın önemli kısmını bizim (Claude'un) yazması gerekir. Unreal'da ise post-process ve özel materyal işi ağır olur.

---

## 2. AI ile 3D Üretim Araçları (2026)

### 2.1 Barındırılan (SaaS) servisler

| Araç | Ücretsiz katman | Ticari hak | Rig/animasyon | Topoloji | Kaynak/güven |
|---|---|---|---|---|---|
| **Meshy** (Meshy-6) | 100 kredi/ay; çıktılar **CC BY 4.0** (atıf zorunlu); API yalnızca ücretli (Pro+) | Ücretli planda tam özel sahiplik (Community'de yayınlamazsak) | Rig 5 kr, animasyon 3 kr; kütüphane `action_id`. Rig için dokulu insansı model, A/T poz ve en fazla 300k yüz şartı. Text-to-motion (FBX/BVH, 2–10 sn) | "Smart topology" 100–15.000 üçgen, quad remesh | [B][8][9][10] |
| Meshy API maliyetleri | — | — | — | Image-to-3D dokulu 30 kr (Meshy-6), remesh 5 kr | [B][8] (2026-07-10) |
| **Tripo** (v3.x) | Yeni hesaba 300 kredi (~2 hafta geçerli). Basic ≈300 kr/ay, 1 eşzamanlı iş; ücretsiz çıktılar herkese açık, CC BY 4.0 | Ücretli planlarda özel model ve ticari hak | `check_riggable` ücretsiz, rig 25 kr, retarget 10 kr/hareket. Hazır hareketler: idle, walk, run, jump, climb, slash, shoot, hurt… | Quad +5 kr, smart low-poly +10 kr | [B][11] |
| Tripo API fiyatı | $1 = 100 kredi; image→3D 20–30 kr (v3) | — | — | — | [B][11] |
| Tripo abonelik | Pro ≈15,90 $/ay (~3.000 kr), Advanced ≈39,90 $/ay (~8.000 kr) | — | — | — | [B][11], değişken |
| **Rodin / Hyper3D** (Gen-2) | Ücretsiz: "10 private assets", dışa aktarım hakkı yok | Creator 30 $/ay'dan itibaren dışa aktarım; API Business 120 $/ay | Yerleşik rig yok (T/A poz zorlama var) | Yüksek detay ve PBR | [B][10], [C][21] |
| **Hunyuan3D 2.5 / PolyGen / 3.0 / 3.1** | Kapalı model, Tencent Cloud API (yurtdışı API 26 Kasım 2025'te açıldı) | API şartlarına bağlı | 2.5 skeletal skinning içeriyor | **PolyGen:** sanat kalitesinde quad/tri retopoloji | [B][15] |
| **Luma Genie** | 2026-01-01'de kapatıldı | — | — | — | [C][21] |
| CSM, Kaedim, Sparc3D | **Doğrulanamadı** (siteler erişilemedi) | — | — | — | [C] |

**Blender MCP entegrasyonu:** ahujasid/mcp-for-blender, Hyper3D Rodin ve Hunyuan3D'nin resmî Tencent Cloud API'sini (anakara "AI3D 3.0" ya da uluslararası "Hunyuan-to-3D Professional", PBR) doğrudan çağırabiliyor [A][45]. Tripo'nun resmî MCP'si (tripo-mcp, 206★) hâlâ "alpha". Son commit 2025-04-14'te atılmış, Blender ve Tripo eklentisi şart [A][12]. Meshy ise MCP yerine resmî bir **CLI ve Claude Code skill** paketi yayımladı (meshy-3d-agent, MIT). Bu paket GUI olmadan API üzerinden çalışıyor [A][9].

### 2.2 Açık ağırlıklı modeller (kendi GPU'nda "sınırsız")

| Model | Lisans (kod/ağırlık) | Donanım | Özellik | Son commit |
|---|---|---|---|---|
| **TRELLIS.2-4B** (Microsoft) | **MIT** | ≥24 GB NVIDIA (A100/H100'de doğrulanmış) | Image→3D, tam PBR, 512³ ≈3 sn / 1024³ ≈17 sn / 1536³ ≈60 sn (H100); doku üretimi ve eğitim kodu dahil | 2026-06-05 [A][16] |
| TRELLIS (v1) | MIT | — | CVPR'25 | 2025-11-05 [A][16] |
| **Hunyuan3D-2.1** | Tencent Community License (**AB/UK/KR hariç**, >1M MAU'da ayrı lisans) | Şekil 10 GB, doku 21 GB, ikisi birlikte 29 GB | İlk tamamen açık PBR hattı | 2025-10-17 [A][13] |
| Hunyuan3D-2 / 2mini / 2mv | Aynı aile | 2mini ≈5 GB [B] | Çoklu görüntü girişi (2mv), Blender eklentisi | 2025-10-28 [A][14] |
| **TripoSR** | MIT (kod ve ağırlık) | ≈6 GB | Hızlı ama kalitesi düşük | [A][17] |
| **TripoSG** | MIT | ≥8 GB | Yüksek kaliteli şekil (doku yok) | 2025-04-18 [A][17] |
| **Stable Fast 3D** | Stability Community License (**yıllık gelir <1M $**, ticari kullanımda kayıt şart) | **CPU backend var** | UV unwrap ve ışık ayrıştırma dahili | 2025-01-22 [A][18] |
| SPAR3D | Aynı lisans | 10,5 GB (düşük VRAM modunda 7 GB) | Nokta bulutu düzenleme | 2025-05-05 [A][18] |
| **StdGEN** | Kod Apache-2.0, **ağırlık lisansı doğrulanamadı** | GPU | **Anime karakteri tek görselden** üretiyor; gövde, kıyafet ve saç ayrı parçalar | 2026-04-17 [A][19] |
| CharacterGen / LHM | Apache-2.0 (kod) | GPU | A-poz karakter / animasyona hazır insan | [A][19] |
| Meshy T2 | Açık kaynak "hazırlanıyor" (2026-08) | — | Native mesh üretimi | [A][20] |

**Bulut konteyner gerçeği:** Konteynerde GPU yok ve Hugging Face engelli. SF3D'nin CPU backend'i teknik olarak çalışabilir, ama ağırlıklar HF'de. Kullanıcı ağ erişimini Custom/Full'a çevirirse deneme yapılabilir. Pratikte açık modeller **kullanıcının PC'sinde** (24 GB'lık RTX 3090/4090 idealdir) ya da kiralık GPU'da çalıştırılmalı. Kiralık GPU fiyatları bu oturumda doğrulanamadı.

---

## 3. Otomatik Rig (Rigging)

| Araç | Maliyet | Lisans/koşul | Güçlü yanı | Zayıf yanı |
|---|---|---|---|---|
| **VRoid** | Ücretsiz | Bkz. §1.1 | Humanoid iskelet, spring bone ve ifadeler hazır | Sadece VRoid mesh'i |
| **Mixamo** | Ücretsiz (Adobe ID, CC aboneliği gerekmiyor) | "Royalty free… commercial… Create video games" [B][24]. Ham dosyalar ekip dışına dağıtılamaz ve ML eğitiminde kullanılamaz [B][25] | Büyük klip kütüphanesi | Yalnızca iki ayaklı insansı; 2026'da fiilen güncellenmiyor [C][21] |
| **AccuRIG** (Reallusion) | Ücretsiz | Kalıcı bir EULA URL'si bulunamadı, "needs-review" [B][26] | Mixamo uyumlu kemik isimleri [C] | ActorCore içerikleri ayrı lisanslı |
| **Meshy / Tripo rig** | 5 kr / 25 kr | Planın lisansına bağlı | İnsansı modelde tek tık | İsimlendirme sağlayıcıya özgü (retarget gerekiyor) |
| **UniRig** (VAST) | Ücretsiz | MIT; yayımlanan checkpoint Articulation-XL2.0 ile eğitilmiş | Yaratık dahil her iskelet; `.vrm` girişi var | GPU şart; tam Rig-XL/VRoid checkpoint'i henüz yayımlanmadı [A][22] |
| **SkinTokens** | Ücretsiz | MIT | Skinning doğruluğunda %98–133 iyileşme (iddia) | ≥14 GB GPU [A][22] |
| AniGen | Ücretsiz | Kod MIT, **ama CUBVH bileşeni ticari olmayan kullanım için** | Animasyona hazır üretim | ≥18 GB [A][22] |
| Make-It-Animatable | Ücretsiz | Kod MIT; eğitimde Mixamo verisi kullanılmış (Mixamo'nun ML yasağı nedeniyle gri alan) | Hızlı rig ve poz | [A][23] |

---

## 4. Animasyon Kaynakları

### 4.1 Hazır kütüphaneler ve mocap servisleri

| Kaynak | İçerik | Lisans/limit | Güven |
|---|---|---|---|
| **Quaternius UAL 1** | 120+ insansı klip (locomotion, dövüş/silah, emote, yüzme) | **CC0**, Godot/Unity/Unreal setleri | [B][27] |
| **Quaternius UAL 2** | 130+ klip: **yakın dövüş/silahlı kombolar**, parkur | **CC0** | [B][27] |
| **KayKit Character Animations** | 161 klip (movement, melee, ranged…) | **CC0** | [B][28] |
| Quaternius Universal Base Characters | 6 insansı base mesh (humanoid rig) + 20 saç | **CC0** | [B][27] |
| **Mixamo** | Binlerce klip | Telifsiz ticari kullanım (bkz. §3) | [B][24] |
| **Rokoko Vision (Create)** | Videodan harekete ve metinden harekete | Ücretsiz Starter: **30 sn/ay** Vision işleme, FBX dışa aktarım; "all generated data… can be used commercially" | [B][30] |
| **DeepMotion Animate 3D / SayMotion** | Videodan mocap (8 kişiye kadar, el ve yüz ek ücretli) | **Freemium ticari olmayan kullanım için**, 60 sn/ay. Ücretli planlar (yıllık): Starter 9 $, Innovator 17 $, Professional 39 $, Studio 83 $/ay. 1 kredi = 1 saniye | [B][31] |
| Move.ai | Tek/çoklu kamera mocap | API ve fiyatlar satış ekibi üzerinden; **doğrulanamadı** | [B][32] |
| QuickMagic, Plask | Video mocap | **Doğrulanamadı** | [C] |
| **Cascadeur** | Fizik destekli keyframe, AutoPosing ve ara kare üretimi | Ücretsiz ve "Indie" katmanları var; eşik ve fiyat **doğrulanamadı**. 2026.2 (Ağustos 2026) additive katman ve Python API getirmiş [C] | [C] |

### 4.2 Açık metinden-harekete (text-to-motion) modeller

| Model | Lisans | VRAM | Çıktı/iskelet | Uygunluk |
|---|---|---|---|---|
| **Kimodo** (NVIDIA, 2026-03) | Kod Apache-2.0; SOMA ve G1 ağırlıkları **NVIDIA Open Model License**; SMPL-X varyantı yalnızca Ar-Ge lisansıyla | ≈17 GB; `TEXT_ENCODER_DEVICE=cpu` ile <3 GB | SOMA 77 eklemli iskelet. Metin + keyframe + yol kısıtları, zaman çizelgesi editörü | **En umut verici seçenek.** "Commercially-friendly" 700 saatlik mocap ile eğitilmiş. Model lisansının ticari şartları doğrulanmalı [A][34] |
| ARDY (NVIDIA, SIGGRAPH 2026) | Apache-2.0 | Metin kodlayıcı ≈14 GB | Gerçek zamanlı, etkileşimli hareket üretimi | Araştırma aşamasında, SOMA sürümü "coming soon" [A][35] |
| **HY-Motion 1.0** (Tencent, 2025-12) | Tencent Community License (**AB/UK/KR hariç**, çıktı dahil) | 26 GB (Lite: 24 GB) | SMPL-H → "wood" FBX (fbxsdkpy ile) | Bölge riski ve SMPL-H bağımlılığı var [A][33] |
| MoMask / MotionGPT | Kod MIT | Orta | HumanML3D (AMASS türevi) | Eğitim verisinin lisansı ticari açıdan gri; son commit 2024 [A][36] |
| GVHMR (video→SMPL-X) | **"educational, research and non-profit purposes only"** | — | — | **Ticari kullanım yasak.** Bunu kullanan mixamo-llm-mocap zinciri de aynı şekilde bloke [A][37] |

**Pratik değerlendirme:** Text-to-motion çıktısı 2026'da bloklama ve ara kare için iyi. Ancak anime dövüşündeki abartılı poz, bekleme (hold) ve silah teması gibi gereksinimleri tek başına karşılamıyor. Temizlik için Cascadeur ya da Blender şart.

### 4.3 Anime tarzı animasyon ilkeleri (tasarım rehberi, [C])

- **Limited animation / held frames:** Kritik pozlarda 2s ya da 3s'lerde "stepped" anahtar kareler, hareket sırasında ise tam akıcılık kullanılır. Guilty Gear Xrd ekibinin 2015 GDC sunumu bu hibridin referansıdır.
- **Diğer teknikler:** Güçlü antisipasyon (kurma) ve çok hızlı eylem, smear kareleri (uzatılmış mesh ya da hareket bulanıklığı karesi), **impact frame** (1–3 karelik negatif/yüksek kontrast flaş), hitstop (5–12 karelik donma), kamera sarsıntısı, hız çizgileri, kıyafet ve saç için gecikmeli takip hareketi (spring bone).
- **Dövüş klip seti (silah arketipi başına yaklaşık 40–60 klip):** 8 yönlü yürüme/koşma, 4 yönlü dodge/dash, 4–5 vuruşluk hafif kombo, ağır/şarjlı saldırı, 3–6 özel yetenek, blok/parry, yöne göre hafif ve ağır hit reaction, stagger, knockdown ve kalkış, havada kombo, ölüm, etkileşimler. UAL2 ile KayKit temeli karşılıyor. **İmza hareketler** (boss'lar, ultimate'ler, "Solo Leveling anı") ise mocap veya text-to-motion bloklaması üstüne el cilasıyla yapılmalı.
- **Root motion:** Dodge ve saldırılarda root motion, locomotion'da in-place kullanmak her üç motorda da standart yaklaşım.

### 4.4 Motorlara göre retarget

- **Godot 4:** İçe aktarmada `BoneMap` + `SkeletonProfileHumanoid` ile otomatik eşleme yapılıyor. Animasyon paylaşmak için hem kemik isimleri hem de **Bone Rest**'ler eşleşmeli [A][38]. FBX içe aktarımı ufbx ile yerleşik, `.blend` içe aktarımı Blender kurulu olmasını gerektiriyor [A][38].
- **Unity:** Mecanim Humanoid Avatar ile retarget en olgun seçenek; UniVRM humanoid'i otomatik tanımlıyor [C].
- **Unreal 5:** IK Rig + IK Retargeter (VRM4U retarget varlıklarını üretiyor) [C][6].

---

## 5. Yüz Animasyonu ve Lip Sync

| Araç | Lisans | Motor | Not |
|---|---|---|---|
| VRM ifadeleri | Spesifikasyon | Hepsi | aa/ih/ou/ee/oh + duygular + blink [A][3] |
| **Rhubarb Lip Sync** | MIT | Motor bağımsız CLI | Sesten ağız şekli (A–H) üretiyor; VRM vizemlerine eşlenebilir. Son commit 2025-04 [A][39] |
| **uLipSync** | MIT | Unity | MFCC tabanlı, Job/Burst, VRM uyumlu, 1.671★ [A][39] |
| **NVIDIA Audio2Face-3D** | SDK MIT, UE5 eklentisi MIT (UE 5.5/5.6), modeller NVIDIA Open Model License; Audio2Emotion yalnızca A2F ile birlikte kullanılabilir | UE5, Maya, C++ SDK | Dudak, dil ve duygu. NVIDIA GPU'da hızlanıyor, CPU'ya da düşebiliyor [A][40] |
| OVR LipSync (Meta) | Meta lisansı, **doğrulanamadı** | Unity/UE | — |

Anime yüzü için gerçekçi dil ve yanak simülasyonuna gerek yok. **Beş vizem blendshape'i, göz dokusu veya ifade değişimi ve kaş blendshape'leri** yeterli. En ucuz ve en tutarlı yol, Rhubarb ya da uLipSync'i VRM ifadeleriyle birleştirmek.

---

## 6. Ücretsiz Varlık Kütüphaneleri ve Lisansları

| Kaynak | Lisans | Ne işe yarar | Dikkat |
|---|---|---|---|
| Quaternius | CC0 (paket sayfası başına) | Low-poly kitler, rigli karakterler, UAL | Stil low-poly, toon'a uyarlanmalı [B][29] |
| KayKit | CC0 | Karakter, zindan kiti, animasyon | Tek gradyan atlas; değiştirilmemiş haliyle yeniden satılmamalı [B][28] |
| Kenney | CC0 | Binlerce modüler kit, parçacık dokusu | Lisans hub sayfasında değil, paket sayfasında [B][29] |
| Poly Haven | CC0 | HDRI, PBR doku, model | Blender MCP'den doğrudan aranabiliyor [A][45], [B][29] |
| Sketchfab | **Model başına** (CC BY, CC BY-SA, NC, ND ya da mağaza EULA'sı) | Tek tek model | NC ve ND ticari oyunda kullanılamaz; "editorial" asset'ler ticari değil [B][29] |
| Fab (Epic) | "Fab Standard License" motor bağımsız olabilir; **"Epic Content License" yalnızca Unreal** | Megascans vb. | Rozet her asset için ayrı kontrol edilmeli [B][29] |
| Unity Asset Store / Synty | EULA / ücretli | — | **Doğrulanamadı** [C] |

---

## 7. Anime Dövüş VFX'i

- **Effekseer:** Araç MIT lisanslı. Örnek efektlerin sayfası "distributed under CC-0" diyor [B][41]. Godot 4, Unity ve Unreal eklentileri var (EffekseerForGodot4, 114★) [A][41]. Anime tarzı slash, aura ve patlama efektleri için motordan bağımsız çalışan en iyi ücretsiz yol bu.
- **Godot:** gdquest godot-visual-effects (1.325★), VFX-sketchbook-Godot-4.x (549★), GODOT-VFX-LIBRARY (320★, "designed specifically for action games") ve Juicee (game-feel/hitstop editörü, 144★) [A][42]. Her birinin lisansı ayrıca kontrol edilmeli. Godot Shaders sitesinde gönderiler CC0/MIT/**GPL**; GPL kapalı kaynak oyun için güvensiz [B][29].
- **CC0 dokular:** Kenney Particle Pack (80 doku), Unity Labs VFX flipbook'ları (CC0, motor bağımsız) ve JangaFX ücretsiz EmberGen VDB'leri (CC0) [B][43].
- **Shader tabanlı anime VFX tarifleri [C]:** UV kaydırmalı slash mesh'i + noise erozyon (dissolve), fresnel aura, ekran bozulması, radial blur ve hız çizgileri, impact frame için tam ekran renk ters çevirme. Hepsini Claude'un GDShader, HLSL veya Niagara ile yazması mümkün. 2D flipbook'lar için AI görsel üretimi başka bir raporun konusu.

---

## 8. Claude'un DCC ve Motorları Sürmesi: MCP Sunucuları

### 8.1 Karşılaştırma tablosu

| MCP | ★ | Son commit | Lisans | Yetenek | Bulut konteynerde (GPU yok) çalışır mı? |
|---|---|---|---|---|---|
| **ahujasid/mcp-for-blender** (eski adı blender-mcp) | 29.284 | 2026-09-24 | MIT | Soket tabanlı eklenti, nesne ve materyal işleri, `execute_blender_code`, GLB/FBX dışa aktarım, Poly Haven, Sketchfab, Poly Pizza, **Hyper3D Rodin, Hunyuan3D API**. Telemetri isteğe bağlı (opt-in) | **Hayır (resmî olarak).** Çalışan bir Blender GUI'si ve panelden "Start MCP Server" gerekiyor; download.blender.org da engelli [A][45] |
| **Blender Lab resmî MCP** (projects.blender.org/lab/blender_mcp) | — | — | GPL-3.0 | Blender Foundation Lab projesi | Upstream'e erişilemedi [A][46] |
| bpy-dev/blender-mcp (Blender Lab fork'u) | 94 | 2026-09 | GPL-3.0 | `_for_cli` araçları, **standalone `bpy` backend ile headless** çalışma | **Evet, muhtemelen** (bpy 5.2.x ile). Geliştirici önizlemesi [A][46] |
| tripo-mcp | 206 | 2025-04-14 | MIT | Tripo'dan Blender'a aktarım (alpha) | Hayır [A][12] |
| **Coding-Solo/godot-mcp** | 5.811 | 2026-04-16 | MIT | Editörü ya da projeyi başlatma, hata ayıklama çıktısı, headless GDScript ile sahne ve düğüm işleri, UID yönetimi | **Evet.** Godot CLI kullanıyor; Godot 4.7.2 headless konteynerde çalıştı [A][48] |
| tugcantopaloglu/godot-mcp (fork) | 466 | 2026-07-13 | MIT | 157 araç, headless sahne işlemleri, `validate_script`, `export_project`; Godot 4.4+ (4.7'de test edilmiş) | **Evet** (headless kısımlar) [A][48] |
| **hi-godot/godot-ai** | 2.581 | 2026-09-23 | MIT | 46 araç / 120+ işlem, canlı editör eklentisi (Coplay ekibinden) | Kısmen. Canlı editör gerekiyor; `--headless` editörle çalışıp çalışmadığı **doğrulanamadı** [A][48] |
| youichi-uda/godot-mcp-pro | 606 | 2026-09-24 | Repo MIT; ürün "$15 one-time" | 162 araç (animasyon, shader, parçacık, girdi simülasyonu) | Editör gerekiyor [A][48] |
| **CoplayDev/unity-mcp** | 14.461 | 2026-09-20 | MIT | v10.0.0 (2026-06-30), Unity 2021.3–6.x, asset/sahne/script/test, VFX ve animasyon araç grupları, Roslyn doğrulama | **Hayır.** Unity Editor ve lisans aktivasyonu gerekiyor [A][49] |
| IvanMurzak/Unity-MCP | 4.332 | 2026-09-23 | Apache-2.0 | Tek satırla C# metotlarını araca çevirme, CLI | Hayır [A][49] |
| CoderGamester/mcp-unity | 1.910 | 2026-09-03 | MIT | Yaklaşık 30 araç + kaynaklar | Hayır [A][49] |
| **Unity resmî** (`com.unity.ai.assistant`) | — | — | Unity (relay kapalı kaynak) | Unity 6+, "Project Settings → AI → Unity MCP", her yeni istemci için bekleyen bağlantı onayı | Hayır [B][49] |
| chongdashu/unreal-mcp | 2.085 | **2025-04-22 (bakımsız)** | Lisans dosyası yok | Blueprint, aktör ve editör işleri | Hayır [A][50] |
| ChiR24/Unreal_mcp | 885 | 2026-09-23 | MIT | C++ Automation Bridge | Hayır [A][50] |
| tumourlove/monolith | 314 | 2026-09-10 | MIT | UE 5.7/5.8, 1.400+ eylem: Blueprint, Material, **Niagara, Animation, GAS, ComboGraph** | Hayır [A][50] |
| **Epic resmî** (UE 5.8 `ModelContextProtocol`) | — | — | Epic EULA | Deneysel. Eklenti kendi başına hiç araç sunmuyor; ToolsetRegistry ve AllToolsets eklentileri gerekiyor | Hayır [B][50] |

### 8.2 Konteyner testleri (2026-09-24, kendi ölçümüm)

- `Godot_v4.7.2-stable_linux.x86_64 --headless --version` komutu `4.7.2.stable.official` döndürdü. github.com release indirmesi ağ politikasında açık.
- `uv venv --python 3.13` ve `uv pip install bpy==5.2.2` başarılı oldu (manylinux wheel 402 MB) [A][47]. Primitive oluşturma, Decimate modifier ve glTF + FBX dışa aktarma yarım saniyede tamamlandı. **Cycles CPU** ile 256×256, 16 örnek render ≈0,9 sn sürdü. EEVEE ve Workbench `libEGL.so.1` eksik olduğu için başarısız oldu.
- **Anlamı:** Claude bulutta GUI'siz bir "asset fabrikası" kurabilir. Toplu glTF/FBX/VRM dönüştürme, kemik adlandırma ve eşleme, decimate/LOD üretimi, doku atlası paketleme, Cycles ile küçük önizleme render'ı ve Godot headless içe aktarma/doğrulama yapılabilir. Etkileşimli modelleme, weight paint ve motor içi görsel ayar ise kullanıcının PC'sinde Blender MCP ve motor MCP'siyle yapılmalı.

---

## 9. Önerilen Uçtan Uca Karakter ve Animasyon Hattı

### 9.1 Adımlar

1. **Stil bibliyası (2D):** Karakter turnaround sayfaları (ön, yan ve arka, A-poz), renk paleti ve siluet kuralları hazırlanır. Görseller AI ile üretilir (görsel araçları başka raporda). Bu sayfalar aynı zamanda image→3D modellerine girdi olur.
2. **Kahramanlar ve önemli NPC'ler (insansı):** VRoid Studio'da temel gövde ve yüz hazırlanır. Ardından Blender'da (VRM Add-on + Blender MCP) özel saç kartları eklenir. Zırh ve aksesuarlar AI ile üretilir (Meshy veya Tripo'da ücretli bir ay, ya da yerelde TRELLIS.2), remesh edilir, gövdeye weight transfer yapılır. Son olarak özel dokular boyanır ve **VRM 1.0 olarak dışa aktarılır**. Motora godot-vrm, UniVRM veya VRM4U ile alınır. Spring bone ve ifadeler hazır gelir.
3. **Oyuncu avatarı ve karakter editörü:** VRoid mesh'i kullanılmaz (lisans kısıtı, §1.1). Quaternius Universal Base Characters (CC0) ya da kendi base mesh'imiz üzerine morph ve parça değiştirme sistemi kurulur.
4. **Canavarlar ve boss'lar:** Konsept görselden image→3D (Tripo/Meshy/Rodin ücretli ya da yerel TRELLIS.2/TripoSG) üretilir. Ardından retopoloji yapılır (Meshy remesh, Instant Meshes ya da QuadriFlow; ikisi de BSD-3 [B][53]). İnsansı olanlar Tripo/Meshy/AccuRIG ile, yaratıklar UniRig ya da elle rig'lenir. Boss imza hareketleri elle keyframe edilir.
5. **Prop, silah ve çevre:** AI 3D + CC0 kitler (Quaternius/KayKit/Kenney/Poly Haven) kullanılır. Hepsi ortak toon materyaline ve palet LUT'una bağlanarak stil birliği sağlanır.
6. **Animasyon:** Temel set UAL1 + UAL2 + KayKit (CC0) ve Mixamo'dan gelir. İmza hareketler için kullanıcı kendini telefonla çeker, video Rokoko Vision'a (ücretsiz 30 sn/ay) ya da ücretli bir aylığına DeepMotion'a verilir. Alternatif olarak GPU varsa Kimodo ile metin ve keyframe kısıtlı bloklama yapılır. Sonra Cascadeur veya Blender'da **anime zamanlaması** eklenir (hold, smear, impact) ve motorda retarget edilir.
7. **Yüz:** VRM ifadeleri + Rhubarb (Godot/Unreal) ya da uLipSync (Unity) kullanılır. Ara sahnelerde Audio2Face (UE) değerlendirilebilir.
8. **VFX:** Effekseer + shader VFX + CC0 flipbook'lar. Hitstop, kamera sarsıntısı ve impact frame kod tarafında yapılır.
9. **Otomasyon:** Bulutta bpy ve Godot headless ile pipeline script'leri (CI) çalışır. Yerelde Blender MCP ve motor MCP'si kullanılır. Her asset için bir **köken kaydı** tutulur: kaynak, lisans, tarih, ücretli plan ve prompt.

### 9.2 Motorlara göre fark

| Konu | Godot 4.7 | Unity 6 | Unreal 5.8 |
|---|---|---|---|
| VRM | godot-vrm (springBone optimizasyon istiyor) | UniVRM (referans) | VRM4U |
| Anime toon shader | MToon + özel GDShader (iş yükü orta/yüksek) | En zengin: lilToon, MToon, UTS, NPR örnekleri | Özel materyal ve post-process (yüksek iş yükü) |
| Retarget | BoneMap + SkeletonProfileHumanoid | Humanoid Avatar (en kolay) | IK Retargeter |
| Lip sync | Rhubarb ile özel entegrasyon | uLipSync | Audio2Face eklentisi |
| VFX | GPUParticles + Effekseer | VFX Graph + Effekseer | Niagara + Effekseer |
| MCP olgunluğu | İyi (5,8k★ + godot-ai) | **En iyi** (14,5k★ + resmî) | Orta (resmî MCP deneysel) |
| Claude'un bulutta sürebilmesi | **Evet (headless)** | Hayır | Hayır |

### 9.3 Maliyet ve beklenen kalite

| Senaryo | Aylık maliyet | Beklenen kalite |
|---|---|---|
| **Sıfır bütçe:** VRoid, Blender, CC0 kitler, Mixamo, Rokoko ücretsiz, Rhubarb, Effekseer | 0 $ | Kahramanlar "iyi indie anime" seviyesinde; animasyonlar "genel"; imza hareketler kısıtlı |
| **Önerilen üretim ayları:** + Meshy Pro veya Tripo Pro + DeepMotion/Rokoko alt ücretli plan + Cascadeur Indie | ≈16 $ (Tripo Pro [B]) + 9–39 $ (DeepMotion [B]) + Cascadeur (doğrulanamadı). Toplam yaklaşık **30–80 $/ay** | Prop ve canavarlarda hızlı üretim, imza hareketlerde mocap, ticari haklar net |
| **Yerel GPU (24 GB):** TRELLIS.2, Hunyuan 2.1 (AB riski), Kimodo, UniRig | Donanım yatırımı; ek abonelik yok | Sınırsız deneme; kalite SaaS'a yakın ama retopo yükü artıyor |

---

## 10. AI Araçlarının Hâlâ Zayıf Olduğu Yerler ve Çözümler

| Sorun | Neden | Çözüm |
|---|---|---|
| Topoloji (üçgen çorbası, yüksek poligon, manifold olmayan yüzeyler) | Voxel ya da SDF'den mesh çıkarımı | Meshy smart topology/remesh, Hunyuan PolyGen (API), Instant Meshes/QuadriFlow; kahramanlarda elle retopo |
| Eller ve parmaklar | Parmaklar kaynaşık çıkıyor, rig bozuluyor | Eli VRoid ya da base mesh'ten al; parmak kemiklerini kontrol et; eldiven tasarımıyla gizle |
| Anime yüzü | Yumrulu düzlemler, blendshape yok | Yüzü **her zaman** VRoid ya da base mesh'ten al; SDF yüz gölgesi ve özel normaller kullan |
| Saç | Tek parça kütle, spring bone yok | VRoid veya Blender'da saç kartları + VRM springBone |
| Dokuya gömülü ışık | Görselden geldiği için gölgeler "pişmiş" | Retexture'da düz albedo iste; toon ramp'la ez; el boyamasıyla düzelt |
| Arka yüz uydurması | Tek görsel girdisi | Çoklu görüntü girişi (Hunyuan 2mv, Tripo multiview, Meshy multi-image) + turnaround sayfası |
| Skinning ve kıyafet kırpılması | Otomatik ağırlıklar | Weight paint düzeltmesi, VRoid gövdesine weight transfer, kıyafet altındaki gövdeyi silme |
| AI hareket kalitesi | Ayak kayması, titreme, "genel" hareket; anime abartısı ve silah teması yok | Yalnızca bloklama için kullan; Cascadeur/Blender'da cilala; foot-lock; stepped key |
| Stil tutarlılığı | Her asset farklı modelden geliyor | Stil bibliyası, sabit prompt şablonları, ortak toon shader ve palet LUT'u |
| Lisans karmaşası | CC BY ücretsiz planlar, bölge kısıtları, NC veri setleri | Ticari asset'leri yalnızca ücretli planda üret; köken kaydı tut; Hunyuan, GVHMR ve NC veri setlerinden kaçın |

---

## Oyunumuz İçin Çıkarımlar

1. **Karakter stratejisi: "VRoid gövde/yüz + AI aksesuar + el cilası."** 3–6 ana kahraman ve önemli NPC'ler VRoid tabanlı yapılmalı, sonra Blender'da özelleştirilip VRM 1.0 olarak motora alınmalı. Oyuncunun özelleştirdiği avatar ise **CC0 base mesh** üzerine kurulmalı (VRoid'in "karakter yaratıcı" yasağı).
2. **Üçüncü taraf VRM ve Booth modelleri kullanılmamalı.** Varsayılan meta bayrakları şiddet ve kurumsal kullanıma kapalı.
3. **Hunyuan3D ve HY-Motion çıktıları ticari yapıya hiç girmemeli.** Oyun Steam'de AB, İngiltere ve Kore'ye de satılacak, lisans ise çıktının bu bölgelerde "display" edilmesini yasaklıyor. Güvenli açık alternatifler: TRELLIS.2 (MIT), TripoSG/TripoSR (MIT) ve Kimodo (Apache-2.0 kod + NVIDIA Open Model).
4. **AI 3D SaaS'ı "üretim sprint'i" modeliyle kullanalım.** Asset listesi önceden hazırlanır, ardından bir ya da iki ay Tripo Pro (≈16 $) veya Meshy Pro alınıp toplu üretim yapılır. Ücretsiz plan çıktıları (CC BY, herkese açık) yalnızca prototipte kullanılmalı.
5. **Animasyon temeli bugünden hazır ve 0 $.** Prototipte UAL1 + UAL2 + KayKit (CC0) ile locomotion ve dövüş seti kurulmalı. İmza hareketler (ultimate, boss, "gölge ordusu çağırma" tarzı anlar) mocap ve el cilasıyla yapılmalı.
6. **Anime hissi animasyon zamanlamasında ve shader'da yakalanır, poligon sayısında değil.** Bütçe ve zaman öncelikle toon shader (ramp + SDF yüz + outline), hitstop/impact frame ve VFX'e ayrılmalı.
7. **Claude'un iş bölümü:** Bulutta bpy ve Godot headless ile bir "asset fabrikası" kurulmalı (dönüştürme, doğrulama, LOD, önizleme, köken kaydı). Kullanıcının PC'sinde Blender MCP (ahujasid) ve seçilen motorun MCP'si kurulmalı: Unity için CoplayDev, Godot için Coding-Solo veya godot-ai, Unreal için monolith veya ChiR24.
8. **Motor kararı için sanat hattı puanı.** Anime toon kalitesi ve MCP olgunluğu açısından Unity önde. Claude'un bulutta tek başına çalışabilmesi açısından Godot önde. Unreal en ağır seçenek. Nihai kararda bu tablo diğer raporlardaki telif ve gelir analiziyle birlikte tartılmalı.
9. **Kullanıcının donanımı öğrenilmeli.** 24 GB VRAM'li bir GPU varsa TRELLIS.2, UniRig ve Kimodo "sınırsız ve ücretsiz" hale gelir. Yoksa SaaS sprint'i ya da kiralık GPU gerekir.
10. **Köken ve lisans kaydı (asset registry) ilk günden tutulmalı.** Steam'in AI açıklama formu ve olası hukuki denetim için bu şart.

## Belirsizlikler ve Riskler

- **SaaS fiyatları ikincil kaynaklardan (2026-07 / 2026-09).** Meshy, Tripo, Rodin ve DeepMotion rakamları başka projelerin canlı sayfa alıntıları; doğrudan doğrulanmadı. Tripo'nun ücretsiz kredisi için kaynaklar çelişiyor (300 ile ~600/ay). Satın almadan önce resmî sayfalar kontrol edilmeli.
- **Doğrulanamayanlar:** Cascadeur fiyatı ve lisans eşikleri; Move.ai, QuickMagic, Plask, CSM, Kaedim ve Sparc3D. Mixamo'nun uzun vadede ayakta kalıp kalmayacağı da belirsiz (güncellenmiyor).
- **Doğrudan okunamayan lisanslar:** NVIDIA Open Model License'ın tam ticari şartları, StdGEN ağırlık lisansı, AccuRIG EULA'sı ve Unity resmî MCP koşulları okunamadı (nvidia.com, huggingface.co ve reallusion.com erişilemedi).
- **HY-Motion çıktısı SMPL-H iskeletine dayanıyor.** SMPL ailesi modelleri ticari olmayan kullanım lisanslı. Yalnızca hareket verisinin bundan etkilenip etkilenmediği hukuken belirsiz.
- **Make-It-Animatable ve benzerleri Mixamo verisiyle eğitilmiş.** Mixamo'nun "ML eğitiminde kullanılamaz" şartıyla çelişebilir, bu da çıktıları gri alana sokar.
- **VRoid:** Bazı preset öğelerin "special clause" taşıması mümkün, her öğe ayrıca kontrol edilmeli. VRoid görünümünün pazarda "ucuz" algılanma riski de var; özelleştirme bütçesi ayrılmalı.
- **MCP ekosistemi çok hızlı değişiyor** (chongdashu/unreal-mcp gibi projeler bir yılda bakımsız kalabiliyor). `execute_code` araçları keyfi kod çalıştırıyor; kaydetme ve sürüm kontrolü disiplini şart.
- **Bulut hattı kırılgan:** bpy wheel'i Python 3.13'e sabit. Blender Lab resmî MCP'sine (projects.blender.org) erişilemedi.
- **AI asset'lerinin telif koruması ve Steam açıklama yükümlülüğü** başka bir raporun konusu, ama bu hattı doğrudan etkiliyor.

## Kaynaklar

1. TMHSDigital/Free-Game-Dev-Assets — VRoid Studio girdisi (vroid.com/en/studio/guidelines alıntıları, doğrulama tarihi 2026-09-23): https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/characters/vroid-studio.md
2. VRM 1.0 meta spesifikasyonu: https://github.com/vrm-c/vrm-specification/blob/master/specification/VRMC_vrm-1.0/meta.md
3. VRM 1.0 expressions spesifikasyonu: https://github.com/vrm-c/vrm-specification/blob/master/specification/VRMC_vrm-1.0/expressions.md
4. UniVRM: https://github.com/vrm-c/UniVRM
5. godot-vrm: https://github.com/V-Sekai/godot-vrm
6. VRM4U: https://github.com/ruyo/VRM4U
7. VRM Add-on for Blender: https://github.com/saturday06/VRM-Addon-for-Blender
8. Meshy sağlayıcı skill'i (docs.meshy.ai alıntıları, 2026-07-10): https://github.com/calesthio/generative-media-skills/blob/main/skills/providers/3d-generation/meshy-3d/SKILL.md
9. Meshy resmî agent skill ve CLI: https://github.com/meshy-dev/meshy-3d-agent ; https://github.com/meshy-dev/meshy-3d-agent/blob/main/skills/meshy-3d-generation/references/pipelines.md
10. SerSan recon (hyper3d.ai/pricing ve meshy.ai/pricing alıntıları, 2026-08-27): https://github.com/SerSan-AI-Studio/Sersan/blob/main/docs/recon-2026-08-27/research/web-3d-from-photo.md
11. Tripo sağlayıcı skill'i (2026-07-10): https://github.com/calesthio/generative-media-skills/blob/main/skills/providers/3d-generation/tripo-3d/SKILL.md
12. tripo-mcp: https://github.com/VAST-AI-Research/tripo-mcp
13. Hunyuan3D-2.1 LICENSE ve README: https://github.com/Tencent-Hunyuan/Hunyuan3D-2.1 ; https://raw.githubusercontent.com/Tencent-Hunyuan/Hunyuan3D-2.1/main/LICENSE
14. Hunyuan3D-2: https://github.com/Tencent-Hunyuan/Hunyuan3D-2
15. Hunyuan3D sağlayıcı skill'i (sürüm ve erişim, 2026-07-10): https://github.com/calesthio/generative-media-skills/blob/main/skills/providers/3d-generation/tencent-hunyuan3d/SKILL.md
16. TRELLIS.2 ve TRELLIS: https://github.com/microsoft/TRELLIS.2 ; https://github.com/microsoft/TRELLIS
17. TripoSR ve TripoSG: https://github.com/VAST-AI-Research/TripoSR ; https://github.com/VAST-AI-Research/TripoSG
18. Stable Fast 3D ve SPAR3D (Stability Community License): https://github.com/Stability-AI/stable-fast-3d ; https://github.com/Stability-AI/stable-point-aware-3d
19. StdGEN, CharacterGen, LHM: https://github.com/hyz317/StdGEN ; https://github.com/zjp-shadow/CharacterGen ; https://github.com/aigc3d/LHM
20. Meshy T2: https://github.com/meshy-dev/meshy-t2
21. ClawVille "AI 3D Asset Generation — State of the Art (May 2026)" (ikincil): https://github.com/ItachiDevv/ClawVille/blob/main/docs/visual-creation-research/03-3d-asset-generation.md
22. UniRig, SkinTokens, AniGen: https://github.com/VAST-AI-Research/UniRig ; https://github.com/VAST-AI-Research/SkinTokens ; https://github.com/VAST-AI-Research/AniGen
23. Make-It-Animatable: https://github.com/jasongzy/Make-It-Animatable
24. Mixamo girdisi (Adobe FAQ alıntısı, 2026-07-19): https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/animation/mixamo.md
25. TalkingHead README (Mixamo ham dosya ve ML kısıtı): https://github.com/met4citizen/TalkingHead
26. AccuRIG girdisi: https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/tools/accurig.md
27. Quaternius UAL 1/2 ve Base Characters girdileri: https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/animation/quaternius-universal-animation-library.md ; .../quaternius-universal-animation-library-2.md ; .../catalog/characters/quaternius-universal-base-characters.md ; UAL ayna deposu: https://github.com/J-Ponzo/gltf-universal-animation-library
28. KayKit girdileri: https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/3d/kaykit.md ; .../catalog/animation/kaykit-character-animations.md
29. Kenney, Quaternius, Poly Haven, Sketchfab, Fab, Godot Shaders girdileri ve high-risk.md: https://github.com/TMHSDigital/Free-Game-Dev-Assets/tree/main/catalog ; https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/docs/high-risk.md
30. Rokoko Vision girdisi (2026-08-24): https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/animation/rokoko-vision.md
31. DeepMotion Animate 3D skill'i (2026-07-11): https://github.com/calesthio/generative-media-skills/blob/main/skills/providers/motion-capture/deepmotion-animate-3d/SKILL.md
32. Move AI skill'i: https://github.com/calesthio/generative-media-skills/blob/main/skills/providers/motion-capture/move-ai-motion-capture/SKILL.md
33. HY-Motion 1.0 (README, License.txt, smplh2woodfbx.py): https://github.com/Tencent-Hunyuan/HY-Motion-1.0
34. Kimodo: https://github.com/nv-tlabs/kimodo
35. ARDY: https://github.com/nv-tlabs/ardy
36. MoMask ve MotionGPT: https://github.com/EricGuo5513/momask-codes ; https://github.com/OpenMotionLab/MotionGPT
37. GVHMR LICENSE ve mixamo-llm-mocap: https://github.com/zju3dv/GVHMR ; https://github.com/squall01337/mixamo-llm-mocap
38. Godot dokümanları — skeleton retargeting ve FBX (ufbx): https://github.com/godotengine/godot-docs/blob/master/tutorials/assets_pipeline/retargeting_3d_skeletons.rst ; https://github.com/godotengine/godot-docs/blob/master/tutorials/assets_pipeline/importing_3d_scenes/available_formats.rst
39. Rhubarb Lip Sync ve uLipSync: https://github.com/DanielSWolf/rhubarb-lip-sync ; https://github.com/hecomi/uLipSync
40. NVIDIA Audio2Face-3D: https://github.com/NVIDIA/Audio2Face-3D
41. Effekseer, EffekseerForGodot4 ve örnek efekt lisansı: https://github.com/effekseer/Effekseer ; https://github.com/effekseer/EffekseerForGodot4 ; https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/shaders-vfx/effekseer-samples.md
42. Godot VFX depoları: https://github.com/gdquest-demos/godot-visual-effects ; https://github.com/gtibo/VFX-sketchbook-Godot-4.x ; https://github.com/haowg/GODOT-VFX-LIBRARY ; https://github.com/Kelpekk/Juicee
43. CC0 VFX dokuları: https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/catalog/shaders-vfx/kenney-particle-pack.md ; .../unity-labs-vfx-flipbooks.md ; .../jangafx-free-vdb.md
44. Toon/NPR shader depoları: https://github.com/Gaolingx/GenshinCelShaderURP ; https://github.com/Unity-Technologies/com.unity.toonshader ; https://github.com/lilxyzw/lilToon ; https://github.com/Santarh/MToon ; https://github.com/ColinLeung-NiloCat/UnityURPToonLitShaderExample ; https://github.com/EXPWorlds/Godot-Cel-Shader ; https://github.com/CaptainProton42/FlexibleToonShaderGD ; https://github.com/gdquest-demos/godot-shaders ; https://github.com/ashtonland/Unreal-Engine-Cel-Shading
45. MCP for Blender (eski adı blender-mcp): https://github.com/ahujasid/mcp-for-blender
46. Blender Lab MCP'nin fork'u ve NOTICE (upstream: projects.blender.org/lab/blender_mcp): https://github.com/bpy-dev/blender-mcp
47. bpy (PyPI): https://pypi.org/project/bpy/
48. Godot MCP'ler: https://github.com/Coding-Solo/godot-mcp ; https://github.com/tugcantopaloglu/godot-mcp ; https://github.com/hi-godot/godot-ai ; https://github.com/youichi-uda/godot-mcp-pro ; https://github.com/ee0pdt/Godot-MCP
49. Unity MCP'ler ve resmî MCP notları: https://github.com/CoplayDev/unity-mcp ; https://github.com/IvanMurzak/Unity-MCP ; https://github.com/CoderGamester/mcp-unity ; https://github.com/AlexeyPerov/Unity-Open-MCP/blob/main/docs/mcp-tools-comparison.md ; https://github.com/OmerZeyveli/kinglet-unity/blob/main/MCP-SETUP.md
50. Unreal MCP'ler ve Epic resmî MCP notları: https://github.com/chongdashu/unreal-mcp ; https://github.com/ChiR24/Unreal_mcp ; https://github.com/tumourlove/monolith ; https://github.com/flopperam/unreal-engine-mcp ; https://github.com/interaeronav/TokenEfficiencyEngine/blob/main/docs/research/07-epic-official-unreal-mcp.md ; https://github.com/JosephOIbrahim/UnrealEngine_Bridge/blob/main/docs/EPIC_MCP_MATRIX.md
51. Godot 4.7.2 sürümü: https://github.com/godotengine/godot/releases/tag/4.7.2-stable
52. AI asset politikası notları: https://github.com/TMHSDigital/Free-Game-Dev-Assets/blob/main/docs/ai-assets.md
53. Instant Meshes ve QuadriFlow: https://github.com/wjakob/instant-meshes ; https://github.com/hjwdzh/QuadriFlow
54. VN3 lisans örneği (Booth): https://github.com/Auzlex/vn3-license-solarialabs
