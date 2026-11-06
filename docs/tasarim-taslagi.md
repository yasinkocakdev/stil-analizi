# Stil Analizi: Tasarım Taslağı

- **Durum:** Taslak. Beyin fırtınası sürüyor, onaylanmış bir tasarım değil.
- **Tarih:** 2026-11-06

## Amaç

Açık bir Instagram hesabının post ve highlight'larındaki kıyafetleri analiz edip kişinin moda stilini çıkarmak. Sonra bu stili kullanıcıya uyarlanmış bir alışveriş listesi ve kombin önerilerine dönüştürmek.

**Başarı ölçütü:** Kullanıcı raporu okuyunca "Bu kişi böyle giyiniyor, ben de şunları alıp şöyle kombinlerim" diyebilmeli.

## Kapsam

**Dahil:** Kıyafet, ayakkabı ve aksesuar; renk, kesim ve desen; görünen marka ya da logo; stil etiketleri (örneğin minimal, streetwear, old money).

**Hariç:** Kişinin kimliği, yüz tanıma, konum ve kişisel bilgiler. Kişi internette araştırılmaz; internet araştırması yalnızca ürün ve markalar için yapılır.

## Kullanım akışı

```
/stil-analizi <instagram-linki>
```

Kullanıcı yalnızca linki verir. Sistem gerisini baştan sona kendisi yapar.

## Mimari (taslak)

| # | Aşama | Ne yapar | Araç |
|---|-------|----------|------|
| 1 | İndirme | Postları ve highlight'ları `data/<kullanici>/raw/` klasörüne indirir | instaloader |
| 2 | Ön işleme | Videolardan kare çıkarır, birbirine çok benzeyen kareleri eler, kıyafet görünmeyen kareleri ayıklar | ffmpeg, perceptual hash |
| 3 | Görsel analizi | Her görsel için yapılandırılmış bir JSON üretir: parçalar, renkler, kesim, marka, stil etiketleri | Claude Code (görseller partiler halinde alt ajanlara dağıtılır) |
| 4 | Birleştirme | Tüm JSON'lardan özet çıkarır: renk paleti, en sık giyilen parçalar, markalar, tekrar eden kombin formülleri | Script |
| 5 | Ürün araştırması | Tespit edilen parça ve markalar için benzer ürünleri, fiyatları ve mağazaları bulur | Claude Code web araması |
| 6 | Rapor | Stil profili, alışveriş listesi ve kombin önerilerini içeren lokal bir HTML sayfası üretir | HTML (gerekirse sonra PDF) |

Her aşama sonucunu diske yazar. Böylece yarıda kalan bir çalıştırma kaldığı yerden devam edebilir. Bu önemli, çünkü görsel çok olduğunda analiz birkaç oturuma yayılabilir.

### İndirme kuralları

- Highlight'lar için kullanıcı instaloader'a terminalde bir kez kendisi giriş yapar. Şifre kodda veya repoda tutulmaz.
- İndirme yavaş ve sakin yapılır. Bot korumasını atlatma girişimi (proxy, sahte tarayıcı kimliği vb.) olmaz.
- Instagram engel ya da doğrulama isterse sistem durur ve kullanıcıya haber verir.
- **Yedek yol:** Kullanıcı ekran kaydı veya ekran görüntülerini `data/<kullanici>/manual/` klasörüne koyar. 2. aşamadan sonrası aynı şekilde çalışır.
- **Risk:** Otomatik indirme Instagram'ın kullanım koşullarına aykırıdır ve hesap kısıtlanabilir. Bu riski kullanıcı kabul eder.

## Verilen kararlar

| Konu | Karar |
|------|-------|
| Girdi | Instagram profil linki |
| Veri toplama | instaloader; yedek olarak manuel klasör |
| Analiz motoru | Claude Code içinde (ek API anahtarı yok) |
| Odak | Yalnızca kıyafet |
| Çıktı | Lokal web sayfası; beğenilmezse PDF |
| Rapor içeriği | Moda analizi, alışveriş listesi, kombin önerileri |

## Gizlilik ve repo kuralları

- İndirilen medya ve üretilen raporlar yalnızca lokalde tutulur. `data/` ve `output/` klasörleri GitHub'a gönderilmez.
- Instagram oturum dosyaları repoya girmez.
- Raporlar kişisel kullanım içindir.

## Açık sorular

1. **Kombin önerileri kime göre?** Önerilerin kullanıcıya uyması için cinsiyet, beden/vücut tipi, bütçe ve mevcut gardırop gibi bilgilerden hangileri kullanılacak?
2. **Alışveriş listesi nereden?** Hangi ülke ve mağazalar (örneğin Türkiye'deki siteler mi, global markalar mı)? Fiyat aralığı ne olacak?
3. **İki hesap nasıl raporlanacak?** Ayrı raporlar mı olacak, yoksa iki stili karşılaştıran tek bir rapor mu?
4. **Script dili:** Python öneriliyor (instaloader Python ile yazılmış). Başka bir tercih var mı?
5. **Ölçek:** Hesap başına kabaca kaç post ve highlight var? Kullanım limiti planı buna göre yapılacak.
6. **instaloader bugün highlight'ları indirebiliyor mu?** Uygulamanın ilk adımında küçük bir testle doğrulanacak.
