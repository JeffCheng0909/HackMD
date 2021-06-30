# JavaScript

### 概述

script 標籤 (HTML tag) 中被瀏覽器執行。而 <script> 標籤可以放在網頁 HTML 的任何地方，像是 <body> 或 <head> 中。
```
<!doctype html>
<html>

<head>
<script>
    alert('Hello world!');
</script>
</head>

<body>
My first JS page!
</body>
</html>
```
瀏覽器遇到 <script> 標籤時，會停止解析 HTML 文件，來先執行 <scipt> 裡面的 JS 程式碼，等到執行完程式碼，才會繼續解析接下來的 HTML 文件。

### 引用JavaScript 檔案

`<script src="JavaScript 檔案位址.js"></script>`
`<script src="/hello.js"></script>`

引用外部的 JavaScript 檔案，例如引用 jQuery library:
`<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>`

### 註解(Comment)
```
// 這是單行註解

/*
這是...
多
行
註解
*/
```

### 空白 (whitespace)
空白 (space), tab 或換行符號 (newline characters) 在 JavaScript 都稱為空白 (whitespace)，JavaScript 程式碼在解析時，會忽略所有的空白，所以你可以自由利用空白字元來編排你的程式碼讓它更好讀。
```
var x = ['stringggggggggg1', 'stringggggggggg2', 'stringggggggggg3'];

// 這個寫法，和上面的意思是一模一樣的
var x = [
    'stringggggggggg1',
    'stringggggggggg2',
    'stringggggggggg3'
];
```
### 有區分大小寫 (case sensitive)
不像 HTML，JavaScript 語句是有區分大小寫的，無論是對於變數、函數或物件名稱，如 alert() 寫成 Alert() 是會產生錯誤的。

### 變數 (variable)
```
//可以用 var 關鍵字來宣告一個變數
//例如，我們宣告一個變數 x，並將 x 的值設為 100：
var x;
x = 100;

//你也可以在宣告變數的同時指定值
var x = 100;

//你也可以用逗號 , 分隔開，一次宣告多個變數
var fruit1, fruit2;
```

### 變數作用域 (Variable Scope)
JavaScript 的變數有其作用的範圍，在作用範圍以外的程式碼就無法存取到該變數。

JavaScript 的 scope 是所謂的 function scope，亦即一個 function 中會建立一個新的 scope。

```
// 在 function 裡面宣告的變數，作用(存在)範圍只在 function 裡面 (local)

function foo() {
    var carName = 'Ferrari';
    alert(carName); // 會顯示 Ferrari
}

alert(carName); // 會發生錯誤，因為找不到變數
```

```
// 在 function 以外的地方宣告的變數，是所謂的全域變數 (global variable)，
所有的 JS 程式碼都能存取到這個變數

// carName 是一個全域變數
var carName = 'Ferrari';
    
function foo() {
    alert(carName); // 會顯示 Ferrari
}

alert(carName); // 會顯示 Ferrari
```

> !注意: JavaScript 不像其他程式語言有 package level 的 scope，只有 global 或 local，所以一個 global variable 在任何地方都可以被存取到，甚至是跨不同的 JS 檔案的程式碼。

> 所以一般會避免使用全域變數，避免全域的命名空間 (namespace) 被污染，不同檔案的同名全域變數很容易被意外互相覆蓋。

### 駝峰式命名 (Camel Case)
JavaScript 習慣的變數命名風格是所謂的駝峰式命名 (camel case)。

像是 firstName, lastName, carName，也就是第二個字的字母大寫。

### JavaScript 資料型態 (Data Types)

#### 1.基本資料型態 (primitive data types)
1. 布林值 (Boolean): 只包含兩種值 true / false
2. null: null 是一個特殊值 (keyword)，表示這變數裡面沒有東西
3. undefined: undefined 也是一個特殊值 (keyword)，表示值還沒有定義或還未指定
4. 數值 (Number): 數值類型的值，像是 42 / 3.14159 / 0
5. 字串 (String): 像是 'hello world' / 汽車


#### 2.參考資料型態 (reference data types)
1. 陣列 (Array): 陣列用來儲存多個資料，陣列中的資料數量，就是這個陣列的長度 (length)
2. 物件 (Object): 基本上，基本資料型態以外的都是物件型態
3. 方法 (Function): 特殊型別
4. Boolean、Number、String、Math、Date...etc

#### 補充-參考資料型態
布林、數值和字串三種基本型別都有個別對應到一個物件類別，透過該物件類別包裝後，可以進行函式操作，例如字串物件可使用substr()等函式。可以透過下面的方式將型別包裝成物件與操作：
```
var b = new Boolean(false);
var n = new Number(5566);
var s = new String('friend');
 
// 包裝後型別為object
console.log(typeof(b)); // object
console.log(typeof(n)); // object
console.log(typeof(s)); // object
 
// 由於自動轉型，仍然可以比較
console.log(b == false);    // true
console.log(n == 5566);     // true
console.log(s == 'friend'); // true
```
### JavaScript 是動態型別的語言 

JavaScript 是動態型別的語言，你在宣告變數的時候，不用指定一個型別給這變數。
```
// 例如你不用像這樣，跟 JS 直譯器說 score 是一個數字
int score = 101;
```
JavaScript 直譯器 (Interpreter, 也就是瀏覽器) 會根據你給的值，自動給一個適當的型態。
```
// 所以只需要這樣直接宣告變數並給值
var score = 101;
```
動態型別的意思也是說，你可以隨時指定不同型態的值，給同樣一個變數。
```
var score = 101; // 數值型態
score = 'Mike 得到 101 分'; // 字串型態
```

### typeof
typeof 運算字用來判斷一個運算元 (operand) 是什麼資料型態。

> 適用於判斷基本型別。

> 對於參考資料型別，除了function會返回function外，其他一律會返回Objecct型別，無法精確判斷。
```
// 輸出 string
console.log(typeof 'hello');

// 輸出 number
console.log(typeof 123);

// 輸出 boolean
console.log(typeof true);


let arr = [1,2,3];
let obj = {name: 'jartto'};
let obj1 = null;

// 輸出 object
console.log(typeof arr);

// 輸出 object
console.log(typeof obj);

// 輸出 object (instanceof Object會顯示false)
console.log(typeof obj1);

// 輸出 function 
console.log(typeof function(){});
```
### instanceof 
instanceof 運算字用來判斷型別以及繼承關係。

> 適用於判斷參考資料型別。

> 對於基本資料型別不能被instanceof精確判斷，一律會返回false。
```
// 輸出 false
console.log('hello' instanceof String);

// 輸出 true
console.log(new String('str') instanceof String);

// 輸出 false
console.log(123 instanceof Number);

// 輸出 true
console.log(new Number(2) instanceof Number);

// 輸出 false
console.log(true instanceof Boolean);


let arr = [1,2,3];
let obj = {name: 'jartto'};
let obj1 = null;

// 輸出 true
console.log(arr instanceof Array);

// 輸出 true
console.log(obj instanceof Object);

// 輸出 false
console.log(obj1 instanceof Object);

// 輸出 true
console.log(function(){} instanceof Function); 
```
### JavaScript 運算子 (Operators)
1. 指定運算子 (Assignment Operators)
2. 比較運算子 (Comparison Operators)
3. 算術運算子 (Arithmetic Operators)
4. 位元運算子 (Bitwise Operators)
5. 邏輯運算子 (Logical Operators)
6. 字串運算子 (String Operators)
7. 三元運算子 (Conditional (ternary) operator)


一個二元運算子，需要有兩個運算元，一個在運算子前面，一個在運算子後面
```
1 + 2
x * y
```
一個一元運算子，需要有一個運算元，可能是在運算子前面，或是在運算子後面
```
x++
// 或
++x
```

#### 1.指定運算子 (Assignment Operators)
指定運算子用來指定一個值給一個變數。

| 運算子 | 例子 | 說明 |
| -------- | -------- | -------- |
| =     | x = y     | 將 y 值指定給 x 變數     |
| +=     | x += y     | 意思跟 x = x + y 一樣，將 x y 相加後的值指定回 x 變數     |
| -=     | x -= y     | 意思跟 x = x - y 一樣，將 x y 相減後的值指定回 x 變數     |
| *=    | x *= y     | 意思跟 x = x * y 一樣，將 x y 相乘後的值指定回 x 變數     |
| /=    | x /= y     | 意思跟 x = x / y 一樣，將 x y 相除後的值指定回 x 變數     |
| %=    | x %= y     | 意思跟 x = x % y 一樣，將 x 除以 y 的餘數指定回 x 變數     |

#### 2.比較運算子 (Comparison Operators)
用來比較運算子兩邊運算元的關係，比較後傳回 true 或 false。運算元可以是數值、字串、表達式 (expression) 或物件等。

對於不同型態的值，JavaScript 會嘗試將他們轉型 (type conversion) 到同樣型態後，再做比較，通常是先轉到數值型態。

| 運算子 | 例子   | 說明 |
| -------- | -------- | -------- |
| ==     | 3 == var1     | 如果兩邊相等就返回 true     |
| !=     | var1 != 4     | 如果兩邊不相等就返回 true     |
| ===     | 3 === var1     | 跟 == 的差異在於，=== 不會自動嘗試轉型，型態和值都一樣才會返回 true     |
| !==    | var1 !== '3'     | 跟 != 的差異在於，!== 不會自動嘗試轉型，型態或值不一樣都會返回 true     |
| >    | var2 > var1     | 如果左邊運算元大於右邊的就返回 true     |
| >=    | var1 >= 3	     | 如果左邊運算元大於或等於右邊的就返回 true     |

#### 3.算術運算子 (Arithmetic Operators)
算術運算子用來做常見的加減乘除數值運算。

#### 4.位元運算子 (Bitwise Operators)
用來做二進制的位元運算，位元運算子會將運算元看作 32 bits 位元來做運算，然後運算完後會返回數值型態的結果。

#### 5.邏輯運算子 (Logical Operators)
邏輯運算子用來做布林值 (boolean) 的運算，運算結果傳回 true 或 false。

`例如: &&、||、!`

&& 和 || 還有比較特別的地方，如果運算元的值不是布林值，實際上會傳回其中一個運算元的值
```
// foo 是 Dog
var foo = 'Cat' && 'Dog';

// foo 是 false
// 因為 && 遇到 false 的運算元，就會直接返回，不會繼續再往下判斷 (Short-circuit evaluation)
var foo = false && 'Cat';

// foo 是 Cat
// 因為 || 遇到 true 的運算元，就會直接返回，不會繼續再往下判斷 (Short-circuit evaluation)
var foo = 'Cat' || 'Dog';

// foo 是 Cat
var foo = false || 'Cat';
```
#### 7.三元運算子 (Conditional (ternary) operator)

如果 condition 是 true， 就傳回 val1 的結果，否則傳回 val2 的結果。

`condition ? val1 : val2`

```
// 如果 age 變數大於等於 18，則 status 就會是 adult
// 相反的，如果 age 變數小於 18，則 status 就會是 minor
var status = (age >= 18) ? 'adult' : 'minor';
```

#### 運算子優先權 (Operator precedence)
各種運算子在處理上的優先次序 (precedence) 是依一般算術規則，先乘除後加減，如果你有一些運算要優先處理，可以放在 () 小括號裡面。

```
100 + 50 / 2 = 125
(100 + 50) / 2 = 75
```
### JavaScript 流程控制 (Control flow)
1. if...else [同Java]
2. switch [同Java]
3. for [同Java]
4. while [同Java]
5. label (搭配break、continue好用)
6. try catch finally

#### Falsy values
JavaScript 只有對下面這些值會判斷為 false 其他都是 true
1. 布林值 false
2. undefined
3. null
4. 數值 0
5. NaN
6. 空字串 ''

```
var text = '';
if (text) {
    // 我不會被執行
} else {
    // 我會被執行
}
```

#### switch [同Java]
標準寫法
```
switch (fruitType) {
    case 'Oranges':
        alert('Oranges');
        break;
    case 'Apples':
        alert('Apples');
        break;
    case 'Bananas':
        alert('Bananas');
        break;
    case 'Cherries':
        alert('Cherries');
        break;
    case 'Mangoes':
        alert('Mangoes');
        break;
    case 'Papayas':
        alert('Papayas');
        break;
    default:
        alert('沒有符合的條件');
}
```
break關鍵字重要性

當 JavaScript 執行到 break 這個關鍵字的時後，就會直接跳出整個 switch 區塊，繼續往下執行。

而如果沒有 break 則程式會從符合的 case 區塊開始，一路往下執行到遇到 break 為止！

這種行為我們稱做 Fall-Through。

```
// 如果 fruitType 是 Apples 的時候，會同時執行 Apples, Bananas 和 Cherries 區塊，
// 直到碰到 Cherries 區塊中的 break 為止才會跳出整個 switch 區塊

switch (fruitType) {
    case 'Oranges':
        alert('Oranges');
        break;
    case 'Apples':
        alert('Apples');
    case 'Bananas':
        alert('Bananas');
    case 'Cherries':
        alert('Cherries');
        break;
    case 'Mangoes':
        alert('Mangoes');
        break;
    case 'Papayas':
        alert('Papayas');
        break;
    default:
        alert('沒有符合的條件');
}
```
可以利用這個特性，撰寫像是這類程式碼
```
switch (new Date().getDay()) {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        alert('工作天 :(');
        break;
    case 6:
    case 0:
        alert('週末 :)');
}
```
#### for
標準寫法
```
var counter = 0;
for (var i = 0; i < 5; i++) {
    counter += i;
}

// 上面的迴圈執行完後，最後 counter 的值會是 10！
```
可以用逗點 , 隔開多個初始化語句。
```
for (var i = 0, j=10; i < 5; i++) {
    // .....
}
```
也可以省略 initialExpression 或 incrementExpression 語句。
```
var i = 0;
var counter = 0;
for (; i < 5;) { 
    counter += i;
    i += 1;
}
```
可以省略全部語句 ，這其實就是無窮迴圈 (infinite loop) 的意思。
```
var i = 0;
var counter = 0;
for (;;) {
    counter += i;
    i += 1;
    if (i >= 5) {
        // 如果你沒用 break 跳出 for 迴圈，則整個程式會卡在迴圈裡面出不去喔
        break;
    }
}
```
break: 用來跳出整個 for 迴圈，讓程式繼續往下執行。

continue: 用來讓程式跳過迴圈剩餘的程式碼，直接執行下一次迴圈。

continue: 直接PASS這次for迴圈，迴圈內之後的其他程式碼都不跑。
```
var counter = 0;
for (var i = 0; i < 5; i++) {
    if (i < 3) {
        continue;
    }
    counter += i;
}

// counter 的值會是 7
```

#### label (標籤)
label 可以用來標記一個迴圈，label 用來搭配 break 和 continue 一起使用。

可以發現，當你有多層迴圈的時候，label可以用來很方便的直接跳出外層的迴圈！

用 break; 只會跳出當前這「一個」迴圈。

搭配break使用:
```
var x = 0;
var z = 0;

// 把外層的迴圈標記叫做 labelCancelLoops

labelCancelLoops:
while (true) {
    console.log('Outer loops: ' + x);
    x += 1;
    z = 1;
    while (true) {
        console.log('Inner loops: ' + z);
        z += 1;
        if (z === 3 && x === 3) {
            // 跳出 labelCancelLoops 迴圈
            break labelCancelLoops;
        } else if (z === 3) {
            // 跳出當前迴圈
            break;
        }
    }
}
```

result
```
Outer loops: 0
Inner loops: 1
Inner loops: 2
Outer loops: 1
Inner loops: 1
Inner loops: 2
Outer loops: 2
Inner loops: 1
Inner loops: 2
```
搭配continue使用:
```
var i, j;

// 把外層的迴圈標記叫做 loop1

loop1:
for (i = 0; i < 3; i++) {
    // 把內層的迴圈標做 loop2
    loop2:
    for (j = 0; j < 3; j++) {
        if (i === 1 && j === 1) {
            // 跳出 loop1 迴圈
            continue loop1;
        }
        console.log('i = ' + i + ', j = ' + j);
    }
}
```

result
```
i = 0, j = 0
i = 0, j = 1
i = 0, j = 2
i = 1, j = 0
i = 2, j = 0
i = 2, j = 1
i = 2, j = 2
```

### Function (函數)
函數 (function) 用來將會重複使用的程式碼封裝在一起，方便重複執行。

函數宣告:
```
function functionName(parameter1, parameter2, ...) {
    // statements

    // return value;
}
```
宣告一個計算平方的函數，和Java不同，並不用宣告傳入和回傳型別
```
function square(number) {
    return number * number;
}
```
呼叫函數:
宣告一個函數並不會自動的執行它，你要使用函式呼叫的語法，來呼叫並執行一個函數的內容。
```
functionName(parameter1, parameter2, ...);
```
呼叫計算平方函數
```
// 這樣會輸出 100
console.log(square(10));

// 可以將返回值存到一個變數
var squareValue = square(10);

// 函數呼叫的返回值，可以像變數一樣做操作
// 這樣會輸出 1000
console.log(square(10) * 10)
```
#### 變數的存在範圍 (Function scope)
1. 你在函數內定義的任何變數 (local variable)，只有在函數裡面才可以存取到這個變數。
2. 在函數裡面除了可以存取到局部變數 (local variable)，也可以存取到全域變數 (global variable)。

> 在函數內部的變數，有宣告var為局部變數(var num1=2)，沒宣告var則為全域變數(num2=5)。

```
// 全域變數 - global scope
var num1 = 20;
var num2 = 3;
var name = 'Mike';

// 這個函數定義全域空間 - global scope
function multiply() {
    // 函數內部可以存取到全域變數
    return num1 * num2;
}

// 輸出 60
console.log(multiply());

function getScore () {
    // 局部變數 - function scope
    // 作用範圍只在函數內部
    var num1 = 2;
    var num3 = 4;
    
    // 如果沒加 var 宣告變數，這個變數則是一個全域變數
    num2 = 5; // 存取到全域變數 num2
    num4 = 6; // 宣告一個新的全域變數 num4

    // 函數也可以宣告在其他函數內部 (nested function) - function scope
    function add() {
        // 內部函數可以存取到外部函數的局部變數
        return name + ' scored ' + (num1 + num2 + num3);
    }
  
    return add();
}

console.log(getScore()); //  "Mike scored 11"

// 會存取到全域變數 num1，輸出 20
console.log(num1);

// 會存取到全域變數 num2，輸出 5
// 因為全域變數 num2 在函數內部被設成 5
console.log(num2);

//會存取到全域變數 num4，輸出 6
console.log(num4);

// 全域空間存取不到 function 內部的變數
// 會發生錯誤 - Uncaught ReferenceError
console.log(num3);

// 全域空間也存取不到 function 的內部函數
// 會發生錯誤 - Uncaught ReferenceError
console.log(add());
```

#### 函數表達式 (Function expression)

函數在 JavaScript 是一個一級物件 (first-class object)，所以
1.可以將function儲存成變數
2.可以將function當成參數代入另一個function中
3.可以在一個function中回傳另一個function
4.function一樣有屬性
5.function遇到return，就會終止函式執行


這意思就是一個函數可以當作別的函數的參數、函數的返回值、或做為一個變數的值。

所以你也可以用 Function expression 的方式來宣告一個函數，將一個匿名函數 (anonymous function / function literal) 當作值指定給一個變數。

#### 匿名函數
```
var square = function(number) {
    return number * number;
};
```
#### 不支援多載
```
//在同一個作用域下，出現兩個名稱相同的函式，後面的會覆蓋前面的函式

function test(a){
}

function test(a,b){
}


test(23);
test(2,23);
//都是執行第二個函式
```
### try catch finally Error Handling (例外處理)
> 例外處理 (error handling) 是 JavaScript 的一種程式流程控制，你可以在程式執行可能拋出錯誤的地方使用，主動捕捉並處理錯誤，避免整個程式因為發生錯誤而停止執行。

> 把可能出錯的程式碼放在 try 區塊中；然後出錯時的處理程式碼放在 catch 區塊中；而放在 finally 區塊中的程式碼無論如何都會在最後被執行。

```
try {

   // 預期可能會發生錯誤的程式碼

} catch (e) {

   // try 區塊有拋出錯誤時，則執行這裡的程式碼

} finally {

   // finally 區塊的程式碼一定會在最後被執行
   // 你可以省略 finally 區塊

}
```

常見錯誤:
| 錯誤類型 | 說明 |
| -------- | -------- |
|EvalError|eval() 執行錯誤|
|RangeError|一個數值超過允許範圍|
|ReferenceError|存取未宣告的變數|
|SyntaxError|程式語法錯誤|
|TypeError|型別錯誤|
|URIError|URI handling 相關函數例如 decodeURIComponent() 執行時錯誤|

實例:
```
// 因為我們沒有宣告 blah 這函數，呼叫 blah 函數時會發生錯誤
// 上面程式碼依序會跳出視窗 "ReferenceError: blah is not defined"

try {
    blah('Hello world');

} catch(err) {
    alert(err.name + ': ' + err.message);

} finally {
    alert('try catch 區塊結束');
}
```

主動拋出例外錯誤 throw:
可以用 throw 關鍵字在程式中主動拋出錯誤，拋出的例外可以是一個字串 (string)、數字 (number) 或錯誤物件 (error object)。
```
try {
    throw 'myException';
} catch (err) {
    // err 是字串 "myException"
    err;
}

try {
    throw 101;
} catch (err) {
    // err 是數字 101
    err;
}
```
自訂錯誤物件 new Error()：
JavaScript 有一個 Error 物件，所有的例外錯誤都是繼承自 Error 物件，可以客製化一個自己的錯誤物件。
```
try {
    throw new Error('oops');
} catch (err) {
    // 輸出 "Error: oops"
    console.log(err.name + ': ' + err.message);
}
```
instanceof 判斷錯誤類型:
```
try {
    foo.bar();

} catch (err) {

    // 如果錯誤類型是 EvalError
    if (err instanceof EvalError) {
        console.log(err.name + ': ' + err.message);

    // 如果錯誤類型是 RangeError    
    } else if (err instanceof RangeError) {
        console.log(err.name + ': ' + err.message);
    }
    // ...
}
```

### JavaScript 物件(Object)

#### 概述
物件為了封裝資料、重複使用，且方便傳遞而存在。

* 簡單來說，就是一堆(key-value paris) 的組合
* 名稱(key)只能是字串
* 值(value)可以放任何資料型別
基本型別string、number、boolean - 通常稱屬性
參考型別object、array - 通常稱屬性
參考型別 function - 通常稱方法

#### 定義物件 - 建立物件的兩種方式
```
// Object Constructor (物件建構式)
var myObj = new Object();

// Object Literal (物件實字)
var myObj = {};
```

#### 物件的屬性 - 方法1
```
var myObj = {};

// 建立一個叫 color 的屬性，值是 blue
myObj.color = 'blue';

// 存取物件屬性
var myColor = myObj.color;
```

#### 物件的屬性 - 方法2
```
var myObj = {};

// 建立一個叫 color 的屬性，值是 blue
// []內如果是屬性名必須有引號，否則會被當成是變數
myObj['color'] = 'blue';

// 存取物件屬性
var myColor = myObj['color'];
```
```
// 用 [] 特別的地方在於，中括號裡面可以是一個變數
// []內如果是變數名不需要有引號

var myObj = {};
var propName = 'color';

// 建立一個叫 color 的屬性，值是 blue
myObj[propName] = 'blue';

// 都會輸出 blue
console.log(myObj[propName]);
console.log(myObj.color);


// 但如果你用 . 運算子
// 會新增一個叫 propName 的屬性，而不是新增一個叫 color的屬性
myObj.propName = 'blue';
```

#### 宣告物件時，同時建立屬性
```
// 建立一個物件，這物件有兩個屬性 color 和 height
var myObj = {'color': 'blue', 'height': 101};


// object literal 中的屬性名稱的引號可以省略
// 建立一個物件，這物件有兩個屬性 color 和 height
var myObj = {color: 'blue', height: 101};
```

#### 物件方法
```
var me = {
    firstName: 'Mike',
    lastName: 'Lee',
    age: 30,
    fullName: function() {
        return this.firstName + ' ' + this.lastName;
    }
}

// name = 'Mike Lee'
var name = me.fullName();
```



#### 實例
```
// this指的是這一個物件，指屬性或方法在哪個物件下被呼叫，this就是屬於這個呼叫的物件
// 在這邊，this指的是john物件

var 物件名稱 = {
  key1:value1,
  key2:value2
}

var john = {
  name:"John",
  age:23,
  greeting:function(){
    console.log("Hello, I'm "+this.name)    
  }
}

console.log(john.age); //取值
john.age = 100; //設值
console.log(john.age);
john.greeting(); //執行方法
```
#### JS物件可以動態新增與刪除屬性與方法
```
var john = {
  name:"John",
  age:23,
  greeting:function(){
    console.log("Hello, I'm "+this.name);    
  }
}

//新增屬性與方法
john.interests = ["reading","running","travel"];

john.bio = function(){
    console.log("Hi I'm "+this.name + " My age is "+this.age+", and I like "+this.interests[0]+" and " + this.interests[1]);
}

john.bio();


//刪除屬性
delete john.age;
```
#### 物件轉字串/字串轉物件
```
//物件轉字串
JSON.stringify(物件變數)

var str = JSON.stringify(john)

str = {"name":"John","age":23,"interests":["reading","running","travel"]}


//字串轉物件
JSON.parse(字串)

var john = JSON.parse(str)
```
#### 變數-傳值
```
//基本型別都是以傳值方式進行變數的傳遞
//a 和 b 是存在於兩個獨立不同的記憶體位置中

var a = 3;
var b = a;
a = 2;

console.log(a); //2
console.log(b); //3
```
#### 變數-傳址
```
//參考型別都是以傳址方式進行變數的傳遞
//c、d指向同一個記憶體位置，所以不管值怎麼變化，c和d拿到的值會相同

var c = {greeting : "Hello"};
var d = c;
c.greeting = "Hola";

console.log(c); //{greeting : "Hola"}
console.log(d); //{greeting : "Hola"}
```
#### 補充-淺拷貝與深拷貝
```
//淺拷貝 (因相同記憶體位置，故更改後會拿到相同的值)
var obj1 = { a: 10, b: 20, c: 30 }; 
var obj2 = obj1; 
obj2.b = 100; 

console.log(obj1); // { a: 10, b: 100, c: 30 }
console.log(obj2); // { a: 10, b: 100, c: 30 } 


//深拷貝 (各自獨立)
var obj1 = { a: 10, b: 20, c: 30 }; 
var obj2 = Object.assign({}, obj1); 
obj2.b = 100; 

console.log(obj1); // { a: 10, b: 20, c: 30 }
console.log(obj2); // { a: 10, b: 100, c: 30 }
```
#### 數值(Number)物件-常用方法
```
Number() //字串轉數字
Number('3.14') // 3.14
Number('100')  // 100
Number('a123') // NaN

Number() //布林值轉數字
Number(false) // 0
Number(true)  // 1


parseInt() / Number.parseInt() //字串轉整數，兩者是一樣的函式
parseInt('10');       // 10
parseInt('10.6');     // 10

var x = Number('3.14');
var y = parseInt('3.14');
var z = Number.parseInt('3.14');

console.log(x); //3.14
console.log(y); //3
console.log(z); //3

console.log(typeof x); //number
console.log(typeof y); //number
console.log(typeof z); //number


var num = 123456.22324;

xxx.toString(); //數字轉字串，並回傳


//取到小數點第x位，並回傳成字串
toFixed(x);

num.toFixed(3) //123456.223


xxx.valueOf() //將Number物件轉型成基本數值型態
[與Java的Integer.valueOf(int i)不同，Java為轉型成參考型別Integer]

var numObj = new Number(10);
console.log(typeof numObj); // object

var num = numObj.valueOf();
console.log(num);           // 10
console.log(typeof num);    // number
```
#### 布林值(Boolean)物件
在 JavaScript 中，只有這些值會被當作是 false，除此以外的值都是 true！
* null
* 數值 0
* NaN
* 空字串 ''
* undefined
```
var x = 0;
Boolean(x); // false

x = 100;
Boolean(x); // true

x = '';
Boolean(x); // false

x = 'hi';
Boolean(x); // true

x = null;
Boolean(x); // false
```
#### Math物件-常用方法 [全部與Java寫法相同]
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
#### 字串物件(String)-特殊字元
> 因為字串必須包在單引號或雙引號裡面，但是要特別注意的雙引號裡面不能有雙引號、單引號裡面不能有單引號。
```
// 下面這些都會發生錯誤：
var str = 'Mike's pet.';
var str = "This is a "book".";


// 你可以改成這樣就會正確，因為雙引號裡面可以有單引號，或單引號裡面可以有雙引號：
var str = "Mike's pet.";
var str = 'This is a "book".';


// 或是使用跳脫字元 (escape character) 反斜線 (backslash) \，來跳脫引號：
var str = 'Mike\'s pet.';   // Mike's pet.

var str = "This is a \"book\".";   // This is a "book".


+ //字串相加
var str = 'hel' + 'lo';
console.log(str);   // 輸出 'hello'


var name = 'Mike';
var str2 = str + ' ' + name;
console.log(str2);   // 輸出 'hello Mike'


// str2 += '!' 意思同 str2 = str2 + '!'
str2 += '!';
console.log(str2);   // 輸出 'hello Mike!'


concat() //字串相加
var hello = 'Hello, ';
console.log(hello.concat('Mike', ' have a nice day.')); //輸出 'Hello, Mike have a nice day.'

var hello = 'Hello, ';
console.log(hello + 'Mike' + ' have a nice day.'); // 輸出 'Hello, Mike have a nice day.'
```
#### 字串物件(String)-型別轉換 & 比較
```
String() //數字轉字串
String(123) // '123'
String(100 + 23) // '123'

String() //布林值轉字串
String(true) // 'true'
String(false) // 'false'


//可以用 === 或 == 運算子來判斷兩個字串是否相等
var str = 'hello world';

if (str === 'hello world') {
    console.log('eqaul');
}   // 會輸出 'equal'


var str = 'hello world';

if (str !== 'hello Mars') {
    console.log('not eqaul');
}   // 會輸出 'not equal'

```

#### 字串物件(String)-常用方法 [全部與Java寫法相同]
```
str.length //返回字串長度

str.charAt(n) //返回索引值n的字元，不存在則返回空字串

str.indexOf(字串s,開始索引值n) //返回字串首次出現位置，從索引值n開始查詢，不存在則回傳-1
str.lastIndexOf(字串s,開始索引值n) //返回字串最後出現位置，從索引值n開始查詢，不存在則回傳-1

str.substring(索引值n,索引值m) //返回從索引值n到(m-1)之間的字元，m可省略表示擷取到最後

str.substr(索引值n，取幾個) //返回從索引值n開始，取幾個字元

str.replace(字串r,字串s) //將原字串中的r替換成s，只替換第一個遇到的字串，與Java不同
str.replace(/字串r(無引號)/g,字串s) //將原字串中的r全部替換成s

str.split(字串s) //以字串s切割原字串，並返回n個子字串的陣列(分割)

str.trim() //返回一個去除開頭與結尾的所有空白字元字串

str.toUpperCase() //將字串轉大寫
str.toLowerCase() //將字串轉小寫
```
```
var str = "I love javascript love me";

str.length //25

str.charAt(3) //o

str.indexOf("o") //3

str.lastIndexOf("o") //19

str.indexOf("ava") //8

str.substring(2,5) //lov

str.substr(2,3) //lov

str.replace(/l/g,"L") //I Love javascript Love me
str.replace(/love/g,"LOVE") //I LOVE javascript LOVE me


var arr = str.split(" ");
for(i=0;i<arr.length;i++){
	console.log(arr[i]);
}
//I
//love
//javascript
//love
//me
```
#### 日期物件(Date)-常用方法
```
var now = new Date(); //建立日期物件為今天的日期[語法同Java]

var day1 = new Date(2020,4,21); //建立日期物件("西元年,月-1,日") //May 21 2020
var day2 = new Date(2020,4,21,12,10,30); //建立日期物件("西元年,月-1,日,時,分,秒")

now.getTime(); //回傳至1970/01/01至今的毫秒數[語法同Java]
now.getFullYear(); //回傳完整的西元年，如2004
now.getYear(); //若介於1900~1999年間，回傳後兩碼西元年，否則回傳與1900的差距
now.getMonth(); //回傳月份(0~11)，須自己+1
now.getDay(); //回傳星期幾(0~6)
now.getDate(); //回傳日期(1~31)
now.getHours(); //回傳小時(0~23)
now.getMinutes(); //回傳分(0~59)
now.getSeconds(); //回傳秒(0~59)
now.getMilliseconds(); //回傳毫秒(0-999)

now.setTime();
now.setFullYear();
依此類推
```
#### 陣列宣告
```
//JS陣列的內容可以放任何資料型別，包括基本型別及參考型別，同Java陣列。
//JS陣列的長度在宣告時，或者宣告後都可以動態配置。不同於Java陣列一開始一定要宣告長度，且不可改變。
//[] 與 new Array()一樣都是宣告一個新陣列


Type1:
var students = [];
students[0] = "Mark";
students[1] = "Tom";

Type2:
var students = ["Mark","Tom"];


Type3:
var students = new Array();
students[0] = "Mark";
students[1] = "Tom";

Type4:
var students = new Array("Mark","Tom");


宣告長度:
var students = [3];
var students = new Array(3);

```
#### 陣列常用屬性與方法
```
var a =["Mark","Zuck","Pony","Elon"];

a.length //陣列長度

a.push("Mary") //新增最後一個元素
a.pop() //移除最後一個元素，並返回移除的元素值

a.unshift("Mary") //新增第一個元素
a.shift() //移除第一個元素，並返回移除的元素值

a.slice(n,m) //任意截取出陣列的一部分，從索引值n到索引值m-1(切片)

a.splice(起始index,刪除個數) //移除從index開始算起，共幾個元素，並返回移除的元素值(接合)

a.reverse() //反轉陣列

a.sort() //陣列按Unicode code point由小到大排序

a.indexOf("Mark") //找出第一個該元素的索引值，若找不到則回傳-1
a.lastIndexOf("Mark") //找出最後一個該元素的索引值，若找不到則回傳-1

a.join("@@") //將陣列中所有元素，藉由指定字符合併在一起變成字串

a.concat(ary1,ary2,...); //多個陣列相加

forEach() //遍歷陣列中的每一個元素
```
```
push():

var fruits = ['Apple', 'Banana'];

fruits.push('Orange');

console.log(fruits); //輸出 ["Apple", "Banana", "Orange"]



pop():

var fruits = ['Apple', 'Banana'];

var last = fruits.pop(); //Banana

console.log(fruits); //輸出 ["Apple"]



slice():

var fruits = ['Banana', 'Orange', 'Lemon', 'Apple', 'Mango'];

var foo1 = fruits.slice(1, 3);

console.log(foo1); //輸出 ["Orange", "Lemon"]



splice():刪除元素

var fruits = ['Banana', 'Orange', 'Apple', 'Mango', 'Peach'];
var removed = fruits.splice(2, 2);

console.log(fruits); //輸出 ["Banana", "Orange", "Peach"]

console.log(removed); //輸出 ["Apple", "Mango"]



splice():刪除並新增元素

var fruits = ['Banana', 'Orange', 'Apple', 'Mango', 'Peach'];
var removed = fruits.splice(2, 2, 'Watermelon', 'Lemon');

console.log(fruits); //輸出 ["Banana", "Orange", "Watermelon", "Lemon", "Peach"]

console.log(removed); //輸出 ["Apple", "Mango"]



splice():新增元素

var fruits = ['Banana', 'Orange', 'Apple', 'Mango', 'Peach'];
var removed = fruits.splice(1, 0, 'Watermelon', 'Lemon');

console.log(fruits); //輸出 ["Banana", "Watermelon", "Lemon", "Orange", "Apple", "Mango", "Peach"]


console.log(removed); //輸出 []



sort():

var scores = [1, 10, 21, 2]; 

scores.sort(); //返回 [1, 10, 2, 21]
               //注意 10 會排在 2 前面
               //因為字串 '10' 的第一個字元 '1' 比 '2' 的 Unicode code point 小


var things = ['word', 'Word', '1 Word', '2 Words'];

things.sort(); //返回 ["1 Word", "2 Words", "Word", "word"]
               //因為數字的 Unicode code point 比英文字小



sort():搭配reverse()

var fruits = ['cherries', 'apples', 'bananas'];

fruits.sort();
fruits.reverse();

console.log(fruits); //輸出 ["cherries", "bananas", "apples"]



concat:

var num1 = [1, 2, 3];
var num2 = [4, 5, 6];
var num3 = [7, 8, 9];

var nums = num1.concat(num2, num3);

console.log(nums); //輸出 [1, 2, 3, 4, 5, 6, 7, 8, 9]



forEach():

//currentValue 代表目前處理到的元素的值
//index 代表目前處理到的元素的索引位置
//array 代表陣列本身

function logArrayElements(currentValue, index, array) {
    console.log('ary[' + index + '] = ' + currentValue);
}

['a', 'b', 'c'].forEach(logArrayElements);

//ary[0] = a
//ary[1] = b
//ary[2] = c
```

#### JSON(JavaScript Object Notation)

> JSON 和 JavaScript 是沒有直接關聯的，JSON 是一套獨立於語言 (language agnostic) 的資料交換格式，現在幾乎所有的主流程式語言都支援 JSON。

是一種常見的資料交換格式，使用大括號定義成對的鍵和值

1. 資料是成對的鍵和值，使用 : 符號分隔。
2. 資料之間使用 , 符號分隔。
3. 使用大括號定義物件。
4. 使用方框號定義物件陣列。
````
{
   "key1":"value1",
   "key2":"value2",
   "key3":"value3",
}
````
物件陣列
````
[
   {
   "title":"ASP網頁設計",
   "author":"陳會安",
   "category":"Web"  
   }
   {
   "title":"PHP網頁設計",
   "author":"陳雷",
   "category":"Web"  
   }
]
````
````
{
   "Boss":"陳會安"
   "Employee":[
     {"name":"陳允傑","tel","02-22222222"},
     {"name":"陳小東","tel","02-33333333"},
     {"name":"陳小春","tel","02-11111111"},   
   ]
}

//JSON物件陣列可以擁有多個JSON物件，比如Employee是一個物件陣列，擁有3個JSON物件。
````
JavaScript 內建提供 JSON.parse() 和 JSON.stringify() 兩個函數來操作 JSON。
```
JSON.parse(text) //用來將 JSON 字串轉換成 JavaScript 物件。


JSON.parse('{}'); //{}

JSON.parse('true'); //true

JSON.parse('"foo"'); //"foo"

JSON.parse('[1, 5, "false"]'); //[1, 5, "false"]

JSON.parse('null'); //null
```
```
JSON.stringify(value) //用來將 JavaScript 物件轉換成 JSON 字串。


JSON.stringify({}); //'{}'

JSON.stringify(true); //'true'

JSON.stringify('foo'); //'"foo"'

JSON.stringify([1, 'false', false]); //'[1,"false",false]'

JSON.stringify({x: 5}); //'{"x":5}'
```

### 瀏覽器物件模型 (BOM - Browser Object Model)
瀏覽器物件模型 (BOM, Browser Object Model) 是瀏覽器提供的物件，讓你可以透過 JavaScript 直接跟瀏覽器溝通或做操作。


共有以下幾種常用物件:
* window: 讓你可以存取操作瀏覽器視窗
* screen: 讓你可以存取使用者的螢幕畫面資訊
* location: 讓你可以存取操作頁面的網址 (URL)
* history: 讓你可以操作瀏覽器的上一頁、下一頁
* navigator: 讓你可以存取瀏覽器資訊
* Popup: 讓你可以使用瀏覽器內建的彈跳視窗
* Timer: 讓你可以使用瀏覽器內建的計時器
* cookie: 讓你可以管理瀏覽器的 cookie


#### window
```
1. 取得瀏覽器視窗的寬高，單位是 px (pixels)

window.innerWidth //視窗的可見寬度(不包含工具列、捲軸等)

window.innerHeight //視窗的可見高度(不包含工具列、捲軸等)


window.outerWidth //整個視窗的寬度(包含工具列、捲軸等)

window.outerHeight //整個視窗的高度(包含工具列、捲軸等)
```

```
2. 瀏覽器開啟新視窗 window.open() 

window.open('http://www.fooish.com/');
var windowObjectReference = window.open(
    'http://www.fooish.com/',
    'fooish',
    'width=800,height=600,resizable=no,scrollbars=yes,status=no,location=no'
);
```
```
3. 關閉瀏覽器視窗 window.close()

//開啟視窗
var win = window.open('http://www.fooish.com/');

//關閉視窗
win.close();

註:僅限於window.open() 開啟的視窗 
```
```
4. 移動瀏覽器視窗 window.moveTo(), window.moveBy()

//window.moveTo(x, y) 參數 x, y 的單位是 px，分別表示移動視窗位置至距離螢幕左緣和上緣多少的距離。

var win = window.open('http://www.fooish.com/', '', 'width=200,height=100');

win.moveTo(100, 100);


//window.moveBy(deltaX, deltaY) 以視窗目前的位置為基準，分別要往左和往下移動多少距離 px。

var win = window.open('http://www.fooish.com/', '', 'width=200,height=100');

win.moveBy(200, 200);
```
```
5. 改變瀏覽器視窗的大小 window.resizeTo()

var win = window.open('http://www.fooish.com/');

window.resizeTo(800, 600);


註:僅限於window.open() 開啟的視窗 
```
#### screen
```
1. 取得使用者螢幕的寬高大小

var screenWidth = screen.width;

var screenHeight = screen.height;


2. 取得使用者瀏覽器可以使用的寬高大小

var screenAvailWidth = screen.availWidth;

var screenAvailHeight = screen.availHeight;


3. 取得使用者螢幕的色彩深度/位數
screen.colorDepth;


4. 取得使用者螢幕的像素深度/位數
screen.pixelDepth;
```
#### location
```
1. 取得當前網頁的網址
location.href;


2. 取得當前網頁的網域名稱
location.hostname;


3. 取得當前網頁的網址路徑
location.pathname;


4. 取得當前網頁的網址參數
location.search;


5. 改變當前網頁的網址

location.href = '/jquery/'; //切到同一個網站，不同的路徑

location.href = 'https://www.google.com/'; //切換到另一個網站


6. 在當前視窗載入一個新的網頁
location.assign('http://www.fooish.com/');


7. 重新整理網頁
location.reload(true);


8. 當前視窗載入一個新的網頁，當前網頁的瀏覽紀錄會被新的網頁取代掉
location.replace(url);
```
#### history
```
1. 取得使用者在當前視窗下，總共瀏覽了幾個網頁
history.length 


2. 使瀏覽器回到上一頁
history.back();


3. 使瀏覽器回到下一頁
history.forward();


4. 明確指定瀏覽器要回去幾頁
history.go()
```
#### Popup
```
1. 用來跳出提示 (警告) 對話視窗 alert()
alert(message);


2. 用來跳出需要使用者確認的對話視窗，對話視窗中會有確定及取消兩個按鈕 confirm()

//confirm() 執行後會返回一個布林值 (boolean)，用來表示使用者按了確定 (true) 或是取消 (false)。

var yes = confirm('你確定嗎？');

if (yes) {
    alert('你按了確定按鈕');
} else {
    alert('你按了取消按鈕');
}


3. 用來跳出一個文字輸入的對話視窗 prompt()

var nickname = prompt('請輸入你的暱稱');

alert('Hello ' + nickname);
```

#### Timer















### 文件物件模型DOM
* Document Object Model
* 