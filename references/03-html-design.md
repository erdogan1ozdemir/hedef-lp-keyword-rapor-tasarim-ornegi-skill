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
`clone-website` skill'i veya canlı DOM/asset çıkarımı kullan. Header/nav/footer'ın HTML+CSS'ini ve
asset'lerini (logo, ikon, font) çıkar; gövdeyi kendi geliştirilmiş bileşenlerinle değiştir. Proprietary
font yüklenemiyorsa en yakın fallback'i kullan ve not düş.

## Varyant sistemi (4 varyant + yüzen seçici)

Tek sayfada, sağ kenarda **yüzen "VARYANT" seçici** ile anlık değişen 4 CRO varyantı sun. Seçim
`localStorage`'da saklanır (sayfalar arası korunur) ve `#v=a|b|c|d` hash ile de açılabilir (QA/paylaşım).
`body[data-variant=a|b|c|d]` ile CSS sürülür; varyanta özel öğeler DOM'da hep bulunur, CSS ile gösterilir.

4 varyantı **CRO hipotezi** olarak çeşitlendir (sayfa tipine göre uyarlanır). Mevcut işteki örnek:
- **A · Zengin** · geniş açıklama, büyük logolar/etiketler, bilgi yoğun. (Kartlarda dönen **conic
  glow** + gradient ile "premium" his · `@property` ile animasyonlu conic-gradient kenar.)
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

## Marka uyumu
Tasarım örneği hedef markanın renk/tipografi/logosunu kullanır (klon kabuğundan). Geliştirilen
bileşenler de marka diline sadık kalır; CRO/UX iyileştirmesi görsel kimliği bozmadan yapılır.

## QA
Fresh port'ta servis et (tarayıcı önbelleği için yeni port), `#v=a..d` ile her varyantı ekran
görüntüsüyle doğrula: kartlar eşit, popover doğru yöne açılıyor ve kartı büyütmüyor, kart tıklaması
detaya gidiyor, butonlar soft, conic glow çalışıyor, 0 kırık görsel, em-dash 0. Vercel/preview linki
verilecekse onu da test et.
