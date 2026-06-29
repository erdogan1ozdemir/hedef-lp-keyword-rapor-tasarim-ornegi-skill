# 03 · HTML tasarım örneği

Hedef sayfanın **gerçekçi bir klonu** üzerinde, sayfa içi gövdeyi CRO/CX/UI-UX'e göre geliştiren ve
**birden çok varyant** sunan tasarım örneği. Amaç: kullanıcı hâlâ hedef domaindeymiş hissetsin
(header/nav/footer aynı), ama içerik bileşenleri görsel ve dönüşüm olarak iyileştirilmiş olsun.

## İlke: değişmeyen kabuk + özelleştirilen gövde

- **Değişmeyen (birebir klonla):** header, üst navigasyon, alt navigasyon/footer, breadcrumb,
  global renk/tipografi, logo. Kullanıcı aynı sitedeymiş gibi hissetmeli.
- **Değişen (yeniden tasarla):** sayfa içi gövde · hedef sayfanın tipine göre bileşenler:
  - **hub/onboarding:** hero, "nedir" tanım bloğu, değer/karşılaştırma, adımlar, SSS.
  - **hizmet:** hizmet anlatımı, faydalar, fiyat/teklif, sosyal kanıt, CTA.
  - **listeleme/kategori:** filtre + kartlar (mevcut işteki gibi), kart içi detay.
  - **ürün/hizmet detay:** sol bilgi kartı + sağ abonelik/satın alma + sekmeli detaylar.
  - **kampanya/LP:** tek amaçlı hero + kanıt + tek güçlü CTA.

## Klonlama
**`clone-website` skill'ini kullan** (yoksa canlı DOM/asset çıkarımı). Header/nav/footer'ı **birebir**
çıkar ve klonla; gövdeyi kendi geliştirilmiş bileşenlerinle değiştir.
- **Renkleri BİREBİR al (çok önemli):** renkleri tahmin etme; canlı sayfadan **computed style** ile
  gerçek hex kodlarını çıkar (`getComputedStyle` ile arka plan/kart/buton/accent renklerini ve frekansını
  topla) ve token'lara birebir yaz. Uydurma ara-ton kullanma (ör. gerçek #001151 dururken #0a1a5e yazma).
- **Header / footer 1:1:** yapı, logo, menü ve footer canlı sayfayla aynı olmalı; logoyu inline SVG yap
  (CDN'e bağımlı kalma). Proprietary font yüklenemiyorsa en yakın fallback'i kullan ve not düş.

## Varyant sistemi (4 varyant + yüzen seçici)

Tek sayfada, sağ kenarda **yüzen "VARYANT" seçici** ile anlık değişen 4 CRO varyantı sun. Seçim
`localStorage`'da saklanır (sayfalar arası korunur) ve `#v=a|b|c|d` hash ile de açılabilir (QA/paylaşım).
`body[data-variant=a|b|c|d]` ile CSS sürülür; varyanta özel öğeler DOM'da hep bulunur, CSS ile gösterilir.

4 varyantı **CRO hipotezi** olarak çeşitlendir (sayfa tipine göre uyarlanır). Mevcut işteki örnek:
- **A · Zengin** · geniş açıklama, büyük logolar/etiketler, bilgi yoğun. Premium his için **temiz
  çerçeve + yumuşak gölge** (ve istenirse düşük-opaklıkta düz iç-glow) kullan. **Conic-gradient ile
  parantez/yay kenar KULLANMA** (transparent boşluklu conic, kartın kenarında "(" gibi yaylar
  oluşturur · yasak). Premium algı temiz kart + accent şerit/rozet ile sağlanır.
- **B · Sade** · küçük logolar, az metin, düz başlık, tek güçlü fiyat/CTA. Hızlı tarama hipotezi.
- **C · Değer** · tasarruf satırı (üstü çizili eski fiyat + "~%X daha uygun"), değer kartı; değer
  çerçevesi hipotezi.
- **D · Detay** · rakip-tarzı belirgin "Detaylar" butonları, çerçeveli başlık, en detaylı bilgi.

Farklı varyantlarda farklı gradient geçişleri, gölge ve glow denemeleri yapılabilir. UI/UX kararları
için `ui-ux-pro-max` ve `frontend-design` skill'lerinden yararlan.

## Etkileşim desenleri (mevcut işten damıtılmış)

- **Eşit kartlar:** liste/kart düzenlerinde tüm kartlar **eşit yükseklik ve genişlik**; içerik bitince
  kart biter, alta boşluk uzamaz. Grid: `.layout{align-items:start}` (kartlar yan kolona/sidebar'a
  göre uzamasın), kart grid'i `align-items:stretch` + foot `margin-top:auto` ile eşit boy.
- **Kart içi "Detaylar" popover'ı:** "Detaylar" detay sayfasına gitmek yerine **mevcut kartın
  üstüne gelen** bir popover açar (kart boyunu değiştirmez, `position:absolute` overlay). Yön varyanta
  göre: bir varyantta yukarı, başka birinde aşağı açılabilir. Karta (buton dışına) tıklayınca detay
  sayfasına gidilir; yalnız "Detaylar" popover'ı açar. (Rakip örnek: TT/GeForce Now akordeonları.)
- **Soft butonlar:** CTA'lar gölgeli/çerçeveli, hover'da hafif yükselme.
- **"Parantez" gibi süslemelerden kaçın:** renkli kıvrımlı kenarlar premium görünmeyi düşürür; temiz
  kart + accent şerit/rozet tercih et.
- **Detay sayfası tutarlılığı:** abonelik/satın alma + "detaylar" bölümü tüm varyantlarda **tutarlı**;
  varyanta göre değişen yer sol bilgi kartı ve sayfanın alt kısmı olur.

## Çoklu sayfa (gerekirse)
Hedef tek sayfa olsa da, detay/alt sayfa örneği faydalıysa ikinci bir HTML (`detay.html?...`) üretilebilir.
Aksi halde tek `index.html` yeterli. Footer/nav her sayfada aynı kabukla render edilir (ortak `app.js`).

## Deploy için tek dosya (önemli)
Tasarım örneği bir alt yolda (`/demo`) yayınlanacaksa **tek dosya self-contained** üret: CSS, JS ve
logo SVG **inline**. Sebebi: `cleanUrls` ile `/demo` (sondaki `/` yok) açıldığında göreli `style.css`
/ `app.js` linkleri kök'e (`/style.css`) çözülüp 404 olur ve sayfa **stilsiz** gelir. Inline edersen
hiçbir host'ta bozulmaz. Klon kabuğun logosunu da inline SVG yap (CDN'e bağımlı kalma). Bkz. `06-deploy.md`.

## İçerik bileşenleri (gövdede · CRO dışı)
Tasarım örneği yalnız dönüşüm bloğu değil, **geliştirilmiş içeriği** de gösterir:
- **SSS'leri kümele + açılır-kapanır yap.** Canlı sayfadaki tüm soruları al ama tek uzun açık liste
  yapma; konu başlıklarına (küme) ayır ve her soruyu `<details>` akordeon (kapalı) yap + üstte hızlı
  erişim chip'leri. Okunabilirliği artırır, soruya erişimi kolaylaştırır.
- **Hedefte olmayan karşılaştırma tablolarını ekle** (rapordaki gap'ten): hız-ihtiyaç eşleme, indirme
  süresi, metrik açıklama. Her satır ilgili pakete bağlanır (bilgi → dönüşüm köprüsü).
- **Canlı içeriği alıp rapordaki öneri/aksiyonlarla geliştir** (5G/ADSL/ölçüm içeriği, eksik FAQ'lar).

## Marka uyumu
Tasarım örneği hedef markanın renk/tipografi/logosunu kullanır (klon kabuğundan). Geliştirilen
bileşenler de marka diline sadık kalır; CRO/UX iyileştirmesi görsel kimliği bozmadan yapılır.

## QA
Fresh port'ta servis et (tarayıcı önbelleği için yeni port), `#v=a..d` ile her varyantı ekran
görüntüsüyle doğrula: kartlar eşit, popover doğru yöne açılıyor ve kartı büyütmüyor, kart tıklaması
detaya gidiyor, butonlar soft, conic glow çalışıyor, 0 kırık görsel, em-dash 0. Vercel/preview linki
verilecekse onu da test et.
