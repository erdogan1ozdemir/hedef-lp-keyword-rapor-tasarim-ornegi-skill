---
name: hedef-lp-rapor-tasarim
description: >-
  Tek bir hedef sayfa (landing page / hub / hizmet / listeleme / ürün-hizmet detay) ve hedef
  anahtar kelime alıp o sayfa için üç şey üretir: (1) SEO + GEO + rakip analizi HTML raporu,
  (2) hedef domainin header/navigasyon/footer'ını koruyup sayfa içi gövdeyi CRO/CX/UI-UX'e göre
  geliştiren, birden çok tasarım varyantı sunan HTML tasarım örneği, ve (3) talep edilirse Inbound
  Design System ile sunum. Mevcut Turkcell One çalışmasının jenerik, tekrar kullanılabilir hali.
  Bu skill'i ŞU durumlarda kullan: kullanıcı bir marka sayfası/LP verip "bu sayfa için SEO/GEO
  rapor + tasarım önerisi hazırla", "hedef kelime ile landing page analizi", "şu sayfayı CRO/UX
  varyantlarıyla yeniden tasarla", "marka sayfasını iyileştir, varyant öner", "rakip analizi raporu
  + tasarım örneği", "bu hub/listeleme/detay sayfası için tasarım varyantı" dediğinde · kullanıcı
  "rapor" ya da "tasarım" kelimesini açıkça söylemese bile, bir hedef URL + kelime verip o sayfanın
  SEO görünürlüğünü ve tasarımını birlikte ele almak istiyorsa tetikle. Tetikleyiciler: "hedef sayfa
  raporu", "LP analizi", "landing page tasarım önerisi", "sayfa için varyant tasarla", "CRO tasarım
  örneği", "SEO GEO rapor + tasarım", "marka sayfası iyileştirme".
---

# Hedef Sayfa · SEO/GEO Rapor + Tasarım Örneği + Sunum

Bu skill, **tek bir hedef sayfa** ve **bir hedef kelime** için danışmanlık paketi üretir. Eski
Turkcell One işinde iki sayfa (hub + listeleme) vardı ve listeleme için tasarım hazırlanmıştı; bu
skill o süreci **jenerikleştirir**: artık tek bir hedef sayfa verilir, o sayfa hem raporlanır hem de
listeleme örneğindeki gibi **tasarım varyantlarıyla** geliştirilir.

Üç çıktı vardır. **Rapor ve tasarım örneği her zaman üretilir; sunum yalnızca istenirse.**

1. **HTML rapor** · SEO + GEO + rakip + talep havuzu + sosyal duygu + CRO/CX bulguları. Görünüm
   olarak mevcut Inbound raporuyla birebir aynı tarzda; sadece renkler hedef markanın LP rengine
   uyarlanır (okunabilirlik korunarak). Bkz. `references/02-html-report.md`.
2. **HTML tasarım örneği** · hedef domainin **header / navigasyon / footer gibi değişmeyecek
   alanları korunur**, sayfa içi gövde CRO/CX/UI-UX'e göre yeniden tasarlanır; **4 varyant** ve
   sağda yüzen bir varyant seçici sunulur. Kullanıcı yine hedef domaindeymiş hissi korunur.
   Bkz. `references/03-html-design.md`.
3. **Sunum (opsiyonel)** · Inbound Design System (Bricolage + Outfit, coral #FF7B52 + dark teal
   #10332F) ile, raporun tüm bölümlerini yansıtan HTML deck. Bkz. `references/04-presentation.md`.

## En önemli kural: veri eksikse ÖNCE sor, sonra başla

Bu skill canlı sayfaya, rakip SERP'lerine ve marka görsellerine ihtiyaç duyar. Bir alanı kendin
alamayacaksan ya da veri eksikse, **işe başlamadan önce kullanıcıdan iste.** Yanlış varsayımla
ilerleyip baştan yapmak pahalıdır. Intake adımını atlama.

`references/00-intake.md` dosyasındaki **gereklilik listesini** oku ve eksik olanları kullanıcıya
tek mesajda, net biçimde sor. Zorunlu girdiler gelmeden araştırmaya/üretime geçme.

Zorunlu (bunlar olmadan başlama):
- **Hedef sayfa URL'i** (tek sayfa).
- **Hedef kelime** (bir veya birkaç; ana sorgu).
- **Hedef sayfa ekran görüntüleri** · masaüstü + mobil. Playwright/Chrome ile alabiliyorsan al;
  alamıyorsan (giriş duvarı, bot engeli, render sorunu) kullanıcıdan iste.

İsteğe bağlı ama varsa kaliteyi artırır (yoksa sor / varsay):
- **Marka rengi / logo** (rapor renk uyarlaması + tasarım klonu için). Sayfadan çıkarılabilir;
  belirsizse onayla.
- **Rakip seti** (yoksa SERP/AI keşfiyle türet).
- **Mevcut SEO/optimizasyon dokümanı** (varsa rapor "Doc'ta var / Analiz eki" ayrımı için).
- **Diller** (varsayılan Türkçe).
- **Sunum isteniyor mu?** (varsayılan: hayır · yalnızca rapor + tasarım).

## Akış (sırayla)

```
0. INTAKE      → gereklilikleri topla, eksikse sor (references/00-intake.md)
1. ARAŞTIRMA   → kelime/SERP/AI Overview/Trends/rakip/sosyal veri (references/01-research.md)
2. RAPOR       → HTML rapor, marka rengine uyarlanmış (references/02-html-report.md)
3. TASARIM     → hedef sayfa klon kabuğu + 4 gövde varyantı (references/03-html-design.md)
4. SUNUM       → istenirse Inbound DS deck (references/04-presentation.md)
5. GÖRSEL/EKSİK→ tamamlanamayan görselleri kullanıcıdan iste (references/05-screenshots-and-gaps.md)
6. TESLİM      → çıktıları özetle, canlı/önizleme linki ver, eksikleri listele
```

Her adımı bitirince çıktıyı **görsel olarak QA et** (yerel `python3 -m http.server` + Playwright ile
ekran görüntüsü). Üretimden önce ne göründüğünü doğrula; "tamam" demeden önce gör.

## Çalışma gereklilikleri (skill çalışırken)

- **MCP araçları:** DataForSEO (`mcp__dfs-mcp__*` veya registry) kelime hacmi/KD/SERP/AI Overview/
  Trends için; Ahrefs çapraz doğrulama için; Playwright/Chrome ekran görüntüsü + canlı gözlem için.
  Biri yoksa graceful düş: canlı Chrome gözlemi + kullanıcıdan veri iste. Hangi kaynaktan ne
  aldığını rapora **bir kez** (yöntem notu + footer) yaz, her bölüme tekrar damga **basma**.
- **Klonlama:** tasarım örneğinin kabuğu için `clone-website` skill'i veya canlı DOM/asset çıkarımı
  kullanılabilir. Header/nav/footer birebir; gövde özelleştirilir.
- **Sunum:** Inbound Design System bundle'ını çalışırken indir: `references/04-presentation.md`
  içindeki URL'den `tar -xzf` ile aç, README'sini oku, slayt şablonlarını kullan.
- **Görsel doğrulama:** Playwright ekran görüntüleri worktree köküne `./<dosya>.png` kaydeder; PIL
  (Pillow) ile kırpma/yeniden boyutlama yap. LibreOffice yoksa pptx pixel-render edilemez · HTML
  deck ile QA et.

## Yazım ve görselleştirme kuralları (rapor + sunum + tasarım metinleri)

Bu kurallar mevcut işin damıtılmış halidir; `references/02-html-report.md` içinde örneklerle açılır.

- **Dil:** varsayılan Türkçe, pasif/3. tekil, kurumsal ton. **Em-dash (uzun tire) kullanma**; yerine · veya virgül.
- **Kesin vaat / abartı yok:** "garanti, en iyi, kesinlikle" yerine "değerlendirilebilir,
  gözlemlenmektedir, fayda sağlayabilir".
- **Terimler orijinal dilde:** SEO jargonunu Türkçeleştirme. "atıf" yerine **mention**, "makine
  okunur" yerine **machine-readable**, "çapa" yerine **anchor / anchor text**, ayrıca SERP, AI
  Overview, GEO, KD, Content Gap, FAQPage, CWV/LCP/CLS/INP, AggregateOffer, long-tail. Her terimi
  `<span class="term" data-term="...">` ile işaretle; sayfanın üstüne çıkan, ekrana sığan bir
  tooltip ile tanım göster. Tüm terimler bir **Terim Sözlüğü** bölümünde toplanır.
- **Tarih damgalı, doğrulanmış veri:** rakip fiyat/paket ve SERP sıraları gözlem tarihiyle; SERP
  sıralarını DataForSEO ile **doğrula**, "şu sorgu → şu URL" tablolarını **tıklanabilir** ver.
- **Doğrulanamayan görsel = kullanıcıya sor.** Bkz. `references/05-screenshots-and-gaps.md`.

## Çıktı klasör yapısı

Çalışma klasörü altında (proje adıyla):
```
<proje>/
├── <marka>-rapor-html/      → index.html + assets/screenshots/ + data/
├── <marka>-tasarim-html/    → index.html (+ detay.html vb.) + style.css + app.js + assets/
├── <marka>-sunum/           → index.html (Inbound DS deck) + assets/  (istenirse)
└── CALISMA-TAKIP.md         → adım adım ne yapıldı, hangi veri nereden, eksikler
```

Teslimde her çıktının yolunu ve (varsa) canlı/önizleme linkini ver, raporda görsel olarak eksik
kalan ne varsa **net bir liste** halinde kullanıcıdan iste.

## Referans dosyaları

| Dosya | İçerik |
|---|---|
| `references/00-intake.md` | Gereklilik listesi + kullanıcıya sorulacak sorular + intake kapısı |
| `references/01-research.md` | DataForSEO/Ahrefs/SERP/AI Overview/Trends/sosyal araştırma reçetesi |
| `references/02-html-report.md` | Rapor bölümleri, şablon, marka rengi uyarlama, görselleştirme |
| `references/03-html-design.md` | Tasarım örneği: klon kabuk + 4 gövde varyantı + yüzen seçici |
| `references/04-presentation.md` | Inbound DS deck: indir, slayt eşleme, tema |
| `references/05-screenshots-and-gaps.md` | Ekran görüntüsü ihtiyaçları + eksikleri kullanıcıdan isteme |
| `assets/report-shell.css` | Raporun marka-token'lı temel CSS'i (başlangıç şablonu) |

Önce `references/00-intake.md`'i oku ve intake kapısını uygula. Sonra sırayla ilerle.
