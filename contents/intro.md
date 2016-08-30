# 介紹

新式的CSS3中就已經有包含動畫的可定義值，內容相當的完整。CSS動畫指的是使用以CSS定義為主的動畫效果，又可以分成以下兩類:

- CSS轉場/過渡(transitions): 主要以開始狀態、結束狀態與持續期間(duration)三種參數，以及可指定的漸變函數(transition timing function)，將DOM元素或網頁上的物件進行轉變。

- CSS動畫(animations): 又稱為關鍵影格(Keyframe)動畫，可以加入關鍵影格，提供許多動畫片段的組合。

CSS動畫相較於使用JavaScript為主的動畫有一些好處:

- 簡單，對於一些簡單的動畫特效，不需要使用到程式語言就可以製作出動畫。
- 低消費，對於資源的消耗非常低。
- 最佳化，瀏覽器對於CSS動畫可以提供最佳化。

CSS轉場(transitions)與CSS動畫(animations)有一些相同之處:

- 都是使用CSS定義，然後監聽DOM元素的改變作出動畫效果
- 都可以設定漸變函數(transition timing function)，控制動畫的運動(效果展現)的曲線
- 都可以設定持續期間(duration)，控制動畫持續的時間
- 都有對應的event(事件)，可以送出動畫的狀態，可讓JavaScript再加以監聽或控制(可程式化)
- 都可以用視覺化方式看到CSS屬性正在改變的狀態

## CSS轉場(transitions)與CSS動畫(animations)的不同之處

### 觸發(Trigger)方式不同

轉場(transitions)觸發使用`:hover`僞(pseudo)類別為最經常使用，其他可觸發的還有`:active`、`:focus`、`:checked`等等，另一種方式是使用JavaScript語言動態加入或移除CSS類別，更多範例可以參考[這一篇範例](https://www.impressivewebs.com/css3-transitions-without-hover/)。

動畫(animations)不需要觸發，當你定義好就會開始進行動畫。

### 循環/重覆播放(Looping)

轉場(transitions)沒有指定循環播放的屬性可用。

動畫(animations)有`animation-iteration-count`屬性可指定循環播放的次數，或是用"infinite"指定為不斷重覆播放。

### 定義關鍵影格(Keyframes)/中途點

轉場(transitions)沒有這特性。動畫的撥放就是從開始到結束。

動畫(animations)可以額外定義關鍵影格(Keyframes)，可以製作更複雜的動畫效果。

> 註: 有一個常會搞混的`transform`的CSS的新屬性，它可以把網頁上的物件或元素進行變形、翻轉或2d與3d的效果，它並不是與動畫有關的屬性，你可以把它當成是類似字體顏色大小、透明度(opacity)的屬性。也可以搭配CSS動畫來使用。

### 搭配JavaScript互動的混合作法

轉場(transitions)很容易可以搭配JavaScript程式作額外的互動應用。

動畫(animations)比較不容易，但仍然是可以搭配JavaScript使用。
