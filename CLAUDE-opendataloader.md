# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proje Tanımı

Tıp fakültesi İç Hastalıkları (Dahiliye) ders notlarını içeren bir Markdown bilgi tabanı. PDF ders materyallerinden **opendataloader-pdf** ile yapılandırılmış içerik çıkarılır, Claude ile Markdown notlarına dönüştürülür.

- **Dil:** Türkçe (tıbbi terminoloji dahil)
- **Kurum:** ADÜ Tıp Fakültesi - İç Hastalıkları
- **Yayın platformu:** GitBook (`SUMMARY.md`)

---

## PDF'den Not Üretim İş Akışı

### 1. PDF Türünü Belirle

```bash
# PDF'in metin katmanı var mı kontrol et
pdfinfo dosya.pdf
```

- Dijital PDF (slayt, e-kitap) → **Adım 2a (Dijital)**
- Taranmış PDF (fotokopi, fotoğraf) → **Adım 1b**, sonra **Adım 2a (Taranmış)**

### 1a. Dijital PDF (Slayt / E-kitap)

Metin PDF'in içine gömülü olduğundan OCR gerekmez. opendataloader-pdf yerel modda çalışır, Java haricinde ek bağımlılık yoktur.

```bash
# Kurulum (bir kez)
pip install -U opendataloader-pdf   # Java 11+ gerekli

# Markdown + JSON çıkar
opendataloader-pdf dosya.pdf --output-dir ./parsed --format markdown,json

# Klasör toplu işleme
opendataloader-pdf ./klasor/ --output-dir ./parsed --format markdown,json
```

Karmaşık/kenarsız tablo içeren slaytlar için hybrid mod:

```bash
pip install -U "opendataloader-pdf[hybrid]"

# Terminal 1
opendataloader-pdf-hybrid --port 5002

# Terminal 2
opendataloader-pdf --hybrid docling-fast dosya.pdf --output-dir ./parsed --format markdown,json
```

### 1b. Taranmış PDF'leri Önce OCR'la (yalnızca taranmış PDF'ler için)

```bash
# pdf-ocr-machine ile Tesseract Türkçe OCR uygula
pdf-ocr dosya.pdf --output-dir ./ocr-output --lang tur+eng
# Çıktı: ocr-output/dosya.pdf (metin katmanlı)
```

### 2a. Taranmış PDF → opendataloader-pdf ile Yapılandırılmış İçerik Çıkar

OCR uygulanmış PDF (`ocr-output/dosya.pdf`) artık metin katmanlı, opendataloader-pdf local modda parse eder:

```bash
opendataloader-pdf ocr-output/dosya.pdf --output-dir ./parsed --format markdown,json
```

### 2b. Görselleri Çıkar

```bash
# Görsel çıkarma (poppler - değişmedi)
pdfimages -png dosya.pdf konu-adi-images/image
```

- Görselleri `konu-adi-images/` klasörüne taşı (aynı dizinde)
- Sıralı isimlendirme: `image-000.png`, `image-001.png`, `image-002.png`...
- Gereksiz/boş/dekoratif görselleri ayıkla

### 3. Markdown Ders Notu Oluşturma

opendataloader-pdf'in çıktısı (`parsed/dosya.md`) başlık hiyerarşisini, tabloları ve okuma sırasını büyük ölçüde korur. Bu dosyayı Claude'a ver:

- Aşağıdaki **Referans Format** bölümüne uygun şekilde yeniden yapılandır
- Görselleri ilgili metin bölümlerine yerleştir
- Tabloları kontrol et — opendataloader genellikle hazır getirir, gerekirse düzelt
- JSON çıktısındaki (`parsed/dosya.json`) bounding box bilgisi hangi görselin nerede olduğunu bulmak için kullanılabilir

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
| -------- | -------- | -------- |
| Veri     | Veri     | Veri     |
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

### ASCII Akış Şemaları
```markdown
         Tetikleyici Faktör
                ↓
        ┌───────┴────────┐
        ↓                ↓
   Durum A           Durum B
        ↓                ↓
   Sonuç A           Sonuç B
```

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
- Uzun çizgi (em dash) kullanma
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
