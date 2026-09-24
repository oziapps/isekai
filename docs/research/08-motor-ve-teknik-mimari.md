# 08 — Motor Seçimi ve Teknik Mimari (Godot vs Unity vs Unreal, AI-ajan odaklı)

> Araştırma tarihi: 2026-09-24 · Hazırlayan: araştırma alt-ajanı (Claude) · Kapsam: anime tarzı 3D isekai aksiyon-RPG'si için motor karşılaştırması, AI kodlama ajanı (Claude Code) uyumluluğu, bulut konteynerde headless çalıştırma, CI/test, önerilen proje mimarisi, kod kuralları, performans bütçesi.

**Yöntem notu (önemli):** Bu oturumda WebSearch kotası (200/200) dolmuştu. godotengine.org, unity.com, docs.unity3d.com, dev.epicgames.com, w4games.com gibi alan adları egress proxy tarafından engellendi (kendim denedim: `EGRESS_BLOCKED` / HTTP 000). Bu yüzden:
- **[A] Birincil / kendim doğruladım:** Resmî kaynak GitHub'da okundu (godot, godot-website, godot-docs, Unity-Technologies/TermsOfService, UnityCsReference etiketleri, lisans dosyaları), yıldız sayıları GitHub arama API'sinden alındı ya da testi **bu konteynerde kendim çalıştırdım** (Godot 4.7.2 headless, Xvfb + yazılım Vulkan ile render, .NET derlemesi).
- **[B] Tarihli ikincil:** Başka bir projenin tarih vererek canlı sayfadan aktardığı bilgi (örneğin 2026-09-05'te unity.com/pricing'den doğrulandığını söyleyen bir referans dosyası, 2026-09-24 tarihli bir Unreal inceleme belgesi).
- **[C] Doğrulanamadı:** Eğitim bilgime ya da tarihsiz kaynağa dayanıyor. Güven düşük.

---

## Özet

1. **Öneri: Godot 4.7.x (şu an 4.7.2'ye sabitlenmiş), dil olarak katı tipli GDScript.** Karar büyük ölçüde "Claude Code ana geliştirici" gerçeğine dayanıyor. Üç motor içinde yalnızca Godot'u bulut konteynerimizde (4 vCPU, 16 GB RAM, GPU yok) **kurabildim, içe aktarma yapabildim, test koşturabildim ve ekran görüntüsü alabildim**. Hepsini GUI'siz yaptım [A].
2. **Güncel sürümler [A]:** Godot 4.5 (2025-09-15), 4.6 (2026-01-25), 4.7 (2026-06-17), **4.7.2 (2026-08-16)**. `master` dalı 4.8-dev. Unity 6.3 (6000.3, 2025-12-03, **LTS**), 6.4 (2026-03-18), 6.5 (2026-06-15), **6.6 (6000.6.2f1, 2026-09-18)**; 6.7 beta. Unreal: 5.7 (2025-11-12), **5.8.0 (2026-06-17), 5.8.3 (2026-09-22)**. 5.8 son UE5 sürümü olarak planlanıyor [B].
3. **Konteyner testlerim [A]:** Godot Linux editörü 77,9 MB zip (açılmış ikili 146 MB). `--headless --import` küçük projede 9,1 sn, headless test koşusu 0,27 sn sürdü ve exit code doğru döndü. **Xvfb + Mesa llvmpipe (yazılım Vulkan) ile Forward+ render alınabildi** (stencil outline'lı toon küre, ≈9,8 sn). `apt` üzerinden `dotnet-sdk-8.0` kuruldu, Godot .NET sürümüyle C# derlenip headless koşturuldu. `--doctool` ile sürüme tam uyan 1.036 sınıflık API XML'i 1,2 sn'de döküldü.
4. **Unity ve Unreal bulutta pratik değil:** `download.unity3d.com` ve `dev.epicgames.com` engelli [A]. Unity CI için lisans aktivasyonu (`.ulf` + e-posta/şifre secret'ları) gerekiyor [A]. Unreal'ın prebuilt Linux paketi ~25 GB zip / ~43 GB açılmış, kaynaktan derleme ~225 GB [B]. Konteynerde ~29 GB boş disk var [A].
5. **Metin tabanlı formatlar:** Godot'un `.tscn`/`.tres`/`.gd` dosyaları "mostly human-readable" ve VCS dostu [A]. Unity sahneleri YAML ama fileID/GUID referanslarına ve `.meta` dosyalarına bağlı [A örnek dosya / C yorum]. Unreal'da `.uasset`, `.umap`, Blueprint, AnimBP ve materyal grafikleri **ikili**. Blueprint düğümleri Python'dan kurulamıyor [B].
6. **Anime/toon ekosistemi en zengin Unity'de:** UTS3 (Unity Companion License, yalnızca Unity), lilToon (MIT), UnityURPToonLitShaderExample (7.793★), GenshinCelShaderURP (768★), UniVRM (3.388★) [A]. Godot'ta yerleşik **Toon diffuse/specular modları** ve **4.5'ten beri stencil tabanlı Outline modu** var (render ile doğruladım), ama topluluk shader'ları küçük (en büyüğü 245★). SDF yüz gölgesi gibi "Genshin" teknikleri bizim yazmamız gereken işler [A].
7. **Godot'un 2025–26'da kapattığı boşluklar [A]:** Jolt varsayılan fizik (4.6), yeni IK çatısı (TwoBoneIK3D/FABRIK3D/CCDIK3D… 4.6), SpringBoneSimulator3D (saç ve etek), stencil buffer (4.5), shader baker (TPS demosunda D3D12/Metal'de 20× daha hızlı açılış, 4.5), benzersiz Node ID'leri (4.6), delta-encoded patch PCK (4.6), HDR çıktı + AreaLight3D + `Tween.tween_await` (4.7), Tracy/Perfetto profil (4.6).
8. **Konsol:** Godot MIT olduğu için resmî konsol desteği yok. Yol üçüncü taraflardan geçiyor: W4 Games (Switch, Switch 2, Xbox Series, PS5), Lone Wolf, Pineapple Works, RAWRLAB, Sickhead vd. [A]. W4 Consoles ücreti 800 $/yıl/platform ya da 2.000 $/yıl tüm platformlar (<300 bin $ gelir ve <30 çalışan), gelir payı yok [B].
9. **Lisans ve maliyet:** Godot MIT, telif yok. Unity Personal, son 12 ayda **200.000 $ "Total Finances"** eşiğine kadar ücretsiz (fon da sayılıyor). Unity 6 ve öncesi için "royalty, revenue share veya runtime fee yok" maddesi şart metninde [A]. Pro 2.310 $/yıl/koltuk [B]. Unreal'da ürün başına ömür boyu ilk 1 M $'dan sonra %5 telif, "Launch Everywhere with Epic" ile %3,5, EGS gelirine telif yok [B].
10. **MCP ve ajan araçları:** Unity MCP en olgunu (CoplayDev 14.461★) ama editör gerektiriyor. Godot'ta Coding-Solo/godot-mcp (5.811★) headless CLI ile çalışıyor [A]. Epic'in resmî Claude Code eklentisi ve UE 5.8 MCP'si deneysel, editörün açık olmasını istiyor [A/B].
11. **GDScript mi C# mı?** 7k★'lı godogen projesi GDScript'ten C#'a geçti (2026-04-06), gerekçesi LLM'in C#'ta ilk denemede daha doğru kod üretmesi [B]. Ama Godot 4'te C# **web'e export edilemiyor**, Android/iOS'ta **deneysel** [A]. Ben GDScript'te `untyped_declaration=Error` + `--check-only` kapısının aynı hata sınıfını parse aşamasında yakaladığını doğruladım [A]. Öneri: katı GDScript. Sıcak yollar gerekirse GDExtension.
12. **Mimari ilkeleri:** Veri güdümlü (bir içerik = bir `.tres`; denge tabloları CSV), küçük sahneler ve bileşen düğümleri, tipli sinyallerle EventBus, "GAS-lite" yetenek sistemi, çerçeve verisiyle (startup/active/recovery) aksiyon durum makinesi. Kayıt dosyası JSON + şema sürümü + migrasyon. **Kullanıcıdan gelen `.tres` asla yüklenmez**, çünkü gömülü script çalıştırabilir [A].
13. **Oyun yapısı motora göre şekillenmeli:** Kesintisiz dev açık dünya yerine hub şehir + instanced zindan katları / "Gate"ler. Bu yapı hem Solo Leveling/DanMachi kurgusuna hem Godot'un güçlü olduğu ölçeğe uyuyor [C: Godot'un büyük açık dünya ölçeklenmesi burada ölçülmedi].
14. **Risk yönetimi:** İlk 2–3 hafta bir "Anime Rendering Spike" kapısı konmalı. VRoid tabanlı test karakteri hedef görünüme ulaşmazsa Unity'ye geçiş seçeneği açık tutulmalı. Karar matrisinde Godot 3,88, Unity 3,80, Unreal 3,05 çıktı. Fark küçük ve ağırlıklara duyarlı (§5).

---

## 1. Sürüm Durumu (2026-09-24)

| Motor | Güncel kararlı | Tarih | Not | Kaynak |
|---|---|---|---|---|
| Godot | **4.7.2-stable** | 2026-08-16 | 4.7: 2026-06-17 · 4.6: 2026-01-25 · 4.5: 2025-09-15 · `master` = 4.8-dev | [A][1][2] |
| Unity | **6.6 (6000.6.2f1)** | 2026-09-18 | 6.3 = **LTS** (6000.3.0f1: 2025-12-03; 6000.3.24f1'e kadar yama), 6.4: 2026-03-18, 6.5: 2026-06-15, 6.7 beta 1: 2026-09-17 | [A][9][10] |
| Unreal | **5.8.3** | 2026-09-22 | 5.8.0: 2026-06-17, 5.7: 2025-11-12. "5.8 son UE5". UE6 tarihi kaynaklar arasında çelişkili ("late 2027 EA" ve "~2029") | [B][16][17] |

Godot tarihleri etiket commit'lerinden, Unity tarihleri Unity'nin kendi `UnityCsReference` deposundaki sürüm etiketlerinden alındı. Unreal tarihleri ikincil kaynaklardan geliyor, çünkü EpicGames/UnrealEngine deposu hesap bağlamadan erişilemiyor.

---

## 2. Karşılaştırma: Oyun Özellikleri

### 2.1 Anime / toon render kalitesi

| Konu | Godot 4.7 | Unity 6.x (URP) | Unreal 5.8 |
|---|---|---|---|
| Yerleşik toon | `StandardMaterial3D`: **Diffuse Toon** ("hard cut"), **Specular Toon** [A][5] | Yok; URP'de özel shader veya paket | Yerleşik toon shading modeli yok [C] |
| Outline | **Stencil "Outline" ve "X-Ray" modları (4.5+)**, klasik "Grow" + ters cull ikinci pas [A][5]. 4.7.2'de render edip doğruladım [A] | Renderer Feature, UTS3/lilToon outline | Post-process veya ters hull materyali (özel iş) |
| Hazır anime shader | godot-vrm içinde MToon (471★); EXPWorlds Cel (245★), FlexibleToon (201★), godot-toon-outline (113★), godot-anime-sdf-shader (11★, SDF yüz) [A][22] | **UTS3** (Built-in/URP/HDRP; Unity Companion License), **lilToon** (MIT), MToon/UniVRM (3.388★), URPToonLit örneği (7.793★), GenshinCelShaderURP (768★; örnek modeller ticari değil), UnityGenshinToonShader (378★) [A][11][12][22] | VRM4U MToon; KawaiiToonShading (0★, 2026-07); motor fork'u gerektiren eski projeler [A][22] |
| Özel post-process | `CompositorEffect` (RenderingDevice ile özel pas) [A][5] | URP Render Graph / Renderer Features [C] | Post-process materyalleri (güçlü) |
| İkincil hareket (saç/etek) | **SpringBoneSimulator3D** + çarpışma şekilleri (yerleşik) [A][5] | UniVRM SpringBone, Magica Cloth (ücretli) [C] | Chaos Cloth, AnimDynamics |
| HDR / parlama | **HDR çıktı (4.7)**, glow tonemap öncesi (4.6), ayarlanabilir AgX (4.6) [A][3][4] | HDR çıktı var [C] | En güçlü |

**Yorum:** Genshin tarzı karakter görünümü büyük ölçüde shader işi: ramp dokular, SDF yüz gölgesi, düzeltilmiş yüz normalleri, rim light, outline ve stilize post. Bunların hepsi Godot'un GLSL benzeri, metin tabanlı shader dilinde yazılabilir. Claude bu işi metin olarak üretip Xvfb render'ı ile görsel olarak kontrol edebilir. Unity'de aynı sonuç **hazır** geliyor. Godot'ta tahminen 2–4 haftalık shader ve pipeline işi gerekiyor [C: süre tahmini].

### 2.2 3D aksiyon savaşı araçları

| Konu | Godot | Unity | Unreal |
|---|---|---|---|
| Animasyon durum makinesi | AnimationTree + `AnimationNodeStateMachine`, BlendSpace; **root motion** (`get_root_motion_position/rotation`) [A][5] | Mecanim + Animation Rigging + Timeline (olgun) [C] | AnimBP, **Motion Matching** (5.4'ten beri üretimde), Control Rig [B][16] |
| IK | **4.6 yeni IK çatısı:** IKModifier3D, TwoBoneIK3D, SplineIK3D, FABRIK3D, CCDIK3D, JacobianIK3D + kısıtlar [A][4] | Animation Rigging [C] | Control Rig, Full-Body IK |
| Retarget | BoneMap + SkeletonProfileHumanoid, RetargetModifier3D [A][5] | Humanoid Avatar (en kolayı) | IK Retargeter |
| Hitbox/fizik | Area3D, ShapeCast3D; **Jolt varsayılan (4.6)** [A][4] | PhysX; Physics Queries | Chaos |
| Yetenek sistemi | Hazır yok; biz yazacağız (§6.4) | Hazır yok (Asset Store'da var) | **Gameplay Ability System** (GAS) yerleşik [A: Epic eklentisinde GAS toolset'i listeleniyor][18] |
| AI | LimboAI (BT + HSM, 3.028★) [A][23] | Behavior paketleri | Behavior Tree, StateTree |
| Kamera | Phantom Camera (Cinemachine esinli, 3.572★) [A][23] | **Cinemachine** | Kamera sistemi + Sequencer |
| Ara sahne | AnimationPlayer + `Tween.tween_await` (4.7) + Dialogue Manager (3.876★) [A][3][23] | Timeline | **Sequencer** (en güçlü) |

### 2.3 Performans, platformlar, ağ, içe aktarma, yerelleştirme, kayıt, mod

| Konu | Godot | Unity | Unreal |
|---|---|---|---|
| Orta PC | Forward+ için önerilen: GTX 1050 / RX 460 sınıfı ve Vulkan 1.2 (basit projeler için) [A][6]. Shader baker, ubershader'lar (4.4) ve D3D12 varsayılanı (4.6, Windows) [A][4][7] | URP ölçeklenebilir; GPU Resident Drawer (Unity 6 / SRP 17) [A][13] | Nanite/Lumen ağır. Geliştirme için RTX 2080 / 8 GB+ öneriliyor [B][16] |
| Steam Deck | Linux native export; Vulkan Forward+ veya Mobile renderer [C: Deck'te ölçülmedi] | Olgun [C] | Ölçekleme gerekiyor [C] |
| Konsol | Üçüncü taraf: **W4** (Switch/Switch 2/Xbox Series/PS5), Lone Wolf, Pineapple Works, RAWRLAB, mazette!, Tuanisapps, Seaven, Sickhead [A][8]. W4 fiyatı §2.4'te [B] | Onaylı middleware; konsol için Pro gerekli [B][19] | Onaylı geliştiriciye birinci taraf destek [C] |
| Mobil | Android/iOS (GDScript tam; **C# deneysel**) [A][5]. 4.7'de VirtualJoystick yerleşik [A][3] | En güçlüsü [C] | Ağır |
| Ağ | Yüksek seviye multiplayer (ENet), WebSocket, WebRTC [A][5]; netfox (rollback, 1.105★) [A][23]; Nakama (13.404★, üç motoru da destekliyor) [A][23] | Netcode for GameObjects/Entities [C] | **Replikasyon en olgunu** [C] |
| glTF/FBX/VRM | glTF 2.0 önerilen format; runtime glTF yükleme; FBX (ufbx) [A][5]; godot-vrm (VRM 0/1, MToon, springBone) [A][22] | UniVRM (referans) | VRM4U; Interchange glTF'de 4 kemik etkisi sınırı hatası (5.8) [B][16] |
| Yerelleştirme | CSV ve gettext; BiDi, RTL ayna, pseudolocalization [A][5]; 4.6'da CSV iyileştirmesi [A][4] | Localization paketi [C] | String Tables |
| Kayıt | JSON, ConfigFile, `FileAccess.store_var` [A][5]. **`.tres` gömülü GDScript taşıyabilir**; güvenli yükleyici gerekir [A][24] | Özel [C] | SaveGame nesneleri |
| Mod | PCK/ZIP paketleri; güvenlik uyarısı resmî dokümanda [A][5]. 4.6 delta patch PCK [A][4]. godot-mod-loader (677★) [A][23] | Zor (IL2CPP) [C] | Zor (cook/pak) [C] |
| Steam | GodotSteam (3.749★). **GitHub deposu arşivlenmiş**; güncel konumu doğrulanamadı [A/C][23] | Steamworks.NET [C] | Online Subsystem Steam [C] |

### 2.4 Lisans ve maliyet (bizim için)

| | Godot | Unity | Unreal |
|---|---|---|---|
| Lisans | MIT [A] | Personal: son 12 ay "Total Finances" ≤ **200.000 $** (fon dahil; eşik aşılırsa "not use Unity Personal at all, even for… prototyping"). Pro: 200.001 $ – 24.999.999 $ [A][14] | EULA; ürün başına ömür boyu ilk **1 M $** muaf, sonrasında **%5**. "Launch Everywhere with Epic" ile **%3,5**; **EGS geliri muaf**; çeyreklik 10 bin $ muafiyeti "uçurum" şeklinde çalışıyor [B][19][20] |
| Runtime fee | Yok | Şart metni: Unity 6 ve öncesiyle yapılan projeler için "without royalty, revenue share, or a runtime fee" [A][14] | Yok |
| Koltuk ücreti | 0 | Pro **2.310 $/yıl/koltuk** (210 $/ay) [B][19] | 0 (oyun için) |
| Zorunlu atıf | Yok (MIT bildirimi) | Credits varsa "…was made with Unity®…" metni zorunlu. Splash ekranı Unity 6+ Personal'da isteğe bağlı [A][14][B][19] | Yok [C] |
| Konsol ek maliyeti | W4: 800 $/platform/yıl ya da 2.000 $/yıl tümü (<300 bin $ gelir, <30 kişi). Pro: 4.000 $ / 10.000 $. Gelir payı yok [B][19] | Pro lisansı [B] | Yok [C] |

Ayrıntılı gelir hesabı için bkz. `04-monetizasyon-ve-regulasyon.md`.

---

## 3. AI-Ajan Uyumluluğu (kritik kriter)

### 3.1 Bulut konteynerinde fiilen yaptıklarım (2026-09-24)

| Test | Sonuç |
|---|---|
| Godot 4.7.2 indirme (github.com releases) | ✅ Editör zip 77,9 MB. Tüm export şablonları 1,28 GB (4.7'de platform bazında indirme var), .NET sürümü 107,7 MB, win64 86 MB [A][1][3] |
| `--headless --import` (küçük proje) | ✅ 9,1 sn |
| Headless test koşucusu (`-s res://tests/run_tests.gd`) | ✅ 0,27 sn, exit code 0/1 doğru (Resource yükleme, formül ve EventBus sinyali test edildi) |
| Katı tip kapısı (`untyped_declaration=Error` + `--check-only`) | ✅ Tipsiz `var` ve Variant'tan `:=` çıkarımı **parse hatası** verdi, exit 1 |
| Görsel doğrulama: `xvfb-run` + `mesa-vulkan-drivers` (llvmpipe) | ✅ Forward+ Vulkan render, toon + stencil outline'lı küre PNG'ye kaydedildi (640×360, toplam ≈9,8 sn). `apt` Ubuntu arşivi erişilebilir durumda |
| C#: `apt install dotnet-sdk-8.0` + Godot .NET 4.7.2 | ✅ `dotnet build` 7,7 sn (NuGet'ten Godot.NET.Sdk indi), headless C# SceneTree koştu (sınıf adı dosya adıyla birebir olmalı) |
| `--doctool` API dökümü | ✅ 1.036 XML (6,6 MB) 1,2 sn'de. İmzalar tam, açıklamalar boş. Açıklamalar için godot deposunun `doc/classes`'ı etiketten çekilebilir |
| Unity / Unreal | ❌ `download.unity3d.com`, `docs.unity3d.com`, `dev.epicgames.com` engelli (HTTP 000). Unreal için disk de yetmiyor (~29 GB boş) |

Anlamı şu: Godot seçilirse Claude **birden fazla paralel bulut oturumunda** kod yazabilir, içe aktarabilir, test koşturabilir, ekran görüntüsüyle görsel QA yapabilir ve export alabilir. Bunun için kullanıcının PC'sinin açık olmasına gerek yok. Unity ve Unreal'da bu döngü kullanıcının makinesine (ya da GPU'lu bir self-hosted runner'a) bağlı kalıyor.

### 3.2 Karşılaştırma tablosu

| Kriter | Godot 4.7 | Unity 6.x | Unreal 5.8 |
|---|---|---|---|
| Sahne ve varlık formatı | `.tscn`/`.tres` metin, "mostly human-readable… easy for VCS" [A][5]; `.gd.uid` yan dosyası (tek satır `uid://…`) [A] | YAML (`%TAG !u! tag:unity3d.com,2011:`) [A][15]; referanslar `fileID` + `.meta` GUID [C]. Elle düzenleme kırılgan | `.uasset`/`.umap` ikili; Blueprint, AnimBP ve materyal grafikleri ikili; OFPA ile aktör başına dosya; `.utxt` deneysel [B][16] |
| Headless (GPU'suz) | `--headless` export'ta resmî olarak "required on platforms that do not have GPU access (such as CI)" [A][5] | `-batchmode -nographics` + lisans aktivasyonu [A][21] | `-nullrhi` ile test ve cook yapılabiliyor. Otomasyon testi başarısız olsa bile **exit code 0** dönüyor [B][16] |
| Boyut | ~78 MB | Birkaç GB [C] | ~25 GB zip / ~43 GB açılmış; kaynaktan ~225 GB [B][16] |
| CI | GitHub releases'tan indir ve koş; gdUnit4-action; godot-ci Docker (1.129★) [A][21] | GameCI: unity-builder (1.096★), unity-test-runner (266★). `UNITY_LICENSE`/`EMAIL`/`PASSWORD` secret'ları [A][21] | RunUAT BuildCookRun; pratikte self-hosted runner şart [B] |
| Test çatısı | **GUT 9.7.1** (MIT, 2.739★, 4.7.x dalı), **gdUnit4 v6.2.1** (MIT, 1.241★, 4.5–4.7.1; GDScript + C#) [A][21] | Unity Test Framework (NUnit) [C] | Automation + Gauntlet [B] |
| MCP | Coding-Solo/godot-mcp 5.811★ (CLI, headless ✅), hi-godot/godot-ai 2.581★ (editör), tugcantopaloglu/godot-mcp 466★ (157 araç, 4.7'de test edilmiş), godot-mcp-pro 606★ (15 $) [A][22] | **CoplayDev/unity-mcp 14.461★**; resmî `com.unity.ai.assistant` MCP [A/B][22] | Epic resmî `ModelContextProtocol` (UE 5.8, deneysel) + Claude Code eklentisi (303★). **Editör açık olmalı** [A][18] |
| Ajan skill'leri | godogen 6.993★, GodotPrompter 755★ [A][25] | gamedev-skills (çok motorlu, 1.133★) [A] | Epic resmî skill'i, quodsoler 344★ [A] |
| Dil ve LLM | GDScript (Godot'a özel eğitim verisi en fazla bu dilde) veya C# | C# (en büyük genel korpus) | C++ (UHT makroları, uzun derleme; Linux'ta Live Coding yok) + Blueprint (metin değil) [B][16] |

### 3.3 GDScript mi, C# mı?

- **C# lehine:** godogen tüm skill'lerini 2026-04-06'da C#/.NET 9'a taşıdı. Gerekçe: GDScript'te `:=` çıkarımının Variant döndüren API'lerde (`load()`, `instantiate()`, `abs/clamp/lerp/min/max`, dizi erişimi) sessizce bozulması. C#'ta tek `dotnet build` tüm bu hataları yakalıyor. Aynı kaynak şunu da not ediyor: "C# enum names are unreliable in LLM output (training data is predominantly GDScript)" [B][25].
- **GDScript lehine:** Godot 4'te C# **web'e export edilemiyor**, Android/iOS'ta **deneysel** [A][5]. Eklentilerin çoğu GDScript. godot-mod-loader "GDScript based" oyunlar için [A][23]. Derleme adımı yok, hot-reload var. Godot'a özel örneklerin çoğu GDScript. En önemlisi: **godogen'in şikâyet ettiği hata sınıfını katı ayarlar parse aşamasında yakalıyor.** Bunu kendim doğruladım (§3.1).
- **Karar:** Katı tipli GDScript. Proje ayarları `untyped_declaration=Error` (diğer "unsafe_*" uyarıları en az Warn); her PR'da `--check-only` + gdlint. Çıkış kriteri: Dikey dilimde (vertical slice) script kaynaklı CPU süresi karede >3 ms olursa ya da ajanın runtime tip hataları yüksek kalırsa, sıcak sistemler **GDExtension'a (C++/Rust)** taşınır. Karma GDScript+C# kod tabanından kaçınılmalı [C: kendi değerlendirmem].

---

## 4. Motorlara Göre Kısa Değerlendirme

**Godot 4.7.** Artıları: metin formatları, headless doğrulama döngüsü, 78 MB boyut, MIT, sıfır telif, 4.5–4.7'de gelen anime ve aksiyon için kritik özellikler (stencil outline, IK, Jolt, spring bone, HDR, shader baker). Eksileri: anime shader'ları ve animasyon araçları kendi başımıza yazılacak. Konsol üçüncü taraf üzerinden gidiyor. Büyük ölçekli 3D aksiyon oyunlarında kanıtlanmışlığı Unity/Unreal'dan az [C]. GodotSteam'in bakım konumu belirsiz [C].

**Unity 6.x.** Artıları: en zengin anime/VRM/lip-sync ekosistemi, en olgun MCP, olgun mobil ve konsol, Timeline, Cinemachine, VFX Graph. Eksileri: Claude bulutta Unity'yi kuramıyor ve çalıştıramıyor. YAML + GUID referansları ajan için kırılgan. 200 bin $ sonrası koltuk ücreti var (tek kişi için yönetilebilir). Şartlar "Tier Eligibility" gibi sürekli uyum yükü getiriyor [A][14].

**Unreal 5.8.** Artıları: AAA render, GAS, Motion Matching, Sequencer, replikasyon, MetaHuman; Epic'in resmî Claude eklentisi. Eksileri: ikili varlıklar, 40+ GB kurulum, C++ derleme döngüsü, Linux'ta Live Coding yok, toon render en zahmetli motor, %5 telif. Tek geliştirici + AI ajanı senaryosu için en ağır seçenek.

---

## 5. Karar Matrisi (ağırlıklar benim önerim, puanlar 1–5)

| Kriter (ağırlık) | Godot | Unity | Unreal |
|---|---|---|---|
| AI ajan özerkliği: bulut, headless, metin formatı (%25) | 5 | 2 | 1 |
| Anime render ekosistemi (%15) | 3 | 5 | 2 |
| Aksiyon savaşı ve animasyon araçları (%15) | 3,5 | 4 | 5 |
| Lisans ve maliyet (%10) | 5 | 4 | 3 |
| Performans ve ölçeklenebilirlik (%10) | 3 | 4 | 5 |
| Platform erişimi: konsol ve mobil (%10) | 3 | 5 | 5 |
| Ekosistem ve hazır varlıklar (%10) | 3 | 5 | 4 |
| İterasyon hızı ve boyut (%5) | 5 | 3 | 1 |
| **Ağırlıklı toplam** | **3,88** | **3,80** | **3,05** |

**Duyarlılık:** AI özerkliğinin ağırlığı %15'e indirilip anime ekosistemininki %25'e çıkarılırsa Unity 4,10'a çıkıyor, Godot 3,68'e iniyor. Yani karar kullanıcının iş modeline bağlı. **Claude'un ana geliştirici olduğu ve paralel bulut oturumlarıyla çalışacağı bu projede** doğru ağırlık AI özerkliği. Ama bu, doğrulanması gereken bir varsayım. Bu yüzden §8'deki "Rendering Spike" kapısını öneriyorum.

---

## 6. Önerilen Proje Mimarisi (Godot 4.7, GDScript)

### 6.1 Depo yapısı

```
isekai/
├─ project.godot              # tek motor sürümü: tools/godot_version.txt = 4.7.2
├─ CLAUDE.md                  # ajan kuralları (özet §6.8)
├─ .mcp.json                  # godot-mcp (Coding-Solo), headless CLI
├─ .claude/skills/            # godot-check, godot-test, godot-shot, data-validate, asset-import
├─ .github/workflows/         # ci.yml (her PR), nightly-export.yml, release.yml
├─ docs/ (research/, design/, adr/, architecture/interfaces.md)
├─ addons/                    # 3. parti: gdUnit4, phantom_camera, dialogue_manager, godot-vrm, limboai*
├─ src/
│  ├─ core/                   # autoload'lar + temel tipler (Result, Rng, Log)
│  ├─ systems/                # her sistem = kendi klasörü + README (public API) + testler
│  │  ├─ combat/  abilities/  stats/  status_effects/  progression/
│  │  ├─ inventory/  loot/  crafting/  quests/  dialogue/  ai/
│  │  ├─ world/ (hub, gate/zindan üretimi, spawner)  camera/  input/  audio/  vfx/
│  ├─ entities/ (player/, enemies/, npcs/, bosses/)   # küçük sahneler + bileşen düğümleri
│  └─ ui/ (theme/, screens/, widgets/, system_window/) # "System" arayüzü (Solo Leveling tarzı)
├─ data/                      # İÇERİĞİN TEK DOĞRU KAYNAĞI
│  ├─ abilities/*.tres  items/*.tres  enemies/*.tres  gates/*.tres  quests/*.tres
│  ├─ balance/*.csv           # XP eğrisi, drop oranları, stat büyümesi (tablo)
│  ├─ dialogue/*.dialogue     # Dialogue Manager
│  └─ localization/*.csv      # anahtar,en,tr,ja…
├─ assets/ (models/, textures/, audio/, vfx/, fonts/)   # Git LFS; PROVENANCE.csv zorunlu
├─ tools/ (python: bpy pipeline, veri doğrulayıcı, codegen; gd: editör araçları)
└─ tests/ (unit/, integration/, smoke/, sim/, visual/golden/)
```
\* LimboAI (MIT) ya C++ modülü ya da GDExtension olarak kullanılabiliyor. GDExtension sürümü özel motor derlemesi gerektirmiyor, ama README'ye göre "somewhat limited in features" [A][23]. İkili eklenti olduğu için Godot sürümüyle uyumu CI'da kontrol edilmeli.

### 6.2 Autoload'lar (en fazla 8; Godot dokümanı autoload'u aşırı kullanmamayı öğütlüyor [A][5])

| Autoload | Sorumluluk | Kural |
|---|---|---|
| `EventBus` | Yalnızca **tipli sinyaller** (`damage_dealt`, `enemy_killed`, `quest_updated`…) | Durum tutmaz |
| `GameState` | Oturum durumu: aktif profil, dünya, zorluk | Tek mutable global |
| `DataRegistry` | Başlangıçta `data/`'yı tarar, id → Resource indeksi kurar, eksik referansı hata sayar | Salt okunur |
| `SaveService` | JSON kayıt/yükleme, migrasyon, yedek, Steam Cloud köprüsü | §6.6 |
| `SettingsService` | ConfigFile; grafik ön ayarı (PC/Deck), ses, tuş atamaları | — |
| `SceneRouter` | `ResourceLoader.load_threaded_request` ile yükleme ekranı, hub ↔ gate geçişleri | — |
| `AudioDirector` | Müzik katmanları, bus'lar, seslendirme kuyruğu | — |
| `Log` | 4.5 özel logger + script backtrace ile oyun içi hata raporu [A][7] | — |

### 6.3 Veri güdümlü tasarım

- **Tipli Resource sınıfları** (`class_name AbilityData extends Resource`, `@export` alanlar). Konteynerde test ettiğim örnek aynen bu kalıpta [A]. **Her içerik ayrı bir `.tres` dosyası** olmalı: diff'ler küçük kalır, paralel ajan çakışması azalır.
- **Denge tabloları CSV'de** tutulur (LLM ve tablo dostu). `tools/` altındaki bir script ya da `EditorImportPlugin` bunları tipli Resource'lara çevirir. CI'da codegen çalıştırılır, ardından `git diff --exit-code` ile üretilmiş dosyaların güncel olduğu kontrol edilir.
- **ID kuralı:** `StringName` id, küçük harf ve alt çizgi. CI'da tekillik ve "tüm referanslar çözülüyor mu" doğrulaması yapılır.
- **Runtime'da Resource'lar değiştirilmez.** Durum gerekiyorsa `duplicate()` ya da ayrı bir durum nesnesi kullanılır.

### 6.4 Savaş ve yetenek sistemi ("GAS-lite")

- **Aktör bileşenleri:** `StatBlock` (temel değer + toplamsal/çarpımsal modifier), `TagSet` (sayaçlı StringName kümesi: `state.stunned`, `element.fire`), `AbilitySystem` (verilmiş yetenekler, cooldown, maliyet, aktif efektler), `Hurtbox`/`Hitbox` (Area3D/ShapeCast3D), `HitReaction`.
- **AbilityData →** hedefleme + maliyet + cooldown + bir `Array[EffectData]` listesi (`DamageEffect`, `ApplyStatusEffect`, `SpawnProjectileEffect`, `DashEffect`, `SummonShadowEffect` gibi). Efektler `apply(ctx: EffectContext)` üzerinden **saf fonksiyon** gibi çalışır, sahneden bağımsız birim test edilir. RNG enjekte edildiği için deterministiktir.
- **Aksiyon durum makinesi (oyuncu ve bosslar):** Hiyerarşik yapı: Locomotion {Idle, Move, Sprint, Air}, Action {Attack[n], Skill, Dodge, Parry, HitStun, Knockdown}, Cinematic. Her aksiyon bir `ActionData` kaynağıdır: startup/active/recovery kareleri, cancel pencereleri, i-frame, root motion bayrağı, hitstop süresi, kamera sarsıntısı, VFX/SFX ipuçları. Savaş mantığı sabit **60 Hz** `_physics_process`'te çalışır. Animasyon ayrı katmandadır: AnimationTree durum makinesi ve BlendSpace, saldırılarda root motion, ayak yerleşimi için TwoBoneIK3D, saç ve etek için SpringBoneSimulator3D [A][4][5].
- **Hasar hattı:** `HitEvent` → `DamageCalc` (saf) → uygula → `EventBus.damage_dealt` → UI (hasar sayıları), VFX, SFX, kamera ve hitstop dinleyicileri. Sistemler birbirini doğrudan çağırmaz.

### 6.5 Dünya yapısı

Hub şehri (Lonca, dükkân, NPC ilişkileri) ile **instanced "Gate/zindan katları"** kombinasyonu öneriyorum. Katlar `GateData` ile tanımlanır: biyom, kat sayısı, düşman havuzu, boss, modifier'lar. Oda parçalarından prosedürel olarak birleştirilir. Bu hem Solo Leveling'in Gate'lerine hem DanMachi'nin katlı zindanına birebir uyuyor. Ayrıca sahneleri küçük ve yüklenebilir tutarak performans riskini azaltıyor [C].

### 6.6 Kayıt sistemi

- `user://saves/slot_N.json` içinde `schema_version` alanı ve `migrations/` altında `v1_to_v2.gd` gibi sıralı migrasyonlar olur. Yazma **atomik** yapılır (geçici dosyaya yaz, sonra yeniden adlandır). 3 dönen yedek ve sağlama toplamı tutulur. Steam Cloud GodotSteam üzerinden bağlanır.
- **Kullanıcı dizininden asla `.tres`/`.res` yüklenmez.** Godot Safe Resource Loader'ın açıkladığı gibi `.tres` gömülü GDScript taşıyabilir [A][24]. PCK modları için de resmî doküman güvenlik uyarısı yapıyor [A][5].
- CI'da eski sürüm kayıt fikstürlerini yükleyen **migrasyon testleri** koşar.

### 6.7 Yerelleştirme ve mod

- Tüm metinler anahtarla tutulur (`UI_*`, `ABILITY_*_NAME`, `DLG_*`). Godot'nun CSV çevirileri kullanılır (4.6'da iyileşti) [A][4]. CI'da **pseudolocalization** açık bir ekran görüntüsü turu yapılır (taşan metni yakalamak için) [A][5]. JP/CN için font fallback eklenir. Seslendirme dosyaları dil klasörlerine ayrılır, altyazı zamanlaması veri dosyasında tutulur.
- **Mod v1 (lansman sonrası): yalnızca veri modları.** CSV/JSON ve varlık içeren PCK/ZIP paketleri tip beyaz listesiyle yüklenir, script içeremez. **Mod v2:** godot-mod-loader ile script modları, kullanıcıya açık risk uyarısıyla sunulur [A][23]. DLC ve yamalarda 4.6'nın delta patch PCK'ları kullanılır [A][4].

### 6.8 Kod kuralları (CLAUDE.md özeti)

1. Godot resmî GDScript stil kılavuzu uygulanır. `gdformat`/`gdlint` (gdtoolkit 4.5.0, PyPI) pre-commit'te ve CI'da koşar [A][21].
2. **Statik tip zorunlu.** `untyped_declaration=Error`, `--check-only` kapısı var [A]. Motor API'si tahmin edilmez: pinli sürümden `--doctool` XML'i ya da `doc/classes` kontrol edilir [A]. Godot 3 sözdizimi yasak (`yield`, `KinematicBody` vb.) [C: yaygın LLM hatası].
3. İsimlendirme: dosya, fonksiyon ve değişkenler `snake_case`; `class_name` `PascalCase`; sabitler `SCREAMING_CASE`; sinyaller geçmiş zaman (`health_changed`); özel üyeler `_` önekli.
4. **"Signals up, calls down."** `get_node("../../x")` yasak. `%UniqueName` ya da `@export` düğüm referansı kullanılır.
5. Mantık `RefCounted` sınıflarda (test edilebilir), sunum Node'larda durur. Sihirli sayı yazılmaz, değerler `data/`'dan gelir.
6. Oynanış `_physics_process` içinde ve delta tabanlı yazılır. Rastgelelik tohumlanmış `Rng` servisiyle üretilir.
7. Genel API `##` doc-comment ile belgelenir. Her sistemin `README.md` dosyası public API'yi ve dinlediği/yaydığı sinyalleri listeler.
8. Hata yönetiminde `push_error` + debug `assert` kullanılır. Sessiz `null` dönüşü yasak.

### 6.9 Paralel AI ajanları için depo düzeni

- **Bir sistem = bir klasör = bir görev sahibi.** Sistemler arası iletişim yalnızca sistemin facade'ı (`api.gd`) ya da `EventBus` üzerinden olur. Sözleşmeler `docs/architecture/interfaces.md` dosyasında ve **sözleşme testlerinde** tutulur.
- **Küçük sahneler.** Büyük sahne, alt sahnelerin örneklenmesiyle kurulur. 4.6'nın benzersiz Node ID'leri yeniden düzenlemeyi güvenli kılıyor [A][4]. Aynı `.tscn` dosyasına iki ajan aynı anda dokunmamalı.
- **Bir içerik = bir dosya.** Kayıt dizinleri (registry) elle düzenlenmez, codegen ile üretilir.
- Her ajan oturumu ayrı dal veya git worktree'de çalışır. PR, CI geçmeden birleşmez. Tasarım kararları `docs/adr/` altında ADR olarak yazılır.
- `.gitattributes`: `*.glb *.vrm *.png *.wav *.ogg *.psd` LFS'e gider. `.tscn`/`.tres`/`.gd` düz metin kalır. `.godot/` dizini git'e girmez, CI önbelleğine alınır.

---

## 7. Test ve CI Stratejisi

| Katman | Ne | Nerede |
|---|---|---|
| 0. Statik | gdformat --check, gdlint, `--check-only`, veri şeması ve id doğrulama (Python) | Her PR, bulut ve Actions |
| 1. Birim | gdUnit4 (ya da GUT), saf mantık: hasar, stat, loot, XP, kayıt migrasyonu | Her PR (saniyeler) |
| 2. Entegrasyon ve duman | Her `.tscn` örneklenir, N kare headless koşturulur, `push_error` = başarısız | Her PR |
| 3. Simülasyon | Deterministik savaş simülasyonu (ör. 1.000 dövüş): TTK ve DPS eğrileri, ekonomi kaynak/tüketim dengesi | Gece |
| 4. Görsel regresyon | Xvfb + llvmpipe ile ana sahnelerin PNG'leri altın görüntülerle toleranslı karşılaştırılır. Claude görüntüleri kendisi de inceler (çok kipli). Ayrıca pseudolocalization turu | Gece, kritik PR'larda |
| 5. Export | Linux ve Windows build'leri, artefakt olarak yüklenir. Etiket gelince game-ci/steam-deploy (344★) ile Steam'e gönderilir [A][21] | Gece ve sürüm |
| 6. Performans | CPU tarafı headless monitörlerle ölçülür. GPU ve Deck ölçümleri kullanıcının PC'sinde / Deck'te haftalık yapılır (Tracy/Perfetto, 4.6) [A][4] | Haftalık |

GitHub Actions iskeleti (özet):

```yaml
jobs:
  test:
    runs-on: ubuntu-24.04
    steps:
      - uses: actions/checkout@v4
        with: { lfs: true }
      - run: |
          V=$(cat tools/godot_version.txt)   # 4.7.2
          curl -sLo g.zip https://github.com/godotengine/godot/releases/download/$V-stable/Godot_v$V-stable_linux.x86_64.zip
          unzip -q g.zip && mv Godot_v$V-stable_linux.x86_64 /usr/local/bin/godot
      - uses: actions/cache@v4
        with: { path: .godot, key: godot-import-${{ hashFiles('assets/**', 'data/**') }} }
      - run: godot --headless --import
      - run: find src -name '*.gd' -print0 | xargs -0 -n1 godot --headless --check-only -s   # ya da tek script ile toplu kontrol
      - run: GODOT_BIN=/usr/local/bin/godot xvfb-run -a addons/gdUnit4/runtest.sh -a res://tests
        # runtest.sh, GdUnitCmdTool.gd'yi çağırır (depoda doğrulandı). Alternatif: resmî gdUnit4-action.
        # Headless mod için kullanılacak bayrak gdUnit4 sürümüne göre kontrol edilmeli [C]
```

**Bulut oturumu SessionStart hook'u:** Godot'u GitHub releases'tan indirir, `apt install xvfb mesa-vulkan-drivers` çalıştırır (her ikisi de bu oturumda çalıştı) ve `.mcp.json` içindeki godot-mcp'yi `npx` ile başlatır (npm registry izinli).

---

## 8. Performans Bütçesi (hedef; öneri, ölçülmüş değer değil)

| Profil | Çözünürlük / FPS hedefi | Renderer |
|---|---|---|
| Düşük-orta PC (GTX 1060 / RX 580 sınıfı, 16 GB) | 1080p / 60 ("Orta") | Forward+ |
| Steam Deck | 800p / 40 hedef, 30 taban ("Deck" ön ayarı) | Forward+, Mobile ile karşılaştırılmalı |
| Önerilen PC (RTX 3060 sınıfı) | 1440p / 60+ ("Yüksek") | Forward+ |

**60 FPS'te 16,6 ms kare bütçesi.** CPU (ana thread): oynanış script'leri ≤2,5 ms · fizik (Jolt) ≤1,5 · animasyon (AnimationTree, IK, spring bone) ≤2,0 · AI ≤1,0 · UI ≤0,8 · motor ve render CPU ≤5,0 · pay ≈3,8. GPU: opak + toon ≤6 ms · outline ≤0,8 · gölge ≤2 · post (glow, renk, SSR/SSAO Deck'te kapalı) ≤2 · VFX ≤1,5 · UI ≤0,5 · pay ≈3,8.

**İçerik bütçesi (PC / Deck):**
- Draw call: ≤1.500 / ≤800.
- Ekrandaki üçgen: ≤2 M / ≤0,8 M.
- Kahraman: 40–70k üçgen, ≤3 materyal, 2K dokular, ≤120 kemik (saç ve etek zincirleri dahil).
- Sıradan düşman: 8–15k üçgen, ≤60 kemik. Boss: ≤100k üçgen.
- Eşzamanlı animasyonlu düşman: ≤40 / ≤25 (animasyon LOD'u ve görünürlük mesafeleriyle).
- VRAM ≤3 GB, RAM ≤4 GB (Deck).
- Yükleme ≤8 sn (SSD). **Shader takılması sıfır** (4.5 shader baker + ubershader'lar) [A][7].
- Kurulum boyutu ≤20 GB.

---

## Oyunumuz İçin Çıkarımlar

1. **Motor: Godot 4.7.2'ye sabitle.** 4.8'e ancak kararlı sürüm + en az bir yama çıktıktan sonra, ayrı bir dalda ve tüm test takımı geçerek yükselt. Sürüm `tools/godot_version.txt` dosyasında tek yerde tutulur.
2. **Dil: katı tipli GDScript.** C# kullanılmaz (mobil ve konsol riski, karma kod tabanı). Sıcak yollar için GDExtension kullanılır. Dikey dilimde tekrar değerlendirilir (§3.3).
3. **İlk 2–3 hafta "Anime Rendering Spike" kapısı:** VRoid/VRM test karakteri + ramp shading + SDF yüz gölgesi + stencil outline + rim light + stilize post + spring bone saç ile üç sabit kamera açısından hedef konsept karelerine ulaşılmalı. Kullanıcının onayı alınmalı ve Deck'te ≥40 FPS görülmeli. **Başarısız olursa Unity 6.3 LTS'ye geçiş** değerlendirilir. Bu kapı erken konduğu için geçişin maliyeti düşük kalır.
4. **Claude'un bulut "doğrulama döngüsü" ilk günden kurulsun:** SessionStart hook, `godot-check` / `godot-test` / `godot-shot` skill'leri, `.mcp.json` içinde godot-mcp, `--doctool` API dökümü. Paralel oturumlar bu döngü sayesinde güvenle çalışabilir.
5. **Oyun yapısını motora göre şekillendir:** Hub + instanced Gate/zindan katları. Kesintisiz açık dünya en az ilk sürümde kapsam dışı.
6. **Yetenek sistemi GAS-lite ve veri güdümlü olsun:** Solo Leveling'in "Sistem" penceresi, sınıf/iş değişimi, gölge çağırma gibi fantezi özellikleri `EffectData` kombinasyonlarıyla, kod yazmadan içerik olarak eklenebilmeli.
7. **Çok oyunculu mod lansmanda yok.** Asenkron sosyal özellikler (liderlik tablosu, lonca) Nakama gibi bir arka uçla sonraya bırakılır. Savaş kodu yine de deterministik ve sunucu otoriteli dönüşüme uygun yazılır (netfox ile ileride co-op zindan mümkün).
8. **Konsol: PC (Steam) + Steam Deck önce.** Konsol için 1.0 + 12–24 ay içinde W4 ya da bir porting ortağı değerlendirilir (lisans maliyeti ~2.000 $/yıl [B]). Bu yüzden şimdiden: gamepad-öncelikli UI, yalnızca GDScript, platforma özel kod `platform/` soyutlamasının arkasında.
9. **Güvenlik ve hukuk:** Kullanıcı `.tres` dosyası yüklenmez. Her varlık için `PROVENANCE.csv` tutulur (rapor 06). Unity'ye geçilirse "Tier Eligibility" ve credits atıf metni takip edilir [A][14].

## Belirsizlikler ve Riskler

- **Anime görsel kalitesinde Godot riski (orta-yüksek):** Unity'deki UTS3/lilToon seviyesine ulaşmak için özel shader işi gerekiyor. Godot topluluğunda SDF yüz gölgesi örnekleri çok küçük (11★). Bu yüzden spike kapısı şart.
- **Büyük 3D sahne performansı:** Godot'un yoğun sahnelerde Unity/Unreal'a göre ölçeklenmesi burada ölçülmedi [C]. Bütçeler ve instanced yapı bu riski azaltıyor, ama Deck ölçümü erken yapılmalı.
- **Konsol:** Tek küçük satıcıya (W4) veya porting ortağına bağımlılık var. W4 fiyatları ikincil kaynaktan [B]. Nintendo'nun Switch 2 devkit politikası indie'ler için kısıtlı olabilir [B][19].
- **GodotSteam:** GitHub deposu arşivlenmiş görünüyor, yeni konumu ve bakım durumu doğrulanamadı [C].
- **LLM hata profili:** GDScript'te Godot 3 sözdizimi halüsinasyonu ve Variant çıkarımı riski var. Katı ayarlar ve `--doctool` bunu azaltıyor ama sıfırlamıyor. godogen'in C# tercihi karşı kanıt olarak not edilmeli [B].
- **Yazılım render sınırı:** llvmpipe ile ekran görüntüsü alınabiliyor ama **video kaydı ve performans ölçümü güvenilir değil** (godogen de yazılım Vulkan'da videonun atlanmasını öneriyor [B][25]). GPU ölçümleri kullanıcının makinesinde yapılmalı.
- **Doğrulanamayanlar:** Unity Editor'ün disk boyutu, Unreal'ın 5.8 konsol ve Deck performansı, UE6 tarihi (kaynaklar çelişiyor), gdUnit4'ün 4.7.2 ile resmî uyumu (README 4.7.1'e kadar listeliyor; büyük olasılıkla çalışır), Steam Deck donanım özellikleri (bu oturumda birincil kaynağa ulaşılamadı).
- **Fiyatlar hızla eskiyor:** Unity Pro fiyatı iki yılda iki kez arttı [B][19]. Lansmandan önce tüm lisans ve fiyat tabloları yeniden doğrulanmalı.
- **Ağ politikası değişirse:** Bu oturumda Ubuntu apt arşivi, NuGet ve github.com erişilebildi. Ortam "Trusted" ayarından çıkarılırsa ya da değişirse SessionStart kurulumu bozulabilir. Godot ikilisini depo dışında (ör. releases önbelleği) tutmak yedek plan olabilir.

## Kaynaklar

1. Godot sürüm etiketleri ve indirmeler (etiket commit tarihleri `git fetch` ile okundu; boyutlar HTTP HEAD ile ölçüldü): https://github.com/godotengine/godot/releases/tag/4.7.2-stable · https://github.com/godotengine/godot/releases/download/4.7.2-stable/Godot_v4.7.2-stable_linux.x86_64.zip · https://raw.githubusercontent.com/godotengine/godot/master/version.py
2. Godot 4.5/4.6/4.7 etiketleri: https://github.com/godotengine/godot/tree/4.5-stable · https://github.com/godotengine/godot/tree/4.6-stable · https://github.com/godotengine/godot/tree/4.7-stable
3. Godot 4.7 sürüm sayfası verisi: https://github.com/godotengine/godot-website/blob/master/_data/release_4_7/features.yml · https://github.com/godotengine/godot-website/blob/master/_data/release_4_7/general.yml · https://github.com/godotengine/godot-website/blob/master/collections/_article/godot-4-7-lights-camera-action.md
4. Godot 4.6 sürüm sayfası verisi: https://github.com/godotengine/godot-website/blob/master/_data/release_4_6/features.yml · https://github.com/godotengine/godot-website/blob/master/_data/release_4_6/general.yml
5. Godot dokümanları (godot-docs, master, 2026-09-22): https://github.com/godotengine/godot-docs/blob/master/tutorials/editor/command_line_tutorial.rst · …/tutorials/3d/standard_material_3d.rst · …/tutorials/scripting/c_sharp/c_sharp_basics.rst · …/tutorials/export/exporting_pcks.rst · …/tutorials/io/saving_games.rst · …/tutorials/animation/animation_tree.rst · …/about/list_of_features.rst · …/engine_details/file_formats/tscn.rst · …/tutorials/rendering/compositor.rst · …/tutorials/best_practices/autoloads_versus_regular_nodes.rst · …/classes/class_springbonesimulator3d.rst · …/classes/class_ikmodifier3d.rst
6. Godot sistem gereksinimleri: https://github.com/godotengine/godot-docs/blob/master/about/system_requirements.rst
7. Godot 4.5 sürüm girdileri (stencil, shader baker, backtrace, abstract, variadic): https://github.com/godotengine/godot-website/tree/master/collections/_release_4_5
8. Godot konsol sayfası ve yazıları: https://github.com/godotengine/godot-website/blob/master/pages/consoles.html · https://github.com/godotengine/godot-website/blob/master/collections/_article/about-official-console-ports.md · https://github.com/godotengine/godot-website/blob/master/collections/_article/godot-consoles-all-you-need-know.md
9. Unity sürüm etiketleri (UnityCsReference): https://github.com/Unity-Technologies/UnityCsReference/tags
10. Unity 6.3 LTS / 6.0 LTS ifadesi (Unity'nin kendi deposu): https://github.com/Unity-Technologies/arfoundation-samples
11. Unity Toon Shader (UTS3) README ve lisansı: https://github.com/Unity-Technologies/com.unity.toonshader
12. lilToon (MIT): https://github.com/lilxyzw/lilToon · UnityURPToonLitShaderExample: https://github.com/ColinLeung-NiloCat/UnityURPToonLitShaderExample · GenshinCelShaderURP: https://github.com/Gaolingx/GenshinCelShaderURP · UnityGenshinToonShader: https://github.com/kaze-mio/UnityGenshinToonShader
13. Unity HDRP "What's new 17" (GPU Resident Drawer): https://github.com/Unity-Technologies/Graphics/blob/master/Packages/com.unity.render-pipelines.high-definition/Documentation~/whats-new-17.md
14. Unity Editor Software Terms (Last Updated: June 30, 2026): https://github.com/Unity-Technologies/TermsOfService/blob/HEAD/Unity%20Software%20Additional%20Terms.md
15. Unity YAML sahne örneği: https://github.com/Unity-Technologies/EntityComponentSystemSamples/blob/master/EntitiesSamples/Assets/Boids/Boids.unity
16. Unreal Engine ajan/headless inceleme belgesi (2026-09-24; sürüm tarihleri, boyutlar, ikili formatlar, CLI): https://github.com/r-melvin/krakow-1795/blob/HEAD/docs/UNREAL_SPIKE.md
17. Unreal lisans özeti (ikincil): https://github.com/intendednull/buiy/blob/HEAD/docs/prior-art/unreal-slate-umg/distribution-and-governance.md · Birincil (bu oturumda erişilemedi, rapor 04'te kullanıldı): https://www.unrealengine.com/en-US/license
18. Epic resmî Claude Code eklentisi: https://github.com/EpicGames/unreal-engine-skills-for-claude-code-plugin
19. Motor lisans/fiyat referans dosyası (last-verified 2026-09-05; Unity Pro 2.310 $, W4 fiyatları, 6.3 LTS, splash/atıf, UE EULA ayrıntıları): https://github.com/austintheriot/dotfiles/blob/HEAD/.claude/rules/game-engines.md · Destekleyici: https://github.com/knightdx91-alt/Bloodborn/blob/HEAD/design/pillars.md
20. Rapor 04 (monetizasyon), Unity/Unreal birincil fiyat URL'leri: `docs/research/04-monetizasyon-ve-regulasyon.md` (https://unity.com/pricing, https://www.unrealengine.com/en-US/license)
21. Test ve CI: https://github.com/bitwes/Gut · https://github.com/godot-gdunit-labs/gdUnit4 · https://github.com/godot-gdunit-labs/gdUnit4-action · https://github.com/abarichello/godot-ci · https://pypi.org/project/gdtoolkit/ · https://github.com/game-ci/documentation/blob/main/docs/03-github/02-activation.mdx · https://github.com/game-ci/unity-builder · https://github.com/game-ci/unity-test-runner · https://github.com/game-ci/steam-deploy
22. MCP'ler, VRM ve shader depoları: https://github.com/Coding-Solo/godot-mcp · https://github.com/hi-godot/godot-ai · https://github.com/tugcantopaloglu/godot-mcp · https://github.com/youichi-uda/godot-mcp-pro · https://github.com/CoplayDev/unity-mcp · https://github.com/V-Sekai/godot-vrm · https://github.com/vrm-c/UniVRM · https://github.com/EXPWorlds/Godot-Cel-Shader · https://github.com/CaptainProton42/FlexibleToonShaderGD · https://github.com/EMBYRDEV/godot-toon-outline · https://github.com/albanogiovanni/godot-anime-sdf-shader · https://github.com/pookiepied/KawaiiToonShading · rapor 06 (`06-ai-3d-ve-animasyon-araclari.md`)
23. Godot eklentileri: https://github.com/limbonaut/limboai · https://github.com/ramokz/phantom-camera · https://github.com/nathanhoad/godot_dialogue_manager · https://github.com/foxssake/netfox · https://github.com/heroiclabs/nakama · https://github.com/GodotSteam/GodotSteam · https://github.com/GodotModding/godot-mod-loader
24. Godot Safe Resource Loader (`.tres` içinde gömülü GDScript riski): https://github.com/derkork/godot-safe-resource-loader
25. godogen (GDScript → C# geçişi, headless yakalama notları): https://github.com/htdt/godogen · https://github.com/htdt/godogen/blob/HEAD/docs/gdscript-vs-csharp.md · https://github.com/htdt/godogen/blob/HEAD/engines/godot.md · https://github.com/htdt/godogen/blob/HEAD/CHANGELOG.md · GodotPrompter: https://github.com/jame581/GodotPrompter
26. Claude Code bulut oturumları (ağ erişimi, ortam): https://code.claude.com/docs/en/claude-code-on-the-web
27. Kendi konteyner ölçümlerim (2026-09-24): Godot 4.7.2 headless import/test/check-only, Xvfb + Mesa llvmpipe 25.2.8 render, Ubuntu 24.04 apt `dotnet-sdk-8.0` 8.0.131, Godot .NET 4.7.2 + `dotnet build`, `--doctool`. Erişim testleri: download.unity3d.com, docs.unity3d.com, dev.epicgames.com, docs.godotengine.org, w4games.com → engelli; api.nuget.org ve archive.ubuntu.com → erişilebilir.
