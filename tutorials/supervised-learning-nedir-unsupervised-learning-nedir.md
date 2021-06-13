---
description: >-
  Bu makalemizde machine learning eğitim sürecinde kullanılan farklı methodları
  inceliyor olacağız. Kullanıldıkları yerleri belirtecek önemli noktaları
  sizlere belirtmeye çalışacağız.
---

# Supervised Learning nedir Unsupervised learning nedir?

### Supervised Machine Learning \(Teşvikli Öğrenme\)

Türkçesi Teşvikli Öğrenme olarak geçen Supervised Learning’de aşağıdaki ifadede de gösterildiği gibi **input** ve **output** olarak iki farklı değişkenimiz vardır. Modelimiz input değerini oluşturacağımız mapping fonksiyonu içerisinde kullanarak bir output üretmektedir. Bunun için belirli bir ::success rate:: belirlenir. Amaç modelimize bu success rate’ i üzerinde doğru sonuç ürettirmektir.

* _İnput_ -&gt; X
* _Output_ -&gt; Y

```text
f(X) => mapping function
Y = f(X)
```

Bu öğrenme tipine teşvikli öğrenme denilmesinin sebebi eğitilecek datasetin sisteme öğrenim başlangıcında verilmesidir.

#### Teşvikli Öğrenme problemleri daha da gruplandırılabilir;

* **Classification \(Sınıflandırma\)**: Output değerlerinin kategorilerden oluştuğu problem tipleridir. **Örn:** _Kırmızı, Sarı_, veya _Hasta, Sağlıklı_ gibi…
* **Regression \(Gerileme\)** Output değerlerinin gerçek verilerden oluştuğu değerlerdir. **Örn:** _Dolar, Türk Lirası_ veya _Kilo, Boy_

#### Bazı gerçek zamanlı kullanılan problem örnekleri

* **Linear Regression** \( ~Regression~ \)
* **Random Forest** \( ~Regression~, ~Classification~ \)
* **Support Vector Machines** \( ~Classification~ \)

### Unsupervised Machine Learning \(Teşviksiz Öğrenme\)

Türkçesi Teşviksiz, Yardım Olmadan Öğrenme olarak geçen Unsupervised Learning’ de sistemimize yalnızca input datası verilir. Bu öğrenim yönteminde modele herhangi bir yardım sağlanmaz ve modelden belirli bir output vermesi beklenmez. Çünkü neyin doğru neyin yanlış olduğu sisteme belirtilmemiştir.

#### Teşviksiz Öğrenim problemleri daha da gruplandırılabilir;

* **Clustering \(Bölükleştirme\)** Bu tip problem yönteminde yapılmak istenen; data yı belirli gruplara bölerek, farklı grupların sistem üzerindeki etkisini görmektir. Müşterileri satın alma davranışına göre gruplamak bu gruba örnek olarak verilebilir.
* **Association \(İlişkilendirme\)** Bu tip problem yönteminde, X ürününü alan insanların Y ürününü de alma eğiliminde olup olmadığı keşfedilmeye çalışılır

#### Bazı gerçek zamanlı kullanılan problem örnekleri

* **k-means** \( ~Clustering~ \)
* **Apriori Algorithm** \( ~Association~ \)

### Semi-Supervised Machine Learning \(Yarı Teşvikli Öğrenme\)

Türkçesi Yarı Teşvikli Öğrenme olarak geçen bu öğrenim methodunda datasetimiz içerisinde çok fazla verimiz var fakat verilerimizin çoğu etikelenmemiştir. Yani verilerimiz çoğu için modelimiz bir öğrenim süreci geçirmesi gerekir \(Unsupervised\). Diğer etiketlenen kısımlarda ise modelimiz bizden yardım aldığı için ne yapması gerektiğini biliyor olucaktır \(Supervised\).

Buna en uygun örnek olarak fotoğraf albümü verilebilir. Fotoğraf albümünde fotoğraflarımızın bazılarının etiketli olduğunu \(_köpek, kedi, insan, araba, vs._\) çoğunun ise etiketli olmadığını varsayalım. Bu verilerimiz ile bir model eğitmeye kalktığımızda etiketlenmemiş kısımları için modelimizin bir tahmin yürütmesi ve bir süreçten geçmesi gerekecektir \(Unsupervised\).

Çoğu gerçek zamanlı problemler bu alana düştüğünü de belirtmekte fayda vardır. Eğer verilerinizi kendiniz etiketlemek durumundaysanız bu oldukça fazla zaman alıcak ve oldukça masraflı olacaktır. Etiketlenmemiş verilen toplanması ve saklanması gerçekten ucuz ve kolaydır.

### Genel Özet

Bu makalemizde supervised, unsupervised ve semi-supervised machine learning methodlarına değindik.

Genel olarak şunları öğrendik;

* **Supervised:** Bütün veriler etiketlenmiştir. Algoritmalar, girdi verilerinden çıktıyı tahmin etmeyi öğrenirler
* **Unsupervised:** Hiç bir veri etiketlenmemiştir. Algoritmalar girdi verilerinden doğal yapıyı öğrenirler.
* **Semi-Supervised** Bazı veriler etiketlenmiştir ancak çoğu veri etiketlenmemiştir. Supervised Learning ve Unsupervised Learning teknikleri birlikte kullanılabilir.

### Yararlanılan Kaynaklar 📚

* [Supervised and Unsupervised Machine Learning Algorithms by Jason Brownlee](https://machinelearningmastery.com/supervised-and-unsupervised-machine-learning-algorithms/)

### İletişim Halinde Olalım 😊

Benimle sosyal medya hesaplarım aracılığıyla iletişime geçebilirsiniz.

* [Linkedin Hesabım](https://www.linkedin.com/in/afozbek/)
* [Github Hesabım](https://github.com/afozbek)
* [Twitter Hesabım](https://twitter.com/afozbek_)

