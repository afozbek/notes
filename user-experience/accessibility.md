# Web Accessibility Notlar

## Web Accessibility Notları

Created By: Abdullah Furkan Özbek Last Edited: Dec 05, 2019 10:08 PM Tags: accessibility, frontend, user-experience

## What is Web Accessibility

Accessibility is strongly related to universal design which is the process of creating products that are usable by people with the widest possible range of abilities, operating within the widest possible range of situations. This is about making things accessible to all people \(whether they have a disability or not\).

> Making an accessible site means making it for ‘almost’ everyone.

{% hint style="success" %}
The power of the Web is in its universality. Access by everyone regardless of disability is an essential aspect.

                          -- Tim Berners-Lee, W3C Director and inventor of the World Wide Web 
{% endhint %}

### Who Affects By It

1. Web accessibility means that websites, tools, and technologies are designed and developed so that people with disabilities can use them. More specifically, people can:
   * perceive, understand, navigate, and interact with the Web
   * contribute to the Web
2. Web accessibility encompasses all disabilities that affect access to the Web, including:
   * auditory \(işitsel\)
   * cognitive \(bilişsel-idrak\)
   * neurological \(nörolojik, sinirsel\)
   * physical \(fiziksel\)
   * speech \(konuşma\)
   * visual \(görme\)
3. Web accessibility also benefits people without disabilities, for example:
   * people using mobile phones, smart watches, smart TVs, and other devices with small screens, different input modes, etc.
   * older people with changing abilities due to ageing
   * people with “temporary disabilities” such as a broken arm or lost glasses
   * people with “situational limitations” such as in bright sunlight or in an environment where they cannot listen to audio
   * people using a slow Internet connection, or who have limited or expensive bandwidth

{% embed url="https://www.youtube.com/watch?v=LdVlbO7\_hz8" caption="Understanding Diversity" %}

## Accessibility Types

{% embed url="https://medium.com/@realabhijeet4u/9-tips-to-get-bare-minimum-of-web-accessibility-739899a9437c" %}

### Keyboard accessible

All the interactive elements of your page e.g. text boxes, buttons etc should be accessible by keyboard. That means you should be able to bring focus on them by using Tab and Shift+Tab keys.

Most of the interactive elements are keyboard accessible by default, i.e. browser takes care of making them keyboard ‘focus-able’.

Non interactive elements like div, span and images are not keyboard accessibly by default. This is fine because users don’t generally need to interact with them.

### Tab-order

Eğer kullanıcı bir veri girmiyorsa ve bir yere yönlenmiyorsa **focusable** olması gereksizdir

* The order in which elements get focus is called tab-order. Developers need to take care that the interactive elements have logical tab-order. Tab order should follow the natural reading sequence i.e. top to bottom and right to left \(for an RTL type language\). If your tab focus is jumping around the page unpredictably then its not going to be great experience for the users.
* Tab-order mainly depends on the dom-order, i.e. the way you have written your html. Any element which is ahead in the dom tree automatically goes ahead in the tab-order.
* Sometimes people use css to make the element appear in an order which is different form dom-order. Example

```markup
<a href="#" style="float:right;">Right aligned link</a> 
<a href="#">Link 1</a> 
<a href="#">Link 2</a>
```

* In above example first the focus will move to right and then it will come to left because right aligned link appears above in dom. That’s not great because you would generally expect leftmost link to be focussed first. 

This is how you can **solve** it:

```markup
<a href="#">Link 1</a> 
<a href="#">Link 2</a> 
<a href="#" style="float:right;">Right aligned link</a>
```

**INERT** initially belirli kısımları unfocusable yapmak için kullanılan bir js kütüphanesi:

{% embed url="https://github.com/WICG/inert/blob/master/src/inert.js" caption="inert.js" %}

### tabindex

Recommended Usage **0 for tab accessible** and **-1 for tab unaccessible**

* To make a non interactive element focusable you can give it tabindex= 0 attribute. Example: Dummy text&lt;/div&gt;. This not only makes the element tab accessible but also makes it programmatically focusable. That means you can call .focus\(\) on that element.
* tabindex= -1 will take out any interactive element from tab-order. That means you can not access it through keyboard. This is particularly useful when you want to make few links/buttons inaccessible when they are behind an overlay or transitioned out of display \(e.g. hamburger menus\)
* Positive tabindex value makes the element tab accessible and also puts the element ahead in tab-order based on the value of the attribute. But positive tabindex values are considered anti-pattern becuase it may get very confusing more than one elements have positive tabindex values. So, don’t use positive tabindex.

### Use native elements

{% embed url="http://nativeformelements.com/" %}

* As far as possible please use native elements for any specific purpose. That means, for example, if you need a button then just use button tag rather than making a button using divs or spans.
* Native interactive elements like buttons, selectboxes etc have many built in accessibility features which you might miss if you are creating your own.

### Guideline for custom elements

* If you must create a custom element then make sure that you go through the wai-aria best practices guide: [WAI-ARIA Authoring Practices 1.1](https://www.w3.org/TR/wai-aria-practices-1.1/)
* These guidelines tell you how the keyboard interactions should be for any element. It also has links to demo and code examples for our help.

{% embed url="https://codepen.io/afozbek/pen/yLyLWVG" %}

Kodda da görüldüğü gibi tabindex değerimiz 0 yapılarak div elementini focusable yapıyoruz.

{% embed url="https://www.youtube.com/watch?v=CZGqnp06DnI&list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g&index=5" %}

{% embed url="https://www.w3.org/TR/wai-aria-practices-1.1/examples/button/button.html" %}

### Screen readers

* Many users with visual impairment rely on assistive tools like screen readers to get information on the page and to interact with page
* Always use **alt attribute** for images. Screen readers would read out the alt text for its users who have difficulty in seeing the image.
* Use proper heading tags , ,  etc for headings, because screen readers allow users to navigate within the content of page using headings.
* Make efficient use of semantic tags like , , ,  etc because screen readers allow users to navigate within the content of page using these tags.
* Screen readers need to identify the interactive elements correctly so it can ask users to interact with them. For example, if you have created a button using  tag then screen reader will call it out as button. But if your button is something like this Submit then screen reader will call it a “group” because div is grouping element, and user would not understand that they are supposed to interact with that element.

**How HTML elements are supported by screen readers**

{% embed url="https://thepaciellogroup.github.io/AT-browser-tests/?utm\_source=html5weekly&utm\_medium=email" %}

### **Labels and aria attributes**

* Any code written in html not only has a visual representation but also has a semantical representation called accessibility tree. Accessibility tree is used by assistive tools like screen readers to inform the user about the accessibility properties like type, name, state and value of the element. The values of these accessibility properties are computed by browser based on the information provided in html code.

![](../.gitbook/assets/1ncw2mdwhofoxlhkzagsnla%20%281%29.png)

* In above example name is computed by the  tag. Make use of label tag wherever applicable.
* Use aria-label attribute to ensure that element has a name. Suppose you have a save button which does not have a text content, then browser will not be able to compute its name. We can mention aria-label attribute to help browser compute its name.

![](../.gitbook/assets/15gmyvcwop-voychqnp6vmq.png)

* Similarly use different aria attributes like role, aria-labelledby, aria-expanded, aria-checked etc to help browser compute accessibility properties:

{% embed url="https://www.w3.org/TR/wai-aria-practices-1.1/" %}

### **Use tools**

* [aXe](https://chrome.google.com/webstore/detail/axe/lhdoppojpmngadmnindnejefpokejbdd) is an amazing tool to identify the accessibility gaps in your page. It is a chrome extension. Install it and use through chrome dev tools to analyse the accessibility of the page.
* Use aXe to analyse colour contrast in your page. A bad colour contrast ratio will make it difficult for few users to read the text. aXe can point out the regions of your page where the contrast does not match the [WCAG guidelines](https://www.w3.org/TR/WCAG20/#visual-audio-contrast).
* Chrome has an experimental [accessibility inspector](https://gist.github.com/marcysutton/0a42f815878c159517a55e6652e3b23a) in dev tools. Go to setting -&gt; experiments in chrome dev tools to enable it. This tool helps by letting you know the computed accessibility properties
* If you want to automate the accessibility audit in your project, you can use [axe-core](https://github.com/dequelabs/axe-core). It is a node module which you can include in your build process.

### **Libraries and polyfills**

[**inert.js**](https://github.com/WICG/inert) is a very useful library which helps you make a part of your page tab **inaccessible or accessible**. This is particularly useful when you want to make few links/buttons inaccessible when they are behind an overlay or transitioned out of display \(e.g. hamburger menus\)

Focus-ring is the outline which gets displayed around the control when it receives focus. At times, especially with buttons, these focus rings are not very aesthetically pleasant so developers tend to disable it in css \(outline:none\). Mouse users wouldn’t face any issues because of this but keyboard users find it problematic because can’t figure out whether the control has focus or not. Ideally focus ring should be visible to keyboard user even if it is invisible for mouse user. Here is an awesome library;

{% embed url="https://github.com/WICG/focus-ring" %}

{% embed url="https://medium.com/hackernoon/removing-that-ugly-focus-ring-and-keeping-it-too-6c8727fefcd2" %}

### Screenshots

![What-If](../.gitbook/assets/code-accessibility-warning%20%281%29.jpg)

![Checking Accessibility With AXE](../.gitbook/assets/screen-shot-2019-12-09-at-09.18.02.png)

![Checking Accessibility With Chrome Lighthouse](../.gitbook/assets/screen-shot-2019-12-09-at-09.20.42.png)

![](../.gitbook/assets/screen-shot-2019-12-09-at-09.21.51%20%281%29.png)

![](../.gitbook/assets/screen-shot-2019-12-09-at-09.22.23.png)

### Yararlanılan Kaynaklar

{% embed url="https://www.w3.org/WAI/fundamentals/accessibility-intro/" %}

{% embed url="https://frontendmasters.com/books/front-end-handbook/2019/\#4.14" %}

{% embed url="https://www.youtube.com/playlist?list=PLNYkxOF6rcICWx0C9LVWWVqvHlYJyqw7g" %}

