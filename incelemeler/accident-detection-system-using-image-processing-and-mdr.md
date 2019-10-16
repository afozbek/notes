# Accident Detection System using Image Processing and MDR

* [İlgili Makale](https://github.com/afozbek/arac-kaza-tespiti/tree/84ec87d7a25201fe9e05970f9d8971daafdb898c/pdfs/Accident%20Detection%20System%20using%20Image%20Processing%20and%20MDR.pdf)

Aracın kaza tespitinin yapılabilmesi için belirli bir `threshold` değeri belirlenir. Ardından bu değeri aşan araçların trafik kazası yaptığın varsayılır. Bu işlem ise belirli değerlerin sum\(toplamasından\) oluşur.

* Belirli Değerler
  * Acceleration \(Km/sa, m/sn - Gidilen Hız\) -&gt; `ac`
  * Position \(Bulunulan konum\) -&gt; `pos`
  * Area \(Kaplanan alan, genişlik, büyüklük\) -&gt; `area`
  * Direction \(Gidilen yön, istikamet\) -&gt; `dir`
  * Threshold \(Verilen Limit Değer\) -&gt; `thr`

```python
if (ac + post + area + dir) >= thr:
    # Traffic Accident
else:
    # Vehicle Tracking...
```

