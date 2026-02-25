# CLAUDE.md - Pediatri Ders Notları Reposu

## Proje Tanımı

Bu repo, tıp fakültesi pediatri ders notlarını içeren bir GitBook bilgi tabanıdır. PDF formatındaki ders materyallerinden **poppler** araçları (pdftotext, pdfimages) ile metin ve görseller çıkarılır, ardından Claude ile Anafilaksi.md referans formatında yapılandırılmış Markdown ders notlarına dönüştürülür.

**Dil:** Türkçe (tıbbi terminoloji dahil)
**Kurum:** ADÜ Tıp Fakültesi - Çocuk Sağlığı ve Hastalıkları

---

## PDF'den Not Üretim İş Akışı

### 1. PDF'den İçerik Çıkarma
```bash
# Metin çıkarma
pdftotext -layout dosya.pdf dosya.txt

# Görsel çıkarma (PNG formatında)
pdfimages -png dosya.pdf output-prefix
```

### 2. Görselleri Düzenleme
- Çıkarılan görselleri `konu-adi-images/` klasörüne taşı
- Sıralı isimlendirme: `image-000.png`, `image-001.png`, `image-002.png`...
- Gereksiz/boş/dekoratif görselleri ayıkla

### 3. Markdown Ders Notu Oluşturma
- Aşağıdaki **Referans Format** bölümüne uygun şekilde yapılandır
- Görselleri ilgili metin bölümlerine yerleştir
- Tabloları markdown tablo formatına dönüştür

---

## Referans Format (Anafilaksi.md Standardı)

Her ders notu aşağıdaki yapıyı takip eder:

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
3. [Klinik Bulgular](#klinik-bulgular)
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
- Başlıklarda emoji KULLANILMAZ, sadece içerikte kullanılır

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

## Klasör Yapısı

```
pd/
├── acil/                          # Çocuk Acil
├── alerji-immunoloji/             # Alerji ve İmmünoloji
├── enfeksiyon/                    # Enfeksiyon Hastalıkları
├── genel/                         # Genel Pediatri
├── gis/                           # Gastrointestinal Sistem
├── hemato/                        # Hematoloji-Onkoloji
│   ├── Hemoglobinopatiler.md
│   └── hemoglobinopatiler-images/ # Konu adı-images/ formatı
├── kardiyoloji/                   # Kardiyoloji
├── nefro/                         # Nefroloji
├── neon/                          # Neonatoloji
├── notlar/                        # Genel Notlar
├── yogun-bakim/                   # Yoğun Bakım
├── çıkmış/                        # Çıkmış Sorular
├── SUMMARY.md                     # GitBook İçindekiler
└── README.md                      # Proje Tanıtımı
```

### Yeni Konu Ekleme Kuralları
1. İlgili uzmanlık klasörüne yerleştir
2. Dosya adı: **kebab-case** Türkçe (ör: `atesli-cocuga-yaklasim.md`)
3. Görseller: `konu-adi-images/` alt klasörü, aynı dizinde
4. Görsel adlandırma: `image-000.png`, `image-001.png`...
5. `SUMMARY.md` dosyasına yeni konuyu ekle
6. `README.md` dosyasını güncelle

---

## Yazım Kuralları

- **Dil:** Türkçe tıbbi terminoloji (gerektiğinde parantez içinde İngilizce/Latince karşılık)
- **Vurgulama:** `**kalın**` tercih edilir, *italik* nadiren kullanılır
- **Listeler:** `*` veya `-` ile madde işareti, `1.` ile numaralı liste
- **Tıbbi birimler:** Standart kısaltmalar (mg/kg, mL, mmHg, /dk, %, U/L)
- **Vital bulgular:** `Nabız X/dk, TA X/X mmHg, Solunum X/dk, SpO₂ %X`
- **İlaç dozları:** `İlaç adı X mg/kg/doz (maks: X mg)` formatı
- Blockquote (`>`) tanımlar ve klinik kurallar için kullanılır
- Gereksiz HTML kullanılmaz (tablo hücreleri hariç)

---

## İzin Verilen Bash Komutları

```
pdftotext, pdfimages, ls, mkdir, mv, cp
```

---

## Yapılmaması Gerekenler

- Başlıklara emoji ekleme
- Ham HTML kullanma (tablo hücreleri hariç)
- İngilizce içerik üretme (terim karşılıkları hariç)
- Mevcut dosyaların formatını bozmadan düzenleme yapma
- Görsel dosyalarını ana klasöre koyma (her zaman `-images/` alt klasörü kullan)
- Kaynak/hazırlayan bilgisi olmadan not oluşturma
