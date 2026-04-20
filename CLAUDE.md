# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proje Tanımı

Tıp fakültesi İç Hastalıkları (Dahiliye) ders notlarını içeren bir Markdown bilgi tabanı. PDF ders materyallerinden **poppler** araçları ile metin/görsel çıkarılır, Claude ile yapılandırılmış Markdown notlarına dönüştürülür.

- **Dil:** Türkçe (tıbbi terminoloji dahil)
- **Kurum:** ADÜ Tıp Fakültesi - İç Hastalıkları
- **Yayın platformu:** GitBook (`SUMMARY.md`)

## Repo Yapısı

```
pd/
├── Gastroenteroloji/
│   ├── notlar/              ← Yayınlanan ders notları (.md + -images/)
│   ├── Berk Baş/            ← Hoca bazlı kaynak PDF/ham dosyalar
│   ├── Mehmet Hadi Yaşa/
│   └── İsmail Taşkıran/
├── Endokrinoloji/notlar/
├── Nefroloji/notlar/
├── Hematoloji/notlar/
├── Romatoloji/notlar/
├── Onkoloji/notlar/
├── İmmunoloji ve Alerji/notlar/
├── cikmis-sorular/          ← Sınav çıkmış soruları
├── STÇ/                     ← Stajyer tamamlayıcı çıkmışlar (ayrı yapı)
├── SUMMARY.md               ← GitBook içindekiler
└── README.md                ← Ana sayfa (GitBook + genel)
```

- Her uzmanlık dalının yayınlanan notları `UzmanlıkAdı/notlar/` altındadır
- Hoca bazlı alt klasörler (`UzmanlıkAdı/HocaAdı/`) kaynak PDF'ler içindir, yayına dahil değildir
- Görsel klasörleri her zaman notlarla aynı dizinde: `notlar/konu-adi-images/`
- **Dikkat:** `onkoloji/` vs `Onkoloji/` gibi case tutarsızlıkları mevcut (macOS case-insensitive ama Linux case-sensitive)

---

## PDF'den Not Üretim İş Akışı

### 0. PDF Türünü Belirle

```bash
pdfinfo dosya.pdf   # Metin katmanı var mı kontrol et
```

- Dijital PDF (slayt, e-kitap) → **Adım 1a**
- Taranmış PDF (fotokopi, fotoğraf) → **Adım 1b**, ardından **Adım 1a**

### 1a. Dijital PDF — opendataloader-pdf ile Parse Et

```bash
pip install -U opendataloader-pdf   # Java 11+ gerekli (bir kez)

opendataloader-pdf dosya.pdf --output-dir ./parsed --format markdown,json
```

Karmaşık/kenarsız tablolar içeren slaytlar için hybrid mod:

```bash
pip install -U "opendataloader-pdf[hybrid]"

# Terminal 1
opendataloader-pdf-hybrid --port 5002

# Terminal 2
opendataloader-pdf --hybrid docling-fast dosya.pdf --output-dir ./parsed --format markdown,json
```

`parsed/dosya.md` başlık hiyerarşisini ve tabloları büyük ölçüde hazır getirir. `parsed/dosya.json` bounding-box bilgisiyle hangi görselin nerede olduğu bulunabilir.

### 1b. Taranmış PDF — Önce OCR Uygula

```bash
pdf-ocr dosya.pdf --output-dir ./ocr-output --lang tur+eng
# Çıktı: ocr-output/dosya.pdf (metin katmanlı) → ardından 1a ile parse et
```

### 2. Görselleri Çıkar ve Düzenle

```bash
pdfimages -png dosya.pdf konu-adi-images/image   # Görsel çıkarma
```

- Görselleri `konu-adi-images/` klasörüne taşı (aynı dizinde)
- Sıralı isimlendirme: `image-000.png`, `image-001.png`, `image-002.png`...
- Gereksiz/boş/dekoratif görselleri ayıkla

### 3. Markdown Ders Notu Oluşturma

- Aşağıdaki **Referans Format** bölümüne uygun şekilde yapılandır
- Görselleri ilgili metin bölümlerine yerleştir
- Tabloları kontrol et — opendataloader genellikle hazır getirir, gerekirse düzelt

---

## Yeni Konu Eklerken Güncellenmesi Gereken Dosyalar

1. İlgili uzmanlık klasörüne `.md` dosyasını yerleştir
2. **`SUMMARY.md`** — GitBook içindekilere yeni konuyu ekle
3. **`README.md`** — Ana sayfadaki konu listesine ekle

---

## Referans Format (Anafilaksi.md Standardı)

### Dosya Başlığı
```markdown
# KONU BAŞLIĞI

**Hazırlayan:** Prof. Dr. Ad Soyad
**Bölüm:** İlgili Bölüm Adı

---
```

### İçindekiler (kapsamlı notlarda)
```markdown
## İÇİNDEKİLER

1. [Tanım ve Epidemiyoloji](#tanım-ve-epidemiyoloji)
2. [Patofizyoloji](#patofizyoloji)
...
```

### Bölüm Hiyerarşisi
- `##` → Ana bölümler (BÜYÜK HARF)
- `###` → Alt bölümler (İlk Harf Büyük)
- `####` → Alt-alt bölümler
- Bölümler arası ayırıcı: `---` veya `***`

### Tablo Formatı
```markdown
| Başlık 1 | Başlık 2 | Başlık 3 |
|---|---|---|
| Veri | Veri | Veri |
```
- Karmaşık hücre içerikleri için `<p>` ve `<br>` HTML etiketleri kullanılabilir

### Emoji Kullanımı
- Organ sistemleri: 🔴 🫁 💓 🤢 🧠 👁️
- Uyarılar: ⚠️ 🚨 ❌ ✅
- Yönler/değişimler: ↑ ↓ → ←
- Diğer: 💡 (ipucu), 📋 (vaka), 📊 (veri), ⭐ (önemli)
- **Başlıklarda emoji KULLANILMAZ**, sadece içerikte kullanılır

### Önemli Not Formatı
```markdown
**⚠️ ÖNEMLİ:**

* Kritik bilgi burada
* Bir diğer önemli nokta
```

### Klinik Vaka Formatı
```markdown
**📋 VAKA ÖRNEĞİ 1: Başlık**

**Hasta:** Yaş, cinsiyet, bilgi
**Öykü:** Klinik öykü
**Fizik Muayene:** Vital bulgular (Nabız X/dk, TA X/X mmHg, SpO₂ %X)
**Tanı:** ...
**Tedavi:** ...
**İzlem:** ...

**Öğretici Notlar:**
1. ...
2. ...
```

### Görsel Referans Formatı
```markdown
![Açıklayıcı Türkçe Alt Metin](klasor-images/image-000.png)
```

### Mermaid Diyagramları (tercih edilen akış şeması yöntemi)

PDF'deki algoritma/flowchart görselleri **Mermaid** formatında yeniden çizilir. Hem Obsidian (yerleşik destek) hem GitBook bunu otomatik render eder. Mermaid varsa görsel tekrara gerek yok -- görseli silip sadece mermaid bırakılır.

```markdown
\`\`\`mermaid
flowchart TD
    A[Başlangıç sorusu] --> B[Karar 1]
    A --> C[Karar 2]
    B -->|Evet| D([Sonuç A])
    B -->|Hayır| E([Sonuç B])

    classDef diagnose fill:#c8e6c9,stroke:#2e7d32,color:#1b5e20
    classDef exclude fill:#ffcdd2,stroke:#c62828,color:#b71c1c
    classDef test fill:#bbdefb,stroke:#1565c0,color:#0d47a1
    class D diagnose
    class E exclude
    class A,B,C test
\`\`\`
```

**Renk paleti (klinik anlam):**
- 🟢 `#c8e6c9` -- tanı konur / pozitif sonuç (`diagnose` sınıfı)
- 🔴 `#ffcdd2` -- dışlanır / kontrendikasyon (`exclude` sınıfı)
- 🔵 `#bbdefb` -- test/karar adımı (`test` sınıfı)
- 🟡 `#fff9c4` -- uyarı / ara karar (opsiyonel, `warning` sınıfı)

**Şekil kuralları:**
- `[]` dikdörtgen -- karar / test adımı
- `([])` yuvarlak köşeli -- final tanı / sonuç
- `{}` rombus -- evet/hayır kararı (opsiyonel)

**Diyagram tipleri:**
- `flowchart TD` -- algoritmalar (yukarıdan aşağı, en sık)
- `flowchart LR` -- soldan sağa (zaman çizelgeleri)
- `sequenceDiagram` -- hücre sinyali, ilaç-reseptör etkileşimleri
- `classDiagram` -- hastalık sınıflamaları
- `mindmap` -- konu özetleri

**ASCII akış şemaları artık tercih edilmez** -- mermaid daha okunaklı ve render edilebilir. Eski notlarda ASCII varsa zorla değiştirme; yeni notlarda mermaid kullan.

---

## Dosya Adlandırma Kuralları

- Ders notu dosya adı: **kebab-case** Türkçe (ör: `diyabet-mellitus.md`)
- Görsel klasörü: `konu-adi-images/` (not dosyasıyla aynı dizinde)
- Görsel dosyaları: `image-000.png`, `image-001.png`...

---

## Yazım Kuralları

- **Dil:** Türkçe tıbbi terminoloji (gerektiğinde parantez içinde İngilizce/Latince karşılık)
- **Vurgulama:** `**kalın**` tercih edilir, *italik* nadiren kullanılır
- **Listeler:** `*` veya `-` ile madde işareti, `1.` ile numaralı liste
- **Tıbbi birimler:** Standart kısaltmalar (mg/kg, mL, mmHg, /dk, %, U/L)
- **Vital bulgular:** `Nabız X/dk, TA X/X mmHg, Solunum X/dk, SpO₂ %X`
- **İlaç dozları:** `İlaç adı X mg/doz (maks: X mg)` formatı
- Blockquote (`>`) tanımlar ve klinik kurallar için kullanılır
- Gereksiz HTML kullanılmaz (tablo hücreleri hariç)

---

## Yapılmaması Gerekenler

- Başlıklara emoji ekleme
- Ham HTML kullanma (tablo hücreleri hariç)
- İngilizce içerik üretme (terim karşılıkları hariç)
- Mevcut dosyaların formatını bozmadan düzenleme yapma
- Görsel dosyalarını ana klasöre koyma (her zaman `-images/` alt klasörü kullan)
- Kaynak/hazırlayan bilgisi olmadan not oluşturma
- Uzun çizgi (em dash `—`) kullanma; tire (`-`) veya iki tire (`--`) kullan

---

## Anki Desteleri

Kullanıcı **Anki destesi / kartı** istediğinde:

- Çıktılar **her zaman** `~/Desktop/anki-d/` klasörü altına oluşturulur (proje klasörüne **değil**).
- Her ders notu için ayrı bir alt klasör aç: `~/Desktop/anki-d/<konu-adi>/`
- Format: **CSV**, ayırıcı **tab** (`\t`), iki alan: `ön<TAB>arka` — `&lt;` / `&gt;` gibi HTML entity'leri `;` ile bittiği için noktalı virgül ayırıcı **kullanılmaz**
- HTML'e izin verilir (Anki içe aktarımında "Allow HTML in fields" açık olmalı)
- Çoklu maddeli cevaplarda maddeler `<br>` ile alt alta ve **rotasyonlu renklerde** `<span style="color:#...">` etiketleriyle yazılır
- Renk paleti: `#e74c3c` (kırmızı), `#2980b9` (mavi), `#27ae60` (yeşil), `#e67e22` (turuncu), `#8e44ad` (mor), `#16a085` (teal)
- Her ana başlık için ayrı bir CSV dosyası oluşturulur (`01-...csv`, `02-...csv` şeklinde sıralı)
- Klasöre kısa bir `README.md` eklenir (içe aktarma talimatı + deste listesi)
