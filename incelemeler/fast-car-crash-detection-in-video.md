# Fast car crash detection in video

* [İlgili Makale](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/pdfs/Fast%20car%20crash%20detection%20in%20video.pdf)

## Table Of Contents

* [Açıklama](fast-car-crash-detection-in-video.md#açıklama)
* [Araba Kaza Tespiti Aşamaları](fast-car-crash-detection-in-video.md#araba-kaza-tespiti-aşamaları)
* [Kullanılan Teknolojiler](fast-car-crash-detection-in-video.md#kullanılan-teknolojiler)
* [ViF Nedir? Neden Kullanılır?](fast-car-crash-detection-in-video.md#vif)
* [Önemli Noktalar](fast-car-crash-detection-in-video.md#Önemli-noktalar)
* [Ekran Görüntüleri](fast-car-crash-detection-in-video.md#bazı-ekran-görüntüleri)

### Açıklama

Bu makalede açıklanan olaylar bizim kendi amacımıza yönelik olduğundan yüksek önem taşıyor. Makalenin herkes tarafından güzelce ve detaylıca okunması, kaçırılan noktaların buraya eklenmesi ve takım arkadaşları ile paylaşılması gerekmektedir.

### Araba Kaza Tespiti Aşamaları

* Araba tespiti için kullanılan CNN kütüphanesi: _YOLO_ \(**Car Detection**\)
* Veri setindeki her arabanın kısa vidolarını oluştur. \(**Car Tracker**\)
* Videolar üzerinde vif algoritmasını kullan ve svm ile modelini kur.\(**Car Crash**\)
* Car Trackerde kullanılanlar: **Danellijan korelasyon Filtresi** + **DFT\(Discrete Foruier Transform\)** 
* Car crash: **Violent Flow Descriptor\(ViF\)** + **Support Vector Machine\(SVM\)**

### Kullanılan Teknolojiler

* GSM\(Global System for Mobile\)
* GPS\(Global Positioning System\)
* Kameralar
* Akıllı telefonlar

### ViF

### Önemli Noktalar

* Kaza Tespiti Algoritması'nda frame faktörünün yüksek önemi olabilir.
* Dataset oluşturulmasının düşünülmesi gerekiyor. Makalede kendileri oluşturmuş.
* Büyük videoları parçalara bölerek küçük videolar yapmışlar ve modellerini buna uygun olarak kullanmışlar

### Bazı Ekran Görüntüleri

* **\[Alt=Car Detect-Crash-Tract\]** ![Car Detect-Crash-Tract](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Car-Detection-Tracking-Crash.png)
* **\[Alt=Architecture of YOLO\]** ![Architecture of YOLO](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Architecture-Yolo.png)
* **\[Alt=Yolo Car Detection\]** ![Yolo Car Detection](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Yolo-Car-Detection.png)
* **\[Alt=Correlation Filter\]** ![Correlation Filter](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Correlation-Filter.png)
* **\[Alt=ViF Descriptor Algorithm\]** ![ViF Descriptor Algorithm](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Vif-Algorithm.png)
* **\[Alt=Car Crash Detection\]** ![Car Crash Detection](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Car-Crash-Detection.png)
* **\[Alt=Car Frames\]** ![Car Frames](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Car-Frames.png)
* **\[Alt=Car Crash Detection with Proposed Method\]** ![Car Crash Detection with Proposed Method](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/incelemeler/images/Fast&#32;car&#32;crash&#32;detection&#32;in&#32;video/Car-Detect-proposed.png)

