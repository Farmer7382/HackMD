# Html學習筆記

### 空元素
空元素是沒有結束標籤的元素，像是圖片元素 <img>，例如我們可以用 img 標籤來顯示一張圖片：
`<img src="/images/myphoto.png">`

### HTML 標籤屬性 (Attribute)
HTML 標籤中還有所謂的屬性 (Attribute)，**屬性是用來提供該標籤的額外資訊**，屬性出現在起始標籤中，語法如下：
`<tag attribute1="value2" attribute2="value2">`
像是前面提到的例子`<img src="/images/myphoto.png">`，其中 src 就是 img 的屬性。

### HTML 全域屬性 (global attributes)
#### id 元素唯一識別符號:
id 是用來設定 HTML 元素的唯一識別符號 (identifier)，**每個 HTML 元素的 id 需要是在整份 HTML 文件中獨一無二 (unique) 不可重複的。**

設定 id 有三種用途:
```
1. 用作 <a> 連結的錨點 (anchor) 名稱。例如點擊連結<a href="#myid">會跳到 <tag id="myid">元素處
2. 用在 JavaScript 可以透過 id 存取該元素
3. 用在 CSS 可以用 id 當選擇器 (selector)
```

語法範例:
`<p id="exciting">The most exciting paragraph on the page. One of a kind!</p>`

#### class 元素類別名稱:
class 是用來設定 HTML 元素的類別名稱 (class names)，**每一個 HTML 元素可以有多個類別**，你可以用空格分隔 (space-separated) 開不同的類別名稱。

class 有兩種用途：
```
1. 用在 JavaScript 可以透過 class 存取該元素
2. 用在 CSS 可以用 class 當選擇器 (selector)
```

語法範例:
`<p class="note editorial">Above point sounds a bit obvious. Remove/rewrite?</p>`

#### style 設定 CSS 樣式:
style 用來直接設定該 HTML 元素的 CSS 樣式 (inline style)，而用 style 屬性設定的 CSS 優先權是最高的，會蓋過寫在 `<style>` 或外部樣式表中的樣式。

語法範例:
```
<p style="padding: 15px; line-height: 1.5; text-align: center; border: 3px solid #000;">
   Hello World!
</p>
```

#### `<hidden>` 隱藏元素:
hidden 用來設定該 HTML 元素是否要被從畫面中隱藏起來，通常讓使用者滿足某些條件後才能看見。hidden 是一個布林屬性 (boolean)。

語法範例:
```
<p>你看得見我</p>
<p hidden>你看不見我</p>
```
### HTML `<head>` 標籤 (Tag):
HTML 網頁中一定有一個 (也只會有一個) `<head>`標籤 (tag)，`<head>` 是接在 `<html>` 下面的第一個標籤，而在 `<body>` 起始標籤前面結束。

`<head>` 標籤作用上是當作一個容器，裡面包含著不同用途的 HTML tags，而這些 tag 的內容通常不會被顯示在頁面上，僅用來說明關於該網頁的元資訊 (metadata)，像是指定網頁的標題，或像是指定該網頁所使用的編碼等。

語法範例:
```
<!DOCTYPE html>
<html>
  <head>
    <title>Page Head</title>
    <link href="page.css" rel="stylesheet">
  </head>
  <body>
    <!-- blah blah -->
  </body>
</html>
```

被包含在 `<head>` 裡面的標籤有這些：
```
* <title> 網頁名稱
* <meta> 網頁 metadata
* <style> CSS 樣式
* <link> CSS 樣式表
* <script> JavaScript 程式碼
* <noscript> 網頁不支援 JavaScript 時的處理
* <base> base URL
```

#### *HTML `<title>` 標籤 (tag) - 設定網頁標題
HTML 網頁中一定有一個 (也只會有一個) `<title>` 標籤 (tag)，`<title>` 是用來描述網頁的標題。

網頁標題通常會在：
* 顯示在瀏覽器的書籤 (favorites, bookmarks)
* 顯示在瀏覽器的頁籤上 (tab, toolbar)
* 顯示在搜尋引擎的網頁搜尋結果中

#### *HTML `<style>` 標籤 (tag) - 寫 CSS 樣式排版
除了用 `<style>` 或 `<link>` 標籤來寫 CSS，所有的 HTML 標籤都可以用 style 屬性來指定該 HTML 元素的 CSS 樣式。
`<p style="color:red">This is a paragraph.</p>`上面的 p 段落文字會變成是紅色。

### HTML `<body>` 標籤 (tag)
HTML 網頁中一定有一個 (也只會有一個) `<body>` 標籤 (tag)，`<body>` 接在 `<head>` 結束標籤後面。

`<body>` 標籤作用上是當作一個容器，用來呈現網頁的主要內容，`<body>` 裡面會再包含有不同用途和語意的 HTML tags 來描述和架構出網頁內容。

`<body>` 裡面主要是放使用者從螢幕上看得到的內容，相對於 `<head>` 是放使用者看不見給機器看的內容。

#### HTML `<p>` 段落標籤 (tag)
HTML `<p>` 標籤是用來描述一段文字段落 (paragraph)，瀏覽器預設會在段落間幫你做換行和留邊距 (margin)。

#### HTML `<br>` 換行標籤 (tag)
在 HTML 文件中不是用 \n (new line) 來換行，而是用 `<br>` 來做內容換行 (line break) 的效果。

#### HTML 圖片 `<img>` 標籤 (tag)
`<img>` 主要是搭配 src 屬性來指定圖片位址，使用範例：
```
<img src="https://example.com/media/photo.jpg" width="600" height="400" alt="一張圖片">
```
src
指定圖片位址 (URL)，只有這個屬性是必需要有的。

width
一個整數值，指定圖片寬度像素 (pixels)，有指定的好處是可以避面頁面渲染時的跳動，因為瀏覽器不用等圖片下載完才能計算圖片寬度。

height
一個整數值，指定圖片高度像素 (pixels)，有指定的好處是可以避面頁面渲染時的跳動，因為瀏覽器不用等圖片下載完才能計算圖片高度。

alt
圖片替代文字 (alternate text)，當圖片無法顯示時，瀏覽器會顯示此文字。這文字說明對 SEO 也很有助益，所以建議圖片都需要有 alt。

title
可以指定一段文字，在當滑鼠滑過圖片時，會自動顯示這段文字。

#### HTML 超連結 `<a>` 標籤 (tag)
用來建立超連結 (hyperlink) -- 通往其他頁面、檔案、Email 地址、或其他 URL 的超連結。

實例:

* 連結到站外
```
<a href="https://www.youtube.com/">這個連結</a>會連到 YouTube<br>
<a href="https://www.google.com/">這個連結</a>會連到 Google<br>
<a href="/html/image-img-tag.html">這個連結</a>會連到 Fooish 圖片標籤教學頁面
```

* 頁內超連結
```
//先替某一段落取名字(設定一個錨點)
<a name="BrainStorm">

<a href="#BrainStorm">
連接到本網頁的BrainStorm段落
</a>
```

屬性:

* href 指定一個 URL 看連結要連到哪邊。
* target 指定在什麼地方打開連結。

target 有下面這些屬性值：
* _self: 預設值，在當前視窗開啟
* _blank: 在新視窗開啟
* _parent: 在上一層父視窗開啟
* _top: 在最頂層父視窗開啟
* framename: 指定在哪個框架中開啟

`<a href="https://www.fooish.com/" target="_blank">Fooish 技術教學</a>`

* 圖片超連結
```
<a href="https://zh.wikipedia.org/wiki/櫻桃小丸子">

<img src="GIF/b6_small.gif">
</a>
```
### HTML 項目列表清單
HTML 有三類型的列表清單：
無序的列表 (unordered lists) `<ul>`
有序的列表 (ordered lists) `<ol>`
定義的列表 (definition lists) `<dl>`

```
<ul>
  <li>first item</li>
  <li>second item</li>
  <li>third item</li>
</ul>
```
* first item
* second item
* third item
```
<ol>
  <li>first item</li>
  <li>second item</li>
  <li>third item</li>
</ol>
```
1. first item
2. second item
3. third item
```
<ol>
  <li>ordered item 1</li>
  <li>
    ordered item 2
    <ul>
      <li>unordered item 2-1</li>
      <li>unordered item 2-2</li>
    </ul>
  </li>
  <li>ordered item 3</li>
</ol>
```
1. ordered item 1
2. ordered item 2
* unordered item 2-1
* unordered item 2-2
3. ordered item 3


### HTML表格
`<table>, <tr> 和 <td> 是 HTML 表格中最常見到也一定會用到的三個標籤，<table> 用來包著整個表格的結構和內容，<tr> (table row) 用來定義表格有幾個橫列 (row)，<tr> 裡面有 <td> (table data) 用來定義表格有幾個直行 (cloumn)，至於 <td> 裡面就是放實際單元格的資料。`

```
<table>
  <tr>
    <td>國家</td>
    <td>首都</td>
    <td>人口</td>
    <td>語言</td>
  </tr>
  <tr>
    <td>USA</td>
    <td>Washington D.C.</td>
    <td>309 million</td>
    <td>English</td>
  </tr>
  <tr>
    <td>Sweden</td>
    <td>Stockholm</td>
    <td>9 million</td>
    <td>Swedish</td>
  </tr>
</table>
```

`<th> (table header) 用來表示表格欄位的標題，<th> 可以用來替代 <td> 使用，用來在語意上更明確的聲明這一格是一個標題。則表格標題在瀏覽器預設樣式中會顯示成粗體字。`
```
<table>
  <tr>
    <th>國家</th>
    <th>首都</th>
    <th>人口</th>
    <th>語言</th>
  </tr>
  <tr>
    <td>USA</td>
    <td>Washington D.C.</td>
    <td>309 million</td>
    <td>English</td>
  </tr>
  <tr>
    <td>Sweden</td>
    <td>Stockholm</td>
    <td>9 million</td>
    <td>Swedish</td>
  </tr>
</table>
```

```
<table border="5" cellSpacing="8" cellPadding="10">
//cellSpacing=格子與格子的間距，cellPadding=格子內資料與格線的間距
```


| 國家 | 首都 | 人口 | 語言 |
| ---- | --- | --- | --- |
| USA| Washington D.C | 309 million |English|
| Sweden | Stockholm | 9 million|Swedish|


#### 合併儲存格: colspan 和 rowspan 屬性 (attributes)
合併表格可以利用 `<td>` 和 `<th>` 標籤上的 colspan 和 rowspan 屬性，colspan 是用來水平合併多行 (column) 的儲存格，rowspan 則用來垂直合併多列 (row) 的儲存格。
```
<table>
  <tr>
    <th>項目</th>
    <th>金額</th>
    <th>總金額</th>
  </tr>
  <tr>
    <td>iPhone 11</td>
    <td>$24,900</td>
    <td rowspan="2">$31,390</td>
  </tr>
  <tr>
    <td>AirPods</td>
    <td>$6,490</td>
  </tr>
</table>
```

| 項目 | 金額 | 總金額 |
| -------- | -------- | -------- |
| iPhone 11| $24,900| $31,390(合併)|
| AirPods| $6,490| $31,390(合併)|
上方例子中，rowspan="2" 表示從這一列開始往下合併至下一列 (共 2 列)。

所以說，你 rowspan 合併幾列，後面幾列的 `<tr>` 中同樣位置的 `<td>` 就要省略不寫。

```
<table>
  <tr>
    <th>項目</th>
    <th>金額</th>
  </tr>
  <tr>
    <td>iPhone 11</td>
    <td>$24,900</td>
  </tr>
  <tr>
    <td>AirPods</td>
    <td>$6,490</td>
  </tr>
  <tr>
    <td colspan="2">總金額: $31,390</td>
  </tr>
</table>
```

| 項目 | 金額 |
| -------- | -------- | 
| iPhone 11| $24,900|
| AirPods| $6,490| 
| 總金額: $31,390(合併)| 總金額: $31,390(合併)| 
上方例子中，colspan="2" 表示從這一行開始往右合併至下一行 (共 2 行)。

所以說，你 colspan 合併幾行，該儲存格緊接著的同一列 `<tr>` 後面的幾個 `<td>` 就要省略不寫。
		
### HTML 表單 (form)
HTML 表單 (form) 是用來讓使用者輸入資料，這些資料可以用來和使用者互動，例如表單內容填完後可以傳回遠端伺服器 (web server)，像常見的連絡表單。

#### `<form>` 標籤 (tag)
`<form>` 標籤是用來建立一個 HTML 表單，`<form>` 做為表單的容器，裡面還會有不同用途的其他標籤來建構出完整的表單內容。

`<form>` 標籤屬性 (attribute):

action: 用來指定一個位址 (URL)，這個位址是告訴瀏覽器 (browser) 當 user 按送出表單後，要將表格的內容送去哪邊。

method: 用來指定資料傳輸時用的 HTTP 協議，最常用的是 get 或 post：
* get: 會將表單資料放在 form action 請求的位址 URL 網址參數列 (URL GET parameters) 上面送出。get 通常用在資料量較小或非敏感的資料，因為資料會被放在網址中直接傳出，容易被直接看到資料。
* post: 會將表單資料放在 HTTP 傳輸封包 body 中送出。post 通常用在表單資料量比較大、有夾帶檔案上傳 (file upload) 或隱私性考量的資料。

target: 用來指定瀏覽器要在何處顯示表單送出後伺服器回應的結果。值有這些選項：
* _self: 顯示在表單所在的當前視窗
* _blank: 顯示在新頁籤/視窗
* _parent: 顯示在上一層的視窗 (用在例如如果表單是放在 `<iframe>` 中)
* _top: 顯示在最頂層的視窗
* autocomplete: 指示這個表單中的欄位是否啟用瀏覽器自動完成機制。值有這些選項：
* off: 否
* on: 是，預設值
```
<form action="/formprocess.php" method="post">
  
  <!-- ....表單 HTMLs .... -->
  
</form>
```
上面例子中，我們建立了一個表單，且宣告這個表單的資料會被用 http post 的方法送到 "/formprocess.php" 這隻遠端程式。

#### 常見的 HTML 表單元素
常見的表單元素有像是 `<input>`, `<textarea>`, `<select>` 等。

```
<input type="text"> 建立一個文字輸入欄位
<input type="password"> 建立一個密碼文字輸入欄位，和 text 的差別是，使用者輸入的內容不會被明碼顯示在螢幕畫面中
<input type="checkbox"> 建立一個核取方塊
<input type="radio"> 建立一個選項按鈕
<input type="submit"> 建立一個送出表單的按鈕
```
`<input>` 的大部分 type 都可以再搭配上 value 屬性，指定一個預設值。像是 type="text" 搭配 value= 指定輸入框中的預填文字；type="submit" 搭配 value= 指定按鈕文字。

`<input>` 是個空元素不需要 closing tag。

```
<textarea rows="指定輸入框的高度/列數，一個整數"
          cols="指定輸入框的寬度/行數，一個整數">
  
  輸入欄位中的預設文字內容
  
</textarea>
```
`<textarea>` 是用來宣告一個可以輸入多行文字的輸入框 (multi-line textbox)。

```
<select>
    <option>Option 1</option>
    <option>Option 2</option>
    <option value="3">Option 3</option>
</select>
```
`<select>` 是用來宣告一個下拉式選單 (drop-down select boxes)，而 `<select>` 標籤裡面還會有 `<option>` 標籤用來宣告有哪些選項。

`<option>` 裡面的文字就是使用者會看到的選項內容，而 `<option>` 上的 value 屬性是用來指定表單送出去時遠端伺服器會收到的值，沒有設定 value 的話，預設值會是 `<option>` 裡面的內容。

一個完整的 HTML 表單範例:
```
<form action="/formprocess.php" method="post">

    <p>Name:</p>
    <p><input type="text" name="name" value="你的名字"></p>

    <p>Email:</p>
    <p><input name="species" type="text"></p>

    <p>Comments: </p>
    <p><textarea name="comments" rows="5" cols="20">你的留言</textarea></p>

    <p>請問你最有興趣學習的技術:</p>
    <p><input type="radio" name="interest" value="html"> HTML</p>
    <p><input type="radio" name="interest" value="css"> CSS</p>
    <p><input type="radio" name="interest" value="js"> JavaScript</p>

    <p><input type="submit" value="送出資料"></p>

</form>
```

#### input
* disabled: 將元件設定為禁用狀態

`<input disabled>`
* readonly: 將元件設為唯獨不可更改內容的狀態

`<input value="點我看看可否編輯" readonly>`

* required: 指定為必填欄位

`<input required>`

* text input 的 placeholder 屬性: 輸入的提示訊息

`<input placeholder="請輸入帳號">`

* 密碼輸入欄位

`<input type="password">`

* checkbox 核取方塊(多選)

```
<input type="checkbox" name="subscribe" value="html-newsletter"> Subscribe to HTML newsletter?<br>
<input type="checkbox" name="subscribe" value="js-newsletter"> Subscribe to JavaScript newsletter?
```
當使用者勾選時，就會隨著表單送出像是 "subscribe=newsletter" 的資料；相反的，如果 checkbox 沒有被勾選，就不會有任何資料被送出。

**對於不同的 checkbox 你可以用一樣的 name 也可以用不一樣**，一樣的話，會送出像是 "subscribe=html-newsletter&subscribe=js-newsletter" 格式的資料。

* radio 選項按鈕(單選)
```
請選擇你最喜歡的顏色：<br>
<input type="radio" name="color" value="red"> red<br>
<input type="radio" name="color" value="green"> green<br>
<input type="radio" name="color" value="blue"> blue
```


radio (radio button) 是單選項按鈕，用來處理表單中有多選一時的情況，搭配 value 屬性 (預設值是 "on") 來指定當使用者選取此選項時要傳送給遠端伺服器什麼值。

**同一組 radio button 的選項，需要都是一樣的 name，所以只能選擇一項。**

* checkbox 和 radio 的 checked 屬性: 預設勾選

`<input type="checkbox" checked> Subscribe to newsletter?`

* submit button 表單的送出按鈕

`<input type="submit" value="Send Request">`

當使用者點了 submit button 就會送出表單給遠端的伺服器，用 value 屬性可以設定按鈕名稱。

* reset 重設表單狀態

`<input type="reset" value="Reset">`

reset 用來讓使用者點了可以重設表單內容回到初始狀態，而 value 屬性可以設定 reset 按鈕的名稱。

* hidden 隱藏資料欄位

`<input name="itemid" type="hidden" value="fwoxla">`

hidden 是用來當你想傳送一些值回遠端 server，但你不想或不需要讓使用者看見這些內容。

* image 圖片送出按鈕

```
<input type="image"
       src="/media/examples/login-button.png"
       alt="Login"
       width="100" height="30">
```

送出按鈕除了可以用前面提到的文字按鈕，也可以是圖片按鈕。

* 檔案上傳 (file upload)

`<input type="file" accept="image/*,.pdf">`
```
.檔案類型: 例如 .jpg, .pdf, .doc
明確指定 MIME type: 例如 image/jpeg, image/png
audio/*: 指任何聲音檔
video/*: 指任何影片檔
image/*: 指任何圖檔
```

```
<input type="file" accept="image/*,.pdf" multiple>
搭配 multiple 屬性，一次可同時選多個檔案上傳
```

* tel 電話號碼輸入欄位

`<input type="tel">`

* url 網址輸入欄位

`<input type="url">`

* email 電子郵件輸入欄位

`<input type="email">`

* date 日期輸入欄位

```
<input type="date"
       value="2020-04-20"
       min="2020-04-01"
       max="2022-04-30"
       step="5">
```
```
max: 可以輸入的最晚日期
min: 可以輸入的最早日期
step: 設定一個數字，用來控制日期元件一次跳動的幅度；或在送出表單之前，瀏覽器會對日期欄位做驗證，日期需要符合 step 設定的跳動區間
```

* time 時間輸入欄位

```
<input type="time"
       value="06:00"
       min="02:00"
       max="22:00"
       step="5">
```
```
max: 可以輸入的最晚時間
min: 可以輸入的最早時間
step: 設定一個數字，用來控制時間元件一次跳動的幅度；或在送出表單之前，瀏覽器會對時間欄位做驗證，時間需要符合 step 設定的跳動區間
```

* number 數字輸入欄位

```
<input type="number"
       step="10"
       min="0"
       max="1000">
```
```
max: 可以輸入的最大值
min: 可以輸入的最小值
step: 設定一個數字，用來控制數字元件一次跳動的幅度；或在送出表單之前，瀏覽器會對欄位做驗證，數字需要符合 step 設定的跳動區間
```

* range 數字範圍滑動選取欄位

`<input type="range" min="-10" max="10">`

* color 顏色選擇器

`<input type="color" value="#ff0000">`

#### 表單欄位驗證 (pattern validation) - pattern 屬性
text, date, search, url, tel, email 和 password 等輸入欄位可以利用 pattern 屬性搭配正規表達式 (regular expression) 來做表單欄位驗證。
`<input pattern="正規表達式">`

如果使用者輸入的內容不符合 pattern，在表單送出去之前就會被瀏覽器驗證錯誤而擋下。


```
<input type="text" pattern="[a-z]{4,8}">

<input type="time" pattern="[0-9]{2}:[0-9]{2}">

<input type="email" pattern=".+@beststartupever.com">
```

#### 下拉式選單`<select>`, `<option>`, `<optgroup>`

```
<select>
    <option>請選擇你最愛的寵物</option>
    <option>Dog</option>
    <option>Cat</option>
    <option>Hamster</option>
    <option>Parrot</option>
    <option>Spider</option>
    <option>Goldfish</option>
</select>
```

`<select>` 標籤上可以用的屬性 (attributes)
```
name: 聲明欄位名稱
disabled: 將欄位設定為禁用的狀態，是一個布林 (boolean) 屬性
required: 將欄位設定為必填，是一個布林 (boolean) 屬性
```

`<option>` 選單中的選項
```
<option> 是用來建立選項，而選項內容放在 <option></option> 標籤裡面。

<option> 標籤上有這些屬性：

value: 指定如果選了該選項，表單要傳送什麼值給遠端伺服器，如果沒設定 value，預設是送 <option> 的內容
selected: 設定預先選取此選項，是一個布林屬性
label: 說明選項的含義，有設定時會被瀏覽器顯示為選項內容，通常用來當做簡短版的選項文字
disabled: 將選項設定為不可選的狀態，是一個布林 (boolean) 屬性
```

```
<select name="pets">
    <option value="">請選擇你最愛的寵物</option>
    <option value="dog">Dog</option>
    <option value="cat" selected>Cat</option>
    <option value="hamster">Hamster</option>
    <option value="parrot">Parrot</option>
    <option value="spider" disabled>Spider</option>
    <option value="goldfish">Goldfish</option>
</select>
```
#### 可多選的選單 - `<select>` 的 multiple 和 size 屬性
```
<select name="cars" multiple>
  <option value="volvo">Volvo</option>
  <option value="bmw">BMW</option>
  <option value="saab">Saab</option>
  <option value="benz">Benz</option>
  <option value="audi">Audi</option>
</select>
```

`<select>` 的 size 屬性

size 是用來指定一次讓使用者看到幾個選項，預設值是 1；但如果有設定 multiple 時，預設值則是 4。
```
<select name="cars" multiple size="5">
  <option value="volvo">Volvo</option>
  <option value="bmw">BMW</option>
  <option value="saab">Saab</option>
  <option value="benz">Benz</option>
  <option value="audi">Audi</option>
</select>
```

`<optgroup>` 選項分區 (option group)

`<optgroup>` 可以用來將同樣性質的選項分做一區一區的來顯示，而在 `<optgroup>` 上有一個 label 屬性是用來設定該分區的名稱。
```
<select name="catordog">
  <optgroup label="Cats">
    <option>Tiger</option>
    <option>Leopard</option>
    <option>Lynx</option>
  </optgroup>
  <optgroup label="Dogs">
    <option>Grey Wolf</option>
    <option>Red Fox</option>
    <option>Fennec</option>
  </optgroup>
</select>
```

#### HTML `<button>` 表單按鈕

`<button>` 標籤 (tag) 是用來建立一個按鈕，而按鈕文字是放在 `<button></button>` 之間。

按鈕屬性:
```
name: 按鈕名稱
type: 按鈕的形式，有三種選項：
submit: 表單送出按鈕，預設值
reset: 表單內容重置按鈕.
button: 沒任何特殊功能的一般按鈕，通常配合 JavaScript 使用

value: 當 type="submit" 時，隨表單送出給遠端 server 的值
disabled: 禁用此按鈕
```
`<button type="button">Push Me</button>`

```
功能相同:
<button type="reset">Reset1</button>
<input type="reset" value="Reset2">
```

#### HTML `<label>` 表單欄位標題
`<label>` 用來給表單的控制元件一個說明標題，可以搭配 `<label>` 的像是 input, textarea, select, button, meter, output, progress 這些表單元件。
```
<div>
    <label>Do you like cheese?</label>
    <input type="checkbox">
</div>
<div>
    <label>Do you like peas?</label>
    <input type="checkbox">
</div>
```
<div>
    Do you like cheese?
    <input type="checkbox">
</div>
<div>
    Do you like peas?
    <input type="checkbox">
</div>
<br>

`<label>` 還有一個常見的用途，是**用來增加表單元件的可點擊範圍**，什麼意思呢？就是當你點 label 的文字時，等於你同時點擊了 label 關聯的表單元件。

而我們是利用 label 的 for 屬性，將 for 的屬性值設定為某表單元件的 id 值，藉此來建立關聯。
```
<label for="emailadd">Email address: </label>
<input type="email" name="emailadd" id="emailadd">
```
**點一下 "Email address" 文字，效果會等於你直接點了 input 輸入框。**

將表單元件直接包在 `<label></label>` 裡面，也可以有一樣的效果。
```
<label>Do you like peas?
  <input type="checkbox" name="peas">
</label>
```

#### HTML 表單控制元件分組 `<fieldset>`, `<legend>`
`<fieldset>` 標籤 (tag) 用來對表單 (form) 中的控制元件做分組 (group)，而 `<legend>` 標籤通常是 `<fieldset>` 裡面的第一個元素作為該分組的標題 (caption)。
```
<form>
  <fieldset>
    <legend>Personal details</legend>
    <label>Your name:</label> <input name="yourname">
    <label>Your age:</label> <input type="number" name="yourage">
  </fieldset>

  <fieldset>
    <legend>Your address</legend>
    <label>Street:</label> <input name="street">
    <label>Zip code / post code:</label> <input name="postcode">
  </fieldset>
</form>
```

### HTML `<div>` 區塊容器元素

`<div>` 標籤 (tag) 是用來當作容器 (container)，用來包裹其他 HTML，將 HTML 文件的內容整理出不同獨立區塊 (block)，用途是方便給 CSS 做樣式排版或方便給 JavaScript 做互動操作，至於 `<div>` 本身沒任何特殊意義也不帶任何標籤語意。

```
<div class="shadowbox">
  <p>paragraph 1</p>
  <p>paragraph 2</p>
  <p>paragraph 3</p>
</div>
```
我們將好幾個段落用 `<div>` 包在一起，在 `<div>` 上加個 id 或 class 屬性，就可以直接在這三個段落外面加上一個陰影框啦：

```
.shadowbox {
  width: 15em;
  border: 1px solid #333;
  box-shadow: 8px 8px 5px #444;
  padding: 8px 12px;
  background-image: linear-gradient(180deg, #fff, #ddd 40%, #ccc);
}
```
> div 主要是用作區塊 (block) 容器，如果是包裹單一行內 (inline) 的情況，則是使用 span。

### HTML `<span>` 行內容器
`<span>` 標籤 (tag) 是用來當作容器 (container)，用來包裹文字 (text) 或其他行內 (inline) 的 HTML，用途是方便給 CSS 做樣式排版或方便給 JavaScript 做互動操作，至於 `<span>` 本身沒任何特殊意義也不帶任何標籤語意。

`<p>My mother has <span class="highlight">blue</span> eyes.</p>`

我們將 blue 這句文字用 `<span>` 包著，在 `<span>` 上加個 id 或 class 屬性，就可以對這個 span 裡面的內容設定不同樣式啦：
```
.highlight {
  color: blue;
}
```

### HTML `<strong>` 強調重要性
`<strong>` 標籤 (tag) 其語意 (semantic) 是用來強調一段內容特別重要 (strong importance for its contents)！瀏覽器預設的 strong 樣式也是會用粗體字顯示。

`<p>When doing x it is <strong>imperative</strong> to do y before proceeding.</p>`

> `<b>` 標籤雖然也會將包裹的內容文字變成是粗體字的效果，但 `<b>` 僅止於樣式的用途，標籤本身沒有任何語意，不像是 `<strong>` 有特殊語意表示內容的重要性，所以 `<strong>` 和 `<b>` 標籤對於 SEO 搜尋引擎理解網頁內容是有極大的根本性差異的。通常也會建議少用`<b>`，如果真的想用粗體字效果的話，其實你應該使用 CSS。


### HTML `<em>` 對內容著重強調 (emphasis)
`<em>` 標籤 (tag) 其語意 (semantic) 是用來強調 (emphasis) 讀者留意著重閱讀某一段內容，而瀏覽器預設 em 的樣式是會用斜體字顯示。
```
<p>
  In HTML 5, what was previously called <em>block-level</em> content is now called <em>flow</em> content.
</p>
```
> `<i>` 標籤雖然也會將包裹的內容文字變成是斜體字的效果，但 `<i>` 標籤本身沒有任何語意，不像是 `<em>` 有特殊語意表示對內容的著重強調，所以 `<em>` 和 `<i>` 標籤對於 SEO 搜尋引擎理解網頁內容是有根本性差異的。通常也會建議少用 `<i>`，如果真的想用斜體字效果的話，其實你應該使用 CSS

### HTML `<mark>` 突顯高亮文字
`<mark>` 標籤 (tag) 用來突顯或高光 (highlight) 一段文字，目的是讓這段文字可以在它的上下文中被突顯出來，例如可以用來在搜尋結果中突顯搜尋關鍵字，而瀏覽器預設會用語法高亮的樣式顯示被 mark 住的文字。

`<p>mark 元素用於<mark>高亮</mark>突顯內容</p>`

> `<mark>` 和`<strong>` 標籤語意上的差別在於，strong 是強調內容在上下文中的重要性，而 mark 是用來突顯內容和上下文的關聯性。

### HTML `<hr>` 水平分隔線
`<hr>` 標籤本身的語意是用來做文字段落的焦點或場景轉換 (thematic break)，視覺效果上則是一條水平分隔線。

> `<hr>` 本身沒有內容是一個空元素，所以不需要 closing tag。

### HTML `<code>` 顯示程式碼內容
`<code>` 標籤 (tag) 用來顯示電腦程式碼 (computer code) 內容，而瀏覽器預設會以 monospace 等寬字型 (fixed-width font) 來顯示 `<code>` 中的內容。

`<p>Regular text. <code>This is code.</code> Regular text.</p>`