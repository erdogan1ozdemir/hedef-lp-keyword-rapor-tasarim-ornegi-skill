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
8. **Sayfa içi & CWV** · Title/Meta/H1/H2, Schema (WebPage/Product/FAQPage), görsel alt metin,
   LCP/CLS/INP işaretleri (TTI/DOM proxy), iç bağlantı, onpage skoru. CrUX/PSI ile teyit önerisi notu.
9. **CRO / CX gözlemi** · hedef sayfanın hero/CTA, karşılaştırma, değer bloğu, sosyal kanıt,
   mobil öncelik durumu · tasarım önerilerinin (03) dayanağı.

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
