# stil-analizi

Açık bir Instagram hesabındaki post ve highlight'lardan **kıyafet stilini** çıkaran, sonucu alışveriş listesi ve kombin önerilerine dönüştüren kişisel bir araç.

> **Durum:** Taslak aşamasında. Tasarım kararları ve açık sorular: [docs/tasarim-taslagi.md](docs/tasarim-taslagi.md)

## Ne yapacak?

1. Instagram profil linkini alır.
2. Postları ve highlight'ları indirir, videolardan kare çıkarır.
3. Her görseldeki kıyafetleri analiz eder: parça, renk, kesim, görünen marka.
4. Bulunan parça ve markaları internette araştırır: benzer ürünler, fiyatlar, mağazalar.
5. Lokal bir web sayfası üretir: stil profili, alışveriş listesi, kombin önerileri.

## Planlanan kullanım

Claude Code içinde çalışan bir komut olarak tasarlanıyor:

```
/stil-analizi https://www.instagram.com/<kullanici-adi>/
```

## İlkeler

- **Sadece kıyafet:** Yüz tanıma, konum ya da kişisel bilgi toplama yok. İnternet araştırması yalnızca ürün ve markalar için yapılır.
- **İndirilen medya repoya girmez:** `data/` ve `output/` klasörleri `.gitignore` içinde.
- **Şifre kodda tutulmaz:** Instagram girişini kullanıcı terminalde kendisi yapar.

> **Uyarı:** Instagram'dan otomatik indirme, platformun kullanım koşullarına aykırıdır ve hesabın kısıtlanmasına yol açabilir. Sorumluluk aracı çalıştıran kullanıcıdadır.

## Yol haritası

Gün gün ayrıntılı plan: [docs/gunluk-plan.md](docs/gunluk-plan.md)

- [x] Fikir ve ilk kararlar
- [ ] Tasarımın tamamlanması
- [ ] İndirme ve videodan kare çıkarma
- [ ] Görsel analizi
- [ ] Ürün araştırması
- [ ] Web raporu
- [ ] PDF çıktısı (gerekirse)
