---
description: >-
  Bu notta SVG ile alakalı araştırmalar yapılmış ve alınan notlar aşağıda
  açıklanmıştır
---

# All About SVG’s

### SVG nedir

Scalable Vector Graphics XML tabanlı bir resim formatıdır. Diğer resim formatları \(_jpg_, _png_, _gif_\) aksine **SVG** ~pixel tabanlı~ değil ~vektör tabanlıdır~. Bu sebeple düzenlenmesi ve editlenmesi\(düzenlenmesi\) bir hayli kolaydır. Özellikle animasyonlarda yaygın olarak kullanılması bu esnek yapısından kaynaklanır.

### SVG’yi neden kullanmalıyım

* Dosya boyutu çok küçüktür
* Farklı cihaz boyutlarında da netlik kaybetmez
* Retina \(Yüksek piksel yoğunluğuna sahip\) ekranlarda mükemmel gözükür
* Tasarım kontrolleri oldukça kolaydır

### SVG leri en uygun hale getirmek için yapılabilecek adımlar

SVG leri kullandığımızda optimize etmek için yapabileceğimiz bazı adımlar bulunuyor. Bunları yapma nedenimiz SVG boyutunu küçültmek, anlaşılabilirliğini artırmak ve web performansımızı artırmaktır.

Kullanılabilecek uygulamalar arasında açık kaynak olarak paylaşılmış [svgo](https://github.com/svg/svgo) projesi kullanılabilir. Veya [svgo-gui](https://github.com/svg/svgo-gui) ile manuel olarak da yapabilirsiniz. SVG optimize işlemleri için bir çok farklı uygulama bulunuyor. Paylaşılanlar bunlardan sadece bazılarıdır.

> **Not**: SVG iconları içindeki `b` tagı yerine `use` tagının kullanılması performansta ciddi bir artışa sebep olacaktır.

### SVG’lerin implement edilme şekilleri

* **Image** taglarıyla import edilebilir. **Picture** elementi ile de import edilebilir.

  ```markup
  <img src="bblogo.svg" alt="Breaking Borders Logo" />
  ```

* **Background Image** kullanarak yapılabilir. Bu method SVG ler üzerinde değişiklik yapılmasını kısıtlayacağını unutmayalım 😉

  ```css
  .logo {
  background-image: url(bblogo.svg);
  }
  ```

* **Iframe** aracılığıyla import edilebilir

  ```markup
  <iframe src="bblogo.svg">Your browser does not support iframes</iframe>
  ```

* **Embed** ile de eklenebilir

  ```markup
  <embed type="image/svg+xml" src="bblogo.svg" />
  ```

* **Object** ile SVG ler import edilebilir. Bu SVG leri import etmek için en sağlıklı yöntemlerden biridir.

  ```markup
  <object type="image/svg+xml" data="svg-ok.svg">
  <p class="no-support">
    Your browser does not support SVG!
  </p>
  </object>
  ```

Eğer SVG elementimizin yedeğini\(fallback\) tag içerisinde eklemek istersek;

```markup
<svg viewBox="-20 -20 40 40">
  <!-- SVG code snipped -->
  <image src="fallback.png" xlink:href="" />
</svg>
```

Fakat bu şekilde image eklememiş tarayıcı tarafında birden fazla istek atılmasına neden olacaktır. Bunu önlemek için;

```markup
<object type=”image/svg+xml” data=”mySVG.svg”>
  <div id="fallback"></div>
</object>
```

```css
#fallback {
  background: url(fallback.png);
  width: 15em;
  height: 12em;
  ...
}
```

şeklinde bir önlem almak bu sorunun önüne geçmek için yardımcı olacaktır.

* **Inline** Olarak da import edilebilir. Hızlı bir şekilde SVG ler üzerinde işlem yapmak için en uygun yöntemdir. Http isteğinden kurtulacağınız için performans kazanırsınız. Fakat tarayıcılar artık SVG dosyasını ~cache~ yapamaz. Ve SVG dosyalarına html in içerisinde müdahale etmek ileride çok fazla sıkıntı doğurur.

  ```markup
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 68 65">
  <path fill="#1A374D" d="M42 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v21l12 15-7 15.7c14.5 13.9 35 2.8 35-13.7 0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"/>
  <path d="M14 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v41c0 8.2 9.2 17 20 17s20-9.2 20-20c0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"/>
  </svg>
  ```

### Tavsiye Edilen Kullanım Sırası

1. **Object**
2. **Image veya Background-Image**
3. **Inline Olarak**
4. **Embed veya iframe**

|  | **Object** | Inline | Img | Background-image |
| :--- | :--- | :--- | :--- | :--- |
| **CSS Manipulation** | Yes | Yes | Some Inline | Some Inline |
| **JS Manipulation** | Yes | Yes | No | No |
| **SVG Animation** | Yes | Yes | Yes | Yes |
| I**nteractive SVG Animation** | Yes | Yes | No | No |

### SVG’ye Css ile Müdahale Etme

SVG lerin bir diğer güzel özelliği ise değiştirmek istediğimiz bir özelliği kolayca uygulayabilmemiz. Örneğin bir adet kırmızı renkli icon umuz var ve biz bu iconun rengini farklı sayfalarda mavi yapmak istiyoruz. Bunun için yeni bir icon oluşturmak yerine css ile rengini düzenleyebilmemiz bizi gereksiz dosyalardan kurtarıyor.

Bunun için 2 türlü yöntemimiz var;

* Ya vericeğimiz stilleri\(style/css\) inline olarak element içerisinde vermek

  ```markup
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 68 65">
  <style type="text/css">
    <![CDATA[
    .firstb { fill: yellow; }
    .secondb { fill: red; }
    ]]>
  </style>
  <path class="secondb" d="M42 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v21l12 15-7 15.7c14.5 13.9 35 2.8 35-13.7 0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"/>
  <path class="firstb" d="M14 27v-20c0-3.7-3.3-7-7-7s-7 3.3-7 7v41c0 8.2 9.2 17 20 17s20-9.2 20-20c0-13.3-13.4-21.8-26-18zm6 25c-3.9 0-7-3.1-7-7s3.1-7 7-7 7 3.1 7 7-3.1 7-7 7z"/>
  </svg>
  ```

* External css dosyasında gerekli style’ları yazmak

  ```markup
  <!-- Add to very start of SVG file before <svg> -->
  <?xml-stylesheet type="text/css" href="style.css"?>
  ```

  ```css
  // In style.css
  .firstb { fill: yellow; }
  .secondb { fill: red; }
  ```

### Son Sözler

SVG çoğu tarayıcı tarafından destekleniyor. Bu sebeple SVG’leri kullanırken uygulamamızın SVG tarafından bozulacağı riski bir hayli az görünüyor. Bunun için tarayıcı desteklerini inceleyebileceğiniz [caniuse.com](https://caniuse.com/#search=svg) sitesine bakabilirsiniz.

### İletişim Halinde Olalım 😊

Benimle sosyal medya hesaplarım aracılığıyla iletişime geçebilirsiniz.

* [Linkedin Hesabım](https://www.linkedin.com/in/afozbek/)
* [Github Hesabım](https://github.com/afozbek)
* [Twitter Hesabım](https://twitter.com/afozbek_)

### Yararlanılan Kaynaklar

* [A Practical Guide to SVGs on the web](https://svgontheweb.com)
* [The Ultimate Guide To SVG by  Ezequiel Bruni](https://www.webdesignerdepot.com/2015/01/the-ultimate-guide-to-svg/)
* [ Using SVG by Chris Coyier ](https://css-tricks.com/using-svg/)
* [A Complete Guide to SVG Fallbacks by Amelia Bellamy-Royds](https://css-tricks.com/a-complete-guide-to-svg-fallbacks/)

## 

