# Vue.js 手牽手
### 網址
```
https://ithelp.ithome.com.tw/users/20129072/ironman/3052


目前進度:
2020it邦鐵人賽-30天手把手的Vue.js教學 Day11 - 認識Vue Components
https://ithelp.ithome.com.tw/articles/10242042
```

### 簡介
```
Vue是一個MVVM框架，M(資料) V(畫面) VM(ViewModel=Vue)。

VM是中介者負責牽起資料&畫面，資料綁定的概念。
```

### 編輯器 & 外掛設定

#### 主工具
```
1. VS Code 
2. Vue.js devtools
3. node.js
```

#### VS Code外掛
```
1. cdnjs
2. Live Server
3. Prettier
4. Vetur
```
```
nvm = node version manager = 控管電腦上不同的node.js版本
```

### jQuery資料綁定 vs Vue資料綁定
> 差別在Vue可直接更改畫面資料，jQuery必須分兩個動作。
```
Vue:
data.title = 'Alex宅幹嘛'


jQuery:
data.title = 'Alex宅幹嘛'
$('.title > h1').text(data.title);
```
#### jQuery資料綁定
```
<body>

<div class="title">
  <img class="logo" src="">
  <h1></h1>
</div>


<script>
let data = {
  src: './images/vue-iron.png'
  title : 'Vue.js手牽手，一起嗑光全家桶'
}

$('.title > h1').text(data.title);
$('.logo').attr('src',data.src);

</script>
</body>
```

#### Vue資料綁定
```
<body>
<div id="app">
--畫面--
  <div class="title">
    //v-bind:可縮寫為:
    <img class ="logo" v-bind:src="src">
    <img class ="logo" :src="src">
  
  
    //{{title}}可快速取值
    <h1 v-text="title"></h1>
    <h1 v-html="title"></h1>
    <h1>{{title}}</h1>
  </div>
</div>
--畫面--


--資料--
<script>
let data = {
  src: './images/vue-iron.png'
  title : 'Vue.js手牽手，一起嗑光全家桶'
}
--資料--


//第一步，綁定畫面與資料
let vm = new Vue({
  el: '#app',
  data: data
})
</script>
</body>
```
> el - 綁定 HTML 檔的標籤，這說明「 HTML 裡 id 為 app 的 div 由我來操控」；反過來說，id 不是 app 的 div 都不歸我這個 Vue 實體操作。

> data - 資料，是一個物件，負責我們在樣板的插值中想顯示的資料，插值以雙大括號寫在 HTML 中，並與 data 中的同名對應屬性單向綁定。屬性可以賦予各種型別的值：數值（10）、字串（友好商店）、布林值、陣列（各種精靈球）、物件都是可行的。

#### data寫法
> 在vue實體中的data屬性有兩種寫法
```
//這種寫法記得要寫return，讓它呼叫data時可以得到一個物件

data() {
    return {
      message: 'Welcome to Vue!'
    };
  }
```
```
data: {
    message: 'Welcome to Vue!'
}
```
#### 字串佔位符
> ES6 的 Template Strings 模版字符串，就是用占位符的方式来拼接字符串

>注意使用佔位符時要用` 非單引號
```
const name = '小缘'
const age = 14


console.info(`大家好，我叫${name}，今年${age}岁了`)
// 等价于
console.info("大家好，我叫" + name + "，今年" + age + "岁了")
```
### v-text, v-html
#### v-text
```
<div id="app"><!-- 樣板 templates -->
  <p>歡迎來到{{ shopName }}！雙大括號插值版本</p>
  <p>歡迎來到<span v-text="shopName"></span>！指令 v-text 版本</p>
</div>


let vm = new Vue({
  el:'#app',
  data:{
    shopName: '友好商店',
  }
})
```
```
歡迎來到友好商店！雙大括號插值版本
歡迎來到友好商店！指令 v-text 版本
```
#### v-html
> 與 v-text 效果類似，但可以輸出 HTML 代碼。但因為用變數將 HTML 寫入網頁可能會產生 XSS 攻擊的風險，所以只能在信任的資料上運用 v-html。
```
<div id="app"><!-- 樣板 templates -->
  <p>歡迎來到{{ shopName }}！雙大括號插值版本</p>
  <p>歡迎來到<span v-text="shopName"></span>！指令 v-text 版本</p>
  <p>歡迎來到<span v-html="shopName"></span>！指令 v-html 版本</p>
</div>


let vm = new Vue({
  el:'#app',
  data:{
    shopName: '<span style="color:red;">友好商店</span>',
  }
})
```
```
歡迎來到<span style="color:red;">友好商店</span>！雙大括號插值版本
歡迎來到<span style="color:red;">友好商店</span>！指令 v-text 版本
歡迎來到友好商店！指令 v-html 版本  //友好商店為紅字
```
### v-bind (屬性綁定)
> 綁在 HTML 上的屬性 (attribute) 若希望能與 vue instance 結合，就要加上 v-bind:some_attribute (簡寫 :some_attribute)。

> :value="variable"

> :some_attribute(原生屬性) / :some_property(自定義)
```
如下所示，在 <a> 上的屬性 title，若希望能帶入資料 hint，就要使用 :title="hint"。
```
```
<div id="app">
  <a href="#" :title="hint" :data="hint">${ text }</a>
</div>


var vm = new Vue({
  el: '#app',
  delimiters: ['${', '}'],
  data: {
    text: '把滑鼠移過來看看！',
    hint: '我是標題！'
  }
});
```
```
  <div id="app">
    <label for="name">輸入你想顯示的文字吧!</label>
    <input type="text" v-model="message" name="msg">
    <h1 v-if="isWelcomed">{{ message }}</h1>
    <img :src="imgSrc">
  </div>
  
<script>
var vm = new Vue({
  el : "#app",
  data : {
    message: 'Welcome to Vue!',
    imgSrc: 'https://upload.cc/i1/2020/08/23/rGPIy0.jpg',
    isWelcomed: true
  }
});
</script>
```
#### v-bind:style
> v-bind 的效果是提供 HTML 屬性，讓我們可以依據條件與情形動態操作該 HTML 標籤下的屬性細節。如：div區塊內的文字樣式style，img內的圖片連結src等等。
```
<div id="app">
  <p>歡迎來到<span v-html="shopName_00"></span>！指令 v-html 版本</p>
  <p>歡迎來到<span v-bind:style="isRed" v-text="shopName_01"></span>！指令 v-bind:style + v-text 版本</p>
</div>


let vm = new Vue({
  el:'#app',
  data:{
    shopName_00: '<span style="color:red;">友好商店</span>',
    shopName_01: '友好商店',
    isRed: {color: 'red'}
  }
})
```
```
歡迎來到友好商店！指令 v-html 版本  //友好商店為紅字
歡迎來到友好商店！指令 v-bind:style + v-text 版本  //友好商店為紅字
```
#### v-bind:class
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

<style>
.redWord {
color: red;
}
</style>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>

<div id="app">
    <p>歡迎來到<span v-bind:style="isRed" v-text="shopName_01"></span>！指令 v-bind:style + v-text 版本</p>
    <p>歡迎來到<span v-bind:class="classIsRed" v-text="shopName_01"></span>！指令 v-bind:class + v-text 版本</p>
</div>
    
<script>
let vm = new Vue({
  el:'#app',
  data:{
    shopName_01: '友好商店',
    isRed: {
      color: 'red',
    },
    classIsRed: 'redWord',
  }
})
</script>
</body>
```
```
歡迎來到友好商店！指令 v-bind:style + v-text 版本  //友好商店為紅字

歡迎來到友好商店！指令 v-bind:class + v-text 版本  //友好商店為紅字
```
> 套用多個樣式-使用陣列
```
<div id="app">
   <p>歡迎來到<span v-bind:class="[classIsRed, classIsBold]" v-text="shopName_01"></span>！指令 v-bind:class + v-text 多個樣式版本</p>
</div>


.redWord {
color: red;
}
.boldWord {
font-weight:bold;
}


let vm = new Vue({
  el:'#app',
  data:{
    shopName_01: '友好商店',
    classIsRed: 'redWord',
    classIsBold: 'boldWord'
  }
})
```
> 以物件來編寫(不好的寫法)
```
<div id="app">
  <p>歡迎來到<span v-bind:class="{redWord: true, boldWord: true}" v-text="shopName_01"></span>！指令 v-bind:class + v-text 物件版本 1</p>
</div>


.redWord {
color: red;
}

.boldWord {
font-weight:bold;
}
```
> 以物件來編寫(較好的寫法)
```
<div id="app">
  <p>歡迎來到<span v-bind:class="{redWord: isItRed, boldWord: IsitBold}" v-text="shopName_01"></span>！指令 v-bind:class + v-text 物件版本 2</p>
</div>


.redWord {
color: red;
}

.boldWord {
font-weight:bold;
}


let vm = new Vue({
  el:'#app',
  data:{
    shopName_01: '友好商店',
    isItRed: true,
    IsitBold: true
  }
})
```
> 較易閱讀寫法
```
<div id="app">
  <p>歡迎來到<span v-bind:class="caution" v-text="shopName_01"></span>！指令 v-bind:class + v-text 物件版本 3</p>
</div>


.redWord {
color: red;
}

.boldWord {
font-weight:bold;
}


let vm = new Vue({
  el:'#app',
  data:{
    shopName_01: '友好商店',
    caution: {
      redWord: true,
      boldWord: true
    }
  }
})
```
### v-if & v-show (條件渲染)
> 條件渲染，簡單說就是若某種情況，我就要render某些元素出來
```
  <div id="app">
    <p v-if="isLogin">我已登入</p>
    <p v-show="isAdmin">我是管理員</p>
    <button @click="isAdmin = !isAdmin">點我切換轉管理員身分</button>
  </div>
<script>

var vm = new Vue({
  el : "#app",
  data : {
    isAdmin: false,
    isLogin: true
  }
});
</script>
```
#### v-if & v-show差異
```
v-show 因為是單純控制css display屬性決定要不要出現，效能表現會比較好一點。
v-if可以用在template(子元件的顯示上) v-show無法。
v-if可以搭配v-else-if、v-else等directives使用。
```
#### v-if & v-else 
> v-else一定要緊接在v-if的元件後面，否則會報錯
```
  <div id="app">
    <p v-if="isLogin">我已登入</p>
    <p v-else>我沒登入喔</p>
    <button @click="isLogin = !isLogin">點我切換登入登出</button>
  </div>
<script>

var vm = new Vue({
  el : "#app",
  data : {
    isLogin: true
  }
});
</script>
```
### v-for 用陣列渲染列表
> v-for可以對陣列或物件的元素進行循環，將元素渲染在頁面上，概念類似原生javascript的for迴圈。

> v-for="item in items" 前方的變數你可以自由命名，後方則是你存在data屬性中的陣列/物件。然後決定渲染的格式，例如最簡單的就是直接在v-for指令內的寫下{{ item }}，那這樣items內的所有元素就會依序渲染在頁面上。

> 由於效能考量，在預設的狀況下，Vue.js 會儘量重覆使用已渲染好的元素。若不設定 key 值，不會重新渲染元素，只會部份更新。

#### 設定key值差異
```
//無設定key值的話，原本輸入框的值按下reverse不會重新渲染排序

<div id="app">
  <ul>
    <li v-for="(item, index) in list" :key="item.id">
      ${ index } <input type="text" :placeholder="item.name" />
  </ul>
  <button @click="hand">reverse</button>
</div>
    
<script>
let vm = new Vue({
  el:"#app",
  delimiters: ['${', '}'],
  data(){
    return{
      list: [
      { id: '123456789', name: '選項 1' },
      { id: '234567890', name: '選項 2' },
      { id: '345678901', name: '選項 3' },
    ]
    };
  },
  methods:{
    hand(){
      vm.list.reverse();
    }
  }
});
</script>
```
#### 陣列
##### sample1
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>

<div  id="app">
  <p>Show all balls</p>
  <ul>
    <li v-for="ball in balls">{{ball}}</li>
  </ul>
</div>

<script>
var vm = new Vue({
  el : "#app",
  data : {
    balls : ['精靈球','超級球','無敵球']
  }
});
</script>
</body>
```
##### sample2
```
  <div id="app">
    <h1>V-for demo</h1>
    <ul>
      <li v-for="(item,index) in list">
      index:{{index}} name:{{item.name}}
      </li>
    </ul>
  </div>
<script>
var vm = new Vue({
  el : "#app",
  data : {
    list: [
      { id: '123456789', name: '選項 1' },
      { id: '234567890', name: '選項 2' },
      { id: '345678901', name: '選項 3' },
    ]
    }
});
</script>
```
```
index:0 name:選項 1
index:1 name:選項 2
index:2 name:選項 3
```
#### 物件-只取值
> v-for也可以套用在物件上，不變更item in items特殊語法，他只會取物件內的值（value），不會取鍵或索引。
```
<div id="app2">
  <ul>
    <li v-for="ball in pokeball">
      {{ ball }}
    </li>
  </ul>
</div>

<script>
var vm = new Vue({
  el: '#app2',
  data: {
    pokeball: {
      name: '精靈球',
      price: 200,
      description: '用於投向野生寶可夢並將其捕捉的球。它是膠囊樣式的。'
    }
  },
});
</script>
```
```
精靈球
200
用於投向野生寶可夢並將其捕捉的球。它是膠囊樣式的。
```
#### 物件-取value, key, index
> 如果沒有用到index，是可以省略的。value, key 跟 index 都可以取自己需要的別名代替，別名會依據逗號的次序分別被認為是value, key 跟 index。
```
<div  id="app">
  <p>Show all balls</p>
  <ul>
    <li v-for="(price,ball,index) in balls">
      {{index+1}} - {{ball}} - ${{price}}</li>
  </ul>
</div>

<script>
var vm = new Vue({
  el : "#app",
  data : {
    balls: {
      '精靈球': 200,
      '超級球': 600,
      '高級球': 1200
    }  
  }
});
</script>
```
```
1 - 精靈球 - $200
2 - 超級球 - $600
3 - 高級球 - $1200
```
###  v-model 與雙向綁定
> v-model可以進行資料雙向綁定，最常見於取得使用者的 input 例如：文字區域textarea、單選radio、下拉式選單select等等，並與同名的 data 內的資料做綁定。而且v-model會根據監聽的對象來自動選正確的方式來更新值。

#### 雙向綁定概述
```
//一般情況下都是由下方的vue實體 -> DOM

//雙向綁定 = 在DOM中操作vue實體中的變數、同時希望在實體做的任何更動也會反應在template中


<div id="app">
  <p><input type="text" v-model="message"></p>
  <p>{{message}}</p>
</div>
  
<script>
var vm = new Vue({
  el : "#app",
  data : {
    message : "default"
    }
});
</script>
```
#### input
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>

<div id="app">
  <p>歡迎來到<span v-text="shopName_01"></span>！請告訴我您需要的商品！</p>
  <input v-model="goods"></input>
  <p v-text="goods"></p>
</div>
    
<script>
let vm = new Vue({
  el:'#app',
  data:{
    shopName_01: '友好商店',
    goods:''
  }
})
</script>
</body>
```
```
input輸入的值同步顯示在<p v-text="goods"></p>
```
#### radio
```
<div id="app">
  <input type="radio" value="精靈球" v-model="goods">
  <label for="精靈球">精靈球</label>
  <br>
  <input type="radio" value="超級球" v-model="goods">
  <label for="超級球">超級球</label>
  <br>
  <p v-text="goods"></p>
</div>
```
#### checkbox
```
<div id="app">
  <input type="checkbox" id="精靈球" value="精靈球" v-model="goods">
  <label for="精靈球">精靈球</label>
  <input type="checkbox" id="超級球" value="超級球" v-model="goods">
  <label for="超級球">超級球</label>
  <input type="checkbox" id="高級球" value="高級球" v-model="goods">
  <label for="高級球">高級球</label>
  <p v-text="goods"></p>
</div>
    
<script>
let vm = new Vue({
  el:'#app',
  data:{
    shopName_01: '友好商店',
    goods: []
  }
})
</script>
```
```
goods 需改成陣列
```
#### select
```
<div id="app">
  <select v-model="goods">
    <option disabled value="">請告訴我您想購買的商品</option>
    <option>精靈球</option>
    <option>超級球</option>
    <option>高級球</option>
  </select>
  <p v-text="goods"></p>
</div>
```
#### 模擬送出表單
```
<div class="form-container" id="app">
  <form>
    <h2>模擬送出表單</h2>
    <div class="input-group">
      <label for="username">請輸入帳號: </label>
      <input type="text" name="username" v-model="username">
    </div>
    <div class="input-group">
      <label for="password">請輸入密碼: </label>
      <input type="text" name="password" v-model="password">
    </div>
    <button @click.prevent="handleSubmit">送出</button>
  </form>
</div>
    
<script>
let vm = new Vue({
  el:'#app',
  data() {
    return {
      message: '你好 我是Danny',
      textColor: 'red',
      username: '',
      password: ''
    };
  },
  methods: {
    handleSubmit() {
      alert(`你所輸入的帳號是: ${this.username} \n而你所輸入的密碼是${this.password}`);
    }
  }
})
</script>
```
### v-on
> v-on: Vue中的event handler!

> v-on:click縮寫為@click

> v-on可接其他事件，如v-on:dblclick、v-on:focus等等

> v-on指令可以將事件偵聽器與一個元素（如按鈕）綁定。事件偵聽器也可以傳入值。在v-on:click後方填入「方法」的名稱，便能每當按鈕被按下時呼叫那個方法，而方法就如一般 javascript 的 function 一樣，而且必須把他們寫在methods裡。methods通常與el、data對齊。
#### 基本範例
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>


<div id="app">
  <button v-on:click="inc">+1</button> 
  <p v-text="total"></p>
</div>

    
<script>
var vm = new Vue({
  el: '#app',
  data: {
    total: '0'
  },
  methods: {
    inc() {
      this.total++;   //這裡的 this 指向 Vue 實體
    },
  }
})
</script>
</body>
```
```
每點一次 +1 按鈕，下面的<p v-text="total"></p>數值也會增加 1。
```
#### 進階範例
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

<style>
input[type=number]{
    width: 25px;
    text-align: center
} 

input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
    -webkit-appearance: none 
}

</style>
</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>


<div id="app">
  <h3>請告訴我您需要的款式與數量</h3>
  <p><span v-text="ball[0]"></span> $<span v-text="price[0]"></span> 
    <button v-on:click="dec">-1</button> 
    <input name="ball01" type=number v-model="ballTotal"> 
    <button v-on:click="inc">+1</button> 目前精靈球【數量：<span v-text="ballTotal"></span>】 【總額：<span v-text="sum"></span>】</p>
</div>

<script>
var vm = new Vue({
  el: '#app',
  data: {
    ball: ['精靈球', '超級球', '高級球'],
    price:[ 200, 600, 1200],
    ballTotal: 0
  },
  methods: {
    inc() {
      this.ballTotal++;
    },
    dec() {
      this.ballTotal--;
    },
  },
  computed: {
    sum() {
      return this.ballTotal * 200;
    }
  },
})
</script>
</body>
</html>
```
```
//也可改寫成watch

    watch : {
      ballTotal: function(){
        this.sum = this.ballTotal * 200;
      }
    }
```
### computed vs watch
> computed 最大特點是必須回傳一個值，並且會把它緩存起來，當函式裏的依賴改變時，才會重新執行和求值。但 watch 與 methods 不會強制要求回傳一個值，它們只需執行動作，不一定要回傳值。

> watch可以處理非同步工作，computed 無法進行非同步工作。

### computed
> 計算屬性，有點像介於資料與方法之間，既可以像資料一樣填入雙大括號，渲染頁面，同時花費緩存空間偵聽著取用的資料的值是否有變動，如果變動了，計算屬性的值也會立刻跟著更新。
> computed必定要return某個值。
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>


<div id="app">
 <p>輸入城市<input type="text" v-model="city">&nbsp;<span v-text="city"></span></p>
 <p>地址為<input type="text" v-model="region"></span>&nbsp;<span v-text="region">區</span></p>
 <p>呼叫Computed: <span v-text="fullLocation"></span></p>
</div>

<script>
var vm = new Vue({
  el : "#app",
  data : {
    city : "",
    region : ""
  },
  computed : {
    fullLocation(){
      return this.city + this.region;
    }
  }
});
</script>
</body>
```
### watch
> watch 監聽器，用以監聽某個數據，並觸發相對應的處理。

> 你要監聽的值，可以是data屬性的變數、或是computed計算後的值。

> watch 可以讓我們監聽 data 物件屬性或計算屬性的變化，每當監聽的對象的值產生變化時，實行watch裡面的程式碼。我們可以用watch來做跟computed計算屬性一樣的事情。
#### 基礎範例
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>


<div id="app">
 <p>輸入城市<input type="text" v-model="city">&nbsp;<span v-text="city"></span></p>
 <p>地址為<input type="text" v-model="region"></span>&nbsp;<span v-text="region">區</span></p>
 <p>使用watch監聽: <span v-text="fullLocation"></span></p>
</div>

<script>
var vm = new Vue({
  el : "#app",
  data : {
    city : "",
    region : "",
    fullLocation : ""
  },
  watch : {
    //監控值改變，給予新值
    region(newVal, oldVal){
      this.fullLocation = this.city + " " + newVal;
    },
    city(newVal, oldVal){
      this.fullLocation = newVal + " " + this.region;
    },
    //監控值改變，執行方法
    region(){
      alert("region發生改變了");  //region重複監控，只會執行其中一個，錯誤寫法
    }
  }
});
</script>
</body>


//此寫法結果相同
  watch : {
    region: function(newVal, oldVal){
      this.fullLocation = this.city + " " + newVal;
    },
    city: function(newVal, oldVal){
      this.fullLocation = newVal + " " + this.region;
    }
  }   
    
    
//此寫法結果相同    
  watch : {
    region : {
      handler(newVal,oldVal){
        this.fullLocation = this.city + " " + newVal;
      }
    },
    city : {
      handler(newVal,oldVal){
        this.fullLocation = newVal + " " + this.region;
      }
    }
  }    
```
#### 監聽物件
```
watch屬性中有一些可傳入的選項讓你更精確的控制整個流程，不過為了傳入options，在寫法上會稍微不太一樣

如果你想傳入options，上述的寫法就必須改為以下，以物件的方式表示，其中包含:
-handler function
-options(其中包含immediate & deep，預設為false)


handler: 就是你watch中需要具體執行的方法，當watch的值發生變化的時候，就會觸發這個handler。

immediate: 設為 true 可讓監聽值在初始和值被改變時觸發 callback handler。(設為false的話在一開始還沒呼叫watch時{{fullData}}是沒有值的)

deep: 若設置為true，則會一同監聽深層的值是否有變化，比方說之前的例子，你便可以直接監聽整個person物件，這樣當person物件中有任何變化時都會觸發handler function。
```
```
我們會是監聽該key值(EX:"person.name")，並以字串的方式傳入。
```
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>

<div id="app">
 <p>輸入名字<input type="text" v-model="person.name">&nbsp;<span v-text="person.name"></span></p>
 <p>輸入ID<input type="text" v-model="person.id"></span>&nbsp;<span v-text="person.id"></span></p>
 <p>呼叫Watch: {{fullData}}</p>
</div>

<script>
var vm = new Vue({
el : "#app",
data : {
  person: {
        name: 'Danny',
        id: 9831032
  },
  fullData : ""
},
watch:{ 
  "person.name" : {
     handler(newVal, oldVal) {
       this.fullData = newVal + this.person.id;
     },
     immediate: true,
     deep: true
  },
  "person.id" : {
     handler(newVal, oldVal) {
       this.fullData = this.person.name + newVal;
     },
     immediate: true,
     deep: true
  },    
}
});
</script>
</body>
```
### Vue 的生命週期
#### 無使用 keep-alive 標籤
* beforeCreate
```
初始化vue實體，這時候實體尚未建立，裡面的屬性自然也不能取用。
```
* created
```
實體創建完成，你所建立的屬性(data、methods等)也成功綁定到該實體上，可以讀取data內的值，
但DOM元素尚未生成，且$el元素也還不存在。
```
* beforeMount
```
在創建的vue實體被掛載之前的階段，此時$el元素尚未被建立。
```
* mounted
```
元素已掛載，$el被建立，是最常使用的生命週期 hook。
已產出真正的頁面，DOM元素也已經產生，可以做各種元素的操作，一般來說很常在這個階段或是created階段發出API請求。
```
* beforeUpdate
```
在頁面元素被更新前觸發的階段，數據已經更新、但頁面還沒有渲染。
```
* updated
```
數據更新且頁面也渲染了更新後的結果。
```
* beforeDestroy
```
Vue實體要被銷毀前的階段，可以在這個階段做一些最後詢問之類的功能。
```
* destroyed
```
Vue實例銷毀，所有的DOM 元素綁定被解除、移除偵聽事件、Vue child 實例也被一併銷毀。
```
#### 使用 keep-alive 標籤
> 若是在 HTML 有使用 keep-alive 標籤，其特性是可以維持資料狀態，只會有 activated Hook 與 deactivated Hook 的情況產生，則不觸發 destroyed Hook 。

> 反之，若在 HTML 沒有使用 keep-alive 標籤，則會觸發 destroyed Hook 銷毀資料。

* ctivated (用於keep-alive標籤的兩個階段)
```
若你的HTML標籤內有設定keep-alive，就會觸發這個階段的函數，並跳過之前的destroy階段。
```
* deActivated (用於keep-alive標籤的兩個階段)
```
停用keep-alive時會觸發的階段。
```
#### 基礎範例
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  
  a,
  button {
    color: #4fc08d;
  }
  
  button {
    background: none;
    border: solid 1px;
    border-radius: 2em;
    font: inherit;
    padding: 0.75em 2em;
  }
  </style>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>


<div id="app">
  <h1>{{message}}</h1>
   <label for="message">請輸入訊息</label>
  <input type="text" v-model="message">
</div>

<script>
var vm = new Vue({
  el : "#app",
  data() {
    return {
      message: 'Welcome to Vue!'
    };
  },
  methods: {
    doSomething() {
      alert('Hello!');
    }
  },
  beforeCreate(){
    console.log('beforeCreate called')
  },
  created() {
    console.log('created called')
  },
  beforeMount() {
    console.log('beforeMount called')
  },
  mounted() {
    console.log('mounted called')
  },
  beforeUpdate() {
    console.log('beforeUpdate called')
  },
  updated() {
    console.log('updated called')
  }
});
</script>
</body>
```
```
//未操作頁面前
beforeCreate called
created called
beforeMount called
mounted called

//輸入訊息(操作頁面後)
beforeUpdate called
updated called
```
### async & await (非同步 & 等待)
> 在async function內，會先等await做完事，才繼續進行下面的程式碼。

> 使用場景:要將await的結果拿來下面的程式碼使用

> 因為是非同步，所以當async卡住的時候，會先執行2222，再執行1111
```
async function test1(){
    await new Promise((a,b)=>{
        setTimeout(a,1000)})
        console.log("1111")
}

test1();
console.log("2222");
```
```
2222
1111
```
### 頁面傳遞
```
[父層給子層東西] example(爺FBEM0400 子PageTab 孫SaveForm)

父
//:systemDate 對應 props
<SaveForm
  slot="belowCardDetail"
  ref="saveForm"
  :systemDate="systemDate"  //傳變數值  
/>

子
props: 
{
    systemDate: String,
}
       
this.systemDate  //拿來用
==============================================================================	 
[子層給父層東西] example(父PageTab 子BtnGroupCRUD)

父
//由前面的@searchBtnClick拿來接
<BtnGroupCRUD
  @searchBtnClick="searchBtnClick"
  @clearBtnClick="clearBtnClick"
/>

子
searchBtnClick() {
  this.$emit("searchBtnClick");
}
==============================================================================	
[父層搶子層東西] example(父PageTab 子SearchForm)  (當子層沒有按鍵可以觸發，比如一個查詢框)

父
searchFormData() {
  return this.$refs.searchForm.formData;
}

子
<SearchForm ref="searchForm" :sourceNum.sync="sourceNum" />    (寫在父層內的子層標籤上，子層內不須寫)
==============================================================================	

sourceNum.sync  為了子層直接修改父曾特定的值


A import B來用  A是父層 B是子層

PageTab=父層

<SearchForm ref="sForm" :sourceNum.sync="source" /> 子層

   this.$emit("update:sourceNum","test");   //sync可使用此方法來更新父值
   
   
<BtnGroupCRUD
  :add="false"  //傳屬性出去給子層
  :customBtns="customBtns"
  @overruleBtnClick="overruleBtnClick"  //子層傳遞click事件到父層，clear動作在父層做
/>   
```
### 練習
#### 計算機
```
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例 - 菜鸟教程(runoob.com)</title>

</head>
<body>
<script src="https://cdn.staticfile.org/vue/2.2.2/vue.min.js"></script>
  <style>  
    #app {
      font-family: "Avenir", Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #2c3e50;
      margin-top: 60px;
    }  
      
    .flexbox {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100vw;
      height: 100vh;
    }
      
    .calculator {
      display: grid;
      width: 300px;
      margin: 0 auto;
      font-size: 40px;
      grid-template-columns: repeat(4, 1fr);
      grid-auto-rows: minmax(50px, auto);
      border: .3px solid #868383;
      border-radius: 3rem;
      padding: .8em;
      background-color: #222;
    }
      
    .display {
      grid-column: 1/5;
      background-color: lightblue;
      text-align: right;
      padding-right: 20px;
      background-color: #D3D3D3;
      color: #333;
      margin-bottom: 10px;
      border-radius: 16px;
      outline: 0;
      font-size: 36px;
    }
      
    .btn {
      border: 1px solid black;
      background-color: #999;
      cursor: pointer;
      border-radius: 40px;
      margin: 10px;
      color: #222;
      font-weight: bold;
      text-align: center;
      transition: background-color 0.2s ease-in;
    }
      
    .btn:hover {
     background-color: #868383;   
    }
    .dark {
      background-color: #333;
      color: #ffffff;
    }
    .operator {
      background-color: #e08d1f;
    }
    .zero {
      grid-column: 1/3;
    }
    </style>


<div class="form-container" id="app">
  <div class="flexbox">
    <div class="calculator">
      <input class="display" v-model="current"></input>
      <div class="btn dark" @click="clear">C</div>
      <div class="btn dark">+/-</div>
      <div class="btn dark">%</div>
      <div class="btn operator" @click="divide">/</div>
      <div class="btn" @click="append('7')">7</div>
      <div class="btn" @click="append('8')">8</div>
      <div class="btn" @click="append('9')">9</div>
      <div class="btn operator" @click="multiply">x</div>
      <div class="btn" @click="append('4')">4</div>
      <div class="btn" @click="append('5')">5</div>
      <div class="btn" @click="append('6')">6</div>
      <div class="btn operator" @click="subtract">-</div>
      <div class="btn" @click="append('1')">1</div>
      <div class="btn" @click="append('2')">2</div>
      <div class="btn" @click="append('3')">3</div>
      <div class="btn operator" @click="plus">+</div>
      <div class="btn zero" @click="append('0')">0</div>
      <div class="btn" >.</div>
      <div class="btn operator" @click="equal">=</div>
    </div>
  </div>s
</div>
    
<script>
let vm = new Vue({
  el:'#app',
  name: "Calculator",
  data() {
    return {
      current: "",
      previous: "",
      operator: null,
      operatorClicked: false
    };
  },
  methods:{
    append(number) {
      // 如果已點選任何運算子，則清空目前的值
      if (this.operatorClicked) {
        this.current = "";
      }

      // 重置operatorClicked的值，讓第二個數字也能正常輸入
      this.operatorClicked = false;
      this.current = this.current == "0" ? `${number}` : `${this.current}${number}`;
    },
    plus() {
      // 傳入運算函數
      this.operator = (a, b) => a + b;
      // 呼叫設定setPrevious的函數
      this.setPrevious();
    },
    subtract(){
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    multiply(){
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    divide(){
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    setPrevious() {
      // 將目前的值存在previous(按下個數字前要清空目前的current)
      this.previous = this.current;
      // 表示使用者確實按下任何一個運算子
      this.operatorClicked = true;
    },
    equal() {
      console.log(this.current, this.previous);
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      )}`;
      this.operator = null;
      this.operatorClicked = false;
    },
    clear(){
      this.current = '';
    }
  }
});
</script>
</body>
```