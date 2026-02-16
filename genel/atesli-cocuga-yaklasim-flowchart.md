# ATEŞLİ ÇOCUĞA YAKLAŞIM - ALGOR İTMALAR

**Bölüm:** Genel Pediatri
**Format:** Mermaid Flowcharts

---

## İÇİNDEKİLER

1. [Tanımlar: Ateş vs Hipertermi](#tanımlar-ateş-vs-hipertermi)
2. [Ateş Ölçüm Yöntemleri](#ateş-ölçüm-yöntemleri)
3. [Ana Karar Ağacı](#ana-karar-ağacı)
4. [Yenidoğan (0-28 Gün) Algoritması](#yenidoğan-0-28-gün-algoritması)
5. [29-90 Gün Algoritması](#29-90-gün-algoritması)
6. [Düşük Risk Kriterleri (Boston/Philadelphia/Pittsburgh/Rochester)](#düşük-risk-kriterleri)
7. [3-36 Ay Algoritması](#3-36-ay-algoritması)
8. [İBE Risk Faktörleri](#ibe-risk-faktörleri)
9. [Antipiretik Tedavi](#antipiretik-tedavi)
10. [Normal Vital Bulgular](#normal-vital-bulgular)

---

## TANIMLAR: ATEŞ VS HİPERTERMİ

```mermaid
flowchart TD
    Start([Yükselmiş Vücut<br/>Sıcaklığı]) --> Type{Hipotalamik<br/>Set Noktası?}

    Type -->|Yükselmiş| Fever[ATEŞ<br/>Fever]
    Type -->|Normal| Hyper[HİPERTERMİ<br/>Hyperthermia]

    Fever --> F1[MSS tarafından<br/>düzenlenen]
    Fever --> F2[Biyolojik yanıtın<br/>parçası]
    Fever --> F3[Etkenler:<br/>Enfeksiyon<br/>İnflamasyon<br/>Malignite<br/>İlaç]

    F1 --> FTx[Tedavi:<br/>Antipiretik<br/>Altta yatan<br/>nedenin tedavisi]
    F2 --> FTx
    F3 --> FTx

    Hyper --> H1[Termoregülasyon<br/>bozukluğu]
    Hyper --> H2[Isı üretimi > Kaybı]
    Hyper --> H3[Etkenler:<br/>Isı çarpması<br/>Aşırı egzersiz<br/>Malign hipertermi]

    H1 --> HTx[Tedavi:<br/>Soğutma<br/>Antipiretik<br/>ETKİSİZ!]
    H2 --> HTx
    H3 --> HTx

    style Fever fill:#e17055
    style Hyper fill:#fdcb6e
    style FTx fill:#00b894
    style HTx fill:#0984e3
```

---

## ATEŞ ÖLÇÜM YÖNTEMLERİ

```mermaid
flowchart TD
    Start([Ateş Ölçümü]) --> Age{Yaş?}

    Age -->|<4 hafta| Baby[REKTAL<br/>veya AKSİLLER]
    Age -->|4 hafta-4 yaş| Young[AKSİLLER<br/>TİMPANİK<br/>REKTAL]
    Age -->|≥4 yaş| Older[ORAL<br/>AKSİLLER<br/>TİMPANİK]

    Baby --> B1[REKTAL:<br/>Referans Standart<br/><3 ay için<br/>≥38.0°C = Ateş]
    Baby --> B2[AKSİLLER:<br/>NICE önerisi<br/><4 hafta için<br/>≥37.4°C = Ateş]

    Young --> Y1[AKSİLLER:<br/>Kolay, Güvenli<br/>Rektalden düşük<br/>≥37.4°C = Ateş]
    Young --> Y2[TİMPANİK:<br/>Hızlı, Kolay<br/>Serümen etkiler<br/>≥37.6°C = Ateş]
    Young --> Y3[REKTAL:<br/>En doğru<br/>İnvaziv<br/>≥38.0°C = Ateş]

    Older --> O1[ORAL:<br/>İşbirliği gerekir<br/>Rektalden 0.6°C düşük<br/>≥37.4°C = Ateş]
    Older --> O2[AKSİLLER/TİMPANİK:<br/>Alternatif]

    B1 --> Avoid
    B2 --> Avoid
    Y1 --> Avoid
    Y2 --> Avoid
    Y3 --> Avoid
    O1 --> Avoid
    O2 --> Avoid

    Avoid[❌ ÖNERİLMEYEN] --> A1[Alın:<br/>Değişken<br/>Klinik karar için<br/>KULLANMA]
    Avoid --> A2[Akıllı Telefon:<br/>Kanıt YOK<br/>ÖNERİLMEZ]

    style B1 fill:#0984e3
    style O1 fill:#00b894
    style Avoid fill:#d63031
```

---

## ANA KARAR AĞACI

```mermaid
flowchart TD
    Start([ATEŞLİ ÇOCUK]) --> Sick{HASTA GÖRÜNÜM?<br/>Letarji/Huzursuz/<br/>Hipotonik/<br/>Dolaşım Bozuk/<br/>Nöbet/Peteşi}

    Sick -->|EVET<br/>Yaştan Bağımsız| Emergency[🚨 ACİL!<br/>Sepsis Yüksek Risk<br/>HSV riski 0-6 hafta]

    Emergency --> E1[Stabilizasyon<br/>ABC]
    E1 --> E2[Hospitalize]
    E2 --> E3[Sepsis Taraması<br/>Ampirik Antibiyotik]

    Sick -->|HAYIR<br/>İyi Görünümlü| Age{Yaş?}

    Age -->|0-28 gün| NB[YENİDOĞAN<br/>En Yüksek Risk]
    Age -->|29-90 gün| IF[SÜT ÇOCUĞU<br/>Orta Risk]
    Age -->|3-36 ay| TD[KÜÇÜK ÇOCUK<br/>Düşük-Orta Risk]
    Age -->|>36 ay| OL[BÜYÜK ÇOCUK<br/>Fokal Enfeksiyon Ara<br/>Genellikle Düşük Risk]

    NB --> NBAlgo[📋 Yenidoğan<br/>Algoritması]
    IF --> IFAlgo[📋 29-90 Gün<br/>Algoritması]
    TD --> TDAlgo[📋 3-36 Ay<br/>Algoritması]

    style Emergency fill:#d63031
    style NB fill:#ff6b6b
    style IF fill:#ffd93d
    style TD fill:#6bcf7f
    style OL fill:#95e1d3
```

---

## YENİDOĞAN (0-28 GÜN) ALGORİTMASI

```mermaid
flowchart TD
    Start([YENİDOĞAN 0-28 gün<br/>ATEŞ]) --> Always[🏥 MUTLAKA<br/>HASTANEYEYATIRİR]

    Always --> Tests[📋 TAM SEPSİS TARAMASI<br/>Hızlı Değerlendirme]

    Tests --> T1[CBC + Periferik Yayma]
    Tests --> T2[Kan Kültürü]
    Tests --> T3[İdrar Analizi + Kültür<br/>Sonda/Suprapubik]
    Tests --> T4[Lomber Ponksiyon<br/>BOS Analizi]
    Tests --> T5[AC Grafisi<br/>Solunum bulguları varsa]
    Tests --> T6[Gaita Kültürü<br/>İshal varsa]

    T1 --> Abx
    T2 --> Abx
    T3 --> Abx
    T4 --> Abx
    T5 --> Abx
    T6 --> Abx

    Abx[💊 AMPİRİK ANTİBİYOTİK<br/>İV<br/>HEMEN BAŞLA] --> AbxChoice{Antibiyotik?}

    AbxChoice --> A1[Ampisilin +<br/>Gentamisin]
    AbxChoice --> A2[Ampisilin +<br/>Sefotaksim]

    A1 --> HSV{0-6 HAFTA?<br/>HSV Riski}
    A2 --> HSV

    HSV -->|EVET| Acy[+ ASİKLOVİR<br/>BOS HSV PCR<br/>Sonucu bekle]
    HSV -->|HAYIR| Monitor

    Acy --> Monitor[Yoğun İzlem<br/>Monitorizasyon]

    Monitor --> Culture{Kültür<br/>Sonuçları<br/>48-72 saat}

    Culture -->|POZİTİF<br/>Bakteriyemi/<br/>Menenjit/İYE| Pos[Hedefe Yönelik<br/>Antibiyotik<br/>Tam Süre Tedavi<br/>10-14 gün]

    Culture -->|NEGATİF<br/>Klinik İyi| Neg{Klinik Durum?}

    Neg -->|İyi| Stop[Antibiyotik<br/>Kesmeyi Düşün<br/>48-72 saat sonra]
    Neg -->|Kötü| Continue[Tedaviye Devam<br/>Tam değerlendirme]

    Pos --> F/U[Takip<br/>Komplikasyon<br/>İzlemi]
    Stop --> F/U
    Continue --> F/U

    style Start fill:#ff6b6b
    style Always fill:#d63031
    style Abx fill:#6c5ce7
    style HSV fill:#fd79a8
    style Acy fill:#e17055
```

---

## 29-90 GÜN ALGORİTMASI

```mermaid
flowchart TD
    Start([29-90 GÜN<br/>İYİ GÖRÜNÜMLÜ<br/>ATEŞ]) --> Labs[📊 LABORATUVAR<br/>TESTLERİ]

    Labs --> L1[CBC]
    Labs --> L2[PCT veya CRP]
    Labs --> L3[ANC]
    Labs --> L4[İdrar Analizi<br/>+ Kültür]

    L1 --> Risk
    L2 --> Risk
    L3 --> Risk
    L4 --> Risk

    Risk{İBE Belirteçleri?<br/>PCT > 0.5 ng/mL<br/>CRP ≥ 20 mg/L<br/>ANC > 4000 veya >5200} -->|YÜKSEK| HighRisk[🔴 YÜKSEK RİSK<br/>İBE Olasılığı Yüksek]

    Risk -->|NORMAL<br/>Tüm Belirteçler<br/>Normal| LowCheck[Düşük Risk<br/>Kriterleri<br/>Değerlendir]

    HighRisk --> HR1[🏥 Hospitalize]
    HR1 --> HR2[Tam Sepsis Taraması<br/>Kan, İdrar, BOS]
    HR2 --> HR3[💊 Ampirik<br/>Antibiyotik<br/>Ampisilin + Gentamisin<br/>veya Seftriakson]

    LowCheck --> Criteria{HANGİ KRİTER?}

    Criteria --> Boston[BOSTON]
    Criteria --> Philly[PHILADELPHIA]
    Criteria --> Pitt[PITTSBURGH]
    Criteria --> Roch[ROCHESTER]

    Boston --> BCheck{Kriterler<br/>Karşılanıyor?}
    Philly --> PCheck{Kriterler<br/>Karşılanıyor?}
    Pitt --> PiCheck{Kriterler<br/>Karşılanıyor?}
    Roch --> RCheck{Kriterler<br/>Karşılanıyor?}

    BCheck -->|EVET| LowRisk
    PCheck -->|EVET| LowRisk
    PiCheck -->|EVET| LowRisk
    RCheck -->|EVET| LowRisk

    BCheck -->|HAYIR| NotLow
    PCheck -->|HAYIR| NotLow
    PiCheck -->|HAYIR| NotLow
    RCheck -->|HAYIR| NotLow

    LowRisk[✅ DÜŞÜK RİSK] --> Management{Yönetim?}

    Management -->|Seçenek 1| Out[Ayaktan İzlem<br/>24 saat içinde<br/>Tekrar Değerlendirme<br/>Güvenilir Takip]

    Management -->|Seçenek 2| Obs[Hastane Gözlemi<br/>24-48 saat<br/>Kültür Sonuçları<br/>Bekle]

    Out --> Edu[⚠️ AİLE EĞİTİMİ<br/>Ateş devam ederse<br/>Kötüleşme<br/>Yeni semptom<br/>HEMEN başvur]

    NotLow[❌ Düşük Risk DEĞİL] --> NL1[Hospitalize +<br/>Antibiyotik<br/>Düşün]

    style HighRisk fill:#d63031
    style LowRisk fill:#00b894
    style NotLow fill:#e17055
```

---

## DÜŞÜK RİSK KRİTERLERİ

### BOSTON KRİTERLERİ

```mermaid
flowchart TD
    Start([BOSTON]) --> C1{Genel Durum +<br/>Aktivite İyi?}
    C1 -->|EVET| C2{FM Normal?}
    C1 -->|HAYIR| Fail

    C2 -->|EVET| C3[CBC:<br/>BKH < 20,000/mm³]
    C2 -->|HAYIR| Fail

    C3 --> C4[İdrar:<br/>Lökosit Esteraz<br/>Negatif]

    C4 --> C5[BOS:<br/>Lökosit < 10x10⁶/L]

    C5 --> Pass[✅ DÜŞÜK RİSK<br/>Boston Kriterleri<br/>Karşılandı]

    Fail[❌ DÜŞÜK RİSK DEĞİL]

    style Pass fill:#00b894
    style Fail fill:#d63031
```

### PHILADELPHIA PROTOKOLÜ

```mermaid
flowchart TD
    Start([PHILADELPHIA]) --> C1{Genel Durum +<br/>Aktivite İyi?}
    C1 -->|EVET| C2{FM Normal?}
    C1 -->|HAYIR| Fail

    C2 -->|EVET| C3[CBC:<br/>BKH < 15,000/mm³<br/>İmmatür/Total<br/>Nötrofil < 0.2]
    C2 -->|HAYIR| Fail

    C3 --> C4[İdrar:<br/>BKH < 10/hpf<br/>Gram Boyama (-)]

    C4 --> C5[BOS:<br/>BKH < 8/mm³<br/>Gram Boyama (-)]

    C5 --> C6[AC Grafi:<br/>İnfiltrasyon (-)]

    C6 --> C7[Gaita:<br/>Eritrosit (-)<br/>Bol Lökosit (-)<br/>İshalde]

    C7 --> Pass[✅ DÜŞÜK RİSK<br/>Philadelphia<br/>Karşılandı]

    Fail[❌ DÜŞÜK RİSK DEĞİL]

    style Pass fill:#00b894
    style Fail fill:#d63031
```

### PITTSBURGH REHBERİ

```mermaid
flowchart TD
    Start([PITTSBURGH]) --> C1{Genel Durum +<br/>Aktivite İyi?}
    C1 -->|EVET| C2{FM Normal?}
    C1 -->|HAYIR| Fail

    C2 -->|EVET| C3[CBC:<br/>BKH 5,000-15,000/mm³<br/>Çomak < 1500/mm³]
    C2 -->|HAYIR| Fail

    C3 --> C4[İdrar:<br/>BKH < 9/mm³<br/>Gram Boyama (-)]

    C4 --> C5[BOS:<br/>BKH < 5/mm³<br/>Gram Boyama (-)<br/>Travmatize LP:<br/>BKH/KKH < 1:500]

    C5 --> C6[AC Grafi:<br/>İnfiltrasyon (-)]

    C6 --> C7[Gaita:<br/>BKH < 5/hpf<br/>İshalde]

    C7 --> Pass[✅ DÜŞÜK RİSK<br/>Pittsburgh<br/>Karşılandı]

    Fail[❌ DÜŞÜK RİSK DEĞİL]

    style Pass fill:#00b894
    style Fail fill:#d63031
```

### ROCHESTER KRİTERLERİ

```mermaid
flowchart TD
    Start([ROCHESTER]) --> C1{Genel Durum +<br/>Aktivite İyi?}
    C1 -->|EVET| C2{FM Normal?}
    C1 -->|HAYIR| Fail

    C2 -->|EVET| C3{Önceden<br/>Hospitalizasyon<br/>YOK?}
    C2 -->|HAYIR| Fail

    C3 -->|EVET| C4{Kronik Hastalık<br/>YOK?}
    C3 -->|HAYIR| Fail

    C4 -->|EVET| C5[CBC:<br/>BKH 5,000-15,000/mm³<br/>Çomak < 1500/mm³]
    C4 -->|HAYIR| Fail

    C5 --> C6[İdrar:<br/>BKH < 10/hpf<br/>40x büyütme]

    C6 --> C7[Gaita:<br/>BKH < 5/hpf<br/>İshalde]

    C7 --> Pass[✅ DÜŞÜK RİSK<br/>Rochester<br/>Karşılandı]

    Fail[❌ DÜŞÜK RİSK DEĞİL]

    style Pass fill:#00b894
    style Fail fill:#d63031
```

---

## 3-36 AY ALGORİTMASI

```mermaid
flowchart TD
    Start([3-36 AY<br/>İYİ GÖRÜNÜMLÜ<br/>ATEŞ]) --> Temp{Ateş<br/>Derecesi?}

    Temp -->|< 39°C<br/>DÜŞÜK| Low[🌡️ DÜŞÜK ATEŞ]
    Temp -->|≥ 39°C<br/>YÜKSEK| High[🌡️ YÜKSEK ATEŞ<br/>İBE Riski ↑]

    Low --> LowMgmt[❌ AB Endikasyonu YOK<br/>❌ İleri Tetkik YOK]

    LowMgmt --> LowAdv[⚠️ AİLEYİ UYAR]

    LowAdv --> W1[Ateş > 48 saat]
    LowAdv --> W2[Kötüleşme]
    LowAdv --> W3[Yeni semptom]

    W1 --> Return[Tekrar Başvuru]
    W2 --> Return
    W3 --> Return

    High --> Vacc{Aşılama<br/>Durumu?}

    Vacc -->|TAM AŞILI<br/>Yaşına Uygun| Full[TAM AŞILI<br/>İBE Riski Düşük]
    Vacc -->|AŞISIZ/<br/>EKSİK AŞILI| Incomplete[AŞISIZ/EKSİK<br/>İBE Riski YÜKSEK]

    Full --> RiskFull{Risk Faktörleri?}

    RiskFull --> RF1[İYE Risk:<br/>< 24 ay Kız<br/>< 12 ay Erkek sünnetsiz<br/>< 6 ay Tüm erkek<br/>Önceden İYE<br/>Anomali]

    RiskFull --> RF2[İBE Risk:<br/>WBC > 15,000<br/>ANC > 4000-5200<br/>PCT > 0.5<br/>CRP > 20<br/>İdrarda ≥10 lökosit]

    RF1 --> Eval
    RF2 --> Eval

    Eval{Risk Var?} -->|EVET| TestFull[📋 İLERİ TETKİKLER<br/>İdrar Kültürü<br/>Kan Testleri]
    Eval -->|HAYIR| NoRisk[✅ Risk YOK<br/>Fokal Enfeksiyon<br/>Ara<br/>Semptomatik]

    TestFull --> Result{Sonuç?}

    Result -->|POZİTİF<br/>İYE/Bakteriyemi| Tx[💊 Hedefe Yönelik<br/>Antibiyotik<br/>İYE: Oral/IV<br/>Bakteriyemi: Hospitalize]
    Result -->|NEGATİF| F/U1[Takip<br/>48-72 saat]

    Incomplete --> IncRisk[🔴 YÜKSEK RİSK<br/>Kapsamlı Değerlendirme]

    IncRisk --> IncTest[📋 Dikkatli Test<br/>CBC, PCT/CRP<br/>İdrar Kültürü<br/>Düşün]

    IncTest --> IncResult{Bulgular?}

    IncResult -->|ANORMAL| IncTx[Hospitalize +<br/>Antibiyotik]
    IncResult -->|NORMAL| IncF/U[Yakın Takip<br/>24-48 saat]

    style Low fill:#00b894
    style High fill:#e17055
    style Full fill:#0984e3
    style Incomplete fill:#fdcb6e
    style NoRisk fill:#00b894
    style IncRisk fill:#d63031
```

---

## İBE RİSK FAKTÖRLERİ

```mermaid
flowchart TD
    Start([İBE RİSK<br/>DEĞERLENDİRMESİ<br/>3-36 ay, ≥39°C]) --> Types[Risk Faktörleri<br/>2 Kategori]

    Types --> Lab[LABORATUVAR<br/>Risk Faktörleri]
    Types --> Clin[KLİNİK<br/>Risk Faktörleri]

    Lab --> L1{WBC<br/>> 15,000/mm³?}
    Lab --> L2{ANC<br/>> 4000 veya >5200?}
    Lab --> L3{PCT<br/>> 0.5 ng/mL?}
    Lab --> L4{CRP<br/>≥ 20 mg/L?}
    Lab --> L5{İdrarda<br/>≥10 lökosit?}

    L1 -->|EVET| LabPos[🔴 LAB RİSK<br/>YÜKSEK]
    L2 -->|EVET| LabPos
    L3 -->|EVET| LabPos
    L4 -->|EVET| LabPos
    L5 -->|EVET| LabPos

    L1 -->|HAYIR| LabCheck
    L2 -->|HAYIR| LabCheck
    L3 -->|HAYIR| LabCheck
    L4 -->|HAYIR| LabCheck
    L5 -->|HAYIR| LabCheck

    LabCheck{Tüm<br/>Normal?} -->|EVET| LabNeg[✅ LAB RİSK<br/>DÜŞÜK]

    Clin --> C1{İYE RİSK?}

    C1 --> C1a[< 24 ay Kız]
    C1 --> C1b[< 12 ay Erkek sünnetsiz]
    C1 --> C1c[< 6 ay Tüm erkek]
    C1 --> C1d[Önceden İYE]
    C1 --> C1e[Üriner Anomali]

    C1a -->|EVET| ClinPos[🔴 İYE RİSKİ<br/>YÜKSEK]
    C1b -->|EVET| ClinPos
    C1c -->|EVET| ClinPos
    C1d -->|EVET| ClinPos
    C1e -->|EVET| ClinPos

    C1a -->|HAYIR| ClinCheck
    C1b -->|HAYIR| ClinCheck
    C1c -->|HAYIR| ClinCheck
    C1d -->|HAYIR| ClinCheck
    C1e -->|HAYIR| ClinCheck

    ClinCheck{İYE<br/>Riski?} -->|HAYIR| ClinNeg[✅ KLİNİK RİSK<br/>DÜŞÜK]

    LabPos --> Action[📋 İLERİ TESTİ<br/>GEREKTİRİR]
    ClinPos --> Action

    Action --> Tests[İdrar Kültürü MUTLAKA<br/>Kan Kültürü Düşün<br/>Diğer Testler]

    Tests --> TxDecision{Test<br/>Sonuçları?}

    TxDecision -->|POZİTİF| Treat[💊 Antibiyotik<br/>Tedavisi]
    TxDecision -->|NEGATİF| Monitor[Takip<br/>48-72 saat]

    Treat --> T1[İYE:<br/>Oral/IV<br/>7-10 gün]
    Treat --> T2[Bakteriyemi:<br/>Hospitalize<br/>IV Antibiyotik]

    LabNeg --> LowRisk[RİSK DÜŞÜK]
    ClinNeg --> LowRisk

    LowRisk --> Focal[Fokal<br/>Enfeksiyon Ara]

    Focal --> F1[Otitis Media?]
    Focal --> F2[Farenjit?]
    Focal --> F3[Pnömoni?]
    Focal --> F4[Sinüzit?]

    F1 -->|VAR| FocalTx[Hedefe Yönelik<br/>Tedavi]
    F2 -->|VAR| FocalTx
    F3 -->|VAR| FocalTx
    F4 -->|VAR| FocalTx

    F1 -->|YOK| Viral
    F2 -->|YOK| Viral
    F3 -->|YOK| Viral
    F4 -->|YOK| Viral

    Viral[Muhtemelen Viral] --> Symp[Semptomatik<br/>Tedavi]

    style LabPos fill:#d63031
    style ClinPos fill:#d63031
    style LabNeg fill:#00b894
    style ClinNeg fill:#00b894
```

---

## ANTİPİRETİK TEDAVİ

```mermaid
flowchart TD
    Start([ATEŞ<br/>Antipiretik<br/>Gerekli mi?]) --> Indication{ENDİKASYON?}

    Indication -->|VAR| Indic
    Indication -->|YOK| NoNeed[Sağlıklı Çocuk<br/>Konforu İyi<br/>❌ Gerekmeyebilir]

    Indic[ANTİPİRETİK<br/>ENDİKASYONLARI] --> I1[Şok]
    Indic --> I2[Kardiyopulmoner<br/>Hastalık]
    Indic --> I3[Nörolojik Hastalık]
    Indic --> I4[Dehidratasyon/<br/>Elektrolit Dengesizliği]
    Indic --> I5[Yüksek Ateş ≥40°C]
    Indic --> I6[Ciddi Kafa Travması]
    Indic --> I7[Kardiyak Arrest Sonrası]
    Indic --> I8[Çocuğun Konforu Bozuk]

    I1 --> Give
    I2 --> Give
    I3 --> Give
    I4 --> Give
    I5 --> Give
    I6 --> Give
    I7 --> Give
    I8 --> Give

    Give[✅ ANTİPİRETİK<br/>VERİLMELİ] --> Choice{İLK<br/>TERCİH?}

    Choice --> Para[PARASETAMOL<br/>İlk Tercih]
    Choice --> Ibu[İBUPROFEN<br/>Alternatif]

    Para --> ParaDose[10-15 mg/kg/doz<br/>Her 4-6 saat<br/>Maks: 75 mg/kg/gün<br/>veya 4 g/gün]

    Ibu --> IbuAge{Yaş?}

    IbuAge -->|< 6 ay| IbuNo[❌ Genellikle<br/>ÖNERİLMEZ<br/>Renal İmmatürite<br/>Dehidratasyon Riski]

    IbuAge -->|≥ 6 ay| IbuDose[5-10 mg/kg/doz<br/>Her 6-8 saat<br/>Maks: 40 mg/kg/gün<br/>veya 1200 mg/gün]

    ParaDose --> Compare
    IbuDose --> Compare

    Compare[KARŞILAŞTIRMA] --> Comp1[Etkinlik:<br/>İbuprofen biraz<br/>daha etkili]
    Compare --> Comp2[Süre:<br/>İbuprofen 6-8 saat<br/>Parasetamol 4-6 saat]
    Compare --> Comp3[Anti-inflamatuvar:<br/>İbuprofen VAR<br/>Parasetamol YOK]

    Comp1 --> NoResponse
    Comp2 --> NoResponse
    Comp3 --> NoResponse

    NoResponse[3-4 SAAT SONRA<br/>YANIT YOK?] --> Switch{İlaç<br/>Değişimi}

    Switch --> S1[Parasetamol<br/>→ İbuprofen<br/>✅ GEÇİLEBİLİR]

    Switch --> S2[İbuprofen<br/>→ Parasetamol<br/>✅ GEÇİLEBİLİR]

    S1 --> Warning
    S2 --> Warning

    Warning[⚠️ DİKKAT] --> W1[❌ KOMBİNASYON<br/>ÖNERİLMEZ<br/>Doz Karışıklığı<br/>Toksisite Riski]

    W1 --> W2[❌ ASPİRİN<br/>KONTRENDİKE<br/>Reye Sendromu<br/>Ensefalopati +<br/>Karaciğer Yetmezliği]

    style Para fill:#0984e3
    style Ibu fill:#6c5ce7
    style IbuNo fill:#d63031
    style W1 fill:#d63031
    style W2 fill:#d63031
```

---

## NORMAL VİTAL BULGULAR

```mermaid
flowchart TD
    Start([Vital Bulgular<br/>Değerlendirmesi]) --> Age{Yaş?}

    Age -->|<1 ay| NB[YENİDOĞAN]
    Age -->|1-12 ay| Inf[BEBEK]
    Age -->|1-3 yaş| Tod[KÜÇÜK ÇOCUK]
    Age -->|3-6 yaş| Pre[OKUL ÖNCESİ]
    Age -->|6-12 yaş| Sch[OKUL ÇAĞI]

    NB --> N1[Kalp Hızı:<br/>100-160 /dk]
    NB --> N2[Solunum:<br/>30-60 /dk]
    NB --> N3[Sistolik KB:<br/>> 60 mmHg]

    Inf --> I1[Kalp Hızı:<br/>100-150 /dk]
    Inf --> I2[Solunum:<br/>25-40 /dk]
    Inf --> I3[Sistolik KB:<br/>> 70 mmHg]

    Tod --> T1[Kalp Hızı:<br/>90-140 /dk]
    Tod --> T2[Solunum:<br/>20-30 /dk]
    Tod --> T3[Sistolik KB:<br/>> 70 + 2×yaş<br/>mmHg]

    Pre --> P1[Kalp Hızı:<br/>80-120 /dk]
    Pre --> P2[Solunum:<br/>20-25 /dk]
    Pre --> P3[Sistolik KB:<br/>> 70 + 2×yaş<br/>mmHg]

    Sch --> S1[Kalp Hızı:<br/>70-110 /dk]
    Sch --> S2[Solunum:<br/>15-20 /dk]
    Sch --> S3[Sistolik KB:<br/>> 70 + 2×yaş<br/>mmHg]

    N1 --> Fever
    N2 --> Fever
    N3 --> Fever
    I1 --> Fever
    I2 --> Fever
    I3 --> Fever
    T1 --> Fever
    T2 --> Fever
    T3 --> Fever
    P1 --> Fever
    P2 --> Fever
    P3 --> Fever
    S1 --> Fever
    S2 --> Fever
    S3 --> Fever

    Fever[ATEŞTE<br/>BEKLENEBİLECEK<br/>ARTIŞ] --> F1[Kalp Hızı:<br/>+10-15 atım/dk<br/>Her 1°C için]

    Fever --> F2[Solunum Hızı:<br/>+3-5 solunum/dk<br/>Her 1°C için]

    F1 --> Check{Beklenenden<br/>FAZLA Artış?}
    F2 --> Check

    Check -->|EVET| Red[🚨 KIRMIZI BAYRAK<br/>Ciddi Enfeksiyon<br/>Sepsis Şüphesi]

    Red --> RF1[Taşikardi<br/>Çok Yüksek]
    Red --> RF2[Takipne<br/>Belirgin Artış]
    Red --> RF3[Hipotansiyon<br/>Yaşa Göre Düşük]
    Red --> RF4[SpO₂ < 92%<br/>Hipoksi]

    RF1 --> Action[ACİL<br/>DEĞERLENDİRME<br/>GEREKTİRİR]
    RF2 --> Action
    RF3 --> Action
    RF4 --> Action

    Check -->|HAYIR| Normal[Ateşe Bağlı<br/>Normal Artış<br/>Endişe Yok]

    style Red fill:#d63031
    style Action fill:#d63031
    style Normal fill:#00b894
```

---

## NEREDE YAYINLAYACAĞIZ?

### Platform Uyumluluğu

```mermaid
flowchart LR
    File([atesli-cocuga-yaklasim-<br/>flowchart.md]) --> Platforms[Yayınlanabilecek<br/>Platformlar]

    Platforms --> GitHub[✅ GitHub<br/>Native Mermaid<br/>Otomatik Render]

    Platforms --> GitBook[✅ GitBook<br/>Mermaid Plugin<br/>gitbook.yaml]

    Platforms --> VSCode[✅ VS Code<br/>Mermaid Preview<br/>Uzantısı]

    Platforms --> Notion[✅ Notion<br/>Mermaid Blokları<br/>Destekler]

    Platforms --> Web[✅ Web<br/>Mermaid.js<br/>CDN]

    GitHub --> Link1[README.md'ye Link]
    GitBook --> Link1
    VSCode --> Link1
    Notion --> Link1
    Web --> Link1

    Link1 --> Link2[SUMMARY.md'ye<br/>Nested Link]

    Link2 --> Link3[Ana Ders Notunda<br/>Referans]

    style File fill:#0984e3
    style GitHub fill:#00b894
    style GitBook fill:#00b894
```

### Önerilen Kullanım

1. **Ana ders notunda bağlantı:**
```markdown
📊 **Görsel Algoritmalar:** [Flowcharts](atesli-cocuga-yaklasim-flowchart.md)
```

2. **SUMMARY.md'de nested:**
```markdown
* [Ateşli Çocuğa Yaklaşım](genel/atesli-cocuga-yaklasim.md)
  * [📊 Algoritmalar](genel/atesli-cocuga-yaklasim-flowchart.md)
```

3. **README.md'ye:**
```markdown
## 📊 Görsel Algoritmalar
- [Ateşli Çocuğa Yaklaşım Flowcharts](genel/atesli-cocuga-yaklasim-flowchart.md)
```

---

**Kaynak:** Pediatri Ders Notları
**Format:** Mermaid Flowcharts
**Tarih:** 2024
