# MS SQL + Stored Procedure

### CRUD
```
#INSERT INTO DEPT2(DEPTNO,LOC) VALUES(70,'基隆車站'); //有三個欄位，不用全部新增

SELECT DEPTNO,LOC FROM DEPT2;

UPDATE DEPT2 SET LOC='基隆廟口' WHERE DEPTNO=70;

#DELETE FROM DEPT2 WHERE DEPTNO=70;

```

### 新增Table
````
USE 教務系統 
GO
CREATE TABLE 員工 (
   身份證字號 char(10)   NOT NULL PRIMARY KEY,
   姓名       varchar(12) NOT NULL,
   城市       varchar(5)  DEFAULT '台北',
   街道       varchar(30),
   電話       char(12),
   薪水       money,
   保險       money,
   扣稅       money
)
//使用USE切換使用的資料庫，GO代表批次的結束(相當於Commit)
````
````
USE 教務系統 
GO
CREATE TABLE 教授 (
   建檔編號    int         IDENTITY(1000, 1), 
   教授編號    char(4)     NOT NULL PRIMARY KEY,
   職稱        varchar(10),
   科系        varchar(5),
   身份證字號   char(10)   NOT NULL
)
//IDENTITY為自動編號欄位，起始值1000，遞增值1
````
````
USE 教務系統 
GO
CREATE TABLE 班級 (
   教授編號   char(4)  NOT NULL, 
   課程編號   char(5)  NOT NULL,
   學號       char(4)  NOT NULL
              REFERENCES 學生 (學號),
   上課時間   datetime,
   教室       varchar(8), 
   PRIMARY KEY (學號, 教授編號, 課程編號),
   FOREIGN KEY (教授編號) REFERENCES 教授 (教授編號),
   FOREIGN KEY (課程編號) REFERENCES 課程 (課程編號)
)
//主鍵及外來鍵設定
````
````
USE master 
GO
IF  EXISTS (SELECT name FROM sys.databases WHERE name='教務系統')
DROP DATABASE [教務系統]
GO

CREATE DATABASE [教務系統]
GO

USE [教務系統]
GO

CREATE TABLE [學生] (
	[學號] char(4) NOT NULL,
	[姓名] varchar(12) NOT NULL,
	[性別] char(2) NULL,
	[電話] varchar(15) NULL,
	[生日] datetime NULL,
  PRIMARY KEY ([學號])
) 
GO

CREATE TABLE [課程] (
	[課程編號] char(5) NOT NULL,
	[名稱] varchar(30) NULL,
	[學分] int NULL,
  PRIMARY KEY ([課程編號])
) 
GO

CREATE TABLE [教授] (
	[教授編號] char(4) NOT NULL,
	[職稱] varchar(10) NULL,
	[科系] varchar(5) NULL,
	[身份證字號] char(10) NOT NULL,
  PRIMARY KEY ([教授編號])
) 
GO

CREATE TABLE [班級] (
	[教授編號] char(4) NOT NULL,
	[學號] char(4) NOT NULL,
	[課程編號] char(5) NOT NULL,	
	[上課時間] datetime NULL,
	[教室] varchar(8) NULL,
  PRIMARY KEY ([教授編號],[課程編號],[學號])
) 
GO

CREATE TABLE [員工] (
	[身份證字號] CHAR(10) NOT NULL,
	[姓名] varchar(12) NULL,
	[城市] char(5) NULL,
	[街道] varchar(30) NULL,
	[電話] char(12) NULL,
	[薪水] money NULL,
	[保險] money NULL,
	[扣稅] money NULL,
  PRIMARY KEY ([身份證字號])
) 
GO

ALTER TABLE [班級]
  ADD FOREIGN KEY([學號]) REFERENCES [學生] ([學號])
GO
ALTER TABLE [班級] 
  ADD FOREIGN KEY([課程編號]) REFERENCES [課程] ([課程編號])  
GO
ALTER TABLE [班級] 
  ADD FOREIGN KEY([教授編號]) REFERENCES [教授] ([教授編號])   
GO
ALTER TABLE [教授] 
  ADD FOREIGN KEY([身份證字號]) REFERENCES [員工] ([身份證字號])   
GO

INSERT INTO [學生] 
VALUES ('S001','陳會安','男','02-22222222','1997/09/03')
GO
INSERT INTO [學生] 
VALUES ('S002','江小魚','女','03-33333333','1998/02/02')
GO
INSERT INTO [學生] 
VALUES ('S003','張無忌','男','04-44444444','1996/05/03')
GO
INSERT INTO [學生] 
VALUES ('S004','陳小安','男','05-55555555','1996/06/13')
GO
INSERT INTO [學生] 
VALUES ('S005','孫燕之','女','06-66666666',NULL)
GO
INSERT INTO [學生] 
VALUES ('S006','周杰輪','男','02-33333333','1995/12/23')
GO
INSERT INTO [學生] 
VALUES ('S007','蔡一零','女','03-66666666','1995/11/23')
GO
INSERT INTO [學生] 
VALUES ('S008','劉得華','男','02-11111122','1995/02/23')
GO

INSERT INTO [課程] 
VALUES ('CS101','計算檮概論',4)
GO
INSERT INTO [課程] 
VALUES ('CS121','離散數學',4)
GO
INSERT INTO [課程] 
VALUES ('CS111','線性代數',4)
GO
INSERT INTO [課程] 
VALUES ('CS203','程式語言',3)
GO
INSERT INTO [課程] 
VALUES ('CS213','物件導向程式設計',2)
GO
INSERT INTO [課程] 
VALUES ('CS222','資料庫管理系統',3)
GO
INSERT INTO [課程] 
VALUES ('CS205','網頁程式設計',3)
GO
INSERT INTO [課程] 
VALUES ('CS349','物件導向分析',3)
GO

INSERT INTO [員工] 
VALUES ('A123456789','陳慶新','台北','信義路',
        '02-11111111', 80000, 5000, 2000)
GO
INSERT INTO [員工] 
VALUES ('A222222222','楊金欉','桃園','中正路',
        '03-11111111', 80000, 4500, 2000)
GO
INSERT INTO [員工] 
VALUES ('H098765432','李鴻章','基隆','信四路',
        '02-33111111', 60000, 4000, 1500)
GO
INSERT INTO [員工] 
VALUES ('F213456780','陳小安','新北','新店區四維路',
        NULL, 50000, 3000, 1000)
GO
INSERT INTO [員工] 
VALUES ('A221304680','郭富城','台北','忠孝東路',
        '02-55555555', 35000, 1000, 800)
GO
INSERT INTO [員工] 
VALUES ('F332213046','張無忌','台北','仁愛路',
        '02-55555555', 50000, 1500, 1000)
GO
INSERT INTO [員工] 
VALUES ('D333300333','王心零','桃園','經國路',
        NULL, 50000, 2500, 1000)
GO
INSERT INTO [員工] 
VALUES ('D444403333','劉得華','新北','板橋區文心路',
        '04-55555555', 25000, 500, 500)
GO
INSERT INTO [員工] 
VALUES ('E444006666','小龍女','新北','板橋區中正路',
        '04-55555555', 25000, 500, 500)
GO

INSERT INTO [教授] 
VALUES ('I001','教授',  'CS', 'A123456789')
GO
INSERT INTO [教授] 
VALUES ('I002','教授',  'CS', 'A222222222')
GO
INSERT INTO [教授] 
VALUES ('I003','副教授','CIS','H098765432')
GO
INSERT INTO [教授] 
VALUES ('I004','講師','MATH', 'F213456780')
GO

INSERT INTO [班級] 
VALUES ('I001','S001','CS101','12:00:00','180-M')
GO
INSERT INTO [班級] 
VALUES ('I001','S005','CS101','12:00:00','180-M')
GO
INSERT INTO [班級] 
VALUES ('I001','S006','CS101','12:00:00','180-M')
GO
INSERT INTO [班級] 
VALUES ('I002','S003','CS121','08:00:00','221-S')
GO
INSERT INTO [班級] 
VALUES ('I002','S008','CS121','08:00:00','221-S')
GO

INSERT INTO [班級] 
VALUES ('I004','S003','CS111','15:00:00','321-M')
GO
INSERT INTO [班級] 
VALUES ('I004','S002','CS111','15:00:00','321-M')
GO
INSERT INTO [班級] 
VALUES ('I004','S005','CS111','15:00:00','321-M')
GO
INSERT INTO [班級] 
VALUES ('I001','S003','CS213','09:00:00','622-G')
GO
INSERT INTO [班級] 
VALUES ('I001','S005','CS213','09:00:00','622-G')
GO
INSERT INTO [班級] 
VALUES ('I003','S001','CS213','12:00:00','500-K')
GO
INSERT INTO [班級] 
VALUES ('I003','S006','CS213','12:00:00','500-K')
GO
INSERT INTO [班級] 
VALUES ('I002','S001','CS222','13:00:00','100-M')
GO
INSERT INTO [班級] 
VALUES ('I002','S002','CS222','13:00:00','100-M')
GO
INSERT INTO [班級] 
VALUES ('I002','S004','CS222','13:00:00','100-M')
GO
INSERT INTO [班級] 
VALUES ('I003','S001','CS203','10:00:00','221-S')
GO
INSERT INTO [班級] 
VALUES ('I003','S006','CS203','10:00:00','221-S')
GO
INSERT INTO [班級] 
VALUES ('I003','S008','CS203','10:00:00','221-S')
GO
INSERT INTO [班級] 
VALUES ('I003','S002','CS203','14:00:00','327-S')
GO
INSERT INTO [班級] 
VALUES ('I001','S001','CS349','15:00:00','380-L')
GO
INSERT INTO [班級] 
VALUES ('I001','S003','CS349','15:00:00','380-L')
GO
````
````
USE 教務系統 
GO
CREATE TABLE TEST (
   ID char(10)            NOT NULL,
   NAME       varchar(12) NOT NULL,
)
GO


INSERT INTO TEST(ID,NAME) VALUES(10,'JACK');

INSERT INTO TEST　VALUES(20,'TOM');

//兩種皆可新增完成
````



### Transact-SQL(T-SQL)
ASNI-SQL結構化查詢語言可程式化的擴充版本
> 因為ANSI-SQL指令主要是針對查詢和維護資料庫的資料，缺乏基本程式設計能力，也無法宣告變數或建立流程控制。
> 
> T-SQL則增加了變數宣告、流程控制、錯誤處理等等。
<br>

#### T-SQL資料庫物件完整名稱
````
伺服器名稱.資料庫名稱.結構描述名稱.物件名稱
JEFF-PC.教務系統.dbo.員工
//dbo為預設結構描述名稱
````

#### 宣告變數與變數初值
````
DECLARE @balance int
DECLARE @total int = 100
PRINT @balance
PRINT @total
//可選擇指定或不指定初始值，無指定初始值預設為null
````

#### 指定變數值
在批次宣告T-SQL變數後，可以使用SET指令指定變數值
````
DECLARE @balance int
SET @balance = 1000
SET @balance = @balance * 1.02
PRINT '總額:' + CAST(@balance AS char)
````
使用SELECT指定變數值
````
DECLARE @myName varchar(12)
SELECT @myName = '陳會安'
SELECT @myName AS 姓名   //表格title
````
````
DECLARE @myName varchar(12)
DECLARE @myCity varchar(10)
SELECT @myName = 姓名, @myCity = 城市   //實際資料表title
FROM 員工 WHERE 薪水 >= 60000
SELECT @myName AS 姓名1, @myCity AS 城市1   //查詢顯示表格title
````
````
DECLARE @c_no varchar(5)
SELECT @c_no = 'CS101' 
SELECT 課程編號, 名稱, 學分 
FROM 課程
WHERE 課程編號 = @c_no
````
#### 變數值種類
* 純量變數 : 一種儲存標準資料類型的單一值。
* 資料表變數 : 一種儲存整個資料表內容的變數，可以在資料表變數使用SELECT、INSERT、DELETE、UPDATE指令，將它視為標準資料表來使用。

````
DECLARE @students table   //@students為資料表變數
( std_no  char(4), name  varchar(12) )
INSERT @students

SELECT 學號, 姓名 FROM 學生 
WHERE 性別 = '男'

SELECT * FROM @students
````
#### SQL Server的系統函數
為一全域變數，可以傳回SQL Server系統資訊的值。

1. @@IDENTIFY:傳回伺服器最後產生IDENTITY欄位自動編號的值，如無產生則傳回null。
2. @@ROWCOUNT:傳回最近T-SQL指令敘述所影響的紀錄數。
3. @@ERROR:傳回最近執行T-SQL指令所產生的錯誤編號，如無錯誤則傳回0。
4. @@SERVERNAME:傳回伺服器名稱。
````
DECLARE @MyRowCount int, @MyIdentity int
INSERT 課程備份2
SELECT 課程編號, 名稱, 學分 FROM 課程 
WHERE 學分 >= 4
SET @MyRowCount = @@ROWCOUNT
SET @MyIdentity = @@IDENTITY
SELECT @MyRowCount AS 影響的記錄數, 
       @@SERVERNAME AS 伺服器名稱,
       @MyIdentity AS 自動編號,
       @@ERROR AS 錯誤編號
````
#### 類型轉換運算子
* CAST運算子(ANSI-SQL)
````
DECLARE @total int

PRINT '學分總數:' + CAST(@total AS char)
PRINT CAST('2016-06-30' AS datetime)
````
* CONVERT()函數(T-SQL)
````
PRINT '學分總數:' + CONVERT(char,@total)
PRINT CONVERT(datetime,'2016-06-30')
````
### 流程控制

#### BEGIN/END指令區塊
可以將多個T-SQL指令群組成一個邏輯區塊，通常是搭配流程控制指令來使用。

當流程控制指令需要執行兩個或以上的T-SQL指令時，就必須使用BEGIN/END指令將它們括起來。

有點類似{......}
````
DECLARE @dbName varchar(10) = '教務系統'
IF @dbName = '教務系統'
BEGIN
   PRINT '資料庫: 教務系統'
   PRINT '資料表: 教授, 課程'
END
//IF條件如果成立，則執行BEGIN/END區塊
````
````
DECLARE @height int
SET @height = 125
IF @height <= 120 
   PRINT '半票'
IF @height > 120 
BEGIN
   PRINT '全票'
   PRINT 'height > 120'
END
````
````
IF (SELECT COUNT(*) FROM 教授) >= 1
   PRINT '教授資料表有存在記錄!'
ELSE
   PRINT '教授資料表沒有記錄!'
````
#### 資料庫檢查DB_ID & OBJECT_ID
* DB_ID(資料庫名稱) : 檢查參數的資料庫名稱是否存在，不存在則傳回null
* OBJECT_ID(物件名稱) : 檢查參數的資料表、檢視表、預存程序、自訂函數、觸發程序的物件是否存在，不存在則傳回null
````
IF DB_ID('教務系統') IS NOT NULL
   PRINT '找到教務系統資料庫!'
ELSE
   PRINT '教務系統資料庫找不到!'
USE 教務系統
IF OBJECT_ID('課程') IS NOT NULL
   PRINT '找到課程資料表!'
ELSE
   PRINT '找不到課程資料表!'
````
#### RETURN中斷查詢指令
可以中斷批次或預存程序的執行，在RETURN之後的T-SQL指令敘述都不會執行。
````
DECLARE @total int
SET @total = (SELECT COUNT(*) FROM 課程)
IF (SELECT COUNT(*) FROM 學生) >= 1
BEGIN
   PRINT '學生資料表有記錄資料!'
   RETURN
END
ELSE
   PRINT '學生資料表沒有記錄資料!'
PRINT '課程數:' + CAST(@total AS char)
//不會顯示最後的課程數
````
#### CASE多條件函數
* 簡單CASE函數(CASE後需加輸入運算式)
````
SELECT 學號, 姓名, 

   CASE 性別         //原先資料表欄位title
      WHEN '男' THEN 'Male'   //改為顯示Male
      WHEN '女' THEN 'Female'
      ELSE 'N/A'
   END AS 學生性別   //顯示於查詢結果欄位title
   
FROM 學生
````
| 學號 | 姓名 | 學生性別 |
| -------- | -------- | -------- |
| S001     | 陳會安     | Male     |
| S002     | 江小魚     | Female     |

* 搜尋CASE函數(CASE後不需加輸入運算式)
````
DECLARE @type varchar(12), @age int
SET @age = 25
SET @type = 

   CASE 
      WHEN @age < 15 THEN '小孩'
      WHEN @age < 60 THEN '成人'
      WHEN @age < 100 THEN '老人'
      ELSE 'Free'
   END
   
PRINT @type
````
#### WHILE迴圈控制

基礎迴圈
````
DECLARE @COUNT INT,@TOTAL INT;
SET @COUNT=1
SET @TOTAL=0
WHILE @COUNT<=5
BEGIN
SET @TOTAL = @TOTAL+@COUNT
PRINT '計數'+CONVERT(VARCHAR,@COUNT)
SET @COUNT = @COUNT+1
END
PRINT '1加到5 = '+CAST(@TOTAL AS VARCHAR)
````
````
計數1
計數2
計數3
計數4
計數5
1加到5 = 15
````
巢狀迴圈
````
USE 教務系統 
GO
DECLARE @book_Id int, @category_Id int
CREATE TABLE TextBooks (book_Id int, category_Id int)
SET @book_Id = 0
SET @category_Id = 0 

WHILE @book_Id < 2
BEGIN
   SET @book_Id = @book_Id + 1

   WHILE @category_Id < 3
   BEGIN 
      SET @category_Id = @category_Id + 1
      INSERT INTO TextBooks 
      VALUES(@book_Id, @category_Id)
   END

   SET @category_Id = 0 
END

SELECT * FROM TextBooks
DROP TABLE TextBooks
````

| book_Id | category_Id | 
| -------- | -------- |
| 1     | 1     | 
| 1     | 2     | 
| 1     | 3     | 
| 2     | 1     | 
| 2     | 2     | 
| 2     | 3     | 

BREAK關鍵字跳出迴圈
````
DECLARE @counter int, @total int
SET @total = 0
SET @counter = 1
WHILE @counter <= 15
BEGIN
   SET @total = @total + @counter
   PRINT '計數: ' + CAST(@counter AS char)
   SET @counter = @counter + 1
   IF @counter > 5 BREAK
END
PRINT '1 加到 5 = ' + CAST(@total AS char)
````
````
計數:1
計數:2
計數:3
計數:4
計數:5
1加到5 = 15
````
CONTINUE關鍵字繼續迴圈(PASS自己這次，進行下次迴圈)
````
DECLARE @counter int, @total int
SET @total = 0
SET @counter = 0
WHILE @counter < 10
BEGIN
   SET @counter = @counter + 1
   IF @counter % 2 = 0 CONTINUE
   SET @total = @total + @counter
END
PRINT '總和: ' + CAST(@total AS char)

//總和: 25 
````
GOTO關鍵字跳出迴圈
````
DECLARE @book_Id int, @category_Id int
CREATE TABLE TextBooks (book_Id int, category_Id int)
SET @book_Id = 0
SET @category_Id = 0 
WHILE @book_Id < 2
BEGIN
   SET @book_Id = @book_Id + 1
   WHILE @category_Id < 3
   BEGIN 
      SET @category_Id = @category_Id + 1
      IF @book_id = 1 AND @category_id = 3
          GOTO BREAK_POINT
      INSERT INTO TextBooks 
      VALUES(@book_Id, @category_Id)
   END
   SET @category_Id = 0 
END
BREAK_POINT:
SELECT * FROM TextBooks
DROP TABLE TextBooks
````
#### IIF函數(類似三元運算子)
````
DECLARE @math int = 65
DECLARE @english int = 70
DECLARE @result varchar(10)
SET @result = IIF ( @math > @english, '數學高', '英文高' )
PRINT @result

//英文高
````
````
DECLARE @a int = 55
DECLARE @b int = 40
SELECT IIF ( @a > @b and @b > 35, 'TRUE', 'FALSE' ) AS 結果

//TRUE
````
#### CHOOSE函數
````
DECLARE @type int
SET @type = 2
DECLARE @result varchar(10)
SET @result = CHOOSE ( @type, '全票', '半票', '敬老票', '免票')
PRINT @result

//半票
//索引值從1開始
````
### 批次(Batches)
一組T-SQL指令敘述的集合，批次可以一次執行多個指令敘述。
可使用GO指令來定義批次的結束。

GO並不是T-SQL指令，只是代表一個結束點的符號，以便在T-SQL指令碼檔案分隔出一至多個批次。

如果在T-SQL指令碼沒有使用GO指令，則代表此T-SQL指令碼就是一個批次，因為SQL Server會自動幫它加上GO指令。


### 建立檢視表(VIEW)
是一個虛擬資料表，本身並沒有儲存資料，只有定義資料。
````
CREATE VIEW 學生聯絡_檢視 (學號, 學生姓名, 學生電話)
AS
SELECT 學號, 姓名, 電話 FROM 學生
GO

SELECT * FROM 學生聯絡_檢視


修改已建立之檢視表，需使用
CREATE OR REPLACE VIEW XXX AS 
````

### 錯誤處理
TRY/CATCH錯誤處理指令敘述內，CATCH區塊必須緊接在TRY區塊之後。
````
BEGIN TRY
    T-SQL指令敘述
END TRY
BEGIN CATCH
    T-SQL指令敘述
END CATCH
````
````
BEGIN TRY
   SELECT 1/0   -- 除以零的錯誤
END TRY
BEGIN CATCH
   -- 顯示錯誤資訊
   SELECT ERROR_NUMBER() AS ErrorNumber, 
          ERROR_SEVERITY() AS ErrorSeverity, 
          ERROR_STATE() AS ErrorState,
          ERROR_PROCEDURE() AS ErrorProcedure,
          ERROR_LINE() AS ErrorLine, 
          ERROR_MESSAGE() AS ErrorMessage
END CATCH 
````
````
ERROR_NUMBER() : 傳回錯誤號碼
ERROR_SEVERITY() : 傳回錯誤嚴重性代碼
ERROR_STATE() : 傳回錯誤狀態碼 
ERROR_PROCEDURE() : 傳回發生錯誤的預存或觸發程序名稱 
ERROR_LINE() : 傳回造成錯誤的行列號 
ERROR_MESSAGE() : 傳回完整的錯誤訊息 
````
#### 使用RAISERROR()函數產生錯誤訊息
RAISERROR()函數除了可產生系統預設錯誤訊息外，也可自行新增所需的錯誤訊息。
````
EXEC sp_addmessage 訊息編號,嚴重等級,'錯誤訊息文字',@lang='使用的語言'
//自訂訊息編號需大於50000
````
````
EXEC sp_addmessage 55555, 5 ,'Error! grade < 0!', 
       @lang = 'us_english'
GO
EXEC sp_addmessage 55555, 5 ,'成績為負數的錯誤!', 
       @lang = '繁體中文'
````
````
BEGIN TRY
   RAISERROR (55555, 17, 10)
END TRY
BEGIN CATCH
   SELECT ERROR_NUMBER() AS ErrorNumber, 
          ERROR_SEVERITY() AS ErrorSeverity, 
          ERROR_STATE() AS ErrorState,
          ERROR_PROCEDURE() AS ErrorProcedure,
          ERROR_LINE() AS ErrorLine, 
          ERROR_MESSAGE() AS ErrorMessage
END CATCH 

//ERROR_SEVERITY大於10才會由TRY/CATCH去處理，小於10則只會顯示錯誤訊息
````

| ErrorNumber | ErrorSeverity | ErrorState |ErrorProcedure |ErrorLine |ErrorMessage |
| -------- | -------- | -------- |-------- |-------- |-------- |
| 55555     | 17     | 10     |NULL     |2     |成績為負數的錯誤!     |

#### THROW指令敘述
可使用THROW指令敘述來丟出例外，用來取代RAISERROR()函數。
```
THROW [錯誤編號,錯誤訊息,狀態值]
```
```
CREATE TABLE MyTEMPDB (ID INT PRIMARY KEY )
BEGIN TRY
   INSERT MyTEMPDB(ID) VALUES(1)
   INSERT MyTEMPDB(ID) VALUES(1)  -- 重複插入記錄
END TRY
BEGIN CATCH
   THROW
END CATCH

//因重複插入產生錯誤，使用THROW丟出例外，會由SQL Server處理來顯示系統預設的錯誤訊息
```
```
訊息 2627，層級 14，狀態 1，行 6
違反 PRIMARY KEY 條件約束 'PK__MyTEMPDB__3214EC279B22A246'。無法在物件 'dbo.MyTEMPDB' 中插入重複的索引鍵。重複的索引鍵值是 (1)。
```
```
BEGIN TRY
   SELECT 1/0   -- 除以零的錯誤
END TRY
BEGIN CATCH
   THROW 51000, '除以零的錯誤....', 1
END CATCH 
//顯示自訂的錯誤訊息
```
```
訊息 51000，層級 16，狀態 1，行 5
除以零的錯誤....
```

### 預存程序
> 在資料庫儲存複雜程式，以便外部程式呼叫的資料庫物件，可以視為資料庫的一種函式或子程式。
> 
> 是一組T-SQL指令的集合，只需編譯一次就可以執行多次，所以可以增進系統效能。
> 
> 在用戶端只須送出一列指令敘述就可執行位在Server伺服器的預存程序，不須傳送大量指令敘述，可減少網路傳送量。
> 
> 很像寫一支API，寫一個Method。再用EXEC去CALL它。

#### 特性
* 預存程序可封裝，並隱藏複雜的商業邏輯。
* 預存程序可以回傳值，並可以接受參數。
* 預存程序無法使用 SELECT 指令執行，因為它是子程式，與檢視表、資料表或使用者定義函式不同。
* 預存程序可以用在資料檢驗，強制實行商業邏輯等。

#### 分類
1. 使用者自訂 : 較常使用
2. 系統預設 : 會以sp字首開頭

#### 基本範例
````
CREATE PROCEDURE 課程資料報表 
AS
BEGIN

	SELECT 課程編號,名稱,學分
	FROM 課程

END
GO
//執行 > 儲存
````
````
CREATE PROCEDURE 學生上課報表 AS
BEGIN
  SELECT 學生.學號, 學生.姓名, 課程.*, 教授.*
  FROM 教授 INNER JOIN
  (課程 INNER JOIN 
  (學生 INNER JOIN 班級 ON 學生.學號 = 班級.學號) 
  ON 班級.課程編號 = 課程.課程編號) 
  ON 班級.教授編號 = 教授.教授編號
END
````
````
EXEC 預存程序名
//執行預存程序
````
````
DECLARE @AA CHAR(20)
SET @AA = '學生上課報表'
EXEC @AA

//可將預存程序儲存在變數中再拿來執行
````

#### 暫存預存程序
跟隨Session存在，即使用者上線時存在，使用者離線後，SQL Server就自動刪除暫存預存程序。

分為兩種:<br>
1.#開頭的區域暫存預存程序。
2.##開頭的全域暫存預存程序。
````
CREATE PROC #學生查詢 AS
BEGIN
  SELECT 學號, 姓名, 電話
  FROM 學生
END
GO
EXEC #學生查詢
````
#### 參數傳遞
可在預存程序宣告一至多個參數，參數值是在呼叫預存程序時，才由使用者提供。

**預存程序參數預設是一種輸入參數。可使用OUTPUT關鍵字，將參數宣告成輸出參數。**
````
CREATE PROCEDURE 課程查詢
   @c_no char(5)
AS
BEGIN
  SELECT 課程編號, 名稱, 學分
  FROM 課程
  WHERE 課程編號 = @c_no
END
````
````
CREATE PROCEDURE 員工查詢
   @salary money,
   @tax    money
AS
BEGIN
  IF @salary <= 0
     SET @salary = 30000
  IF @tax <= 0
     SET @tax = 300
  SELECT 身份證字號, 姓名, 
      (薪水-扣稅) AS 所得額
  FROM 員工
  WHERE 薪水 >= @salary
    AND 扣稅 >= @tax
END
````
````
EXEC 預存程序名 參數值1,參數值2
EXEC 預存程序名 @參數名1=參數值1,@參數名2=參數值2
//執行帶參數預存程序
````
````
CREATE PROCEDURE 地址查詢
   @city char(5) = '台北',
   @street varchar(30) = '中正路'
AS
BEGIN
  SELECT 身份證字號, 姓名, 
      (薪水-扣稅) AS 所得額, 
      (城市+街道) AS 地址
  FROM 員工
  WHERE 城市 LIKE @city
    AND 街道 LIKE @street
END
//給定預設值參數
````
````
EXEC 地址查詢 @street ='忠孝東路';
EXEC 地址查詢 default,'忠孝東路';
//沒給值的就載入預設值
````
#### 巢狀呼叫範例
````
CREATE PROCEDURE 呼叫程序
   @proc_name varchar(30)
AS
PRINT '開始層數: ' + CAST(@@NESTLEVEL AS char)
EXEC @proc_name
PRINT '結束層數: ' + CAST(@@NESTLEVEL AS char)
GO
CREATE PROCEDURE 測試程序
AS
PRINT '層數: ' + CAST(@@NESTLEVEL AS char)
````
````
EXEC 呼叫程序 '測試程序'

//測試程序當參數傳入然後呼叫
````
````
開始層數: 1
層數: 2
結束層數: 1
````
#### 預存程序的傳回值
預存程序可以傳回一些訊息，可以使用RETURN關鍵字傳回整數值來表示執行狀態，或在宣告參數時使用OUTPUT關鍵字，表示將參數值傳回呼叫者。

使用RETURN關鍵字
````
CREATE PROCEDURE 新增課程
   @c_no char(5),   //傳入參數
   @title  varchar(30),
   @credits int
AS
BEGIN
  DECLARE @errorNo int   //宣告變數
  INSERT INTO 課程 
  VALUES (@c_no, @title, @credits)
  SET @errorNo = @@ERROR   //@@=全域變數
  IF @errorNo <> 0   //不等於
  BEGIN
    IF @errorNo = 2627   //錯誤碼
       PRINT '錯誤! 重複索引鍵!'
    ELSE
       PRINT '錯誤! 未知錯誤發生!'
    RETURN @errorNO
  END
END

//當程序執行到RETURN關鍵字時，會馬上中止程序的執行，並且傳回資訊。
//預設成功傳回值為0
//因為會傳回值，故在EXEC時需要宣告一個變數來取得傳回值。
//EXEC @傳回值變數 = 預存程序名稱 參數值
````
````
DECLARE @retVar int
EXEC @retVar = 新增課程 'CS222','資料庫程式設計',3
PRINT '傳回代碼:' + CONVERT(varchar, @retVar)  

//需轉換成varchar，因字串不能加int
//使用上述預存程序來新增一筆課程紀錄
//錯誤! 重複索引鍵! 傳回代碼:2627
````

使用OUTPUT關鍵字
````
CREATE PROCEDURE 薪水查詢
   @name  varchar(12),
   @salary  money  OUTPUT   //輸出參數
AS
BEGIN
  SELECT @salary = 薪水
  FROM 員工
  WHERE 姓名 = @name
END

//使用OUTPUT關鍵字，將參數宣告成輸出參數
````
````
DECLARE @mySalary money
EXEC 薪水查詢 '張無忌', @salary = @mySalary OUTPUT
PRINT 'Joe”s薪水:' + CONVERT(varchar, @mySalary)

//在EXEC時需要宣告一個變數來取得傳回值。
//EXEC 預存程序名稱 @傳回值變數 = 參數值 OUTPUT
````
#### 修改預存程序
可以使用ALTER PROCEDURE指令來修改預存程序內容，但無法更改預存程序名稱。
```
ALTER PROCEDURE 課程資料報表 AS
BEGIN
  SELECT 課程編號, 名稱, 學分
  FROM 課程
  WHERE 學分 > 3
END
GO
EXEC 課程資料報表
```
可以使用DROP PROCEDURE來刪除預存程序
```
DROP PROCEDURE 課程資料報表
```
#### 系統預存程序
```
EXEC sp_helptext 預存程序名稱

//傳回預存程序內容
```
```
EXEC sp_columns TABLE名稱

//傳回欄位資訊
```

### 順序物件
建立
````
CREATE SEQUENCE 編號順序 AS INT
   START WITH 1   //起始值   
   INCREMENT BY 1   //增量值
   MINVALUE 1   //最小值
   NO MAXVALUE
````
使用
````
SELECT NEXT VALUE FOR 整數順序 AS 整數順序
````
````
SET IDENTITY_INSERT 好客戶 ON
GO
INSERT INTO 好客戶 (客戶編號, 身份證字號, 姓名)
VALUES (NEXT VALUE FOR 編號順序, 'A333333333' , '王大安')
GO
SET IDENTITY_INSERT 好客戶 OFF
GO
SET IDENTITY_INSERT 好員工 ON
GO
INSERT INTO 好員工 (員工編號, 姓名)
VALUES (NEXT VALUE FOR 編號順序, '王允傑')
GO
INSERT INTO 好員工 (員工編號, 姓名)
VALUES (NEXT VALUE FOR 編號順序, '陳允傑')
GO
SET IDENTITY_INSERT 好員工 OFF
GO
SELECT * FROM 好客戶
GO
SELECT * FROM 好員工

//結果會是兩個查詢結果的SEQ有連續，為客戶編號1、員工編號2~3
````

### 不同群組取第一筆資料
```
SELECT BUS_CODE,(SELECT TOP 1 VENDOR_NAME1 FROM VENDOR B WHERE B.BUS_CODE = A.BUS_CODE GROUP BY VENDOR_NAME1) AS VENDOR_NAME1
FROM VENDOR A
GROUP BY BUS_CODE;


//192.168.5.98 SunSystemData
SELECT * FROM (
SELECT  ROW_NUMBER() OVER (PARTITION BY B.LDG_TXN_REF ORDER BY C.HELD_JNL_SEQ) AS ROWN,C.PROV_JNL_TYPE, B.LDG_TXN_REF ,C.HELD_JNL_SEQ , A.HELD_JNL_NUM, C.ORIGINATOR_ID, C.DESCR, 
CASE WHEN C.D_C='D' THEN SUM(C.AMOUNT) END AMT_D ,CASE WHEN C.D_C='C' THEN SUM(C.AMOUNT) END AMT_C , 
CASE WHEN C.D_C='D' THEN SUM(C.RPT_AMT) END RPT_D ,CASE WHEN C.D_C='C' THEN SUM(C.RPT_AMT) END RPT_C
FROM SunSystemsData.dbo.F99_HELD_JNL_CTRL A
LEFT JOIN SunSystemsData.dbo.F99_HELD_JNL_HDR B ON A.HELD_JNL_NUM = B.HELD_JNL_NUM
LEFT JOIN SunSystemsData.dbo.F99_HELD_JNL_LINE C ON A.HELD_JNL_NUM = C.HELD_JNL_NUM
WHERE 
B.HDR_TYPE=1 AND C.LINE_DELETED <> 1 AND A.BDGT_CODE='A' 
GROUP BY C.PROV_JNL_TYPE, B.LDG_TXN_REF, A.HELD_JNL_NUM, C. ORIGINATOR_ID, C.DESCR, C.D_C, HELD_JNL_SEQ
--ORDER BY B.LDG_TXN_REF, C.HELD_JNL_SEQ
) TTT
WHERE ROWN = 1
ORDER BY LDG_TXN_REF, HELD_JNL_SEQ
```
```
//EMP2 FROM ORACLE

//找出第一筆
SELECT * FROM (
SELECT ROW_NUMBER() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2)
WHERE ROWN=1;


//只可看出排序
SELECT ROW_NUMBER() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2;
```
### 不同群組取第一筆資料(排序三種類型補充)
```
1.ROW_NUMBER() OVER
//同群組依照金額排名，流水號排序DEPTNO(10)1-2-3-4... DEPTNO(20)1-2-3...
SELECT ROW_NUMBER() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2

//把PARTITION拿掉就是不分群全部依照金額做排序
SELECT ROW_NUMBER() OVER (ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2

2.DENSE_RANK() OVER
//同群組依照金額排名，流水號排序，但有相同金額時，排序會為DEPTNO(10)1-1-2-3-4...
SELECT DENSE_RANK() OVER(PARTITION BY DEPTNO ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2

//把PARTITION拿掉就是不分群全部依照金額做排序
SELECT DENSE_RANK() OVER(ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2

3.RANK() OVER
//同群組依照金額排名，流水號排序，但有相同金額時，排序會為DEPTNO(10)1-1-3-4...
SELECT RANK() OVER(PARTITION BY DEPTNO ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2

//把PARTITION拿掉就是不分群全部依照金額做排序
SELECT RANK() OVER(ORDER BY SAL DESC) AS ROWN, DEPTNO, EMPNO, SAL FROM EMP2
```

### TABLE鎖定
> 在TEST1未執行COMMIT前，TABLE會鎖住，TEST2會無法查詢或更新。但只要TEST1一執行COMMIT，TEST2即會進行剛剛卡住的動作。
```
// QUERY1
BEGIN TRAN
SELECT * FROM dbo.TEST WITH(TABLOCKX) 
UPDATE dbo.TEST SET NAME='TEST1' WHERE ID='10'

COMMIT


// QUERY2
BEGIN TRAN
SELECT * FROM dbo.TEST WITH(TABLOCKX) 
UPDATE dbo.TEST SET NAME='TEST2' WHERE ID='10'

COMMIT


```
















### 舊案參考
192.168.5.92 FISSYS_HOTA
迴圈cursor與TempTable
