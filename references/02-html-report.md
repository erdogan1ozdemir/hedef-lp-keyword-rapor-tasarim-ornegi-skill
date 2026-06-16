# 02 · HTML rapor

Tek dosyalık (self-contained) HTML rapor. Görünüm mevcut Inbound raporuyla **birebir aynı tarz**;
yalnız renkler hedef markanın LP rengine uyarlanır (okunabilirlik korunarak). Başlangıç stili için
`assets/report-shell.css`'i kullan (CSS değişkenleriyle tokenlanmış).

## Genel kabuk

- **İki sütun:** solda yapışkan **ToC (Bölümler)** + sağda içerik. ToC biraz sola taşınır, gölge +
  dönen **conic glow** ile öne çıkar; mobilde gizlenip sağ-altta "☰ Bölümler" FAB + sheet ile açılır.
- **Header:** marka adı + "Rakip Analizi & SEO / GEO Değerlendirmesi" + tarih çipi + "Hedef: <path>"
  + Inbound wordmark.
- **Kartlar/karoseller:** gölgeli; üstüne gelince coral/accent **highlight glow** (hover lift).
- **Responsive, büyük-okunur tipografi** (gövde ~1.02rem / 1.65).
- **Lightbox:** her ekran görüntüsü tıklanınca tam ekran açılır (`data-full` + `data-cap`).
- **Term tooltip:** `.term[data-term]` → ekranın üstüne çıkan, ekrana sığan, ortalanmış,
  tüm elementlerin üstünde (z-index yüksek) tooltip; hover + tıkla ile açılır.
- **Grafikler:** Chart.js (donut/bar/line) ile ton dağılımı, content gap, trends, görünürlük.

## Bölüm seti (hedef sayfaya göre uyarlanır)

Sıra ve içerik mevcut yapıyı izler; gereksiz bölüm atlanabilir, sayfa tipine göre vurgular değişir:

1. **Yönetici Özeti** — 3 öne çıkan kart (mevcut durum / en büyük fırsat / öncelikli aksiyon) +
   KPI gösterge paneli (organik sıra, content gap kelime sayısı, en yüksek hacimli fırsat + KD,
   AI Overview durumu, vb.) + öne çıkanlar listesi.
2. **Yöntem & Kapsam** — veri kaynakları (DataForSEO + Ahrefs + canlı SERP/AI Overview + Trends),
   rakip seti, şeffaflık notu. **Tarih ve kaynak burada bir kez** geçer.
3. **Ürün / Sayfa Yapısı** — hedef sayfanın/ürünün yapısı (paketler, kademeler, fiyat, kapsam).
4. **SERP & Görünürlük** — doğrulanmış, **tıklanabilir** SERP tablosu (sıra/sonuç/sahip/tip/bağlantı)
   + canlı SERP ekran görüntüleri + PAA + sayfa rol haritası/kanibalizasyon notu.
5. **AI Overview & GEO** — AI Overview bulgusu (kaynak dağılımı, tanım alıntısı, mention durumu) +
   **GEO yol haritası** (alıntılanabilir tanım, eksiksiz FAQPage, machine-readable karşılaştırma
   tablosu, değer bloğu, 40-60 kelimelik alıntılanabilir pasaj, robots.txt GPTBot/Google-Extended/
   PerplexityBot + llms.txt, publisher mention, dateModified tazeliği).
6. **Talep Havuzu & Content Gap** — hacim/KD/rakip/fırsat tablosu + "hangi sorgu → hangi rakip URL"
   doğrulanmış, tıklanabilir tablo + ilgili ekran görüntüleri.
7. **Rakip İçerikte Neler Var** — karşılaştırma matrisi (marka vs rakipler) + editöryel liderler +
   operatör/sektör rakipleri (ekran görüntüleri **hizalı** bir satırda).
8. **Google Trends** — zaman içinde ilgi + yükselen sorgular/konular (split düzen).
9. **Sosyal Duygu** — ton dağılımı grafiği + **gruplanmış** kartlar (Olumlu / Soru / Geri bildirim) +
   "İlgili ekran görüntüleri" (X/Ekşi vb. — bkz. 05 kaydırmalı karosel) + Şikayetvar sinyali.
10. **Kullanıcı Soruları & İçerik Eşleşmesi** — küme/örnek soru/yanıt yeri/FAQ adayı tablosu.
11. **CRO / CX / UI-UX** — hedef sayfa (birincil) + (varsa) ikincil sayfa gözlemleri; tasarım
    önerisi + **tasarım örneğinin canlı/önizleme linki** ve 4 varyanttan bahis (bkz. 03).
12. **Sayfa İçi & CWV** — denetim tablosu (öncelik etiketli) + ölçüm seti (onpage skoru, Title/Meta
    krk, H2 sayısı, script, görsel alt metin, TTI/DOM) + CrUX/PSI teyit notu.
13. **Aksiyon & İçerik Brief** — sekmeler: **Teknik · İçerik & PAA · CRO/CX/UI-UX · Core Web Vitals
    · Örnek İçerik Brief**. Mevcut SEO dokümanı varsa kaynak etiketi: `Doc'ta var` (gri) / `Doc + ek`
    (amber) / `Analiz eki` (coral) ile raporun özgün katkısını ayır; bir lejant + açıklama ekle.
14. **Geliştirme Alanları** — mevcut sayfalara eklenebilir bloklar + fırsat skoru tablosu.
15. **Terim Sözlüğü & Kaynaklar** — `data-term` ile işaretlenen tüm terimlerin kısa tanımı + kaynak
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
  çıktısı olduğu için kabul edilebilir — kullanıcıya teyit ettir).

## Görselleştirme ve okunabilirlik
- Uzun "okuma" callout'larını kısa madde imlerine indir.
- Tablolar `.table-wrap` içinde, başlık satırı koyu, satırlar alternatif zebra, gölgeli.
- Grafik kartları (`.chart-card`) açıklayıcı alt başlık + gölge + hover glow.
- Ekran görüntüleri `shot-grid` içinde; benzer alanların ss'leri **aynı hizada** (ayrı hizalı satır).
- KPI kartları: büyük değer (accent) + etiket + alt not.

## QA (üretimden sonra)
`python3 -m http.server` ile servis et, Playwright ile bölümleri gez ve ekran görüntüsü al. Kontrol:
em-dash 0, kırık görsel 0, tooltip çözülüyor, ToC glow/FAB çalışıyor, tablolar hizalı, mojibake
(UTF-8 dışı `Ã`, `Ä±` vb.) yok. Mojibake bulursan kaynağı düzelt (genelde sed/perl UTF-8 hatası).
