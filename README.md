# hedef-lp-rapor-tasarim · Claude Code Skill

**Tek bir hedef landing page** alır, o sayfayı çevresindeki rekabet ortamıyla birlikte analiz eder ve üç çıktıyı tek akışta üretir: **SEO/GEO raporu**, **tasarım/CRO örnekleri** ve isteğe bağlı **sunum (PPTX)**. Hedef URL ve hedef kelime verildiğinde, ham veriyi toplamaktan rapor yazımına, tasarım mockup'larına ve teslime kadar uçtan uca ilerler.

Skill, tek bir sayfaya odaklanır: bütün bir siteyi taramak yerine **verilen URL'i + hedef kelimeyi** merkeze alır, rakip sayfaları aynı eksende karşılaştırır ve önerileri o sayfaya özel verir.

---

## Üç çıktı

| Çıktı | Ne içerir | Format |
|-------|-----------|--------|
| **1. SEO/GEO raporu** | Hedef kelime SERP konumu, AI Overview/GEO görünürlüğü, talep havuzu, rakip sayfa içerik kıyası, on-page + teknik bulgular, CWV, somut aksiyon listesi | Inbound brand kit'li **HTML rapor** |
| **2. Tasarım / CRO örnekleri** | Hedef sayfanın CRO/UX varyantları (yeniden tasarım örnekleri), rakip sayfa analizi, "mevcut vs önerilen" karşılaştırması, metodoloji notları | Bağımsız (self-contained) **responsive HTML mockup** + notlar |
| **3. Sunum** *(opsiyonel)* | Bulguların ve tasarım önerilerinin müşteriye sunum hâli | **PPTX** (pptxgenjs) |

Çıktı seti esnektir: kullanıcı sadece raporu, sadece tasarımı veya üçünü birlikte isteyebilir. Sunum yalnızca açıkça istendiğinde üretilir.

---

## Turkcell One bağlamı

Bu skill, Inbound ajansının **Turkcell One** (dijital abonelik bundle, ~Haz 2026 lansman) SEO/GEO danışmanlık işi için geliştirilen akışın genelleştirilmiş hâlidir. O işteki üç deliverable ile birebir aynı mantığı izler:

- **HTML rapor** → SERP, AI Overview/GEO, talep havuzu, rakip içerik, sosyal duygu, CRO, CWV, aksiyon bölümleri.
- **Paket/landing sayfaları** → canlı site klonu üzerinde CRO varyantları (A Zengin / B Sade / C Değer / D Detay tarzı) + sağ floating varyant seçici.
- **Sunum** → yalnızca PPTX (pptxgenjs `build-deck.js` deseni); HTML deck istenmediği sürece üretilmez.

Marka teması ve yazım kuralları Turkcell One işinden devralınır (aşağıdaki *Çıktı dili/stil* bölümüne bakın). Skill bu bağlamdan bağımsız da çalışır: herhangi bir markanın tek bir hedef sayfası için aynı akış kullanılabilir.

---

## Skill'i nasıl çalıştırırım

Skill, **SKILL.md açıklamasındaki tetikleyicilerle otomatik tetiklenir**: bir hedef URL + rapor/tasarım/sunum isteği geçen mesajlar bu skill'i açar. İstenirse **Skill aracıyla açıkça da çağrılabilir** (skill adı: `hedef-lp-rapor-tasarim`).

### Yazabileceğin somut örnek promptlar

Her örnek **tek hedef sayfa + hedef kelime** içerir; akışın geri dönüp soru sormasını en aza indirir. URL ve kelimeleri kendi işine göre değiştir.

```
Şu sayfa için SEO/GEO rapor + tasarım örneği hazırla.
URL: https://www.ornek.com/paketler/dijital-bundle · hedef kelime: dijital abonelik paketi
```

```
Bu landing page'i CRO/UX varyantlarıyla yeniden tasarla ve rakip analizi raporu çıkar:
https://www.ornek.com/kampanya/yaz-firsati · hedef kelime: yaz kampanyası
```

```
https://www.ornek.com/urun/aile-paketi sayfası için rapor + tasarım + sunum (pptx) hazırla;
hedef kelime: aile internet paketi · dil: Türkçe
```

```
hedef-lp-rapor-tasarim ile çalış: tek sayfa, sadece SEO/GEO raporu yeter (tasarım/sunum gerekmez).
URL: https://www.ornek.com/blog/rehber · hedef kelime: kurulum rehberi
```

> İlk üç örnek skill'i **otomatik** tetikler (URL + rapor/tasarım/sunum niyeti yeterli). Dördüncü örnek, skill'i **adıyla açıkça** çağırma biçimidir: tetikleme konusunda emin olmak istediğinde `hedef-lp-rapor-tasarim ile çalış` diye başla.

### Baştan verebileceğin bilgiler (geri-gidip-sormayı azaltır)

Akış eksik bilgiyi sorar; ama aşağıdakileri baştan verirsen üretime daha hızlı geçilir:

- **Hedef URL** *(zorunlu)* · analiz ve tasarımın merkezindeki tek sayfa.
- **Hedef kelime** *(zorunlu)* · SERP/GEO ve içerik kıyasının dayandığı ana terim.
- **Masaüstü + mobil ekran görüntüleri** · sayfanın mevcut hâli (login arkası / erişilemeyen sayfalar için kritik).
- **Marka rengi / logo** · tasarım örnekleri ve raporun markaya uygun çıkması için.
- **Rakip seti** · kıyaslanacak 3-4 sayfa/marka; verilmezse vertical'e göre önerilir.
- **Mevcut SEO dokümanı** · varsa anahtar kelime listesi, brief, önceki audit.
- **Sunum isteniyor mu?** · evet/hayır (varsayılan: hayır, yalnızca istenirse PPTX).
- **Dil** · çıktı dili (varsayılan: Türkçe).

---

## Nasıl çalışır

Akış kapı (gate) mantığıyla ilerler: **zorunlu girdiler gelmeden üretime geçilmez.** Aşamalar sırayla yürür ve her görsel adımda Playwright ile QA yapılır.

1. **Intake kapısı (zorunlu girdiler).** Hedef URL + hedef kelime + istenen çıktı seti (rapor / tasarım / sunum) + dil netleşene kadar **araştırma/üretim başlamaz.** Eksik olan tek tek sorulur; mesajdan veya hedef sayfadan çıkarsanabilen şeyler tekrar sorulmaz. Bu kapı, baştan eksik veriyle yanlış yöne gidilmesini engeller.
2. **Kullanıcı onayı.** Toparlanan brief (hedef sayfa, hedef kelime, rakip seti, çıktı seti, marka teması) kullanıcıya özetlenir; **ağır üretime geçmeden önce onay alınır.** Onay sonrası akış kesintisiz ilerler.
3. **Araştırma.** Hedef sayfa Playwright ile incelenir (design token'lar, header/footer, on-page sinyaller, mevcut görsel hâl). SERP/GEO ve talep verisi toplanır; rakip sayfalar aynı eksende kıyaslanır. Bu adım için gereken eksik araçlar/veri kaynakları **akış içinde yüklenir veya araştırılır** (aşağıdaki *Gereksinimler* bölümüne bakın).
4. **Rapor.** Toplanan veriden Inbound brand kit'li HTML rapor yazılır: SERP konumu, AI Overview/GEO görünürlüğü, talep havuzu, rakip içerik kıyası, on-page + teknik bulgular, CWV ve somut aksiyon listesi.
5. **Tasarım.** Hedef sayfanın tasarım dili klonlanır; CRO/UX varyantları bağımsız responsive HTML mockup olarak üretilir. "Mevcut vs önerilen" karşılaştırması ve metodoloji notları eklenir.
6. **Sunum *(opsiyonel)*.** Yalnızca istenmişse, bulgular ve tasarım önerileri PPTX'e dökülür (pptxgenjs). HTML deck istenmediği sürece üretilmez.
7. **Teslim.** Çıktılar tek tek listelenir; ilgili dosya yolları ve (varsa) repo/önizleme linkleri paylaşılır.

**Görsel QA (her adımda).** Üretilen her görsel çıktı (rapor sayfası, mockup, deck önizlemesi) **Playwright ile masaüstü + mobil ekran görüntüsü** alınarak kontrol edilir; bozuk/eksik render düzeltilir.

**Tamamlanamayan görseller.** Login arkası, erişim engelli veya teknik nedenle alınamayan ekran görüntüleri **net bir liste hâlinde** kullanıcıdan istenir; her madde için ilgili URL/link verilir, böylece kullanıcı eksik görseli kolayca sağlayabilir.

---

## Kurulum

Skill bir Claude Code skill'idir; skills dizinine kopyalanır (`SKILL.md` kökte olmalı):

```
~/.claude/skills/hedef-lp-rapor-tasarim/
├── SKILL.md                       # tetikleyiciler + tam çalışma akışı + çalışma gereklilikleri
├── README.md                      # bu dosya
├── references/
│   ├── 00-intake.md               # gereklilik toplama + kullanıcıya sorular
│   ├── 01-research.md             # DataForSEO/Ahrefs/SERP/AI Overview/Trends/sosyal araştırma
│   ├── 02-html-report.md          # rapor bölümleri, marka rengi uyarlama, görselleştirme
│   ├── 03-html-design.md          # tasarım örneği: klon kabuk + 4 varyant + yüzen seçici
│   ├── 04-presentation.md         # Inbound Design System deck (indir, slayt eşle)
│   └── 05-screenshots-and-gaps.md # ekran görüntüsü ihtiyaçları + eksikleri kullanıcıdan isteme
└── assets/
    └── report-shell.css           # raporun marka-token'lı temel CSS'i
```

Kurulumdan sonra skill, tetikleyici ifadelerle otomatik açılır veya Skill aracıyla `hedef-lp-rapor-tasarim` adıyla çağrılır.

---

## Gereksinimler (çalışırken)

Skill, çalışmak için bazı dış araçlara ve varlıklara ihtiyaç duyar. **Eksik olanların çoğu akış içinde yüklenir/araştırılır**; kullanıcının elle kurulum yapması genelde beklenmez, yalnızca bağlantı/yetki gerektiren adımlar onay isteyebilir. Ayrıntı SKILL.md'nin **"Çalışma gereklilikleri"** bölümündedir.

- **MCP araçları (DataForSEO SERP/keyword, Ahrefs backlink, Playwright, Chrome vb.).** Gerekli MCP araçlarının şemaları **ToolSearch ile yüklenir**; bağlantı/yetki gerektiren MCP'ler **registry + authenticate akışıyla bağlanır**. MCP'ler otomatik *kurulmaz*: bağlantı veya yetki adımı kullanıcı onayı isteyebilir. Skill ihtiyaç duyduğu araç ailesini belirler, yükler ve gerekiyorsa bağlanır.
- **Pillow (görsel işleme).** Gerektiğinde **pip ile otomatik kurulur.**
- **pptxgenjs (yalnızca sunum istenirse).** Gerektiğinde **npm ile otomatik kurulur.**
- **Inbound design system bundle (brand kit / tema).** Gerektiğinde **otomatik indirilir.**
- **Playwright (görsel QA).** Ekran görüntüleri ve render kontrolü için kullanılır; eksik tarayıcı bağımlılıkları akış içinde tamamlanır.

Bir gereksinim sağlanamazsa (ör. bağlantı yetkisi verilmemiş bir MCP), skill bunu **açıkça bildirir** ve ya alternatif bir veri kaynağına geçer ya da kullanıcıdan gereken erişimi ister; sessizce yanlış veriyle ilerlemez.

---

## Çıktı dili / stil

Varsayılan dil **Türkçe**'dir (kullanıcı başka dil isterse ona uyulur). Yazım kuralları kesin:

- **Uzun tire (em-dash) yasak** → yerine `·` veya virgül.
- **Pasif, 3. tekil** anlatım.
- **Kesin vaat / abartı yok** (abartılı metrik, garanti dili kullanılmaz).
- **Tarih / kaynak damgası bir kez** (yöntem + footer'da), tekrar edilmez.
- **SEO terimleri orijinal dilde:** "atıf" yerine **mention**, "makine okunur" yerine **machine-readable**, "çapa" yerine **anchor**; ayrıca SERP, AI Overview, GEO, KD, Content Gap, CWV/LCP/CLS/INP, FAQPage. Terimler `data-term` ile işaretlenir ve **Terim Sözlüğü** bölümünde toplanır.
- Tema: **Inbound coral `#FF7B52` + dark teal `#10332F`**, **Outfit + Bricolage** font ailesi.

Tasarım örnekleri ve raporlar, kullanıcı bir marka teması (renk/logo) verdiğinde o markaya uyarlanır; vermediğinde Inbound brand kit'i kullanılır.

---

## Lisans

İç kullanım (Inbound). Üretilen rapor, tasarım ve sunum çıktıları ilgili müşteri işine aittir.
