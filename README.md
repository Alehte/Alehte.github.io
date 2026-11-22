# lehtestudios — tanıtım sitesi

lehtestudios ve **All in Together** oyunu için tek sayfalık tanıtım sitesi.
Düz HTML ve CSS. Derleme adımı, framework, paket yöneticisi ve JavaScript yok.
Çerez, analitik, takip aracı, reklam kodu ve harici yazı tipi yok.

Yayın adresi (planlanan): `https://alehte.github.io/` (depo: `Alehte/Alehte.github.io`)

## Dosyalar

| Yol | Ne |
|---|---|
| `index.html` | Ana sayfa |
| `404.html` | GitHub Pages'in bulunamayan adreslerde gösterdiği sayfa |
| `css/site.css` | Bütün stiller; renk ve boşluk değişkenleri en üstte (`:root`) |
| `fonts/` | Fredoka (yerel, SIL OFL 1.1, lisans `fonts/LICENSE-Fredoka.txt`) |
| `img/` | Ekran görüntüleri (WebP), ikonlar, paylaşım görseli `og.png` |
| `favicon.ico` | Tarayıcı sekme ikonu |
| `robots.txt`, `sitemap.xml` | Arama motorları için |
| `.nojekyll` | GitHub Pages'in Jekyll'i atlaması için; `.well-known/` gibi noktayla başlayan klasörlerin yayına girmesini sağlar |

Bütün yollar köke göre (`/css/site.css`). Site bir alt yolda (`/depo-adi/`) değil, alan adının kökünde yayınlanmalıdır.

## Yerelde test

```sh
cd lehtestudios-site
python -m http.server 8000
```

Tarayıcıda `http://localhost:8000/` adresini aç. 404 sayfasını görmek için `http://localhost:8000/404.html` adresini aç.
`python -m http.server` bilinmeyen adreslerde `404.html` dosyasını göstermez; bunu yalnızca GitHub Pages yapar.

## Yayınlama (GitHub Pages)

1. GitHub'da `Alehte.github.io` adlı herkese açık bir depo oluştur.
2. Bu klasörü o depoya gönder (`main` dalı).
3. Depo ayarları: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, dal `main`, klasör `/ (root)`.

## Android uygulama bağlantısı (assetlinks.json): YAPILACAK

Android, alan adı doğrulaması için dosyayı yalnızca alan adının **kökünde** arar:
`https://alehte.github.io/.well-known/assetlinks.json`

Oyunun kendi deposundaki (`Oyunum`) dosya `https://alehte.github.io/Oyunum/.well-known/...` adresinde kalır. Android o adrese bakmaz.
Bu yüzden dosyanın bu sitede durması gerekir.

Android paketi henüz hazır olmadığı için dosya **bilerek eklenmedi**.
Uydurma ya da eski bir parmak izi yayınlamak doğrulamayı bozar.
Paketleme aşamasında:

1. `.well-known/assetlinks.json` dosyasını oluştur:

   ```json
   [{
     "relation": ["delegate_permission/common.handle_all_urls"],
     "target": {
       "namespace": "android_app",
       "package_name": "com.alehte.allintogether",
       "sha256_cert_fingerprints": ["<İMZA ANAHTARININ SHA-256 PARMAK İZİ>"]
     }
   }]
   ```

2. Parmak izini, Play Console'da **Test ve yayınla → Uygulama bütünlüğü → Uygulama imzalama** sayfasından al.
   Play App Signing kullanılıyorsa yerel yükleme anahtarının parmak izi değil, **Google'ın uygulama imzalama anahtarınınki** gerekir.
   İki anahtar da kullanılacaksa ikisini de listeye yaz.
3. Paket adını (`package_name`) uygulamanın gerçek paket adıyla karşılaştır.
4. Yayından sonra şu adresin JSON döndürdüğünü kontrol et:
   `https://alehte.github.io/.well-known/assetlinks.json`
   `.nojekyll` dosyası silinirse bu klasör yayına girmez.

## İçerik notları

- Metinler oyunun koduna göre yazıldı: bölüm sayıları, tahta boyutları, jokerler.
  Oyunda bunlar değişirse `index.html` dosyasını da güncelle.
- "İlk açılıştan sonra internetsiz" ifadesi, 14 Kasım 2026'da yayındaki oyunda test edildi:
  önbellek dolduktan sonra ağ kapatıldı, dört oyun da açıldı.
  Beşinci oyun Karanlıkta Süzül 22 Kasım 2026'da siteye eklendi; internetsiz açılışı bu test kapsamında değildi, ayrıca denenmeli.
- "Şu an reklam ve uygulama içi satın alma yok" ifadesi şimdiki zamanla yazıldı.
  Oyuna reklam ya da satın alma eklenirse bu cümleleri (Neden denemeye değer, SSS) ve gizlilik politikasını değiştir.
- Ekran görüntüleri oyunun temiz bir başlangıç durumundan headless Chrome ile alındı (390×844, 540 px genişliğe küçültüldü).
