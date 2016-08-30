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

轉場特效使用四個CSS屬性來進行定義，這些屬性可以合併到一個`transition`屬性之中:

- transition-property: 定義哪些CSS屬性會被轉場效果影響。除了這些被指定的屬性，其他的轉場一如以往的會在瞬間完成。要特別注意的是，並非所有的CSS屬性都可以進行轉場，可用的屬性所有清單在[這份資料](http://oli.jp/2010/css-animatable-properties/)與[可進行動畫的屬性](https://www.w3.org/TR/2009/WD-css3-transitions-20091201/#animatable-properties-)，其中也包含了SVG的屬性。如果這個屬性定義為`transform`，代表任何使用了`transform`的屬性都會被偵測來進行動畫。如果這個屬性定義為`all`，就會自動偵測所有可進行動畫的屬性，包含`transform`影響的屬性。預設值就是`all`。

- transition-duration: 定義轉場的持續時間。可以只定義一個時間給所有屬性使用，也可以分別給定不同時間。時間通常以`s`為單位(秒)，可以定義小數點例如`0.5s`或`.5s`，預設值是`0s`。

- transition-timing-function: 設定轉場時所依據的貝茲曲線。內建的幾個數值如下:

  - ease
  - linear
  - ease-in
  - ease-out
  - ease-in-out
  - step-start
  - step-end
  - steps()
  - cubic-bezier()

其中`cubic-bezier()`的數值，可以到[cubic-bezier.com](http://cubic-bezier.com/)來自訂所需要的貝茲曲線參數值。預設值是`ease-in`。


- transition-delay: 定義多久之後開始發生轉場，這是一個延遲開始的時間。時間通常以`s`為單位(秒)，可以定義小數點例如`0.5s`，預設值是`0s`。

合併寫法是按照上面的依順寫成一行，所以如果都是以預設值來寫CSS定義的話，會看到非常簡單的寫法像這樣:

```
transition: .5s;
```

相當於下面這樣，`.5s`代表的是持續期間(duration)，而且因為最後面的那個延遲開始(delay)的預設值是0s，一般都不寫:

```
transition: all .5s ease-in;
```

你可以為每個不同的CSS屬性分別設定轉場的動畫定義:

```css
.box {
background: #2db34a;
border-radius: 6px;
height: 95px;
width: 95px;
transition: background .2s linear, border-radius 1s ease-in 1s;

}

.box:hover {
background: #ff2956;
border-radius: 50%;
}
```

以下為這個範例的執行結果，你可以把滑鼠游標放在上面久一點，因為第二個屬性(圓角邊)會在1s後才延遲開始。

[](codepen://eyesofkids/JRPdXb/)
