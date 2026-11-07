# Veri

Bu klasördeki veri dosyaları git'e **eklenmez** (`.gitignore`). Bu README'den başka bir dosya git'e girmez.

## Kaynak

**Anthropic Economic Index**, Hugging Face: <https://huggingface.co/datasets/Anthropic/EconomicIndex>
Lisans: veri CC-BY, kod MIT.

| Dosya | Hugging Face yolu |
|---|---|
| `onet_task_statements.csv` | `release_2025_02_10/onet_task_statements.csv` |
| `task_penetration.csv` | `labor_market_impacts/task_penetration.csv` |
| `job_exposure.csv` | `labor_market_impacts/job_exposure.csv` |

Doğrudan indirme linki: `https://huggingface.co/datasets/Anthropic/EconomicIndex/resolve/main/<yol>`

## İndirme (isteğe bağlı)

Notebook dosyaları burada bulamazsa doğrudan Hugging Face'ten okur. Çevrimdışı çalışmak
veya veri sürümünü sabitlemek için dosyaları buraya indirin (proje kökünden, PowerShell):

```powershell
$B = "https://huggingface.co/datasets/Anthropic/EconomicIndex/resolve/main"
Invoke-WebRequest "$B/release_2025_02_10/onet_task_statements.csv" -OutFile data/onet_task_statements.csv
Invoke-WebRequest "$B/labor_market_impacts/task_penetration.csv"   -OutFile data/task_penetration.csv
Invoke-WebRequest "$B/labor_market_impacts/job_exposure.csv"       -OutFile data/job_exposure.csv
```

Not: `labor_market_impacts` klasöründe README yoktur (Kasım 2026 itibarıyla). Sütun tanımları
için: <https://www.anthropic.com/research/labor-market-impacts>
