# CSS3動畫(animations)

如果你已經有一些CSS3轉場的基礎，可以很快的掌握CSS3動畫(animations)的部份，它有部份的屬性與CSS3轉場類似。

## 動畫的基礎定義

動畫的這三個屬性，持續期間、時間函式與延遲開始時間，這部份的內容與CSS3轉場一模一樣:

- animation-duration: 持續期間。時間通常以`s`為單位(秒)，可以定義小數點例如`0.5s`或`.5s`，預設值是`0s`。
- animation-timing-function: 時間函式，這是用來設定轉場過程時所使用的貝茲曲線，預設值是`ease`。
- animation-delay: 延遲開始時間。時間通常以`s`為單位(秒)，可以定義小數點例如`0.5s`或`.5s`，預設值是`0s`。

但與轉場不同的是，轉場使用的第1個屬性是用`transition-property`直接定義要進行轉場的屬性，而動畫是使用`animation-name`定義一組名稱。

這個名稱是對應到關鍵影格`@keyframes`的規則(rule)的名稱，一個最簡單的`@keyframes`規則如下，`0%`代表第一個關鍵影格，也就是開始的狀態，也可以使用`from`代表。`100%`則是最後一個關鍵影格，結束的狀態，也可以使用`to`代表，中間的部份依照不同的時期可以用百分比來表示，這是依照你的持續時間來分割的:

```css
@keyframes pinpon {
  0% {
    left: 0;
    top: 0;
  }
  50% {
    left: 200px;
    top: 150px;
  }
  100% {
    left: 300px;
    top: 0;
  }
}
```

對照的CSS3其他定義值如下，可以看到這裡的`animation-name`指定為上面的"pinpon"關鍵影格名稱:

```
  animation-name: pinpon;
  animation-duration: 3s;
  animation-timing-function: ease-in;
  animation-delay: 1s;
```

下面是這個範例的執行結果，它是一載入頁面立即執行的，如果看不到請重新載入範例的頁面。這是動畫的特性，不過也有另外可以讓它用類似轉場的觸發方式來執行，後面會再提到。

[](codepen://eyesofkids/JRPGqX/)

## 其他更多的屬性

動畫還有其他一些不同的屬性可以進行定義，以下列出來:

- `animation-iteration-count`(播放循環次數): 用於設定動畫播放次數，預設是1，可以設定正整數，例如5。或帶有小數點的小數，例如0.5代表播放半次。`infinite`代表永不停止的播放。

- `animation-direction`(播放方向): 用於定義播放的方向，有以下幾種值可以使用:

  - normal(正常)
  - reverse(反向/倒帶)
  - alternate(輪流)
  - alternate-reverse(輪流與反向)

運用這兩個屬性，可以把上面的範例再調整一下，讓球的運動可以來回不斷的跳動，例如以下的範例:

[](codepen://eyesofkids/BLBKKO/)


- `animation-fill-mode`(播放後樣式): 指的是動畫播放後的樣式，是不是要保留在最後的狀態。預設值是`none`，設定為`forwards`會停留在最後的樣式，`backwards`則是一開始的樣式。`both`是兩者都套用。這個值會因為`animation-direction`屬性的方向值而有不同的套用對象。

下面的範例是使用`forwards`來指定，最後會停留在最後套用的樣式。

[](codepen://eyesofkids/GjKkWd/)

- `animation-play-state`(播放狀態): 這個屬性可以控制動畫播放的暫停，預設是`running`，可以設為`paused`來暫停播放。

下面的範例是使用`:hover`加上`paused`，滑鼠游標放在球上面，動畫就會暫停，游標移出後又會繼續。

[](codepen://eyesofkids/kkNbGr/)

## 簡寫語法(整合語法)

由於animation的屬性有8個之多，要使用簡寫的方式把所有的屬性寫成一行會比較不容易。以下列出所有的屬性順序與其預設值:

```
animation-name: none
animation-duration: 0s
animation-timing-function: ease
animation-delay: 0s
animation-iteration-count: 1
animation-direction: normal
animation-fill-mode: none
animation-play-state: running
```

> 順序口訣: 名詞支援次方"填充""狀態" - 名稱、持續、貝茲、延遲、次數、方向、填充(最後樣式)、狀態(暫停/執行)

在簡寫語法中，名稱(animation-name)可以放在第一個值，也可以放在最後一個值，例如像下面這些寫法中的`slidein`實際上是`@keyframes`的規則的名稱:

```
/* @keyframes duration | timing-function | delay |
   iteration-count | direction | fill-mode | play-state | name */
  animation: 3s ease-in 1s 2 reverse both paused slidein;

/* @keyframes duration | timing-function | delay | name */
  animation: 3s linear 1s slidein;

/* @keyframes duration | name */
  animation: 3s slidein;
```

## 供應商前綴字(Vendor Prefixes)

與轉場相同，CSS3動畫屬性也有供應商前綴字的問題，現在一般來說只需要加上`-webkit-`前綴字即可。可以使用以下的工具來協助加上:

- 各種編輯器中的[Autoprefixer外掛功能](https://github.com/postcss/autoprefixer#text-editors-and-ide)
- [Autoprefixer CSS online](https://autoprefixer.github.io/)線上轉換工具
- [Pleeease](http://pleeease.io/play/)線上轉換工具

## 使用`:hover`來觸發動畫

下面的範例可以用一個外圍的div元素來框住進行CSS3動畫的球元素，讓它在滑鼠游標移入在上面時才開始進行動畫，按住滑鼠右鍵時可以暫停動畫。但你應該發現不論如何，使用CSS3動畫是無法在播放期間直接中止的。

[](codepen://eyesofkids/JRPXBy/)
