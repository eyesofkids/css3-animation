## 變形(transform) 3D基本使用

變形的3D應用是以2D為基礎知識，所以你會發現幾乎所有的變形函式的名稱都差不多。

## perspective屬性

實際上螢幕上只有2維，3維是模擬出來的效果。也就是以2次元模擬出3次元的形狀。3D相較於2D多了一個Z軸的數值。基礎的3D的三個軸，X軸是螢幕上的水平座標軸，Y軸是垂直座標軸，Z軸則是由螢幕射出的另一個虛擬的座標軸，它代表的是DOM元素(或物件)的遠近距離。負值的Z軸數值是比原先的元素還愈遠，也就是愈小，正值代表愈近，也就是愈大。

`perspective`中文是"透視"的意思，在3D設計中是一個重要的屬性，它代表了Z軸為0(z=0)到使用者(觀看者)的距離(也可以稱為深度)，以這個觀測距離來決定物件的大小(遠近)情況，當超過這個觀測距離，DOM元素(物件)將會不可見。以下為最簡單的兩種範例:

下面是使用`perspective`(透視)加上`translateZ`(以Z軸平移)的範例，你可以看到當移動的長度為負數與正數的差異。

[](codepen://eyesofkids/WGZraq)

下面是使用`perspective`(透視)加上`rotateX`、`rotateY`與`rotateZ`(以各軸旋轉)的範例。

[](codepen://eyesofkids/ALAVgX)

觀測者的原點是可以用另一個屬性`perspective-origin`來改變，稱之為透視原點或消失點(vanishing point)，這個屬性可以使用X軸與Y軸的偏移量，或是像或是用top/bottom、left/right等組合來直接定義新的位置。Z軸的原點則是永遠都是在螢幕的位置，要藉由`perspective`來移動觀測者的位置。

要講解3D的特性需要先畫出一個cube(正方體, 骰子)，比較容易理解。我們用變形函式中的rotate與translate搭配，可以先畫出一個正方體。




- perspective
- perspective-origin
- transform-style


http://www.w3cplus.com/css3/css3-3d-transform.html
http://css3.bradshawenterprises.com/transforms/#css3dtransforms
