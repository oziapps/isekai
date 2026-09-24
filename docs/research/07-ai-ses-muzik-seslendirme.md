# 07 — Yapay Zekâ ve Ücretsiz Araçlarla Seslendirme, TTS, Müzik ve SFX (2026)

> Hazırlanma: 2026-09-24
>
> **Yöntem ve sınırlar (önce bunu okuyun):** Bu rapor yazılırken oturumun ortak WebSearch kotası (200/200) dolmuştu. elevenlabs.io, ai.google.dev, docs.cloud.google.com, huggingface.co, suno.com, sagaftra.org, fmod.com, sonniss.com ve Microsoft/Azure siteleri egress proxy tarafından engelliydi. Bu yüzden doğrulama şu kaynaklardan yapıldı:
> - Resmî GitHub repolarındaki README ve LICENSE dosyaları (raw.githubusercontent.com). Buna Microsoft'un GitHub'daki Azure doküman kaynağı ve Google'ın Gemini Cookbook'u da dahil.
> - PyPI ve npm kayıtları (sürüm ve tarih bilgisi için)
> - Erişilebilen **cloud.google.com** fiyat sayfaları
> - **code.claude.com** dokümanları
> - Bu container'da yapılan **canlı testler**: erişim testleri ve CPU üzerinde gerçek bir TTS çalıştırması
>
> **Güven notasyonu:**
> - **[Y]:** Birincil kaynak bu oturumda okundu.
> - **[T]:** Bu container'da canlı test edildi.
> - **[O]:** Orta güven. İkincil kaynak, kardeş rapor ya da çıkarım.
> - **[D]:** Doğrulanamadı. Model bilgisine (Haziran 2026'ya kadar) dayanıyor. Karar vermeden önce kontrol edilmeli.
>
> Köşeli parantezli sayılar `## Kaynaklar` listesini gösteriyor.

## Özet

- **Container'dan doğrudan erişilebilen tek ses sağlayıcısı Google.** `texttospeech.googleapis.com` ve `generativelanguage.googleapis.com` anahtarsız isteğe Google'ın kendi 403 JSON'uyla cevap verdi, yani erişilebilir durumdalar. `api.elevenlabs.io` ise `connect_rejected` hatasıyla engellendi [T]. ElevenLabs, MiniMax, Cartesia ve Azure için ya API credential, ya Custom ağ, ya da claude.ai connector'ı gerekiyor [48].
- **Google'ın ses fiyatları çok düşük ve doğrulandı** [1]:
  - **Chirp 3 HD:** Her ay ilk **1 milyon karakter ücretsiz**, sonrası 30 $/1M karakter.
  - **Gemini 2.5 Flash TTS:** 10 $/1M ses token'ı. Saniyede 25 token üretildiği için dakikası yaklaşık **0,015 $** ediyor.
  - **Gemini 2.5 Pro TTS ve 3.1 Flash TTS:** 20 $/1M token, dakikası yaklaşık **0,03 $**.
  - **Yeni hesaplara 300 $ kredi** veriliyor [4]. Bu, bir günlük "blitz" için en güçlü yasal kaynak.
- **Gemini API'de artık "Gemini 3.8 TTS" var** (`gemini-3.8-flash-tts`, `-flash-lite-tts`) [5][6]:
  - 30 hazır ses
  - **Voice Design:** Metinle tarif ederek sıfırdan özgün ses yaratma
  - **Voice Replication:** Klonlama. Sahibinin sesli rıza cümlesini okuması zorunlu, yapay zekâ sesleri referans olarak kabul edilmiyor.
  - Çok konuşmacılı diyalog

  Özgün anime karakterleri için "tarif et, klonlama" yaklaşımı hem etik hem hukuken temiz.
- **ElevenLabs'in yerel MCP sunucusu kullanımdan kaldırıldı (deprecated).** Yerini OAuth'lu **uzak (hosted) MCP** aldı: `https://api.elevenlabs.io/v1/mcp` [10]. Resmî `elevenlabs/skills` paketi TTS, SFX, müzik, ses değiştirme ve dublaj becerilerini içeriyor [12].
  - Ücretsiz katman: ayda **10 bin kredi** [10].
  - Modeller: `eleven_v3` 70+ dil, `multilingual_v2` 29 dil, `flash_v2_5` 32 dil ve %50 daha ucuz [11].
  - Ücretsiz katmanın ticari kullanım izni ve plan fiyatları doğrulanamadı [D].
- **Açık modellerde lisans tuzakları var. Ticari kullanım YASAK olanlar:**
  - F5-TTS ağırlıkları (CC-BY-NC) [25]
  - XTTS-v2 (CPML) [26]
  - Fish Audio S2 (Research License, ticari için yazılı lisans şart) [24]
  - Higgs Audio v3 (ticari olmayan) [17]
  - MusicGen (CC-BY-NC) [40]
  - MMAudio (CC-BY-NC) [43]
  - ThinkSound [42]
  - YuE2: şirketler için ayrıca lisans gerekiyor [39]
- **Ticari kullanıma açık, güçlü seçenekler:**
  - **VoxCPM2** (Apache-2.0; 30 dil, **Türkçe ve Japonca dahil**, Voice Design) [36]
  - **Chatterbox Multilingual V3** (MIT; 23 dil, TR ve JA dahil) [19]
  - **Qwen3-TTS** (Apache-2.0; JA/EN, Voice Design) [35]
  - **Kokoro-82M** (Apache) [18]
  - **GPT-SoVITS** (MIT; JA/EN/KO/ZH) [23]
  - **IndexTTS-2.5** (bilibili lisansı: 100 milyon aylık kullanıcı veya 1 milyar RMB ciro altında ücretsiz ticari) [21]
  - **AivisSpeech + ACML lisanslı modeller** (Japonca anime tınısı; ticari serbest, kredi isteğe bağlı) [33]
- **Microsoft VibeVoice-TTS kodu kaldırıldı.** Microsoft Eylül 2025'te kötüye kullanım gerekçesiyle kodu sildi. Kalan Realtime-0.5B için de "ticari kullanım önerilmez" diyor [22].
- **Container'da (4 vCPU, GPU yok) gerçekçi yerel TTS yalnızca hafif modellerle mümkün.** Kokoro ONNX'i GitHub Releases'ten indirip çalıştırdık: 5,7 sn İngilizce sesi 2,66 sn'de üretti (**RTF 0,47**, yani gerçek zamandan ~2 kat hızlı) [T].
  - Ağırlıklarının çoğu huggingface.co'da duran modeller (VoxCPM2, Chatterbox, Qwen3-TTS) Trusted ağda **indirilemiyor** [T].
  - Bu modeller ya kullanıcının kendi GPU'lu PC'sinde ya da Custom ağla çalıştırılmalı.
- **Müzik tarafı** [3][7][8][38]:
  - Google **Lyria 3 Pro:** tam şarkı 0,08 $
  - **Lyria 3:** 30 sn klip 0,04 $
  - Gemini API'de **Lyria 3.5:** 3 dakikaya kadar şarkı ve `instrumental_only` parametresi
  - **Lyria RealTime:** "önizlemede, şimdilik kota sınırlı ücretsiz", 48 kHz stereo, yalnızca enstrümantal
  - Yerelde **ACE-Step 1.5** (MIT; 10 sn–10 dk; ≤6 GB VRAM'de de çalışıyor)
- **Suno ve Udio'nun 2025–2026 durumu bu oturumda doğrulanamadı** [D]. Plak şirketi davaları ve anlaşmalardan sonra ücretsiz katmanın sahiplik ve indirme hakları değişti. Oyunun ana müziği için bu iki araç **önerilmiyor**.
- **Uyarlanabilir (adaptive) müzik için ara katmana gerek yok.** Godot 4.3+ yerleşik `AudioStreamInteractive` (klip ve geçiş tablosu), `AudioStreamPlaylist` ve `AudioStreamSynchronized` (katmanlı stem) sınıflarını sunuyor [45]. Gerekirse Godot 4 için FMOD ve Wwise eklentileri de mevcut [46].
- **SFX:**
  - ElevenLabs SFX v2 (0,5–30 sn, döngü desteği) [12]
  - Stable Audio Open (Stability Community License: yıllık 1 milyon $ ciro altında ücretsiz ticari, kayıt gerekli) [42]
  - Kenney (CC0) [47]
  - Sonniss GDC paketleri ve Freesound CC0/CC-BY [D]
  - HunyuanVideo-Foley lisansı **AB, Birleşik Krallık ve Güney Kore'de geçersiz**. Global Steam oyunu için elenmeli [44].
- **Önerilen strateji: hibrit.**
  - Ana kadro (4–6 karakter) insan seslendirmen.
  - Oyundaki diegetik **"Sistem" sesi** (Solo Leveling tarzı bildirim sesi) bilinçli olarak sentetik tasarlanır. Kurguya en uygun ve etik olarak en temiz AI kullanımı bu.
  - İsimli NPC'ler ve "bark" satırları Voice Design ile üretilmiş özgün seslerle yapılır. Hiçbir gerçek kişinin sesi klonlanmaz.
  - Steam beyanı ve her ses dosyası için manifest tutulur.

---

## 1. Container'dan erişim: canlı test sonuçları [T]

| Hedef | Sonuç | Anlamı |
|---|---|---|
| `texttospeech.googleapis.com/v1/voices` | Google 403 JSON ("unregistered callers") | **Erişilebilir.** API anahtarı eklenince çalışır. |
| `generativelanguage.googleapis.com/v1beta/models` | Google 403 JSON | **Erişilebilir** (Gemini TTS, Lyria 3.5, Lyria RealTime) |
| `aiplatform.googleapis.com` | 404 (Google) | Erişilebilir (Vertex: Lyria 2/3, Gemini-TTS) |
| `api.elevenlabs.io` | `connect_rejected` | **Engelli.** Credential, Custom ağ veya connector gerekli. |
| huggingface.co, modelscope.cn, ai.google.dev, elevenlabs.io, suno.com, sonniss.com, freesound.org, fmod.com | engelli | Açık ağırlıklar container'a indirilemez. Dokümanlar okunamaz. |
| github.com Releases | 200/206 | **Kokoro ONNX modeli (325 MB) ve ses dosyası (28 MB) indirildi** |
| pypi.org | 200 | `kokoro-onnx`, `google-genai`, `elevenlabs`, `minimax-mcp` vb. kurulabilir |

**CPU kıyası (Kokoro-82M ONNX, 4 vCPU):**
- Model yükleme: 3,3 sn
- İngilizce 108 karakterlik bir satır: 2,66 sn'de 5,7 sn ses (**RTF 0,468**)
- 54 ses var, bunların 5'i Japonca (`jf_alpha`, `jf_gongitsune`, `jf_nezumi`, `jf_tebukuro`, `jm_kumo`)
- Türkçe yok [T][18]

---

## 2. Ticari TTS servisleri (2026)

| Servis | Ücretsiz katman | Ticari kullanım | JA / EN / TR | MCP / araç | Container'dan erişim |
|---|---|---|---|---|---|
| **Google Chirp 3 HD** | Ayda 1M karakter ücretsiz, sonra 30 $/1M [Y][1]. Faturalandırma açık olmalı [1]. | Ücretli bulut hizmeti. Çıktı kullanıcıya ait [D]. | 75+ dil ve varyant, 380+ ses [Y][2]. JA/TR bu oturumda tek tek doğrulanamadı [O] | GenMedia MCP: `mcp-chirp3-go` [Y][9] | **Evet** |
| **Google Gemini-TTS** (Cloud TTS/Vertex) | Yok ("Not available"). 2.5 Flash: 0,50 $/1M metin + 10 $/1M ses token'ı. 2.5 Pro ve 3.1 Flash: 1 $ + 20 $ [Y][1] | Aynı | 75+ lokal, stil/ton/tempo doğal dille yönetiliyor [Y][2] | GenMedia MCP, `genmedia-voice-director` becerisi [Y][9] | **Evet** |
| **Gemini API: Gemini 3.8 TTS + Voices API** | Gemini API ücretsiz katmanı ve fiyatları doğrulanamadı [D] | [D] | 30 hazır ses, Voice Design, rıza kontrollü Replication, 24 kHz mono WAV [Y][5][6] | `google-genai` SDK 2.25.0 (22.09.2026) [Y][49] | **Evet** |
| **ElevenLabs** | Ayda 10 bin kredi [Y][10] | Ücretsiz katmanda ticari hak yok ve atıf gerekli; Starter'dan itibaren ticari [D] | v3: 70+ dil. Multilingual v2: 29 dil [Y][11]. JA/TR'nin listede olması [O] | **Hosted MCP** `api.elevenlabs.io/v1/mcp` (OAuth) ve `elevenlabs/skills` [Y][10][12] | Hayır (engelli) |
| **Azure AI Speech** | F0 katmanı var, aylık kota fiyat sayfasında ve doğrulanamadı [Y][14]. ~0,5M karakter/ay [D] | Ücretli katmanda evet [D] | **TR:** `tr-TR-Aydın/Elif:MAI-Voice-2` (HD, 10+ duygu stili) + Emel/Ahmet. **JA:** Nanami/Masaru DragonHD dahil 12 ses [Y][14] | Resmî MCP bulunamadı | Hayır |
| **MiniMax Speech** | [D] | [D] | [D] | **Resmî MiniMax-MCP**: `text_to_audio`, `voice_clone`, `voice_design`, `list_voices`. Host `api.minimax.io` [Y][15] | Hayır |
| **Cartesia** | [D] | [D] | [D] | Resmî `cartesia-mcp` 0.22.3 (21.09.2026) [Y][16] | Hayır |
| **Hume (Octave)** | [D] | [D] | [D] | npm `@humeai/mcp-server` 0.3.0 [Y][16] | Hayır |
| **OpenAI TTS** (`gpt-4o-mini-tts` vb.) | Yok [D] | Evet, ama sesin yapay olduğunu kullanıcıya bildirme koşulu var [D] | Çok dilli [D] | Resmî MCP yok | Hayır |
| **Fish Audio API** | [D] | API ile ticari kullanım [D]. **Açık ağırlıklar ticari değil** [Y][24] | S2: 80+ dil, JA "Tier 1", TR "global" [Y][24] | `fish-audio-sdk` 1.3.0 [Y][49] | Hayır |
| **Boson Higgs Audio v3 API** | "Ücretsiz, hız sınırlı genel önizleme" [Y][17] | Ağırlıklar ticari olmayan lisanslı. API şartları [D] | 100+ dil [Y][17] | OpenAI uyumlu REST | Hayır |

### 2.1 ElevenLabs: ayrıntılar
- **Modeller** [Y][11][12]:

  | Model | Dil | Gecikme | Not |
  |---|---|---|---|
  | `eleven_v3` | 70+ | standart | En dramatik performans, çok konuşmacılı diyalog |
  | `eleven_multilingual_v2` | 29 | standart | Kararlılık |
  | `eleven_flash_v2_5` | 32 | ~75 ms | Yarı fiyat |
  | `eleven_turbo_v2_5` | 32 | 250–300 ms | — |

- **SFX** [Y][12]: `eleven_text_to_sound_v2`. Süre 0,5–30 sn, `loop=true` ile kusursuz döngü ve `prompt_influence` ayarı var.
- **Müzik** [Y][12]: `music_v2`.
  - Kompozisyon planıyla bölüm bölüm kontrol: her bölüm 3–120 sn, toplam 3 sn–10 dk.
  - Sözlü ya da enstrümantal parça üretilebiliyor.
  - Inpainting ile var olan parçanın bir bölümü yeniden üretilebiliyor.
  - Stream özelliği yalnızca ücretli planlarda.
  - Ticari lisans kapsamı (plak şirketleriyle yapılan lisans anlaşmaları) doğrulanamadı [D].
- **Kimlik doğrulama:** `xi-api-key` header'ı [Y][12]. Claude Code API credential'ında header adı `xi-api-key`, prefix boş bırakılacak.
- **MCP** [Y][10]:
  - Yerel `elevenlabs-mcp` (PyPI 0.12.2, 04.08.2026) "deprecated, artık bakımı yapılmıyor".
  - Hosted MCP OAuth kullanıyor, bu yüzden anahtar istemciye kopyalanmıyor.

### 2.2 Google: neden varsayılan sağlayıcımız olmalı
- **Erişim:** Container'dan erişim var [T]. Ayrıca yeni müşteriye 300 $ kredi veriliyor ve tam hesap aktive edilmeden ücret kesilmiyor [Y][4].
- **Birim maliyet hesabı** [1]:
  - Gemini-TTS'te ses token'ı "saniyede 25".
  - 1 dakika = 1.500 token. Flash'ta 0,015 $, Pro/3.1 Flash'ta 0,03 $.
  - 1 saatlik bitmiş ses: **0,90 $ / 1,80 $**. Metin girdi maliyeti ihmal edilebilir.
- **Chirp 3 HD** [1][O]:
  - İngilizcede dakikada ~900 karakter varsayımıyla 1M karakter ≈ **18 saat ses**.
  - Bu miktar her ay ücretsiz.
  - Varsayım yaklaşık bir hesap, gerçek oran metne göre değişir.
- **Voices API** [Y][6]:
  - Voice Design: yaş, aksan, tını, tempo ve arketip metinle tarif ediliyor. Her çağrı farklı bir varyasyon üretiyor. 2–3 aday alıp en iyisi seçilir.
  - Replication: 10 sn temiz referans ses ve aynı kişinin aynı odada okuduğu, kelimesi kelimesine rıza cümlesi gerekiyor: *"I am the owner of this voice and I consent to Google using this voice to create a synthetic voice model."*
  - SynthID/C2PA ve deepfake dedektörleri çalışıyor. **Yapay zekâ üretimi sesler referans olarak kabul edilmiyor.**
- **MCP** [Y][9]:
  - GenMedia MCP (Go binary'leri) Gemini TTS, Chirp 3 HD ve Lyria'yı kapsıyor.
  - ADC, `PROJECT_ID` ve `LOCATION` istiyor.
  - Yanında `genmedia-voice-director` ve `genmedia-audio-engineer` ajan becerileri geliyor.

---

## 3. Açık ağırlıklı TTS modelleri: lisans, dil ve CPU matrisi

"Ticari" sütunu ağırlık lisansına göre dolduruldu. Kod lisansı ile ağırlık lisansı farklı olabiliyor.

| Model | Kod / ağırlık lisansı | Ticari? | JA | EN | TR | CPU (container) | Kaynak |
|---|---|---|---|---|---|---|---|
| **Kokoro-82M** | Apache-2.0 / Apache | ✅ | ✅ (5 ses) | ✅ | ❌ | ✅ **RTF 0,47 ölçüldü** | [Y][T][18] |
| **Chatterbox Multilingual V3** (500M) | MIT | ✅ (PerTh filigranı ekliyor) | ✅ | ✅ | ✅ | Mümkün ama yavaş [O]. Ağırlıklar HF'de. | [Y][19] |
| Chatterbox Turbo (350M) / **Nano** (110M) | MIT | ✅ | ❌ | ✅ | ❌ | Nano: 8 çekirdekte 3× gerçek zaman | [Y][19] |
| **VoxCPM2** (2B, 04/2026) | Apache-2.0 (ağırlık dahil) | ✅ | ✅ | ✅ | ✅ | GGUF/llama.cpp-omni var. ~6–8 GB VRAM önerilir. CPU yavaş [O] | [Y][36] |
| **Qwen3-TTS** (0.6B/1.7B, 01/2026) | Apache-2.0 | ✅ | ✅ | ✅ | ❌ | 0.6B CPU'da denenebilir [O] | [Y][35] |
| **IndexTTS-2.5** (08/2026) | bilibili Model License | ✅ (100M MAU veya 1 milyar RMB altı) | ✅ | ✅ | ❌ | GPU önerilir | [Y][21] |
| **GPT-SoVITS** | MIT | ✅ (ama sesin sahibinin rızası şart) | ✅ | ✅ | ❌ | M4 CPU'da RTF 0,526. CPUFast çatalı var | [Y][23] |
| **Style-Bert-VITS2** | AGPL-3.0 (kod). Modellerin lisansı ayrı (JVNV: CC BY-SA 4.0) | Model lisansına bağlı | ✅ (anime tınısı) | ~ | ❌ | Sentez CPU'da çalışıyor | [Y][32] |
| **AivisSpeech Engine** | LGPL-3.0. Modeller ACML / ACML-NC / CC0 | ACML: ✅, kredi isteğe bağlı | ✅ | ❌ | ❌ | **CPU için ONNX Runtime**, Docker `cpu-latest` imajı | [Y][33] |
| VOICEVOX Core | MIT (kod). Karakter seslerinin her birinin ayrı şartları var | Karakter şartına bağlı [D] | ✅ | ❌ | ❌ | ✅ | [Y][34] |
| **CosyVoice 3** (0.5B) | Apache-2.0 | ✅ [O: ağırlık lisansı HF'de] | ✅ | ✅ | ❌ | GPU önerilir | [Y][27] |
| **Dia** (1.6B) / **Dia2** (1B/2B) | Apache-2.0 | ✅ | ❌ | ✅ (yalnızca EN) | ❌ | Dia: yalnızca GPU. Dia2 CPU'ya düşebiliyor | [Y][20] |
| Higgs Audio v2 (3B) / v2.5 (1B) | Kod Apache. Ağırlık lisansı [D] | [D] | çok dilli | ✅ | [D] | ≥24 GB GPU önerilir | [Y][17] |
| **Higgs Audio v3** (4B) | Research & **Non-Commercial** | ❌ | 100+ dil | ✅ | ✅ | — | [Y][17] |
| **Fish Audio S2 Pro** (4B) | Fish Audio Research License (07.03.2026) | ❌ (ticari için yazılı lisans) | ✅ Tier 1 | ✅ | ✅ | GPU | [Y][24] |
| **F5-TTS** | Kod MIT / ağırlık **CC-BY-NC** | ❌ | — | ✅ | — | — | [Y][25] |
| **XTTS-v2** | Kod MPL-2.0 / ağırlık **CPML** | ❌ (Coqui kapandı, ticari lisans alınamıyor [D]) | ✅ | ✅ | ✅ | Yavaş | [Y][26] |
| Orpheus (3B) | Kod Apache. Ağırlık Llama-3.2 tabanlı [O] | Llama lisansı [O] | araştırma sürümü | ✅ | ❌ | llama.cpp ile GPU'suz çalışıyor | [Y][28] |
| Sesame CSM-1B | Kod Apache. Llama-3.2-1B gerekiyor | [O] | ❌ | ✅ | ❌ | CPU örneği var | [Y][30] |
| Kyutai TTS / **Pocket TTS** (100M) | Kod MIT/Apache. Ses lisansları HF'de [O] | [O] | ❌ | ✅ | ❌ | **Pocket: 2 çekirdekte, M4'te ~6× gerçek zaman** | [Y][29] |
| Piper | **GPL-3.0** motor. Her sesin lisansı ayrı | Sese bağlı | ❌ | ✅ | ✅ (tr_TR) | ✅ çok hızlı, ama robotik | [Y][31] |
| NeuTTS (Air/Nano/2E) | NeuTTS Open License 1.0 | ✅ (yıllık ciro < 5 M$ ise) | ❌ | ✅ | ❌ | GGUF, cihaz üstü | [Y][37] |
| **VibeVoice** (Microsoft) | MIT kod. **TTS kodu 05.09.2025'te kaldırıldı**. Realtime-0.5B duruyor | "Ticari kullanım önerilmez" | Deneysel JP sesi | ✅ | ❌ | — | [Y][22] |

**Önemli notlar:**
- **AGPL (Style-Bert-VITS2):** Aracı yalnızca kendi bilgisayarımızda WAV üretmek için kullanır ve kodunu oyuna gömmezsek, AGPL'nin oyuna sıçramaması beklenir [O]. Yine de oyun içinde çalışma anında TTS için AGPL kod **gömülmemeli**.
- **CC BY-SA (JVNV modelleri):** "Share-alike" koşulunun üretilen sese uzanıp uzanmadığı belirsiz. Güvenli seçim **ACML veya CC0 lisanslı** AivisHub modelleri [Y][33].
- **Hazır anime sesleri:** Topluluktaki "hazır anime sesi" GPT-SoVITS/RVC modellerinin çoğu gerçek seiyuu'ların izinsiz klonları. **Kesinlikle kullanılmamalı** (bkz. §4).

---

## 4. Hukuk, etik ve oyuncu tepkisi

| Konu | Durum | Güven |
|---|---|---|
| **Rıza** | Dia ve CSM, "gerçek kişiyi izinsiz taklit" kullanımını açıkça yasaklıyor [20][30]. Gemini Replication sesli rıza istiyor [6]. Chatterbox her çıktıya görünmez filigran gömüyor [19]. | [Y] |
| **SAG-AFTRA Interactive Media Agreement 2025** | Grev Temmuz 2024'te başladı, Haziran 2025'te askıya alındı. Temmuz 2025'te yeni sözleşme yüksek oyla onaylandı. Temel maddeler: dijital kopya (replica) için bilgilendirilmiş rıza ve açıklama, kullanım başına ücret, grev sırasında rızanın askıya alınabilmesi. | [D] (orta) |
| **Japonya "NO MORE 無断生成AI"** | Ekim 2024'te Japonya Aktörler Sendikası (日俳連) çevresindeki 26 seslendirme sanatçısının başlattığı, izinsiz AI ses üretimine karşı kampanya. Japon hayran kitlesi bu konuda çok hassas. | [D] (orta) |
| **Steam beyanı** | Oyuncunun tükettiği AI içeriği (ses dahil) mağaza sayfasında beyan ediliyor. 2025'te çıkan oyunların ~%20'si beyanda bulundu [O][kardeş rapor 02, 05]. | [O] |
| **Oyuncu tepkisi** | Clair Obscur, AI kullanımı yüzünden Indie Game Awards ödüllerini kaybetti [O][02]. AI seslendirme kullanan büyük yapımlar (ör. Embark oyunları) eleştiri aldı ama ticari olarak başarılı oldu [D]. | O/D |
| **AB Yapay Zekâ Yasası md. 50** | Şeffaflık yükümlülükleri 2 Ağustos 2026'dan itibaren uygulanıyor. Açıkça sanatsal ve kurgusal eserlerde ifşa yükümlülüğü hafif. Olası ertelemeler netleşmedi [O][kardeş rapor 04, 05]. | O/D |
| **Türkiye (KVKK)** | Ses kişisel veri. Klonlama amaçlı kullanımda açık rıza gerekli [D]. | D |
| **Telif** | Yalnızca prompt ile üretilen çıktının ABD'de telifle korunmaması muhtemel. İnsan düzenlemesi korunabilir [O][05]. | O |

**Sonuç:** Etik sıralama şöyle olmalı:
1. İnsan sanatçı
2. Voice Design ile sıfırdan tasarlanan ses
3. Yazılı ve ücretli rıza ile klonlanan ses
4. İzinsiz klon: **asla**

Seslendirmen sözleşmelerine bir "AI maddesi" eklenmeli:
- Sesin, ayrı bir ücret ve yazılı onay olmadan model eğitiminde kullanılmayacağı yazılmalı.
- İleride ek satır üretmek istersek satır başı ücret ve iptal hakkı tanınmalı.

---

## 5. İnsan seslendirmen: nerede ve kaça?

| Kanal | Kullanım | Fiyat |
|---|---|---|
| Casting Call Club, Backstage | İngilizce indie/hobi ve yarı-profesyonel seçmeler | Karakter başına düşük yüzlerden birkaç yüz dolara [D] (düşük) |
| Voice123, Voices.com | Profesyonel sendikasız İngilizce/çok dilli | Oturum veya satır paketi başına birkaç yüz $ [D] (düşük) |
| Fiverr | Hızlı ve ucuz. Kalite çok değişken | Paket başına 50–300 $ bandı yaygın [D] (düşük) |
| SAG-AFTRA (sendikalı) | AAA kalite | 4 saatlik oturum başına ~1.000 $+ [D] (orta-düşük) |
| Japonya (seiyuu) | Ajans üzerinden. 日俳連'nin rütbe (ランク) sistemi ücreti belirliyor. Coconala/Skeb gibi platformlarda indie talepler de var | Mutlaka teklif alınmalı [D] |
| Türkiye (dublaj stüdyoları) | TR dublaj | Mutlaka teklif alınmalı [D] |

**Bütçe formülü:** (karakter başına satır × ortalama saniye) ÷ oturum verimi (bitmiş dakika/saat) × saatlik ücret + stüdyo, yönetmen ve düzeltme (pickup) payı (+%20–30).

İlk iş olarak AI ile "scratch VO" (geçici ses) kaydı yapılmalı. Senaryo buna göre kilitlenir. Böylece insan oturumlarında boşa satır ödenmez [O].

---

## 6. Müzik

| Araç | 2026 durumu | Ticari hak | Erişim ve maliyet |
|---|---|---|---|
| **Google Lyria 3 / 3 Pro / 2** (Vertex) | 30 sn klip 0,04 $, tam şarkı 0,08 $, Lyria 2 0,06 $ [Y][3] | Ücretli bulut çıktısı. SynthID filigranı [D] | Container ✅, GenMedia `mcp-lyria-go` [9] |
| **Lyria 3.5** (Gemini API) | 3 dakikaya kadar yapılı şarkı (intro, verse, chorus), çok dilli vokal, `instrumental_only`, BPM ve zamanlı yönlendirme, 10 görsele kadar ilham girdisi [Y][7] | [D] | Container ✅ |
| **Lyria RealTime** (`lyria-realtime-exp`, v1alpha) | "Önizleme, şimdilik kota sınırlı ücretsiz". Enstrümantal, 48 kHz, BPM/yoğunluk/parlaklık/ölçek gerçek zamanlı değişiyor [Y][8] | Önizleme şartları [D] | Container ✅. Canlı ve dinamik savaş müziği prototipi için ideal |
| **ElevenLabs Music** (`music_v2`) | 10 dk'ya kadar, bölüm planı, inpainting [Y][12] | Plak şirketi lisanslarıyla "ticari kullanıma temiz" iddiası [D] | Credential veya connector gerekli |
| **ACE-Step 1.5** (XL 4B: 04/2026) | 10 sn–10 dk, 50+ dilde şarkı sözü, LoRA eğitimi (8 şarkı, 3090'da 1 saat). ≤6 GB VRAM'de DiT-only modda çalışıyor. Kalite "Suno v4.5 ile v5 arası" (kendi iddiası) [Y][38] | **MIT** ✅. Proje "orijinalliği doğrulayın, AI kullanımını açıklayın" diyor [38] | Yerel GPU (kullanıcı PC'si) |
| ACE-Step 1.0 | [Y][38] | Apache-2.0 ✅ | Yerel |
| **YuE2** (3B, 09/2026) | 24 GB VRAM ve BF16 gerekiyor [Y][39] | Ağırlıklar CC BY-NC 4.0 + "yaratıcı izni". Bireysel yaratıcılar çıktıyı para kazanmak için kullanabiliyor, **şirketler lisans almalı** [Y][39]. YuE v1 (eski dal) Apache-2.0 [Y][39] | Yerel |
| MusicGen / AudioGen | [Y][40] | **CC-BY-NC** ❌ | — |
| **Magenta RealTime** | v1: kod Apache + ağırlık **CC-BY 4.0**, "Google çıktılar üzerinde hak iddia etmez" [Y][41]. MRT2: 230M/2.4B, gerçek zamanlı çalışması için Apple Silicon gerekli. Lisansı README'de yok [D] | v1 ✅ (atıfla) | Yerel (Mac veya NVIDIA) |
| Stable Audio Open / 2.5 | Open 1.0 Stability Community License ile yayında (1 M$ altı ücretsiz, kayıt gerekli) [Y][42]. 2.5 kurumsal odaklı ve lisanslı veriyle eğitildi [D] | Koşullu ✅ | Yerel / API |
| **Suno / Udio** | 2024'te büyük plak şirketleri dava açtı. 2025 sonunda bazı anlaşmalar yapıldı (ör. UMG–Udio, WMG–Suno/Udio). Udio indirmeyi kısıtladı, Suno'da indirme ücretli hesaba bağlandı [D] | Suno ücretsiz planında şarkı Suno'nun, ücretli planda kullanıcının [D]. Topluluk `suno-mcp` hesap çerezleriyle çalışıyor (resmî değil, kullanım şartları riski) [Y][49] | **Önerilmiyor** |
| AIVA / Soundraw / Beatoven | AIVA'nın ücretsiz planında telif AIVA'da. Pro planda kullanıcıda [D] | Plana bağlı [D] | — |

**Önerilen müzik yaklaşımı:**
- **Ana tema ve leitmotif'ler insan besteci tarafından yazılmalı** (ya da en azından insan elinden geçmeli). Nedenleri:
  - Anime OP/ED hissini veren vokalli tema şarkısı markanın kimliği.
  - Kardeş rapor 04'teki OST DLC gelir modeli (7,99–9,99 $) özgün ve telif sahibi olunan müzik gerektiriyor.
- Keşif ve arka plan döngüleri, varyasyonlar ve stem'ler AI ile üretilebilir: ACE-Step 1.5 (MIT) veya Lyria. Bunlar insan eliyle düzenlenmeli.
- **Uyarlanabilir müzik** [Y][45]: Godot 4.3+ yerleşik araçları yeterli.
  - `AudioStreamInteractive`: keşif, gerilim ve savaş klipleri arasında geçiş tablosu.
  - `AudioStreamSynchronized`: aynı tempoda katmanlar, ör. boss HP'si düştükçe davulun açılması.
  - `AudioStreamPlaylist`: şehir ve hub müzikleri.
- **FMOD veya Wwise** yalnızca Unity/Unreal seçilirse ya da çok katmanlı mikser gerekirse düşünülmeli. Godot 4 için `fmod-gdextension` (Godot 4.4 ve FMOD 2.03'te test edilmiş) ve Wwise entegrasyonu mevcut [Y][46].
  - FMOD Indie lisansı küçük gelir ve bütçede ücretsiz [D]: ~200 bin $ gelir ve ~500–600 bin $ bütçe altı.
  - Wwise küçük bütçeli projelerde ücretsiz [D]: ~250 bin $ altı, varlık sınırıyla.

---

## 7. SFX

| Kaynak | Lisans | Not |
|---|---|---|
| **ElevenLabs SFX v2** | Ücretli planda ticari [D] | 0,5–30 sn, `loop` desteği, MCP ve becerisi var [Y][12] |
| **Stable Audio Open** | Stability Community License: 1 M$ altı ücretsiz ticari, **kayıt şart** [Y][42] | Yerel GPU |
| **Kenney** | **CC0** (starter kit README'lerinde "sound effects CC0") [Y][47] | UI ve mekanik sesler |
| **Sonniss GDC paketleri** | Telifsiz, ticari kullanım serbest, atıf gerekmiyor [D] | Yılda ~20–30 GB profesyonel kayıt [D] |
| **Freesound** | Ses başına CC0, CC-BY veya CC-BY-NC [D] | **NC olanlar elenmeli**, CC-BY için kredi listesi tutulmalı |
| ZapSplat | Ücretsiz planda atıf gerekiyor, ücretli planda gerekmiyor [D] | — |
| MMAudio | Ağırlık **CC-BY-NC** ❌ [Y][43] | Video-ses senkronu iyi ama ticari değil |
| HunyuanVideo-Foley | Tencent lisansı, **AB/BK/GK hariç** ❌ [Y][44] | Global oyun için elenmeli |
| ThinkSound | "Commercial use is NOT permitted" ❌ [Y][42] | — |
| Veo 3.1 (sesli video) | Ücretli bulut | Ara sahnelerde senkron ses için [O][05] |

---

## 8. Önerilen ses yığınları

### (A) 0 € yığını

| Katman | Container (Claude'un kendisi) | Kullanıcının PC'si (GPU'lu) |
|---|---|---|
| Geçici VO ve prototip | **Kokoro ONNX** (EN; Apache; ağırlıklar GitHub'da) [T] | — |
| Nihai AI sesleri (NPC, bark, Sistem) | **Chirp 3 HD**: ayda 1M karakter ücretsiz (fatura hesabı açık olmalı) [1] | **VoxCPM2** (TR/JA/EN, Voice Design, Apache) · **Chatterbox ML V3** (TR/JA, MIT) · **Qwen3-TTS VoiceDesign** (JA/EN) · **AivisSpeech + ACML/CC0 modeller** (JA anime tınısı) |
| Müzik | Lyria RealTime önizlemesi (kota sınırlı ücretsiz; ticari şartlar [D]) | **ACE-Step 1.5** (MIT) + insan düzenlemesi · Magenta RT v1 (CC-BY) |
| SFX | Kenney (CC0), Sonniss GDC (manuel indirme gerekli, çünkü container'dan erişilemiyor) | **Stable Audio Open** (kayıtlı) + Freesound CC0 |
| Orkestrasyon | `kokoro-onnx`, `google-cloud-texttospeech` | ComfyUI + Comfy MCP (kardeş rapor 05). ACE-Step'in ComfyUI desteği var [38] |

"Tamamen ücretsiz ve sınırsız" olmanın tek yolu açık ağırlıkları kullanıcının kendi GPU'sunda çalıştırmak. Bulut tarafında her seçeneğin bir kotası var.

### (B) 1 günlük "blitz" (24 saat)
Doğrulanabilen "24 saat sınırsız" bir ses denemesi bulunamadı. En güçlü yasal karşılığı **yeni Google Cloud hesabının 300 $ kredisi** [4]. Tamamı container'dan yürütülebilir:

| İş | Hacim (varsayım) | Maliyet (hesap, [1][3]) |
|---|---|---|
| Voice Design ile 40 NPC ve Sistem sesi oluşturma (2–3 aday) | ~120 deneme | Çok düşük [O] |
| Gemini 2.5 Pro TTS ile JA+EN+TR bark ve NPC satırları | 24.000 satır × 4 sn = 1.600 dk | **~48 $** |
| Lyria 3 Pro ile müzik taslakları | 60 parça × 5 varyasyon = 300 şarkı | **~24 $** |
| Lyria 3 ile döngü ve stinger klipleri | 500 × 30 sn | **~20 $** |
| **Toplam** | | **~92 $, 300 $ kredinin çok altında** |

**Gerçek darboğaz para değil.** Asıl sınırlar şunlar:
- Yeni projelerin dakikalık kotaları [D]
- İnsanın dinleme ve seçme süresi

SFX için bu gün ElevenLabs Creator'ın ilk ayı alınabilir (indirimli olduğu iddiası [D]). Credential ile container'dan toplu SFX üretilir, sonra abonelik iptal edilir.

### (C) Küçük bütçe (ör. 1.500–6.000 $, EA dönemi)
1. **İnsan seslendirmen** (bütçenin büyük kısmı): 4–6 ana karakter için yalnızca **kilit sahneler, savaş efor sesleri ve imza replikler**. Hades'teki gibi "az ama bağlama duyarlı satır" ilkesi uygulanmalı (kardeş rapor 03).
2. **Google pay-as-you-go** ile NPC ve bark satırları: 10 saatlik bitmiş ses Pro TTS'te ~18 $ [1].
3. **ElevenLabs** (Creator veya Pro, 1–2 ay): v3 ile duygusal ara replikler ve SFX [D fiyat].
4. **Besteci:** ana tema, 3–5 leitmotif ve vokalli tema şarkısı. AI taslaklar besteciye "referans" olarak verilir. Telif sözleşmesi OST satışını kapsamalı.
5. **Middleware:** Godot yerleşik araçları (0 $). Unity/Unreal seçilirse FMOD Indie [D].

---

## 9. Karakter başına seslendirme planı (öneri)

Satır sayıları **planlama varsayımıdır**, kaynaklı veri değildir. Oyun konsepti netleşince güncellenmeli.

| Karakter / rol | Satır (varsayım) | JP | EN | TR | İnsan mı AI mı? | Araç |
|---|---|---|---|---|---|---|
| **Kahraman** (oyuncu, isekai edilen) | 300–600 (efor sesleri + kilit replikler) | İnsan (2. faz) | **İnsan** | Altyazı | İnsan. Diyalogların çoğu seçmeli ve metin olarak kalır | Kayıt |
| **"Sistem" / Tanrıça arayüzü** | 500–1.500 (bildirim, level-up, görev) | AI | AI | **AI (TR seslendirmeli)** | **Bilinçli olarak sentetik.** Kurguya uygun ve etik olarak temiz | Gemini Voice Design / Chirp 3 HD / VoxCPM2 |
| **Ana yol arkadaşları** (3–4) | Her biri 400–1.000 | İnsan (2. faz) | **İnsan** | Altyazı (gelir olursa AI veya insan TR) | İnsan. Sözleşmeye AI maddesi eklenir | Kayıt |
| **Lonca resepsiyonisti / hub rehberi** (DanMachi'deki Eina benzeri) | 300–800, sık tekrar | İnsan | İnsan | Altyazı | İnsan (oyuncuyla en çok temas eden ses) | Kayıt |
| **Ana kötü + 4–6 boss** | Her biri 50–200 | İnsan | İnsan | Altyazı | İnsan (büyük anlar) | Kayıt + efekt |
| **İsimli NPC'ler** (20–60) | Her biri 10–60 | AI | AI | AI | **AI, Voice Design ile özgün ses** (klon yok) | Gemini TTS / VoxCPM2 / AivisSpeech (JA) |
| **Kalabalık, walla, düşman bark'ları** | 1.000–3.000 | AI | AI | AI | AI + işleme | Chirp 3 HD / Kokoro / ElevenLabs |
| **Canavarlar ve yaratıklar** | — | — | — | — | SFX katmanlama | ElevenLabs SFX / Stable Audio Open / Sonniss + pitch-formant işleme |

**Dil stratejisi:**
- **EA / 1. faz:** İngilizce insan VO (ana kadro) + JP/EN/TR altyazı + tüm dillerde AI Sistem sesi. İngilizce seslendirmen bulmak ve yönetmek, Türkiye'den çalışan tek geliştirici için en kolayı [O].
- **2. faz (satış iyiyse):** Japonca insan dublaj ("dual audio"). Anime hayranı için özgünlük sinyali çok güçlü. Kast için Japon indie platformları veya ajans kullanılabilir [O].
- **Türkçe:** Önce altyazı. Sistem ve NPC'ler için AI TR sesi. TR pazarı karşılığını verirse insan TR dublaj.
- **Yasak:** Türkçe AI dublaj için İngilizce seslendirmenin sesi **rızası ve ek ücreti olmadan** klonlanmayacak.

---

## 10. Claude Code MCP ve API kurulum adımları

### 10.1 Google (varsayılan, Trusted ağda çalışır)
1. Google Cloud'da proje aç. Faturalandırmayı etkinleştir (300 $ kredi burada gelir) [4]. **Text-to-Speech API**, **Vertex AI API** ve/veya Gemini API'yi aç.
2. **Anahtar:** AI Studio'dan Gemini API anahtarı veya Cloud API anahtarı al.
3. **claude.ai/code → ortamı düzenle → API credentials → Add credential** [48]. Bu özellik Pro ve Max planlarında var.
   - Gemini API için:
     - Allowed websites: `generativelanguage.googleapis.com`
     - Header adı: `x-goog-api-key`
     - Prefix: **boş**
   - Cloud TTS için ayrı bir credential ekle: `texttospeech.googleapis.com`, aynı header.
   - Credential'ın gerçekten eklendiğini önce `curl` ile doğrula. SDK "anahtar yok" hatası verirse ortam değişkenine sahte bir değer koymak gerekebilir [O].
4. **Kütüphaneler** PyPI'dan kurulur: `google-genai` (2.25.0), `google-cloud-texttospeech` (2.37.0) [49].
5. **Dil desteği testi:** Türkçe ve Japonca sesleri doğrulamak için şu çağrı yapılır: `GET https://texttospeech.googleapis.com/v1/voices?languageCode=tr-TR` (ve `ja-JP`).
6. **GenMedia MCP (isteğe bağlı)** [9]: ADC (hizmet hesabı) istiyor. Anahtar dosyası ortam değişkenine konursa oturumda görünür hâle gelir. Bu yüzden MCP'yi **kullanıcının kendi PC'sinde** çalıştırmak ya da container'da doğrudan SDK kullanmak daha güvenli.

### 10.2 ElevenLabs (üç yol)
- **Önerilen yol: claude.ai connector.** Özel connector URL'si `https://api.elevenlabs.io/v1/mcp` (OAuth) [10]. Connector trafiği Anthropic sunucularından geçtiği için ağ izin listesine takılmaz [48].
- **Alternatif: API credential.**
  - Host: `api.elevenlabs.io`
  - Header: `xi-api-key`
  - Prefix: boş [12][48]

  Ardından `npx skills add elevenlabs/skills` ve `pip install elevenlabs` (2.69.0) kurulur [12][49].
- **Önerilmeyen yol:** `.mcp.json` içinde `uvx elevenlabs-mcp`. Bu sunucu deprecated ve `ELEVENLABS_API_KEY` oturumda görünür kalır.

### 10.3 MiniMax, Cartesia, Hume
Repo'nun `.mcp.json` dosyasındaki sunucular bulut oturumunda yükleniyor [48]. Örnek:
```json
{
  "mcpServers": {
    "minimax": {
      "command": "uvx",
      "args": ["minimax-mcp", "-y"],
      "env": {
        "MINIMAX_API_HOST": "https://api.minimax.io",
        "MINIMAX_MCP_BASE_PATH": "/home/user/isekai/assets/audio/_raw",
        "MINIMAX_API_RESOURCE_MODE": "local"
      }
    }
  }
}
```
- Anahtarlar `.mcp.json`'a **yazılmamalı**.
- MiniMax için host `api.minimax.io`, header `Authorization`, prefix `Bearer` (MCP README'sindeki host eşleşmesi uyarısına dikkat) [15].
- Cartesia (`cartesia-mcp`) ve Hume (`@humeai/mcp-server`) için de aynı desen kullanılır. Hostları doğrulanamadı [D].

### 10.4 Açık modeller
- **Container:** Yalnızca GitHub veya PyPI'da barınan ağırlıklar indirilebiliyor (Kokoro ONNX) [T].
- **HF'deki ağırlıklar için iki seçenek var:**
  - (a) Ortamı **Custom** ağa geçirip `huggingface.co` ve `*.hf.co` eklemek. CPU'da yine yavaş çalışır.
  - (b) **Önerilen:** Kullanıcının GPU'lu PC'sinde yerel Claude Code + ComfyUI veya Gradio sunucuları çalıştırmak (VoxCPM2, Chatterbox, ACE-Step, Stable Audio Open).
- **Ses manifesti:** Her dosya için `assets/audio/manifest.csv` tutulmalı. Sütunlar: `dosya, karakter, dil, araç/model, sürüm, lisans, ses kaynağı (tasarım/insan/rıza-klon), prompt/seed, insan düzenlemesi, tarih`. Bu kayıt Steam beyanı, AB md. 50 uyumu ve telif savunmasının temeli.

---

## Oyunumuz İçin Çıkarımlar

1. **Varsayılan ses sağlayıcısı Google olmalı.**
   - Container'dan doğrudan erişiliyor.
   - Chirp 3 HD'de ayda 1M karakter ücretsiz, Gemini-TTS'te dakikası 0,015–0,03 $.
   - 300 $ kredi bir günlük blitz için fazlasıyla yeterli [1][4][T].
2. **"Sistem" sesi bilinçli olarak AI olsun.** Solo Leveling tarzı sistem bildirimleri, level-up ve görev sesleri JA/EN/TR üç dilde Voice Design ile tasarlanmış özgün bir sesle yapılır. Böylece AI kullanımı "ucuzluk" gibi değil, **dünyanın kurgusal bir parçası** gibi algılanır. Beyanda da böyle anlatılır.
3. **Ana kadroda insan ses, geniş kadroda tasarlanmış AI ses.** Bu hibrit yapı hem bütçeye uyuyor hem de "AI slop" tepkisini sınırlıyor. **Hiçbir gerçek kişinin sesi (özellikle seiyuu'lar) klonlanmayacak.**
4. **Lisans beyaz listesi** `docs/legal/model-whitelist.md` dosyasına işlenmeli:
   - **İzinli:** Kokoro, VoxCPM2, Chatterbox, Qwen3-TTS, GPT-SoVITS (rızalı ses), IndexTTS-2.5, AivisSpeech + ACML/CC0, ACE-Step, Stable Audio Open (kayıtlı), Kenney.
   - **Yasak:** F5-TTS, XTTS-v2, Fish S2 açık ağırlıkları, Higgs v3, MusicGen, MMAudio, ThinkSound, HunyuanVideo-Foley, Suno ücretsiz planı.
5. **Türkçe ses için ilk adaylar:**
   - Gemini-TTS ve Chirp 3 HD (TR sesleri API'den doğrulanmalı)
   - VoxCPM2 (yerel, Apache)
   - Chatterbox ML V3 (yerel, MIT)
   - Azure `tr-TR MAI-Voice-2` (duygu stilleri güçlü, ama credential gerekiyor)
6. **Japonca anime tınısı için** AivisSpeech + ACML modelleri ve Gemini Voice Design karşılaştırılmalı. Japon kullanıcılar için AI kullanımı kredilerde açıkça yazılmalı.
7. **Müzik:**
   - Ana tema ve leitmotif'ler için insan besteci.
   - Döngü ve varyasyonlar için ACE-Step 1.5 veya Lyria ve insan düzenlemesi.
   - Uyarlanabilir sistem Godot'nun `AudioStreamInteractive` ve `AudioStreamSynchronized` sınıflarıyla kurulur. Lyria RealTime ile "dinamik savaş müziği" prototipi denenebilir.
8. **Senaryo önce, kayıt sonra.** Önce AI ile scratch VO yapılır, ritim ve metin oyun içinde test edilir, satırlar kilitlenir, en son insan oturumlarına geçilir.
9. **Sözleşme ve manifest işleri erkenden** yapılmalı: seslendirmen AI maddesi, besteci telif devri (OST satışı için) ve ses manifesti.
10. **Kurulum sırası:**
    1. Google credential
    2. `google-genai` ile bir `tools/audio/tts_batch.py` betiği (YAML senaryodan toplu üretim)
    3. ElevenLabs connector (SFX için)
    4. Kullanıcının PC'sinde ComfyUI + ACE-Step / Stable Audio Open

## Belirsizlikler ve Riskler

- **Doğrulanamayan ticari şartlar [D]:**
  - ElevenLabs plan fiyatları ve ücretsiz katmanın ticari yasağı ya da atıf şartı
  - ElevenLabs Music'in lisans kapsamı
  - Gemini API'de TTS ve Lyria'nın ücretsiz katmanı
  - Lyria RealTime önizleme çıktılarının ticari kullanımı
  - Suno, Udio ve AIVA'nın güncel şartları

  Bunlar birincil sayfalardan kontrol edilmeden para harcanmamalı.
- **Dil desteği:**
  - Chirp 3 HD ve Gemini-TTS'in tr-TR ve ja-JP sesleri tek tek doğrulanmadı. Sayfada yalnızca "75+ dil ve varyant" yazıyor [2].
  - ElevenLabs v3'ün 70+ dili içinde TR ve JA'nın olması [O].
- **Kota ve hız sınırları:** Yeni GCP projelerinin varsayılan kotaları blitz'i yavaşlatabilir [D].
- **Model lisansı değişimi:** Lisanslar değişebiliyor. Örnekler: YuE'nin v1'deki Apache lisansından v2'de NC'ye geçmesi [39], Higgs'in v3'te non-commercial olması [17], VibeVoice'un geri çekilmesi [22]. Her sürüm manifestte sabitlenmeli.
- **Share-alike ve AGPL yorumu:** JVNV (CC BY-SA) çıktılarına ve Style-Bert-VITS2 (AGPL) kullanımına dair yorumlarımız hukuki görüş değil [O].
- **Oyuncu tepkisi:** Beyan edilmiş AI sesleri anime topluluğunda (özellikle JP) olumsuz karşılanabilir. Riski azaltmak için ana kadroda insan ses, şeffaf beyan ve "Sistem" kurgusu kullanılmalı.
- **Hukuki gelişmeler:** SAG-AFTRA 2025 maddeleri, "NO MORE 無断生成AI" kampanyası ve AB AI Act md. 50'nin oyunlara uygulanması bu oturumda birincil kaynaktan okunamadı [D].
- **Donanım:** Kullanıcının GPU'su bilinmiyor. 6 GB altı VRAM'de VoxCPM2, ACE-Step XL ve Stable Audio pratik olmayabilir [36][38]. Bu durumda bulut API'leri ağırlık kazanır.
- **Watermark:** Chatterbox çıktıları (PerTh) ve Google çıktıları (SynthID [D]) filigran taşıyor. Bu şeffaflık açısından iyi, ama sonradan "insan kaydı" diye sunulamaz. Zaten sunulmamalı.

## Kaynaklar

1. Google Cloud Text-to-Speech fiyatları (Gemini-TTS, Chirp 3 HD, ücretsiz kotalar): https://cloud.google.com/text-to-speech/pricing
2. Google Cloud Text-to-Speech ürün sayfası (380+ ses, 75+ dil, Gemini-TTS, instant custom voice): https://cloud.google.com/text-to-speech
3. Google Cloud generative AI fiyatları (Lyria 2/3/3 Pro): https://cloud.google.com/vertex-ai/generative-ai/pricing (yönlendirme: https://cloud.google.com/gemini-enterprise-agent-platform/generative-ai/pricing)
4. Google Cloud Free Program (300 $ kredi): https://cloud.google.com/free
5. Gemini Cookbook, TTS (Gemini 3.8 TTS): https://github.com/google-gemini/cookbook/blob/main/quickstarts/Get_started_TTS.ipynb
6. Gemini Cookbook, Voices API (Voice Design ve Replication, rıza): https://github.com/google-gemini/cookbook/blob/main/quickstarts/Get_Started_Voices.ipynb
7. Gemini Cookbook, Lyria 3.5: https://github.com/google-gemini/cookbook/blob/main/quickstarts/Get_started_Lyria.ipynb
8. Gemini Cookbook, Lyria RealTime: https://github.com/google-gemini/cookbook/blob/main/quickstarts/Get_started_LyriaRealTime.ipynb
9. Google GenMedia MCP: https://github.com/GoogleCloudPlatform/vertex-ai-creative-studio/tree/main/experiments/mcp-genmedia
10. ElevenLabs MCP (deprecated uyarısı, hosted MCP, 10 bin kredi): https://github.com/elevenlabs/elevenlabs-mcp
11. ElevenLabs Python SDK (model listesi): https://github.com/elevenlabs/elevenlabs-python
12. ElevenLabs Skills (text-to-speech, sound-effects, music, setup-api-key): https://github.com/elevenlabs/skills
13. PyPI elevenlabs-mcp: https://pypi.org/project/elevenlabs-mcp/
14. Azure Speech dokümanları (GitHub kaynağı: TTS dil/ses tablosu, kotalar): https://github.com/MicrosoftDocs/azure-ai-docs/blob/main/articles/ai-services/speech-service/includes/language-support/tts.md ve https://github.com/MicrosoftDocs/azure-ai-docs/blob/main/articles/ai-services/speech-service/speech-services-quotas-and-limits.md
15. MiniMax MCP: https://github.com/MiniMax-AI/MiniMax-MCP
16. Cartesia MCP (PyPI) ve Hume MCP (npm): https://pypi.org/project/cartesia-mcp/ ve https://www.npmjs.com/package/@humeai/mcp-server
17. Boson Higgs Audio (v3 notu ve README_V2): https://github.com/boson-ai/higgs-audio
18. Kokoro ve Kokoro ONNX: https://github.com/hexgrad/kokoro ve https://github.com/thewh1teagle/kokoro-onnx
19. Chatterbox (Multilingual V3, Turbo, Nano, PerTh): https://github.com/resemble-ai/chatterbox
20. Dia ve Dia2: https://github.com/nari-labs/dia ve https://github.com/nari-labs/dia2
21. IndexTTS (README ve bilibili Model License): https://github.com/index-tts/index-tts
22. Microsoft VibeVoice: https://github.com/microsoft/VibeVoice
23. GPT-SoVITS: https://github.com/RVC-Boss/GPT-SoVITS
24. Fish Speech / Fish Audio S2 (README ve Research License): https://github.com/fishaudio/fish-speech
25. F5-TTS: https://github.com/SWivid/F5-TTS
26. Coqui TTS (idiap fork) ve model lisansları: https://github.com/idiap/coqui-ai-TTS ve https://github.com/idiap/coqui-ai-TTS/blob/dev/TTS/.models.json
27. CosyVoice: https://github.com/FunAudioLLM/CosyVoice
28. Orpheus TTS: https://github.com/canopyai/Orpheus-TTS
29. Kyutai TTS ve Pocket TTS: https://github.com/kyutai-labs/delayed-streams-modeling ve https://github.com/kyutai-labs/pocket-tts
30. Sesame CSM: https://github.com/SesameAILabs/csm
31. Piper (GPL-3.0, VOICES.md): https://github.com/OHF-Voice/piper1-gpl
32. Style-Bert-VITS2 (README ve TERMS_OF_USE): https://github.com/litagin02/Style-Bert-VITS2 ve https://github.com/litagin02/Style-Bert-VITS2/blob/master/docs/TERMS_OF_USE.md
33. AivisSpeech Engine ve ACML 1.0: https://github.com/Aivis-Project/AivisSpeech-Engine ve https://github.com/Aivis-Project/ACML/blob/master/ACML-1.0.md
34. VOICEVOX Core: https://github.com/VOICEVOX/voicevox_core
35. Qwen3-TTS: https://github.com/QwenLM/Qwen3-TTS
36. VoxCPM2: https://github.com/OpenBMB/VoxCPM
37. NeuTTS (LICENSE): https://github.com/neuphonic/neutts-air
38. ACE-Step 1.5 ve ACE-Step: https://github.com/ace-step/ACE-Step-1.5 ve https://github.com/ace-step/ACE-Step
39. YuE / YuE2 (ana dal ve YuE-v1 dalı): https://github.com/multimodal-art-projection/YuE ve https://github.com/multimodal-art-projection/YuE/tree/YuE-v1
40. AudioCraft (MusicGen/AudioGen): https://github.com/facebookresearch/audiocraft
41. Magenta RealTime (MRT2 ve v1_legacy lisansı): https://github.com/magenta/magenta-realtime ve https://github.com/magenta/magenta-realtime/tree/v1_legacy
42. Stable Audio Tools, ThinkSound ve içindeki Stability AI Community License metni: https://github.com/Stability-AI/stable-audio-tools, https://github.com/FunAudioLLM/ThinkSound ve https://github.com/FunAudioLLM/ThinkSound/blob/main/third_party/LICENSE_StabilityAI.md
43. MMAudio: https://github.com/hkchengrex/MMAudio
44. HunyuanVideo-Foley (LICENSE, bölge istisnası): https://github.com/Tencent-Hunyuan/HunyuanVideo-Foley
45. Godot interaktif müzik sınıfları (4.3-stable etiketi dahil): https://github.com/godotengine/godot/blob/master/modules/interactive_music/doc_classes/AudioStreamInteractive.xml (ayrıca AudioStreamPlaylist.xml ve AudioStreamSynchronized.xml)
46. FMOD GDExtension ve Wwise Godot entegrasyonu: https://github.com/utopia-rise/fmod-gdextension ve https://github.com/alessandrofama/wwise-godot-integration
47. Kenney Starter Kit (ses efektleri CC0): https://github.com/KenneyNL/Starter-Kit-3D-Platformer
48. Claude Code cloud environments (ağ seviyeleri, API credentials, connector'lar, .mcp.json): https://code.claude.com/docs/en/cloud-environments
49. PyPI/npm sürüm kayıtları (elevenlabs 2.69.0, google-genai 2.25.0, google-cloud-texttospeech 2.37.0, kokoro-onnx 0.6.1, chatterbox-tts 0.1.7, pocket-tts 3.2.0, piper-tts 1.8.0, voxcpm 2.0.3, qwen-tts 0.1.1, fish-audio-sdk 1.3.0, cartesia 4.2.0, minimax-mcp 0.0.19, suno-mcp 0.1.0): https://pypi.org/project/elevenlabs/ , https://pypi.org/project/google-genai/ , https://pypi.org/project/kokoro-onnx/ , https://pypi.org/project/minimax-mcp/ , https://pypi.org/project/suno-mcp/
50. Kardeş raporlar (Steam beyanı, AB AI Act, Clair Obscur, Hades diyalog ilkesi, OST fiyatı): `docs/research/02-pazar-ve-rakip-analizi.md`, `03-oynanis-ve-baglilik-tasarimi.md`, `04-monetizasyon-ve-regulasyon.md`, `05-ai-gorsel-video-araclari.md`

**Doğrulama için önerilen, bu oturumda erişilemeyen birincil kaynaklar ([D] iddialar için):**
- https://elevenlabs.io/pricing
- https://elevenlabs.io/docs/agents-platform/operate/hosted-mcp
- https://ai.google.dev/gemini-api/docs/pricing
- https://docs.cloud.google.com/text-to-speech/docs/chirp3-hd
- https://azure.microsoft.com/pricing/details/speech/
- https://www.sagaftra.org/contracts-industry-resources/contracts/interactive-media-video-game-agreement
- https://suno.com/pricing
- https://www.fmod.com/licensing
- https://www.audiokinetic.com/pricing/
- https://sonniss.com/gameaudiogdc
- https://freesound.org/help/faq/
- https://eur-lex.europa.eu/eli/reg/2024/1689/oj
