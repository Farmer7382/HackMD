# Java8 Lambda 
#### Stream
```
1. Stream 可以執行一系列的操作，用起來很像 Builder 模式，操作是以一個接一個的方式串起來。

2. Stream 方法的串接規則，中間串接的永遠是回傳 Stream 型別的方法，只有最後一個才是串接傳回某個非 Stream 型別的值的方法。

3. 在 API 文件中，屬於終止操作的方法，會有「 This is a terminal operation. 」這樣的標示，表示這個方法只能串接在最後一個。

4. Stream 提供 filter、sort、map 等功能。
```
* IntStream
```
// 原始寫法
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}

// 簡化寫法
IntStream.range(0, 10).forEach(i -> System.out.println(i));

// Method References寫法
IntStream.range(0, 10).forEach(System.out::println);
```
```
show 0 ~ 9
```
* count
```
public class Test {
    public static void main(String args[]) {

        long count = Stream.of("Tony", "Tom", "John", "Amy", "Emma", "Iris").count();
        System.out.println("count: " + count);
    }
}
```
```
count: 6
```
* max, min
```
to be fill
```
* sorted
```
to be fill
```



#### collect
> 用 collect 方法來收集，回傳集合
```
public class Test {
    public static void main(String args[]) {

        List<String> names1 = Stream.of("Tony", "Tom", "Jonn").collect(Collectors.toList());
        
        List<String> names2 = Stream.of("Tony", "Tom", "Jonn").collect(Collectors.toCollection(ArrayList::new));
        
        List<String> names3 = Arrays.asList("Tony", "Tom", "Jonn");
        
        Set<String> names4 = Stream.of("Tony", "Tony", "Tony", "Tom", "Jonn").collect(Collectors.toSet());
        
        System.out.println(names1.toString());
        
        System.out.println(names2.toString());
        
        System.out.println(names3.toString());
        
        System.out.println(names4.toString());
    }
}
```
```
[Tony, Tom, Jonn]
[Tony, Tom, Jonn]
[Tony, Tom, Jonn]
[Tony, Tom, Jonn]
```


#### filter
> filter(Boolean)，過濾符合()內標準的東西
```
public class Test2 {
    public static void main(String[] args) {

        List<Integer> numbers = Lists.newArrayList(1, 2, 3, 4);
        
        Stream<Integer> even = numbers.stream().filter(e -> e % 2 == 0);

        List<Integer> evenNumbers = even.collect(Collectors.toList());
    
        System.out.println(evenNumbers);
        
    }
}
```
```
[2, 4]
```
```
public class Test {
    public static void main(String args[]) {
        
        List<String> names2 = Stream.of("Tony", "Tom", "John", "Andy")
                .filter(name -> name.startsWith("T"))
                .collect(Collectors.toList());

        System.out.println(names2.toString());
        
    }
}
```
```
[Tony, Tom]
```
#### map
> map (將某個輸入資料轉換成另一個資料輸出)
* 轉換大寫
```
public class Test {
    public static void main(String args[]) {
    
        List<String> list = Arrays.asList("aaa", "bbb", "ccc");
        
        list = list.stream().map(f -> f.toUpperCase()).collect(Collectors.toList());
        
        // Method References寫法
        list = list.stream().map(String::toUpperCase).collect(Collectors.toList());
        
        System.out.println(list);
    }
}
```
* 轉換大寫-其他方法
```
public class Test {
    public static void main(String args[]) {

        List<String> list = Arrays.asList("aaa", "bbb", "ccc");

        list.replaceAll(f -> f.toUpperCase());

        System.out.println(list); 
    }
}
```
```
public class Test {
    public static void main(String args[]) {

        List<String> list = Arrays.asList("aaa", "bbb", "ccc");
        List<String> resultList = new ArrayList<>();
          
        for(String str : list){
            resultList.add(str.toUpperCase());
        }

        System.out.println(resultList);
    }
}
```
```
[AAA, BBB, CCC]
```
#### filter vs map
```
public class Test {
    public static void main(String args[]) {

        List<Integer> numbers = Arrays.asList(1, 2, 3, 4);

        List<Integer> mod2List1 = numbers.stream().map(f -> f % 2).collect(Collectors.toList());
        List<Integer> mod2List2 = numbers.stream().filter(f -> f % 2 == 0).collect(Collectors.toList());
        
        System.out.println(mod2List1);
        System.out.println(mod2List2);
    }
}
```
```
[1, 0, 1, 0]
[2, 4]
```
#### forEach
```
List features = Arrays.asList("Lambdas", "Default Method", "Stream API", "Date and Time API");

features.forEach(n -> System.out.println(n));

//另一種寫法
features.forEach(System.out::println);
```
####  Predicate介面
> Predicate 是用作 lambda 表示式或方法引用的賦值目標的功能介面
* 簡介
```
Predicate<Integer> noGreaterThan5 =  x -> x > 5;

我們建立了一個名為 noGreaterThan5 的 Predicate。該 Predicate 採用整數輸入；
因此，T 在這裡是整數。該 Predicate 將檢查輸入引數是否大於 5。
```
* 範例
```
public class Test {
    public static void main(String[] args) {

        Predicate<String> nameGreaterThan4 = x -> x.length() > 4;
        
        List<String> name = Arrays.asList("Ram", "Karan", "Aarya", "Rahul", "Om", "Pranav" );
        
        //將Predicate標準放入filter引數
        List<String> name_filtered = name.stream().filter(nameGreaterThan4).collect(Collectors.toList());
        
        System.out.println(name_filtered);
        
    }
}
```
```
public class Test {
    public static void main(String args[]) {

        List<String> name = Arrays.asList("Ram", "Karan", "Aarya", "Rahul", "Om", "Pranav" );

        //直接在filter引數內建立標準
        List<String> name_filtered = name.stream().filter( x -> x.length() > 4).collect(Collectors.toList());

        System.out.println(name_filtered);
        
    }
}
```
```
[Karan, Aarya, Rahul, Pranav]
```
#### ::用法
> 類名：：方法名
```
 person -> person.getAge();
 
 Person：：getAge
 
 
 new HashMap<>()
 
 HsahMap :: new
 
 
```
#### LocalDate
```
to be fill
```

#### Optional
* 舊寫法
```
public static void main(String[] args) {
    String nickName = getNickName("Duke");
    if (nickName == null) {
        nickName = "Openhome Reader";
    }
    out.println(nickName);
}

private static String getNickName(String name) {
    Map<String, String> nickNames = new HashMap<>(); // 假裝的鍵值資料庫
    nickNames.put("Justin", "caterpillar");
    nickNames.put("Monica", "momor");
    nickNames.put("Irene", "hamimi");
    return nickNames.get(name); // 鍵不存在時會傳回null
}
```
* 新寫法
```
public static void main(String[] args) {
    Optional<String> nickNameOptional = getNickName("Duke");
    String nickName;
    if(nickNameOptional.isPresent()) {
        nickName = nickNameOptional.get();
    } else {
        nickName = "Openhome Reader";
    }

    System.out.println(nickName);
}

private static Optional<String> getNickName(String name) {
    Map<String, String> nickNames = new HashMap<>(); // 假裝的鍵值資料庫
    nickNames.put("Justin", "caterpillar");
    nickNames.put("Monica", "momor");
    nickNames.put("Irene", "hamimi");

    String nickName = nickNames.get(name);

    if(nickName == null) {
        return Optional.empty();
    } else {
        return Optional.of(nickName);
    }
}
```