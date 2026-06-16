# 05 · Ekran görüntüleri ve eksikleri kullanıcıdan isteme

Rapor ve tasarım, kanıt niteliğinde **gerçek ekran görüntüleri** içerir. Bir görseli kendin
alamıyorsan ya da rapor görsel olarak eksik kalıyorsa, **bunu net biçimde listele ve kullanıcıdan
iste** Â· eksik bırakıp geçme, uydurma görsel koyma.

## Hangi ekran görüntüleri gerekir (tipik)
- **Hedef sayfa:** masaüstü + mobil tam-sayfa (tasarım klonu + CRO bölümü için).
- **SERP:** ana sorgu canlı SERP (masaüstü + mobil), "<kelime> nedir" AI Overview (AI Bakışı).
- **Rakip kanıtı:** "şu sorgu → rakip URL" sayfaları (ör. operatör tarife/blog sayfaları).
- **Rakip içerik:** editöryel liderlerin (haber/teknoloji sitesi) sayfa görünümleri.
- **Sosyal duygu:** X araması, Ekşi başlığı, Şikayetvar (marka filtresi + varsa ürüne özgü şikayet).
- **AI Overview kaynak paneli** (mention dağılımı görünür kapsam).

Rapora başlarken kullanıcıya **gereken ekran görüntülerinin listesini ve nereden alınacağını
(linklerle)** ilet ki tıklayıp gönderebilsin.

## Kendin alma (Playwright/Chrome)
- Canlı URL'e git, tam-sayfa yakala. Dosya genelde worktree köküne `./<ad>.png` kaydedilir; bul ve
  PIL ile işle.
- **Kırpma/boyutlama (PIL/Pillow):** üst-çapalı kırp (banner/reklam/menü çubuğunu at), makul genişliğe
  (~900-1500px) yeniden boyutla, `optimize=True` ile kaydet. **Asla devasa (10MB+) ham görsel gömme**
  Â· performansı bozar; kırp + küçült.
- **Gereksiz alanları temizle:** özellikle X'te sol menü (Anasayfa/Keşfet/Profil), reklam banner'ları,
  çerez bildirimleri kırpılır. Kullanıcı paylaşımı/tweet metinleri **kesilmemeli** Â· gerekirse mobil
  yakalamadan (tek sütun, tam metin) kırp.
- **Bölme:** uzun akışları 2-3 parçaya böl (X 1/2, X 2/2; Ekşi 1/2, Ekşi 2/2) ki daha çok içerik görünsün.

## Kullanıcı pano (paste) görselini dosyaya çeviremezsin
Kullanıcı sohbete görsel yapıştırırsa onu doğrudan dosya olarak kaydedemezsin. Ya kullanıcıdan
`Downloads/`'a kaydetmesini iste, ya da mümkünse ilgili sayfayı **canlı yeniden yakala** (örn.
Şikayetvar şikayet sayfasını URL'inden Playwright ile aç + kırp). Pano görselini yalnız içerik/metin
okumak için kullan.

## Kaydırmalı (carousel) ekran görüntüleri
Sosyal/rakip ss bölümlerinde "diğer görselleri" kaydırmalı sun: yatay kaydırılabilir bir şerit + sağ/sol
ok butonları. Ön plandaki mevcut görseller sabit kalır; ok'a basınca şerit kayar, ek görseller görünür.
Her görsel tıklanınca **lightbox** ile büyük açılır.

## Küçük thumbnail + büyük lightbox
Yer kaplayan görselleri (ör. Şikayetvar uzun yakalamaları) **küçük** (örn. dörtte bir) göster; tıklayınca
lightbox ile tam boyda aç. `shot-grid` + `data-full` deseni bunu sağlar.

## Raporda tamamlanamayan görsel = kullanıcıya talep
Bir bölüm görsel bekliyor ama alınamıyorsa:
1. O bölüme yer tutucu/eksik notu koyma yerine, görseli **kibarca iste**.
2. Teslim özetinde **"Bekleyen ekran görüntüleri"** başlığı altında, her biri için **doğrudan link**
   ver (kullanıcı tıklayıp çeksin), beklenen dosya adıyla (ör. `ss-trends-<marka>.png`).
3. Görsel gelince ilgili bölüme göm + lightbox/carousel'e ekle.

## İsimlendirme
`assets/screenshots/ss-<kaynak>-<marka>[-n].png` (ör. `ss-serp-<marka>-masaustu.png`,
`ss-aio-nedir-<marka>.png`, `ss-eksi-<marka>-1.png`). Tutarlı isim, sonradan değiştirmeyi kolaylaştırır.
