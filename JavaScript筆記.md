# JavaScript筆記
### 網址
```
https://www.w3school.com.cn/js/index.asp
目前進度: 0

http://www.w3big.com/zh-TW/js/js-output.html#gsc.tab=0
```
### JavaScript 顯示數據
> JavaScript 可以通過不同的方式來輸出數據
```
#使用window.alert()彈出警告框。(省略為alert)
#使用document.write()方法將內容寫到HTML文檔中。
#使用innerHTML寫入到HTML元素。
#使用console.log()寫入到瀏覽器的控制台。
```
#### document.write() 直接輸出在頁面上
> 1.請使用document.write() 僅僅向文檔輸出寫內容。

> 2.如果在文檔已完成加載後執行document.write，整個HTML 頁面將被覆蓋。

1.僅多了一行時間
```
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>本教程(w3big.com)</title> 
</head>
<body>
	
<h1>我的第一个 Web 页面</h1>
<p>我的第一个段落。</p>
<script>
document.write(Date());
</script>
	
</body>
</html>
```
2.整個頁面會被取代掉，只剩時間
```
<!DOCTYPE html>
<html>
<head> 
<meta charset="utf-8"> 
<title>本教程(w3big.com)</title> 
</head>
<body>
	
<h1>我的第一个 Web 页面</h1>
<p>我的第一个段落。</p>
<button onclick="myFunction()">点我</button>
<script>
function myFunction() 
{
    document.write(Date());
}
</script>
	
</body>
</html>	
```

#### 外部的JavaScript
```
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
</body>
</html>
```

#### 抓取元素範例

```
document.getElementById("demo").style.color="red";

document.getElementById("demo").innerText="test";

document.getElementById("demo").innerHTML = "test";
```
### 對象
#### 建立對象並存取
> 兩種存取方式
```
1.objectName.propertyName

2.objectName["propertyName"]
```
```
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript Objects</h2>

<p>There are two different ways to access an object property.</p>

<p>You can use person.property or person["property"].</p>

<p id="demo"></p>

<script>
// Create an object:
const person = {
  firstName: "John",
  lastName : "Doe",
  id     :  5566
};

// Type1
document.getElementById("demo").innerHTML =
person.firstName + " " + person.lastName;
</script>

// Type2
document.getElementById("demo").innerHTML =
person["firstName"] + " " + person["lastName"];

</body>
</html>
```
```
John Doe
```
#### 建立內含function對象
```
<!DOCTYPE html>
<html>
<body>

<h2>JavaScript Objects</h2>
<p>An object method is a function definition, stored as a property value.</p>

<p id="demo"></p>

<script>
// Create an object:
const person = {
  firstName: "John",
  lastName: "Doe",
  id: 5566,
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
};

// Display data from the object:
document.getElementById("demo").innerHTML = person.fullName();
</script>

</body>
</html>
```
```
John Doe
```
### 事件



### 標準函式 & 匿名函式
* 標準函式
```
//函式定義 - 使用有名稱的函式
function sum(a, b){
    return a+b
}
```
* 匿名函式
```
//函式表達式 - 常數指定為匿名函式
const sum = function(a, b) {
    return a+b
}
```
* ES6箭頭匿名函式(Arrow Function)
```
const sum = (a, b) =>  a + b
```
* 呼叫使用
```
const newValue = sum(100,0)
```
### 以函式作為傳入參數
```
const addOne = function(value){
    return value + 1
}

const addOneAndTwo = function(value, fn){
    return fn(value) + 2
}

console.log(addOneAndTwo(10, addOne)) //13
```