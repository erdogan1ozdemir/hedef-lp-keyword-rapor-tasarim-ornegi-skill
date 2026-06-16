# 00 · Intake · gereklilikleri topla, eksikse sor

Bu skill canlı veriye ve marka görsellerine bağımlıdır. Yanlış varsayımla başlamak baştan yapmaya
yol açar. Bu yüzden **araştırma/üretime geçmeden önce** aşağıdaki girdileri netleştir. Eksik olanları
kullanıcıya **tek, derli toplu bir mesajda** sor; cevap gelmeden ilerleme.

## Neden önden soruyoruz
Hedef sayfanın URL'i olmadan rapor da tasarım da yapılamaz. Ekran görüntüsü alınamazsa (giriş duvarı,
Cloudflare/bot engeli, JS render sorunu) tasarım klonunun kabuğu ve raporun görsel kanıtları eksik
kalır. Marka rengi belirsizse rapor renk uyarlaması ve klon yanlış olur. Bunları baştan çözmek ucuz.

## Zorunlu girdiler (bunlar gelmeden BAŞLAMA)

1. **Hedef sayfa URL'i** · tek bir sayfa. (Ör. bir hub, hizmet, listeleme veya ürün/hizmet detay
   sayfası.) Sayfa tipini de teyit et; tasarım deseni buna göre değişir (bkz. 03).
2. **Hedef kelime(ler)** · en az bir ana sorgu. Birden çok olabilir; biri "ana" olarak işaretlenir.

## Önden alınması / sorulması gerekenler (kalite için)

3. **Hedef sayfa ekran görüntüleri** · masaüstü + mobil.
   - Önce **kendin almayı dene** (Playwright/Chrome MCP + `python3 -m http.server` gerekmez, canlı
     URL'e git). Tam sayfa yakala.
   - Alamıyorsan **kullanıcıdan iste**: "Şu URL'in masaüstü ve mobil tam-sayfa ekran görüntüsünü
     iletir misiniz? Alamadığım için tasarım kabuğu ve rapor görselleri için gerekli."
4. **Marka rengi + logo** · rapor renk uyarlaması ve klon kabuğu için.
   - Sayfadan/CSS'ten çıkarmaya çalış (ana renk, vurgu rengi, logo URL'i). Çıkardıysan kullanıcıya
     **onaylat** ("Marka ana renginiz #XXXXXX, vurgu #YYYYYY olarak algıladım, doğru mu?").
   - Okunabilirlik gözet: marka rengi çok açık/çok doygunsa metin kontrastını koru; rengi
     vurgu/accent olarak kullan, gövde metnini koyu nötrde bırak.
5. **Rakip seti** · yoksa SERP + AI Overview keşfiyle türet (editöryel + operatör/sektör rakipleri +
   UGC). Kullanıcı belirli rakip verdiyse onları baz al.
6. **Mevcut SEO / optimizasyon dokümanı** · varsa iste. Aksiyon bölümünde "Doc'ta var / Doc + ek /
   Analiz eki" ayrımı bu dokümana göre yapılır (raporun özgün katkısını ayırt eder).
7. **Dil(ler)** · varsayılan Türkçe. Farklıysa sor.
8. **Sunum isteniyor mu?** · varsayılan **hayır**. "Sunum (deck) da ister misiniz, yoksa rapor +
   tasarım yeterli mi?" diye sor. İstenirse 04'ü uygula.
9. **Teslim/iletme tercihi** · çıktıların bir repoya push'lanması isteniyorsa repo URL'i; istenmiyorsa
   yerel teslim.

## Intake mesajı şablonu (eksik varsa kullan)

> Başlamadan önce birkaç şeyi netleştireyim:
> 1. **Hedef sayfa URL'i** nedir? (tek sayfa)
> 2. **Hedef kelime(ler)** nedir? (ana sorgu)
> 3. Sayfanın **ekran görüntüsünü** ben almayı deneyeceğim; alamazsam masaüstü + mobil tam-sayfa
>    görüntüyü sizden isteyebilirim.
> 4. **Marka ana rengi / logosu** · sayfadan algılayacağım, sonra onaylatacağım.
> 5. Varsa **rakipler** ve **mevcut SEO dokümanınız**? (yoksa SERP'ten türetirim)
> 6. **Sunum (deck)** de istiyor musunuz, yoksa rapor + tasarım yeterli mi?

Kullanıcı "sen hallet / elindekiyle başla" derse: zorunlu ikisi (URL + kelime) varsa başla, kalanları
yol üstünde türet ve eksik görselleri 05'teki gibi iste. Zorunlu ikisi yoksa yine de sor.

## Sayfa tipi tespiti (URL geldikten sonra)
Sayfayı canlı incele ve tipini sınıfla · tasarım varyant desenleri (03) buna göre seçilir:
- **hub / onboarding** (anlatım, "nedir", yönlendirme)
- **hizmet / servis** sayfası
- **listeleme / kategori** (kartlar, filtreler)
- **ürün / hizmet detay** (fiyat, seçenek, satın alma)
- **kampanya / LP** (tek amaçlı dönüşüm)

Tip belirsizse kullanıcıya teyit ettir. Rapordaki "sayfa rol haritası" ve tasarımdaki bileşen seti
bu tipe göre kurulur.
