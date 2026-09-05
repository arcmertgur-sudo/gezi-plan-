# COP31 Antalya — Bakan Gezisi Sergi Planı

COP31 Blue Zone kapsamındaki 37 mekânı (başkanlık ofisleri, medya merkezi,
genel kurul salonları, VVIP/protokol alanları vb.) tek bir interaktif sayfada
gezilebilir hale getiren statik site.

Görseller önceden JPEG'e çevrilip gömülmüyor — sayfa, `sergi-plani.pdf`
dosyasını doğrudan tarayıcıda [PDF.js](https://mozilla.github.io/pdf.js/)
ile canlı render ediyor. Bu sayede:

- **Kalite kaybı yok** — her sayfa PDF'in kendi çözünürlüğünde, ekran
  boyutuna göre (retina dahil) net şekilde çiziliyor.
- **Güncelleme çok kolay** — `sergi-plani.pdf` dosyasını aynı isim ve aynı
  sayfa sırasıyla yenisiyle değiştirip push etmen yeterli. HTML/JS'e
  dokunmana gerek yok.

## Dosya yapısı

```
index.html        → site (arayüz + PDF.js render mantığı)
sergi-plani.pdf    → kaynak PDF (37 durak + kat planı rehberi, toplam 38 sayfa)
```

## Sayfa – durak eşleşmesi (önemli)

PDF'in **1. sayfası** kat planı rehberi (ana sayfadaki tıklanabilir grid).
**2. sayfa = durak 1, 3. sayfa = durak 2, ... 38. sayfa = durak 37** şeklinde
kayıyor (her durak numarası + 1 = PDF sayfa numarası).

Yeni bir PDF ile güncellersen:
- Sayfa sırası ve toplam sayfa sayısı (38) aynı kalmalı.
- 1. sayfadaki numaralı kutuların konumu değişirse, `index.html` içindeki
  `.hotspot` elemanlarının `left/top/width/height` yüzdelerini (dosyanın
  en üstündeki HTML bloğunda, `hotspot` class'lı butonlarda) yeniden
  hizalaman gerekir. Sadece içerik/render güncelleniyorsa (konumlar aynı
  kalıyorsa) hiçbir şeye dokunman gerekmez.

## Yerel önizleme

Tarayıcılar `file://` üzerinden fetch ile PDF çekmeye izin vermeyebilir,
bu yüzden basit bir sunucuyla aç:

```bash
python3 -m http.server 8000
```

sonra `http://localhost:8000` adresine git.

## Vercel'e deploy

1. Bu repoyu GitHub'a push et
2. [vercel.com/new](https://vercel.com/new) → reponu import et
3. Framework: **Other / Static** (build komutu gerekmez)
4. Deploy'a bas

`main` dalına her push'ta otomatik olarak yeniden deploy edilir.
