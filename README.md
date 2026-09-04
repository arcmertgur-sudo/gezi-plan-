# COP31 Antalya — Bakan Gezisi Sergi Planı

COP31 Blue Zone kapsamındaki 37 mekânı (başkanlık ofisleri, medya merkezi,
genel kurul salonları, VVIP/protokol alanları vb.) tek bir interaktif sayfada
gezilebilir hale getiren statik site.

## Kullanım

Tamamen statik, tek dosyalık (`index.html`) bir site — build adımı,
bağımlılık veya sunucu tarafı kod gerektirmez. Tüm görseller dosyanın
içine gömülüdür.

Yerel önizleme için `index.html` dosyasını doğrudan tarayıcıda açabilir
veya basit bir sunucuyla servis edebilirsin:

```bash
python3 -m http.server 8000
```

sonra `http://localhost:8000` adresine git.

## Vercel'e deploy

Bu repoyu GitHub'a push ettikten sonra Vercel'de:

1. [vercel.com/new](https://vercel.com/new) adresine git
2. Bu GitHub reposunu import et
3. Framework olarak **Other / Static** seç (build komutu gerekmez)
4. Deploy'a bas

Her `main` dalına push'ta otomatik olarak yeniden deploy edilir.
