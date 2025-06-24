# YZM304 Derin Öğrenme – III. Ödev  
## RNN ile Duygu Sınıflandırması


## 1. Giriş

Bu projede metin cümlelerinin duygu içeriklerinin pozitif ya da negatif olarak sınıflandırılması amaçlanmıştır. Bu amaçla iki farklı model geliştirilmiştir: birincisi NumPy ile sıfırdan oluşturulan bir RNN, ikincisi ise PyTorch kütüphanesi kullanılarak inşa edilen modern bir RNN modelidir. Kullanılan veri seti, [vzhou842/rnn-from-scratch](https://github.com/vzhou842/rnn-from-scratch) GitHub deposundaki `sentiment.txt` dosyasıdır.

---

## 2. Yöntem

### 2.1. Scratch RNN (NumPy)
Bu modelde temel RNN hesaplamaları (gizli katman, aktivasyon, softmax vb.) sıfırdan yazılmıştır. Giriş cümleleri önce tokenize edilerek kelime indekslerine çevrilmiştir. Ardından sabit uzunlukta giriş olarak modele verilmiştir.

### 2.2. PyTorch RNN
Bu modelde `nn.RNN` kullanılarak gömülü (embedding) kelime temsilleriyle çalışan bir sınıflayıcı inşa edilmiştir. Eğitim verileri `DataLoader` ile beslenmiş, her epoch sonrası loss ve accuracy değerleri hesaplanmıştır.

---

## 3. Sonuçlar

Aşağıda her iki modelin eğitim başarımı ve karşılaştırmaları yer almaktadır.

### 3.1. Scratch RNN
- Eğitim doğruluğu: %60 civarında
- Basit veri ile sınırlı başarı

### 3.2. PyTorch RNN
- Eğitim doğruluğu: %90+
- Daha sağlam sonuçlar
- GPU desteği ile daha hızlı

---

## 4. Tartışma

NumPy ile sıfırdan yazılan RNN modeli temel mantığın anlaşılması açısından oldukça faydalıdır. Ancak karmaşık veri ve büyük modeller için yetersiz kalır. PyTorch modeli ise hem eğitim süresi hem de doğruluk açısından daha başarılıdır. Embedding, batch işleme ve GPU desteği bu farkı yaratmaktadır.

---

## 5. Referanslar

- Zhou, V. [rnn-from-scratch GitHub](https://github.com/vzhou842/rnn-from-scratch)
- PyTorch Documentation: https://pytorch.org/docs/stable/
- Goodfellow, I. et al. (2016). Deep Learning. MIT Press.
