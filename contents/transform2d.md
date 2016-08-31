## 變形(transform) 2D基本使用

以下以CSS3轉場的動畫效果來配合變形(transform)使用，作為教學的範例。

### 縮放比例(scale)

縮放比例(scale)是指對大小比例進行放大或縮小，數值為正數，例如2代表2倍大，0.5代表一半大小。變形模組中提供了三種函式可供使用，分別為:

- `scale( <number> [, <number> ]? )`: 根據提供的數字值進行放大或縮小，只提供一個數字時X軸與Y軸使用相同的比例。2代表2倍大，0.5代表一半大小。
- `scaleX( <number> )`: 根據提供的數字值進行X軸放大或縮小。
- `scaleY( <number> )`: 根據提供的數字值進行Y軸放大或縮小。

範例:

[](codepen://eyesofkids/xEKOWa)

### 旋轉(rotate)

旋轉(rotate)是將目前的DOM元素或物件進行正時針方向或逆時針方向的旋轉動作。使用的數值是代表正時針方向的正整數角度值，或是代表逆時針方向的負整數值，例如`90deg`代表正90度旋轉，`-90deg`代表逆90度旋轉，超過360度代表轉過一圈再繼續旋轉。

範例:

[](codepen://eyesofkids/jrNAXw)

> 註: 另外有rotateX、rotateY、rotateZ與rotate3d函式，這幾個都是3D的變形使用的。

### 平移(translate)

平移(translate)將目前的DOM元素或物件進行X軸或Y軸的移動，也就是左/右、上/下的移動。數值可以使用CSS中的正負長度數值(px, em, in)，或是百分比。變形模組中提供了三種函式可供使用，分別為:

- translate( <length> | <percentage> [, <length> | <percentage> ]? )
- translateX( <length> | <percentage> )
- translateY( <length> | <percentage> )

範例:

[](codepen://eyesofkids/ORLXGX)


### 傾斜(skew)

傾斜(skew)將目前的DOM元素或物件進行X軸或Y軸以某個角度進行傾斜，角度也是使用正負數後面加上`deg`來代表。

- skew( <angle> [, <angle> ]? )
- skewX( <angle> )
- skewY( <angle> )

範例:

[](codepen://eyesofkids/QKLEZr)

### 矩陣(matrix)

矩陣(matrix)是把6種變形函式組合成一個矩陣進行的變形組合。不是很容易在沒有使用工具的情況下使用。

### 變形原點(transform-origin)

在進行變形時，預設的變形原點都是物件或DOM元素的中心點，用變形原點(transform-origin)可以改變變型的基準點，例如作旋轉變形時可以依照不同的原點位置來進行旋轉。改變原點對於旋轉與縮放會比較明顯看得出不同。

變形原點(transform-origin)可以用正負數值來代表對原來原點的偏移量(X軸偏移量與Y軸偏移量)，或是用top/bottom、left/right等組合來直接定義新的位置。

範例，注意變形原點是在`.box`類別中定義，而不是`:hover`裡:

[](codepen://eyesofkids/YGKGXP)

### 組合語法

單純使用`transform`可以一次套用多個變形函式，例如:

```
transform: rotate(45deg) translateX(200px);
```
