---
description: >-
  Tablist elemanlarının erişebilirlik açısından javascript ile nasıl
  yönetileceğini bu makalede açıklamaya çalışacağım.
---

# Javascript & Erişebilirlik: Tablist

Bu makalemizde tablistler üzerinde erişebilirliği javascript ile nasıl kontrol edebileceğimizi anlatmaya çalışacağım.

Genel olarak odaklanacağım konu başlıklarını açıklayacak olursam;

* Tablist için klavye desteğinin sağlanması
* Screen Reader desteğinin oluşturulması

olucaktır.

Başlangıç olarak bu makaleyi okumadan önce sizleri tablist in erişebilirlik üzerine uygulanması alanında çok fazla bilgi bulabileceğiniz kaynağın linkini paylaşmak istedim. Linke aşağıdaki bookmarktan ulaşabilirsiniz.

{% embed url="https://www.w3.org/TR/wai-aria-practices/examples/tabs/tabs-1/tabs.html" caption="Tablistler için Erişebilirlik Adımları" %}

Erişebilirlik özelliklerini eklerken örnekler üzerinden sizlere açıklamalar yapmaya çalışacağım.

Öncelikle sorunumuzu anlamaya çalışalım.

1. Kullanıcımız tablar arasında geçiş yaparken klavye kullanabilmeli ve tablar arasında ok tuşları ile geçebilmelidir.
2. Kullanıcımız silinebilen tabları klavyesi ile silebilmelidir
3. Screen Reader kullanan kullanıcılarımıza gerekli bilgilendirmeleri düzgün vermemiz gerekmektedir.

Sorunlarımızı listelediğimize göre ilk olarak genel yapıyı şekillendirmeye çalışalım. Çok fazla css e odaklanmak makaleyi uzatacağından stil kısmına çok fazla takılmadan genel olayları eklemeye çalışalım.

### HTML Yapısı

Html yapısı genel olarak button ve ilgili div elementlerinde oluşmaktadır.

{% embed url="https://codepen.io/afozbek/pen/vYEPOad" caption="a11y-tablist-1 - html yapısı" %}

### Aria Özellikleri

Aria özellikleri olarak ihtiyacımız olan elementler genel olarak ilgili butonun seçilip seçilmediğini bilgilendirmek için kullanacağımız **aria-controls** özelliği, kontrol ettiği paneli söylemek için kullanacağımız **aria-controls** özelliği ve ayrıca genel olarak çoğu yapıda ortak kullanılan **tabindex** ve **role** özellikleri olacaktır. Bu özellikler screen reader kullanan kullanıcılara detaylı bilgilendirme yapmak için olacaktır. Daha detaylı bilgilendirme için makalenin başında belirttiğim linke tıklayarak bilgi alabilirsiniz.

```markup
<div class="m-buttonList" role="tablist">
	<button class="m-buttonList__tabBtn" 
        role="tab" 
        aria-selected="true"
        aria-controls="tab1"
        >Tab-1</button>
	<!-- ... -->
</div>
<div class="m-contentList">
	<div class="m-contentList__tab -tab1 -open" 
        id="tab1"
        tabindex="0"
        role="tabpanel"
        >
        Tab-1 panel
      </div>
</div>
```

{% embed url="https://codepen.io/afozbek/pen/XWJGbwN" caption="a11y-tablist-2 - Aria Özellikleri Ekleme" %}

### Stil Ekleme

Css kısmında çok fazla vakit kaybetmek istemediğimden genel olarak yapıyı aktarmaya çalışacağım. O sebeple en azından göze hoş gelmesi açısından css eklemeye çalışalım.

{% embed url="https://codepen.io/afozbek/pen/xxbBGvL" caption="a11y-tablist3 - stil ekleme" %}

Belirtmek istediğim bir noktayı açıklayacak olursam;

```css
.m-contentList {
 &__tab {
  display: none; 
  
  &.-open {
   display: block; 
  }
 }
}
```

Butonumuz tarafından açılan tabımıza javascript tarafında **-open** class ı ekliyeceğiz. İsimlendirme olarak **-open** seçmemim nedeni bu classın modifier özelliğini taşımasındandır. Çok fazla ayrıntıya girmeden devam ediyorum.

Genel olarak yapıya baktığımızda her bir tabımızı aktif eden ilgili butonlarımız bulunmakta ve atanan **-open** class ına göre de ilgilin tabımız açılmaktadır. Html css kısmında eklemek istediklerimiz genel olarak bu kadardı. Manuel olarak **-open** class ını değiştirmeyeceğimiz için artık javascript kısmına geçebiliriz.

### Javascript

Evet artık bu kısımı 2 parçaya bölmek istedim.

* İlk olarak butonlarımıza ekleyeceğimiz event handler ları tanımlıyacağız. Klavye üzerinden hangi tuşları kullanacağımıza bakıcağız. Ve bunları javascript tarafında oluşturacağız.
* Diğer kısımda oluşturduğumuz event leri dolduracağız ve html üzerinde söz sahibi olacağız.

#### Event Tanımlama

Burada bizim aslında kullanmamız gereken elementler: Butonlarımız ve tablarımız. Bu sebeple bunları öncesinde seçmemiz gerekir. Tuş olarak da ok tuşlarını ve tab silmek için delete tuşunu kullanacağımız için bunların key code larını tanımlamamız gerekir. Sonrasında her bir buton için hem **click** hem de **keydown** eventi tanımlamamız gerekicektir. O zaman kodlamaya başlayalım;

```javascript
const keyCodes = {
  up: 38,
  down: 40,
  left: 37,
  right: 39,
  del: 46
 };

const tabBtns = document.querySelectorAll(".m-buttonList__tabBtn");
// Change Html Document to Array
const contentTabs = Array.from(document.querySelectorAll(".m-contentList__tab"));

tabBtns.forEach(btn => {
 btn.addEventListener("keydown", function (e) {
 	     // Change focus between tabs
   }
 });
 
 btn.addEventListener("click", function (e) {
 	     // Switch between tabs
 });
});
```

Burada görüceğiniz gibi her bir buton için keydown ve click event handler ları oluşturduk ve olacak olayları belirttik. Bu kısımda her şey çok açık olduğundan diğer adıma geçiyorum.

#### Event Uygulama

Bu kısım bir önceki bölüme göre birazcık daha dikkat gerektirdiğinden elimden geldiğince her şeyi açıklamaya çalışacağım. Öncelikle click eventinde yapmamız gereken seçilen tabın class ını değiştirmek olacaktır. Bunun için öncelikle bütün tabları dolaşıp **-open** class ını kaldırıp daha sonrasında ise butonun control ettiği tabı bulup o taba -**open** classını ekleyeceğiz;

```javascript
tabBtns.forEach(btn => {
	btn.addEventListener("click", function (e) {
	  contentTabs.forEach(tab=> tab.classList.remove("-open"));
	
	  let controlledTabId = this.getAttribute("aria-controls");
	  let controlledTab = contentTabs.find(tab=> tab.getAttribute("id") === controlledTabId);
	  controlledTab.classList.add("-open");
	});

	// keydown event will be added
});
```

{% embed url="https://codepen.io/afozbek/pen/qBEvOqo" caption="a11y-tablist-4 - event uygulama 1" %}

Click eventimizde yapacaklarımız bu kadardı. Şimdi **keydown** eventini kodlamaya çalışalım. Öncelikle burda anlatmadan önce kodu incelemenizi istiyorum;

```javascript
tabBtns.forEach(btn => {
	
	// ... click event
	
	btn.addEventListener("keydown", function (e) {
	  if (e.keyCode === keyCodes.up || e.keyCode === keyCodes.left) {
	    selectPreviousEl(this, tabBtns[tabBtns.length - 1]);
	  } else if (e.keyCode === keyCodes.down || e.keyCode === keyCodes.right) {
	    selectNextEl(this, tabBtns[0]);
	  } else if (e.keyCode === keyCodes.del) {
	    if (!this.dataset || !this.dataset.hasOwnProperty("deletable")) {
	      console.log("You can't delete that 😢")
	      return;
	    }
	
	    let controlledTabId = this.getAttribute("aria-controls");
	    let controlledTab = contentTabs.find(tab=> tab.getAttribute("id") === controlledTabId);
	
	    controlledTab.parentNode.removeChild(controlledTab);
	    this.parentNode.removeChild(this);
	  }
	});
});

function selectPreviousEl (target, defaultEl) {
  const prevEl = target.previousElementSibling;
  let selectedEl;
  if (prevEl) {
    selectedEl = prevEl;
  } else {
    selectedEl = defaultEl;
  }

  focusSelectedElement(selectedEl);
}

function selectNextEl (target, defaultEl) {
  const nextEl = target.nextElementSibling;
  let selectedEl;
  if (nextEl) {
    selectedEl = nextEl;
  } else {
    selectedEl = defaultEl;
  }

  focusSelectedElement(selectedEl);
}

function focusSelectedElement (selectedEl) {
  tabBtns.forEach(btn=> {
    btn.setAttribute("tabindex", "-1");
    btn.setAttribute("aria-selected", false);
  });

  selectedEl.setAttribute("tabindex", "0");
  selectedEl.setAttribute("aria-selected", true);
  selectedEl.focus();
  selectedEl.click(); // tab lar arasında hemen geçmek istemez iseniz burayı yorum satırına alın
}
```

{% embed url="https://codepen.io/afozbek/pen/qBEvORo" caption="a11y-tablist-5 - event uygulama 2" %}

Burada yapılan olayları açıklayacaksak olursam ok tuşlarına göre focus edilen elementi değiştirdik ve bunları ayrı fonksiyonlara yazarak okunabilirliği artırdık. Tabi ki bu fonksiyonların performansları daha da artırılabilir. Fakat odaklanmamız gereken şu anlık klavye fonksiyonelliğidir. **data-deletable** özelliğine sahip buton **del** tuşuna basıldığında hem kendisi hem de ilgili paneli dom dan silinecektir. Silindikten sonra kullanıcıyı yormamak adına bir önceki kardeş elementi yoksa diğer kardeş elementine focus olacaktır. İkisi de olmama durumunu söyleyecek olursanız genelde bu yapılarda en fazla 1 tane silinecek element bulunur. Yani developer ın eğer öyle bir durum oluşma ihtimali varsa bunu da eklemesi gerektiğini belirtelim.

Benim bu yazıda anlatıcaklarım bu kadar screen reader açısından da test edebilirsiniz. Burada bunu anca ekran görüntüleri ile gösterebilirdim. Fakat bunu kendiniz denerseniz daha bilgilendirici olduğunu düşünmekteyim. Son olarak geliştirdiğimiz yapıyı paylaşak olursam da;

{% embed url="https://codepen.io/afozbek/pen/abzMzje" caption="a11y-tablist-finished - Son Hali" %}

### Son Sözler

Son olarak gördüğünüz gibi aria özelliklerini takip etmek ve kullanmak oldukça kolay. Sadece engelli kullanıcılar için değil, engelli olmayan kullanıcılar için de bir hayli önem arz ediyor. Siz de benim gibi kullanıcı deneyimine bir hayli önem gösteriyorsanız projelerinizde bu konulara dikkat etmeniz hem sizi bir hayli geliştirecek, hem de kullanıcılarınızı sitenizde memnun edecektir. Erişebilir olmak üzere...

### Yararlanılan Kaynaklar 📚

[Aria-Best-Practices](https://www.w3.org/TR/wai-aria-practices/)

{% embed url="https://www.w3.org/TR/wai-aria-practices/" %}

{% embed url="https://www.w3.org/TR/wai-aria-practices/examples/tabs/tabs-1/tabs.html" caption="Tablar ve Tablist lerin Kullanımı" %}

{% embed url="https://dev.to/lkopacz/javascript-and-accessibility-accordions-5ecd" caption="Dev.to da Javascript ve Erişebilirlik: Accordionlar üzerinden yazılmış makale" %}

{% embed url="https://www.accessibility-developer-guide.com/introduction/about/" caption="Accessibility Developer Guide" %}

### İletişim Halinde Olalım 😊

Benimle sosyal medya hesaplarım aracılığıyla iletişime geçebilirsiniz.

* [Linkedin Hesabım](https://www.linkedin.com/in/afozbek/)
* [Github Hesabım](https://github.com/afozbek)
* [Twitter Hesabım](https://twitter.com/afozbek_)

