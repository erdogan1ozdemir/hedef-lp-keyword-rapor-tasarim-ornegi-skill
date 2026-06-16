# 04 · Sunum (opsiyonel) — Inbound Design System deck

Sunum yalnızca kullanıcı isterse üretilir. Raporun tüm bölümlerini yansıtan, **Inbound Design System**
ile hazırlanmış bir slayt destesidir.

## Design system'i çalışırken indir

Inbound Design System bir Claude Design handoff bundle'ıdır. Çalışırken indir, aç, README'sini oku:

```bash
curl -s -o /tmp/inbound-ds.gz "https://api.anthropic.com/v1/design/h/5vYshIIlcSgmneND7nN7HQ"
mkdir -p /tmp/inbound-ds && tar -xzf /tmp/inbound-ds.gz -C /tmp/inbound-ds
# → /tmp/inbound-ds/inbound-design-system/ (README.md + project/)
```

Sonra **README.md ve project/SKILL.md'yi oku** ve ilgili kısımları uygula. Bundle içeriği:
- `project/colors_and_type.css` — tüm token'lar + `@font-face` (Bricolage Grotesque display, Outfit body).
- `project/slides/*.html` — 1280×720 örnek slaytlar: cover, agenda, separator, content cards, KPI,
  quote, table, timeline, closing.
- `project/deck.html` + `project/deck-stage.js` — slaytları çalışan bir deck'e dizen iskelet.
- `project/assets/` — logolar (white/coral/teal), büyük-O dekoratif işaret, daireye kırpılabilir foto.
- `project/ui_kits/website/` — web UI kit (gerekirse).

## Tema (non-negotiables)
- **Fontlar:** Bricolage Grotesque (display) + Outfit (body). Asla Inter/system-ui birincil değil.
- **Renkler:** coral `#FF7B52` + dark teal `#10332F`, beyaz zemin. Yeni renk uydurma; gerekiyorsa
  data-viz token'larıyla genişlet. (Marka rengi raporu uyarlıyoruz; **sunum Inbound markasının**
  kendi sistemidir — kullanıcı aksini istemedikçe Inbound coral/teal kalır.)
- **Text highlight:** kelimenin arkasında coral blok (`.hl`). Markanın imza tipografik hamlesi.
- **Accent line:** 60×3.5px coral pill, başlık/alıntı yanında.
- **Logo:** her içerik slaytında sol-altta; kapakta wordmark alt-ortada; separatörlerde yok.
- **Insight bullets:** `➔` (kalın sağ ok), `•` veya emoji değil.
- **Foto:** daireye kırpılı, sıcak, dokümanter. Stok gülümseme yok.
- **İkon:** markanın özel seti yok; Lucide'a düş ve kullanıcıya bildir.

## Slayt eşleme (raporu yansıt)
~20-28 slayt, raporun bölümleriyle hizalı. Slayt türlerini `project/slides/` şablonlarından kopyala:
- Kapak → İçindekiler → Yönetici Özeti (KPI) → Yöntem & Kapsam → Ürün/Sayfa Yapısı → SERP &
  Görünürlük (tablo + ss) → AI Overview Bulgusu → GEO Yol Haritası → Talep Havuzu & Content Gap →
  Rakip Kanıtı → Rakip İçerik Matrisi → Editöryel Liderler → Operatör/Sektör Rakipleri → Google
  Trends → Sosyal Duygu (gruplar + ss) → Şikayet/itibar sinyali → Kullanıcı Soruları → CRO/CX →
  Sayfa İçi & CWV → Aksiyon: Kaynak Etiketleme → Aksiyon: Teknik → Aksiyon: İçerik & GEO → Aksiyon:
  CRO/CX → Aksiyon: CWV → Örnek İçerik Brief → Geliştirme Alanları → Tasarım Örneği (4 varyant) →
  Terim Sözlüğü → Kapanış.
- Tarih/kaynak damgası yalnız Yöntem + kapanışta; her slayta tekrar basma.
- Raporun ekran görüntülerini deck'e taşı (boyutlandır/kırp).

## Üretim biçimi
- **Varsayılan: HTML deck** (design system HTML tabanlı). `project/slides/*.html` bileşenlerini bir
  deck stage altında topla; `colors_and_type.css` + `deck-stage.js` ile çalıştır. Statik, paylaşılabilir.
- **PPTX isteniyorsa:** aynı temayı (coral/teal, Bricolage/Outfit) pptxgenjs ile kur (cover/closing
  teal, accent line, KPI kartları, tablo, split+ss, badge düzenleri). LibreOffice yoksa pptx
  pixel-render edilemez → içeriği markitdown ile, görünümü eşdeğer HTML deck ile QA et.
- İçeriği önce yapılandırılmış JSON olarak üret (slayt başına layout/eyebrow/title/bullets/table/
  kpis/callout/screenshot/note), sonra deck'e bas — böylece çok-ajanlı üretim ve yeniden derleme kolay.

## QA
HTML deck'i servis edip Playwright ile kapak/KPI/split+ss/badge/kapanış slaytlarını doğrula:
em-dash 0, kırık görsel 0, tema tutarlı, içerik raporla uyumlu. Font yüklü değilse (pptx) PowerPoint
ikame eder — kullanıcıya not düş.
