# 02 · HTML rapor

Tek dosyalık (self-contained) HTML rapor. Görünüm mevcut Inbound raporuyla **birebir aynı tarz**;
yalnız renkler hedef markanın LP rengine uyarlanır (okunabilirlik korunarak). Başlangıç stili için
`assets/report-shell.css`'i kullan (CSS değişkenleriyle tokenlanmış).

## Genel kabuk

- **İki sütun:** solda yapışkan **ToC (Bölümler)** + sağda içerik. ToC biraz sola taşınır, gölge +
  dönen **conic glow** ile öne çıkar; mobilde gizlenip sağ-altta "☰ Bölümler" FAB + sheet ile açılır.
- **ToC ekrana dikey SIĞMALI (önemli):** ToC bölüm sayısı arttığında ekrandan taşmamalı. `.sidenav`
  `max-height:calc(100vh - 92px)` + `display:flex;flex-direction:column` olur; **bölüm linkleri
  `<div class="toc-scroll">…</div>` içine sarılır** ve bu sarmalayıcı `overflow-y:auto;min-height:0`
  ile kendi içinde kayar (başlık `<h4>` sabit kalır). Böylece conic glow korunur, liste taşmaz.
  `assets/report-shell.css` bu kuralları içerir; markup'ta linkleri `.toc-scroll` ile sarmayı unutma.
- **Header (appbar · AÇIK zemin, LOGOLU):** SOL'da **hedef markanın logosu** (inline SVG ya da asset) +
  marka adı + "Rakip Analizi & SEO / GEO Değerlendirmesi" alt başlığı; SAĞ'da tarih çipi, "Hedef: <path>"
  ve **Inbound wordmark** (`assets/inbound-wordmark.png`). Logo HER ZAMAN eklenir (ikisi de). `.appbar` sınıfı.
- **Arka plan kağıt-gri** (`--bg`); kartlar beyaz + çerçeve + gölge ile ayrışır.
- **Kartlar/karoseller:** çerçeve + gölge; üstüne gelince hafif lift. TEK-KENAR şerit/parantez yok (aşağıya bak).
- **Akıcı, büyük-okunur tipografi:** kök font `clamp(16px,0.45vw+14.5px,18.5px)` (turkcell-one okunabilirliği).
- **Lightbox:** her ekran görüntüsü tıklanınca tam ekran açılır (`data-full` + `data-cap`).
- **Term tooltip:** `.term[data-term]` → ekranın üstüne çıkan, ekrana sığan, ortalanmış,
  tüm elementlerin üstünde (z-index yüksek) tooltip; hover + tıkla ile açılır.
- **Grafikler:** Chart.js (donut/bar/line) ile ton dağılımı, content gap, trends, görünürlük.

## Bölüm seti (hedef sayfaya göre uyarlanır)

Sıra ve içerik mevcut yapıyı izler; gereksiz bölüm atlanabilir, sayfa tipine göre vurgular değişir:

1. **Yönetici Özeti** · 3 öne çıkan kart (mevcut durum / en büyük fırsat / öncelikli aksiyon) +
   KPI gösterge paneli (organik sıra, content gap kelime sayısı, en yüksek hacimli fırsat + KD,
   AI Overview durumu, vb.) + öne çıkanlar listesi.
2. **Yöntem & Kapsam** · veri kaynakları (DataForSEO + Ahrefs + canlı SERP/AI Overview + Trends),
   rakip seti, şeffaflık notu. **Tarih ve kaynak burada bir kez** geçer.
3. **Ürün / Sayfa Yapısı** · hedef sayfanın/ürünün yapısı (paketler, kademeler, fiyat, kapsam).
4. **SERP & Görünürlük** · doğrulanmış, **tıklanabilir** SERP tablosu (sıra/sonuç/sahip/tip/bağlantı)
   + canlı SERP ekran görüntüleri + PAA + sayfa rol haritası/kanibalizasyon notu.
5. **AI Overview & GEO** · AI Overview bulgusu (kaynak dağılımı, tanım alıntısı, mention durumu) +
   **GEO yol haritası** (alıntılanabilir tanım, eksiksiz FAQPage, machine-readable karşılaştırma
   tablosu, değer bloğu, 40-60 kelimelik alıntılanabilir pasaj, robots.txt GPTBot/Google-Extended/
   PerplexityBot + llms.txt, publisher mention, dateModified tazeliği).
5b. **Rakip Boşluk Analizi** · rakiplerin trafik aldığı, hedefin almadığı/zayıf olduğu KELİME tablosu
   (hacim/KD/rakip sırası/hedef sırası/durum) + İÇERİK-MODÜL gap tablosu (rakipte var/hedefte yok) +
   FAQ gap listesi. Veri: Ahrefs organic-keywords karşılaştırması (bkz. 01 madde 11). Bu bölüm,
   içerik brief'inin (aşağıda) gerekçesidir.
6. **Talep Havuzu & Content Gap** · hacim/KD/rakip/fırsat tablosu + "hangi sorgu → hangi rakip URL"
   doğrulanmış, tıklanabilir tablo + ilgili ekran görüntüleri.
7. **Rakip İçerikte Neler Var** · karşılaştırma matrisi (marka vs rakipler) + editöryel liderler +
   operatör/sektör rakipleri (ekran görüntüleri **hizalı** bir satırda).
8. **Google Trends** · zaman içinde ilgi + yükselen sorgular/konular (split düzen).
9. **Sosyal Duygu** · ton dağılımı grafiği + **gruplanmış** kartlar (Olumlu / Soru / Geri bildirim) +
   "İlgili ekran görüntüleri" (X/Ekşi vb. · bkz. 05 kaydırmalı karosel) + Şikayetvar sinyali.
10. **Kullanıcı Soruları & İçerik Eşleşmesi** · küme/örnek soru/yanıt yeri/FAQ adayı tablosu.
11. **CRO / CX / UI-UX** · hedef sayfa (birincil) + (varsa) ikincil sayfa gözlemleri; tasarım
    önerisi + **tasarım örneğinin canlı/önizleme linki** ve 4 varyanttan bahis (bkz. 03).
12. **Teknik · Hız · fast.com** · (A) On-page (SEO) denetim tablosu · (B) **ölçülen** CWV tablosu
    (Lighthouse + gerçek tarayıcı; LCP/CLS/TBT/TTI/TTFB/ağırlık, gözlem tarihli, hedge yok) · (C) sayfa
    hızı & gömülü iframe için **preconnect/facade/3.taraf erteleme** önerileri · (D) varsa fast.com tarzı
    **otomatik-başlatma** mekaniğinin sayfa için değerlendirmesi. On-page ile CWV'yi **ayır**.
13. **Aksiyon & Öneriler** · sekmeler: **SEO/Teknik · İçerik & FAQ · GEO · CRO/Dönüşüm · Core Web Vitals**.
    Kaynak etiketleri: `★ önceden iletildi` / `+★ geliştirilmiş` / `Yeni` / `✓ uygulandı` ile raporun
    özgün katkısını ayır; bir lejant ekle.
13b. **İçerik Yazım Brief'i** · DETAYLI ve uygulamaya hazır (boşluk analizini kapatır). En az şunları içerir:
    (1) **Başlık + meta** (≤60 / ≤155 krk) + H1; (2) **başlık hiyerarşisi tablosu** (H1/H2/H3 · her başlık
    altında ne olacak · hedef kelime); (3) **kelime kullanım yoğunluğu tablosu** (birincil/ikincil kelime ·
    kaç kez · nerede); (4) **eklenecek tablolar** (hız-ihtiyaç eşleme, indirme süresi vb.); (5) **eklenecek/
    cevaplanacak FAQ listesi**; (6) **özet/giriş bölümünde ne olmalı**; iç link + schema. Hedef kelimeleri
    ÜÇ katmanda ver: **ana hacim · rakip boşluğu · uzun kuyruk (long-tail)**; başlık hiyerarşisi tablosunda
    her başlık için long-tail/rakip kelime örnekleri ekle. (Brief üretilirken ilgili SEO skill'leri DAHİLİ
    kullanılır; **skill/araç/Claude adları rapora YAZILMAZ** · bkz. SKILL.md "Teslimat dili kuralı".)
14. **Geliştirme Alanları** · mevcut sayfalara eklenebilir bloklar + fırsat skoru tablosu.
15. **Terim Sözlüğü & Kaynaklar** · `data-term` ile işaretlenen tüm terimlerin kısa tanımı + kaynak
    linkleri + footer (tek tarih/kaynak damgası).

## Marka rengi uyarlama (önemli)

`assets/report-shell.css` tüm renkleri CSS değişkeniyle tutar. Markaya uyarlarken **yalnız token'ları**
değiştir; yapıyı bozma:
- `--accent` / `--accent-deep` / `--accent-soft` → markanın **vurgu** rengi (CTA, eyebrow, accent line,
  hover glow, conic glow). Mevcut işteki coral'in yerini alır.
- `--brand` / `--brand-deep` → markanın koyu/kurumsal rengi (header, başlıklar). Mevcut dark teal /
  navy yerini alır.
- Gövde metni daima koyu nötr (`--ink`), zemin beyaz. **Okunabilirlik kontrastını koru** (WCAG AA).
- Marka rengi çok açık veya çok doygunsa: rengi yalnız accent/şerit/rozet olarak kullan, geniş
  zeminlerde değil. Gerekirse koyu bir varyantını üret (`--brand-deep`).
- Inbound wordmark/logosu marka logosuyla değiştirilebilir; değişmezse Inbound imzası kalır (ajans
  çıktısı olduğu için kabul edilebilir · kullanıcıya teyit ettir).

## Görselleştirme ve okunabilirlik
- **Zemin kağıt-gri; her blok NET ayrışır (zorunlu).** Sayfa zemini hafif gri (`--bg`), kartlar beyaz +
  **çerçeve + belirgin gölge**. Kart, callout, insight, tablo sarmalayıcı, grafik kartı, ss kartı, brief
  kartı · hiçbiri düz/çerçevesiz kalmaz. **Section ve tab çerçeveleri belirgin** (1.5px).
- **TEK-KENAR şerit / parantez YASAK · çok önemli (kullanıcı iki kez reddetti).** Yuvarlatılmış karta ne
  `border-left`/`border-right`, **ne de üst renkli ince bant** (`::before` şerit) koy · ikisi de köşe
  yarıçapını izleyip parantez/yay görünümü verir. Vurgu için referans bileşen menüsünden **TAM çerçeveli**
  stil seç: **Yumuşak Glow** (tam çerçeve + accent glow), **Dolu Panel** (tonlu dolgu), **Pill Başlık**,
  **Köşe İkon Rozeti**, **Çift Çerçeve**, **iOS Soft Kart**. Conic-arc kenar da yasak. `.insight` artık
  Yumuşak Glow (tam çerçeve + glow) kullanır.
- **Karosel/vurgu renkleri hedef sitenin tema ve renkleriyle uyumlu olur** (tokenlar `--accent`/`--brand`
  hedef markaya ayarlanır); referans paletini kopyalama.
- **Başlıklar nötr ve net** (devrik/jargonlu değil); gereksiz niteleyici yok ("Yapılacaklar · işaretli ve
  önceliklendirilmiş" değil "Yapılacaklar"). **"Kanıt" sözcüğü kullanma**; "ekran görüntüsü/örnek" yeterli.
- Uzun "okuma" callout'larını kısa madde imlerine indir.
- Tablolar `.table-wrap` içinde, başlık satırı koyu, satırlar alternatif zebra, gölgeli.
- Grafik kartları (`.chart-card`) açıklayıcı alt başlık + gölge + hover glow.
- Ekran görüntüleri `shot-grid` içinde; benzer alanların ss'leri **aynı hizada** (ayrı hizalı satır).
- KPI kartları: büyük değer (accent) + etiket + alt not.

## QA (üretimden sonra)
`python3 -m http.server` ile servis et, Playwright ile bölümleri gez ve ekran görüntüsü al. Kontrol:
em-dash 0, kırık görsel 0, tooltip çözülüyor, ToC glow/FAB çalışıyor, tablolar hizalı, mojibake
(UTF-8 dışı `Ã`, `Ä±` vb.) yok. Mojibake bulursan kaynağı düzelt (genelde sed/perl UTF-8 hatası).
- **Mobil YATAY TAŞMA kontrolü (zorunlu):** 375px viewport'ta Playwright ile
  `document.documentElement.scrollWidth === clientWidth` doğrula (taşma OLMAMALI). Taşma varsa neden
  genelde grid `1fr` track'inin min-content ile şişmesidir → `main` ve grid çocuklarına `min-width:0`,
  `body/html`'e `overflow-x:hidden` (report-shell.css'te var). Taşan elemanı bul:
  `[...document.querySelectorAll('*')].filter(e=>e.getBoundingClientRect().right>innerWidth+1)`.
- **Mobil ToC bottom-sheet:** mobilde "☰ Bölümler" FAB'ı `.toc-sheet` alt-sayfasını açar (sadece
  scroll değil); sheet tüm bölümleri listeler, linke/backdrop/ESC ile kapanır. Masaüstünde sheet gizli.
- **Kısa viewport:** ~620px yükseklikte ToC ekrana sığar ve `.toc-scroll` içinde kayar (taşma yok).
- Playwright ile 375px (mobil) + 1366px (masaüstü) ekran görüntüsü al; parantez/taşma/okunabilirlik doğrula.
- **Deploy uyumu:** çıktı Vercel (statik) ve Railway (node) için hazır olmalı; bkz. `references/06-deploy.md`.
