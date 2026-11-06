# Stil Analizi: Tasarım

- **Durum:** Yön onaylandı (v2). Ayrıntılar her ay o ayın konusuna göre netleşir.
- **Tarih:** 2026-11-06
- **v1'den farkı:** Claude Code'a bağımlılık ve Instagram'dan otomatik indirme kaldırıldı. Proje, herkesin kendi bilgisayarında çalıştırabileceği bir C# uygulamasına dönüştü.

## Amaç

Yazılım bilmeyen biri bile programı indirip kendi bilgisayarında çalıştırabilsin. Kıyafet fotoğraflarını verip şunları alsın:

- **Stil profili:** Renk paleti, sık giyilen parçalar, görünen markalar, tekrar eden kombin formülleri.
- **Alışveriş listesi:** Bu stili yakalamak için alınabilecek parçalar.
- **Kombin önerileri.**

**Başarı ölçütü:** Kullanıcı raporu okuyunca "Bu tarz böyle kuruluyor, ben de şunları alıp şöyle kombinlerim" diyebilmeli.

## İlkeler

- **Fotoğraflar kullanıcıdan gelir.** Ekran görüntüleri, kaydedilen fotoğraflar ya da kendi kıyafet fotoğrafları kullanılabilir. Program hiçbir siteden otomatik indirme yapmaz.
- **Sadece kıyafet analiz edilir.** Yüz tanıma, kimlik ve konum bilgisi yok.
- **Varsayılan olarak lokal ve ücretsiz çalışır.** Fotoğraflar bilgisayardan çıkmaz.
- **Kurulum gerektirmez.** Çift tıklayınca açılır, terminal bilgisi gerekmez.

## Mimari

```
Fotoğraflar ──► Ön işleme ──► IVisionAnalyzer ──► Sonuçlar (SQLite) ──► Özet ──► Rapor (Blazor arayüz)
                (video→kare,     ├─ OllamaAnalyzer   (varsayılan, lokal, ücretsiz)
                 benzer kareleri └─ ClaudeAnalyzer   (isteğe bağlı, kullanıcının API anahtarıyla)
                 eleme)
```

| Proje | Sorumluluk |
|-------|------------|
| `StilAnalizi.Core` | Modeller (`Outfit`, `Garment`, `StyleProfile`), `IVisionAnalyzer` arayüzü, özet çıkarma mantığı. Dış bağımlılığı yok. |
| `StilAnalizi.Analyzers` | `OllamaAnalyzer` ve `ClaudeAnalyzer`: fotoğrafı modele gönderip yapılandırılmış sonuç alır. |
| `StilAnalizi.Web` | Blazor arayüzü: fotoğraf yükleme, ilerleme durumu, rapor ekranı. Verileri SQLite'ta tutar (EF Core). |
| `StilAnalizi.Cli` | 1. ayın konsol uygulaması. Sonradan geliştirici aracı olarak kalır. |
| `StilAnalizi.Tests` | xUnit testleri. |

## Teknoloji

- **.NET 10 (LTS) ve C# 14.** Nullable açık, I/O işlemleri async.
- **Lokal model:** Ollama üzerinde görsel anlayan açık bir model. Model seçimi 3. ayda test edilerek yapılır. Rahat çalışması için 16 GB RAM önerilir.
- **Yüksek kalite modu:** Kullanıcı ayarlardan kendi API anahtarını girer. Anahtar düz metin olarak saklanmaz.
- **Veritabanı:** SQLite (kullanıcı ek bir şey kurmaz) + EF Core.
- **Dağıtım:** Windows ve macOS için `dotnet publish` ile tek dosya üretilir ve GitHub Releases'ta yayınlanır. ffmpeg programla birlikte gelir.

## 6 aylık C# planıyla hizalama

Proje, C# planının yanında günde yaklaşık 2 saatle ilerler. Her ay o ay öğrenilen konuyla bir kat büyür:

| Ay | Plandaki konu | Projeye eklenen |
|----|---------------|-----------------|
| 1 | Temeller, koleksiyonlar, Git | Konsol uygulaması: elle yazılmış kıyafet verisinden renk, parça ve marka istatistiği |
| 2 | OOP, interface, LINQ, xUnit | `StilAnalizi.Core`: modeller, `IVisionAnalyzer`, testler |
| 3 | async, HTTP, dosya, SQL | `OllamaAnalyzer`: gerçek fotoğraf analizi, sonuçların SQLite'a yazılması |
| 4 | DI, validation, EF Core | Blazor arayüzü: sürükle bırak yükleme, rapor ekranı |
| 5 | Güvenlik, loglama | API anahtarıyla yüksek kalite modu, güvenli anahtar saklama, dosya yükleme sertleştirme |
| 6 | CI, yayına alma | GitHub Actions, Windows ve macOS sürümleri, lansman |

Günlük adımlar: [gunluk-plan.md](gunluk-plan.md)

## Repo kuralları

- Kişisel fotoğraflar ve üretilen raporlar repoya girmez (`data/` ve `output/` klasörleri `.gitignore` içinde).
- Örnek veri yalnızca `samples/` klasöründe ve metin olarak tutulur, fotoğraf içermez.
- API anahtarları repoya girmez. Geliştirme sırasında `dotnet user-secrets` kullanılır.
- Commit mesajları İngilizce ve Conventional Commits biçimindedir.

## Açık sorular

1. **Kombin önerileri kime göre?** Kullanıcıdan hangi bilgiler alınacak: cinsiyet, beden, bütçe, mevcut gardırop? (4. ay)
2. **Alışveriş listesi:** Mağaza linkleri mi verilecek, yoksa sadece parça tarifi mi? Ülke ve mağaza seçimi nasıl olacak? (4. ay)
3. **Lokal model:** Hangi Ollama modeli kalite ve hız dengesini en iyi tutturuyor? (3. ay, test ile)
4. **İki stil karşılaştırması:** İlk sürümde olacak mı? (2. ay)
