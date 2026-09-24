# 05 — Yapay Zekâ ile Görsel, Video ve 2D Asset Üretim Araçları (Higgsfield dahil)

> Hazırlanma: 2026-09-24
>
> **Yöntem ve sınırlar:** Bu rapor yazılırken oturumun ortak WebSearch bütçesi (200/200) dolmuştu. higgsfield.ai, ai.google.dev, huggingface.co, fal.ai, civitai.com, kaggle.com, copyright.gov ve store.steampowered.com gibi siteler egress proxy tarafından engelliydi. Bu yüzden doğrulama şu kaynaklardan yapıldı:
> - Resmî GitHub repolarındaki README ve LICENSE dosyaları (raw.githubusercontent.com)
> - npm ve PyPI kayıtları
> - Erişilebilen **cloud.google.com** fiyat sayfası
> - **code.claude.com** dokümanları
> - Bu container'dan yapılan canlı `curl` erişim testleri
>
> Doğrulanamayan her bilgi açıkça **[D] (doğrulanamadı)** diye işaretlendi. Bunlar eğitim verisine dayanıyor ve kullanıcı karar vermeden önce kontrol etmeli.
>
> **Güven notasyonu:**
> - **[Y]:** Birincil kaynak bu oturumda okundu.
> - **[O]:** Orta güven: ikincil kaynak ya da çıkarım.
> - **[D]:** Düşük güven, doğrulanamadı.
>
> Köşeli parantezdeki sayılar `## Kaynaklar` listesine referans veriyor.

## Özet

- **Higgsfield ücretsiz ya da sınırsız bir araç değil. Kredi tabanlı bir "model toplayıcı" (aggregator).** Kendi modelleri var: Soul 2.0, Soul Cinema, Soul ID ile karakter eğitimi, Cinema Studio. Bunların yanında Nano Banana 2/Pro, GPT Image 2.5, FLUX.2, Seedream, Kling 3.0, Seedance 2.5, Veo 3.1, Wan 2.6/2.7 gibi üçüncü taraf modelleri tek hesapta sunuyor [1][3]. Soul karakter eğitimi için en az "Basic" ücretli plan gerekiyor [4]. **Fiyatlar (Higgsfield'in kendi blog/yardım sayfalarından, Eylül 2026):** giriş planı ~9 $/ay (120 kredi), Starter 15 $/ay (200 kredi), Plus 49 $/ay (yıllıkta 39 $; 1.000 kredi), Ultra 129 $/ay (yıllıkta 99 $; 3.000 kredi). Ücretsiz plan kredi içermiyor. Kademe adları 2026'da birkaç kez değişti, üçüncü taraf sitelerde farklı rakamlar dolaşıyor [46][O]. **"Unlimited" yalnızca higgsfield.ai web sitesinde geçerli. MCP, CLI, Canvas ve Supercomputer üzerinden yapılan her üretim, plan ne olursa olsun kredi düşüyor** [47]. Yani Claude'un Higgsfield'i kullanması her zaman kredili (düzeltildi 24.09.2026).
- **Higgsfield'in resmî bir uzak MCP sunucusu var:** `https://mcp.higgsfield.ai/mcp` (HTTP, ilk bağlantıda kimlik doğrulama) [5]. Buna ek olarak resmî bir Claude Code plugin/skill paketi (`higgsfield-ai/skills`) ve MIT lisanslı bir CLI (`higgsfield`) bulunuyor [1][2]. Bizim bulut container'ımızdan `mcp.higgsfield.ai` ve `api.higgsfield.ai` adreslerine **erişilemiyor** (canlı test). Erişim üç yoldan biriyle mümkün: claude.ai connector'ı olarak eklemek, Custom ağ ya da API credential tanımlamak [15].
- **Gerçekten "ücretsiz ve sınırsız" tek seçenek açık ağırlıklı modelleri kullanıcının kendi GPU'sunda çalıştırmak** (ComfyUI ve benzerleri). Bulut tarafındaki her seçenek ya kredi ile ya da hız sınırıyla kısıtlı.
- **ComfyUI artık resmî MCP sunucularına sahip.** Yerel için `comfy-mcp` (PyPI, 40 araç, beta), bulut için `https://cloud.comfy.org/mcp` (OAuth) [16][17]. Bu, Claude'un yerel üretimi doğrudan yönetebilmesi demek.
- **Container'dan doğrudan erişilebilen tek üretim sağlayıcısı Google.** `generativelanguage.googleapis.com` ve `aiplatform.googleapis.com` Trusted ağda açık (canlı test ve [15]). Gemini API'de **Nano Banana 2 Lite (`gemini-3.1-flash-lite-image`) ücretsiz katmana sahip.** Veo Gemini API'de "yalnızca ücretli" [11][12]. Imagen artık hiç kullanılamıyor: Gemini API'de 17.08.2026'da kapatıldı [51] (düzeltildi 24.09.2026). Ücretsiz katmanda gönderilen prompt'lar ve üretilen çıktılar Google tarafından ürün geliştirmede kullanılıyor, insan değerlendiriciler görebiliyor [52].
- **Google Cloud yeni müşterilere 300 $ ücretsiz kredi veriyor** ve sayfa bunun yapay zekâ uygulamaları için kullanılabileceğini söylüyor [10]. Güncel Vertex (yeni adıyla "Gemini Enterprise Agent Platform") fiyatlarıyla 300 $ yaklaşık şunlara yetiyor [9]:
  - ~4.470 adet 1K Nano Banana 2 görseli (0,067 $/adet), Batch modunda ~8.900
  - ya da ~10.000 saniye Veo 3.1 Lite 720p sessiz video (0,03 $/sn)

  Bu, "1 günlük blitz" için en güçlü yasal kaynak. **Ama üç önemli koşul var (düzeltildi 24.09.2026):**
  - Kredi 90 gün geçerli (Google Cloud blogu "91 gün" diyor) [48].
  - **2 Mart 2026'dan sonra açılan hesaplarda 300 $ kredi Gemini API / AI Studio kullanımına harcanamıyor.** Yalnızca Vertex AI (Agent Platform, `aiplatform.googleapis.com`) üzerinden kullanılabiliyor [49]. Yani kredi için AI Studio anahtarı değil, Vertex projesi ve servis hesabı gerekiyor.
  - Ücretsiz deneme hesabı kota artışı isteyemiyor. Yeni projelerde 429 hataları sık görülüyor [50]. Seri üretim için hesabı "Paid"e yükseltmek gerekebilir. Yükseltmede kalan kredi korunuyor, 90 günlük süre içinde harcanmaya devam ediyor [50]. Batch işleri de 24 saate kadar sürebiliyor [53].
- **Google'ın resmî GenMedia MCP sunucuları** Gemini Image (Nano Banana), Veo 3/3.1, Lyria, Gemini TTS/Chirp ve AVTool'u kapsıyor. ADC ve `GOOGLE_CLOUD_PROJECT` istiyor. **Imagen modelleri 30 Haziran 2026 itibarıyla kullanımdan kalkmış (deprecated)** [13]. Vertex'te Imagen 4'ün kapatılma tarihi 30.06.2026, Gemini API'de 17.08.2026. Yerine `gemini-3.1-flash-image` (Nano Banana 2) öneriliyor [51] (düzeltildi 24.09.2026).
- **Lisans tuzakları var:**
  - FLUX.1 [dev], Kontext [dev], FLUX.2 [dev] ve klein 9B ticari olmayan lisanslı. BFL, açık ağırlıkların ticari kullanımı için ayrıca lisans alınmasını istiyor [20][21].
  - Tencent Hunyuan lisansları **AB, Birleşik Krallık ve Güney Kore'de geçersiz**. Çıktıların bu bölgelerde "gösterilmesini" bile yasaklıyor [24]. Steam'de global satacak bir oyun için Hunyuan ailesi elenmeli.
  - Temiz ticari seçenekler: Apache-2.0 lisanslı FLUX.2 klein 4B, Qwen-Image/Edit/Layered, Wan 2.2, Z-Image, FLUX.1 schnell, Chroma; MIT lisanslı HiDream-I1 ve TRELLIS.2 [21][22][23][26][27][28][39].
  - **NoobAI-XL ve onu içeren birleştirilmiş (merge) checkpoint'ler ticari kullanımı yasaklıyor.** Model kartındaki ek madde, "model tarafından üretilen ürünler" dahil her türlü ticarileştirmeyi yasaklıyor [54]. Anime için daha güvenli seçenekler Animagine XL 4.0 ve Illustrious XL v1.0/v1.1. İkisi de CreativeML OpenRAIL++-M lisanslı [55][56] (düzeltildi 24.09.2026).
- **Karakter tutarlılığı artık çözülebilir bir problem.** Kullanılabilecek araçlar:
  - Nano Banana 2/Pro: 14'e kadar referans görsel, çok turlu düzenleme [11]
  - FLUX.2 klein ve Qwen-Image-Edit-2511: çoklu referansla düzenleme [21][22]
  - Karakter başına LoRA eğitimi: ai-toolkit veya kohya [29][30]
  - Higgsfield Soul ID ve Kling "Elements" [2][37]

  Önerilen yol: "karakter bible'ı + referans düzenleme + LoRA + insan rötuşu".
- **Oyun asset'ine özel resmî MCP'ler:** PixelLab (piksel sanatı, 4/8 yönlü karakter, animasyon, tileset) [35], Meshy (3D, rig, animasyon) [36] ve Kling CLI (arka planda MCP kullanıyor) [37].
- **Hukuki durum:**
  - ABD Telif Hakkı Ofisi'nin Ocak 2025 tarihli Part 2 raporuna göre yalnızca prompt ile üretilen çıktı telifle korunmuyor. İnsanın yaptığı seçim, düzenleme ve değişiklikler korunabiliyor [40][D].
  - Steam üretken yapay zekâ kullanımının beyan edilmesini istiyor. 2026'da güncellenen formun odağı oyuncunun tükettiği içerik [41][42].
  - 2025'te Steam'e çıkan oyunların yaklaşık %20'si yapay zekâ kullandığını beyan etti. Clair Obscur, yapay zekâ kullanımı yüzünden Indie Game Awards ödüllerini kaybetti [43][44].
- **Önerilen stratejinin özeti:**
  - **(A) 0 € ile sınırsız:** Kullanıcının yerel GPU'sunda ComfyUI + resmî Comfy MCP + Apache/MIT lisanslı modeller + karakter LoRA'ları.
  - **(B) 24 saatlik blitz:** Yeni Google Cloud hesabının 300 $ kredisiyle container'dan Nano Banana 2/Pro (Batch) ve Veo 3.1 Lite/Fast. Kredi yalnızca **Vertex AI** üzerinden harcanabiliyor, Gemini API anahtarıyla harcanamıyor. Kota için hesabın Paid'e yükseltilmesi gerekebilir [49][50] (düzeltildi 24.09.2026).
  - **(C) Ayda 20–100 $:** Gemini API ücretli katmanı + gerektiğinde Higgsfield veya kiralık GPU.

---

## 1. Higgsfield: 2026'da tam olarak ne?

### 1.1 Ürün ve modeller [Y]

Higgsfield'in resmî model kataloğu [3] iki gruba ayrılıyor.

**Kendi modelleri:**
- Soul 2.0 (editoryal, karakter)
- Soul Cinema, Soul Cast, Soul Location
- Cinema Studio Image 2.5 / Video 3.0
- Marketing Studio, Virality Predictor

**Üçüncü taraf modeller:**

| Tür | Modeller |
|---|---|
| Görsel | Nano Banana, Nano Banana 2, Nano Banana 2 Lite, Nano Banana Pro, GPT Image 1.5/2/2.5, FLUX.2, Flux Kontext Max, Seedream 4.5 / 5.0 Lite, Z-Image, Kling O1 Image, Grok Imagine, Recraft V4.1 |
| Video | Seedance 1.5 Pro / 2.0 / 2.5, Kling 2.6 / 3.0 / 3.0 Turbo, Veo 3 / 3.1 / 3.1 Lite, Gemini Omni Flash, Wan 2.6 / 2.7, Minimax Hailuo, Grok Video 1.5 |
| 3D | Meshy tabanlı "Multi-Image to 3D" |
| Ses | Seed Audio 1.0 |

- CLI'ın kendi açıklaması "40+ model" [1].
- Katalog, anime ve stilize işler için **Flux Kontext Max** ile **Grok Imagine / Grok Video 1.5**'i öneriyor. Karakter ve çizgi film işleri için varsayılan model **Nano Banana 2** [3]. Bu, satıcının kendi değerlendirmesi, bağımsız bir karşılaştırma değil.

### 1.2 Claude'a bağlanma yolları [Y]

| Yol | Nasıl | Kaynak |
|---|---|---|
| Resmî uzak MCP | `https://mcp.higgsfield.ai/mcp` (type: http). Cursor plugin'i ilk bağlantıda kimlik doğrulama istiyor. Claude Code'da: `claude mcp add --transport http higgsfield https://mcp.higgsfield.ai/mcp` | [5]. Komut biçimi Claude Code'un standart sözdizimi. Higgsfield bunu Claude için ayrıca belgelememiş [O] |
| Resmî Claude Code plugin/skills | `/plugin marketplace add higgsfield-ai/skills` → `/plugin install higgsfield@higgsfield`. 9 skill var (generate, soul-id, game-generation…). Skill'ler `higgsfield` CLI'ını sarmalıyor | [2] |
| CLI | `npm i -g @higgsfield/cli` veya `curl … install.sh`. MIT lisanslı, v1.1.26 (2026-09-18). `higgsfield account` kredi bakiyesini, `higgsfield generate cost` iş başına kredi tahminini gösteriyor | [1][7] |
| Bulut API / SDK | Python `higgsfield-client` (Apache-2.0), JS `@higgsfield/client` ve `@higgsfield/cloud-cli`. Kimlik bilgisi `KEY_ID:KEY_SECRET` biçiminde | [6][7] |

**Bizim bulut container'ımız için notlar:**
- `mcp.higgsfield.ai` ve `api.higgsfield.ai` bu oturumda erişilemedi (curl 000).
- Claude Code dokümanına göre, oturumda etkin olan **MCP connector'larının trafiği Anthropic sunucularından geçiyor ve allowlist'e takılmıyor**. **API credential** olarak tanımlanan host'lar da allowlist dışında erişilebilir hâle geliyor. API credential özelliği yalnızca Pro ve Max planlarında var [15].
- Bulut oturumlarında `/plugin` komutu çalışmıyor [14]. Plugin'i repo ayarlarına eklemek ya da skill dosyalarını repoya kopyalamak gerekiyor [O].

### 1.3 Fiyat, ücretsiz katman ve "unlimited"

**Doğrulanabilenler:**
- Sistem kredi tabanlı. İstek `nsfw` ya da `failed` ile sonuçlanırsa kredi iade ediliyor [7].
- Soul eğitimi için "Minimum Basic plan required" hatası dönüyor [4].
- İçerik filtresinde **`ip_detected`** durumu var. Yani telifli karakter veya IP çağrıştıran prompt'lar reddediliyor [4]. Bu bizim için önemli: "Solo Leveling tarzı" gibi prompt'lar hem hukuken hem teknik olarak sorun çıkarır.

**Doğrulama güncellemesi (düzeltildi 24.09.2026):** higgsfield.ai bu container'dan hâlâ engelli. Aşağıdaki bilgiler Higgsfield'in kendi yardım merkezi ve blog sayfalarının arama sonuçlarındaki alıntılarından alındı [46][47][57][58]. Güven: orta–yüksek [O].

| Konu | Doğrulanan durum |
|---|---|
| Planlar (Eylül 2026) | Ücretsiz plan: sınırlı model, kredi yok. Giriş planı ~9 $/ay (120 kredi; sayfaya göre "Basic" ya da "Starter" adıyla geçiyor). Starter 15 $/ay (200 kredi). Plus 49 $/ay, yıllıkta 39 $/ay (1.000 kredi, tüm modeller). Ultra 129 $/ay, yıllıkta 99 $/ay (3.000 kredi, 8 paralel üretim). İşletme planları: Team, Scale, Enterprise [46]. Kademe adları ve rakamlar 2026'da birkaç kez değişti. Üçüncü taraf sitelerde 19/59/129 $ gibi farklı rakamlar var. Kayıttan önce fiyat sayfası kontrol edilmeli |
| Kredilerin ömrü | Abonelik kredileri devretmiyor. Aylık planda her yenilemede, yıllık planda 30 günde bir sıfırlanıyor [46] |
| "Unlimited" ne kapsıyor | Plus ve Ultra, 365 gün boyunca 6 görsel modelde sınırsız kullanım ve Nano Banana 2/Pro için süreli "pencereler" içeriyor. "All Unlimited" ise 20'den fazla modeli kapsayan süreli bir kampanya. **Unlimited yalnızca web uygulamasında geçerli ve her formatta aynı anda 1 üretime izin veriyor** [58] |
| MCP / CLI | **higgsfield.ai dışındaki her üretim (MCP, CLI, Canvas, Supercomputer ve diğer otomasyon araçları) Unlimited durumundan bağımsız olarak her zaman kredi düşüyor** [47] |
| MCP denemesi | 27–31 Temmuz 2026 arasında 24 saatlik bir "Unlimited MCP" denemesi vardı, sona erdi. 22 Ağustos 2026'dan beri yeni kullanıcılar kart doğrulamasıyla **3 günlük MCP denemesi ve yalnızca MCP'de geçerli 100 kredi** alıyor. İptal edilmezse aylık Plus planına dönüşüyor [57] |
| Web denemesi | Yeni kullanıcılara 24 saatlik "ücretsiz sınırsız" web denemesi sunuluyor: 20'den fazla model (Seedance 2.0, Kling 3.0, Nano Banana Pro…), aynı anda 1 üretim. Kart gerekiyor. İptal edilmezse aylık Plus planına dönüşüyor [58]. Yalnızca web'de geçerli, Claude/MCP ile otomatik seri üretimde **kullanılamaz** |
| Ticari kullanım | Higgsfield çıktılar üzerinde hak iddia etmiyor. Çıktının ticari kullanımı plana bağlı değil. Kısıt, çıktılara değil hizmetin kendisinin istismarına yönelik [59] |

**Sonuç:** "Tüm modellerde sınırsız ve ücretsiz" bir plan **yok**. Claude üzerinden Higgsfield her zaman kredili bir araç.

**Değerlendirme:** Higgsfield'in çekici tarafı, en iyi video modellerini (Seedance 2.5, Kling 3.0, Veo 3.1) ve Soul ID karakter kilidini tek hesap ve tek MCP üzerinden sunması. Ama Nano Banana ve Veo gibi Google modelleri, 300 $ krediyle doğrudan Google'dan daha ucuza ve container'dan ek ağ ayarı gerekmeden kullanılabiliyor.

---

## 2. Büyük Karşılaştırma Tablosu

"Container" sütunu, Trusted ağdaki bulut oturumumuzdan erişimi gösteriyor. "Anime" sütunu 1–5 arası editoryal bir değerlendirme; topluluk kanaatine ve satıcı iddialarına dayanıyor, benchmark değil.

| Araç | Tür | Ücretsiz limit | Deneme | Ticari kullanım | Anime | MCP | Container |
|---|---|---|---|---|---|---|---|
| **ComfyUI** (+ resmî `comfy-mcp`) | Yerel UI/motor | Sınırsız (kendi GPU'n) | — | Yazılım GPL-3.0 [19]. Çıktı hakları modelin lisansına bağlı | 5 (anime checkpoint'leriyle) | **Resmî**: `pip install comfy-mcp "comfy-cli>=1.14.0"`, 40 araç [16] | Hayır. Yerel GPU gerekli. `COMFYUI_URL` ile uzak ComfyUI sürülebilir ama Custom ağ ister |
| Forge / InvokeAI | Yerel UI | Sınırsız | — | AGPL-3.0 / Apache-2.0 [30] | 5 | Topluluk | Yerel |
| Illustrious XL / NoobAI-XL / Animagine XL 4 (SDXL anime) | Açık ağırlık | Sınırsız | — | **Modele göre değişiyor (düzeltildi 24.09.2026):** Animagine XL 4.0 ve Illustrious XL v1.0/v1.1 CreativeML OpenRAIL++-M; ticari çıktı serbest, kullanım kısıtları var [55][56]. Illustrious v0.1 Fair AI Public License 1.0-SD. Illustrious v2.0 kartında CreativeML Open RAIL-M yazıyor [56]. **NoobAI-XL: model çıktıları dahil her türlü ticarileştirme yasak** [54]. NoobAI içeren merge'ler bu yasağı devralır [O] | **5** (Danbooru etiketli anime'nin fiilî standardı [O]) | ComfyUI üzerinden | Yerel, ≥8 GB VRAM [O] |
| **FLUX.2 [klein] 4B** | Açık ağırlık, üretim + çoklu referans düzenleme | Sınırsız | — | **Apache-2.0** [21] | 3–4 [O] | ComfyUI | Yerel, ~8 GB VRAM [21] |
| FLUX.1 [dev], Kontext [dev], Krea [dev], FLUX.2 [dev], klein 9B | Açık ağırlık | Sınırsız | — | **Ticari değil.** Çıktıyı ticari kullanmaya izin var ama model kullanımı "non-commercial/non-production". BFL ticari kullanım için lisans istiyor [20][21] | 3–4 | ComfyUI | Yerel. FLUX.2 dev 32B, H100 ya da kuantize 4090 ister [21] |
| FLUX.1 [schnell] | Açık ağırlık | Sınırsız | — | Apache-2.0 [20] | 2–3 | ComfyUI | Yerel |
| **Qwen-Image-2512 / Edit-2511 / Layered** | Açık ağırlık | Sınırsız | — | **Apache-2.0** [22] | 3–4. Edit-2511'de karakter tutarlılığı güçlü [22] | ComfyUI | Yerel, büyük model (kuantize önerilir) [O] |
| **Z-Image / Z-Image-Turbo** | Açık ağırlık | Sınırsız | — | **Apache-2.0** [27] | 3 (fotogerçekçiliğe odaklı) [27] | ComfyUI | Yerel, Turbo 16 GB'a sığıyor [27] |
| HiDream-I1 | Açık ağırlık | Sınırsız | — | MIT [26]. Metin kodlayıcı olarak Llama 3.1 8B Instruct kullanıyor, o bileşen Llama 3.1 Community License'a tabi (düzeltildi 24.09.2026) [26] | 3 | ComfyUI | Yerel, yüksek VRAM [O] |
| Chroma | Açık ağırlık | Sınırsız | — | Eğitim kodu Apache-2.0 [28]. Ağırlıklar Apache-2.0 [O] | 3–4 | ComfyUI | Yerel |
| SD 3.5 | Açık ağırlık | Sınırsız | — | Stability Community License: yıllık geliri 1 M $'ın altındaki şirketlere ücretsiz [D] | 2–3 | ComfyUI | Yerel |
| **Wan 2.2** (TI2V-5B / A14B / Animate-14B / S2V) | Açık video | Sınırsız | — | **Apache-2.0**. "Üretilen içerik üzerinde hak iddia etmiyoruz" [23] | 3–4 | ComfyUI | Yerel. 5B için 24 GB (4090), A14B için resmî olarak 80 GB [23]. Topluluk kuantizasyonuyla daha az [O] |
| LTX-2.x | Açık video | Sınırsız | — | Yıllık geliri 10 M $'ın altındaki kuruluşlara ücretsiz, üstü paralı [25] | 3 | ComfyUI | Yerel |
| HunyuanVideo 1.5 / HunyuanImage 3 / Hunyuan3D | Açık ağırlık | Sınırsız | — | **AB, BK ve G. Kore'de geçersiz. Çıktıyı bu bölgelerde göstermek bile yasak** [24] | 3–4 | ComfyUI | **Kullanılmamalı** |
| **Gemini API: Nano Banana 2 Lite** | Bulut API | **Ücretsiz katman var** (limitler doğrulanamadı) [11]. Ücretsiz katman verisi Google tarafından ürün geliştirmede kullanılıyor [52] | — | Google API şartları. Çıktının sahipliği kullanıcıda [D] | 3–4 | Topluluk MCP'leri (npm'de çok sayıda [38]), kendi scriptimiz | **Evet** (googleapis) |
| **Gemini/Vertex: Nano Banana 2, Pro, Veo 3.1** | Bulut API | Yok. Imagen ve Veo Gemini API'de ücretsiz katmanda yok [12] | **GCP 300 $ kredisi** [10]. 02.03.2026 sonrası açılan hesaplarda yalnızca Vertex üzerinden harcanabiliyor [49] (düzeltildi 24.09.2026) | Ticari kullanıma uygun [O] | 4 (Pro) | **Resmî GenMedia MCP** [13] | **Evet** |
| Hugging Face | Hub, ZeroGPU Spaces, Inference Providers | Ücretsiz hesap: günde 5 dk ZeroGPU, ayda 0,10 $ inference kredisi [31][32] | PRO: günde 40 dk ZeroGPU, ayda 2 $ kredi [31][32] | Space ve model lisansına bağlı | Space'e göre | **Resmî**: `https://huggingface.co/mcp`. claude.ai connector dizininde var [33] | Doğrudan erişim yok. **Connector olarak eklenirse var** [15] |
| Kaggle / Colab / Lightning | Ücretsiz bulut GPU | Kaggle'da haftada ~30 saat GPU [D]. Colab kotası dinamik, garanti yok, bazı üretim arayüzleri ücretsiz katmanda kısıtlı [D] | — | Model lisansına bağlı | 5 (ComfyUI kurulursa) | — | Hayır (tarayıcı veya not defteri) |
| Pollinations | Toplayıcı API | Artık kredili: "Pollen", 1 $ ≈ 1 Pollen. Görev (Quest) tamamlayarak ücretsiz Pollen kazanılıyor [34] | — | Model lisansına bağlı | 3 | **Resmî, hosted**: `gen.pollinations.ai/mcp/pollinations` [34] | Hayır (allowlist). Connector veya credential gerekli |
| Higgsfield | Toplayıcı + kendi modelleri | Ücretsiz plan kredisiz, sınırlı model. Ücretli planlar ~9–129 $/ay. Unlimited yalnızca web'de; MCP/CLI her zaman kredi düşüyor [46][47] | Web: 24 saatlik sınırsız deneme. MCP: 3 gün + 100 MCP kredisi. İkisinde de kart gerekiyor, iptal edilmezse Plus'a dönüşüyor [57][58] | Çıktının ticari kullanımı plana bağlı değil [59] (düzeltildi 24.09.2026) | 4 | **Resmî**: `mcp.higgsfield.ai/mcp` [5] | Hayır. Connector veya credential gerekli |
| Comfy Cloud MCP | Bulut ComfyUI | Aylık 400 kredilik ücretsiz katman. Standard 20 $/ay (~4,4 GPU saati), Creator 35 $, Pro 100 $ [60][O] (düzeltildi 24.09.2026) | [D] | Model lisansına bağlı | 5 | **Resmî**: `cloud.comfy.org/mcp`, OAuth [16][17] | Connector ile |
| fal.ai / Replicate | Toplayıcı API | Kullandıkça öde. Ücretsiz kredi [D] | [D] | Model lisansına bağlı | 4 | Replicate'in resmî npm MCP'si var [38]. fal için topluluk MCP'leri var | Hayır. API credential ile olur |
| **PixelLab** | Piksel sanatı (oyun) | [D] | [D] | [D] | Piksel anime: 4 | **Resmî**: `https://api.pixellab.ai/mcp` [35] | Hayır. Connector veya credential gerekli |
| Scenario / Layer / Ludo / Retro Diffusion | Oyun asset platformu | [D] | [D] | Genelde ticari kullanım odaklı [D] | 3–4 | Scenario: topluluk MCP'si. Layer: resmî SDK [38] | Hayır |
| Meshy / TRELLIS.2 | 3D | Meshy [D]. TRELLIS.2 yerel ve MIT [39] | — | TRELLIS.2 MIT | Anime kahraman karakteri için yetersiz [O] | **Meshy resmî MCP** [36]. API anahtarı için Pro veya üstü plan gerekiyor [36] (düzeltildi 24.09.2026) | Meshy: credential |
| Kling / Runway / Hailuo / Vidu / Pika / Seedance (Dreamina) | Video SaaS | Günlük veya tek seferlik ücretsiz kredi. Ücretsiz planlarda filigran ve ticari kısıt olabilir [D] | Var [D] | Genelde ücretli planlarda [D] | 4 (Kling, Seedance) | Kling resmî CLI'ı arka uçta MCP kullanıyor [37] | Hayır |
| Leonardo / Tensor.art / SeaArt / PixAI / Krea / Ideogram | Görsel SaaS | Günlük token veya kredi [D] | — | Plana ve modele göre değişiyor [D] | PixAI ve Tensor.art anime'de güçlü [O] | Topluluk | Hayır |
| Bing Image Creator / ChatGPT / Meta AI / Grok Imagine | Tüketici uygulaması | Günlük sınırlı [D] | — | Bing: kişisel ve ticari olmayan kullanım maddesi [D]. OpenAI çıktı haklarını kullanıcıya devrediyor [D] | 3–4 | Yok | Hayır (manuel) |
| Midjourney (Niji) | SaaS | Ücretsiz katman yok [D] | — | Ücretli planda ticari kullanım var [D] | **5** (Niji) [O] | Yok (resmî API yok [D]) | Manuel |

---

## 3. Açık Ağırlıklı Yerel Üretim: Detaylar

### 3.1 Donanım eşikleri

Resmî `comfy-mcp` dokümanındaki yönlendirme tablosu [16]:

| VRAM | Öneri |
|---|---|
| ≥24 GB | Yerel üretim iyi bir varsayılan |
| 8 GB ile 24 GB arası | Görsel üretimi sorunsuz. Video yavaş ya da imkânsız |
| <8 GB | Yerel difüzyon çalıştırılmamalı. Partner veya bulut kullanılmalı |
| Apple Silicon | 32 GB'ın üstünde görsel üretimi olur. Video önerilmiyor |

Model bazında:
- FLUX.2 klein 4B yaklaşık 8 GB'a sığıyor (RTX 3090/4070) [21].
- Z-Image-Turbo 16 GB'a sığıyor [27].
- Wan 2.2 TI2V-5B, offload ile 24 GB'ta (4090) 720p/24fps üretiyor [23].

### 3.2 Anime için model seçimi

- **Karakter ve illüstrasyon:** SDXL tabanlı Illustrious ve NoobAI türevleri, topluluğun anime standardı [O]. Lisansları model kartında ayrı ayrı kontrol edilmeli. **Doğrulanan lisanslar (düzeltildi 24.09.2026):**
  - **NoobAI-XL (tüm sürümler):** Fair AI Public License 1.0-SD'ye ek bir madde konmuş: "model, türev modeller veya **model tarafından üretilen ürünler** dahil her türlü ticarileştirmeyi yasaklıyoruz" [54]. Ticari bir oyunda **kullanılamaz**. Civitai'deki pek çok "Illustrious" merge'i NoobAI içeriyor. Soy ağacı (merge tarifi) kontrol edilmeli [O].
  - **Illustrious XL v1.0 / v1.1:** CreativeML OpenRAIL++-M. Ticari çıktı serbest, kullanım kısıtları (yasa dışı, zararlı içerik vb.) var [56].
  - **Illustrious XL v0.1:** Fair AI Public License 1.0-SD. Çıktı serbest, ama türev model dağıtılırsa açık kaynak yapılmalı [56].
  - **Illustrious XL v2.0:** Model kartında CreativeML Open RAIL-M yazıyor, topluluk bu konuda soru soruyor [56][O].
  - **Animagine XL 4.0:** Stability'nin CreativeML OpenRAIL++-M lisansını değiştirmeden kullanıyor. Ticari kullanım serbest [55].
  - **Pony Diffusion V6 XL:** Değiştirilmiş Fair AI Public License 1.0-SD. Çıktıların ticari kullanımı serbest ama modeli para kazanan bir üretim servisinde çalıştırmak yasak [61][O].
  - Oyun asset'i için önerilen taban modeller: **Animagine XL 4.0** veya **Illustrious XL v1.0/v1.1**, ve bunlardan türetilen, NoobAI içermeyen checkpoint ve LoRA'lar.
- **Referansla düzenleme ve tutarlılık:**
  - FLUX.2 klein 4B (Apache): çoklu referans düzenleme [21]
  - Qwen-Image-Edit-2511 (Apache): "Multiple Image Support and Improved Consistency" [22]
- **Katmanlara ayırma:** Qwen-Image-Layered (Aralık 2025) görseli katmanlara ayırıyor [22]. Live2D veya Spine rig'i için parça ayırmada faydalı olabilir [O].
- **Kısa sinematik ve ara sahne:** Wan 2.2 (Apache). Animate-14B, karakter animasyonu ve karakter değiştirme için [23].
- **LoRA eğitimi:**
  - ai-toolkit (MIT): FLUX.2 klein base, Qwen-Image/Edit, Z-Image, Wan 2.x, SDXL, Chroma ve HiDream'i destekliyor. Örnek config'ler "24gb" sınıfı [29].
  - kohya sd-scripts (Apache-2.0) [30].

### 3.3 Claude'un yerel üretimi yönetmesi

- Resmî `comfy-mcp` şunları yapabiliyor [16]:
  - Workflow JSON'u çalıştırma
  - İş izleme
  - Kurulu node, model ve şablonları arama
  - Varyant üretme
  - ComfyUI'ı başlatma ve durdurma
- Kredi harcayan partner modelleri bilinçli olarak bir onay kapısının arkasında tutuluyor [16].
- Topluluk sunucusu `artokun/comfyui-mcp` (763 yıldız) resmî araç çıktığı için bırakıldı. Repo 2026-10-09'da arşivlenecek [18].
- **Pratik sonuç:** Yerel GPU'lu bir PC'de **yerel Claude Code** çalıştırılır ve `comfy-mcp` eklenir. Bulut oturumu ise workflow JSON'larını, prompt manifest'lerini ve stil bible'ını repoda üretir.

---

## 4. Ücretsiz Bulut GPU

| Kaynak | Kota | Not | Güven |
|---|---|---|---|
| HF ZeroGPU | Anonim 2 dk/gün, ücretsiz hesap 5 dk/gün, PRO 40 dk/gün. RTX Pro 6000 Blackwell (48/96 GB) | Ücretsiz hesap en fazla 2 ZeroGPU Space barındırabiliyor. Hesabın 30 günden eski olması gerekiyor | [Y] [32] |
| HF Inference Providers | Ücretsiz 0,10 $/ay, PRO 2 $/ay | Sonrası kullandıkça öde | [Y] [31] |
| Kaggle | Haftada ~30 saat GPU, oturum başına ~12 saat | Kullanım şartlarını kontrol et | [D] |
| Colab ücretsiz | Dinamik T4, garanti yok | 2023'ten beri bazı SD arayüzleri ücretsiz katmanda kısıtlı | [D] |
| Lightning AI | Aylık ücretsiz kredi | Miktar doğrulanamadı | [D] |

**Sonuç:** Bu kotalar deneme ve LoRA eğitimi için işe yarar. Yüzlerce asset'lik seri üretim için yetersiz ve öngörülemez.

---

## 5. Google Yolu: Container'dan Doğrudan Erişilebilen Tek Sağlayıcı

### 5.1 Doğrulanmış fiyatlar [Y] [9]

Kaynak: Google Cloud fiyat sayfası (Vertex AI artık "Gemini Enterprise Agent Platform" adına yönlendiriyor).

| Model | Birim fiyat (Standart) | Flex/Batch |
|---|---|---|
| Nano Banana 2 Lite (`gemini-3.1-flash-lite-image`) | 1K çıktı 0,034 $ | Görsel çıktısı yarı fiyat (15 $/M token) |
| **Nano Banana 2** (`gemini-3.1-flash-image`) | 512px 0,045 $ · 1K 0,067 $ · 2K 0,101 $ · 4K 0,15 $ | Yarı fiyat (30 $/M) |
| **Nano Banana Pro** (`gemini-3-pro-image`; Gemini API'de `gemini-3-pro-image-preview` [11]) | 1K/2K 0,134 $ · 4K 0,24 $ | Yarı fiyat (60 $/M) |
| Imagen 4 Fast / 4 / 4 Ultra | 0,02 / 0,04 / 0,06 $ | **Kapatıldı:** Vertex'te 30.06.2026, Gemini API'de 17.08.2026 [13][51]. Fiyat sayfasında hâlâ listeleniyor (düzeltildi 24.09.2026) |
| Veo 3.1 Lite | 720p sessiz 0,03 $, sesli 0,05 $. 1080p sessiz 0,05 $, sesli 0,08 $ | — |
| Veo 3.1 Fast | 720p sessiz 0,08 $, sesli 0,10 $. 1080p sesli 0,12 $ | — |
| Veo 3.1 | 720p/1080p sesli 0,40 $, sessiz 0,20 $. 4K sesli 0,60 $, sessiz 0,40 $ | — |
| Lyria 3 / 3 Pro | 30 sn klip 0,04 $ / tam şarkı 0,08 $ | — |

Veo için sayfadaki birim "1 count". Bunun saniye başı fiyat olduğu anlaşılıyor [O].

Fiyatlar 24.09.2026'da sayfadan yeniden okundu, hepsi doğru [9]. Sayfada ayrıca "seçili modellerde, net harcamanın %50'si kredi olarak iade edilen promosyon fiyatı" notu var. Görsel başı rakamlar yalnızca çıktı token'larını kapsıyor. Her girdi (referans) görseli NB2'de 1.120 token (~0,00056 $), Pro'da 560 token ekliyor. Bu, 14 referanslı bir istekte bile görsel başına 1 sentin altında kalıyor (düzeltildi 24.09.2026).

### 5.2 Ücretsiz katman ve deneme

- **Gemini API ücretsiz katmanı:**
  - Nano Banana 2 Lite "free tier" içeriyor [11].
  - Imagen için "Image generation is a paid-only feature", Veo için "paid only feature" yazıyor [12].
  - Ücretsiz katmanın dakikalık ve günlük görsel limitleri doğrulanamadı [D].
- **Nano Banana yetenekleri:**
  - 2 ve Pro modelleri 14'e kadar girdi görselini birleştiriyor (6'sı yüksek sadakatle). Lite 3 görsel alıyor.
  - `previous_interaction_id` ile karakter ve stil tutarlılığı korunarak çok turlu düzenleme yapılabiliyor [11].
- **Google Cloud 300 $ kredisi:**
  - "New customers get $300 in free credit… Use your $300 free credit to build AI apps" [10].
  - Tam hesap aktive edilmeden ücret kesilmiyor [10].
  - Kredinin süresi bu sayfada yazmıyor. Genelde 90 gün olarak biliniyor [D]. **Doğrulandı: 90 gün. Google Cloud blogu "91 gün" diyor** [48] (düzeltildi 24.09.2026).
  - Yeni projelerdeki varsayılan kota ve dakikalık sınırlar seri üretimi yavaşlatabilir [D]. **Doğrulandı:** Ücretsiz deneme faturalandırma hesabı kota artışı isteyemiyor, GPU ekleyemiyor, Marketplace'i ve üçüncü taraf (partner) üretken modelleri kullanamıyor. Forumlarda deneme hesabında Gemini isteklerinin hızla kısıldığı ve yeni projelerde `gemini-3.1-flash-image` için 429 hatası alındığı bildiriliyor [50]. Hesap "Paid"e yükseltilince kısıtlar kalkıyor, kalan kredi 90 günlük süre içinde önce harcanıyor [50] (düzeltildi 24.09.2026).
  - **Kapsam (düzeltildi 24.09.2026):** 2 Mart 2026'dan sonra açılan hesaplarda deneme kredisi **Gemini API / AI Studio kullanımına harcanamıyor**. Google Cloud konsolundaki diğer ürünlere, yani Vertex AI'daki Gemini, Nano Banana ve Veo'ya harcanabiliyor [49]. Ayrıca 23 Mart 2026'dan beri yeni AI Studio kullanıcılarından ücretli katman için önceden ödeme (Prepay) istenebiliyor [49][O].
  - **Vertex AI Express Mode** (@gmail.com hesaplarına 90 gün, faturalandırmasız) Nano Banana, Veo ve Lyria'yı ücretsiz kapsamıyor [62][O].
- **300 $ ile ne kadar üretilir (yalnızca çıktı maliyeti):**
  - NB2 1K: ~4.470 görsel, Batch'te ~8.900
  - NB Pro 2K: ~2.240
  - Veo 3.1 Lite 720p sessiz: ~10.000 sn (~166 dk)
  - Veo 3.1 Fast 1080p sesli: ~2.500 sn

  Aritmetik 24.09.2026 fiyatlarıyla doğrulandı. Ancak bu rakamlar yalnızca **Vertex AI** üzerinden ulaşılabilir. Batch işleri 24 saate kadar sürebiliyor [53]. Deneme hesabının kota sınırları nedeniyle 24 saat içinde gerçekçi hacim çok daha düşük olabilir [50] (düzeltildi 24.09.2026).

### 5.3 Bağlantı

- **Resmî GenMedia MCP** [13]:
  - Go binary'leri: `mcp-nanobanana-go`, `mcp-gemini-go`, `mcp-veo-go`, `mcp-lyria-go`, `mcp-chirp3-go`, `mcp-avtool-go`, `mcp-omni-go`. Kurulum betiği GitHub Releases'ten indiriyor.
  - Kimlik doğrulama ADC ile yapılıyor. `GOOGLE_CLOUD_PROJECT` zorunlu, `GENMEDIA_BUCKET` isteğe bağlı.
- **Gemini API anahtarıyla daha basit yol:** Claude, `google-genai` SDK'sıyla bir batch betiği yazar. Anahtar, ortamın **API credential**'ına eklenir: host `generativelanguage.googleapis.com`, header `x-goog-api-key`, prefix yok. Böylece anahtar sandbox'ta görünmez olur [15].
  - **Uyarı (düzeltildi 24.09.2026):** Bu yol 300 $ deneme kredisini **tüketmez** (2 Mart 2026 sonrası açılan hesaplar) [49]. Yalnızca ücretsiz katmanı (NB2 Lite) ya da ücretli/Prepay katmanı kullanır. 300 $ kredi için Vertex yolu gerekir: `google-genai` SDK'sı `vertexai=True` ile, `aiplatform.googleapis.com` üzerinden servis hesabı veya ADC kullanır. Bu, GenMedia MCP'nin kullandığı yol [13]. Servis hesabı anahtarının container'a nasıl güvenle verileceği ayrıca planlanmalı [O].
- Container'dan `generativelanguage.googleapis.com` ve `oauth2.googleapis.com` adresleri Google'ın kendi hata JSON'unu döndürdü, yani erişilebilir durumdalar (canlı test).

---

## 6. Oyun Asset'ine Özel Araçlar

- **PixelLab (resmî MCP)** [35]:
  - Adres: `https://api.pixellab.ai/mcp`
  - Araçlar: `create_character` (4/8 yön), `animate_character` (yürüme, koşma, bekleme), `create_tileset` (Wang tileset), `create_isometric_tile`
  - Claude Code, Godot ve Unity akışlarını açıkça hedefliyor.
  - Yalnızca **piksel sanatı** yönü seçilirse ideal. Yüksek çözünürlüklü anime stiline uygun değil.
- **Meshy (resmî MCP, 24 araç)** [36]: Text/image-to-3D, retexture, remesh, **rig ve animate**, 8K doku. 3D yol seçilirse prop ve düşman için uygun. Anime kahraman karakteri için VRoid veya elle modelleme gibi insan işi gerekecek [O].
- **Kling CLI** [37]: Arka uçta MCP araçlarını kullanıyor. Tekrar kullanılabilir karakter "Elements" ve motion control sunuyor. Filigransız URL'ler ayrıca dönüyor.
- **Layer.ai:** Oyun stüdyolarına yönelik resmî JS SDK'sı var (2026-09) [38]. Fiyat [D].
- **Scenario:** Yalnızca topluluk MCP'si var [38]. Özel model eğitimi sunuyor, fiyat [D].
- **Ludo.ai ve Retro Diffusion:** [D].
- **Higgsfield `game-generation` skill'i:** README'de "sprite, doku, rig'li 3D ve ses" üretimi olarak listeleniyor [2]. Ancak klasör ana dalda görünmüyor (404) [O].

---

## 7. Tutarlılık Problemi: Karakteri Yüzlerce Asset Boyunca Aynı Tutmak

Önerilen boru hattı:

1. **Stil bible'ı.** Palet (HEX), çizgi kalınlığı, gölge kuralı (cel shading, 2 ton), göz ve saç çizim kuralları, 10–20 "altın referans". Repoda `art/bible/` altında tutulur.
2. **Karakter ana sayfası.** Turnaround (ön, yan, arka, 3/4), ifade sayfası, kıyafet ve renk etiketleri.
   - Bulut: Nano Banana Pro. Çoklu referans ve çok turlu düzenleme [11].
   - Yerel: Qwen-Image-Edit-2511 veya FLUX.2 klein 4B [21][22].
3. **Karakter başına LoRA.** Elle seçilmiş 20–40 görselle eğitilir: Illustrious/NoobAI (SDXL) ya da FLUX.2 klein 4B base [29][30]. Bundan sonra poz, sahne ve ifade varyantları LoRA ile, ControlNet (poz, derinlik, çizgi) ve IP-Adapter ile üretilir [O].
4. **Kapalı SaaS alternatifi.** Higgsfield Soul ID. Eğitim yaklaşık 30 dakika sürüyor ve bir `reference_id` döndürüyor [2][4]. Kling Elements da bir seçenek [37]. Soul ID fotogerçekçi yüz odaklı. Anime karakterlerindeki başarısı doğrulanamadı [D].
5. **Otomatik kalite kontrol.** Claude görselleri okuyup bible'a uyumu puanlar. Her asset için bir manifest satırı tutulur: model, lisans, seed, prompt, referanslar, insan düzenlemesi. Bu manifest hem Steam beyanı hem de telif savunması (insan katkısının kaydı) için kanıt olur.
6. **İnsan rötuşu (zorunlu).** Çizgi temizliği, palet sabitleme, el ve parmak düzeltmeleri. Kahraman karakterlerde ve key art'ta profesyonel bir illüstratörle çalışılması önerilir.

---

## 8. Hukuk, Platform ve Oyuncu Algısı

- **ABD Telif Hakkı Ofisi, Part 2 (29.01.2025)** [40][D, erişilemedi]. Tarih ve aşağıdaki özet, hukuk bürosu özetleriyle doğrulandı [65] (düzeltildi 24.09.2026):
  - Yalnızca prompt yazmak yeterli insan yaratıcılığı sayılmıyor.
  - İnsan tarafından yapılmış ifade unsurları, yaratıcı seçim, düzenleme ve değişiklik korunabiliyor.
  - Değerlendirme vaka bazında yapılıyor.
  - **Sonuç:** Saf yapay zekâ çıktısı başkaları tarafından kopyalanabilir. Oyunun kodu, anlatısı, seçim ve düzenlemesi ile elle rötuşlanmış sanat eserleri ise korunabilir.
- **Steam** [41][42]:
  - Ocak 2024'ten beri önceden üretilmiş ve canlı üretilen yapay zekâ içeriğinin beyan edilmesi gerekiyor. Canlı üretimde koruma önlemleri (guardrail) isteniyor.
  - 2026 güncellemesiyle formun odağı "oyuncunun tükettiği içerik". Kod yardımcısı gibi arka plan verimlilik araçları kapsam dışı. Güncelleme Ocak 2026 tarihli. Oyunla gelen ya da mağaza sayfasında görünen yapay zekâ sanatı, sesi, metni ve pazarlama materyali beyan kapsamında [64] (doğrulandı 24.09.2026).
- **AB Yapay Zekâ Yasası, Madde 50** [45][D]: Şeffaflık yükümlülükleri 2 Ağustos 2026'dan itibaren uygulanıyor. Açıkça sanatsal ve kurgusal içerikte ifşa yükümlülüğü hafifletilmiş. **Doğrulandı (düzeltildi 24.09.2026):** Madde 50, Digital Omnibus ertelemesinin dışında kaldı ve 2 Ağustos 2026'da yürürlüğe girdi. Komisyon rehberi 20 Temmuz 2026'da yayımlandı. Mayıs 2026 geçici uzlaşmasına göre, o tarihten önce piyasadaki üretken yapay zekâ sistemlerine 50(2) makine-okunur işaretleme için 2 Aralık 2026'ya kadar süre tanındı. Bu yükümlülük model sağlayıcısına ait, oyun geliştiricisine değil [63][O].
- **Model lisansları:**
  - Hunyuan'ın bölge maddesi [24] ve FLUX [dev] ailesinin ticari olmayan lisansı [20][21] en büyük tuzaklar.
  - FLUX.1 [dev] lisansı "Output… any purpose (including commercial)" diyor ama modelin kendisini "non-commercial and non-production" kullanıma sınırlıyor. BFL, açık ağırlıkları ticari kullanan herkesin lisans almasını şart koşuyor [20]. Riskli gri alan, kullanılmamalı.
- **Oyuncu tepkisi:**
  - Clair Obscur, Indie Game Awards ödüllerini yapay zekâ kullanımı nedeniyle kaybetti (Aralık 2025) [44].
  - 2025 Steam çıkışlarının ~%20'si beyan içeriyor [43].
  - Beyanlı oyunların daha az inceleme aldığı iddia ediliyor, ama nedensellik kanıtlanmadı [43].
  - Call of Duty: Black Ops 6/7'deki yapay zekâ sanatı ve Crunchyroll'un yapay zekâ altyazıları da tepki çekti [D].
  - 2026'ya ait anime oyunu özelinde doğrulanmış bir vaka bulunamadı (arama kotası doldu).
- **Anime topluluğu** sanatçı merkezli. "AI slop" algısı özellikle karakter sanatında ağır cezalandırılıyor [O].

---

## 9. Önerilen Üç Stack

### (A) 0 € bütçe, gerçekten sınırsız

| Katman | Seçim |
|---|---|
| Donanım | Kullanıcının PC'sinde NVIDIA GPU. Görsel için ≥8 GB, rahat LoRA için 12–16 GB, video için 24 GB [16][21][23] |
| Motor | ComfyUI (GPL-3.0) + resmî `comfy-mcp` [16][19] |
| Modeller | Anime checkpoint'i: **Animagine XL 4.0 veya Illustrious XL v1.0/v1.1 (OpenRAIL++-M) tabanlı ve NoobAI içermeyen** bir model (lisansı tek tek kontrol edilmeli) [54][55][56] (düzeltildi 24.09.2026). FLUX.2 klein 4B (Apache), Qwen-Image-Edit-2511 (Apache, kuantize), Wan 2.2 TI2V-5B (Apache). **Hunyuan, FLUX [dev] ve NoobAI-XL kullanılmayacak** |
| LoRA | ai-toolkit (MIT) veya kohya (Apache) [29][30] |
| Claude bağlantısı | **Yerel Claude Code** + `claude mcp add comfy-mcp …` (stdio). Bulut oturumu repoda workflow, prompt manifest'i ve bible üretir. Yerel oturum bunları çalıştırır |
| GPU yoksa | Gemini API ücretsiz katmanında Nano Banana 2 Lite (sınırlı; container'dan erişilebilir) + HF ZeroGPU (günde 5 dk) + Kaggle [D]. Bu durumda "sınırsız" gerçek değil |
| Kullanıcının kurulumu | ComfyUI kurulumu, model indirme (HF/Civitai ev ağından), `pip install comfy-mcp comfy-cli`, yerel Claude Code |

### (B) "1 günlük blitz": 24 saatte deneme kredisiyle seri üretim

Ön koşullar:
- Yeni bir Google Cloud hesabı (300 $ kredi [10]) ve bir proje.
- Vertex API'nin etkinleştirilmesi.
- Bir servis hesabı veya API anahtarı.
- API credential'ı ya da ortam değişkeni olarak eklenmesi [15].
- **Düzeltme (24.09.2026):** Kredi yalnızca Vertex AI üzerinden harcanabiliyor. AI Studio/Gemini API anahtarı krediyi tüketmez [49]. Tüm üretim `aiplatform.googleapis.com` ve Vertex kimlik bilgileriyle yapılmalı.
- **Düzeltme (24.09.2026):** Deneme hesabı kota artışı isteyemiyor [50]. Blitz'ten önce hesap "Paid"e yükseltilmeli (kalan kredi önce harcanır) ve NB2/Veo kotaları kontrol edilmeli. Yükseltme sonrası krediyi aşan kullanım karttan ödenir, bu yüzden bütçe alarmı kurulmalı.

İsteğe bağlı:
- O ay için tek bir Higgsfield paketi (Seedance 2.5 veya Kling 3.0 sinematikleri için; connector ile).
- HF PRO (günde 40 dk ZeroGPU).

| Saat | Adım |
|---|---|
| 0–2 | Hesap ve kota kontrolü. Claude `gen_batch.py` (google-genai, Batch API) ve manifest şemasını yazar. GenMedia MCP kurulur (isteğe bağlı) [13] |
| 2–5 | Stil bible'ı: 20 stil keşfi NB2 1K ile yapılır, 1 stil seçilir. Ana karakterler (6–8) için Nano Banana Pro 2K ile turnaround ve ifade sayfaları üretilir |
| 5–12 | **Batch ile seri üretim:** NB2, tutarlılık için 14 referansa kadar kullanır. NPC portreleri, ifade varyantları, 60–100 arka plan (şehir, Gate, zindan katları), eşya ve yetenek ikonları (512px). Tahmini maliyet ~2.000–4.000 görsel × ~0,034 $ ≈ 70–135 $. Batch işleri 24 saate kadar sürebildiği için ilk batch 0–2. saatte gönderilmeli [53] (düzeltildi 24.09.2026) |
| 12–16 | UI parçaları, kart çerçeveleri, "Sistem penceresi" motifleri. Görsel içinde metin gereken yerlerde Nano Banana Pro kullanılır, karmaşık tipografide güçlü [11] |
| 16–20 | Veo 3.1 Lite/Fast ile 20–40 kısa ara sahne ve trailer çekimi. Örnek: 40 × 8 sn × 0,05–0,12 $ ≈ 16–40 $ |
| 20–24 | Kalite kontrol: Claude'un görsel puanlaması, arka plan kaldırma (rembg vb.), manifest ve lisans kaydı, Steam beyan notu. Kalan kredi ertesi günler için saklanır |

**Uyarılar:**
- 300 $ genelde 90 gün geçerli [D]. **Doğrulandı: 90 gün (Google blogu: 91 gün)** [48] (düzeltildi 24.09.2026). Gerçekte "1 günlük sınırsız" bir teklif değil, cömert bir deneme.
- Higgsfield'in 24 saatlik "sınırsız" web denemesi yalnızca web arayüzünde geçerli ve aynı anda 1 üretime izin veriyor. MCP/CLI üretimleri her zaman kredi düşüyor [47][58]. Bu yüzden Claude'un yöneteceği bir blitz'te kullanılamaz, en fazla elle birkaç sinematik denemesi için işe yarar (düzeltildi 24.09.2026).
- Yeni hesabın dakikalık kotaları seri üretimi yavaşlatabilir.
- Sahte veya çoklu hesapla deneme kredisi toplamak kullanım şartlarına aykırıdır ve önerilmez.

### (C) Küçük bütçe: ayda 20–100 $

| Seçenek | İçerik | Claude bağlantısı |
|---|---|---|
| C1 (bulut, GPU yok) | Gemini API ücretli katmanı: NB2 Batch ~0,034 $/1K. 30 $ ile ~900 görsel. Veo 3.1 Lite. İsteğe bağlı HF PRO. Yeni AI Studio hesaplarında ücretli katman için önceden ödeme (Prepay) gerekebilir [49][O] (düzeltildi 24.09.2026) | Container'dan doğrudan (googleapis). API credential |
| C2 (kiralık GPU) | Saatlik kiralanan 24 GB GPU üzerinde ComfyUI ve kendi LoRA'larımız. Saatlik fiyat [D] | `comfy-mcp` + `COMFYUI_URL` [16]. Bulut oturumu için Custom ağ gerekir. Alternatif: yerel Claude Code |
| C3 (Higgsfield) | Basic veya üstü plan (Soul ID ve 40+ model) [4]. Seedance 2.5 dahil tüm modeller için Plus (49 $/ay, 1.000 kredi) gerekiyor [O]. MCP üzerinden her üretim kredi düşüyor [46][47] (düzeltildi 24.09.2026) | claude.ai custom connector (`mcp.higgsfield.ai/mcp`) veya yerel `claude mcp add` [5][15] |

---

## Oyunumuz İçin Çıkarımlar

1. **Önce asset stratejisini seç, sonra aracı.** Solo geliştirici ve yapay zekâ için en verimli görsel dil:
   - **2D anime:** Live2D veya Spine ile rig'lenmiş karakter portreleri
   - Yapay zekâ ile üretilip elle rötuşlanan arka planlar
   - Sprite veya düşük poligonlu savaş görselleri
   - Kısa video ara sahneleri

   Tam 3D anime kahraman modelleri (Genshin sınıfı) bugünkü yapay zekâ 3D araçlarıyla güvenilir kalitede üretilemiyor [O]. Motor seçimi (Godot 2D, Unity 2D/3D) bu karardan etkilenmeli.
2. **Karar verme akışı:**
   - Kullanıcının GPU'su öğrenilmeli. Model ve VRAM'i paylaşması yeterli.
   - ≥12 GB ise **Stack A** ana üretim hattı olur. Google kredisi yalnızca Nano Banana Pro'nun güçlü olduğu işlerde kullanılır: karakter sayfası, metinli UI ve Veo sinematikleri.
   - GPU yoksa **Stack B** ile başlanır, ardından **C1**'e geçilir.
3. **Container'dan hemen yapılabilecekler:** Kullanıcı Gemini API anahtarını ortamın API credential'ına eklerse (host `generativelanguage.googleapis.com`) Claude bu oturumda **ek ağ ayarı olmadan** Nano Banana üretimi yapabilir. Not: Bu yol 300 $ GCP deneme kredisini kullanmaz. Krediyle üretim için Vertex kimlik bilgisi (`aiplatform.googleapis.com`) gerekir [49] (düzeltildi 24.09.2026). Higgsfield, PixelLab, Hugging Face ve Comfy Cloud için ise ya claude.ai connector'ı ya da Custom ağ veya credential gerekiyor [15].
4. **Higgsfield'i "zorunlu" değil "opsiyonel sinematik aracı" olarak konumla.** Seedance 2.5 ve Kling 3.0 ile anime trailer'ı gibi işlerde değerli. Ama ücretsiz veya sınırsız değil, fiyatı da doğrulanmadı. **Güncelleme (düzeltildi 24.09.2026):** Fiyatlar ~9–129 $/ay. Unlimited yalnızca web'de geçerli, Claude/MCP ile yapılan her üretim kredi düşüyor [46][47]. Yeni kullanıcıya 3 günlük MCP denemesi ve 100 MCP kredisi veriliyor. İptal edilmezse Plus'a (49 $/ay) dönüşüyor [57].
5. **Lisans beyaz listesi (repoda `docs/legal/model-whitelist.md` olarak tutulmalı):**
   - **İzinli:** FLUX.2 klein 4B, FLUX.1 schnell, Qwen-Image ailesi, Z-Image, Wan 2.2, HiDream-I1, Chroma, TRELLIS.2, Google (ücretli veya kredili), lisansı kontrol edilmiş SDXL anime checkpoint'leri (Animagine XL 4.0, Illustrious XL v1.0/v1.1 ve NoobAI içermeyen türevleri) [55][56]
   - **Yasaklı:** Tencent Hunyuan ailesi, FLUX [dev] ailesi (lisans alınmadan), **NoobAI-XL ve onu içeren merge'ler** [54] (düzeltildi 24.09.2026), telifli IP içeren prompt ve LoRA'lar
6. **IP hijyeni.** Prompt'larda "Solo Leveling", "DanMachi" ya da sanatçı adları yasak. Higgsfield'in `ip_detected` filtresi [4] zaten bu yönde çalışıyor. Özgün bir görsel dil kurulmalı.
7. **Şeffaflık ve itibar.**
   - Steam formu dürüstçe doldurulmalı [41][42].
   - Mağaza sayfasında "karakter tasarımları insan elinden geçti" gibi doğru bir ifade kullanılmalı.
   - Yapay zekâ hariç tutan ödüllere başvurulmamalı [44].
   - Ana key art ve ana kahraman için insan illüstratöre bütçe ayrılmalı. En görünür 5–10 görselde yapay zekâ izi bırakılmamalı.
8. **Manifest zorunlu.** Her asset için model, lisans, seed, referanslar ve insan düzenlemesi kaydı tutulmalı. Telif savunmasının [40] ve Madde 50 uyumunun [45] temeli bu kayıt.
9. **Seslendirme ve müzik ayrı raporun konusu.** Yine de not: Google tarafında Lyria 3 (30 sn klip 0,04 $) ve Gemini TTS/Chirp aynı GenMedia MCP'de, container'dan erişilebilir [9][13].

---

## Belirsizlikler ve Riskler

- **Higgsfield'in fiyatı, ücretsiz katmanı, "unlimited" koşulları ve ticari kullanım şartları doğrulanamadı** [8]. Kayıt olmadan önce kullanıcı fiyat sayfasını ve kullanım şartlarını okumalı. CLI'da `higgsfield account status` ve `generate cost` ile gerçek maliyet görülebilir [1][4]. **Güncelleme (düzeltildi 24.09.2026):** Higgsfield'in kendi sayfalarının arama alıntılarıyla büyük ölçüde doğrulandı (bkz. §1.3) [46][47][57][58][59]. Rakamlar sık değiştiği için kayıttan önce yine de kontrol edilmeli.
- **Gemini API ücretsiz katmanının limitleri** ve ücretsiz katmanda verilerin model geliştirmede kullanılıp kullanılmadığı doğrulanamadı [D]. Gizli konsept sanatı için ücretli katman daha güvenli olabilir. **Güncelleme (düzeltildi 24.09.2026):** Veri kullanımı doğrulandı. Ücretsiz katmanda içerik ürün geliştirmede kullanılıyor ve insan değerlendiriciler görebiliyor [52]. Gizli konsept sanatı için ücretli katman ya da Vertex kullanılmalı. Görsel başı ücretsiz limitler hâlâ doğrulanamadı.
- **GCP 300 $ kredisinin süresi ve kapsamı** doğrulanamadı: 90 gün, bazı servislerde kısıtlama ve yeni hesap kotaları [D]. **Güncelleme (düzeltildi 24.09.2026):** 90 gün doğrulandı [48]. 2 Mart 2026 sonrası hesaplarda Gemini API/AI Studio'ya harcanamıyor, yalnızca Vertex'e harcanıyor [49]. Deneme hesabı kota artışı isteyemiyor [50].
- **Anime checkpoint lisansları** (Illustrious, NoobAI, Pony, Animagine) Hugging Face ve Civitai engelli olduğu için okunamadı [D]. Her checkpoint ve LoRA için model kartı ayrıca kontrol edilmeli. **Güncelleme (düzeltildi 24.09.2026):** Arama alıntılarıyla doğrulandı (bkz. §3.2). NoobAI-XL ticari kullanımı yasaklıyor [54]. Animagine XL 4.0 ve Illustrious v1.x OpenRAIL++-M [55][56].
- **Kaggle, Colab, Leonardo, PixAI, Tensor.art, Kling ve diğer SaaS ücretsiz limitleri** sık değişiyor ve doğrulanamadı [D].
- **Telif hukuku belirsiz.** ABD yaklaşımı vaka bazında. Türk FSEK'te eser sahibinin gerçek kişi olması gerektiği yorumu yaygın [D]. Rakipler saf yapay zekâ asset'lerimizi kopyalayabilir.
- **İtibar riski.** Anime kitlesi yapay zekâ sanatına karşı hassas. Beyan edilmezse ve ifşa olursa zarar büyük olur (Clair Obscur örneği [44]).
- **Araç ömrü kısa.**
  - Imagen bir yıl içinde deprecated oldu [13] ve kapatıldı [51]. Gemini 2.5 Flash Image de 2 Ekim 2026'da kapatılacak [O] (düzeltildi 24.09.2026).
  - Topluluk MCP'leri resmî araç çıkınca terk ediliyor [18].
  - Vertex AI yeniden markalandı [9].

  Boru hattı sağlayıcıdan bağımsız kurulmalı: manifest + adaptör betikleri.
- **Güvenlik.** Ev ağındaki ComfyUI'ı internete açmak (tünel) risklidir. Kimlik doğrulama ve IP kısıtı olmadan açılmamalı. API anahtarları ortam değişkeni yerine API credential olarak saklanmalı [15].

---

## Kaynaklar

1. Higgsfield CLI (README, MIT): https://github.com/higgsfield-ai/cli
2. Higgsfield Skills (README, INSTALL, `.claude-plugin/marketplace.json`, COOKBOOK): https://github.com/higgsfield-ai/skills
3. Higgsfield model kataloğu: https://github.com/higgsfield-ai/skills/blob/HEAD/higgsfield-generate/references/model-catalog.md
4. Higgsfield troubleshooting (generate ve soul-id): https://github.com/higgsfield-ai/skills/blob/HEAD/higgsfield-generate/references/troubleshooting.md ve https://github.com/higgsfield-ai/skills/blob/HEAD/higgsfield-soul-id/references/troubleshooting.md
5. Higgsfield Cursor plugin, `mcp.json` (mcp.higgsfield.ai): https://github.com/higgsfield-ai/cursor-plugin/blob/HEAD/mcp.json ve https://github.com/higgsfield-ai/cursor-plugin
6. Higgsfield GitHub organizasyonu ve Python SDK: https://github.com/orgs/higgsfield-ai/repositories ve https://github.com/higgsfield-ai/higgsfield-client
7. Higgsfield npm paketleri: https://www.npmjs.com/package/@higgsfield/cli , https://www.npmjs.com/package/@higgsfield/client , https://www.npmjs.com/package/@higgsfield/cloud-cli
8. Higgsfield fiyat sayfası (bu oturumda erişilemedi): https://higgsfield.ai/pricing
9. Google Cloud generative AI fiyatları (Agent Platform'a yönlendiriyor): https://cloud.google.com/vertex-ai/generative-ai/pricing
10. Google Cloud Free (300 $ kredi): https://cloud.google.com/free
11. Gemini Cookbook, Nano Banana: https://github.com/google-gemini/cookbook/blob/HEAD/quickstarts/Get_Started_Nano_Banana.ipynb
12. Gemini Cookbook, Imagen ve Veo notları: https://github.com/google-gemini/cookbook/blob/HEAD/quickstarts/Get_started_imagen.ipynb ve https://github.com/google-gemini/cookbook/blob/HEAD/quickstarts/Get_started_Veo.ipynb
13. Google GenMedia MCP (README ve mcp-genmedia-go README): https://github.com/GoogleCloudPlatform/genmedia-creative-studio/tree/HEAD/experiments/mcp-genmedia
14. Claude Code on the web: https://code.claude.com/docs/en/claude-code-on-the-web
15. Claude Code cloud environments (ağ seviyeleri, connector'lar, API credentials, varsayılan domainler): https://code.claude.com/docs/en/cloud-environments
16. Comfy MCP (resmî) ve PyPI: https://github.com/Comfy-Org/comfy-mcp ve https://pypi.org/project/comfy-mcp/
17. Comfy Cloud MCP: https://github.com/Comfy-Org/comfy-cloud-mcp
18. artokun/comfyui-mcp (bırakıldı): https://github.com/artokun/comfyui-mcp
19. ComfyUI LICENSE (GPL-3.0): https://github.com/comfyanonymous/ComfyUI/blob/HEAD/LICENSE
20. BFL FLUX README ve FLUX.1 [dev] lisansı: https://github.com/black-forest-labs/flux ve https://github.com/black-forest-labs/flux/blob/HEAD/model_licenses/LICENSE-FLUX1-dev
21. FLUX.2 README (klein ve dev lisansları, VRAM): https://github.com/black-forest-labs/flux2
22. Qwen-Image (Apache-2.0, 2512, Edit-2511, Layered, 2.0): https://github.com/QwenLM/Qwen-Image
23. Wan 2.2 (Apache-2.0, VRAM, Animate, S2V): https://github.com/Wan-Video/Wan2.2
24. Tencent Hunyuan lisansları: https://github.com/Tencent-Hunyuan/HunyuanVideo/blob/HEAD/LICENSE.txt , https://github.com/Tencent-Hunyuan/HunyuanVideo-1.5/blob/HEAD/LICENSE , https://github.com/Tencent-Hunyuan/HunyuanImage-3.0/blob/HEAD/LICENSE , https://github.com/Tencent-Hunyuan/Hunyuan3D-2.1/blob/HEAD/LICENSE
25. LTX-2.x Community License ve LTX-Video LICENSE: https://github.com/Lightricks/LTX-2/blob/HEAD/LICENSE-2_x ve https://github.com/Lightricks/LTX-Video/blob/HEAD/LICENSE
26. HiDream-I1 LICENSE (MIT): https://github.com/HiDream-ai/HiDream-I1/blob/HEAD/LICENSE
27. Z-Image (Apache-2.0): https://github.com/Tongyi-MAI/Z-Image
28. Chroma eğitim kodu (lodestone-rock/flow, Apache-2.0): https://github.com/lodestone-rock/flow
29. ai-toolkit (MIT): https://github.com/ostris/ai-toolkit
30. kohya sd-scripts (Apache-2.0), InvokeAI (Apache-2.0), Forge (AGPL-3.0): https://github.com/kohya-ss/sd-scripts , https://github.com/invoke-ai/InvokeAI , https://github.com/lllyasviel/stable-diffusion-webui-forge
31. Hugging Face Inference Providers fiyatlandırması: https://github.com/huggingface/hub-docs/blob/HEAD/docs/inference-providers/pricing.md
32. Hugging Face ZeroGPU: https://github.com/huggingface/hub-docs/blob/HEAD/docs/hub/spaces-zerogpu.md
33. Hugging Face MCP Server: https://github.com/huggingface/hf-mcp-server
34. Pollinations README: https://github.com/pollinations/pollinations
35. PixelLab MCP: https://github.com/pixellab-code/pixellab-mcp
36. Meshy MCP Server: https://github.com/meshy-dev/meshy-mcp-server
37. Kling CLI (npm): https://www.npmjs.com/package/@klingai/cli-global
38. npm kayıtları: https://www.npmjs.com/package/replicate-mcp , https://www.npmjs.com/package/@layer_ai/sdk , https://www.npmjs.com/package/scenario.com-mcp-server , https://www.npmjs.com/package/@fjacquet/nano-banana-mcp
39. TRELLIS.2 (MIT): https://github.com/microsoft/TRELLIS.2
40. U.S. Copyright Office, Copyright and AI Part 2: Copyrightability (erişilemedi): https://www.copyright.gov/ai/Copyright-and-Artificial-Intelligence-Part-2-Copyrightability-Report.pdf
41. Steam, AI içerik politikası duyurusu, Ocak 2024 (erişilemedi): https://store.steampowered.com/news/group/4145017/view/3862463747997849618
42. PC Gamer, Steam AI beyan formu güncellemesi (02 raporundan): https://www.pcgamer.com/software/ai/steam-updates-ai-disclosure-form-to-specify-that-its-focused-on-ai-generated-content-that-is-consumed-by-players-not-efficiency-tools-used-behind-the-scenes/
43. VGC ve Totally Human, Steam AI beyanları (02 raporundan): https://www.videogameschronicle.com/news/steam-games-disclosing-generative-ai-use-are-up-800-this-year/ ve https://www.totallyhuman.io/blog/games-with-ai-disclosures-have-grossed-an-estimated-660m-on-steam
44. Engadget, Indie Game Awards ve Clair Obscur (02 raporundan): https://www.engadget.com/gaming/the-indie-game-awards-snatches-back-two-trophies-from-clair-obscur-over-its-use-of-generative-ai-164730842.html
45. AB Yapay Zekâ Yasası, Tüzük (AB) 2024/1689 (erişilemedi): https://eur-lex.europa.eu/eli/reg/2024/1689/oj
46. Higgsfield planları ve fiyatları (arama alıntısı; site engelli): https://higgsfield.ai/creator-hub/help-center/plans/how-do-higgsfield-plans-work , https://higgsfield.ai/blog/annual-unlimited-ai-video-plans , https://higgsfield.ai/blog/best-all-in-one-subscription-ai-images-video , https://higgsfield.ai/pricing
47. Higgsfield, "What Uses My Credits" ve "What Are Unlimited Models" (MCP/CLI/Canvas her zaman kredi düşüyor): https://higgsfield.ai/creator-hub/help-center/credits/what-uses-my-credits ve https://higgsfield.ai/creator-hub/help-center/credits/what-are-unlimited-models-and-which-plans-include-them
48. Google Cloud Blog, Free Trial ile Gemini 3 Pro Image (300 $, 91 gün): https://cloud.google.com/blog/topics/developers-practitioners/getting-started-with-gemini-3-unlocking-the-cloud-with-the-free-trial
49. Gemini API Billing (2 Mart 2026 sonrası hesaplarda deneme kredisi Gemini API'ye harcanamıyor; arama alıntısı): https://ai.google.dev/gemini-api/docs/billing
50. Google Cloud Free Program, deneme kısıtları ve yükseltme: https://docs.cloud.google.com/free/docs/free-cloud-features ; forum: https://discuss.google.dev/t/gemini-requests-throttled-on-vertex-ai-free-trial-is-quota-increase-required/341554 ve https://discuss.google.dev/t/429-resource-exhausted-on-gemini-3-1-flash-image-preview-via-vertex-ai-global-endpoint-no-editable-quota-row-visible-new-project/350186
51. Gemini API deprecations (Imagen 4 kapanışı 17.08.2026): https://ai.google.dev/gemini-api/docs/deprecations ; Vertex release notes: https://docs.cloud.google.com/vertex-ai/generative-ai/docs/release-notes
52. Gemini API Additional Terms of Service (Unpaid Services veri kullanımı): https://ai.google.dev/gemini-api/terms
53. Vertex AI batch inference with Gemini (24 saat hedef süre): https://docs.cloud.google.com/vertex-ai/generative-ai/docs/multimodal/batch-prediction-gemini
54. NoobAI-XL model kartı (fair-ai-public-license-1.0-sd + ticarileştirme yasağı): https://huggingface.co/Laxhar/noobai-XL-1.1/raw/main/README.md ve https://huggingface.co/Laxhar/noobai-XL-1.0
55. Animagine XL 4.0 model kartı (CreativeML OpenRAIL++-M): https://huggingface.co/cagliostrolab/animagine-xl-4.0
56. Illustrious XL model kartları (v0.1 FAIPL-1.0-SD; v1.0/v1.1 OpenRAIL++-M; v2.0 lisans tartışması): https://huggingface.co/OnomaAIResearch/Illustrious-xl-early-release-v0 , https://huggingface.co/OnomaAIResearch/Illustrious-XL-v1.0 , https://huggingface.co/OnomaAIResearch/Illustrious-XL-v1.1 , https://huggingface.co/OnomaAIResearch/Illustrious-XL-v2.0/discussions/4
57. Higgsfield changelog ve Unlimited MCP (24 saatlik deneme 31.07.2026'da bitti; 22.08.2026'dan beri 3 gün + 100 MCP kredisi): https://higgsfield.ai/creator-hub/changelog ve https://higgsfield.ai/blog/unlimited-mcp
58. Higgsfield, 24 saatlik ücretsiz sınırsız web denemesi ve All Unlimited: https://higgsfield.ai/blog/free-unlimited-ai-video-generation-2026 ve https://higgsfield.ai/blog/higgsfield-all-unlimited-explained
59. Higgsfield, "Who Owns Your Generations" (ticari kullanım): https://higgsfield.ai/creator-hub/help-center/account/who-owns-my-generations-and-can-i-use-them-commercially
60. Comfy Cloud fiyatları: https://comfy.org/pricing/ ve https://blog.comfy.org/p/comfy-cloud-new-features-and-pricing
61. Pony Diffusion V6 XL model kartı: https://huggingface.co/LyliaEngine/Pony_Diffusion_V6_XL
62. Vertex AI express mode: https://docs.cloud.google.com/vertex-ai/generative-ai/docs/start/express-mode/overview ; ikincil: https://www.cloudzero.com/blog/google-vertex-ai-pricing/
63. Cooley, "EU AI Act: Transparency Obligations Take Effect 2 August 2026": https://www.cooley.com/news/insight/2026/2026-08-03-eu-ai-act-transparency-obligations-take-effect-2-august-2026
64. Steam AI beyan formu güncellemesi (Ocak 2026): https://www.gamedeveloper.com/business/valve-tweaks-and-clarifies-ai-disclosure-rules-for-steam
65. ABD Telif Hakkı Ofisi Part 2 özetleri (29.01.2025): https://ipwatchdog.com/2025/01/29/part-two-copyright-office-ai-report-says-creative-prompting-doesnt-constitute-authorship/ ve https://www.finnegan.com/en/insights/ip-updates/us-copyright-office-ai-prompts-alone-provide-insufficient-control-over-expression-to-protect-ai-generated-content.html
66. Engadget / GamesRadar, Clair Obscur ödüllerinin geri alınması: https://www.gamesradar.com/games/rpg/clair-obscur-expedition-33s-controversial-goty-wins-at-the-indie-game-awards-retracted-after-the-rpgs-use-of-generative-ai/

---

## Doğrulama Notları (24.09.2026)

Bu bölüm, rapordaki karar açısından kritik iddiaların 24.09.2026'da bağımsız olarak yeniden kontrol edilmesiyle eklendi. higgsfield.ai, ai.google.dev, docs.cloud.google.com ve huggingface.co bu container'dan hâlâ engelli. Bu sitelerdeki bilgiler, WebSearch sonuçlarındaki birincil sayfa alıntılarından alındı. cloud.google.com fiyat sayfası, GitHub README/LICENSE dosyaları, PyPI ve npm doğrudan okundu.

| İddia | Sonuç | Düzeltme/Not | Kaynak |
|---|---|---|---|
| Higgsfield plan fiyatları doğrulanamadı; "Unlimited" süreli ve modele bağlı [D] | **Düzeltildi** | Eylül 2026: ~9 $ (120 kredi), Starter 15 $ (200), Plus 49 $ / yıllıkta 39 $ (1.000), Ultra 129 $ / yıllıkta 99 $ (3.000). Ücretsiz plan kredisiz. Kademe adları 2026'da birkaç kez değişti, üçüncü taraf rakamları farklı | [46] |
| Higgsfield "Unlimited" Claude/MCP ile de geçerli olabilir (örtük) | **Düzeltildi** | Unlimited ve ücretsiz üretimler yalnızca higgsfield.ai web'de geçerli. MCP/CLI/Canvas/Supercomputer her zaman kredi düşüyor. 24 saatlik "Unlimited MCP" denemesi 31.07.2026'da bitti. Şu anda 3 gün + 100 MCP kredisi veriliyor, kart gerekiyor, iptal edilmezse Plus'a dönüşüyor | [47][57] |
| Higgsfield "tüm modellerde sınırsız ve ücretsiz" plan yok | Doğrulandı | Yeni kullanıcılara yalnızca web'de 24 saatlik sınırsız deneme var (20'den fazla model, aynı anda 1 üretim, kart gerekli) | [58] |
| Higgsfield ticari kullanım "ücretli planlarda" [D] | **Düzeltildi** | Çıktının ticari kullanımı plana bağlı değil, Higgsfield çıktılar üzerinde hak iddia etmiyor | [59] |
| Higgsfield resmî MCP: `https://mcp.higgsfield.ai/mcp` (HTTP) | Doğrulandı | cursor-plugin `mcp.json` (master dalı) ve Higgsfield'in "Connect to Claude" sayfası. claude.ai'de Customize → Connectors ile eklenip OAuth ile bağlanıyor | [5] |
| Higgsfield Claude plugin: `/plugin marketplace add higgsfield-ai/skills`, 9 skill; CLI MIT v1.1.26 (18.09.2026) | Doğrulandı | README ve npm kaydı. `higgsfield-game-generation` klasörü main dalda hâlâ 404 | [1][2] |
| Gemini API'de NB2 Lite (`gemini-3.1-flash-lite-image`) ücretsiz katmanda | Doğrulandı | Cookbook: "It includes a free tier". Görsel başı ücretsiz limit doğrulanamadı | [11] |
| Gemini API ücretsiz katmanında veri kullanımı [D] | **Doğrulandı (belirsizlik giderildi)** | Unpaid Services'te içerik ürün geliştirmede kullanılıyor ve insan değerlendiriciler görebiliyor. Gizli materyal gönderilmemeli | [52] |
| Imagen 30.06.2026 itibarıyla deprecated | **Düzeltildi (netleştirildi)** | Vertex'te 30.06.2026'da kapatıldı, Gemini API'de 17.08.2026'da kapatıldı. Yerine `gemini-3.1-flash-image` öneriliyor | [13][51] |
| GCP 300 $ kredisi yapay zekâ için kullanılabilir, süresi ~90 gün [D] | **Düzeltildi** | 90 gün (blogda 91 gün). **2 Mart 2026 sonrası açılan hesaplarda Gemini API/AI Studio'ya harcanamıyor, yalnızca Vertex'e harcanıyor.** Deneme hesabı kota artışı isteyemiyor, partner modellerini ve GPU'yu kullanamıyor. Paid'e yükseltmede kalan kredi korunuyor | [48][49][50] |
| NB2 fiyatları 0,045/0,067/0,101/0,15 $; Pro 0,134/0,24 $; Lite 0,034 $; Flex/Batch yarı fiyat | Doğrulandı | Sayfa `gemini-enterprise-agent-platform/generative-ai/pricing` adresine yönleniyor. Rakamlar birebir aynı | [9] |
| Veo 3.1 Lite 0,03/0,05 $; Fast 0,08/0,10/0,12 $; Veo 3.1 0,40/0,60 $ | Doğrulandı | Ek bilgi: Veo 3.1 sessiz 720p/1080p 0,20 $, 4K sessiz 0,40 $ | [9] |
| "~4.470 görsel / ~10.000 sn video" hesabı | Doğrulandı (aritmetik), **koşullu** | 300/0,067 = 4.477; 300/0,03 = 10.000. Yalnızca Vertex üzerinden ulaşılabilir. Batch 24 saate kadar sürebilir, deneme kotaları 24 saatlik hacmi düşürebilir | [9][49][50][53] |
| GenMedia MCP: Gemini Image, Veo, Lyria, Chirp/Gemini TTS, AVTool; ADC; `GOOGLE_CLOUD_PROJECT` zorunlu | Doğrulandı | README ve mcp-genmedia-go README. `mcp-omni-go` da var | [13] |
| `comfy-mcp` (PyPI), 40 araç, beta; `cloud.comfy.org/mcp` OAuth | Doğrulandı | PyPI v0.10.0. comfy-mcp'nin lisansı AGPL-3.0-or-later ya da ticari. VRAM tablosu birebir aynı | [16] |
| Comfy Cloud fiyatı [D] | **Düzeltildi** | Aylık 400 kredilik ücretsiz katman. Standard 20 $ (~4,4 GPU saati), Creator 35 $, Pro 100 $ | [60] [O] |
| FLUX.1 [dev] / Kontext [dev] ticari değil, çıktı ticari kullanılabilir | Doğrulandı | Lisans v1.1.1: model yalnızca ticari olmayan amaçla kullanılabilir. "use (a) for revenue-generating activity… is not a Non-Commercial Purpose". Çıktı "any purpose (including commercial)" | [20] |
| FLUX.2 [dev] ve klein 9B ticari değil; klein 4B Apache-2.0, ~8 GB VRAM | Doğrulandı | FLUX.2 README lisans tablosu. klein 4B Base da Apache-2.0 | [21] |
| Qwen-Image ailesi Apache-2.0 | Doğrulandı | LICENSE Apache-2.0. Not: Qwen-Image-2.0 için README'de ağırlık yayımı yok, yalnızca Qwen Chat'te deneniyor | [22] |
| Wan 2.2 Apache-2.0; TI2V-5B 24 GB (4090); A14B 80 GB | Doğrulandı | LICENSE.txt ve README ("We claim no rights over the your generated contents") | [23] |
| Z-Image Apache-2.0; Turbo 16 GB'a sığıyor | Doğrulandı | README. stable-diffusion.cpp ile 4 GB'a kadar iniyor | [27] |
| HiDream-I1 MIT | Doğrulandı (not eklendi) | Kod ve ağırlıklar MIT. Metin kodlayıcı Llama 3.1 8B Instruct, Llama lisansına tabi | [26] |
| Illustrious / NoobAI / Animagine lisansları "genelde FAIPL veya OpenRAIL++, çıktıya izin var" [D] | **Düzeltildi** | **NoobAI-XL: model çıktıları dahil her türlü ticarileştirme yasak.** Illustrious v0.1 FAIPL-1.0-SD. Illustrious v1.0/v1.1 OpenRAIL++-M. Illustrious v2.0 kartında Open RAIL-M. Animagine XL 4.0 değiştirilmemiş OpenRAIL++-M. Pony V6: değiştirilmiş FAIPL, çıktı ticari serbest, para kazanan inference servisi yasak | [54][55][56][61] |
| Tencent Hunyuan lisansı AB/BK/G. Kore'de geçersiz, çıktının bölge dışında gösterilmesi yasak | Doğrulandı | HunyuanVideo-1.5 LICENSE, Territory tanımı ve Madde 5(c) | [24] |
| LTX-2.x: yıllık geliri 10 M $'ın altındaki kuruluşlara ücretsiz | Doğrulandı | LICENSE-2_x: "annual revenues of at least $10,000,000" için ticari lisans gerekiyor | [25] |
| SD 3.5: yıllık geliri 1 M $'ın altındakilere ücretsiz [D] | Doğrulandı [O] | Stability AI Community License. Kayıt ve "Powered by Stability AI" ibaresi gerekiyor | stability.ai/news/license-update |
| HF ZeroGPU 2/5/40 dk; Inference 0,10 $ / 2 $ | Doğrulandı | hub-docs. PRO, kota sonrası 10 dakikası 1 $'dan devam edebiliyor | [31][32] |
| PixelLab resmî MCP `https://api.pixellab.ai/mcp` | Doğrulandı | README `master` dalında. Kimlik doğrulama Bearer token ile yapılıyor, bu yüzden claude.ai connector'ından çok API credential yoluna uygun [O]. Fiyat hâlâ [D] | [35] |
| Meshy resmî MCP, 24 araç, rig/animate | Doğrulandı | Ek bilgi: Meshy API anahtarı için Pro veya üstü plan gerekiyor. Rig 5, animate 3 kredi | [36] |
| Steam 2026 form güncellemesi: oyuncunun tükettiği içeriğe odaklı | Doğrulandı | Ocak 2026. Oyunla gelen ya da mağaza sayfasındaki sanat, ses, metin ve pazarlama materyali beyan kapsamında | [42][64] |
| ABD Telif Hakkı Ofisi Part 2 (29.01.2025): yalnızca prompt yetmez | Doğrulandı | "prompts alone do not provide sufficient human control". Algılanabilir insan katkısı, seçim/düzenleme ve değişiklik korunabilir | [65] |
| Clair Obscur, Indie Game Awards ödüllerini kaybetti (Aralık 2025) | Doğrulandı | GOTY ve Debut Game geri alındı. Gerekçe: üretken yapay zekâ kullanımı ve başvuruda bunun beyan edilmemesi | [44][66] |
| AB YZ Yasası Madde 50, 2 Ağustos 2026'dan itibaren [D] | Doğrulandı [O] | Madde 50 ertelenmedi. Komisyon rehberi 20.07.2026'da yayımlandı. 50(2) işaretleme için piyasadaki sistemlere 02.12.2026'ya kadar süre var (Mayıs 2026 geçici uzlaşması) | [63] |
| Kaggle haftada ~30 saat GPU [D] | Doğrulandı [O] | ~30 saat/hafta (dalgalı kota), oturum başına 12 saat, T4×2 veya P100 | kaggle.com/docs/efficient-gpu-usage |
| Vertex AI Express Mode ile ücretsiz görsel üretimi mümkün mü? (yeni) | Hayır [O] | Express Mode Flash/Flash-Lite metin modellerini kapsıyor. Nano Banana, Veo ve Lyria ücretsiz değil | [62] |
