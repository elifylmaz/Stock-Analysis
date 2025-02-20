```markdown
# Hisse Senetlerinin Sektörel Benzerlik Analizi ve Sınıflandırma Modeli Geliştirilmesi

![Proje Şeması](https://via.placeholder.com/800x400?text=Sector+Similarity+Analysis+Flow) <!-- Proje şeması eklenebilir -->

## 📌 Proje Amacı
Bu proje, hisse senetlerinin zaman serisi davranışlarını analiz ederek sektörel benzerliklerini tespit etmeyi ve makine öğrenmesi modelleriyle sınıflandırmayı hedefler. Finans, Sağlık, Teknoloji ve Gayrimenkul (Real Estate) sektörlerine odaklanarak yatırım stratejilerine veriye dayalı destek sağlar.

---

## 📊 Veri Toplama ve İşleme
### Veri Kaynakları & Yöntemler
- **Araçlar:** `yfinance`, `investpy`, `quandl`, `BeautifulSoup` (Web Scraping)
- **Toplanan Sektörler:** 
  - Finans, Sağlık, Teknoloji (Temel sektörler)
  - Gayrimenkul (Real Estate) (Ek analiz için)
- **Zaman Aralığı:** 1 Ocak 2005'ten itibaren tarihsel veriler
- **Veri Yapısı Örneği:
  ```csv
  Symbol,Company Name,Market Cap,% Change,Volume,Revenue
  AAPL,Apple Inc.,2.5T,+1.2%,100M,365B
  ```

### Veri Ön İşleme Adımları
1. **Eksik Veri Yönetimi:** 
   - `-` değerlerin `NaN` ile değiştirilmesi
   - `dropna()` ile eksik satırların temizlenmesi
2. **Zaman Serisi Dönüşümleri:**
   - Günlük kapanış fiyatlarının aylık getirilere dönüştürülmesi
   - `pct_change()` ile aylık getiri hesaplama
3. **Özellik Mühendisliği:**
   - `tsfresh` kütüphanesi ile otomatik özellik çıkarımı (varyans, standart sapma, otokorelasyon)
   - PCA ile boyut indirgeme ve özellik seçimi

---

## 🛠️ Model Geliştirme ve Performans
### Kullanılan Modeller ve Sonuçlar
| Model               | Accuracy | F1-Score | ROC-AUC | Eğitim Süresi (s) |
|---------------------|----------|----------|---------|-------------------|
| **CatBoost**        | 77.67%   | 0.776    | 0.9426  | 147.09            |
| Random Forest       | 73.83%   | 0.740    | 0.9225  | 227.38            |
| XGBoost             | 69.17%   | 0.692    | 0.9101  | -                 |
| Gradient Boosting   | 65.30%   | 0.656    | 0.9006  | 878.09            |

### Optimizasyon ve Doğrulama
- **Hiperparametre Ayarı:** `GridSearchCV` ile en iyi parametre kombinasyonlarının belirlenmesi
- **Sınıf Dengesizliği Çözümü:** SMOTE ile her sınıftan 1000 örnek oluşturma
- **Çapraz Doğrulama:** 10 katmanlı Stratified K-Fold

---

## 🚀 Kurulum ve Çalıştırma
### Gereksinimler
```bash
pip install yfinance pandas numpy scipy tsfresh scikit-learn catboost xgboost imbalanced-learn
```

### Adım Adım Çalıştırma
1. **Veri Toplama:**
   ```python
   python src/data_collection.py  # Sektör verilerini çeker ve CSV'ye kaydeder
   ```
2. **Özellik Çıkarımı:**
   ```python
   python src/feature_extraction.py  # Zaman serisi özelliklerini çıkarır
   ```
3. **Model Eğitimi:**
   ```python
   python src/train_model.py --model CatBoost  # En iyi performanslı model
   ```

---

## 📈 Analiz ve Görselleştirmeler
### Performans Karşılaştırması
![Model Performans Grafiği](https://via.placeholder.com/600x400?text=Model+Comparison+Metrics)

### Real Estate Sektör Benzerlik Analizi
| Hisse Senedi | Gerçek Sektör | En Yüksek Benzerlik | Olasılık (%) |
|--------------|---------------|----------------------|-------------|
| DLR          | Gayrimenkul   | Teknoloji            | 50.43%      |
| SUI          | Gayrimenkul   | Finans               | 43.26%      |

---

