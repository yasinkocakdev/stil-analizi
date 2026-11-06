# Günlük Geliştirme Planı

Her gün küçük ama gerçek bir adım atılır ve bir commit'le kaydedilir. Sıra taslaktır; tasarım netleştikçe güncellenir.

Commit mesajları [Conventional Commits](https://www.conventionalcommits.org/) biçiminde yazılır: `tür(alan): ne yapıldı`.

| Gün | Adım | Commit mesajı |
|-----|------|---------------|
| 1 | README, tasarım taslağı, .gitignore | `docs: add README, design draft and .gitignore` |
| 2 | Açık soruları cevapla, tasarımı tamamla | `docs: finalize design decisions` |
| 3 | Python proje iskeleti ve klasör yapısı | `chore: set up Python project structure` |
| 4 | instaloader ile tek post ve tek highlight indirme testi | `feat(download): add instaloader download step` |
| 5 | Manuel klasör desteği (yedek yol) | `feat(download): support manual media folder` |
| 6 | ffmpeg ile videodan kare çıkarma | `feat(preprocess): extract frames from videos` |
| 7 | Birbirine çok benzeyen kareleri eleme | `feat(preprocess): remove near-duplicate frames` |
| 8 | Kıyafet analizi için JSON şeması | `feat(analysis): define outfit JSON schema` |
| 9 | `/stil-analizi` komutunun iskeleti | `feat: add /stil-analizi command skeleton` |
| 10 | Görselleri partiler halinde analiz etme | `feat(analysis): batch image analysis` |
| 11 | Renk, parça ve marka özetini çıkarma | `feat(summary): aggregate colors, items and brands` |
| 12 | Benzer ürünleri internette araştırma | `feat(shopping): research similar products` |
| 13 | Lokal HTML rapor | `feat(report): generate local HTML report` |
| 14 | Kombin önerileri bölümü | `feat(report): add outfit suggestions` |

Sonrası: PDF çıktısı, testler, rapor tasarımının güzelleştirilmesi, iki hesabı karşılaştırma.
