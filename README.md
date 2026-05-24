# blog-assets — `blog` branch

Bu repo, **faruktoy.com/blog** için CDN üzerinden yayınlanan içerik dosyalarını barındırır.  
Ana site ([portfolio repo](https://github.com/faruktoy/portfolio)) build almadan bu repoya bakarak blog içeriğini günceller.

**CDN base URL:** `https://cdn.jsdelivr.net/gh/faruktoy/blog-assets@blog`

---

## Dizin yapısı

```
/
├── index.json              ← Blog yazı listesi (canlı index)
└── post/
    ├── fdm-yuzey-kalitesi/
    │   ├── tr.md
    │   └── en.md
    ├── TurboProp/
    │   ├── c130_turboprop_demonstrator_TR.md
    │   └── c130_turboprop_demonstrator_EN.md
    ├── abs-cf-prototipleme/
    │   ├── tr.md
    │   └── en.md
    └── p3steel-build-log/
        ├── tr.md
        └── en.md
```

---

## index.json

Blog anasayfasının kart listesi ve her yazının CDN yolunu tanımlayan ana dosya.  
Site build almadan yeni yazı yayınlamak veya mevcut yazıyı kaldırmak için sadece bu dosyayı düzenlemek yeterlidir.

### Alan referansı

| Alan | Tip | Açıklama |
|------|-----|----------|
| `slug` | string | Dahili ID. `loadBlogPost` ve cache anahtarı olarak kullanılır. |
| `slugs.tr` | string | Türkçe URL segmenti (örn. `/fdmRA`) |
| `slugs.en` | string | İngilizce URL segmenti. TR ile aynıysa `/en/<slug>` olur, farklıysa standalone (örn. `/ra-in-fdm`) |
| `published` | boolean | `false` ise blog listesinde görünmez, CDN'den içerik çekilmez. |
| `featured` | boolean | `true` ise anasayfada öne çıkan (hero) bölümde gösterilir. |
| `category` | string | `printing` · `aviation` · `it` |
| `mdPath` | string | CDN'deki klasör yolu (örn. `post/fdm-yuzey-kalitesi`) |
| `mdFiles.tr` | string | TR markdown dosya adı |
| `mdFiles.en` | string | EN markdown dosya adı |
| `tr` / `en` | object | Kart için başlık, açıklama, tarih, okuma süresi |

### Örnek giriş

```json
{
  "slug": "fdm-yuzey-kalitesi",
  "slugs": { "tr": "fdmRA", "en": "ra-in-fdm" },
  "published": true,
  "featured": true,
  "category": "printing",
  "mdPath": "post/fdm-yuzey-kalitesi",
  "mdFiles": { "tr": "tr.md", "en": "en.md" },
  "tr": { "title": "...", "desc": "...", "date": "30 Nisan 2026", "readTime": "12 dk" },
  "en": { "title": "...", "desc": "...", "date": "Apr 30, 2026", "readTime": "12 min" }
}
```

---

## Markdown formatı

Her `.md` dosyası şu yapıyı takip eder:

```markdown
---
title: Yazı Başlığı
date: 30 Nisan 2026
readTime: 12 dk okuma
tags: Etiket1, Etiket2
---

# Yazı Başlığı

> Giriş cümlesi (tek paragraf, italik kutu olarak gösterilir)

## Bölüm Başlığı

Bölüm içeriği...

## Kaynaklar

[1]: https://example.com "Kaynak Başlığı"
[2]: https://example.com "Kaynak Başlığı"
```

**Kurallar:**
- Frontmatter (`---`) zorunlu değil ama `title`, `date`, `readTime`, `tags` alanları varsa kullanılır.
- `# Başlık` → yazı adı. Yoksa `index.json`'daki `tr.title` / `en.title` kullanılır.
- `> Giriş` → blockquote olarak yazılan ilk satır intro olur.
- `## Kaynaklar` / `## References` bölümü otomatik olarak referans kutusuna dönüştürülür.
- `[n]: url "Başlık"` formatındaki link tanımları referans listesine eklenir.

---

## Yeni yazı yayınlama

1. Markdown dosyalarını `post/<slug>/tr.md` ve `post/<slug>/en.md` olarak ekle.
2. `index.json`'a yeni bir giriş ekle (`published: true`).
3. jsDelivr cache'ini temizle (editör otomatik yapar):
   ```
   https://purge.jsdelivr.net/gh/faruktoy/blog-assets@blog/index.json
   https://purge.jsdelivr.net/gh/faruktoy/blog-assets@blog/post/<slug>/tr.md
   ```

Editörde **Yayınla** butonuna basıldığında bu adımların tamamı otomatik gerçekleşir.

---

## Taslak yazı

`published: false` olan yazılar:
- Blog listesinde görünmez.
- CDN'den içerik çekilmez.
- Editörde localStorage'dan preview yapılabilir.

Markdown dosyaları repoda bulunabilir ama `published: false` olduğu sürece siteye yansımaz.
