# Günlük Geliştirme Planı

Proje, 6 aylık C# planının yanında günde yaklaşık **2 saatle** ilerler. Her gün küçük ama gerçek bir adım atılır ve bir commit'le kaydedilir. Plan her ayın başında, o ayın konularına göre yenilenir.

Bir adım, C# planında henüz gelmediğin bir konuyu gerektiriyorsa yerini bir sonraki adımla değiştir. Asıl iş C# planıdır.

Commit mesajları [Conventional Commits](https://www.conventionalcommits.org/) biçiminde yazılır: `tür(alan): ne yapıldı`.

## Tamamlananlar

| Gün | Tarih | Adım | Commit |
|-----|-------|------|--------|
| 1 | 2026-11-06 | README, tasarım taslağı, .gitignore | `docs: add README, design draft and .gitignore` |
| 1 | 2026-11-06 | C# ve lokal model yönüne geçiş | `docs: switch to local-first C# design and month 1 plan` |

## 1. ay: Konsol uygulaması (`StilAnalizi.Cli`)

**Ay sonu hedefi:** Elle yazılmış kıyafet verisini okuyup "en sık renkler, parçalar ve markalar" raporu basan, README'si olan bir konsol uygulaması. Bu sürüm bile bir stil profili çıkarır, çünkü veriyi sen fotoğraflara bakarak yazacaksın.

| Gün | Adım | Commit mesajı |
|-----|------|---------------|
| 2 | .NET 10 SDK'yı kur, `StilAnalizi.Cli` konsol projesini oluştur, `.gitignore`'a .NET kalıplarını ekle | `chore: create .NET 10 console project` |
| 3 | `samples/outfits.json` dosyasına fotoğraflara bakarak 10 kombin yaz (parçalar, renkler, marka) | `feat: add sample outfit data` |
| 4 | Dosyayı okuyup ekrana yazdır | `feat: read sample outfits from file` |
| 5 | `Outfit` sınıfı ve `System.Text.Json` ile listeye dönüştürme | `feat: parse outfits into a list` |
| 6 | En sık geçen renkleri `Dictionary<string, int>` ile say | `feat: count most common colors` |
| 7 | Aynı yöntemle parçaları ve markaları say | `feat: count items and brands` |
| 8 | İlk 5'leri düzenli bir rapor halinde yazdır | `feat: print style summary report` |
| 9 | Dosya yolunu komut satırından al, dosya yoksa anlaşılır hata ver | `feat: accept file path argument` |
| 10 | Boş dosya ve bozuk JSON durumlarını yakala | `fix: handle empty or invalid input` |
| 11 | Sayma kodlarını ayrı metotlara böl | `refactor: extract counting methods` |
| 12 | İkinci hesap için 10 kombin ekle, iki stili yan yana göster | `feat: compare two style profiles` |
| 13 | README'ye "nasıl çalıştırılır" bölümü ve örnek çıktı ekle | `docs: add usage instructions` |
| 14 | Haftalık notlar: ne öğrendim, nerede takıldım | `docs: add progress notes` |

**İlk LinkedIn paylaşımı (1. ay sonu):** Problem ne, ilk sürüm ne yapıyor, ne öğrendim. Örnek çıktının ekran görüntüsüyle birlikte.
