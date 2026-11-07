# Proje kuralları (yapay zekâ asistanları ve insanlar için)

Bu repoda kod yazan veya değiştiren herkes (Claude Code dahil) aşağıdaki kurallara uymalıdır.

## Kapsam
- Şu anki aşama **veriyi anlamak ve betimleyici bulgular** çıkarmak. Model ya da çıkarımsal analiz yok.
- Görev çevirileri ve temaları (`GOREV_TR`) elle atanmıştır, veri değildir. Bu her yerde belirtilmelidir.
- Mevcut notebook: `notebooks/00_veriyi_tani.ipynb`. Diğer notebook'lar (otomasyon/destek, zaman trendi)
  proje sahibi karar vermeden **yazılmaz**.

## Kod kuralları
- Python 3.12+. Sürümler `requirements.txt`'te sabittir.
- `SEED = 42`. Tüm rastgelelik bu tohumla sabitlenir.
- `try/except` kullanılmaz. Uyarılar kapatılmaz (`warnings.filterwarnings("ignore")` yasak).
- Her adımda satır sayısı yazdırılır. Satır silen veya çoğaltabilen her işlem (filtre, birleştirme,
  tekrar silme) öncesi ve sonrası sayıyı `log()` ile yazar. Açıklamasız `dropna()` yasaktır.
- Dosya ve sütun adları tahmin edilmez. Okunduktan sonra varlıkları `assert` ile kontrol edilir.
- Her kod hücresinin üstünde Türkçe bir markdown açıklaması bulunur: ne yapıyor, neye bakılmalı.

## Veri
- Veri git'e yüklenmez (`.gitignore: data/`). İndirme adımı `data/README.md` içindedir.
- Kaynak: Anthropic Economic Index (Hugging Face, CC-BY).

## Veriyle ilgili bilinen tuzaklar
- **Meslek kodu biçimi:** `job_exposure` → `13-1071`; `onet_task_statements` → `13-1071.00`.
  Eşleştirme kodun **ilk 7 karakteriyle** yapılır, `.00` kırpılarak değil. Bazı meslekler yalnızca
  alt kodlarla gelir (ör. Muhasebeci: `13-2011.01`, `13-2011.02`; `.00` yok).
- **0 ≠ kullanım yok.** `penetration` ve `observed_exposure` için 0, "kullanım minimum eşiğin altında
  kaldı / yeterince gözlenmedi" demektir. Eşiğin değeri yayımlanmamıştır.
- **Görev birleştirme metinle yapılır** (`task_penetration`'da Task ID yok). Normalizasyon: `strip().lower()`.
  Eşleşmeyen görevler **NaN** kalır, 0 ile doldurulmaz. Eşleşme sayıları her zaman yazdırılır.
- `task_penetration`'da normalize edilmiş metni aynı olan satırlar var. Silinmeden önce penetration
  değerlerinin aynı olduğu `assert` ile doğrulanır.
- `Task Type` sütununda boş değerler var. Bunlar "Belirtilmemiş" olarak gösterilir, silinmez.

## İK meslekleri
| Kod | Türkçe ad | Grup |
|---|---|---|
| 11-3121 | İK Müdürü | İK |
| 11-3111 | Ücret ve Yan Haklar Müdürü | İK |
| 13-1071 | İK Uzmanı | İK |
| 13-1141 | Ücret, Yan Haklar ve İş Analizi Uzmanı | İK |
| 13-1151 | Eğitim ve Geliştirme Uzmanı | İK |
| 43-3051 | Bordro ve Puantaj Memuru | İK |
| 43-4161 | İK Asistanı | İK |
| 13-2011 | Muhasebeci | Karşılaştırma |
| 43-3031 | Muhasebe Memuru | Karşılaştırma |

## Etik
- Bu veriler meslek ve görev düzeyindedir. Bulgular bireyler veya belirli çalışanlar hakkında yargıya
  dönüştürülmez. `observed_exposure` bir "risk" ya da "işten çıkarma" skoru olarak sunulmaz.
