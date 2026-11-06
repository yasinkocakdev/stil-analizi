# stil-analizi

Kıyafet fotoğraflarından **stil profili** çıkaran, bunu alışveriş listesi ve kombin önerilerine dönüştüren, kendi bilgisayarında çalışan bir C# uygulaması.

> **Durum: Beklemede.** Şu an 6 aylık C# öğrenme planıma odaklanıyorum. stil-analizi, bu plan tamamlandıktan sonra (tahmini Mayıs 2027) geliştirilecek. Tasarım ve yol haritası hazır durumda.

## Hangi problemi çözüyor?

Beğendiğin bir tarzı (bir hesabın paylaşımlarını, kaydettiğin fotoğrafları) incelemek için yüzlerce fotoğrafa tek tek bakmak gerekir. stil-analizi bu fotoğrafları analiz eder ve şunları çıkarır:

- **Stil profili:** Renk paleti, en sık giyilen parçalar, görünen markalar, tekrar eden kombin formülleri.
- **Alışveriş listesi:** Bu tarzı yakalamak için alınabilecek parçalar.
- **Kombin önerileri.**

## İlkeler

- **Lokal ve ücretsiz:** Analiz varsayılan olarak bilgisayarındaki bir yapay zekâ modeliyle (Ollama) yapılır. Fotoğrafların hiçbir yere gönderilmez.
- **İsteğe bağlı yüksek kalite modu:** İstersen kendi API anahtarını girip daha güçlü bir model kullanabilirsin.
- **Sadece kıyafet:** Yüz tanıma, kimlik ya da konum bilgisi yok.
- **Kurulumsuz:** Hedef, çift tıklayınca açılan bir program.

## Teknoloji

.NET 10 · C# 14 · Blazor · EF Core + SQLite · Ollama · xUnit · GitHub Actions

## Yol haritası

- [x] Fikir ve tasarım ([docs/tasarim-taslagi.md](docs/tasarim-taslagi.md))
- [ ] 1. ay: Konsol uygulaması, elle yazılmış veriden stil istatistiği
- [ ] 2. ay: Çekirdek kütüphane, modeller, testler
- [ ] 3. ay: Lokal yapay zekâyla gerçek fotoğraf analizi
- [ ] 4. ay: Sürükle bırak arayüz ve rapor ekranı
- [ ] 5. ay: Yüksek kalite modu ve güvenlik
- [ ] 6. ay: Windows ve macOS için indirilebilir sürüm

Gün gün plan: [docs/gunluk-plan.md](docs/gunluk-plan.md)

## Nasıl çalıştırılır?

İlk sürüm hazır olduğunda burada anlatılacak.

## Ne öğrendim?

Her ayın sonunda buraya kısa notlar eklenecek.
