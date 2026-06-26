# 01 · Araştırma reçetesi

Amaç: hedef sayfanın ve hedef kelimenin SEO + GEO + rakip + talep + sosyal görünümünü kanıta dayalı
toplamak. Tüm sayılar **doğrulanmış** olmalı; uydurma yok. Bir veri alınamazsa rapora "gözlem
alınamadı" yaz ve gerekiyorsa kullanıcıdan iste (05).

## Araç haritası (varsa kullan, yoksa graceful düş)

- **DataForSEO** (`mcp__dfs-mcp__*`): kelime hacmi (Google Ads), KD/niyet (Labs), canlı SERP
  (`serp_organic_live_advanced`), AI Overview (SERP item türü `ai_overview`), Google Trends, sayfa
  içi ölçüm (`on_page_instant_pages` / lighthouse). Lokasyon "Turkiye", dil "tr".
- **Ahrefs MCP**: çapraz doğrulama (keyword overview, organic keywords, SERP overview, site audit).
- **Chrome / Playwright**: canlı SERP + AI Overview gözlemi, rakip sayfa içeriği, ekran görüntüsü.
- Hiçbiri yoksa: canlı Chrome gözlemi + kullanıcıdan veri iste.

> Not: araç adları/erişimi değişebilir. Çağırmadan önce ToolSearch ile mevcut MCP araçlarını ara.
> Registry `mcp__dataforseo__*` kapalıysa `mcp__dfs-mcp__*` dene.

## Toplanacak veri blokları

1. **Hedef sayfa(lar) ve rol** · hedef sayfa + (varsa) aynı markanın rakip-içi sayfaları. Her birinin
   ana sorgudaki organik sırası ve rolü (hub=tanım, listeleme=karşılaştırma, detay=işlemsel).
2. **Ana sorgu SERP'i** · `serp_organic_live_advanced` ile **gerçek** ilk sayfa: her sonucun
   `title`, `url`, sahip, tip (Organik / PAA / UGC / Editöryel / Sosyal / Reklam). Markanın hangi
   sayfası kaçıncı? Rakipler kim? Tabloyu **tıklanabilir linklerle** kur. PAA sorularını da al.
3. **AI Overview / GEO** · "<kelime> nedir" ve ana sorgu için AI Overview var mı? Hangi kaynaklar
   birincil (mention)? Marka mention alıyor mu, yoksa yalnız "ziyaret et" adımında mı? Tanım
   alıntısını al. Kaynak dağılımı (hangi yayıncı ~%kaç) bir bulgu olarak ver.
4. **Talep havuzu / content gap** · hedef sayfanın/ürünün çevresindeki yüksek hacimli, düşük KD
   sorgular (fiyat / üyelik / paket / "nedir" türevleri). Her biri için hacim + KD + rakip
   görünürlüğü + fırsat etiketi. **Rakip kanıtı:** "şu sorgu → şu rakip URL (organik #N)" tablosunu
   canlı SERP ile doğrula ve linkle. (Eski işte: "netflix paketleri" → Vodafone #5, TT #7.)
5. **Rakip içerik** · ilk sayfadaki editöryel/rakip sayfaların yapısı (nedir tanımı, karşılaştırma
   tablosu, adımlar, geçiş senaryoları). Karşılaştırma matrisi: marka vs rakip içerik öğeleri.
6. **Google Trends** · ana sorgunun zaman içindeki ilgisi, zirve/lansman, yükselen sorgular ve
   konular, bölgesel ilgi.
7. **Sosyal duygu** · X, Ekşi, Şikayetvar vb. gerçek paylaşımlar/girdiler. Tonu grupla (Olumlu /
   Soru-kafa karışıklığı / Geri bildirim-kapsam). Gerçek kullanıcı adları + özet + öne çıkan nokta.
8. **On-page (SEO)** · Title/Meta/H1/H2, Schema (WebPage/Product/FAQPage), görsel alt/title, iç/dış
   link, içerik/okunabilirlik, breadcrumb. Bunları **CWV'den ayrı** raporla (on-page ≠ CWV).
9. **Core Web Vitals · GERÇEKTEN ölç (hedge yazma).** Sıralama:
   - **Lighthouse** (DataForSEO `on_page_lighthouse`) · LCP/FCP/CLS/TBT/TTI/Speed Index + performans skoru
     + toplam ağırlık + ana iş parçacığı/JS bootup + 3. taraf entity'ler. Lab referansı budur.
   - **PSI API** (`googleapis.com/pagespeedonline/v5`, mobile+desktop) · saha (CrUX) p75 + lab. Anahtarsız
     429 verirse Lighthouse + tarayıcı ölçümüne düş (durumu rapora değil, sohbette belirt).
   - **Gerçek tarayıcı** (Playwright) · PerformanceObserver ile LCP (+öğe), layout-shift (CLS),
     navigation timing (TTFB/FCP/DCL/load). "olmadı tarayıcı aç da ölç."
   - **Ahrefs Site Audit** (varsa) · sayfa/performans sorunları çapraz kontrol.
   - LCP/CLS/INP eşikleri: iyi LCP<2,5sn · CLS<0,1 · INP/TBT proxy<200ms. Embed/iframe sayfalarda
     LCP öğesini gerçek ölçümle tanımla; "ölçülemiyor" yazma.
   - Ayrıca: gömülü test alanının (iframe) **preload/preconnect/facade** ile hızlandırma önerileri;
     varsa fast.com tarzı **otomatik-başlatma** mekaniğinin bu sayfa için uygunluğunu değerlendir.
10. **CRO / CX gözlemi** · hedef sayfanın hero/CTA, karşılaştırma, değer bloğu, sosyal kanıt,
   mobil öncelik durumu · tasarım önerilerinin (03) dayanağı.
11. **RAKİP BOŞLUK (GAP) ANALİZİ · zorunlu, ayrı bölüm.** Rakiplerin trafik aldığı, hedef sayfanın
   almadığı/zayıf olduğu alanları çıkar:
   - **Kelime gap:** her rakip sayfası için Ahrefs `site-explorer-organic-keywords` (mode=exact, country)
     ile trafik getiren kelimeleri çek; hedef sayfanınkiyle karşılaştır. Rakip iyi sırada (top 1-3) ama
     hedef sıralamıyor/5+ ise BOŞLUK. (Alternatif: DataForSEO `dataforseo_labs_google_page_intersection`,
     pages=rakipler, exclude_pages=hedef.) Markalı rakip terimlerini ele.
   - **İçerik/modül gap:** rakip sayfalarda olup hedefte olmayan bölüm/modüller (tablo, hesaplayıcı,
     kampanya kartı, kılavuz). Round-1 rakip distilasyonundan türet.
   - **FAQ gap:** rakiplerin sorduğu, hedefin cevaplamadığı sorular.
   Bunları rapora **"Rakip Boşluk Analizi"** bölümü + `data/07-gap-analysis.md` olarak yaz; tabloyla göster.
12. **İçerik yazım brief'i · zorunlu, ayrı ve DETAYLI bölüm.** Boşlukları kapatacak uygulamaya hazır brief:
   başlık+meta (≤60/≤155 krk), **H1/H2/H3 hiyerarşisi** (her başlık altında ne olacak), **birincil/ikincil
   kelimeler ve kullanım yoğunluğu** (hangi kelime kaç kez, nerede), **eklenecek tablolar** (hız-ihtiyaç,
   indirme süresi vb.), **eklenecek/cevaplanacak FAQ listesi**, **özet/giriş içeriği**, iç link ve schema.
   Üretim/genişletme: `seo-meta-writer`, `seo-content`, `seo-geo`, `seo-schema`, `seo-cluster`,
   `youtube-content-research`. Rapora **"İçerik Yazım Brief'i"** bölümü olarak ekle.

## Çıktı: veri klasörü
Toplanan ham veriyi `<marka>-rapor-html/data/` altına JSON/MD olarak kaydet (keyword-metrics,
serp, ai-overview, trends, social, onpage, content-gap, FINDINGS.md). Rapor bu kanıttan beslenir.

## Doğrulama disiplini
- SERP sıralarını rapora yazmadan önce **canlı çağrıyla** doğrula; sıralar gün/saat değişir, gözlem
  tarihini not et.
- İki kaynak (DataForSEO vs Ahrefs) arasında hacim/KD farkı olabilir; birini esas al, diğerini
  çapraz okuma için sakla, bunu yöntem notunda **bir kez** belirt.
- Marka bundle/yeni ürün terimleri araç veritabanında düşük görünebilir; bu durumda analizi
  "içerdiği platformların / ilgili sorguların talep havuzu" üzerinden derinleştir ve bunu açıkla.
