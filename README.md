# Duygu Sınıflandırması – RNN ile IMDB Veri Kümesi Üzerinde

**Ders:** YZM304 Derin Öğrenme  
**Dönem:** 2024–2025 Bahar Dönemi  
**Ödev:** III. Proje

---

## 1. Giriş

Bu projede, film yorumlarının duygu analizi yapılmıştır. Amaç, verilen bir metnin pozitif mi yoksa negatif mi olduğunu otomatik olarak sınıflandıran bir model geliştirmektir. Metin verilerinin yapısal karmaşıklığı nedeniyle Tekrarlayan Sinir Ağları (RNN) tercih edilmiştir. RNN, sırayla işlenen verilerdeki bağlamı yakalamaya uygundur ve bu proje için sıfırdan yazılan bir RNN modeli ile PyTorch’un hazır RNN modülü kullanılarak iki farklı model geliştirilmiştir.

---

## 2. Yöntem

### Veri Seti

IMDB film yorumları veri seti kullanılmıştır. Veri seti toplam 50000 yorum içermekte olup, eşit sayıda pozitif ve negatif etiket barındırmaktadır. Veri ön işleme aşamasında yorumlar tokenize edilmiş, kelimeler sayısallaştırılmış ve padding uygulanmıştır.

### Model 1: Sıfırdan Yazılan RNN

- Model, temel RNN hücresi mantığı kullanılarak numpy ve PyTorch dışı saf Python ile yazılmıştır.
- Giriş katmanından gizli katmana, oradan çıktı katmanına ağırlıklar rastgele başlatılmıştır.
- İleri geçiş, aktivasyon ve kayıp fonksiyonu el ile kodlanmıştır.
- Eğitimde elde edilen tahminler ve kayıplar izlenmiştir.

### Model 2: PyTorch Hazır RNN Modülü Kullanımı

- PyTorch’un `nn.RNN` sınıfı kullanılmıştır.
- Modelde embedding katmanı, RNN katmanı ve tam bağlı (fully connected) çıkış katmanı yer almaktadır.
- Eğitimde Binary Cross Entropy Loss (BCELoss) ve Adam optimizasyon algoritması tercih edilmiştir.
- Öğrenme hızı 0.0211 olarak belirlenmiş ve 30 epoch boyunca eğitim yapılmıştır.
- Eğitim kodu GPU desteği ile hızlandırılmıştır. 

## 3. Sonuçlar

Her iki modelin test sonuçları aşağıdaki gibidir. Model performansları sınıflandırma raporları ve karmaşıklık matrisleri ile değerlendirilmiştir.

| Model               | Accuracy | Precision (Pozitif) | Recall (Pozitif) | F1-Score (Pozitif) |
|---------------------|----------|---------------------|------------------|--------------------|
| Model 1 (Sıfırdan RNN)  | 0.75     | 0.68                | 0.82             | 0.74               |
| Model 2 (PyTorch RNN)   | 0.87     | 1.00                | 0.70             | 0.83               |

### Karmaşıklık Matrisi (Model 1)

|                   | Negatif Tahmin | Pozitif Tahmin |
|-------------------|----------------|----------------|
| **Negatif**       | 39             | 17             |
| **Pozitif**       | 8              | 36             |

### Karmaşıklık Matrisi (Model 2)

|                   | Negatif Tahmin | Pozitif Tahmin |
|-------------------|----------------|----------------|
| **Negatif**       | 56             | 0              |
| **Pozitif**       | 13             | 31             |

### Eğitim Kayıp Grafiği (Model 2)

_(Buraya eğitim sırasında `train_losses` listesinden matplotlib ile çizilen loss grafiği yerleştirilecek)_

---

## 4. Tartışma

Model 2, PyTorch’un hazır RNN modülünü kullanarak geliştirilmiş ve daha yüksek doğruluk ile genel performans sağlamıştır. Model 1 ise sıfırdan yazılmış temel bir RNN olduğundan eğitim ve tahmin süreçlerinde daha düşük doğruluk ve daha fazla hata oranı görülmüştür.

PyTorch modelinin yüksek precision değeri, pozitif sınıfta hatalı pozitif tahminlerin daha az olduğunu gösterirken; recall değerinin biraz düşük olması, bazı pozitif örneklerin yanlış negatif olarak sınıflandırıldığını göstermektedir. Model 1 ise daha dengeli ancak daha düşük performans göstermektedir.

Gelecek çalışmalarda, LSTM veya GRU gibi daha karmaşık RNN hücreleri ile deneyler yapılabilir. Ayrıca veri artırımı ve hiperparametre optimizasyonu ile performans artırılabilir.

---

## 5. Kaynaklar

- [PyTorch Resmi Dokümantasyon](https://pytorch.org/docs/stable/index.html)  
- [IMDB Dataset on Kaggle](https://www.kaggle.com/datasets/lakshmi25npathi/imdb-dataset-of-50k-movie-reviews)  
- YZM304 Derin Öğrenme Ders Notları  
- [RNN From Scratch Örnek Çalışması](https://github.com/vzhou842/rnn-from-scratch)  

---

**Not:** Proje tüm kodlar tek dosya (main.py) içinde toplanmış olup, çalışma ortamında PyTorch kütüphanesi ve gerekli diğer bağımlılıkların kurulumu sağlanmalıdır. Eğitim sürecinde GPU desteği varsa kullanılması önerilir.
