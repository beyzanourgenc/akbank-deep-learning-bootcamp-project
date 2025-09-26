# akbank-deep-learning-bootcamp-project
Deep Learning image classification project using CNN (Convolutional Neural Networks).  Developed as part of Akbank Deep Learning Bootcamp.
# Akbank Derin Öğrenme Bootcamp Projesi: Görüntü Sınıflandırma

## Projenin Amacı
Bu proje kapsamında, **Convolutional Neural Network (CNN)** mimarisi kullanılarak 6 farklı sınıfa ait doğal görüntülerin sınıflandırılması hedeflenmiştir.  
Amaç, katılımcıların **derin öğrenme** alanında şu konularda deneyim kazanmasıdır:
- Görüntü işleme için veri önişleme ve veri görselleştirme
- CNN mimarisi kurma ve model eğitimi
- Performans değerlendirme metrikleri kullanma
- Modelin hangi bölgelerden etkilendiğini yorumlayabilme (Grad-CAM)
- Hiperparametre optimizasyonu ile model başarımını artırma


## Veri Seti
- Kaynak: [Intel Image Classification Dataset](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)  
- Sınıflar: **Buildings, Forest, Glacier, Mountain, Sea, Street**  
- Dağılım:
  - Eğitim: 11,230 görsel
  - Doğrulama: 2,804 görsel
  - Test: 3,000 görsel

Veriler Kaggle üzerinden otomatik olarak yüklenmiş, yeniden boyutlandırılmış (**150x150**) ve `ImageDataGenerator` ile artırılmıştır (rotation, flip, zoom).

## Yöntem ve Modelleme

### 1. Veri Önişleme
- Görseller normalize edildi (0-1 arası ölçekleme).
- Augmentation ile modelin genelleme kabiliyeti artırıldı.

### 2. Model Mimarisi
Model **Keras** kullanılarak oluşturuldu. Ana bileşenler:
- Conv2D + ReLU (özellik çıkarımı)
- MaxPooling2D (boyut azaltma)
- Dropout (overfitting önleme)
- Dense katmanları + Softmax çıkış

### 3. Eğitim Süreci
- **Optimizer:** Adam
- **Learning rate:** 1e-3 (en başarılı kombinasyonlardan biri)
- **Batch size:** 64
- **Epochs:** 12
- **Callbackler:** EarlyStopping & ReduceLROnPlateau
- GPU hızlandırma (Tesla T4) ile eğitildi

### 4. Değerlendirme
- Accuracy ve Loss eğrileri
- Confusion Matrix
- Classification Report (precision, recall, f1-score)
- Grad-CAM görselleştirmesi

## Sonuçlar

### Ana Model
- **Validation Accuracy:** ~0.82  
- **Test Accuracy:** ~0.84  
- **Macro F1:** 0.85  

**Classification Report (Test Set):**

| Class      | Precision | Recall | F1-Score |
|------------|-----------|--------|----------|
| Buildings  | 0.84      | 0.80   | 0.82     |
| Forest     | 0.96      | 0.97   | 0.96     |
| Glacier    | 0.82      | 0.79   | 0.81     |
| Mountain   | 0.82      | 0.74   | 0.78     |
| Sea        | 0.82      | 0.86   | 0.84     |
| Street     | 0.81      | 0.92   | 0.87     |

- Genel doğruluk: **%84**  
- En güçlü sınıf: Forest (F1 ≈ 0.96)  
- Zorlayıcı sınıflar: Mountain (F1 ≈ 0.78), Glacier (F1 ≈ 0.81)


## Hiperparametre Denemeleri

Farklı learning rate ve dropout oranları ile denemeler yapılmıştır:

- **adam_lr1e-3_do0.40** → best_val_acc = 0.713 → Test Acc ≈ 0.7957  
- **adam_lr5e-4_do0.50** → best_val_acc = 0.742 → Test Acc ≈ 0.7687  
- **adam_lr2e-3_do0.30** → best_val_acc = 0.717 → Test Acc ≈ 0.6755  

En başarılı kombinasyon: **lr=5e-4, dropout=0.50**  
Sonuç: **Test Accuracy ≈ 76.9%**

> Hiperparametre optimizasyonu sayesinde modelin farklı yapılandırmalarının performansı incelenmiş, overfitting/underfitting dengesi gözlemlenmiştir.


## Tartışma
- Model, orman sınıfını çok yüksek doğrulukla sınıflandırırken, görsel benzerlikler sebebiyle dağ ve buzul sınıflarında hata oranı daha yüksektir.  
- Dropout ve learning rate üzerinde yapılan denemeler, modelin daha kararlı öğrenmesini sağlamıştır.  
- Grad-CAM sonuçları, modelin görselin anlamlı bölgelerine odaklandığını göstermiştir.  


## Kaggle Notebook
# Akbank Derin Öğrenme Bootcamp Projesi: Görüntü Sınıflandırma

## Projenin Amacı
Bu proje kapsamında, **Convolutional Neural Network (CNN)** mimarisi kullanılarak 6 farklı sınıfa ait doğal görüntülerin sınıflandırılması hedeflenmiştir.  
Amaç, katılımcıların **derin öğrenme** alanında şu konularda deneyim kazanmasıdır:
- Görüntü işleme için veri önişleme ve veri görselleştirme
- CNN mimarisi kurma ve model eğitimi
- Performans değerlendirme metrikleri kullanma
- Modelin hangi bölgelerden etkilendiğini yorumlayabilme (Grad-CAM)
- Hiperparametre optimizasyonu ile model başarımını artırma

---

## Veri Seti
- Kaynak: [Intel Image Classification Dataset](https://www.kaggle.com/datasets/puneet6060/intel-image-classification)  
- Sınıflar: **Buildings, Forest, Glacier, Mountain, Sea, Street**  
- Dağılım:
  - Eğitim: 11,230 görsel
  - Doğrulama: 2,804 görsel
  - Test: 3,000 görsel

Veriler Kaggle üzerinden otomatik olarak yüklenmiş, yeniden boyutlandırılmış (**150x150**) ve `ImageDataGenerator` ile artırılmıştır (rotation, flip, zoom).

## Yöntem ve Modelleme

### 1. Veri Önişleme
- Görseller normalize edildi (0-1 arası ölçekleme).
- Augmentation ile modelin genelleme kabiliyeti artırıldı.

### 2. Model Mimarisi
Model **Keras** kullanılarak oluşturuldu. Ana bileşenler:
- Conv2D + ReLU (özellik çıkarımı)
- MaxPooling2D (boyut azaltma)
- Dropout (overfitting önleme)
- Dense katmanları + Softmax çıkış

### 3. Eğitim Süreci
- **Optimizer:** Adam
- **Learning rate:** 1e-3 (en başarılı kombinasyonlardan biri)
- **Batch size:** 64
- **Epochs:** 12
- **Callbackler:** EarlyStopping & ReduceLROnPlateau
- GPU hızlandırma (Tesla T4) ile eğitildi

### 4. Değerlendirme
- Accuracy ve Loss eğrileri
- Confusion Matrix
- Classification Report (precision, recall, f1-score)
- Grad-CAM görselleştirmesi

## Sonuçlar

### Ana Model
- **Validation Accuracy:** ~0.82  
- **Test Accuracy:** ~0.84  
- **Macro F1:** 0.85  

**Classification Report (Test Set):**

| Class      | Precision | Recall | F1-Score |
|------------|-----------|--------|----------|
| Buildings  | 0.84      | 0.80   | 0.82     |
| Forest     | 0.96      | 0.97   | 0.96     |
| Glacier    | 0.82      | 0.79   | 0.81     |
| Mountain   | 0.82      | 0.74   | 0.78     |
| Sea        | 0.82      | 0.86   | 0.84     |
| Street     | 0.81      | 0.92   | 0.87     |

- Genel doğruluk: **%84**  
- En güçlü sınıf: Forest (F1 ≈ 0.96)  
- Zorlayıcı sınıflar: Mountain (F1 ≈ 0.78), Glacier (F1 ≈ 0.81)

## Hiperparametre Denemeleri

Farklı learning rate ve dropout oranları ile denemeler yapılmıştır:

- **adam_lr1e-3_do0.40** → best_val_acc = 0.713 → Test Acc ≈ 0.7957  
- **adam_lr5e-4_do0.50** → best_val_acc = 0.742 → Test Acc ≈ 0.7687  
- **adam_lr2e-3_do0.30** → best_val_acc = 0.717 → Test Acc ≈ 0.6755  

En başarılı kombinasyon: **lr=5e-4, dropout=0.50**  
Sonuç: **Test Accuracy ≈ 76.9%**

> Hiperparametre optimizasyonu sayesinde modelin farklı yapılandırmalarının performansı incelenmiş, overfitting/underfitting dengesi gözlemlenmiştir.


## Tartışma
- Model, orman sınıfını çok yüksek doğrulukla sınıflandırırken, görsel benzerlikler sebebiyle dağ ve buzul sınıflarında hata oranı daha yüksektir.  
- Dropout ve learning rate üzerinde yapılan denemeler, modelin daha kararlı öğrenmesini sağlamıştır.  
- Grad-CAM sonuçları, modelin görselin anlamlı bölgelerine odaklandığını göstermiştir.  


## Kaggle Notebook
https://www.kaggle.com/code/beyzanurgen/beyzanurgen-akbanderin-renme-g-ncel

## Katılımcı
- **Beyza Nur Genç**

