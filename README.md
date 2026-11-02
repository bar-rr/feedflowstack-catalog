# FeedFlowStack Catalog

FeedFlowStack uygulamasının **uzaktan güncellenen RSS kataloğu**. Uygulama bu dosyayı okur;
bu sayede bozuk RSS adresleri düzeltilir ve ülke listeleri **APK güncellemeden** değiştirilir.

> ⚠️ Repo adı (`feedflowstack-catalog`), dal adı (`main`) ve dosya yolu (`v1/catalog.json`) **değiştirilmemeli** —
> adres uygulamanın içine gömülüdür:
> `https://raw.githubusercontent.com/bar-rr/feedflowstack-catalog/main/v1/catalog.json`

Bu repoda GitHub Actions yoktur; düzenlemeler GitHub kredisi harcamaz.

## Yapı

```
v1/catalog.json    # Tek dosya: ülkeler, feed'ler, yönlendirmeler
```

## catalog.json alanları

| Alan | Açıklama |
|---|---|
| `schemaVersion` | Dosya formatı. Uygulama sadece tanıdığı sürümü okur. **Elle değiştirmeyin.** |
| `catalogVersion` | Her düzenlemede **1 artırın**. Uygulama yeni sürümü görünce listeyi yeniler. |
| `updated` | Son düzenleme tarihi (YYYY-AA-GG). |
| `countries` | Ana ekrandaki ülke butonları. Sıra = butonların sırası. |
| `countries[].feeds` | O ülkenin hazır RSS listesi. |
| `redirects` | Bozuk adres → yeni adres. Kullanıcının listesindeki eski adres otomatik değişir. |
| `disabled` | Artık çalışmayan adresler. Hazır listeden gizlenir. |

### Feed örneği

```json
{ "name": "CNN Türk", "url": "https://www.cnnturk.com/feed/rss/all/news", "category": "news" }
```

`category` değerleri: `news`, `tech`, `sports`, `business`, `science`, `world`.

### Yönlendirme örneği

```json
"redirects": {
  "https://eski-site.com/rss": "https://yeni-site.com/feed"
}
```

## Telefondan / tabletten düzenleme

1. GitHub uygulamasında veya tarayıcıda `v1/catalog.json` dosyasını açın → kalem (Edit) simgesi.
2. Değişikliği yapın, **`catalogVersion` değerini 1 artırın**.
3. "Commit changes" → doğrudan `main` dalına.

Dikkat: JSON'da virgüller önemlidir — son elemandan sonra virgül olmaz. Bozuk JSON gelirse
uygulama bu dosyayı yok sayar ve önceki/yerleşik listeyi kullanmaya devam eder.
