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

Bu skill canlı veriye, MCP araçlarına ve birkaç yerel araç/kütüphaneye bağlıdır. İlke **ön-uçuş
(preflight)**: her bağımlılık, kullanım anından hemen önce **DENETLENİR** · varsa kullanılır · yoksa
edinim moduna göre **OTO-EDİNİLİR** · yine de edinilemiyorsa graceful şekilde düşülür ve eksik olan
tek mesajda kullanıcıdan istenir. Edinim modu bağımlılığın tipine göre değişir ve birbirine
karıştırılmaz:

- **MCP araçları:** bağlı sunucunun şeması `ToolSearch` ile **YÜKLENİR** (bu kurulum değil, şema
  yüklemesidir). Bağlı olmayan sunucu **kurulamaz**; yalnızca registry'de aranır, `authenticate`
  tetiklenir ve kullanıcıya bağlaması/onaylaması bildirilir.
- **Python/Node paketleri (Pillow, pptxgenjs):** `pip` / `npm` ile **KURULUR**.
- **DS bundle / clone-website:** sırasıyla **İNDİRİLİR** / `Skill` aracı ile çağrılır.

Hangi kaynaktan ne alındığı (ör. ToolSearch ile yüklenen MCP şeması, pip ile kurulan Pillow, indirilen
DS bundle) rapora **bir kez** yazılır: yöntem notu bölümünde ve footer'da.

**Önemli sınır:** bir skill, kimlik bilgisi gerektiren / uzak bir MCP sunucusunu **sessizce kuramaz**.
Bağlı (installed) bir sunucunun şeması `ToolSearch` ile yüklenir (bu kurulum değil, şema yüklemesidir)
ve araçlar doğrudan çağrılır; bağlı olmayan sunucu için yalnızca registry'de aranır, `authenticate`
tetiklenir ve kullanıcıya bağlaması/onaylaması bildirilir.

**MCP araçları · DataForSEO, Ahrefs, Playwright, Chrome**

- **Ne için:** SEO/GEO verisi (DataForSEO: SERP, keyword, on-page · Ahrefs: backlink, organic), sayfa
  render ve görsel QA (Playwright / Chrome).
- **Oto-edinme (bağlıysa):** Araçlar çoğu zaman *deferred* gelir (var, şema yüklenmemiş). Kullanmadan
  önce `ToolSearch` çağrılır: `select:<tam_arac_adi>` veya anahtar kelime sorgusu ile **bağlı
  sunucunun şeması yüklenir**, sonra araç normal çağrılır. Namespace'ler: DataForSEO için
  `mcp__dataforseo__*` / `mcp__dfs-mcp__*`, Playwright için `mcp__plugin_playwright_playwright__*`,
  Chrome için `mcp__Claude_in_Chrome__*` / `mcp__Control_Chrome__*`. Ahrefs'te kimlik doğrulama yüzeyi
  `mcp__plugin_marketing_ahrefs__authenticate` / `__complete_authentication` namespace'indedir; Ahrefs
  veri araçları (site-explorer, keywords-explorer vb.) ise bağlı Ahrefs sunucusunun kendi namespace'i
  altında ToolSearch ile yüklenir.
- **Bağlı değilse:** ToolSearch sorgusu araç döndürmüyorsa sunucu bağlı değildir.
  `mcp__mcp-registry__search_mcp_registry` (veya `suggest_connectors` / `list_connectors`) ile aranır;
  varsa `authenticate` / `complete_authentication` (ör. `mcp__plugin_marketing_ahrefs__authenticate`)
  tetiklenip OAuth başlatılır ve kullanıcıya **bağlaması/onaylaması** bildirilir. Sunucu sessizce
  kurulmaz.
- **Fallback:** DataForSEO/Ahrefs yoksa rapor, kullanıcının sağladığı mevcut SEO dokümanı ve canlı
  sayfa (Playwright/Chrome) ile yetinen sınırlı kapsamda hazırlanır; eksik veri kaynağı rapora not
  düşülür. Playwright/Chrome de yoksa görsel QA atlanır ve durum kullanıcıya bildirilir.

**Python + Pillow**

- **Ne için:** ekran görüntüsü kırpma/ölçekleme, görsel kompozisyon, rapor/sunum görsellerinin işlenmesi.
- **Oto-kurulum (Bash):** `python3 -c "import PIL" 2>/dev/null || python3 -m pip install --quiet --user pillow`.
  Aynı desen herhangi bir pip bağımlılığı için geçerlidir.
- **Fallback:** kurulum başarısızsa görsel işleme adımı atlanır, ham ekran görüntüleri kullanılır ve
  durum not edilir.

**Inbound Design System bundle (yalnızca sunum istenirse)**

- **Ne için:** marka token'ları, fontlar (Bricolage Grotesque · Outfit), logolar, örnek slide ve UI kit'leri.
- **Oto-indirme (Bash):** `[ -d /tmp/inbound-ds ] || { curl -s -o /tmp/inbound-ds.gz "https://api.anthropic.com/v1/design/h/5vYshIIlcSgmneND7nN7HQ"; mkdir -p /tmp/inbound-ds; tar -xzf /tmp/inbound-ds.gz -C /tmp/inbound-ds; }`.
  Ardından `README.md` ve `project/SKILL.md` okunur.
- **Fallback:** indirme başarısızsa marka token'ları kullanıcıdan istenir (renk/logo/font); sunum
  varsayılan nötr stille üretilir ve sapma not edilir.

**clone-website skill**

- **Ne için:** hedef sayfanın tasarım dilini (token, bileşen, asset) çıkarmak ve tasarım örneğini
  sadık biçimde yeniden kurmak.
- **Oto-edinme:** bir Skill'dir, `Skill` aracı ile `clone-website` çağrılır.
- **Fallback:** skill yoksa canlı **DOM/asset çıkarımına** (Playwright / Chrome) düşülür; token ve
  bileşenler doğrudan sayfadan toplanır.

**PPTX üretimi · Node + pptxgenjs**

- **Ne için:** sunum çıktısının `.pptx` olarak üretilmesi.
- **Oto-kurulum (Bash):** `node -e "require('pptxgenjs')" 2>/dev/null || npm install pptxgenjs`.
- **LibreOffice (opsiyonel):** pptx pixel-render QA için kullanılır; yoksa içerik `markitdown` ile,
  görünüm eşdeğer HTML deck ile QA edilir.
- **Fallback:** Node/pptxgenjs edinilemezse sunum HTML deck olarak teslim edilir ve pptx'in
  üretilemediği kullanıcıya bildirilir.

**Yerel HTTP sunucu**

- **Ne için:** HTML rapor/tasarım/deck çıktılarının yerel önizlemesi ve Playwright QA'i.
- **Edinme:** `python3 -m http.server` (stdlib, her zaman mevcuttur, kurulum gerekmez).

## Yazım ve görselleştirme kuralları (rapor + sunum + tasarım metinleri)

Bu kurallar mevcut işin damıtılmış halidir; `references/02-html-report.md` içinde örneklerle açılır.

- **Dil:** varsayılan Türkçe, pasif/3. tekil, kurumsal ton.
- **Em-dash (—) YASAK · çok önemli.** Hiçbir çıktıda uzun tire bulunmamalı; yerine `·`, `,`, `-` veya `&`.
  **Teslimden hemen önce SON KONTROL:** tüm üretilen dosyalarda `grep -rn "—"` çalıştır; çıkan her `—`'yi temizle.
- **"Ölçülemiyor / atfı net değil" gibi ifadeler raporda YASAK.** Rapor markaya gider; bir metrik
  ölçülemediyse hedge cümlesi yazma · ya gerçekten ölç (Lighthouse/PSI/CrUX, gerekiyorsa tarayıcı aç),
  ya da ölçemiyorsan bunu **rapora değil, sohbette kullanıcıya** bildir ("şu veriyi ölçüp iletmem
  gerekiyor"). Raporda yalnızca ölçülmüş, gözlem tarihli gerçek değerler yer alır.
- **Bloklar zeminden NET ayrışır.** Ya kart zemini sayfa zemininden farklı olsun, ya da her blok
  (kart, callout, insight, tablo sarmalayıcı, grafik kartı, ss kartı, brief kartı) **çerçeve + belirgin
  gölge** taşısın. Düz/çerçevesiz blok bırakma. Karosel/vurgu renkleri **hedef site temasına uyumlu**
  (tokenlar markaya ayarlı).
- **"Parantez" / sol-kenar / conic-arc süsleme YASAK (kullanıcı reddetti).** Yuvarlatılmış karta kalın
  `border-left`/`border-right` koyma · kenar köşeyi takip edip "(" parantez yaratır. Vurgu için **üst
  renkli bant** (`::before` height:4px), **tonlu dolu panel**, **pill başlık** veya **köşe rozet** kullan.
  Conic-gradient (transparent boşluklu dönen yay) kenar da yasak. Temiz `border` + yumuşak `box-shadow`.
- **MOBİL YATAY TAŞMA olmamalı (zorunlu).** Grid `1fr` track'leri min-content ile şişip taşma yaratır;
  `main` + grid çocuklarına `min-width:0`, `html/body`'ye `overflow-x:hidden` (report-shell.css'te var).
  Teslimden önce 375px'te `scrollWidth === clientWidth` doğrula. Mobilde ToC, FAB + `.toc-sheet`
  bottom-sheet ile açılır (sadece scroll değil).
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

**Deploy edilecekse (Vercel/Railway)** yapı değişir: **rapor köke** (`/index.html` + `assets/` +
`data/`), tasarım **`/demo`** altına **tek dosya self-contained** olarak alınır; köke `vercel.json`
(cleanUrls), `server.js` (sıfır-bağımlılık statik sunucu) ve `package.json` (`start: node server.js`)
eklenir. Detay ve şablonlar: `references/06-deploy.md`. Kökte `index.html` yoksa `/` boş görünür;
`/demo` göreli asset'leri kırarsa sayfa stilsiz "bozuk" gelir → demo tek dosya yapılır.

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
| `references/06-deploy.md` | Vercel + Railway deploy: kök index.html, /demo tek dosya, vercel.json/server.js/package.json + mobil QA |
| `assets/report-shell.css` | Raporun marka-token'lı temel CSS'i (başlangıç şablonu, ToC dikey-sığar) |

Önce `references/00-intake.md`'i oku ve intake kapısını uygula. Sonra sırayla ilerle.
