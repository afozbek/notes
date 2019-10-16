# Intelligent traffic video surveillance and accident detection system

* [İlgili Makale](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/pdfs/Intelligent%20traffic%20video%20surveillance%20and%20accident%20detection%20system.pdf)
* Çalışmada kaza tespiti, trafik izleme sistemi, trafik sinyal kontrolü uygulamaları gerçekleştirilmiştir.
* Videoların ön işlenmesi ve gürültünün giderilmesi için **hybrid median filter** kullanılmıştır.
* Arabaları takip etmek için **hybrid support vector machine** kullanılmıştır
* Kaza tespiti için **multinomial lojistik regresyon** yöntemi kullanılmıştır.
* Ambulans tespiti yapmak için DNN kullanılmıştır.

## Vehicle Tracking

* Hybrid SVM kullanılmıştır -&gt; SVM + Kalman Filter
* Araç tespitinden sonra Kalman Filtresi kullanılır. Üç adımda uygulanır:
* Tespit edilen araçlara güven değeri \(CFV\) ve ID verildi.
* Araçların gelecekteki konumlarını tahmin etmek için her araca Kalman Filteri tarafından tahmin yapıldı.
* Videonun bir sonraki karesindeki yeni ölçümler tahminlerle karşılaştırılır.

## HFG Feature Extraction - Algoritmada kullanılan feature'lar

* Araç hızındaki ani değişim kaza kaynaklı olacağından dolayı araç hızındaki değişim oranı kaza tespitinde kullanılmıştır. \(variation of velocity\)
* Konumun değişim hızı
* Alanın değişim hızı
* Yönün değişme oranı

## Dataset

Kendileri hazırlamış :/

