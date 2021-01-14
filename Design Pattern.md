# Design Pattern

### Factory Method Pattern 工廠模式
定義一個用於建立物品的介面，讓子類決定實體化哪一個類別。工廠方法使一個類別的實例化延遲到其子類別。
```
public interface Product {
    //敘述自己是什麼商品
    public void describe();
}
```
```
public interface Factory {
    //工廠返回商品
    public Product getProduct();
}
```
```
public class FrenchFries implements Product{

    //預設有鹽巴的
    String state = "有鹽巴";
    //預設的建構
    protected FrenchFries(){}
    //帶入狀態的建構
    protected FrenchFries(String state){
        this.state = state;
    }

    @Override
    public void describe() {
        System.out.println("我是"+ state +"薯條");
    }
}
```
```
public class FrenchFriesFactory implements Factory {

    //返回一般的薯條
    @Override
    public Product getProduct() {
        return new FrenchFries();
    }

    //返回我們想要的狀態的薯條..
    public Product getProduct(String state) {
        return new FrenchFries(state);
    }
}
```
```
        Factory friesFac = new FrenchFriesFactory();
        Product fries = friesFac.getProduct();
        Product myfries = ((FrenchFriesFactory) friesFac).getProduct("無鹽的");

        fries.describe();//我是有鹽巴薯條
        myfries.describe();//我是無鹽的薯條
```

### Proxy Pattern 代理模式
為其他物件提供一種代理以控制對這個物件的存取。

```
public interface IBuyHouse {

//    找適合的房子
    public void findHouse();

//    跟屋主說太貴
    public void priceTooHigh();

//    屋主防禦價錢
    public void defendPrice();

//    成交後，簡化從付訂金到交屋的過程。
    public void finish();

}
```
```
public class LittleEngineer implements IBuyHouse {
    @Override
    public void findHouse() {
//        小小工程師想找在民生社區的房子
        System.out.println("民生社區機能特好！當然找那邊的房子！");
    }

    @Override
    public void priceTooHigh() {
//        價錢實在太貴
        System.out.println("現在台灣薪水那麼低，屋主開那麼高賣不掉啦！");
    }

    @Override
    public void defendPrice() {
//        屋主反擊說價錢已經很便宜
        System.out.println("未來人口越來越少，我們也是自住而已！打我五折吧！");
    }

    @Override
    public void finish() {
//        沒想到屋主同意買到了
        System.out.println("辛苦還房貸幾十年");
    }
}
```
```
public class EstateAgent implements IBuyHouse {

    private IBuyHouse iBuyHouse;

    public EstateAgent(IBuyHouse iBuyHouse){
        this.iBuyHouse = iBuyHouse;
    }

    @Override
    public void findHouse() {
        iBuyHouse.findHouse();
        System.out.println("#房仲幫忙找房子");
    }

    @Override
    public void priceTooHigh() {
        iBuyHouse.priceTooHigh();
        System.out.println("#房仲幫忙喬價錢");
    }

    @Override
    public void defendPrice() {
        iBuyHouse.defendPrice();
        System.out.println("#房仲強力喬價錢");
    }

    @Override
    public void finish() {
        System.out.println("#成交的話房仲幫忙付訂、簽約、用印、完稅、交屋");
        iBuyHouse.finish();
    }
}
```
```
public class Test {
    @org.junit.jupiter.api.Test
    public void test(){
        IBuyHouse littleEngineer = new LittleEngineer();

        IBuyHouse estateAgent = new EstateAgent(littleEngineer);

        estateAgent.findHouse();
        estateAgent.priceTooHigh();
        estateAgent.defendPrice();
        estateAgent.finish();

    }
}
```
```
民生社區機能特好！當然找那邊的房子！
#房仲幫忙找房子
現在台灣薪水那麼低，屋主開那麼高賣不掉啦！
#房仲幫忙喬價錢
未來人口越來越少，我們也是自住而已！打我五折吧！
#房仲強力喬價錢
#成交的話房仲幫忙付訂、簽約、用印、完稅、交屋
辛苦還房貸幾十年
```
### Singleton 單例模式
只有一個類別，其中提供存取自己物件的方法，確保整個系統只有實例化一個物件。

**有幾種方式可以實現單例模式:**
* 懶散(Lazy)模式（線程不安全）
* 懶散模式（線程安全）
* 積極模式
* 雙重鎖 (Double ChockLock)
* 登記式（靜態內部類）
* 枚舉 (enumeration)

```
//試著實現一個積極單例模式

public class SingleObject {
 
   //創建 SingleObject 的一個對象
   private static SingleObject instance = new SingleObject();
 
   //讓構造函數為 private，這樣該類就不會被實例化
   private SingleObject(){}
 
   //獲取唯一可用的對象
   public static SingleObject getInstance(){
      return instance;
   }
 
}
```
```
//試著實現一個懶散單例模式

public class Singleton{
    private static Singleton instance;
    //私有的建構式讓別人不能創造
    private Singleton (){}
    
    //因為整個系統都要存取這個類別，很可能有多個process或thread同時存取
    //為了讓線程安全添加synchronized在多線程下確保物件唯一性
    public static synchronized Singleton getInstance(){
        if (instance == null)
        {
            instance = new Singleton();
        }
        return instance;
    }
}

```
```
//試著用雙重鎖實現(推薦使用)

public class Singleton {
    public static Singleton instance;

    private Singleton(){}

    public static Singleton getInstance(){

//        第一層判斷為了避免不必要的同步
        if(instance == null){
            
            synchronized (Singleton.class){
//                第二層判斷為了在null的狀況下建立實例
                if(instance == null){
                    instance = new Singleton();
                }
            }

        }

        return instance;
    }
}
```
```
//試著用靜態內部類實現(推薦使用)

public class StaticInnerClass {
    private StaticInnerClass(){}

    public static StaticInnerClass getInstance(){
        return StaticInnerClassHolder.instance;
    }

    /**
     * 靜態的內部類別
     */
    private static class StaticInnerClassHolder{
        private static StaticInnerClass instance = new StaticInnerClass();
    }
}
```

**試著寫出SingletonFactory**
```
public abstract class Product {
    public String getName(){
        return this.getClass().getSimpleName();
    }
}

public interface Factory {
    public Product getProduct();
}
```
```
public class Cola extends Product {
}
public class Humberger extends Product {
}
```
```
public class SingletonFactory {

    public static Factory getColaFactory(){
        return ColaFactory.colaFactory;
    }

    public static Factory getHumbergerFactory(){
        return HumbergerFactory.humbergerFactory;
    }


    private static class ColaFactory implements Factory{

        private static ColaFactory colaFactory = new ColaFactory();

        private ColaFactory(){}

        @Override
        public Product getProduct() {
            return new Cola();
        }
    }

    private static class HumbergerFactory implements Factory{

        private static HumbergerFactory humbergerFactory = new HumbergerFactory();

        private HumbergerFactory(){}

        @Override
        public Product getProduct() {
            return new Humberger();
        }
    }
    
}
```
```
public class Test {

    public void test(){

        Cola cola = (Cola) SingletonFactory.getColaFactory().getProduct();
        Humberger humberger =(Humberger) SingletonFactory.getHumbergerFactory().getProduct();
        
        System.out.println(cola.getName());
        System.out.println(humberger.getName());

    }

}
```
```
Cola
Humberger
```


