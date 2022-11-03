# jQuery筆記
### 網址
```
https://www.w3school.com.cn/jquery/index.asp


目前進度:
jQuery AJAX 简介
https://www.w3school.com.cn/jquery/jquery_ajax_intro.asp
```
### 在頁面載入完成的時候自動呼叫某個函式
> The $(document).ready() method allows us to execute a function when the document is fully loaded.

> 在於確保html全部load完，才開始執行js，避免js找不到html dom而發生錯誤，這種寫法等同把js寫在html之後
```
第一種(全部DOM元素下載完之後就會觸發，觸發時間較早)：
$(document).ready(function(){
  do something...
});


第二種(全部DOM元素下載完之後就會觸發，觸發時間較早)：
$(function(){
  do something...
});



Js原生寫法(網頁下載完成才會開始，包括圖片)：
window.onload = function() {
  // 在這撰寫javascript程式碼
};
```
> 除了放在head，也可放在body的尾端

> 放在body的尾端則可省略一開始的$(document).ready(function(){...});
```
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
</head>
<body>

<p>If you click on me, I will disappear.</p>
<p>Click me away!</p>
<p>Click me too!</p>

<script>
  $("p").click(function(){
    $(this).hide();
  });
</script>

</body>
</html>
```
### Selectors
#### 範例
```
//按下button後隱藏所有p標籤

$(document).ready(function(){
  $("button").click(function(){
    $("p").hide();
  });
});
```
```
$("input[name='radio02']:checked").val();  //取得選取的值


<span class="checkbox_box mr-0">
    <input id="radio02_1" type="radio" name="radio02" value="1">
    <label for="radio02_1">保單號碼</label>
</span>
												
<span class="checkbox_box mr-0">
    <input id="radio02_2" type="radio" name="radio02" value="2">
    <label for="radio02_2">強制證號</label>
</span>
```
#### 標籤種類
```
$("#test").hide();  //ID為test
$(".test")  //class為test
$("*")  //所有元素
$(this)  //當下操作的元素

$("p")  //選取<p>元素。
$("input")  //選取<input>元素。
$("p.intro")  //選取所有 class="intro" 的 <p> 元素。
$("p#demo")  //選取所有 id="demo" 的 <p> 元素。
$("#demo.intro")  //選取所有 id="demo" class="intro"的元素。

$("p:first")  //第一個 <p> 元素
$("p:last")  //最後一個 <p> 元素

$("ul li:first")  //第一個ul的第一個li標籤
$("ul li:first-child")  //所有ul的第一個li標籤
$("[href]")  //所有href連結標籤


$(":input")  //所有input元素
$(":button")  //所有 type="button" 的 <input> 元素
$(":text")  //所有type="text" 的 <input> 元素
$(":password")  //所有 type="password" 的 <input> 元素
$(":radio")  //所有 type="radio" 的 <input> 元素
$(":checkbox")  //所有 type="checkbox" 的 <input> 元素
$(":submit")  //所有 type="submit" 的 <input> 元素
$(":selected")  //所有被選取的 input 元素
$(":checked")  //所有被選中的 input 元素
$("input[type=radio][name=radio02]"")  //指定type與name
$("input[name='radio02']:checked").val();  //取得選取的值
$("input[name='password']").val()  //輸入框name為password的值


checkbox: checked
radio: checked
下拉框select: selected
```
### Events

#### click
> 單擊p標籤之後，隱藏當下的p標籤
> click事件其實是由mousedown於mouseup 2個動作構成
```
$("p").click(function(){
  $(this).hide();
});
```
#### dblclick
> 雙擊p標籤之後，隱藏當下的p標籤
```
$("p").dblclick(function(){
  $(this).hide();
});
```
#### mousedown
> 按下滑鼠時，秀出alert
```
$("#p1").mousedown(function(){
  alert("Mouse down over p1!");
});
```
#### mouseup
> 按下滑鼠釋放時，秀出alert
```
$(document).ready(function(){
  $("#p1").mouseup(function(){
    alert("Mouse up over p1!");
  });
});
```
#### mouseenter
> 滑鼠游標移至p1標籤時，秀出alert
```
$(document).ready(function(){
  $("#p1").mouseenter(function(){
    alert("You entered p1!");
  });
});
```
#### mouseleave
> 滑鼠游標移出p1標籤時，秀出alert
```
$(document).ready(function(){
  $("#p1").mouseleave(function(){
    alert("Bye! You now leave p1!");
  });
});
```
#### hover
> 結合mouseenter和mouseleave，依序觸發這兩個function
```
$(document).ready(function(){
  $("#p1").hover(function(){
    alert("You entered p1!");
  },
  function(){
    alert("Bye! You now leave p1!");
  }); 
});
```
#### mousemove
> 移動滑鼠即觸發
```
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $(document).mousemove(function(e){
    $("span").text(e.pageX + ", " + e.pageY);
  });
});
</script>
</head>
<body>
<p>鼠标位于坐标： <span></span>.</p>
</body>
</html>
```
#### focus
> 移動至目的地，點一下滑鼠即獲得焦點

#### blur
> 離開目的地，點一下滑鼠即失去焦點
```
$(document).ready(function(){
  $("input").focus(function(){
    $(this).css("background-color", "yellow");
  });
  $("input").blur(function(){
    $(this).css("background-color", "green");
  });
});
```
#### change
> 當元素的值發生改變時，會觸發 change 事件。
```
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $(".field").change(function(){
    $(this).css("background-color","#FFFFCC");
  });
});
</script>
</head>
<body>
<p>在某個區域被使用或改變時，它會改變顏色。</p>
Enter your name: <input class="field" type="text" />
<p>Car:
<select class="field" name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat">Fiat</option>
<option value="audi">Audi</option>
</select>
</p>
</body>
</html>
```
```
$(document).ready(function(){
  $('input[type=radio][name=userType]').change(function(){
    alert("change");
  });
});
```
#### keydown
> 按下鍵盤

#### keyup
> 鬆開鍵盤
```
$(document).ready(function(){
  $("input").keydown(function(){
    $("input").css("background-color","#FFFFCC");
  });
  $("input").keyup(function(){
    $("input").css("background-color","#D6D6FF");
  });
});
```
#### event.target
```
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript">

$(document).ready(function(){
  $("p, button, h1, h2").click(function(event){
    $("div").html("點擊事件由一個"+event.target.nodeName+"元素所觸發");
  });
});    

</script>
</head>

<body>
<h1>这是一个标题</h1>
<h2>这是另一个标题</h2>
<p>这是一个段落</p>
<button>这是一个按钮</button>
<p>标题、段落和按钮元素定义了一个点击事件。如果您触发了事件，下面的 div 会显示出哪个元素触发了该事件。</p>
<div></div>
</body>
</html>

```
#### on()
> 綁定多個事件可使用on()
```
第一種：
$(document).ready(function(){
  $("p").on("click", function(){
    $(this).hide();
  });
});


另一常用寫法:
$(document).ready(function(){
  $("p").click(function(){
    $(this).hide();
  });
});


第二種：
$(document).ready(function(){
  $("p").on({
    click : function(){
      $(this).hide();
    }
  });
});

//此三種寫法，產生結果相同
```
```
$(document).ready(function(){
  $("p").on({
    mouseenter : function(){
      $(this).css("background-color", "lightgray");
    },  
    mouseleave : function(){
      $(this).css("background-color", "lightblue");
    }, 
    click : function(){
      $(this).css("background-color", "yellow");
    }  
  });
});
```
#### unbind
> 移除事件處理機制
```
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $("p").click(function(){
    $(this).slideToggle();
  });
  $("button").click(function(){
    $("p").unbind();
  });
});
</script>
</head>
<body>
<p>这是一个段落。</p>
<p>这是另一个段落。</p>
<p>点击任何段落可以令其消失。包括本段落。</p>
<button>删除 p 元素的事件处理器</button>
</body>
```
### Effects
#### hide() and show()
```
$(document).ready(function(){
  $("#hide").click(function(){
    $("p").hide();
  });
  $("#show").click(function(){
    $("p").show();
  });
});
```
```
//指定隱藏速度
$(document).ready(function(){
  $("button").click(function(){
    $("p").hide(1000);
  });
});
```
#### toggle (Effect)
> 切換hide() and show()
```
$(document).ready(function(){
  $("button").click(function(){
    $("p").toggle();
  });
});
```
#### slideToggle
> 慢速切換hide() and show()

#### toggle (Event)
> 綁定多個函數
> 當指定元素被點擊時，在兩個或多個函数之間輪流切換
```
<html>
<head>
<script type="text/javascript" src="/jquery/jquery.js"></script>
<script type="text/javascript">
$(document).ready(function(){
  $("button").toggle(
  function(){
    $("body").css("background-color","yellow");
  },
  function(){
    $("body").css("background-color","red");
  },
  function(){
    $("body").css("background-color","blue");
  });
});
</script>
</head>
<body>
<button>请点击这里，来切换不同的背景颜色</button>
</body>
</html>
```
### HTML
#### 獲取與賦值
```
.text() - 設置或返回所選元素的文本内容
.html() - 設置或返回所選元素的内容（包括 HTML 標記）
.val() - 設置或返回表單字段的值
.attr() - 設置或返回屬性
.css() - 設置或返回屬性
.prop() - 設置或返回屬性(jQuery1.6新增方法，常用來設定或獲取checked、selected、disabled等屬性)

.text()、.html()、.val() = 取值
.attr("href") = 取值
.css("background-color") = 取值
.prop("checked") = 取值

.text("Hello")、html("Hello")、val("Hello") = 賦值
.attr("href","http://www.w3school.com.cn") = 賦值
.css("background-color","yellow") = 賦值
.prop("checked",true) = 賦值


attr的返回值是checked或undefined，prop的返回值只有true和false。
```
#### attr與prop區別
> attribute表示HTML文件節點的屬性，property表示JS物件的屬性
```
<body>
<!--div元素中的id、class、user-id就是div這個元素文件節點的attribute-->
<!--user-id是自定義DOM屬性-->
<div id="div1" class="class1" user-id="1"></div>
</body>

<script type="text/javascript">
// 這個obj物件中的username和age就是obj這個js物件的property
var obj = {username:"zhangsan",age:18};
</script>

attr()是JQuery 1.0版本就有的函式，prop()是JQuery 1.6版本新增加的函式。

從1.6開始，使用attr()獲取這些屬性的返回值為String型別，如果被選中(或禁用)就返回checked、selected或disabled，否則(即元素節點沒有該屬性)返回undefined。並且，在某些版本中，這些屬性值表示文件載入時的初始狀態值，即使之後更改了這些元素的選中(或禁用)狀態，對應的屬性值也不會發生改變。

若使用 .prop() 取該元素的屬性 checked 的值，則會取得布林值 true 或 false。

因此，在jQuery 1.6及以後版本中，請使用prop()函式來設定或獲取checked、selected、disabled等屬性。對於其它能夠用prop()實現的操作，也儘量使用prop()函式。
```
#### checked and disable範例
```
//取消選取
<p><input type="checkbox" checked>test</p>

$(":checkbox").attr("checked",false);

$(":checkbox").prop("checked",false);

alert($(":checkbox").attr("checked"));  //undefined

alert($(":checkbox").prop("checked"));  //false


//選取
<p><input type="checkbox">test</p>

$(":checkbox").attr("checked","checked");

$(":checkbox").prop("checked",true);

alert($(":checkbox").attr("checked"));  //checked

alert($(":checkbox").prop("checked"));  //true


//無法輸入
<p><input type="text"></p>

$("input[type=text]").attr("disabled","disabled");

$("input[type=text]").prop("disabled",true)


//可輸入
<p><input type="text" disabled></p>

$("input[type=text]").attr("disabled",false);

$("input[type=text]").prop("disabled",false)
```
####  checked 範例(Js)
```
//取消選取
<p><input type="checkbox" id="aa" checked>test</p>

document.getElementById('aa').checked = false;


//選取
<p><input type="checkbox" id="aa">test</p>

document.getElementById('aa').checked = true;

document.getElementById("aa").setAttribute("checked","checked");
```
#### checkbox取值
```
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>

$(document).ready(function(){
  $("button").click(function(){
    alert($("input:checkbox:checked").val());
  });
});
  
</script>
</head>
<body>

<p><input type=checkbox value="test1"> A</p>
<p><input type=checkbox value="test2"> B</p>
<button>press</button>

</body>
</html>
```
#### select取值
```
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>

$(document).ready(function(){
  $("button").click(function(){
    alert($("option:selected").val());
    alert($("option:selected").text());
  });
});

</script>
</head>
<body>

<p>test select
<select class="field">
<option value="volvo">VOLVO</option>
<option value="honda">HONDA</option>
<option value="toyota">TOYOTA</option>
</select>
</p>
<button>click</button>

</body>
</html>
```
#### checkbox全選&取消
```
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>

$(document).ready(function(){
  $("#yes").click(function(){
    $(":checkbox").prop("checked",true);
  }); 
   $("#no").click(function(){
    $(":checkbox").prop("checked",false);
  });
});

</script>
</head>
<body>

<input type="checkbox" value="aaa">AAA
<input type="checkbox" value="bbb">BBB
<input type="checkbox" value="ccc">CCC

<p>
<button id="yes">全選</button>
<button id="no">取消</button>
</p>

</body>
</html>
```
#### text() & html() & val()
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("#btn1").click(function(){
    $("#test1").text("Hello world!");
  });
  $("#btn2").click(function(){
    $("#test2").html("<b>Hello world!</b>");
  });
  $("#btn3").click(function(){
    $("#test3").val("Dolly Duck");
  });
});
</script>
</head>

<body>
<p id="test1">这是段落。</p>
<p id="test2">这是另一个段落。</p>
<p>Input field: <input type="text" id="test3" value="Mickey Mouse"></p>
<button id="btn1">设置文本</button>
<button id="btn2">设置 HTML</button>
<button id="btn3">设置值</button>
</body>
</html>
```
#### Js vs jQuery
```
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>
$(document).ready(function(){
  document.getElementById("btn1").addEventListener("click",function()
    {
      document.getElementById("test1").innerText = "Hello world!";
    });
});
</script>
</head>

<body>
<p id="test1">这是段落。</p>
<button id="btn1">设置文本</button>
</body>
</html>
```
```
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script>
$(document).ready(function(){
  $("#btn1").on("click",function(){
    $("#test1").text("Hello World!");
  });
});

</script>
</head>

<body>
<p id="test1">这是段落。</p>
<button id="btn1">设置文本</button>
</body>
</html>
```
#### val()
```
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    alert("Value: " + $("#test").val());
  });
});
</script>
</head>

<body>
<p>姓名：<input type="text" id="test" value="米老鼠"></p>
<button>显示值</button>
</body>

</html>
```
#### attr()
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    alert($("#w3s").attr("href"));
  });
});
</script>
</head>

<body>
<p><a href="http://www.w3school.com.cn" id="w3s">W3School.com.cn</a></p>
<button>显示 href 值</button>
</body>

</html>
```
#### 添加元素
```
append() - 在被選元素的結尾插入內容
prepend() - 在被選元素的開頭插入內容
after() - 在被選元素之後插入內容
before() - 在被選元素之前插入內容
```
#### append()
> A.append(B)的意思是將B放到A中來，後面追加

> 添加單一元素，往後面串接
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("#btn1").click(function(){
    $("p").append(" <b>Appended text</b>.");
  });

  $("#btn2").click(function(){
    $("ol").append("<li>Appended item</li>");
  });
});
</script>
</head>

<body>
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
<ol>
<li>List item 1</li>
<li>List item 2</li>
<li>List item 3</li>
</ol>
<button id="btn1">追加文本</button>
<button id="btn2">追加列表项</button>
</body>
</html>
```
>添加多個元素，往後面串接
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
function appendText()
{
var txt1="<p>Text1.</p>";              // 以 HTML 创建新元素
var txt2=$("<p></p>").text("Text2.");  // 以 jQuery 创建新元素
var txt3=document.createElement("p");
txt3.innerHTML="Text3.";               // 通过 DOM 来创建文本
$("body").append(txt1,txt2,txt3);        // 追加新元素
}
</script>
</head>
<body>

<p>This is a paragraph.</p>
<button onclick="appendText()">追加文本</button>

</body>
</html>
```
#### after()
> A.after(B)的意思是將B放到A後面去

> 添加單一元素，往下串接

#### before()
> 添加單一元素，往上串接
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("#btn1").click(function(){
    $("img").before("<b>Before</b>");
  });

  $("#btn2").click(function(){
    $("img").after("<i>After</i>");
  });
});
</script>
</head>

<body>
<img src="/i/eg_w3school.gif" alt="W3School Logo" />
<br><br>
<button id="btn1">在图片前面添加文本</button>
<button id="btn2">在图片后面添加文本</button>
</body>
</html>
```
#### 刪除元素
```
remove() - 删除被選元素（及其子元素）
empty() - 從被選元素中删除子元素
```
#### remove()
> 清空整個div元素

#### empty()
> 清空div內容，但仍保留div外框
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("#div1").remove();
  });
});
</script>
</head>

<body>

<div id="div1" style="height:100px;width:300px;border:1px solid black;background-color:yellow;">
This is some text in the div.
<p>This is a paragraph in the div.</p>
<p>This is another paragraph in the div.</p>
</div>

<br>
<button>删除 div 元素</button>

</body>
</html>
```
> 移除指定的元素
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("p").remove(".italic");
  });
});
</script>
</head>

<body>

<p>This is a paragraph in the div.</p>
<p class="italic"><i>This is another paragraph in the div.</i></p>
<p class="italic"><i>This is another paragraph in the div.</i></p>
<button>删除 class="italic" 的所有 p 元素</button>

</body>
</html>
```
#### CSS類操作
```
addClass() - 向被選元素添加一個或多個類
removeClass() - 從被選元素刪除一個或多個類
toggleClass() - 對被選元素進行添加/刪除類的切換動作
css() - 設置或返回樣式屬性
```
>1.可寫在style區塊，用addClass去添加css。2.也可直接寫在各行內style="xxx"來添加。3.用.css來添加。
```
<div id="div1" style="background-color:lightblue; border:1px solid blue;"></div>

$("div").css({"color":"red","border":"2px solid red"});
```
#### addClass()
> 向不同的元素添加 class 屬性
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>

<script>
$(document).ready(function(){
  $("button").click(function(){
    $("h1,h2,p").addClass("blue");
    $("div").addClass("important");
  });
});
</script>

<style type="text/css">
.important
{
font-weight:bold;
font-size:xx-large;
}
.blue
{
color:blue;
}
</style>
</head>

<body>
<h1>标题 1</h1>
<h2>标题 2</h2>
<p>这是一个段落。</p>
<p>这是另一个段落。</p>
<div>这是非常重要的文本！</div>
<br>
<button>向元素添加类</button>
</body>
</html>
```
#### removeClass()
> 向不同的元素移除 class 屬性
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("h1,h2,p").removeClass("blue");
  });
});
</script>
<style type="text/css">
.important
{
font-weight:bold;
font-size:xx-large;
}
.blue
{
color:blue;
}
</style>
</head>
<body>

<h1 class="blue">标题 1</h1>
<h2 class="blue">标题 2</h2>
<p class="blue">这是一个段落。</p>
<p>这是另一个段落。</p>
<br>
<button>从元素上删除类</button>
</body>
</html>
```
#### toggleClass()
> 向不同的元素切換 class 屬性
#### css()
> 返回首個匹配元素的 background-color 值
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    alert("Background color = " + $("p").css("background-color"));
  });
});
</script>
</head>

<body>
<h2>這是標題</h2>
<p style="background-color:#ff0000">這是一個段落。</p>
<p style="background-color:#00ff00">這是一個段落。</p>
<p style="background-color:#0000ff">這是一個段落。</p>
<button>返回 p 元素的背景色</button>
</body>
</html>
```
> 將為所有匹配元素設置 background-color 值
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("p").css("background-color","yellow");
  });
});
</script>
</head>

<body>
<h2>这是标题</h2>
<p style="background-color:#ff0000">这是一个段落。</p>
<p style="background-color:#00ff00">这是一个段落。</p>
<p style="background-color:#0000ff">这是一个段落。</p>
<p>这是一个段落。</p>
<button>设置 p 元素的背景色</button>
</body>
</html>
```
#### 尺寸
```
width() - 方法設置或返回元素的寬度（不包括内邊距、邊框或外邊距）。
height() - 方法設置或返回元素的高度（不包括内邊距、邊框或外邊距）。 
innerWidth() - 方法返回元素的寬度（包括内邊距）。
innerHeight() - 方法返回元素的高度（包括内邊距）。
outerWidth() - 方法返回元素的寬度（包括内邊距和邊框）。
outerHeight() - 方法返回元素的高度（包括内邊距和邊框）。
```
#### width() & height()
> 返回尺寸
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    var txt="";
    txt+="Width of div: " + $("#div1").width() + "</br>";
    txt+="Height of div: " + $("#div1").height();
    $("#div1").html(txt);
  });
});
</script>
</head>
<body>

<div id="div1" style="height:100px;width:300px;padding:10px;margin:3px;border:1px solid blue;background-color:lightblue;"></div>
<br>
<button>显示 div 的尺寸</button>
<p>width() - 返回元素的宽度。</p>
<p>height() - 返回元素的高度。</p>

</body>
</html>
```
> 調整尺寸
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("button").click(function(){
    $("#div1").width(320).height(320);
  });
});
</script>
</head>
<body>

<div id="div1" style="height:100px;width:300px;padding:10px;margin:3px;border:1px solid blue;background-color:lightblue;"></div>
<br>
<button>调整 div 的尺寸</button>

</body>
</html>
```
### 遍歷
#### 祖先
```
parent() - 方法返回被選元素的直接父元素。
parents() - 方法返回被選元素的所有祖先元素，它一路向上直到文檔的根元素 (<html>)。
parentsUntil() - 方法返回介於兩個给定元素之間的所有祖先元素。
```
#### parent()
```
<!DOCTYPE html>
<html>
<head>
<style>
.ancestors *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("span").parent().css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body>

<div class="ancestors">
  <div style="width:500px;">div (曾祖父)
    <ul>ul (祖父)  
      <li>li (直接父)                //變色
        <span>span</span>
      </li>
    </ul>   
  </div>

  <div style="width:500px;">div (祖父)   
    <p>p (直接父)                   //變色
        <span>span</span>
      </p> 
  </div>
</div>

</body>
</html>
```
#### parentsUntil()
> 返回介於 span 與 div 元素之間的所有祖先元素
```
<!DOCTYPE html>
<html>
<head>
<style>
.ancestors *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("span").parentsUntil("div").css({"color":"red","border":"2px solid red"});
});
</script>
</head>

<body class="ancestors"> body (曾曾祖父)
  <div style="width:500px;">div (曾祖父)
    <ul>ul (祖父)              //變色
      <li>li (直接父)          //變色
        <span>span</span>
      </li>
    </ul>   
  </div>
</body>

</html>
```
#### 後代
```
children() - 返回被选元素的所有直接子元素。
find() - 返回指定選取的元素。
```
#### children()
```
<!DOCTYPE html>
<html>
<head>
<style>
.descendants *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("div").children().css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body>

<div class="descendants" style="width:500px;">div (当前元素) 
  <p>p (子)                  //變色
    <span>span (孙)</span>     
  </p>
  <p>p (child)              //變色
    <span>span (孙)</span>
  </p> 
</div>

</body>
</html>
```
> 指定class = 1的子元素
```
<!DOCTYPE html>
<html>
<head>
<style>
.descendants *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("div").children("p.1").css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body>

<div class="descendants" style="width:500px;">div (当前元素) 
  <p class="1">p (子)       //變色
    <span>span (孙)</span>     
  </p>
  <p class="2">p (子)
    <span>span (孙)</span>
  </p> 
</div>

</body>
</html>
```
#### find()
> 方法返回被選元素的後代元素，一路向下直到最後一個後代。

> 下面的例子返回屬於 div 後代的所有 span 元素
```
<!DOCTYPE html>
<html>
<head>
<style>
.descendants *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("div").find("span").css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body>

<div class="descendants" style="width:500px;">div (current element) 
  <p>p (子)
    <span>span (孙)</span>     //變色
  </p>
  <p>p (child)
    <span>span (孙)</span>     //變色
  </p> 
</div>

</body>
</html>
```
```
<!DOCTYPE html>
<html>
<head>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
<style>
.descendants *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>

<script>
$(document).ready(function(){
  $("button").click(function(){  
    $("div").find("*").css({"color":"red","border":"2px solid red"});
  });
});
</script>
</head>
<body>

<div class="descendants" style="width:500px;">div (当前元素) 
  <p>p (子)
    <span>span (孙)</span>     
  </p>
  <p>p (child)
    <span>span (孙)</span>
  </p> 
</div>

<button>Click</button>

</body>
</html>
```
#### 同胞
```
siblings() - 方法返回被選元素的所有同一層同胞元素。
next() - 方法返回被選元素的下一個同胞元素。
nextAll() - 方法返回被選元素的所有跟随的同胞元素。
nextUntil() - 方法返回介於兩個給定參數之前的所有跟隨的同胞元素。
prev()
prevAll()
prevUntil()
```
#### siblings()
```
<!DOCTYPE html>
<html>
<head>
<style>
.siblings *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("h2").siblings().css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body class="siblings">

<div>div (父)
  <p>p</p>             //變色
  <span>span</span>    //變色
  <h2>h2</h2>
  <h3>h3</h3>          //變色
  <p>p</p>             //變色
</div>

</body>
</html>
```
```
<!DOCTYPE html>
<html>
<head>
<style>
.siblings *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("h2").siblings("p").css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body class="siblings">

<div>div (父)
  <p>p</p>           //變色
  <span>span</span>
  <h2>h2</h2>
  <h3>h3</h3>
  <p>p</p>           //變色
</div>

</body>
</html>
```
#### next()
```
<!DOCTYPE html>
<html>
<head>
<style>
.siblings *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("h2").next().css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body class="siblings">

<div>div (父)
  <p>p</p>
  <span>span</span>
  <h2>h2</h2>
  <h3>h3</h3>   //變色
  <p>p</p>
</div>

</body>
</html>
```
#### nextAll()
```
<!DOCTYPE html>
<html>
<head>
<style>
.siblings *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("h2").nextAll().css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body class="siblings">

<div>div (父)
  <p>p</p>
  <span>span</span>
  <h2>h2</h2>
  <h3>h3</h3>    //變色
  <p>p</p>       //變色
</div>

</body>
</html>
```
#### nextUntil()
```
<!DOCTYPE html>
<html>
<head>
<style>
.siblings *
{ 
display: block;
border: 2px solid lightgrey;
color: lightgrey;
padding: 5px;
margin: 15px;
}
</style>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("h2").nextUntil("h6").css({"color":"red","border":"2px solid red"});
});
</script>
</head>
<body class="siblings">

<div>div (父)
  <p>p</p>
  <span>span</span>
  <h2>h2</h2>
  <h3>h3</h3>  //變色
  <h4>h4</h4>  //變色
  <h5>h5</h5>  //變色
  <h6>h6</h6>
  <p>p</p>
</div>

</body>
</html>
```
#### 過濾
```
first - 方法返回被選元素的首個元素。
last() - 方法返回被選元素的最後一個元素。
eq() - 方法返回被選元素中帶有指定索引號的元素。
filter() - 方法返回匹配的元素。
not() - 返回不匹配的元素。
```
#### first()
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("div p").first().css("background-color","yellow");
});
</script>
</head>
<body>

<h1>欢迎来到我的主页</h1>
<div>
<p>这是 div 中的一个段落。</p>  //變色
</div>

<div>
<p>这是 div 中的另一个段落。</p>
</div>

<p>这也是段落。</p>

</body>
</html>

```
#### eq()
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("p").eq(1).css("background-color","yellow");
});
</script>
</head>
<body>

<h1>欢迎来到我的主页</h1>
<p>我是唐老鸭 (index 0)。</p>
<p>唐老鸭 (index 1)。</p>   //變色
<p>我住在 Duckburg (index 2)。</p>
<p>我最好的朋友是米老鼠 (index 3)。</p>

</body>
</html>
```
#### filter
```
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js">
</script>
<script>
$(document).ready(function(){
  $("p").filter(".intro").css("background-color","yellow");
});
</script>
</head>
<body>

<h1>欢迎来到我的主页</h1>
<p>我是唐老鸭。</p>
<p class="intro">我住在 Duckburg。</p>  //變色
<p class="intro">我爱 Duckburg。</p>   //變色
<p>我最好的朋友是 Mickey。</p>

</body>
</html>
```
### Ajax




### others
#### Js vs jQuery (Attribute & attr)
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <script src="http://libs.baidu.com/jquery/2.0.0/jquery.min.js"></script>
  </head>
  <body>
    <div class="test" custom="hello"></div>
    <div class="test" custom="hi"></div>
    <script type="text/javascript">
    
      var div = document.getElementsByClassName("test");
      alert(div[1].getAttribute("custom"));

      for (var i = 0; i < div.length; i++) {
        alert(div[i].getAttribute("custom"));
      }

=============================================================

      var div = $(".test");
      alert(div.eq(1).attr("custom"));

      var div = $(".test");
      for (var i = 0; i < div.length; i++) {
        alert(div.eq(i).attr("custom"));
      }
    </script>
  </body>
</html>

```
#### onclick (on + 事件名)
```
對 HTML 元素來說，只要支援某個「事件」的觸發，就可以透過 on+事件名 的屬性來註冊事件：

<button id="btn" onclick="console.log('HI');">Click</button>

如同上面範例，透過 onclick 屬性，我們就可以在 <button> 元素上面註冊 click 事件，換句話說，當我按下這個 <button> 元素時，就會執行 console.log('HI'); 的程式碼。
```
```
<button onclick="myhref()">Redirect</button>
<input type="button" onclick="myhref()" value="Redirect">

<button onclick="alert('123')">click</button>
<input type="button" onclick="alert('123')" value="click">

<p onclick="alert('123')">test</p>
<p onclick="$(this).hide();">test</p>
<p onmouseover="$(this).hide();">test</p>

<button onclick="alert('123')">click</button>
<input type="button" onclick="alert('123')" value="click">
```
> 此兩種寫法結果會相同
```
$(function(){
  $("button").click(function(){
    appendText();
  });
});

<button>追加文本</button> 
```
```
<button onclick="appendText()">追加文本</button>
```
