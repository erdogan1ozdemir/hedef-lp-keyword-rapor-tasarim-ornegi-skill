# hedef-lp-rapor-tasarim · Claude Code Skill

Tek bir **hedef sayfa** (landing page / hub / hizmet / listeleme / ürün-hizmet detay) ve bir **hedef
anahtar kelime** alıp o sayfa için danışmanlık paketi üreten bir Claude Code skill'i:

1. **HTML rapor** Â· SEO + GEO + rakip + talep havuzu + sosyal duygu + CRO/CX bulguları. Inbound
   raporuyla aynı tarz; renkler hedef markaya uyarlanır.
2. **HTML tasarım örneği** Â· hedef domainin header/nav/footer'ı korunur, sayfa içi gövde CRO/CX/UI-UX'e
   göre **4 varyant** + sağda yüzen varyant seçici ile geliştirilir.
3. **Sunum (opsiyonel)** Â· Inbound Design System ile, raporun tüm bölümlerini yansıtan deck.

Bu skill, Turkcell One çalışmasının (rapor + paket listeleme tasarımı + sunum) jenerik, tekrar
kullanılabilir halidir. Orada iki sayfa vardı ve listeleme için tasarım yapılmıştı; burada **tek bir
hedef sayfa** verilir ve o sayfa aynı yaklaşımla raporlanıp tasarım varyantlarıyla geliştirilir.

## Kurulum
Bu repoyu bir Claude Code skill dizinine klonla (ör. `~/.claude/skills/hedef-lp-rapor-tasarim/`) veya
bir plugin'in `skills/` klasörüne koy. `SKILL.md` kökte olmalı.

```
hedef-lp-rapor-tasarim/
├── SKILL.md                      # orkestrasyon + tetikleme tanımı
├── references/
│   ├── 00-intake.md              # gereklilik toplama + kullanıcıya sorular
│   ├── 01-research.md            # DataForSEO/Ahrefs/SERP/AI Overview/Trends/sosyal araştırma
│   ├── 02-html-report.md         # rapor bölümleri, marka rengi uyarlama, görselleştirme
│   ├── 03-html-design.md         # tasarım örneği: klon kabuk + 4 varyant + yüzen seçici
│   ├── 04-presentation.md        # Inbound Design System deck (indir, slayt eşle)
│   └── 05-screenshots-and-gaps.md# ekran görüntüsü ihtiyaçları + eksikleri kullanıcıdan isteme
├── assets/
│   └── report-shell.css          # raporun marka-token'lı temel CSS'i
└── README.md
```

## Nasıl çalışır
1. **Intake** Â· hedef URL + hedef kelime zorunlu; ekran görüntüsü/marka rengi/rakip/doküman/sunum
   tercihi netleştirilir. Eksikse önce sorulur.
2. **Araştırma** Â· kelime/SERP/AI Overview/Trends/rakip/sosyal veri (varsa DataForSEO + Ahrefs).
3. **Rapor → Tasarım → (opsiyonel) Sunum** üretilir, her adım Playwright ile görsel QA'lanır.
4. Tamamlanamayan görseller kullanıcıdan **net bir liste + linklerle** istenir.

## Gereksinimler (çalışırken)
- DataForSEO ve/veya Ahrefs MCP (kelime/SERP/AI Overview verisi) Â· yoksa graceful düşer, kullanıcıdan
  veri ister.
- Playwright / Chrome MCP (ekran görüntüsü + canlı gözlem).
- Python + Pillow (görsel kırpma/boyutlama). Sunum için Inbound Design System bundle çalışırken indirilir.

## Çıktı dili ve stil
Varsayılan Türkçe; pasif/3. tekil; em-dash yok; kesin vaat yok; SEO terimleri orijinal dilde
(mention, machine-readable, anchor, SERP, AI Overview, GEO, KD, CWV…) ve `data-term` ile sözlüklü.

## Lisans / kullanım
İç ajans (Inbound) kullanımı için. Inbound Design System ve marka varlıkları ilgili sahiplerine aittir.
