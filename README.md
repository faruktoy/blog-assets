# blog-assets — `blog` dalı

Bu repo **faruktoy.com** ve **blog.faruktoy.com** için CDN üzerinden yayınlanan içerik
dosyalarını barındırır. Site kodu ([portfolio repo](https://github.com/faruktoy/portfolio))
build almadan bu repoya bakarak içeriği günceller.

**CDN base URL:** `https://cdn.jsdelivr.net/gh/faruktoy/blog-assets@blog`

> Repo adı `blog-assets` olarak kalıyor ama içerik artık yalnızca bloglardan ibaret değil:
> **`blog/`** yazıları, **`project/`** portfolyo projelerini tutar. İkisi ayrı indekse,
> ayrı URL ad alanına ve ayrı yayın akışına sahiptir.

---

## Dizin yapısı

```text
/
├── blog/
│   ├── index.json                  ← yazı listesi (kart manifesti)
│   └── post/
│       ├── turboprop/
│       │   ├── tr.md
│       │   ├── en.md
│       │   └── image/              ← yazının kendi görselleri
│       ├── fdm-yuzey-kalitesi/
│       ├── abs-cf-prototipleme/
│       └── p3steel-build-log/
│
└── project/
    ├── index.json                  ← proje listesi (kart manifesti)
    ├── e3a/
    │   ├── project.json            ← dile bağlı OLMAYAN proje gerçekleri
    │   ├── tr.md                   ← recruiter'ın okuyacağı metin
    │   ├── en.md
    │   └── image/
    ├── turboprop/
    ├── formapis/
    └── ...
```

**İki kural:**

1. **Görseller içeriğin yanında durur.** Yazının/projenin klasöründeki `image/` altında.
   Markdown'da **göreli** yazılır: `![alt](image/foo.png)`. Site bunu çalışma anında
   `<CDN base>/<mdPath>/image/foo.png` hâline getirir. Böylece bir içerik taşındığında
   görselleri onunla birlikte gider ve markdown'da hiçbir mutlak CDN adresi kalmaz —
   repo adı veya dal değişse bile içerik bozulmaz.
2. **Klasör adları küçük harf, kebab-case.** jsDelivr büyük/küçük harfe duyarlıdır;
   `TurboProp` ile `turboprop` farklı adreslerdir. Uygulamanın slug eşleşmesi harf
   duyarsızdır ama CDN yolu değildir — bu ikisi karıştığında görsel 404 olur.

---

## `blog/index.json` — **ÜRETİLİR, ELLE DÜZENLEME**

> ⚠️ Bu dosyayı elle değiştirme. Markdown front matter'larından üretiliyor:
>
> ```bash
> cd ../site && npm run build:index     # üret
> cd ../site && npm run check:index     # bayatsa çıkış kodu 1
> ```
>
> Elle yapılan değişiklik ilk üretimde kaybolur. Metadata **markdown'da** değiştirilir.

Neden böyle: eskiden başlık/tarih/okuma süresi hem burada hem front matter'da duruyordu ve
dört yazının **ikisinde** değerler çelişiyordu — blog listesi bir başlık, yazı sayfası başka
bir başlık gösteriyordu. Artık tek kaynak var.

Üretilen alanlar: `slug` (klasör adı), `slugs.{tr,en}`, `published`, `featured`, `category`,
`cover`, `mdPath`, `mdFiles`, `tags`, `legacySlugs`, `relatedProject` ve dil başına
`{title, description, date, readTime}`.

### Yazı front matter şeması

```yaml
---
type: article
slug: "turboprop"            # bu DİLİN URL segmenti; tüm yazılar arasında benzersiz
title: "..."
description: "..."           # kartta ve og:description'da görünür
date: "2026-05-21"           # ISO. Yayınlanmışsa zorunlu
category: "aviation"         # printing · aviation · it (küçük harf anahtar)
tags:
  - Turboprop
  - C-130
cover: ""                    # image/ altında göreli yol; dosya yoksa üretici durur
published: true
featured: true
relatedProject: "turboprop"  # project/<slug> — opsiyonel
legacySlugs: []              # bu yazının eski adresleri (301 kaynağı)
lang: tr
---
```

**`readTime` yoktur.** Gövdeden hesaplanır (kelime / 200, en az 1 dk). Front matter'a yazma.
Değeri yayınlamadan önce görmek istersen: `.\_tools\readTime\readTime.ps1 -v`

**Üretici şunlarda durur (çıkış kodu 1):** `slug`/`title` eksik · `date` ISO değil ·
yayınlanmış yazının tarihi yok · iki yazı aynı slug veya alias'ı kullanıyor · `cover` dosyası
yok · klasör adı büyük harf içeriyor · **dile bağlı olmayan bir alan** (`published`, `featured`,
`category`, `relatedProject`) `tr.md` ile `en.md` arasında çelişiyor.

Son kural önemli: bunlar dile göre değişmeyen alanlardır, iki dosyada da aynı olmalıdır.
Çeliştiklerinde üretici birini seçmez — durur ve söyler.

## `project/index.json`

Aynı işi projeler için yapar: **kart/listeleme manifesti**, uzun içeriğin kaynağı değil.
Alanlar `blog/index.json` ile aynı mantıkta, ek olarak `legacySlugs`, `status`,
`technologies`, `articles`, `cover`.

> Yazılar için üretici hazır (`npm run build:index`); **projeler için henüz değil**, bu dosya
> şimdilik elle güncelleniyor. Aynı üretici projeleri de kapsayınca burası da "üretilir" olacak.

---

## Proje anatomisi

Bir projenin bilgisi **dile bağlı olup olmamasına göre** ikiye ayrılır. Ayrım
"sunum mu yönlendirme mi" değil, **"dile göre değişir mi değişmez mi"**dir:

### `project.json` — dile bağlı olmayan gerçekler

```json
{
  "slug": "e3a",
  "legacySlugs": ["E3A"],
  "slugs": { "tr": "e3a", "en": "e3a" },
  "status": "completed",
  "startDate": "2023-04",
  "endDate": "2024-03",
  "category": "maker",
  "featured": true,
  "published": false,
  "technologies": ["SolidWorks", "AutoCAD", "FDM", "CAD/CAM", "Electronics"],
  "cover": "image/cover.webp",
  "gallery": ["image/full-printer.webp", "image/enclosure.webp"],
  "articles": ["p3steel-build-log"]
}
```

| Alan | Açıklama |
|---|---|
| `slug` | Dahili ID, klasör adıyla aynı |
| `legacySlugs` | **Eski adresler.** Daha önce paylaşılmış URL'ler buraya yazılır, site bunlardan 301 yönlendirir. Adres asla silinmez, buraya taşınır. |
| `slugs.tr` / `.en` | Dil başına URL segmenti. Özel ad ise (E3A gibi) ikisi aynı olabilir. |
| `status` | `completed` · `in-progress` · `planned` (boşsa henüz belirlenmedi) |
| `startDate` / `endDate` | `YYYY-MM` |
| `technologies` | Kart üzerinde rozet olarak gösterilir |
| `cover` | Kapak görseli, `image/` altında göreli yol. OG görseli olarak da kullanılır (1200×630, < 300 KB) |
| `gallery` | Proje sayfasındaki görsel dizisi, göreli yollar |
| `articles` | İlgili blog yazılarının `slug`'ları. **İlişki tek yönlü tanımlanır**; yazıdan projeye ters bağ üretici tarafından hesaplanır. |

### `tr.md` / `en.md` — dile bağlı metin

Recruiter'ın okuyacağı anlatı. Front matter yalnızca dile bağlı alanları taşır:

```markdown
---
title: "3D Yazıcı Yapımı"
slug: "e3a"
description: "P3Steel türevi 3D yazıcı: mekanik kurulum, sistem entegrasyonu ve kalibrasyon."
---

# 3D Yazıcı Yapımı

> Tek cümlelik özet.

## Amaç
## Yaklaşım
## Sonuç
```

---

## Yazı markdown formatı

Front matter şeması yukarıda. Gövde:

```markdown
# Yazı Başlığı

> Giriş cümlesi (blockquote — italik kutu olarak gösterilir)

## Bölüm Başlığı

![Görsel açıklaması](image/sema.png)

## Kaynaklar

[1]: https://example.com "Kaynak Başlığı"
```

**Kurallar**

- Front matter **zorunludur** ve yetkilidir; `# Başlık` satırı yalnızca sayfada görünen
  başlıktır, metadata değil.
- İlk `>` bloğu intro olur; yoksa `description` kullanılır.
- `## Kaynaklar` / `## References` otomatik olarak referans kutusuna dönüşür;
  `[n]: url "Başlık"` tanımları referans listesine girer.
- Görseller **göreli** yazılır (`image/...`). Mutlak CDN adresi yazma.
- Görsel altbilgisi **markdown'dan gelir** — bkz. aşağıdaki bölüm.
- `readTime` diye bir alan yok; her zaman gövdeden hesaplanır.
- **Bir `-` liste maddesi tek satırda yazılır.** Ayrıştırıcı maddenin devamını yeni
  satırda kabul etmiyor; kırılan kısım maddenin dışına düşüp ayrı bir paragraf olur.

---

## Görseller: altbilgi ve kaynak

Görsel, standart markdown başlık (title) alanıyla yazılır:

```markdown
![alt metni](image/sema.webp "Görselin altında görünecek açıklama")
```

| Alan | Nerede görünür |
|---|---|
| `alt metni` | **Görünmez.** Ekran okuyucular ve görsel yüklenmediğinde kullanılır. |
| `"..."` başlık | **Görselin altında**, çerçevenin içinde, ince bir çizgiyle ayrılmış olarak. |

Başlık yazılmazsa `alt` metni altbilgi olarak kullanılır (eski içerik bozulmasın diye).
Yeni içerikte ikisini de yazmak doğrusu: `alt` erişilebilirlik, başlık okuyucu için.

### Altbilgide satır içi markdown çalışır

Altbilgi normal metin gibi işlenir; **kalın**, `kod` ve **bağlantı** yazılabilir.
Kaynak göstermek için ayrı bir alan yok, bağlantıyı doğrudan cümleye koy:

```markdown
![Pal açısı şeması](image/09_amtp.webp "Değişken hatveli bir pervanede pal açısının feather, power, flight idle, ground idle ve reverse bölgeleri arasında nasıl değiştiği. Kaynak: [FAA AMT Handbook — Bölüm 7](https://www.faa.gov/...)")
```

Böyle yazıldığında altbilgi hem açıklamayı hem tıklanabilir kaynağı taşır.

> **Kendi çekimin olmayan bir görselde kaynağı yazmak zorunludur.** Referans görseli
> ile kendi işin arasındaki fark yalnızca bu satırdan anlaşılır.

### Çerçeve

Görseller çerçeve içinde çıkar: kendi yüzeyi, kenarlığı ve altbilgi bölmesi olan bir
`<figure>`. Genişlik her görselde aynı, yükseklik doğal oranına bırakılır. Görsele
tıklanınca tam ekran önizleme açılır (Esc ile kapanır).

---

## Yeni içerik yayınlama

İçerik bu repoda, kod ayrı bir repoda — **iki depolu bir işlem**:

1. Dosyaları ekle (`blog/post/<slug>/` veya `project/<slug>/`), görselleri `image/` altına.
2. Metadata'yı **markdown front matter'ına** yaz (`published: true` dahil), sonra indeksi üret:
   `cd ../site && npm run build:index`. `blog/index.json`'ı elle düzenleme — üretiliyor.
   (Projeler için indeks hâlâ elle.)
3. **`blog` dalına commit + push et.** Yerel diskteki dosyalar hiçbir şeyi etkilemez;
   uygulama içeriği yalnızca CDN'den okur.
4. jsDelivr cache'ini temizle:

   ```text
   https://purge.jsdelivr.net/gh/faruktoy/blog-assets@blog/blog/index.json
   https://purge.jsdelivr.net/gh/faruktoy/blog-assets@blog/blog/post/<slug>/tr.md
   ```

   Editördeki **CDN Purge** düğmesi bunu yapar.
5. **Siteyi yeniden build edip deploy et.** Bu adım atlanırsa yazı SPA'da görünür ama
   **prerender edilmiş HTML'i ve sitemap girdisi olmaz** — yani crawler'lar ve LinkedIn
   için yazı hâlâ yoktur. Atlanması en kolay adım budur.

## Ana sayfada hangi proje, hangi sırayla?

İkisi de `project.json` içinde, yani **içerikte**:

```json
{ "featured": true, "order": 2 }
```

- `featured: true` → ana sayfada "Öne Çıkan Projeler" bölümünde tam kartla görünür.
  `false` → "Diğer Projeler" içinde kompakt kartla.
- `order` → portfolyodaki sıra (küçük olan önce). İsteğe bağlı: `order` verilmemiş bir
  proje, `order` verilmiş olanların **ardına** düşer. Yani bir projeye sıra vermek
  diğerlerini yeniden numaralamayı gerektirmez.

Ana sayfa bu dosyayı çalışma anında okur ve **prerender edilmez**. Sıra ya da öne çıkan
değişikliği için siteyi yeniden yayınlamak gerekmez: `blog` dalına push et, CDN'i purge et,
değişiklik canlıdır.

Kart metni de buradan gelir — başlık ve özet `tr.md` / `en.md` front matter'ından,
etiket `category`'den, teknoloji rozetleri `technologies`'ten.

### `technologies` yalnızca özel ad taşır

Bu alan **dile bağlı değildir** (K5-A) ve iki dilde de aynı rozetler gösterilir. O yüzden
içine yalnızca çevrilmeyen adlar girer: dil, kütüphane, standart, malzeme, yazılım.

```
✔  Python · SolidWorks · Arduino · OMR · SQL · FDM · ABS/CF · PWM · CAD/CAM
✘  Görüntü İşleme · Image Processing · Teknik Resim · Elektronik · Bearings
```

Çevirisi olan genel bir ifade yazarsan diğer dildeki sayfada yabancı bir rozet olarak
durur. Anlatmak istediğin şey rozete sığmıyorsa metnin içinde anlat — rozet bir etiket
şeridi, içerik listesi değil. (K12-A)

---

## Bu depo public

Buradaki her dosya herkese açık. İçerik dosyalarına çalışma notu, yapılacaklar listesi
veya kişiye özel yönerge yazma; yalnızca içeriğin kendisi ve gerekiyorsa kısa bir
eksiklik notu bulunsun:

```markdown
<!-- Bu sayfa henüz yazılmadı. -->
```

---

## Taslak içerik

`published: false` olanlar: listede görünmez, CDN'den çekilmez, sitede hiçbir yere yansımaz.
Markdown dosyaları repoda durabilir.

---

## Adres kuralları

- Yazılar: `blog.faruktoy.com/<slug>` — her dil kökte, kendi benzersiz slug'ıyla.
- Projeler: `faruktoy.com/projects/<slug>`.
- **Eski adres asla silinmez.** Bir slug değişirse eskisi eski-adres listesine taşınır ve
  301 ile yenisine yönlendirilir; LinkedIn'de paylaşılmış olabilir.
- Bu listenin adı **her yerde `legacySlugs`** (karar K11-B) — yazılarda da, projelerde de.
  `aliases` yazarsan üretici build'i düşürür: sessizce yok saymak, o adreslerin 301 tablosuna
  hiç girmemesi ve bir bağlantının fark edilmeden ölmesi demekti.
