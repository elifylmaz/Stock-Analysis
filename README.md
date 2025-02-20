
# Hisse Senetlerinin Sektörel Benzerlik Analizi ve Sınıflandırma Modeli Geliştirilmesi

**Milli Teknoloji Hamlesi** kapsamında düzenlenen **Yapay Zeka Uzmanlık Programı** dahilinde, **Veri Yoğun Uygulamaları** dersi kapsamında **Dr. İsmail Güzel** mentörlüğünde geliştirilmiştir.

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

## 📈 Analiz ve Görselleştirmeler
### Real Estate Sektör Benzerlik Analizi
| Hisse Senedi | Gerçek Sektör | En Yüksek Benzerlik | Olasılık (%) |
|--------------|---------------|----------------------|-------------|
| DLR          | Gayrimenkul   | Teknoloji            | 50.43%      |
| SUI          | Gayrimenkul   | Finans               | 43.26%      |

---

