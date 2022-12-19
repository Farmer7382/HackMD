# 基礎Java


### 方法大全

#### Integer & String 轉換
```
//通常方法名是什麼，就返回什麼

#Integer i = new Integer(123); //boxing

#int x = i.intValue(); //unboxing


Number y;

int z = y.intValue();


#Integer x = Integer.valueOf("123"); //字串轉Integer物件

#int y = Integer.parseInt("456"); //字串轉int


#String z = String.valueOf(789) //數字轉字串 [可將各種型態轉為字串，推薦使用]

#String z = Integer.toString(789); //數字轉字串


example:
String num;.
Integer.parseInt(num);  //return int
Integer.valueOf(num).intValue();  //return int
```
#### String方法
```
str.length() //返回字串長度

str.charAt(n) //返回索引值n的字元，不存在則返回空字串

str.indexOf(字串s,開始索引值n) //返回字串首次出現位置索引值，從索引值n開始查詢，不存在則回傳-1
str.lastIndexOf(字串s,開始索引值n) //返回字串最後出現位置索引值，從索引值n開始查詢，不存在則回傳-1

str.substring(索引值n,索引值m) //返回從索引值n到(m-1)之間的字元，m可省略表示擷取到最後

str.replace(字串r,字串s) //將原字串中的r替換成s

str.trim() //返回一個去除開頭與結尾的所有空白字元字串

str.toUpperCase() //將字串轉大寫
str.toLowerCase() //將字串轉小寫

str1.concat(str2) //字串相加

str1.contains("some str") //是否包含

str.isEmpty() //是否為空 

str.split(字串s) //以字串s切割原字串，並返回n個子字串的陣列(分割)

註:
. 、 $、 | 和 * 等轉義字符，必须得加 \\。
str.split("\\.")
```
```
[需import org.apache.commons.lang3.StringUtils]

#boolean isBlank(String str)
//判斷某字串是否為空或長度為零或由空白構成。
//等於把空白先trim掉再判斷

#boolean isNotBlank(String str)
//判斷某字串是否為空或長度為零或由空白構成。等於!isBlank(String str)
//等於把空白先trim掉再判斷


#boolean isEmpty(String str)
//判斷某字串是否為空，判斷依據為str==null或str.length()==0

#boolean isNotEmpty(String str)
//判斷某字串是否不為空，等於!isEmpty(String str)


example:
StringUtils.isBlank(" "); //true
StringUtils.isEmpty(" "); //false
```
```
//char可以和數字相比較
//使用charAt出來的==比較是比ASCII

String x = "123";
System.out.println(x.charAt(0)); //1
System.out.println(x.charAt(0)==49); //true
                                     
                                    
char x = 'a';
System.out.println(x == 97); //true
System.out.println((int) x == 97); //true                              
```
```
//char陣列轉字串
//字串轉char陣列

public class Draft {
    public static void main(String[] args) {

        char[] cs1 = {'a','p','p','l','e'};

        String fruit = new String(cs1);
        System.out.println(fruit);

        char[] cs2 = fruit.toCharArray();
        System.out.println(Arrays.toString(cs2));
    }
}


//apple
//[a, p, p, l, e]
```
#### Math方法
```
Math.min(值1,值2,...) //傳回參數列的最小值
Math.max(值1,值2,...) //傳回參數列的最大值

Math.random() //傳回一個介於0~1之間的亂數

Math.round(x) //將x值四捨五入 =SQL的ROUND

Math.ceil(x) //傳回一個大於或等於x的最小整數(無條件進位)
Math.floor(x) //傳回一個小於或等於x的最大整數(無條件捨去) =SQL的TRUNC
Math.ceil(2.321) //3
Math.floor(2.321) //2
Math.PI //圓周率
Math.pow(x,y) //x的y次方
Math.sqrt(x) //x的平方根
Math.abs(x) //x的絕對值
```
```
//Math.round負值為五捨六入

System.out.println(Math.round(-0.5)); //0
System.out.println(Math.round(-1.5)); //-1
System.out.println(Math.round(-2.5)); //-2

System.out.println(Math.round(-0.6)); //-1
System.out.println(Math.round(-1.6)); //-2
System.out.println(Math.round(-2.6)); //-3
```
#### 未分類方法
```
//instanceof可以向下比較

public class Draft {
    public static void main(String[] args) {

        Object x = 123;
        Object y = new Integer(222);
        System.out.println(x instanceof Number); //true
        System.out.println(y instanceof Number); //true

    }
}

//如果是繼承關係時，只能SonInstance instanceof FatherClass
```
```
//接收型別宣告為Object，可以向下接收所有的型別

public  class Test1 {
    public boolean isEmpty(Object obj){
        boolean check = false;
        if(obj == null || obj.equals("")){
            check = true;
        }
        return check;
    }
}
```
### 方法基本觀念
```
1. 方法一定要放在某個類別裡面。

2. 方法宣告都是獨立分開的，不可以在一個方法內又宣告另一個方法，但可以呼叫。

3. 同一個class內，兩個不同方法，可直接在A方法內調用B方法，不用new新物件。

4. 只能在方法內調用(呼叫)其他方法。 方法內包了另一個方法。

5. 靜態方法不用new物件即可直接使用。(在同類別直接打 方法名 使用)(在不同類別用 靜態方法所在類別名.方法名 使用)

6. 非靜態方法(在同類別直接打 方法名 使用)(在不同類別用 物件名.方法名 使用)

7. static方法不可使用this，因為this代表物件。

8. static方法只能存取static方法和變數。 (要存取non-static方法就必須先new出物件。)

9. non-static方法可以存取non-static and static方法和變數。

10. 父類別有的方法，子類別就算沒有覆寫也能直接拿來用。

11. function scope，變數一離開方法就被消滅釋放，無法使用。

12. 方法內遇到return = 中斷跳出方法
```

### this關鍵字
```
this指的是這一個物件，指屬性或方法在哪個物件下被呼叫，this就是屬於這個呼叫的物件。

看這個this寫在哪個類別裡面，就是代表這個類別的物件。

實體變數由物件各自獨立維護，彼此不受干擾。
```

### Getter / Setter
```
// 在同一個class下，可直接存取(任何封裝修飾)的實體變數以及使用(任何封裝修飾)的Getter/Setter方法。
// 在不同class下，只能存取(合宜封裝修飾)的實體變數以及(合宜封裝修飾)的Getter/Setter方法。

// .可用於Get or Set，但不管是不是同類別，都必須是。物件名/類別名.變數名。

// 不同class必須要new物件出來才能使用(合宜封裝修飾)的Getter/Setter 以及 .。

// New物件之後使用get / set方法，只能寫在方法內，直接寫在類別底下會報紅字。

// 可覆寫toString方法來列印物件，否則只會印出記憶體位置。


public class Test {

    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public static void main(String[] args) {

        Test tt = new Test();
        tt.name = "Tom";
        tt.age = 18;
        
        tt.setName("Mark");
        tt.setAge(20);

        System.out.println(tt);
        
    }
    
    public String toString(){
        return this.name+" "+this.age+" years old";
    }
    
 
    
    class abc {
        Test a = new Test();
        a.setAge(20); //只能在方法內調用(呼叫)其他方法。
                      //無法運行，會報紅字。
    }  
}
```
```
public class Test1 {
    public static void main(String[] args) {

        Test tt2 = new Test();

        tt2.setName("Tom");
        tt2.setAge(18);

        System.out.println(tt2);
    }
}
```

```
//.可用於Get or Set，但前面必須有物件名 or 類別名

public static void main(String[] args) {

    Material mm = new Material();
    mm.salary=100; //set 100
    System.out.println(mm.salary); //get 100
       
}
```
```
//類別名可直接. 靜態方法/靜態變數

public class Draft {
    private static int num = 20;

    public static void main(String[] args) {
        Draft.num=100; //set 100
        System.out.println(Draft.num); //get 100
        Draft.run();
    }
    
    static void run(){
        System.out.println("run");
    }
    
}
```
### 調用方法原理
```
// 同一個class內，兩個不同方法，可直接在A方法內調用B方法，不用new新物件。
   (non-static 調用 non-static/static)


public class PLEH001Action extends ASIAction
{

    public String[] getLicenseList() {
        return licenseList;
    }


    public String query() throws Exception {
        String[] bbb = getLicenseList();
    }

}
```
```
// 可直接調用

public class Method {

    public void run(){
        System.out.println("run");
    }

    public void sport(){
        run();
    }
   
}
```
```
// 要new物件來調用方法也可以

public class Method {

    public void run() {
        System.out.println("run");
    }
    
    
        Method mm = new Method();
    
        public void sport() {
            mm.run();
            
    }
}
```
```
// 子類別內部也可直接調用

public class Method {

    public void run() {
        System.out.println("run");
    }


    class Method2 {

        public void sport() {
            run();    
        }   
    }
    
}
```
### 淺拷貝 & 深拷貝

#### List的淺拷貝方法
1. 遍歷循環復制
```
List<Person> destList=new ArrayList<Person>(srcList.size());  

for(Person p : srcList){  
    destList.add(p);  
}  
```
2. 使用List的構造方法
```
List<Person> destList=new ArrayList<Person>(srcList);  
```
3. 使用list.addAll()方法
```
List<Person> destList=new ArrayList<Person>();  

destList.addAll(srcList);  
```

#### 陣列的淺拷貝方法
```
int[] x = {1,3,5};

int[] y = x.clone();

int[] z = Arrays.copyOf(x,3); //後者為新陣列長度
```

#### 使用 = 複製 (範例)

> 因陣列是物件，故直接指向過去給另一個新陣列等於是傳址，a、b會指向同一個記憶體位置，所以不管值怎麼變化，a和b拿到的值會相同。

> 淺拷貝 (因相同記憶體位置，故更改後會拿到相同的值)
```
public class Copy {
    public static void main(String[] args) {

        int[] a ={1,3,5};
        int[] b = new int[3];
        b = a;

        a[0] = 999;

        for(int x : a){
            System.out.print(x+"\t");
        } //999 3 5

        System.out.println();

        for(int x : b){
            System.out.print(x+"\t");
        } //999 3 5
    }
}
```
```
<script type="text/javascript">

var a = new Array(1,3,5);
var b = new Array();
var b = a;

console.log(a); //[1,3,5]
console.log(b); //[1,3,5]

a[0] = 999;

console.log(a); //[999,3,5]
console.log(b); //[999,3,5]

</script>>
```
#### 使用方法複製 (淺拷貝範例)
> 基本型別 (以陣列的clone方法、或copyOf方法運作,複製的就是陣列裡存放的值)

> 基本型別都是以傳值方式進行變數的傳遞
> 
> a 和 b 是存在於兩個獨立不同的記憶體位置中

> 使用String也會出現此結果!
```
public class Copy {
    public static void main(String[] args) {

        int[] a ={1,3,5};
        int[] b = new int[3];
//        b = a.clone();
        b = Arrays.copyOf(a,3);

        a[0] = 999;

        for(int x : a){
            System.out.print(x+"\t");
        } //999 3 5

        System.out.println();

        for(int x : b){
            System.out.print(x+"\t");
        } //1 3 5
    }
}
```
> 類別型別 (以陣列的clone方法、或copyOf方法運作,只有複製到物件的參考(位址)而已)

> 類別型別都是以傳址方式進行變數的傳遞
> 
> a 和 b 是指向相同的記憶體位置
```
public class TestShallowCopy {

    public static void main(String[] args) {

        Animal a1 = new Animal(2, 5.0f);
        Animal a2 = new Animal(5, 15.0f);
        Animal[] as = new Animal[2];
        
        as[0] = a1;
        as[1] = a2;
		
        Animal[] as2 = as.clone();
		
        as[0].setAge(10); //資料被修改了, 因為都是相同的記憶體空間

        System.out.println(as[0].getAge()); //10
        System.out.println(as2[0].getAge()); //10
    }
}
```

```
public class Animal {

    private int age;
    private float weight;
	
    public Animal() {
    // 1. 讓繼承的子類別建構子設計較為彈性
    // 2. 留著無參數建構子是為了搭配日後接觸到的"框架(framework)"使用
    }
	
    public Animal(int age, float weight) {
        this.age = age;
        this.weight = weight;
    }
	
    public void speak() {
        System.out.println("Age is = " + age);
        System.out.println("Weight is = " + weight);
    }
	
    public int getAge() {
        return age;
    }
	
    public void setAge(int age) {
        this.age = age;
    }
	
    public float getWeight() {
        return weight;
    }
	
    public void setWeight(float weight) {
        this.weight = weight;
    }
}
```

#### 深拷貝範例1
> 基本型別都是複製值，只有類別型別才會有深拷貝。

> 各自獨立
```
public class TestDeepCopy {

    public static void main(String[] args) {

        Animal a1 = new Animal(2, 5.0f);
        Animal a2 = new Animal(5, 15.0f);
    
        Animal[] as = new Animal[2];
        as[0] = a1;
        as[1] = a2;
		
        // 創建一個陣列, 到時候將複製好的Animal物件放入
        Animal[] as2 = new Animal[as.length];
    
        for (int i = 0; i < as.length; i++) {
    
            Animal originalAnimal = as[i]; //先從原本陣列取出要複製的Animal物件 
        
            Animal newAnimal = new Animal(); //new一個Animal物件 (才會是不同的記憶體空間)
        
            int age = originalAnimal.getAge(); //取出原本Animal物件的值
            float weight = originalAnimal.getWeight();
        
            newAnimal.setAge(age); //將值設定到剛創建出來的Animal物件裡
            newAnimal.setWeight(weight);

            as2[i] = newAnimal; //放進新的陣列裡
    }		
            as[0].setAge(10);
		
        //兩個陣列都是放著Animal物件, 但都是不同的記憶體空間, 因此不會有修改的情況發生
        System.out.println(as[0].getAge()); //10
        System.out.println(as2[0].getAge()); //2		
    }
}
```
#### 深拷貝範例2
```
class Clothes2 {
    String color;
    char size;

    Clothes2(String color, char size) {
        this.color = color;
        this.size = size;
    }
}

public class DeepCopy {
    public static void main(String[] args) {
    
        Clothes2[] c1 = {new Clothes2("red", 'L'), new Clothes2("blue", 'M')};
        var c2 = new Clothes2[c1.length];

        for (var i = 0; i < c1.length; i++) {
            c2[i] = new Clothes2(c1[i].color, c1[i].size);
        }

        c1[0].color = "yellow";
        System.out.println(c1[0].color);
        System.out.println(c2[0].color);
    }
}

//yellow
//red
```


### 流程控制的變數作用域
> 在if、for、while、do-while、try裡面定義的變數，無法在外面使用。

> 和方法內變數離開方法就消滅一樣。

> 所以不要在if、for、while、do-while、try裡面定義變數，改在外面宣告、定義，並且要給定初始值。(因為是區域變數)

> if、for、while、do-while、try區塊內可以賦值給宣告在外面的區域變數。
```
//if錯誤

public class Draft {
    public static void main(String[] args) {

        if (1 == 1) {
            int x = 5;
        }

        System.out.println(x); //報錯

    }
}
```
```
//if錯誤

public class Draft {
    public static void main(String[] args) {

        int x;

        if (1 != 1) {
            x = 5;
        }

        System.out.println(x); //x沒有初始化，報錯

    }
}
```
```
//if正確

public class Draft {
    public static void main(String[] args) {

        int x;  //if區塊內可以賦值給宣告在外面的區域變數
        
        if (1 == 1) {
            x = 5;
        }
        
        System.out.println(x); //5

    }
}
```
```
//for錯誤

public class Draft {
    public static void main(String[] args) {

        for (int i = 0; i < 10; i++) {
            int x = 5;
        }

        System.out.println(x); //報錯

    }
}
```
```
//for錯誤

public class Draft {
    public static void main(String[] args) {

        int x;
        
        for (int i = 0; i < 10; i++) {
            x = 5;
        }

        System.out.println(x); //x沒有初始化，報錯

    }
}
```
```
//for正確

public class Draft {
    public static void main(String[] args) {

        int x = 0;
        
        for (int i = 0; i < 10; i++) {
            x = 5;
        }

        System.out.println(x); //5

    }
}
```
```
//while錯誤

public class Draft {
    public static void main(String[] args) {

        int x = 0;
        
        while (x < 3) {
            int y = 5;
        }
        
        System.out.println(y); //報錯

    }
}
```
```
//while錯誤

public class Draft {
    public static void main(String[] args) {

        int x = 0;
        int y;
        
        while (x < 3) {
            y = 5;
        }
        System.out.println(y); //y沒有初始化，報錯

    }
}
```
```
//while正確

public class Draft {
    public static void main(String[] args) {

        int x = 0;
        int y = 0;
        
        while (x < 3) {
            y = 5;
            x++;
        }
        System.out.println(y); //5

    }
}
```

### if宣告變數
```
//success

public class ABC {
    public static void main(String[] args) {

        if (1 == 1) {
            int x = 5;
        }
        
        int x = 3;

    }
}


//failure

public class ABC {
    public static void main(String[] args) {

        int x = 3;

        if (1 == 1) {
            int x = 5;
        }
    }
}

```

### enum

> enum類別可以單獨宣告或是宣告在其他類別裡面。

> enum可以不用new物件，也無法new，直接取用方法。


> Enum也是類別的一種(所以編譯後會產生class檔)，但是其建構子為 private  所以無法從外部使用，只能在Enum內使用，所以無法從外部產生新的物件。

> Enum的方法會自動設為靜態方法，所以其只能存取靜態成員。

> 標準的單例模式實現


單獨宣告：

* 簡單列舉
```
如果列舉不新增任何方法，列舉值預設為從0開始的有序數值。以 Color 列舉型別舉例，它的列舉常量依次為RED：0，GREEN：1，BLUE：2

enum Color { RED, GREEN, BLUE }
```
* 列舉方法
```
values()：返回enum例項的陣列，而且該陣列中的元素嚴格保持在enum中宣告時的順序。

name()：返回例項名。

ordinal()：返回例項宣告時的次序，從0開始。

getDeclaringClass()：返回例項所屬的enum型別。

equals()：判斷是否為同一個物件。
```
* 方法應用範例1
```
public class EnumMethodDemo {

enum Color {RED, GREEN, BLUE;}
enum Size {BIG, MIDDLE, SMALL;}

public static void main(String args[]) {
System.out.println("=========== Print all Color ===========");

for (Color c : Color.values()) {
System.out.println(c   " ordinal: "   c.ordinal());
}
System.out.println("=========== Print all Size ===========");

for (Size s : Size.values()) {
System.out.println(s   " ordinal: "   s.ordinal());
}

Color green = Color.GREEN;

System.out.println("green name(): "   green.name());
System.out.println("green getDeclaringClass(): "   green.getDeclaringClass());
System.out.println("green hashCode(): "   green.hashCode());
System.out.println("green compareTo Color.GREEN: "   green.compareTo(Color.GREEN));
System.out.println("green equals Color.GREEN: "   green.equals(Color.GREEN));
System.out.println("green equals Size.MIDDLE: "   green.equals(Size.MIDDLE));
System.out.println("green equals 1: "   green.equals(1));
System.out.format("green == Color.BLUE: %b\n", green == Color.BLUE);
}
}
```
```
=========== Print all Color ===========
RED ordinal: 0
GREEN ordinal: 1
BLUE ordinal: 2
=========== Print all Size ===========
BIG ordinal: 0
MIDDLE ordinal: 1
SMALL ordinal: 2
green name(): GREEN
green getDeclaringClass(): class org.zp.javase.enumeration.EnumDemo$Color
green hashCode(): 460141958
green compareTo Color.GREEN: 0
green equals Color.GREEN: true
green equals Size.MIDDLE: false
green equals 1: false
green == Color.BLUE: false
```

* 方法應用範例2
```
class TestEnum6 {

    enum Week{

        Sunday("星期天", 3), Monday("星期一", 8), Tuesday("星期二", 7), Wednesday("星期三", 2.5),
        Thursday("星期四", 6), Friday("星期五", 2), Saturday("星期六", 3.5);

        private String msg;
        private double discount;

        private Week(String msg, double discount){
            this.msg = msg;
            this.discount = discount;
        }

        public String format(){
            return msg + "的折扣是" + discount + "折";
        }

        public double test(){
            return discount;
        }

    }

    public static void main(String[] arg){
        System.out.println(Week.Sunday.format()); //星期天的折扣是3.0折
        System.out.println(Week.Monday.format()); //星期一的折扣是8.0折
        System.out.println(Week.Tuesday.format()); //星期二的折扣是7.0折

        System.out.println(Week.Friday.msg); //星期五
        System.out.println(Week.Friday.discount); //2.0

        System.out.println(Week.Wednesday.test()); //2.5
        
        
        for(Week x: Week.values()){
            System.out.println(x.msg+" "+x.discount);
        } //星期天 3.0 星期一 8.0 星期二 7.0 星期三 2.5 星期四 6.0......
        
    }
}
```
* 方法應用範例3
```
public enum EnumTest {

    fruit1("Apple","Red"),fruit2("Banana","Yellow");

    public String name;
    public String color;

    private EnumTest(String name,String color) {
        this.name = name;
        this.color = color;
    }

    public static void main(String[] args) {
        
        System.out.println(EnumTest.fruit1.name); //Apple
        System.out.println(EnumTest.fruit1.color); //Red
        
    }
}
```

* 專案實作
```
//實體變數宣告為public，別的class才能存取。

public enum SysEnum {

	/**
	 * 狀態碼-失敗
	 */
	statusError("999", "error"),
	/**
	 * 狀態碼-成功
	 */
	statusSuccess("000", "success"),
	/**
	 * 狀態碼-正常執行完畢
	 */
	statusFinish("finish", "process_finish"),
	/**
	 * 狀態碼-正常執行完畢
	 */
	statusBroken("broken", "process_have_serious_error"),

	public String code;
	public String context;

	private SysEnum(String code, String context) {
		this.code = code;
		this.context = context;
	}
}
```
```
//取值

SysEnum.statusSuccess.context
```


### Lambda
1. Runnable
```
public class Test {
    public static void main(String[] args) {

        Runnable run = new Runnable() {
            @Override
            public void run() {
                System.out.println("old run");
            }
        };
        run.run();


        //Lambda寫法
        Runnable run1 = () ->     System.out.println("lambda run");
        run1.run();
    }
}
```

2. forEach
```
public class Test {
    public static void main(String[] args) {

        //使用兩種方法建立集合，以下三個方法皆可取值
        List features = Arrays.asList("Lambdas", "Default Method", "Stream API", "Date and Time API");
        
        List features = new ArrayList();
        features.add("Lambdas");
        features.add("Default Method");
        features.add("Stream API");
        features.add("Date and Time API");
        
              
        //三個方法皆可走訪全部元素
        features.forEach(n -> System.out.println(n));
        
        features.forEach(System.out::println);
        
        for(Object x : features){
            System.out.println(x);
        }
    }
}

註:陣列方法Arrays.asList可快速構建一個List，但此List沒有辦法操作add和remove等方法。
註:Returns a fixed-size list backed by the specified array.
```
2. 補充說明Arrays.asList
```
生成的List的長度是固定的；能夠進行修改操作（比如，修改某個位置的元素），但
不能執行影響長度的操作（如add、remove等操作）。會丟擲UnsupportedOperationException異常。

X錯誤操作:
List<String> array1 = Arrays.asList("Welcome", "to","Java", "world");
array1.add("Cool~~~");
//Exception in thread "main" java.lang.UnsupportedOperationException


O解決方法:
List<String> array1 = new ArrayList<>(Arrays.asList("Welcome", "to", "Java", "world"));
array1.add("Cool~~~");
```


3. IntStream
```
//印出零到九的數字
IntStream.range(0, 10).forEach(i -> System.out.println(i));

IntStream.range(0, 10).forEach(System.out::println);
```

4. filter
```
public class Test {
    public static void main(String[] args) {
        
        List names = Arrays.asList("Java", "Scala", "C++", "Haskell", "Lisp","Jdbc");
        
        Predicate<String> startsWithJ = (n) -> n.startsWith("J");
        Predicate<String> fourLetterLong = (n) -> n.length() == 4;
        
        names.stream()
                .filter(startsWithJ.and(fourLetterLong))
                .forEach((n) -> System.out.println("nName, which starts with 'J' and four letter long is : " + n));
    }
}
```
### 反射

#### 實作範例1
> 動態由傳入的變數來決定new的物件

> Java的反射機制是在編譯並不確定是哪個類被載入了，而是在程式執行的時候才載入、探知、自審。使用在編譯期並不知道的類。這樣的特點就是反射。

> 假如我們有兩個程式設計師，一個程式設計師在寫程式的時候，需要使用第二個程式設計師所寫的類，但第二個程式設計師並沒完成他所寫的類。那麼第一個程式設計師的程式碼能否通過編譯呢？這是不能通過編譯的。利用Java反射的機制，就可以讓第一個程式設計師在沒有得到第二個程式設計師所寫的類的時候，來完成自身程式碼的編譯。

```
public class Draft {
    public static void main(String[] args) {

        String str = "Practice.ABC"; //DB tableName
        String set = "setName";
        String get = "getName";

        try {
            Class c = Class.forName(str);
            Object obj = c.newInstance();

            Method m1 = c.getMethod(set, String.class);
            Method m2 = c.getMethod(get);

            m1.invoke(obj, "Tom");
            String result = (String) m2.invoke(obj);

            System.out.println(result);

        } catch (ClassNotFoundException e) {
            System.out.println("ClassNotFoundException");
        } catch (IllegalAccessException e) {
            System.out.println("IllegalAccessException");
        } catch (InstantiationException e) {
            System.out.println("InstantiationException");
        } catch (NoSuchMethodException e) {
            System.out.println("NoSuchMethodException");
        } catch (InvocationTargetException e) {
            System.out.println("InvocationTargetException");
        }
    }
}

//Tom
```
#### 實作範例2
```
public class Draft {
    public static void main(String[] args) {

        String str = "Practice.ABC";
        String set = "setName";
        String get = "getName";
        String[] name = {"Tom", "Jack", "Mike"};
        ArrayList nameList = new ArrayList();

        try {
            Class c = Class.forName(str);
            Object obj = null;

            for (int i = 0; i < 3; i++) {
                obj = c.newInstance();

                Method m1 = c.getMethod(set, String.class);
                Method m2 = c.getMethod(get);

                m1.invoke(obj, name[i]);

                String result = (String) m2.invoke(obj);

                nameList.add(result);
            }

            System.out.println(nameList);

        } catch (ClassNotFoundException e) {
            System.out.println("ClassNotFoundException");
        } catch (IllegalAccessException e) {
            System.out.println("IllegalAccessException");
        } catch (InstantiationException e) {
            System.out.println("InstantiationException");
        } catch (NoSuchMethodException e) {
            System.out.println("NoSuchMethodException");
        } catch (InvocationTargetException e) {
            System.out.println("InvocationTargetException");
        }
    }
}

//[Tom, Jack, Mike]
```
#### 使用反射導致@Autowired失效解法
> 在运行中发现采用反射方式调用会导致实现类中@value以及@Autowired注解失效，对应注解值都为null。

> 原因：因为在调用invoke反射方法时，Class是直接使用newInstance静态方法来实例化对象。所导致对应@value、@Autowired等注解失效。

> PS：Spring的注解是在Spring实例化的时候扫描注入，当Spring实例化完毕之后如果再去newInstance一个新的对象显然是不受Spring管理了，所以相应的注解都是注入为null。


```
@Service
public class UserService {

	@Autowired
    private UserMapper userMapper;
	
	//新增代码 开始   注意此段
	public static UserService dynamicProxy;
	
	@PostConstruct
	public void init() {  
		System.out.println("userMapper init");  
			dynamicProxy = this;
	} 
	//新增代码 结束
	
	public List<User> queryList() {
		System.out.println("Row22.UserService="+dynamicProxy.userMapper);
		List<User> users=dynamicProxy.userMapper.queryList();
        return users;
    }
	
	public String GetNameByID(int ID) {
		String temp=userMapper.GetNameByID(ID);		
        return temp;
    }
}
```
### 讀txt檔案(搬檔及刪除)
```
//使用renameTo方法，可更改檔名/移動檔案，但Linux系統有時會失敗

//注意:txt中文在檔案中佔兩位，讀進javaCode只佔一位。注意SPEC的index如果是txt的內容位置，需另外過老李轉換檔。

public class Draft {
    public static void main(String[] args) throws IOException {

        String sourcePath = "D:\\data\\source";
        String successDestPath = "D:\\data\\success";
        String failDestPath = "D:\\data\\failed";

        //path only
        File file = new File(sourcePath); 
        String[] fileNameList = file.list();

        for (int i = 0; i < fileNameList.length; i++) {

            //path + filename
            File toBeRenamed = new File(sourcePath + "\\" + fileNameList[i]);
            String oriFileName = fileNameList[i].split("\\.")[0];
            File newFile = new File(sourcePath + "\\" + oriFileName + "_test" + ".txt");

            //搬移檔案
            toBeRenamed.renameTo(newFile);
            
            
            //可用此複製方法取代renameTo
            FileUtils.copyFile(toBeRenamed, newFile);
            
            //但此方法需再自行刪除原始檔案
            FileUtils.forceDelete(toBeRenamed);
        }
    }
}
```
```
public class Draft1 {
    public static void main(String[] args) throws IOException {

        File file = null;
        BufferedReader br = null;
        String successFlag = "";
        InputStreamReader reader = new InputStreamReader(
                new FileInputStream("D:\\data\\source\\CAF_461表二.txt"),"big5");
        br = new BufferedReader(reader);

        String line = "";
        while (line != null) {
            line = br.readLine(); // 一次讀入一行資料
            if (line == null || line.isBlank()) {
                continue;
            } else {
                System.out.println(line);
            }
        }
    }
}
```
### 讀txt檔案(判斷UTF-8/Big5)
```
	public List<String> realTxtCsvData(MultipartFile multipartFile) throws Exception {
		List<String> lineList = new ArrayList<String>();

		File file = multipartFileconvertToFile(multipartFile);
		boolean resutBoolean = determinFilecoding(file);
		InputStreamReader reader = null;
		if (resutBoolean) {
			reader = new InputStreamReader(multipartFile.getInputStream(), "UTF-8"); // 建立一個輸入流物件reader
		} else {
			reader = new InputStreamReader(multipartFile.getInputStream(), "Big5"); // 建立一個輸入流物件reader
		}
		BufferedReader br = new BufferedReader(reader); // 建立一個物件，它把檔案內容轉成計算機能讀懂的語言
		String line = "";
		while (line != null) {
			line = br.readLine(); // 一次讀入一行資料
			if (CommonFunction.checkNotNull(line)) {
				lineList.add(line);
			}

		}
		reader.close();
		br.close();
		return lineList;
	}
```
```
	public boolean determinFilecoding(File file) {
		boolean result = false;
		try {
			FileInputStream in = new java.io.FileInputStream(file);
			byte[] b = new byte[3];
			in.read(b);
			in.close();
			if (b[0] == -17 || b[1] == -69 || b[2] == -65) {
				result = true;
			}
		} catch (Exception e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		return result;
	}
```

### 使用java產出Excel
```
@Lazy
@Api(tags = "FBDM6666 JAVA產生Excel測試")
@RequestMapping("FBDM6666")
@RestController
public class ExcelController {
	private static Logger log = LogManager.getLogger(ExcelController.class);
	private Workbook workbook;
	private CreationHelper creationHelper;
	private String dateFormat;

	@Autowired
	private CreateexcelsetupService createexcelsetupService;

	@Autowired
	private TempdataService tempdataService;

	@PostMapping(value = "/ExportExcel")
	@ResponseBody
	public ResponseEntity<Object> ExportExcel(@RequestHeader(value = "Authorization", required = true) String token)
			throws Exception {
		JsonBean jsonBean = new JsonBean();

		try {

			String filename = "D:/data/NewExcelFile.xls";
			HSSFWorkbook workbook = new HSSFWorkbook();
			HSSFSheet sheet = workbook.createSheet("FirstSheet");

			Createexcelsetup createexcelsetup = new Createexcelsetup();
			createexcelsetup.setType("SpeCommission");
			createexcelsetup.setIdentification("086A");
			List<Createexcelsetup> CreateexcelsetupList = createexcelsetupService
					.queryByCreateexcelsetup(createexcelsetup);

			LinkedHashMap<String, String> titleMap = new LinkedHashMap<>();
			for (Createexcelsetup element : CreateexcelsetupList) {
				titleMap.put(element.getCloumnid(), element.getChinesecloumn());

			}

			List<String> fieldList = new ArrayList<String>(titleMap.keySet());

			List<?> dataList = tempdataService.queryAll();

			for (int i = 0; i <= dataList.size(); i++) {

				Row row = sheet.createRow(i);

				for (int j = 0; j < fieldList.size(); j++) {

					Cell cell = row.createCell(j);
					if (i == 0) {
						cell.setCellValue(titleMap.get(fieldList.get(j)));
					} else {
						Object data = dataList.get(i - 1);
						Object fieldValue = PropertyUtils.getNestedProperty(data, fieldList.get(j));
						this.setCellValueByType(fieldValue, cell);
					}
				}
			}

			FileOutputStream fileOut = new FileOutputStream(filename);
			workbook.write(fileOut);
			fileOut.close();
			workbook.close();
			System.out.println("Your excel file has been generated!");

		} catch (Exception e) {
			log.debug(e.toString());
			Arrays.asList(e.getStackTrace()).stream().forEach(sube -> log.debug(sube.toString()));
			jsonBean.setData("");
			jsonBean.setStatus(SysEnum.statusError.code);
			jsonBean.setMessage("新增資料失敗!");
			return new ResponseEntity<>(jsonBean, HttpStatus.INTERNAL_SERVER_ERROR);
		}
		return new ResponseEntity<>(jsonBean, HttpStatus.OK);
	}

	public void setCellValueByType(Object data, Cell cell) {

		if (data instanceof Number) {
			Double convert = Double.parseDouble(data.toString());
			cell.setCellValue(convert);
		} else if (data instanceof Date) {
			CellStyle style = workbook.createCellStyle();
			style.setDataFormat(creationHelper.createDataFormat().getFormat(dateFormat));
			cell.setCellValue((Date) data);
			cell.setCellStyle(style);
		} else if (data instanceof Boolean) {
			cell.setCellValue((Boolean) data);
		} else {
			cell.setCellValue((String) data);
		}
	}
}
```
### 後端List前端取用
```
後端-將List先轉成JSONArray:
JSONArray jsonList = JSONArray.fromObject(settingList); //List settingList

前端-拿到jsonString再轉回List:
<s:hidden id="jsonList" name="jsonList"/>
var temp = $("#jsonList").val(); //val()拿到字串
var listJson = JSON.parse(temp); //可以把JSON字串格式的物件，恢復成物件格式


GSON??


前端-將物件陣列轉為JSON形式的字串:
var editList = JSON.stringify(selectedData); //Object Array selectedData
$("#editList").val(editList);


後端獲取-轉回JSON陣列：
private String editList;
JSONArray conditionList = JSONArray.fromObject(editList);


後端獲取JSON陣列：
JSONArray toBeCheckArray = JSONArray.fromObject(checkArray);
JSONArray tempArray = toBeCheckArray.getJSONArray(i);
String BusCode = tempArray.getString(0);
```


### JSON後端概述
```
建立JSONObject:
1.JSONObject jsonObject = new JSONObject();
2.JSONObject jsonObject = JSONObject.fromObject(hashMap);
3.JSONObject jsonObject = JSONObject.fromObject(jsonString);

建立JSONArray:
1.JSONArray jsonArray = new JSONArray();
2.JSONArray jsonArray = JSONArray.fromObject(arrayList);
3.JSONArray jsonArray = JSONArray.fromObject(hashMap);
4.JSONArray jsonArray = JSONArray.fromObject(jsonString);

JSONArray放入HashMap:
JSONArray.fromObject(hashMap);

jsonObject：{“UserName”:”ZHULI”,”age”:”30″,”workIn”:”ALI”}

jsonArray：[“ZHULI”,”30″,”ALI”]


獲取JSONObject中的值：
String userName = jsonObject.getString(“key”);

獲取JSONArray中的值：
String userName = jsonArray.getString(index);



String jsonString = "{\"UserName\":\"kobi\",\"age\":\"34\",\"workIn\":\"ALI\",\"Array\":[\"kobi\",\"34\",\"ALI\"]}";

將Json字串轉為java物件:
JSONObject obj = JSONObject.fromObject(jsonString);

獲取Object中的UserName:
obj.getString("UserName");

獲取ArrayObject:
JSONArray transitListArray = obj.getJSONArray("Array");
```
### Gson概述
```
1.將對象轉為JSON形式的字串:
Gson gson = new Gson();
List persons = new ArrayList();
String str = gson.toJson(persons);

2.將JSON字串轉為JAVA物件:
jsonString：[{“name”:”name0”,”age”:0}]
Person person = gson.fromJson(jsonString, Person.class);
```
### logger層級
```
Loggers(寫Log )
被分為五個級別：ALL < TRACE < DEBUG < INFO < WARN < ERROR < FATAL < OFF

只輸出級別不低於設定級別的訊息
ex：Loggers為INFO，則INFO、WARN、ERROR和FATAL都會輸出 DEBUG、TRACE則不會

TRACE:
通常會放一些讓Developer在追bug時，可以補足ERROR或WARN的context資訊。
(如使用者目前是進行什麼功能的操作、使用者目前操作的步驟流程。)

DEBUG:(用的最多)
通常會放一些對於Developer、IT、SystemAdin等可以釐清問題的log。
(如分析效能相關，例如執行時間。分析錯誤相關。)

INFO:
通常會放一些重要的成功訊息並讓QA可以進行確認。
(如Service是否成功啟動、Transacations是否執行完成)

WARN:
用來警示的錯誤，出現時可以提供分析的資訊。
(如網路中斷、轉換的型態可能造成資料遺失、定時執行任務失敗)

ERROR:(用的最多)
一般的錯誤，出現了就必須排時間解決。
(如網路連線中斷無法連回、傳輸資料失敗、CRUD DB失敗)

FATAL:
最緊急的錯誤，需馬上處理。
(嚴重影響財損的錯誤、會讓服務暫停的錯誤)

```

### 基礎概念

#### package
```
1. 要引用不同package的類別需要import xxxPackage.xxxClass

2. 在類別中package xxx;須放在import之前。


package Practice;
import Note.Animal;

public class Draft {
    public static void main(String[] args) {
        
    }
}
```

#### 基本型別 & 包裝類
```
基本型別:byte、short、int、long、float、double、boolean、char

對應包裝類:Byte、Short、Integer、Long、Float、Double、Boolean、Character
```
```
在Java中，任何類別宣告的名稱都可以參考至null，表示該名稱沒有參考至任何物件實體，相當於有個名牌沒有任何人配戴。
```

#### 變數、常數、方法、類別命名規則
```
1. 只能以字母、底線、美元符號開始

2. 名稱中不可有&、%、-、#、@、*
```

#### BigDecimal
```
java中對BigDecimal比較大小一般用的是BigDecimal的compareTo方法

int a = bigDecimal1.compareTo(bigDecimal2)

a = 1,表示bigdemical大於bigdemical2；
a = 0,表示bigdemical等於bigdemical2； 
a = -1,表示bigdemical小於bigdemical2； 
```
```
//用equals比較有時候會出現錯誤

public class Draft2 {
    public static void main(String[] args) {

        BigDecimal bg1 = new BigDecimal("2.0");
        BigDecimal bg2 = new BigDecimal(2.00);
        
        System.out.println(bg1.equals(bg2)); //false
        System.out.println(bg1.compareTo(bg2)); //0
    }
}
```
```
創建時用String避免精度問題
BigDecimal bg = new BigDecimal("1000");

add() //加
subtract() //減
multiply() //乘
divide() //除
```
```
//add要視為+，還是要賦值到一個變數去儲存，不同於List的add

public class Demo {
    public static void main(String[] args) {

        BigDecimal num1 = new BigDecimal(50);
        BigDecimal num2 = new BigDecimal(100);

        num1.add(num2);
        System.out.println(num1); //50

        BigDecimal result = num1.add(num2);
        System.out.println(result); //150
    }
}
```
#### ++運算子
```
//先讓y的值加1，然後將結果的值賦給y
public class Draft {
    public static void main(String[] args) {
        int y=1;
        System.out.println(++y); //2
    }
}


//先把y的值賦予給y，然後將y的值加1，並儲存到記憶體空間。所以輸出值為1，儲存在記憶體的值為2
public class Draft {
    public static void main(String[] args) {
        int y=1;
        System.out.println(y++); //1
        System.out.println(y); //2
    }
}
```
```
//在if條件內的++a一樣會讓a遞增

public class Draft {
    public static void main(String arg[]) {

        int a = 2;
        int b = 1;
        for (int c = 0; c < 5; c++) {
            if ((++a > 2) && (++b > 2)) {
                a++;
            }
        }
        System.out.println("a=" + a + " b=" + b); //a=11 b=6
    }
}
```
#### 型別轉換
> 較小資料型別 轉 較大資料型別 : 自動晉升
> 較大資料型別 轉 較小資料型別 : 需自行強轉型

```
//需型別轉換特例
//高階放到低階一般需強轉型，但+=為特例

public class Draft {
    public static void main(String arg[]) {

        byte x = 5;
        int y = 3;
        
        byte a = x+y; //報錯
        byte b = x+=y; //正確
        
    }
}


public class Draft {
    public static void main(String arg[]) {

        short s1=1;
        s1 = s1 + 1; //報錯
        s1 = (short)(s1 + 1); //正確
        s1+=1; //正確
        
    }
}
```

```
//浮點數預設為double
//int可指定給float

public class Draft {
    public static void main(String arg[]) {
        
        float a = 12; //正確
        float b = 1.2; //報錯
        float c = 1.2F; //正確

    }
}  
```
```
//Java的布林型別不同於C or C++，布林是一個獨立的型別，不能將其他型別的值當作布林型別處理
//int不可轉換為boolean，boolean也不可轉換為int

public class Draft {
    
    int x = 0;
    
    if((boolean)x == false){
        System.out.println("false");
    } //報錯
    
}
```
```
//自動晉升範例

public class Draft {
    public static void main(String[] args) {

        short a = 10;
        byte b = 5;
        char c = 'A';
        int n = 6;
        System.out.println("short->int  " + (a - n)); //4
        System.out.println("byte->int   " + (b * n)); //30
        System.out.println("char->int  " + (c + n)); //71

    }
}
```
```
//利用包裝類轉型範例

public class Draft {
    public static void main(String[] args) {

        int i = 67;
        Integer it = new Integer(i);
        short s = it.shortValue();
        
        double d1=100;
        Double D1 = new Double(d1);
        int p = D1.intValue();
        
    }
}

```
#### ==及Equals
```
基本型別只有 == 比值，沒有equals方法。

參考型別的==跟equals都是比記憶體位置，繼承自Object的原生方法。 (變數所儲存的參考)

String以及Integer等類別可以使用equals來比較內容，是因為override過Object的equals方法。

https://www.gushiciku.cn/pl/gfB3/zh-tw

https://openhome.cc/Gossip/JavaEssence/EqualOperator.html
```
```
//Object用equals相比時，會以內含物件的equals來相比。

public class Draft {
    public static void main(String[] args) {
        
        Object a = new String("abc");
        Object b = new String("abc");
        Object c = new Integer(123);
        Object d = new Integer(123);;

        System.out.println(a == b); //false
        System.out.println(a.equals(b)); //true
        System.out.println(c == d); //false
        System.out.println(c.equals(d)); //true
    }
}
```
```
public class Draft {
    public static void main(String[] args) {

        String name1 = "Java";
        String name2 = name1 + "World";
        System.out.println(name2);


        //反組譯上述程式碼，得知使用+串接字串，會產生新的String物件。
        //盡量不要在迴圈內使用，因效能較差。
        String s = "Java";
        String s1 = (new StringBuilder()).append(s).append("World").toString();
        System.out.println(s1);
    }
}
```
```
//字串比較
//在 Java 中，使用 '+' 串接字串的話會產生一個新的字串物件

public class Draft {
    public static void main(String arg[]) {
        
        String str1="str";
        String str2="string";
        String str3="ing";
        String str4=str1+str3;
        str1=str4;
        System.out.println("str1"+((str1==str2)?"==":"!=")+"str2");
        
        //str1!=str2
        //str4新串接字串的記憶體位置與str2不同       
    }
}
```
```
public class Draft {
    public static void main(String[] args) {

        String a = "abcde";
        String b = "ab";
        String c = b +"cde";
        System.out.println(a == c); //false
    }
}


//一行寫死，編譯器會認為就是要這個東西，不是去串接字串
public class Draft {
    public static void main(String[] args) {

        String a = "abcde";
        String b = "abc"+"de";
        System.out.println(a == b); //true
    }
}
```



```
//基本型別+字串時，基本型別會轉換為字串型別

10.4 + "4.2"  //10.44.2
```


#### 邏輯運算子
```
&&:
exp1    exp2    exp1&&exp2
--------------------------
flase   false   false
false   ture    false
true    false   false
true    true    true


||:
exp1    exp2    exp1&&exp2
--------------------------
flase   false   false
false   ture    ture
true    false   true
true    true    true
```
```
public class Draft {
    public static void main(String arg[]) {
    
        int x = 10;
        int y = 21;
        System.out.println(((x > y) && (x < y))); //false
        
    }
}


public class Draft {
    public static void main(String arg[]) {

        int x = 10;
        int y = 21;
        System.out.println(((x == y) || (x > y))); //false
        System.out.println(((x > y) || (x < y))); //true
        
    }
}
```

#### overload
```
可以根據參數數目及型別不同，建立多個相同名稱的方法。
```

#### override
```
子類別繼承父類別之後，可以改寫父類別的方法。但必須:

1.方法名稱、2.參數個數、3.參數型別、4.回傳值皆與父類別相同。

5.存取修飾子等級不能小於原方法，

6.當父類別定義有throws的方法時，子類別所throws的Exception不能大於父類別，

7.加有final修飾的方法不能被override、static方法只能覆寫為static方法。

8.子類別覆寫父類別方法之後，會以子類別覆寫後的方法為主。
```

#### public static void main(String args[])
```
public: main方法是Java程序運行時調用的第一個方法，因此它必須對Java環境可見。所以可見性設置為pulic。

static: Java平台調用這個方法時不會創建這個類的一個實例，因此這個方法必須聲明為static。

void: main方法沒有返回值。

String 是命令行傳進參數的類型，args是指命令行傳進的字符串數組。
```
#### System.out.println()
```
System是系統提供的預定義的final類，out是一個PrintStream對象，println是out對象裡面一個重載的方法。
```

#### abstract
```
1. 抽象類別不一定要有抽象方法。但抽象方法一定要放在抽象類別裡面。

2. 不能用private、static、final修飾抽象方法。 (因為就是要讓後面的人override)

3. 抽象類別還是可以宣告建構子，為了讓後面的子類別可以把共同的資料交給父類別完成設定。

4. 抽象方法沒有方法主體，連{}都沒有，且必須加上abstract修飾子。

5. 抽象類別無法產生實體，即無法new新物件。

6. 子類別繼承了抽象父類別，並實作出父類別所有抽象方法，此子類別就不再是抽象類別，即可以new新物件。 (非抽象方法則不用實作出來，即可new新物件)
```

#### Interface
```
1. 介面是一種所有方法皆為抽象方法的抽象類別。

2. 介面內所有方法預設皆是public abstract，故可省略不寫，也不可更改。

3. 介面內所有變數預設皆是public final static，故可省略不寫，也不可更改，但必須初始化。

4. 介面沒有建構子。

5. 介面與介面之間是可以再繼承的(extends)。

6. 一個介面可以同時繼承多個介面extends。一個類別只能繼承一個類別extends，但可以實作多個介面implements。

7. 介面不能new新物件 (Interfaces cannot be instantiated)。

8. 子類別必須implements父介面後，並實作出父介面所有抽象方法，此子類別就不再是抽象類別，即可以new新物件。

9. 使用介面主要目的為:1.實現多重繼承 2.預先定義規格 3.貼標籤(空介面) 4.型態轉換(父多型) 5.降低相依性。

10. 使用介面好處，可代替類別繼承時需全盤繼承的缺點，但還是能具有共同的行為。
```
#### abstract 範例
```
public abstract class PP {

    public abstract void run();

}
```
```
public class HelloWorld extends PP{

    //若沒實作run出來就無法new新物件
    public void run(){
        System.out.println("run");
    }; 
    
    
    public static void main(String[] args) {

        HelloWorld hh = new HelloWorld();
        
        hh.run();
    }
}
```
#### Interface 範例

* 範例1
```
public interface PP {
    
    public abstract void run();
    
}
```
```
public class HelloWorld implements PP{

    //若沒實作run出來就無法new新物件
    public void run(){
        System.out.println("run");
    }; 


    public static void main(String[] args) {

        HelloWorld hh = new HelloWorld();

        hh.run();;
    }
}
```
* 範例2
```
// D繼承實作C介面，也就意味著要實現A、B、C三個介面的抽象方法

public class Draft {
    public static void main(String[] args) {
        D d = new D();
        d.sayA();
        d.sayB();
        d.sayC();
    }
}

interface A {
    String a = "我是介面A";

    public void sayA();
}

interface B {
    String b = "我是介面B";

    public void sayB();
}


interface C extends A, B {
    String c = "我是介面C";

    public void sayC();
}


class D implements C {
    public void sayC() {
        System.out.println(c);
    }

    public void sayA() {
        System.out.println(a);
    }

    public void sayB() {
        System.out.println(b);
    }
}
```
```
我是介面A
我是介面B
我是介面C
```

#### 建構子
```
1. 建構子名稱需與類別名稱相同。

2. 建構子無回傳值，連void都不能加。

3. Java會自動給一個不帶參數的建構子，一旦宣告其他建構子，則Java會自動將此預設隱形的建構子移除。

4. 建構子只能接在new後面來呼叫，每個物件的建構子只會在誕生執行一次。

4. 在Java中只要看到new，一定就是建立新物件，會有一個新的記憶體位置。

5. 建構子可以overload。

6. 建構子不能被override。

7. 建構子無法被繼承，但可以呼叫。

8. 子類別的建構子中，會自動被加上一個預設隱形的super()建構子。

8. 因為Java在執行子類別的建構子之前，會先呼叫父類別中無參數的建構子。

static class Son extends Father {
    Son(){
        super();
    }
}
```
#### 建構子覆載範例
```
public class PenConstOverload {
    private String brand;
    private double price;
	
    public PenConstOverload(String brand, double price) {
        this.brand = brand;
        this.price = price;
    }
	
    public PenConstOverload(double price) {
        this("SKB", price);
    }
	
    public PenConstOverload(String brand) {
        this(brand, 10);
    }
	
    public PenConstOverload() {
        this("SKB", 10);   //this要放第一行。
                           //this("SKB", 10)等於是執行上面匹配的第一個建構子。
                           //再由上面匹配的建構子傳到最上面實體變數，完成資料設定。
    }
	
    public void showInfo() {
        System.out.println("牌子為： " + brand);
        System.out.println("價格為： " + price);
        System.out.println("=============");
    }
	
    public static void main(String[] args) {
		
        PenConstOverload p1 = new PenConstOverload("A", 20);
        PenConstOverload p2 = new PenConstOverload(40);
        PenConstOverload p3 = new PenConstOverload("B");
        PenConstOverload p4 = new PenConstOverload();
		
        p1.showInfo();
        p2.showInfo();
        p3.showInfo();
        p4.showInfo();
    }
}

```
```
牌子為： A
價格為： 20.0
=============
牌子為： SKB
價格為： 40.0
=============
牌子為： B
價格為： 10.0
=============
牌子為： SKB
價格為： 10.0
=============
```
#### 預設建構子範例
```
public class Build {

    public Build(int a){
        
    }
    
    public static void main(String[] args) {

        Build bb = new Build(3);   //宣告了有參數建構子之後，預設無參數建構子就會被拿掉。

    }

    class Test extends Build{
    
        public Test(){     
            super(5);   //宣告了有參數建構子之後，預設無參數建構子就會被拿掉，所以super();會報錯。
            System.out.println("Test");
            
        }
    }
}
```
#### 繼承
```
1. 繼承 = 子類別/介面 具有 父類別/介面 全部的屬性和方法 (父類別/介面有的東西，子類別/介面都會有)。

2. 子類別繼承父類別之後，除了可以選擇override父類別方法之外，也可以選擇overload父類別方法。

3. is-a = Subclass is-a Superclass

4. has-a = Class A 內new了一個C物件 = A has-a C
```
* 範例1
```
//子類別會擁有父類別所有的屬性跟方法

public class Father {

    public String eyes = "雙眼皮";
    public String faceColor = "白色";

    public String language() {
        return "漢語";
    }

    public String eat() {
        return "我喜歡吃辣椒";
    }

    public Father() {
    }
}	
```
```
public class Son extends Father {
	public static void main(String[] args) {
    
		Son son = new Son();
        
		System.out.println("眼睛是" + son.eyes + " 膚色是 " + son.faceColor);
		System.out.println("我的語言是 " + son.language() + " 還有" + son.eat());
        
	}
}
```
```
眼睛是雙眼皮 膚色是白色

我的語言是 漢語 還有我喜歡吃辣椒
```
* 範例2
```
public class Draft {
    public static void main(String[] args) {
        Rectangular r = new Rectangular(15, 8, "長方形");        //產生長方形的物件實體
        Circle cir = new Circle(1.5, "圓形");                     //產生圓形的物件實體
        EqualTriangle tr = new EqualTriangle("三角形", 8, 9);    //產生三角形的物件實體
        System.out.println(r.name + "的長" + r.length + " 寬" + r.width + " 面積" +
                r.area() + " 周長" + r.perimeter());
        System.out.println(cir.name + "的半徑" + cir.r + " 面積" + cir.area() +
                " 周長" + cir.perimeter());
        System.out.println(tr.name + "的高" + tr.hight + " 底" + tr.width + " 面積" + tr.area()
                + " 周長" + tr.perimeter());
    }
}

abstract class Shape {
    String name;
    double length, width, hight;
    double r;
    double a = 3.14;

    abstract double area();                                            // 求面積

    abstract double perimeter();                                    // 求周長

    public Shape(double length, double width, String name) {        // 四邊形的建構方法
        this.length = length;
        this.width = width;
        this.name = name;
    }

    public Shape(String name, double width, double hight) {            // 三角形的建構方法
        this.hight = hight;
        this.width = width;
        this.name = name;
    }

    public Shape(double r, String name) {                                // 圓形的建構方法
        this.r = r;
        this.name = name;
    }
}

class EqualTriangle extends Shape {                                    // 等邊三角形
    public EqualTriangle(String name, double width, double hight) {
//利用建構方法為三角形的邊、高、名字設定值
        super(name, width, hight);
    }

    double area() {                            //實現area()抽象方法，表示三角形面積的公式
        return width * hight / 2;
    }

    double perimeter() {                    //實現perimeter()抽象方法，表示三角形周長的公式
        return 3 * width;
    }
}

class Circle extends Shape {                    // 圓形
    public Circle(double r, String name) {    //利用建構方法為圓形的半徑、名字設定值
        super(r, name);
    }

    double area() {                                //實現area()抽象方法，表示圓形面積的公式
        return a * r * r;
    }

    double perimeter() {                        //實現perimeter()抽象方法，表示圓形周長的公式
        return 2 * a * r;
    }
}

class Rectangular extends Shape {        // 長方形
    public Rectangular(double length, double width, String name) {
        super(length, width, name);
    }

    double area() {                            //實現area()抽象方法，表示長方形面積的公式
        return length * width;
    }

    double perimeter() {                    //實現perimeter()抽象方法，表示長方形周長的公式
        return (length + width) * 2;
    }
}
```
* 範例3
```
public class Employee {
    private int empno;
    private String ename;

    public void setEmpno(int empno) {
        this.empno = empno;
    }

    public int getEmpno() {
        return empno;
    }

    public void setEname(String ename) {
        this.ename = ename;
    }

    public String getEname() {
        return ename;
    }

    public Employee(int empno, String ename) {
        this.empno = empno;
        this.ename = ename;
    }

    public Employee(int empno) {
        this(empno, "-");
    }

    public Employee(String ename) {
        this(0, ename);
    }

    public Employee() {
    }

    public void display() {
        System.out.println("empno = " + empno);
        System.out.println("ename = " + ename);
    }
}
```
```
public class FullTimeEmployee extends Employee {

    private double monthlySalary; // 月薪

    public void display() {
        super.display();
        System.out.println("月薪 = " + monthlySalary);
    }

    public FullTimeEmployee(int empno, String ename, double monthlySalary) {
        super(empno, ename);   //設定在父類別裡
        this.monthlySalary = monthlySalary;   //設定在子類別裡
    }
}
```
```
public class TestFullTimeEmployee {

    public static void main(String[] args) {
        FullTimeEmployee f1 = new FullTimeEmployee(7002 ,"David", 50000.0 );          
        f1.display();
    }
}
```
```
empno = 7002
ename = David
月薪 = 50000.0
```
* 範例4
```
//子類別繼承父類別之後，除了可以override之外，也可以選擇overload。

public class Draft {

    public int test(int i) {
        return i;

    }
}


class OverloadTest extends Draft {

    public int test(int i, int j) {
        return j;
    }

    public int test(int i) {
        return i;

    }
    
}
```

#### 繼承(呼叫建構子)範例

> Java會自動加上一個預設隱形的super()建構子。

> Java在執行子類別的建構方法之前，會先呼叫父類別中無參數的建構方法，為了對繼承自父類別的成員做初始化的操作。

> 若已知父類別沒有無參數建構子，可以在super()，填入父類別帶有參數的建構子，讓系統找到正確的建構子。
```
public class Build {
    public static void main(String[] args) {

        Father ff = new Father();
        System.out.println();
        Son ss = new Son();
        System.out.println();
        Grandson oo = new Grandson();

    }

    static class Father {
        Father(){
        
            System.out.println("Father Constructor");
            
        }
    }

    static class Son extends Father {
        Son(){
//            super();
            System.out.println("Son Constructor");
        }
    }

    static class Grandson extends Son{
        Grandson(){
//            super();
            System.out.println("Grandson Constructor");
        }
    }
}
```
```
Father Constructor

Father Constructor
Son Constructor

Father Constructor
Son Constructor
Grandson Constructor
```
#### 日期處理

* Convert String to java.util.Date
```
String now = "20210727";

SimpleDateFormat df = new SimpleDateFormat("yyyyMMdd");

Date date = df.parse(now);

System.out.println(date);
```

* Convert Date to String
```
Date now = new Date();

SimpleDateFormat df = new SimpleDateFormat("yyyyMMddHHmmssS");

String date = df.format(now);

System.out.println(date);
```
* 創立沒有時分秒的當下時間
```
LocalDate nowLocalDate = LocalDate.now();
Date dateToday = Date.from(nowLocalDate.atStartOfDay(ZoneId.systemDefault()).toInstant());


Mon May 16 00:00:00 CST 2022

```
* 日期比大小
```
public class Test05 {
    public static void main(String[] args) throws ParseException {
        Date date1 = new Date(); //2022-05-16
        String str = "2022-05-01";
        SimpleDateFormat sf = new SimpleDateFormat("yyyy-MM-dd");
        Date date2 = sf.parse(str);
        System.out.println(date2.before(date1));
    }
}

//true
```
```
void testDateCompare() throws ParseException {
  SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
  Date date1 = sdf.parse("2009-12-31");
  Date date2 = sdf.parse("2019-01-31");

  System.out.println("date1 : " + sdf.format(date1));
  System.out.println("date2 : " + sdf.format(date2));

  if (date1.compareTo(date2) > 0) {
    System.out.println("Date1 时间在 Date2 之后");
  } else if (date1.compareTo(date2) < 0) {
    System.out.println("Date1 时间在 Date2 之前");
  } else if (date1.compareTo(date2) == 0) {
    System.out.println("Date1 时间与 Date2 相等");
  } else {
    System.out.println("程序怎么会运行到这里?正常应该不会");
  }
}
```
* 增加Date時間到最後一秒
```
    public static Date dateToDateEnd(Date date){
        if (date == null) {
            return null;
        }
        Calendar calendar = Calendar.getInstance();
        LocalDate localDate = convertDateToLocalDate(date);
        calendar.set(Calendar.YEAR, localDate.getYear());
        calendar.set(Calendar.MONTH, localDate.getMonthValue()-1);
        calendar.set(Calendar.DAY_OF_MONTH, localDate.getDayOfMonth());
        calendar.set(Calendar.HOUR_OF_DAY, 23);
        calendar.set(Calendar.MINUTE, 59);
        calendar.set(Calendar.SECOND, 59);
        calendar.set(Calendar.MILLISECOND, 999);
        return calendar.getTime();
    }
```
#### 集合族譜
```
List: 
1. 會自動按加入先後順序排列。
2. 允許重複的值加入。
3. 有索引值。
4. 可使用iterator & for-each & for迴圈取值。
5. 集合可放不同型別物件。
 
 
HashSet:
1. 取出時無順序性(按加入順序&大小排列)。
2. [值重複不會被加入。]
3. [沒有索引值。]
4. [需使用iterator跟for-each取值。]
5. 集合可放不同型別物件。

TreeSet:
1. 會自動按大小排列(由小到大)。
2. [值重複不會被加入。]
3. [沒有索引值。]
4. [需使用iterator跟for-each取值。]
5. 集合需放同型別物件，否則排序會爆掉。

LinkedHashSet:
1. 會自動按加入先後順序排列。
2. [值重複不會被加入。]
3. [沒有索引值。]
4. [需使用iterator跟for-each取值。]
5. 集合可放不同型別物件。


HashMap:
1. 取出時無順序性(按加入順序&大小排列)。
2. [Key值重複定義時，後面的值會覆蓋掉前面的值。]
3. [有索引值。]
4. [可使用iterator & for-each取值，但需先使用KeySet 或 values方法轉換。]
5. 集合可放不同型別物件。
6. key/value允許null。

HashTable:
1. 取出時無順序性
2. [Key值重複定義時，後面的值會覆蓋掉前面的值。]
3. 實現多執行緒安全，效能較差。
4. key/value不允許null。

TreeMap:
1. 放入的元素會自動按Key的大小排列(由小到大)。
2. [Key值重複定義時，後面的值會覆蓋掉前面的值。]
3. [有索引值。]
4. [可使用iterator & for-each取值，但需先使用KeySet 或 values方法轉換。]
5. 集合需放同型別key(Key需同型別，但Value不用)。

LinkedHashMap:
1. 會自動按加入先後順序排列。
2. [Key值重複定義時，後面的值會覆蓋掉前面的值。]
3. [有索引值。]
4. [可使用iterator & for-each取值，但需先使用KeySet 或 values方法轉換。]
5. 集合可放不同型別物件。
```

```
Iterator > Collection > List > ArrayList
                             > LinkedList
                             > Vector

                      > Set  > HashSet
                             > TreeSet
                             > LinkedHashSet
                      
                      > Queue > LinkedList
                              > PriorityQueue

public interface Collection extends Iterable

public interface List extends Collection
public interface Set extends Collection
public interface Queue extends Collection

public class ArrayList extends AbstractList
                       implements List, RandomAccess, Cloneable, Serializable
                       
       
Map > HashMap
    > TreeMap
    > LinkedHashMap
    > Hashtable

public class HashMap extends AbstractMap
                     implements Map, Cloneable, Serializable
```
#### 集合方法
* Collection定義的方法
```
add(obj); //加入物件

add(index, element); //將物件插入到指定的位置

addAll(Collection c); //將c的所有元素加入集合當中

clear(); //清空集合

remove(obj); //刪除obj

removeAll(Collection c); //刪除c的所有元素

contains(obj); //集合是否包含obj物件

containsAll(Collection c); //集合是否包含c中的所有元素

equals(obj); //集合是否與obj相等

isEmpty(); //集合是否為空

toArray(); //將集合轉為物件陣列

size(); //集合元素個數
```
* List定義的方法
```
get(int index); //拿到索引值物件

set(int index, E element); //更改索引值物件的值
```
* Map定義的方法
```
put(K key, V value); //加入物件

get(Object key); //拿到索引值物件

containsKey(Object key); //是否包含此key物件

containsValue(Object value); //是否包含此value物件

keySet(); //將所有的key轉為Set物件 

values(); //將所有的value轉為Collection物件 

entrySet(); //將所有的key和value轉為Set<Map.Entry<String, String>>物件，並用getKey() & getValue()取用
```
#### 字串、陣列、集合為空判斷
```
public class Draft {
    public static void main(String args[]) {

        String str="";
        
        int[] x = new int[3];
        int[] y = new int[0];
        int[] z = null;       
        
        List list = new ArrayList();

        
        
        System.out.println(str.isEmpty()); //true
        System.out.println(str.length()==0); //true
        System.out.println(str.equals("")); //true


        //只有當一個陣列包含零個元素並且長度為零時，這個陣列才是空的。
        System.out.println(x.length==0); //false
        System.out.println(y.length==0); //true
        System.out.println(z == null); //true


        System.out.println(list.isEmpty()); //true
        System.out.println(list.size()==0); //true
        System.out.println(list == null);  //false

    }
}
```
#### 字串、集合內含元素方法
```
public class Draft2 {
    public static void main(String[] args) {

        List list = new ArrayList();

        list.add("a");
        list.add("b");
        System.out.println(list.contains("a")); //true


        Map map = new HashMap<>();
        map.put("1", "APPLE");
        map.put("2", "BANANA");

        System.out.println(map.containsKey("1")); //true
        System.out.println(map.containsValue("BANANA")); //true


        String str = "ABC";
        System.out.println(str.contains("A")); //true
        System.out.println(str.contains("AB")); //true
    }
}
```
#### 列印集合、陣列
```
//陣列
public class Draft {
    public static void main(String[] args) {

        int[] array = new int[3];

        array[0]=2;
        array[1]=1;
        array[2]=3;

        System.out.println(Arrays.toString(array)); //[2,1,3]

    }
}


//集合
public class Draft {
    public static void main(String[] args) {

        List<Integer> list = new LinkedList<Integer>();
        
        list.add(3);
        list.add(1);
        list.add(5);
        
        System.out.println(list); //[3, 1, 5]

    }
}
```
#### 陣列塞值
```
public class Draft {
    public static void main(String[] args) {

        int[] intArray = new int[3];
        System.out.println(Arrays.toString(intArray));

        Arrays.fill(intArray, 100);
        System.out.println(Arrays.toString(intArray));
    }
}

//[0, 0, 0]
//[100, 100, 100]
```
#### 陣列集合轉換
```
//集合轉陣列

public class Draft {
    public static void main(String args[]) {

        ArrayList<Integer> list = new ArrayList<Integer>();
        list.add(10);
        list.add(12);
        list.add(31);
        
        Object[] obj = list.toArray();
        System.out.println(Arrays.toString(obj)); //[10, 12, 31]

        Integer array[] = new Integer[list.size()];
        array = list.toArray(array);
        System.out.println(Arrays.toString(array)); //[10, 12, 31]
    }
}
```
```
//集合轉陣列(不使用API)

public class Draft {
    public static void main(String args[]) {

        List<Integer> list = new ArrayList<Integer>();

        list.add(3);
        list.add(1);
        list.add(2);

        int[] array = new int[3];

        int j=0;
        for(int i=0;i<list.size();i++){
            array[j] = list.get(i);
            j++;
            if(j==3){
                break;
            }
        }

        System.out.println(Arrays.toString(array)); //[3, 1, 2]

    }
}
```
```
//陣列轉集合

public class Draft {
    public static void main(String args[]) {

        int[] array = {10,12,31};
        List list = new ArrayList();

        for(int x : array){
            list.add(x);
        }

        System.out.println(list); //[10, 12, 31]
        
    }
}
```
#### 陣列&集合取用物件
```
public class Draft {
    public static void main(String[] args) {

        Material m1 = new Material("Tom",50000);
        Material m2 = new Material("Mark",70000);


        Material[] array = {m1,m2};

        System.out.println(array[0].getName());
        System.out.println(array[0].getSalary());
        System.out.println(array[1].getName());
        System.out.println(array[1].getSalary());


        List<Material> list = new ArrayList<Material>();
        list.add(m1);
        list.add(m2);

        System.out.println(list.get(0).getName());
        System.out.println(list.get(0).getSalary());
        System.out.println(list.get(1).getName());
        System.out.println(list.get(1).getSalary());

    }
}
```
#### 同名model放入集合

* OK範例
```
public class Demo {
    public static void main(String[] args) {

        ABC abc = null;
        int count = 1;
        List<ABC> list = new ArrayList<ABC>();
        
        for (int i = 0; i < 2; i++) {
            abc = new ABC(); //同樣名稱變數放進list，因new新的記憶體空間，故後面的值不會覆蓋前面的。
            abc.setId(count);
            list.add(abc);
            count++;
        }
        
        System.out.println("size = " + list.size());

        for (ABC a : list) {
            System.out.println(a.getId());
        }
    }
}
```
```
size = 2
1
2
```
* NG範例
```
public class Draft {
    public static void main(String[] args) {

        ABC abc = new ABC();
        int count = 1;
        List<ABC> list = new ArrayList<ABC>();

        for (int i = 0; i < 2; i++) {
            abc.setId(count); //因為是同一個物件的記憶體位置，第二次SET會改變第一個放入物件的值。
            list.add(abc);
            count++;
        }

        System.out.println("size = " + list.size());

        for (ABC a : list) {
            System.out.println(a.getId());
        }
    }
}
```
```
size = 2
2
2
```
* OK範例
```
public class Draft {
    public static void main(String[] args) {

        List<ABC> list1 = new ArrayList<>();

        ABC a1 = new ABC();
        a1.setName("Tom");
        ABC a2 = new ABC();
        a2.setName("Jack");

        list1.add(a1);
        list1.add(a2);

        List<ABC> list2 = new ArrayList<>();

        int count = 1;

        for (ABC x : list1) { //將物件逐個取出設定，設定完放入list2，不會有覆蓋情況產生。
            x.setId(count);
            list2.add(x);
            count++;
        }

        System.out.println("size = " + list2.size());
        System.out.println(list2.get(0).getId());
        System.out.println(list2.get(0).getName());
        System.out.println(list2.get(1).getId());
        System.out.println(list2.get(1).getName());
    }
}
```
```
size = 2
1
Tom
2
Jack
```
* OK範例
```
public class Draft {
    public static void main(String[] args) {

        List list1 = new ArrayList();
        List list2 = new ArrayList();
        list1.add(1);
        list1.add(3);
        
        for (Object x : list1) {
            list2.add(x);
        }
        
        System.out.println(list2); //[1, 3]
    }
}
```
#### Foreach拿出物件設定
```
public class Demo {
    public static void main(String[] args) {
        
        int count = 1;
        ABC a1 = new ABC("Tom");
        ABC a2 = new ABC("Jack");
        
        List<ABC> list = new ArrayList<>();
        list.add(a1);
        list.add(a2);
        
        for (ABC x : list) {
            x.setId(count); //將物件逐個取出設定，設定完再放回原集合。
            count++;
        }

        System.out.println(list.get(0).getId());
        System.out.println(list.get(0).getName());
        System.out.println(list.get(1).getId());
        System.out.println(list.get(1).getName());

    }
}
```
```
1
Tom
2
Jack
```
#### Object集合轉其他物件集合
> 先將Object集合放入物件，再將此物件強轉型。
```
public class Demo {
    public static void main(String[] args) {

        Object obj1 = new ABC(001, "Tom");
        Object obj2 = new ABC(002, "Jack");

        List<Object> list1 = new ArrayList<>();
        list1.add(obj1);
        list1.add(obj2);

        Object obj = list1;
        List<ABC> list2 = (List<ABC>) obj;

        System.out.println(list2.get(0).getId()); //1
        System.out.println(list2.get(0).getName()); //Tom
        System.out.println(list2.get(1).getId()); //2
        System.out.println(list2.get(1).getName()); //Jack

    }
}
```
#### 不指定長度的二維陣列 (非矩形的多維陣列)
> 程式設計中經常用到這樣一種特殊的二維陣列，它的列數確定，但是每列的長度不確定。這樣的的陣列實現方法：先創建制定列數，之後再各別指定每一個一維陣列的長度。
```
public class Draft {
    public static void main(String[] args) {

        int[][] arr = new int[2][];
        
        arr[0] = new int[]{1, 2, 3, 4, 5}; //必須先初始化長度，必須有new int[]
        arr[1] = new int[]{1, 2, 3};

        for (int[] row : arr) {
            for (int value : row) {
                System.out.printf("%2d", value);
            }
            System.out.println();
        }
    }
}

//1 2 3 4 5
//1 2 3
```
```
//也可以用此方法建立

int[][] arr = {
    {,2,3,4,5}
    {1,2,3}   
}
```
#### 二維陣列使用For-Each取值
```
%d 就是普通的输出

%2d 输出占2个位置，如输出2时，是一个空格和2，如200时输出200
```
```
public class Draft {
    public static void main(String[] args) {

        int[][] array = {
                {1, 3, 5},
                {2, 4, 6}
        };

        for (int[] row : array) {
            for (int value : row) {
                System.out.printf("%2d", value);
            }
            System.out.println();
        }
    }
}
```
```
 1 3 5
 2 4 6
```



#### StringBuffer 

> 只會產生一個實例，效能較好。

* 建構子
```
//共有四種物件建立方法

1.StringBuffer sb = new StringBuffer();
2.StringBuffer sb = new StringBuffer(126); //指定長度
3.StringBuffer sb = new StringBuffer("abc"); //以字串物件初始化內容
4.StringBuffer sb = new StringBuffer('c'); //以字元初始化內容


sb.append("str"); //串接

sb.reverse(); //反轉
```
* String和StringBuffer比對內容
```
//需將StringBuffer轉為String比對 或 使用contentEquals方法比對

public class Demo {
    public static void main(String[] args) {

        String str = new String("Here we are");
        StringBuffer sb = new StringBuffer("Here we are");

        System.out.println(str.contentEquals(sb)); //true
        System.out.println(str.equals(sb)); //false

        String temp = sb.toString();
        System.out.println(temp.equals(str)); //true

    }
}
```




#### 巢狀三元運算子
```
public class Test {
    public static void main(String[] args) {

        int x = 10;

        if (x > 10) {
            System.out.println(">");
        } else if (x < 10) {
            System.out.println("<");
        } else {
            System.out.println("=");
        }

       System.out.println( x > 10 ? " > " : x < 10 ? " < " : " = ");

    }
}

// 列印結果皆為 =

//result = true ? "A" : "B";  一般標準寫法
```
#### for迴圈
```
//第一次執行只看條件判斷，就執行程式區塊
//第二次執行先跑完計次再看條件判斷

for(初始設定; 條件判斷; 計次){

}
```
#### break、continue
> break、continue直接出去
> 迴圈外 的底下程式碼還是會走完

> 用於for、while迴圈

> label: break或continue所標記的迴圈

```
//break範例1

//break，直接跳出內迴圈，內迴圈底下語句不執行。
//內迴圈break結束之後，會執行迴圈外底下程式碼，才開始下一次外迴圈。


public class Draft {
    public static void main(String[] args) {

        for (int i = 0; i <= 2; i++) {
            for (int j = 0; j <= i; j++) {
                if (j == 1) {
                    break;
                }
                System.out.println("Outer = " + i + " " + "Inner = " + j);
            }
            System.out.println("Outer circle");
        }
    }
}
```
```
Outer = 0 Inner = 0
Outer circle
Outer = 1 Inner = 0
Outer circle
Outer = 2 Inner = 0
Outer circle
```
```
//continue範例1

//coutinue，pass此次內迴圈，繼續執行下次迴圈，內迴圈底下語句不執行。
//內迴圈結束之後，會執行下面程式碼，才開始下一次外迴圈。

public class Draft {
    public static void main(String[] args) {

        for (int i = 0; i <= 2; i++) {
            for (int j = 0; j <= i; j++) {
                if (j == 1) {
                    continue;
                }
                System.out.println("Outer = " + i + " " + "Inner = " + j);
            }
            System.out.println("Outer circle");
        }
    }
}
```
```
Outer = 0 Inner = 0
Outer circle
Outer = 1 Inner = 0
Outer circle
Outer = 2 Inner = 0
Outer = 2 Inner = 2
Outer circle
```
```
//break範例2

public class Draft {
    public static void main(String[] args) {

        Label:
        for (int i = 0; i <= 2; i++) {
            for (int j = 0; j <= i; j++) {
                if (j == 1) {
                    break Label;
                }
                System.out.println("Outer = " + i + " " + "Inner = " + j);
            }
            System.out.println("Outer circle");
        }
    }
}
```
```
Outer = 0 Inner = 0
Outer circle
Outer = 1 Inner = 0
```
```
//continue範例2

public class Draft {
    public static void main(String[] args) {

        Label:
        for (int i = 0; i <= 2; i++) {
            for (int j = 0; j <= i; j++) {
                if (j == 1) {
                    continue Label;
                }
                System.out.println("Outer = " + i + " " + "Inner = " + j);
            }
            System.out.println("Outer circle");
        }
    }
}
```
```
Outer = 0 Inner = 0
Outer circle
Outer = 1 Inner = 0
Outer = 2 Inner = 0
```
#### Exception類型
```
執行時例外(RuntimeException / Unchecked Exception): 

1. 程式可執行，跑到有問題的地方才會炸掉。 
2. 最常遇到的例外類型。
3. IndexOutOfBoundsException、NullPointerException、ClassCastException等等。
```
```
檢查型例外(Checked Exception)

1. 程式不可執行，在IDE就會有紅底線錯誤。
2. ClassNotFoundException等等。
```
#### try/catch/finally
> 可使用的三種組合: try + catch / try + finally / try + catch + finally 

#### try/catch執行順序
> 有例外處理，讓程式可以持續進行下去，而不會中斷在例外處。

> try區塊遇到例外會直接跳轉進catch，try區塊內後續程式碼不執行。

> catch捕捉後，會繼續執行後續程式碼。
```
public class Draft {
    public static void main(String[] args) {
        int arry[] = { 0, 1, 3, 4, 6 };
        int a = 0;

        try {
            int z = 5 / a;
            for (int i = 0; i < 10; i++) {
                System.out.println(arry[i]);
            }
        } catch (ArithmeticException e) {
            System.out.println("0不能作為被除數");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("arry[]的長度是5，陣列下標越界了");
        }
        System.out.println("例外處理後繼續運行程式");
    }
}
```
```
0不能作為被除數

例外處理後繼續運行程式
```
> 當例外未由catch捕捉時，會炸掉直接中斷，由系統處理，後續程式碼也不會執行。
```
public class Draft {
    public static void main(String[] args)  {
        int a = 2;
        String b[]=new String[2];
       
       try {
            int z = 5 / a;
            System.out.println("z="+z);
            b[0].toLowerCase();
        } catch (ArithmeticException e) {
            System.out.println("0不能作為被除數");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("arry[]的長度是5，陣列下標越界了");
        }
        System.out.println("例外處理後繼續運行程式");
    }
}
```
```
z=2

Exception in thread "main" java.lang.NullPointerException
	at Practice.Draft.main(Draft.java:15)
```
#### throws
> 宣告在方法的頭部，表示誰呼叫此方法，就由誰處理這個例外。

> 方法中必須宣告所有可能發生的例外。

> 呼叫者可以選擇用try/catch處理，或者用throws再次丟出。
```
public class Draft {
    public static void main(String[] args) {

        try {
            Draft df = new Draft();
            df.throwsTest(3);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("由呼叫的地方處理例外");
        }
        System.out.println("例外處理後繼續運行程式");
    }

    public void throwsTest(int x) throws ArrayIndexOutOfBoundsException, NullPointerException {

        int[] array = {1, 2, 3};
        System.out.println(array[x]);
        
    }
}
```
* 就算方法中沒有宣告可能發生的例外，呼叫方還是能處理，宣告是讓程式碼易讀。
```
public class Draft {
    public static void main(String[] args) {

        try {
            Draft df = new Draft();
            df.throwsTest(3);
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("由呼叫的地方處理例外");
        }
        System.out.println("例外處理後繼續運行程式");
    }

    public void throwsTest(int x) {

        int[] array = {1, 2, 3};
        System.out.println(array[x]);
        
    }
}
```
```
由呼叫的地方處理例外

例外處理後繼續運行程式
```
#### throw
> 在一個方法中，可以有多條throw語句

> 兩種用法: throw 例外物件名; / throw new 例外類別名();

~~使用throw關鍵字，必須用try/catch自己捕獲處理，或者是在頭部用throws再拋出給呼叫者處理~~

* 範例1
```
public class Draft {
    void findThows() {
        try {
            throw new ArithmeticException();
        } catch (ArithmeticException ae) {
            throw ae;   //throw 例外物件名;
        }
    }

    public static void main(String args[]) {
        Draft ct = new Draft();
        //對方法進行例外處理
        try {
            ct.findThows();
        } catch (ArithmeticException ae) {
            System.out.println("出現例外的原因是:" + ae);
        }
    }
}

//出現例外的原因是:java.lang.ArithmeticException
```
* 範例2
```
//因沒有用catch捕捉，會炸掉直接中斷，由系統處理，後續程式碼After throw_do then print也不會執行。

public class Draft {
    public static void main(String[] args) {
        try {
            System.out.println("Only try,no have catch");
            throw_do();
            System.out.println("After throw_do then print");
        } finally {
            System.out.println("finally excuting");
        }
    }

    public static void throw_do() {
        throw new ArithmeticException();   //throw new 例外類別名();
    }
}

```
```
Only try,no have catch

finally excuting

Exception in thread "main" java.lang.ArithmeticException
```
* 範例3-1
```
//可以在包在try丟出，用catch去接

public class Draft {
    public static void main(String[] args) {
        try {

            throw new Exception();

        } catch (Exception e) {

            System.out.println("自己丟自己處理");
        }
    }
}

//自己丟自己處理
```
* 範例3-2
```
//也可以直接丟出，在呼叫方處理

public class Draft {
    public static void main(String[] args) {
        try {
        
            System.out.println("123");
            test();
            
        } catch (ArithmeticException e) {
            System.out.println("ArithmeticException");
        }
    }

    public static void test() {
        throw new ArithmeticException();
    }
}

//123
//ArithmeticException
```
#### 自訂例外
> 1.必須繼承Throwable / Exception / RuntimeException其中之一。
> 2.必須有一個預設的無參數建構子。
> 3.必須有一個帶String參數建構子。
```
public class MyException extends Exception {
	
	public MyException() {
	}
	
	public MyException(String message) {
		super(message);
	}
}
```
```
public class TestMyException {

	public static void main(String[] args) {
		try {

			throw new MyException("發生自訂的例外了!");

		} catch (MyException e) {
			System.out.println(e.getMessage());
		}
	}
}

//發生自訂的例外了!
```
#### commit & rollback
> 所有的DML語句都要顯示提交，就是要執行COMMIT / ROLLBACK。

> DML 語句就是 INSERT / DELETE / UPDATE / SELECT。

> DML 語句，執行完之後，處理的數據，都會放在回滾段中，等待用戶進行提交（COMMIT）或者回滾（ROLLBACK），當用戶執行COMMIT / ROLLBACK 後，放在回滾段中的數據就會被刪除。

> 1.若指令皆正確,則執行 commit 完成異動 => 相關 table 資料被更新。

> 2.若指令有任何一條錯誤,則執行 rollback 取消異動 => 相關 table 資料維持原狀。

> COMMIT後就不能ROLLBACK了。

> 必須提交，因為如果沒有執行 commit 或是 rollback，那麼資料會持續處於鎖定狀態，造成其他使用者必須繼續等待。

> 同一條session，尚未commit前，可以查到先前insert的資料。

#### 輸入/輸出流

* 範例1
```
public class Draft {
    public static void main(String args[]) {
        int c;
        
        //產生輸入流
        InputStreamReader in = new InputStreamReader(System.in);
        
        //在console產生輸出流
        OutputStreamWriter out = new OutputStreamWriter(System.out);
        
        try {
            System.out.println("請輸入一行字元,並按enter鍵結束");
            while ((c = in.read()) != '\n') {
                out.write(c);
            }
            
            out.close();    //如果不關閉輸出流，則螢幕上什麼顯示也沒有
            in.close();
        } catch (IOException e) {
            System.out.println("輸入流有誤!");
        }
    }
}
```
#### 執行緒概述
> 執行緒之間是各自獨立的，各自做自己的事情不彼此影響，補貨&結帳。

> 呼叫執行緒物件的start()方法(即啟動執行緒),執行物件中的run方法。

> xx.start();只能用一次，xx物件跑完就死亡了。

> 當無法繼承Thread的時候可以選擇實作Runnable。

* 建構子
```
Thread()

Thread(Runnable target)

Thread(Runnable target, String name)

Thread(String name)

Thread(ThreadGroup group, Runnable target)

Thread(ThreadGroup group, Runnable target, String name)

Thread(ThreadGroup group, Runnable target, String name, long stackSize)

Thread(ThreadGroup group, String name)


Runnable target = Runnable物件
String name = 新執行緒的名稱
ThreadGroup group = 執行緒組
```

* 繼承Thread
```
public class CounterThread extends Thread {
    int counter = 5;

    public CounterThread() {
    } 

    public void run() { 
        while (counter > 0) {
            System.out.println(counter);
            counter--;

            try {
                Thread.sleep(1000); // 暫停一秒
            } catch (Exception e) {
            }
        }
    }

    public static void main(String args[]) {
        CounterThread t1 = new CounterThread(); 
        CounterThread t2 = new CounterThread();
        t1.start();
        t2.start();
    }
}
```
```
5
5
4
4
3
3
2
2
1
1
```
* 實作Runnable
```
public class CounterRunnable implements Runnable {
    int counter = 5;

    public CounterRunnable() {
    }

    public void run() {
        while (counter > 0) {
            System.out.println(counter);
            counter--;

            try {
                Thread.sleep(1000);
            } catch (Exception e) {
            }
        }
    }

    public static void main(String arg[]) {

        CounterRunnable r1 = new CounterRunnable();
        Thread t1 = new Thread(r1);

        CounterRunnable r2 = new CounterRunnable();
        Thread t2 = new Thread(r2);

        t1.start();
        t2.start();
    }
}
```
```
5
5
4
4
3
3
2
2
1
1
```
#### 執行緒的同步(synchronized)
> 當一個物件(或變數)同時被多個執行緒存取，那麼這個物件必須使用執行緒同步。

> 同步有三種方式: 1.同步程式碼區塊 2.同步方法 3.同步類別資料
```
synchronized (this) { 
    out.println(name + " getting balance..."); 
    balance = getBalance(); 
    out.println(name + " balance got is " + balance); 
    balance += amount; 
    out.println(name + " setting balance..."); 
    setBalance(balance); 
} 
```
```
synchronized public void produce(int qty) {
    while (stock > 20) {
    System.out.println("庫存量超過20，暫停生產");
    try {
        wait();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
}
```
```
synchronized (Testsync2.class)
```
> 同步相關方法
```
wait() : 會無條件釋放搶到的旗標(Lock)。

sleep() : 不會釋放物件旗標(Lock)。

notify() : 喚醒一個wait狀態的執行緒。

notifyAll() : 喚醒所有wait狀態的執行緒。

yield() : 暫停目前正在執行的執行緒物件，並執行其他執行緒。
```

* 範例1
```
public class Draft {
    public static void main(String[] args) {
        ThreadTest1 t1 = new ThreadTest1();
        new Thread(t1).start();
        new Thread(t1).start();
        System.out.println(t1.call());
    }
}

class ThreadTest1 implements Runnable {
    private int x;
    private int y;

    public synchronized void run() {
        for (int i = 0; i < 4; i++) {
            x++;
            y++;
            try {
                Thread.sleep(200);
            } catch (InterruptedException e) {
                System.out.println("執行緒出錯了");
            }
            System.out.println(Thread.currentThread().getName() + " x=" + x
                    + ",y=" + y + "  " + i);
        }
    }

    public synchronized String call() {
        String name = Thread.currentThread().getName();
        return "Hellow " + name;
    }
}
```
```
Hellow main
Thread-0 x=1,y=1  0
Thread-0 x=2,y=2  1
Thread-0 x=3,y=3  2
Thread-0 x=4,y=4  3
Thread-1 x=5,y=5  0
Thread-1 x=6,y=6  1
Thread-1 x=7,y=7  2
Thread-1 x=8,y=8  3
```
#### 轉發（forward）和重定向（redirect）區別
```
在Servlet中兩種實現： 

forward方式：request.getRequestDispatcher("/somePage.jsp").forward(request, response);

redirect方式：response.sendRedirect("/somePage.jsp");
	  
1.forward是服務器內部重定向，程序收到請求後重新定向到另一個程序，客戶機並不知道。
	  
2.forward是容器中控制權的轉向，在客戶端瀏覽器地址欄中不會顯示出轉向後的地址。
	  
3.forward 會將 request state , bean 等等信息帶往下一個 jsp 。
		  
4.使用 forward 你就可以用 getAttribute() 來取的前一個 jsp 所放入的 bean 等等資料。
	  
5.與redirect方式相比，forward更加高效。
	  
	  
1.redirect則是服務器收到請求後發送一個狀態頭給客戶，客戶將再請求一次，這裏多了兩次網絡通信的來往。
	  
2.redirect是完全的跳轉，瀏覽器將會得到跳轉的地址，並重新發送請求鏈接。這樣，從瀏覽器的地址欄中可以看到跳轉後的鏈接地址。
	  
3.redirect 是送到 client 端後再一次 request , 所以資料不被保留。
```
### 練習題
#### 陣列求最大值
```
public class Draft {
    public static void main(String args[]) {
        int[] array = new int[10];

        for(int i=0;i<array.length;i++){
            array[i] = (int)(Math.random()*100)+1;
        }
        
        Arrays.sort(array);

        System.out.println(Arrays.toString(array));

        int max = array[0];
        for(int i=1;i<array.length;i++){
            if(array[i]>max){
                max = array[i];
            }
        }
        System.out.println(max);
    }
}
```
#### switch觀念
```
//case後面的值不能是變數或者運算式，case b:編譯錯誤
//如果是final修飾並設定初始值的變數就可以

public class Draft {

    final static short a = 3;
    public static int b = 1;

    public static void main(String[] args) {
        for (int c = 0; c < 5; c++) {
            switch (c) {
                case b:
                    System.out.print("4 ");
                case a - 1:
                    System.out.print("5 ");
                case a:
                    System.out.print("6 ");
            }
        }
    }
}

//編譯錯誤
```
```
public class Draft {

    final static int a = 3;
    public static int b = 1;

    public static void main(String[] args) {
        for (int c = 0; c < 5; c++) {
            switch (c) {
                case a - 2:
                    System.out.print("4 ");
                    break;
                case a - 1:
                    System.out.print("5 ");
                    break;
                case a:
                    System.out.print("6 ");
                    break;
            }
        }
    }
}

//4 5 6 
```
#### switch判斷是否為母音小寫字母
```
public class Draft {
    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        char y;
        while (true) {
            System.out.println("please insert");
            String x = sc.next();
            y = x.charAt(0);
            if (!(y < 97 || y > 122)) {
                break;
            } else {
                System.out.println("重新輸入");
            }
        }
        
        switch (y) {
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                System.out.println(y + "是母音小寫字母");
                break;
            default:
                System.out.println(y + "不是母音小寫字母");
        }
    }
}
```
#### 字串只取英文部分
```
public class CharClass {
    public static void main(String[] args) {

        String str = "AHCT001";

        int index = 0;
        for (int i = 0; i < str.length(); i++) {
            if (str.charAt(i) >= 48 && str.charAt(i) <= 57) {
                index = i;
                break;
            }
        }
        
        String insknd = str.substring(0, index);
        System.out.println(insknd);

    }
}

//AHCT
```
#### return中斷
```
//到return RESULT_EXCEL_NO_DATA; 會直接跳出，設定相關參數不會執行到

	if (CollectionUtils.isEmpty(reportList)) {

		addActionMessage("報表查詢無資料");
		return RESULT_EXCEL_NO_DATA;
        
	}
	// 設定相關參數	
	this.setExporterMap(ExcelReportUtils.processExcelParamter());


```