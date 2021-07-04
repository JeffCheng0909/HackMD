# 基礎Java


### 方法大全

#### Integer and String
```
//通常方法名是什麼，就返回什麼

#Integer i = new Integer(123); //boxing

#int x = i.intValue(); //unboxing


#Integer x = Integer.valueOf("123"); //字串轉Integer物件

#int y = Integer.parseInt("456"); //字串轉int


#String z = String.valueOf(789) //數字轉字串 [可將各種型態轉為字串，推薦使用]

#String z = Integer.toString(789); //數字轉字串


example:
String num;
Integer.parseInt(num);  //return int
Integer.valueOf(num).intValue();  //return int


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
//Math.round負值為五捨六入

System.out.println(Math.round(-0.5)); //0
System.out.println(Math.round(-1.5)); //-1
System.out.println(Math.round(-2.5)); //-2

System.out.println(Math.round(-0.6)); //-1
System.out.println(Math.round(-1.6)); //-2
System.out.println(Math.round(-2.6)); //-3
```
### 方法基本觀念
```
1. 方法一定要放在某個類別裡面。

2. 方法宣告都是獨立分開的，不可以在一個方法內又宣告另一個方法，但可以呼叫。

3. 同一個class內，兩個不同方法，可直接在A方法內調用B方法，不用new新物件。

4. 只能在方法內調用(呼叫)其他方法。

5. 靜態方法不用new物件即可直接使用。(在同類別直接打 方法名 使用)(在不同類別用 靜態方法所在類別名.方法名 使用)

6. 非靜態方法(同類別直接打 方法名 使用)(不同類別用 物件名.方法名 使用)

7. static方法不可使用this，因為this代表物件。

8. static方法只能存取static方法和變數。 (要存取non-static方法就必須先new出物件。)

9. non-static方法可以存取non-static and static方法和變數。
```

### Getter / Setter
```
// 當實體變數為private。在同一個class下，可使用. 或者public的 Getter/Setter存取。
// 當實體變數為private。在不同class下，只能使用public的 Getter/Setter存取。

// .可用於Get or Set，但不管是不是同類別，前面都必須有物件名， xxx.變數名。

// 當實體變數為public，在任何class下，可使用. 或者public的 Getter/Setter存取。
// 同class可直接使用方法名呼叫Getter/Setter，但使用 . 則必須new物件出來。
// 不同class必須要new物件出來才能使用Getter/Setter 以及 .。

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
//.可用於Get or Set，但前面必須有物件名

public static void main(String[] args) {

    Material mm = new Material();
    mm.salary=100; //set 100
    System.out.println(mm.salary); //get 100
       
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

### 巢狀三元運算子
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

3. IntStream
```
//印出一到九的數字
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

#### 使用方法複製 (深拷貝範例)
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

#### ==及Equals
```
基本型別只有 == 比值，沒有Equals方法。

參考型別的==跟equals都是比記憶體位置。

String以及Integer等類別可以使用equals來比較內容，是因為override過Object的equals方法。
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

2. 不能用private、static、final修飾抽象方法。

3. 抽象類別還是可以宣告建構子，為了讓後面的子類別可以把共同的資料交給父類別完成設定。

4. 抽象方法沒有方法主體，連{}都沒有，且必須加上abstract修飾子。

5. 抽象類別無法產生實體，即無法new新物件。

6. 子類別繼承了抽象父類別，並實作出父介面所有抽象方法，此子類別就不再是抽象類別，即可以new新物件。
```

#### Interface
```
1. 介面是一種所有方法皆為抽象方法的抽象類別。

2. 介面內所有方法預設皆是abstract、public，故可省略不寫，也不可更改。

3. 介面沒有建構子。

4. 介面與介面之間是可以再繼承的(extends)。

5. 介面不能new新物件 (Interfaces cannot be instantiated)。

6. 子類別必須implements父介面後，並實作出父介面所有抽象方法，此子類別就不再是抽象類別，即可以new新物件。

7. 使用介面主要目的為:1.實現多重繼承 2.預先定義規格 3.貼標籤(空介面) 4.型態轉換(父多型) 5.降低相依性。

8. 使用介面好處，可代替類別繼承時需全盤繼承的缺點，但還是能具有共同的行為。
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
