#🌟 StarFinal: Bp-Rp Renk İndeksi ile Teff Tahmini

Bu proje, yıldızların Bp−Rp renk indeksi ile etkin sıcaklıklarının (Teff) tahmin edilmesi üzerine kuruludur. Hem Bayesian Ridge Regression hem de MCMC (Markov Chain Monte Carlo, NumPyro/NUTS) yöntemleri kullanılarak modeller oluşturulmuş, farklı veri kümeleri üzerinde test edilmiştir.
---

## İçindekiler
- [Proje Amacı](#-proje-amacı)  
- [Kullanılan Yöntemler](#-kullanılan-yöntemler)  
- [Veri Setleri](#-veri-setleri)  
- [Kurulum ve Çalıştırma](#️-kurulum-ve-çalıştırma)  
- [Kod Yapısı](#-kod-yapısı)  
- [Sonuçlar](#-sonuçlar)  

---
## Proje Amacı
Bp−Rp renk indeksi ve Teff arasındaki ilişkiyi modellemek.
Farklı polinom dereceleri ve α/λ parametreleriyle Bayesian Ridge’i test etmek.
MCMC ile belirsizlikleri hesaplamak.
Yeni veri kümelerinde (ör. kumeler2_bprp.txt, variable_members.dat, UPK_220.gaia) modelin genellenebilirliğini incelemek. Gerekli veri dosyaları StarFinal repository'sinde bulunmaktadır.
---
## Kullanılan Yöntemler
Bayesian Ridge Regression → α, λ başlangıç değerleri denenerek en uygun model seçildi.
Polinomsal Özellikler (Vandermonde) → renk indeksi için polinom tabanlı özellikler üretildi.
MCMC (NumPyro + NUTS) → posterior dağılımlar örneklenip tahminler ±1σ belirsizlik ile sunuldu.
Karşılaştırma → R², MAE, MSE, RMSE metrikleri hesaplandı.
---
## Veri Setleri
Projede kullanılan ana ve ek dosyalar:
spec_table.d → Ana eğitim verisi (Teff, Bp−Rp).
kumeler2_bprp.txt, kümeler_(bp-rp)_(bp-rp)0=.txt → Küme verileri.
variable_members.dat, UPK_220.gaia → Ek test verileri.
---
## Kurulum ve Çalıştırma
Gerekli kütüphaneleri yüklemek için: pip install numpy pandas matplotlib scikit-learn jax jaxlib numpyro arviz corner graphviz
Colab’da çalıştırmak için dosyaları yükleyip notebook’u açın dosyaları adlarına uygun yükleyin.
---
## Kod Yapısı
Notebook içindeki ana adımlar:
Veri Yükleme ve Temizleme → NaN değerleri silme, sayısal dönüştürme.
Bayesian Ridge → Model 1 & Model 2 denemeleri, skorlar ve grafikler.
Parçalı Polinom Denklem → Bp−Rp için [0–2] ve [2–5] aralıklarında farklı denklemler.
Yeni Veri Üzerinde Testler → Küme ve UPK verileri üzerinde tahminler.
MCMC Tahminleri → NumPyro ile posterior dağılım ve belirsizlik grafikleri.
Karşılaştırma ve Hata Analizi → Gerçek Teff vs model tahminleri, hata tablolar

## Sonuçlar
Model 1 (α = 1/var(y), λ=1.0) başarısız → R² negatif.
Model 2 (α=1.0, λ=1e−3) başarılı → R² ≈ 0.97, MAE ≈ 220 K.
MCMC tahminleri ±1σ bandıyla güvenilir aralıklar sundu.
Yeni verilerde (UPK, kümeler) model mantıklı tahminler üretti.
