## 變形(transform) 3D基本使用

變形的3D應用是以2D為基礎知識，所以你會發現幾乎所有的變形函式的名稱都差不多。

## perspective屬性

實際上螢幕上只有2維，3維是模擬出來的效果。也就是以2次元模擬出3次元的形狀。3D相較於2D多了一個Z軸的數值。基礎的3D的三個軸，X軸是螢幕上的水平座標軸，Y軸是垂直座標軸，Z軸則是由螢幕射出的另一個虛擬的座標軸，它代表的是DOM元素(或物件)的遠近距離。負值的Z軸數值是比原先的元素還愈遠，也就是愈小，正值代表愈近，也就是愈大。

`perspective`中文是"透視"的意思，在3D設計中是一個重要的屬性，它代表了Z軸為0(z=0)到觀看者的距離(也可以稱為深度)，以這個觀測距離來決定物件的大小(遠近)情況，當超過這個觀測距離，DOM元素(物件)將會不可見。根據[這份資料](https://developer.apple.com/library/safari/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Using2Dand3DTransforms/Using2Dand3DTransforms.html)的說明，`perspective`設定為300px或更少時，會有強烈的失真，500px到1000px的失真較為中等，2000px以上的失真就很輕微。

一般來說，我們會在要進行3D變形的外層容器元素來定義`perspective`，這樣包含在其內的子元素(物件)都可以按照這個深度來進行變形。`perspective`的設定方式有兩種，一種是直接定義`perspective`屬性:

```
perspective: 500px;
```

另一種是定義在transform中，以類似函式的方式來定義數值:

```
transform: perspective(250px);
```

一個使用`rotateX`旋轉正45度的範例如下，你可以增加或減少`perspective`的數值來觀察變形的情況:

[](codepen://eyesofkids/ozvavz?height=500)

https://drafts.csswg.org/css-transforms/#perspective

https://developer.apple.com/library/safari/documentation/InternetWeb/Conceptual/SafariVisualEffectsProgGuide/Using2Dand3DTransforms/Using2Dand3DTransforms.html

http://www.slideshare.net/kswlee/css3-2d3d-transform

https://www.git-tower.com/blog/css3-transforms/

https://dev.opera.com/articles/understanding-3d-transforms/#perspective

以下為最簡單的兩種範例:

下面是使用`perspective`(透視)加上`translateZ`(以Z軸平移)的範例，你可以看到當移動的長度為負數與正數的差異。

[](codepen://eyesofkids/WGZraq)

下面是使用`perspective`(透視)加上`rotateX`、`rotateY`與`rotateZ`(以各軸旋轉)的範例。

[](codepen://eyesofkids/ALAVgX)

觀測者的原點是可以用另一個屬性`perspective-origin`來改變，稱之為透視原點或消失點(vanishing point, 到最遠處消失的那個點)，這個屬性可以使用X軸與Y軸的長度數值或百分比(原點為0%)，或是像或是用top/center/bottom、left/center/right等組合來直接定義新的位置，正中央為50%，數值是center。`perspective-origin`與`perspective`合併可以形成透視矩陣(perspective matrix)。

https://www.smashingmagazine.com/2016/07/front-end-challenge-accepted-css-3d-cube/

要進一步講解3D的特性需要先畫出一個cube(正方體, 骰子)，比較容易理解。我們用變形函式中的rotate與translate搭配，可以先畫出一個正方體。

HTML碼的基本結構如下，`scene`是一個場景，`cube`則是在這個場景中的正方體，一個正方體有6個面，也就是6個2D的區塊，分別以前後上下左右來區分:

```html
<div class="scene">
  <div  class="cube">
    <div class="front">前</div>
    <div class="back">後</div>
    <div class="top">上</div>
    <div class="bottom">下</div>
    <div class="left">左</div>
    <div class="right">右</div>
  </div>
</div>
```

每一面的CSS共同的屬性定義如下，我們定義它為200x200像素的大小，並可在裡面呈現置中的文字，文字的顏色、大小等等定義。其中有一個屬性`backface-visibility`，它可以控制要不要看到被擋住的那些面，可以使用`visible`與`hidden`，預設是看不到被擋住的面也就是`hidden`。這裡的範例是使用`visible`，讓我們能透視看得到被擋住的面:

```css
.cube div {
  display: block;
  position: absolute;
  width: 200px;
  height: 200px;
  line-height: 200px;
  font-size: 40px;
  color: white;
  text-align: center;
  backface-visibility: visible;
}
```

前面(front)與後面(back)的定義最為簡單，除了各自的顏色外，前面(front)即是由Z軸向外(向使用者)突出100px，100px即是整個正方體邊長200px的一半。後面(back)則是再加上以Y軸為準旋轉180度的變形即可。

```css
.front {
  background: rgba(0, 0, 0, 0.4);
  transform: translateZ(100px);
}

.back {
  background: rgba(0, 255, 0, 1);
  transform: rotateY(180deg) translateZ(100px);
}
```

再來是上面(top)與下面(bottom)，除了以Z軸平移100px外，加上以X軸為準的旋轉90度與-90度就完成了。

```css
.top {
  background: rgba(196, 0, 0, 0.7);
  transform: rotateX(90deg) translateZ(100px);
}

.bottom {
  background: rgba(196, 0, 196, 0.7);
  transform: rotateX(-90deg) translateZ(100px);
}
```

左面(left)與右面(right)，除了以Z軸平移100px外，再加上以Y軸為準旋轉90度與-90度的變形即可，這與背面(back)有點類似。

```css
.left {
  background: rgba(0, 0, 196, 0.7);
  transform: rotateY(-90deg) translateZ(100px);
}

.right {
  background: rgba(196, 196, 0, 0.7);
  transform: rotateY(90deg) translateZ(100px);
}
```

再回到`.cube`的定義中，只有設定一個`transform-style`屬性，這個屬性代表它的子元素要使用3D的方式來進行位置指示。只有`preserve-3d`與`flat`兩種值可用，預設是flat，也就是平面(平坦)的意思。

```css
.cube {
  transform-style: preserve-3d;
}
```

最上層的`scene`是我們要用的場景類別，它的CSS定義如下，除了定義固定的寬與高之外，另外定義了`perspective`與`perspective-origin`兩個屬性:

```css
.scene {
  width: 200px;
  height: 200px;
  margin: 50px 0 0 50px;

  perspective: 800px;
  perspective-origin: 50% -150px;
}
```

`perspective`如同上面所說的，是透視的深度，與z=0之間的距離。`perspective-origin`則是透視原點(或消失點)，這裡是使用中心點(50%)與向上偏移150px。

最後的範例結果如下，因為要讓它看起來像是個正方體，我加上了以Y軸旋轉的CSS3動畫:

[](codepen://eyesofkids/VKkXmE?height=500)

這幾個屬性的用法都可以在正方體中看到。花點時間調整一下其中的數值應該很容易理解。
