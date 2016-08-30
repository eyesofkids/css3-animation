# CSS3轉場效果(transitions)

在CSS3之前的轉場特效，都是立即完成的，轉場特效提供了更為豐富的動畫效果，以下為本章用來說明的一個簡單範例:

```css
.box {
background: #2db34a;
border-radius: 6px;
height: 95px;
width: 95px;
}

.box:hover {
background: #ff2956;
}
```

下面是我們的第一個範例，左邊的是用上面的定義的方形，右邊的有另外加一行`transition: 1s;`的定義，它會在滑鼠游標在上面時，出現轉場效果，滑鼠游標移開後會回復原來的屬性，你可以比對看看兩者的不同。

[](codepen://eyesofkids/vXBOAA/)

轉場特效使用四個CSS屬性來進行定義，這些屬性可以整個合併到一個`transition`屬性之中:

- **transition-property**: 定義哪些CSS屬性會被轉場效果影響。除了這些被指定的屬性，其他的轉場一如以往的會在瞬間完成。要特別注意的是，並非所有的CSS屬性都可以進行轉場，可用的屬性所有清單在[這份資料](http://oli.jp/2010/css-animatable-properties/)與[可進行動畫屬性](https://www.w3.org/TR/2009/WD-css3-transitions-20091201/#animatable-properties-)，其中也包含了SVG的屬性。如果這個屬性定義為`transform`，代表任何使用了`transform`的屬性都會被偵測來進行動畫。如果這個屬性定義為`all`，就會自動偵測所有可進行動畫的屬性，包含`transform`影響的屬性。預設值就是`all`。

- **transition-duration**: 定義轉場的持續時間。可以只定義一個時間給所有屬性使用，也可以分別給定不同時間。時間通常以`s`為單位(秒)，可以定義小數點例如`0.5s`或`.5s`，預設值是`0s`。

- **transition-timing-function**: 時間函式，這是用來設定轉場過程時所使用的貝茲曲線。內建的幾個可直接使用數值如下，直接使用名稱就可以取用。在[這個頁面](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function)中看到所有的預設值的範例:

  - ease
  - linear
  - ease-in
  - ease-out
  - ease-in-out
  - step-start
  - step-end
  - steps()
  - cubic-bezier()

其中`cubic-bezier()`的數值，可以到[cubic-bezier.com](http://cubic-bezier.com/)來自訂所需要的貝茲曲線參數值，或是到這一頁[Easing函數](http://easings.net/zh-tw)或[CSS EASING ANIMATION TOOL](https://matthewlein.com/ceaser/)的裡面挑選你想要的Easing函數，使用四個數字值可以產生一個貝茲曲線。預設值是`ease`。

- **transition-delay**: 定義多久之後開始發生轉場，這是一個延遲開始的時間。時間通常以`s`為單位(秒)，可以定義小數點例如`0.5s`或`.5s`，預設值是`0s`。

`transition`屬性的合併寫法是按照上面的順序依次寫成一整行，所以如果都是以預設值來寫CSS定義的話，可以用非常簡單的寫法像這樣:

```
transition: .5s;
```

相當於下面這樣，第1、3、4值都是使用預設值。而`.5s`代表的是持續期間(duration)，而且因為最後面的那個延遲開始(delay)的預設值是0s，一般都不寫:

```
transition: all .5s ease;
```

> 註: 雖然你可以用`ms`(微秒，千分之一秒)為單位來設定持續與延遲開始時間，但似乎不必要，因為太短暫的時間差人眼無法感覺差異。

> 順序口訣: 屬性的順序的口訣，例如"屬持茲遲"(手持支援)或"屬續貝延"(手續被延期)

你也可以為每個不同的CSS屬性分別設定轉場的動畫定義:

```css
.box {
background: #2db34a;
border-radius: 6px;
height: 95px;
width: 95px;

-webkit-transition: background .2s linear, border-radius 1s ease-in 1s;
transition: background .2s linear, border-radius 1s ease-in 1s;
}

.box:hover {
background: #ff2956;
border-radius: 50%;
}
```

以下為這個範例的執行結果，你可以把滑鼠游標放在上面久一點，因為第二個屬性(圓角邊)會在1s後才延遲開始。

[](codepen://eyesofkids/JRPdXb/)

轉場特效的概念十分簡單，開始狀態、結束狀態，以及持續時間、轉場使用的貝茲曲線函式。對滑鼠滑入(hover)來說，`.box`是開始狀態，而`.box:hover`是結束狀態。但當滑鼠游標離開時，就會兩個顛倒過來。那到底`transition`該加在`.box`中還是`.box:hover`中？大部份的情況是只需要加在`.box`中，除非你希望滑鼠游標移入與離開是兩種不同的轉場特效情況，不過你需要把所有的屬性都對應好，不然會產生立即執行的失效情況。如果你只加在:hover中大概是錯誤的寫法。以下為範例:

[](codepen://eyesofkids/kkNWmL)

## 供應商前綴字(Vendor Prefixes)

供應商前綴字的出現是由於瀏覽器不同品牌的廠商，搶先於標準完成前就開始發佈已包含實作功能造成的結果。因為這些CSS屬性有可能在瀏覽器中有可能是屬於實驗性質的，所以在前面加上了瀏覽器供應商的前綴字，代表是要開啟這個實驗性的CSS屬性，到後來變成一個要為了相容不同瀏覽器的特殊寫法。而且，這不只是針對CSS3動畫相關的屬性，在一些新式的屬性，例如陰影或漸層，都有需要使用供應商前綴字的情況。由於瀏覽器新版本都自動偵測支援，現在這個問題會比較少見了。

不過，要記住哪一些屬性是需要加供應商前綴字，哪一些則不用，這是件非常令人頭痛的事情。一般都會使用一種叫Autoprefixer(自動前綴字產生器)的工具來幫忙轉換，例如下面的工具:

- 各種編輯器中的[Autoprefixer外掛功能](https://github.com/postcss/autoprefixer#text-editors-and-ide)
- [Autoprefixer CSS online](https://autoprefixer.github.io/)線上轉換工具
- [Pleeease](http://pleeease.io/play/)線上轉換工具

現在一般來說只需要加上`-webkit-`前綴字即可，例如以下的範例:

```
-webkit-transition: background .2s linear, border-radius 1s ease-in 1s;
transition: background .2s linear, border-radius 1s ease-in 1s;
```
