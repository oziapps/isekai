# CLAUDE.md — TAMGA: Adsızın Kaydı

Bu depo, özgün bir isekai anime aksiyon-roguelite oyunu olan **TAMGA: Adsızın Kaydı**'nın planını ve (ileride) kaynak kodunu içerir. Tek kişilik Türk geliştirici + Claude Code ajanlarıyla yapılır. Belgeler Türkçedir; kod, tanımlayıcılar ve commit mesajları İngilizcedir.

## Önce oku

1. `docs/concepts/00-karar-kaydi.md` — **bağlayıcı kanon** (K-01…K-53). Çelişkide bu dosya kazanır. Yeni karar = yeni K satırı; sessizce değiştirme.
2. `docs/00-yonetici-ozeti.md` — tek sayfalık özet ve belge haritası.
3. İşine göre ilgili belge: sistemler `docs/02-…`, teknik `docs/06-…`, sanat/asset `docs/07-…`, ses `docs/08-…`, AI araçları `docs/09-…`, yol haritası `docs/10-…`.
4. Terimler için `docs/SOZLUK.md` (K-27). UI metinlerinde ve kodda bu terimleri kullan.

## Değişmez kurallar

- **Özgün IP.** Mevcut anime/manhwa adlarını, terimlerini, UI görünümünü kopyalama. Yasak küme (K-26): "Hunter", "Shadow", "Arise", "Dungeon Break", "Penalty Zone", "Red Gate", mavi hologram pencereler, siyah duman estetiği. Mağaza/pazarlama metinlerinde "Solo Leveling" adı geçmez.
- **Adil model.** Gacha, loot box, enerji, premium para birimi, güç satışı, süreli teklif ve oyun içi mağaza yok. Hiçbir ücretli ürün rastgele tabloya bağlanamaz.
- **Oyunda canlı LLM yok (EA).** NPC hafızası olay bayraklarıyla.
- **Kan yok, mürekkep var.** Hedef PEGI 12/16, ESRB T.
- **Lisans disiplini.** Kara listedeki model/araçları kullanma (K-38: Hunyuan ailesi, NoobAI ve merge'leri, FLUX [dev] ailesi, FLUX.2 klein 9B, GVHMR, F5-TTS, XTTS-v2, MusicGen, MMAudio, Fish S2, Higgs Audio v3, RMBG-1.4). Oyuna giren her varlık `PROVENANCE.csv`'ye bir satır olarak yazılır; AI placeholder'lar `__PLACEHOLDER__` önekiyle işaretlenir ve sürüm öncesi taranır.
- **İnsan finalleri.** Logo, key art, capsule, kahraman final tasarımları, 2D portre finalleri, cut-in panelleri ve Yankı/Adlı siluetleri insan eliyle yapılır; AI yalnızca keşif ve hızlandırma içindir.
- **Sır yok.** API anahtarlarını asla koda, belgelere ya da sohbete yazma; bulut ortamının "API credentials" özelliğini veya yerel ortam değişkenlerini kullan.

## Teknik kurallar

- **Motor:** Godot **4.7.2-stable** (sabit). **Katı tipli GDScript**: `untyped_declaration=Error`; her PR `--check-only` kapısından geçer. Sıcak yollar gerekirse GDExtension.
- **Veri güdümlü:** bir içerik = bir `.tres`; denge tabloları CSV; aksiyonlar `ActionData` (startup/active/recovery kareleri, 60 Hz mantık). Kullanıcıdan gelen `.tres` asla yüklenmez; kayıtlar şema sürümlü JSON + migrasyon.
- **Kamera:** Kapılarda 3/4 yüksek açı (K-02). Omuz üstü serbest kamera yok.
- **Sunucu yok:** yalnızca Steam liderlik tablosu. EA'da co-op yok, açık dünya yok.
- **Performans:** PC ≤40, Steam Deck ≤25 animasyonlu düşman; Deck ≥40 FPS.

## Bulut oturumunda çalışma

- Makine: 4 vCPU, 16 GB RAM, **GPU yok**. Ağ "Trusted": paket kayıtları, GitHub, `*.googleapis.com` açık; diğer siteler kapalı.
- Godot'u GitHub sürümlerinden indir ve headless çalıştır:
  ```bash
  curl -sL -o /tmp/godot.zip https://github.com/godotengine/godot/releases/download/4.7.2-stable/Godot_v4.7.2-stable_linux.x86_64.zip
  unzip -o -q /tmp/godot.zip -d /tmp && /tmp/Godot_v4.7.2-stable_linux.x86_64 --headless --version
  ```
- Headless yapılabilenler: import, testler, simülasyonlar ("1.000 oyun günü"), `--check-only`, Xvfb + llvmpipe ile ekran görüntüsü. Kullanıcının PC'sinde yapılması gerekenler: editörde görsel ayar, gamepad hissi, Steam Deck testi, yerel GPU ile asset üretimi.

## Çalışma düzeni

- Değişiklikler küçük ve modüler olmalı; paralel ajanlar farklı modüllerde çalışır (bkz. `docs/06-teknik-mimari.md`).
- Kapsam K-22 tablosuna bağlıdır; yeni özellik eklemeden önce kesme sırasını (K-24) ve üretim hızı ölçümlerini kontrol et.
- Commit mesajları İngilizce ve açıklayıcı olmalı; belgelerdeki kararlar Türkçe kalır.
