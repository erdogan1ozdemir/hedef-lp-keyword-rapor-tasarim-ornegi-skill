# 06 · Deploy (Vercel + Railway uyumu)

Rapor ve tasarım çıktıları **statik HTML**'dir; iki yaygın host için kutudan çıktığı gibi çalışmalı:
**Vercel** (statik) ve **Railway/Render** (Node, `PORT` ile). Aşağıdaki desen ikisini de karşılar.

## En önemli iki kural
1. **Kökte `index.html` olmalı.** Host `/` adresinde bunu servis eder. Çıktıları alt klasörde
   (`<marka>-rapor-html/`) bırakırsan kök boş görünür. Deploy edilecekse **rapor köke**, tasarım
   **`/demo`** (veya `<marka>-tasarim-html/`) altına alınır.
2. **Asset yolları kırılmamalı.** `cleanUrls` ile `/demo` (sondaki `/` olmadan) açıldığında, sayfadaki
   **göreli** `style.css` / `app.js` linkleri `/style.css` gibi **kök'e** çözülür ve 404 olur (sayfa
   stilsiz "bozuk" görünür). İki çözümden biri:
   - **Tek dosya (önerilen):** tasarım/demo sayfasını **self-contained** yap (CSS+JS+logo SVG inline).
     Hiçbir harici asset yolu kalmaz; her host'ta bozulmaz.
   - veya **absolute path** kullan: `href="/demo/style.css"`, `src="/demo/app.js"`.
   Raporun ekran görüntüleri kökten servis edildiğinde göreli `assets/...` çalışır (kök dizin gibidir).

## Önerilen repo yapısı (deploy için)
```
/
├── index.html            → rapor (kökte yayınlanır → "/")
├── assets/screenshots/   → rapor görselleri (göreli: assets/...)
├── data/                 → ham bulgular (kanıt)
├── demo/index.html       → tasarım örneği, TEK DOSYA self-contained ("/demo")
├── vercel.json           → cleanUrls (Vercel)
├── server.js             → sıfır-bağımlılık statik sunucu (Railway/Render)
├── package.json          → { "scripts": { "start": "node server.js" } }
└── README.md
```

## vercel.json (Vercel · statik)
```json
{ "cleanUrls": true, "trailingSlash": false }
```
Vercel `build` script'i yoksa repo'yu statik servis eder; `package.json`'daki `start` script'ini
çalıştırmaz (yalnızca Railway/Render kullanır). Kök `server.js` otomatik fonksiyon olarak deploy
edilmez (sadece `/api` altı fonksiyon sayılır), bu yüzden Vercel'i bozmaz.

## server.js (Railway/Render · Node, sıfır bağımlılık)
`PORT` env'ini dinleyen, `/` → `index.html`, `/demo` → `demo/index.html` çözen küçük statik sunucu.
Path-traversal koruması ekle. Şablon (kısalt/uyarlanabilir):
```js
const http=require('http'),fs=require('fs'),path=require('path');
const ROOT=__dirname,PORT=process.env.PORT||3000;
const T={'.html':'text/html; charset=utf-8','.css':'text/css','.js':'text/javascript',
'.json':'application/json','.svg':'image/svg+xml','.jpg':'image/jpeg','.jpeg':'image/jpeg',
'.png':'image/png','.webp':'image/webp','.ico':'image/x-icon'};
function resolve(u){let p=decodeURIComponent(u.split('?')[0].split('#')[0]);if(p.endsWith('/'))p+='index.html';
let fp=path.normalize(path.join(ROOT,p));if(!fp.startsWith(ROOT))return null;
if(fs.existsSync(fp)&&fs.statSync(fp).isDirectory())fp=path.join(fp,'index.html');
else if(!fs.existsSync(fp)&&fs.existsSync(fp+'.html'))fp=fp+'.html';
else if(!fs.existsSync(fp)&&fs.existsSync(path.join(fp,'index.html')))fp=path.join(fp,'index.html');
return fs.existsSync(fp)&&fs.statSync(fp).isFile()?fp:null;}
http.createServer((req,res)=>{const fp=resolve(req.url==='/'?'/index.html':req.url);
if(!fp){res.writeHead(404);res.end('404');return;}
res.writeHead(200,{'Content-Type':T[path.extname(fp)]||'application/octet-stream'});
fs.createReadStream(fp).pipe(res);}).listen(PORT);
```

## package.json (Railway Node algılaması için)
```json
{ "name":"<proje>", "private":true, "scripts":{ "start":"node server.js" }, "engines":{ "node":">=18" } }
```

## Mobil uyum (her zaman)
- Rapor: `@media(max-width:900px)` ile tek sütun, ToC gizlenir + "☰ Bölümler" FAB; ToC ayrıca
  `max-height + .toc-scroll` ile kısa ekranlara sığar (bkz. 02).
- Tasarım/demo: hero tek sütun, kartlar tek kolon, yüzen varyant seçici mobilde alt şeride iner.
- `<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">` zorunlu.
- Playwright ile 390px (mobil) ve 1440×620 (kısa) viewport'ta QA et.
```
