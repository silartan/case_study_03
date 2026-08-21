#  Tekstil Satış ve Müşteri Analitiği Dashboard Projesi

Bu proje, tekstil sektöründe faaliyet gösteren bir işletmenin satış performansını, müşteri dinamiklerini, ürün karlılığını ve bölgesel pazar stratejilerini uçtan uca analiz etmek amacıyla **Microsoft Power BI** kullanılarak geliştirilmiştir.

---

##  Projenin Amacı ve Kapsamı
Rapor; üst yönetim, satış ekipleri ve ürün yöneticileri için stratejik karar alma süreçlerini destekleyen 4 temel analitik katmandan oluşmaktadır:
* **Yönetim Satış Performans Özeti:** Ciro, hacim, sipariş adedi ve genel satış trendlerinin tek sayfada takibi.
* **Müşteri Segmentasyonu ve Sadakat Analizi:** Müşteri satın alma sıklığı (Seyrek, Düzenli, Sadık), müşteri bazlı ciro katkısı ve konsantrasyon analizi.
* **Ürün Optimizasyon Stratejileri:** Kumaş türleri (Denim / Gabardin), ürün konseptleri ve fiyat segmentleri (Premium, Orta, Düşük) bazında getiri analizi.
* **Bölgesel Satış Hedefi ve Büyüme Stratejileri:** Ülke/bölge bazında ciro büyüklüğü, katma değerli kumaş fiyatlandırması (€/m) ve pazar bazlı ürün tercihleri.

---

##  Dashboard Görselleri

### 1. Yönetim Satış Performans Özeti
![Yönetim Dashboardu](outputs/Yonetim_Dashboardu.png)

### 2. Müşteri Segmentasyonu ve Sadakat Analizi
![Müşteri Segmentasyon Dashboardu](outputs/Musteri_Segmentasyon_Dashboardu.png)

### 3. Ürün Optimizasyon Stratejileri
![Ürün Optimizasyon Dashboardu](outputs/Urun_Optimizasyon_Dashboardu.png)

### 4. Bölgesel Satış Hedefi ve Büyüme Stratejileri
![Bölgesel Satış Dashboardu](outputs/Bolgesel_Satis_Dashboardu.png)

---

##  Veri Modeli, DAX Ölçüleri ve Sütun Hesaplamaları

Projede dinamik KPI takibi, segmentasyon ve karlılık analizi için geliştirilen formüller:

### 1. Temel KPI ve Performans Ölçüleri (Measures)

* **Toplam Ciro (€):**
```dax
Toplam Ciro EUR = SUM('Satış Verileri'[Fatura Tutarı (EUR)])
```

* **Toplam Sipariş Sayısı:**
```dax
Toplam Sipariş = DISTINCTCOUNT('Satış Verileri'[Satış Belge No])
```

* **Ortalama Sipariş Tutarı (€):**
```dax
Ortalama Sipariş Tutarı = DIVIDE([Toplam Ciro EUR], [Toplam Sipariş], 0)
```

* **Birim Başı Ortalama Kumaş Fiyatı (€/m):**
```dax
Birim Başı Ortalama Fiyat = DIVIDE([Toplam Ciro EUR], SUM('Satış Verileri'[Miktar]), 0)
```

* **Müşteri Başına Ortalama Ciro (€):**
```dax
Müşteri Başına Ortalama Ciro = DIVIDE([Toplam Ciro EUR], DISTINCTCOUNT('Satış Verileri'[Müşteri]), 0)
```

---

### 2. Segmentasyon ve İş Mantığı (Calculated Columns)

* **Müşteri Sipariş Sıklığı Segmentasyonu:**
```dax
Müşteri Satın Alma Sıklığı = 
SWITCH(
    TRUE(),
    'Satış Verileri'[Müşteri Toplam Sipariş] >= 200, "Çok Sık (Sadık)",
    'Satış Verileri'[Müşteri Toplam Sipariş] >= 50, "Düzenli",
    'Satış Verileri'[Müşteri Toplam Sipariş] >= 10, "Orta Sıklık",
    "Seyrek / Yeni"
)
```

* **Fiyat Skalası Segmentasyonu:**
```dax
Fiyat Skalası = 
SWITCH(
    TRUE(),
    'Satış Verileri'[Birim Fiyat] >= 5.0, "Premium Segment",
    'Satış Verileri'[Birim Fiyat] >= 3.5, "Orta Segment",
    "Düşük Segment"
)
```

---

##  Klasör Yapısı

```plaintext
case_study_03/
│
├── data/          # Ham veri seti
├── report/        # Power BI (.pbix) çalışma dosyası
├── outputs/       # Dashboard ekran görüntüleri (.png)
└── README.md      # Proje dokümantasyonu
```

---

## 🛠️ Kullanılan Teknolojiler
* **BI & Görselleştirme:** Microsoft Power BI Desktop
* **Modelleme & Hesaplama:** DAX (Data Analysis Expressions), Power Query
* **Veri Yönetimi:** Excel / CSV Data Source
