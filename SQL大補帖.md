# SQL大補帖

### CRUD
```
#INSERT INTO DEPT2(DEPTNO,LOC) VALUES(70,'基隆車站'); //有三個欄位，不用全部新增

SELECT DEPTNO,LOC FROM DEPT2;

UPDATE DEPT2 SET LOC='基隆廟口' WHERE DEPTNO=70;

#DELETE FROM DEPT2 WHERE DEPTNO=70;

```
```
寫的順序：SELECT > FROM > WHERE > GROUP BY > HAVING > ORDER BY
```
### PK and FK
```
PK被FK參考的時候，不能刪除PK值，也不能修改值。

PK沒有值A1234的時候，FK不能寫入A1234，也不能建立FK連結。 PK有值的時候，FK才能寫入。

建立從PK父層開始，刪除從FK子層開始。
```
### 刪除主表同時刪除子表(Cascade)
```
--刪除PK可連動刪除FK(注意順序)--

ALTER TABLE child_table_name 
  ADD CONSTRAINT fk_name 
  FOREIGN KEY (child_column_name) 
  REFERENCES parent_table_name(parent_column_name) 
  ON DELETE CASCADE;

ALTER TABLE CUST 
  ADD CONSTRAINT FK_NAME
  FOREIGN KEY (CUST_ID) 
  REFERENCES ACCT(CUST_ID) 
  ON DELETE CASCADE;
 (ON UPDATE CASCADE)
```
### 刪除主表同時刪除子表
```
主表:
create table tb1
(
   weeklyNo varchar(17) primary key,
   remark varchar(200)
);

子表:
create table tb2
(
   timeId varchar(17) primary key,
   weeklyNo varchar(17),
   foreign key(weeklyNo) references tb1(weeklyNo)
);


//通过主表ID删除，在删除主表数据的时候，跟主表外键关联的子表数据也会相应的删除。
delete t1,t2 from tb2 t2,tb1 t1 where t1.weeklyNo=t2.weeklyNo and t1.weeklyNo='1';
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
```
```
INSERT INTO TEST(ID,NAME) VALUES(10,'JACK');

INSERT INTO TEST　VALUES(20,'TOM');

//兩種皆可新增完成
````
### 限制查詢筆數(TOP, LIMIT, ROWNUM)
* SQL Server
```
SELECT TOP 10 * FROM Customers;
```
* MySQL 
```
SELECT * FROM customers LIMIT 10;
```
* Oracle 
```
SELECT * FROM customers WHERE ROWNUM <= 10;
```
### 查詢區間兩種寫法
```
SELECT * FROM customers
WHERE Quantity
BETWEEN 1000 AND 4000;


SELECT * FROM customers
WHERE Quantity >= 1000 AND Quantity <= 4000;
```
### ANY (滿足其中一個值，就篩選進來) (ANY=SOME)
```
=ANY(xxx,xxx)  相當於=SOME(xxx,xxx)  相當於 IN(xxx,xxx)

SELECT 
  EMPLOYEE_ID,
  FIRST_NAME,
  JOB_ID,
  SALARY,
  DEPARTMENT_ID
FROM EMPLOYEES 
WHERE salary = ANY(
                   24000,12000,10000
                )
ORDER BY employee_id;
```
### ALL (滿足全部的值，才篩選進來)
```
SELECT 
  EMPLOYEE_ID,
  FIRST_NAME,
  JOB_ID,
  SALARY,
  DEPARTMENT_ID
FROM EMPLOYEES 
WHERE salary = ALL(
                   12000,10000
                )
ORDER BY employee_id;
```
### 轉換匯總
```
Oracle 可以使用TO_CHAR( )、TO_DATE( )函數、TO_NUMBER( )函數、CAST( )函數

SQL Server 可以使用CONVERT( )函數、CAST( )函數

CAST( )函數為ANSI-SQL

CONVERT( )函數為T-SQL
```
* Oracle
```
//以下結果相同，可交替使用

SELECT  TO_NUMBER('123')+1  AS  A  FROM  DUAL;

SELECT  CAST('123'  AS  NUMBER)+1  AS  A  FROM  DUAL;


//以下結果相同，可交替使用

SELECT  TO_CHAR(123)  AS  ABC  FROM  DUAL;

SELECT  CAST (123  AS  VARCHAR(20))  AS  ABC  FROM  DUAL;
```
* SQL Server
```
//以下結果相同，可交替使用

SELECT  CAST('2016-06-30'  AS  DATE)  AS  ABC;

SELECT  CONVERT(DATE,'2016-06-30')  AS  ABC;


//以下結果相同，可交替使用

SELECT  CAST(123  AS  VARCHAR(20))  AS  ABC;

SELECT  CONVERT(VARCHAR(20), 123)  AS  ABC;
```
### TO_CHAR (日期轉字串 / 數字轉字串)
```
SELECT 
  TO_CHAR(SYSDATE,'YYYY MM DD HH24 MI SS') TEST1,
  TO_CHAR(SYSDATE,'YYYY/MM/DD HH24 MI SS') TEST2,
  TO_CHAR(SYSDATE,'YYYYMMDDHH24MISS') TEST3
  TO_CHAR(HIREDATE, 'YYYY') FROM EMP2; //只要年
FROM DUAL;
```
### TO_DATE (字串轉日期)
```
SELECT 
  TO_DATE('2014-05-17','YYYY-MM-DD')
FROM DUAL;
```
### NUMBER轉DATE (數字轉字串再轉日期)
```
SELECT 
TO_DATE(TO_CHAR(20140520),'YYYY-MM-DD')
FROM DUAL ;
```
### TO_NUMBER (字串轉數字)
```
SELECT 
to_number('11239781') +1
FROM DUAL ;
```
### ROUND (四捨五入)
```
SELECT 
  ROUND(1.436), //1
  ROUND(1.536), //2
  ROUND(1.444,2), //1.44
  ROUND(1.555,2) //1.56
FROM DUAL;
```
### TRUNC (無條件捨去)
```
SELECT 
  TRUNC(1.436), //1
  TRUNC(1.536), //1
  TRUNC(1.444,2), //1.44
  TRUNC(1.555,2) //1.55
FROM DUAL;
```
### MOD (取餘數)
```
SELECT 
  MOD(3001,6) //1
FROM DUAL;
```
### DATEADD (日期增加)
```
//增加30日
SELECT  WORKDAT FROM CALENDAR 
WHERE WORKDAT BETWEEN '2022-11-01' AND DATEADD(day, 30, '2022-11-01') 
AND WORKMAK='Y' ORDER BY WORKDAT 
```
### 字串連結
* SQL Server
```
SELECT CONCAT(EMPNO,ENAME) AS ABC FROM EMP2;
```
* Oracle 
```
//差別在於||' WORDS '|| 中間可以加入其他文字串接

SELECT EMPNO ||''|| ENAME AS ABC FROM EMP2;

SELECT CONCAT(EMPNO,ENAME) AS ABC FROM EMP2;
```
### LOWER/ UPPER (字串轉全大小寫)
```
SELECT 
  EMPLOYEE_ID,
  LOWER(FIRST_NAME) //UPPER(FIRST_NAME)
FROM EMPLOYEES 
WHERE EMPLOYEE_ID = 100;
```
### SUBSTR (取一段字串)
```
SUBSTR('字串',起始位置,取幾個)
SUBSTR('字串',起始位置)

在Java substring(index,index);   在oralce SUBSTR(index,取幾個)   兩個是不同的
//Java substring()是index從0開始，不含結尾處。//"hamburger".substring(3,8)
//Oracle SUBSTR是index從1開始，含結尾處。// SUBSTR(FIRST_NAME,1,2)
```
### LENGTH (求長度)
```
SELECT 
  EMPLOYEE_ID,
  FIRST_NAME,
  LENGTH(FIRST_NAME)
FROM EMPLOYEES 
WHERE EMPLOYEE_ID = 100;
```
### LPAD/RPAD (補值)
```
LPAD 向左填補滿位數
LPAD(欄位,總位數,補值)

SELECT 
  EMPLOYEE_ID,
  FIRST_NAME,
  SALARY,
  LPAD(SALARY,10,0)
FROM EMPLOYEES 
WHERE EMPLOYEE_ID = 100;
```
### TRIM (去頭尾)
```
TRIM 去掉字串前後不要的字 //只能去掉前後一個字元，中間無法去掉

SELECT 
  EMPLOYEE_ID,
  FIRST_NAME,
  TRIM('S' FROM FIRST_NAME)
FROM EMPLOYEES 
WHERE EMPLOYEE_ID = 100;
```
### REPLACE (置換文字)
```
SELECT 
  EMPLOYEE_ID,
  FIRST_NAME,
  REPLACE(FIRST_NAME,'S','L') // L取代FIRST_NAME的S
FROM EMPLOYEES 
WHERE EMPLOYEE_ID = 100;
```
### 空字串以及NULL
```
在ORACLE裡，根本沒有空字串('')這種東西，空字串會被視為NULL。

在SQL-SERVER，可以設定值為空字串('')或者是NULL。
```
### NVL/NVL2 不同資料庫用法
```
NVL、NVL2  // Oracle獨有方法

ISNULL  //MS-SQL獨有方法

SELECT CASE WHEN THEN  //ANSI通用方法

COALESCE  //ANSI通用方法
```
* NVL (如果是NULL,則用此值)
```
SELECT 
      employee_id,
      commission_pct,
      NVL(commission_pct,0) "佣金"
FROM employees;
```
* NVL2(要判斷的欄位, 如果不是NULL 則取這裡, 如果是NULL則取這裡)
```
SELECT 
      employee_id,
      commission_pct,
      NVL2(commission_pct,'有佣金','無佣金') "佣金"
FROM employees
WHERE employee_id > 140;
```
### CASE WHEN THEN (ELSE) END (如果為XX條件，則輸出OO)
```
SELECT 
      employee_id,
      salary,
      case  when salary between 0     and 4999  then '低收入'
            when salary between 5000  and 9999  then '中低收入'
            when salary between 10000 and 14999 then '中收入'
            when salary between 15000 and 19999 then '中高收入'
            else  '高收入' 
   end "薪水收入等次"
FROM employees
WHERE employee_id > 140
order by salary;
```
### DECODE (如果為XX值，則輸出OO值)
```
select 
      employee_id,
      salary,
      decode( salary ,  2500 , '收入為2500',
                        3000 , '收入為3000',
                        '其它收入') TEXT1
FROM employees
WHERE employee_id > 140
ORDER BY salary;
```
### JOIN自己
```
CREATE TABLE tb_Employee
(
    Id INT IDENTITY(1,1) NOT NULL,
    Name VARCHAR(16) NOT NULL,
    City VARCHAR(64) NULL
)
GO
INSERT INTO tb_Employee VALUES('Joe', 'New York')
INSERT INTO tb_Employee VALUES('Henry', 'Taipei')
INSERT INTO tb_Employee VALUES('Sam','Tokyo')
INSERT INTO tb_Employee VALUES('Max', 'New York')
INSERT INTO tb_Employee VALUES('Kenny', 'New York')
GO

DECLARE @NAME VARCHAR(16)
SET @NAME='MAX'

SELECT B.NAME, B.CITY FROM tb_Employee A 
JOIN tb_Employee B ON A.City = B.City 
WHERE A.NAME = @NAME;
```
```
找出住在相同城市的那些人

Joe	    New York
Max	    New York
Kenny	New York
```
### 特殊JOIN方法
* 不用JOIN 的JOIN用法 (FROM後放多個TABLE，JOIN ON改成WHERE)
```
//結果相同

SELECT E.EMPNO, E.DEPTNO, D.DNAME 
FROM EMP2 E, DEPT2 D
WHERE E.DEPTNO = D.DEPTNO;


SELECT E.EMPNO, E.DEPTNO, D.DNAME 
FROM EMP2 E
JOIN DEPT2 D ON E.DEPTNO = D.DEPTNO;
```
* JOIN USING (=JOIN ON)
```
//結果相同

SELECT E.EMPNO, D.DNAME
FROM EMP2 E
JOIN DEPT2 D ON E.DEPTNO = D.DEPTNO;


SELECT E.EMPNO, D.DNAME
FROM EMP2 E
JOIN DEPT2 D USING(DEPTNO);
```
### 避免一對多JOIN時的重複資料地雷 
> on的key值如果不是一對一關係，是一對多時就會出現查詢時重複資料問題。

> 一對多並不一定是問題，主要還是看表與表之間的關係。
```
LEFT JOIN 

DISTINCT   (篩掉重複的)

ON         (多個KEY做ON連結 / 或者設定多個欄位條件XXX=???  才能避免重複)

GROUP BY (除了聚集函數以外，所有欄位皆要放入)

ON ex:
bank_branch_code	account_no
0042570	            257001009796      
0050267	            026001329439      
0050267	            026001358251      
0050267	            026001361111      
0050267	            026001378880      
0050267	            026051066161      
0050290	            029001332561      
0050290	            029001334784      
0050290	            029001350411      
0050290	            029051051422      
0050290	            029051055151      

bank_branch_code	account_no
0050290	            029001350411   
0042570	            257001009796     
0050267	            026001378880   
```
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
### 不同群組取第一筆資料 (排序三種類型補充)
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
### 資料逐筆/多筆加總
```
//子查詢:逐筆累計金額
//外查詢:查出每兩筆的金額

SELECT PRICE FROM
(SELECT ROW_NUMBER() OVER (PARTITION BY R11_MESSAGE ORDER BY R11_MESSAGE) AS NO,SUM(PRICE) OVER(PARTITION BY SERIALNO ORDER BY ROWNUM) AS PRICE
FROM A1)
WHERE MOD(NO,2)=0;
```
### SELECT時自建欄位
```
SELECT '我是多餘的' as C, LOC FROM DEPT2;

SELECT 100 AS PRICE, DEPTNO FROM DEPT2;
```

### 重複相同欄位
```
SELECT 'TRUE' AS QUERYED, DEPTNO, LOC, LOC AS LOC1, LOC AS LOC2 FROM DEPT2;
```
### 定序衝突
```
SELECT A.DESCR,(A.ACNT_CODE collate Chinese_Taiwan_Stroke_CI_AS) AS ACNT_CODE
,A.ACNT_TYPE,B.REM001 
FROM [SunSystemsData].dbo.PK1_ACNT A JOIN [FISBNP].dbo.APS020PF B 
ON (ACNT_CODE collate Chinese_Taiwan_Stroke_CI_AS) = ACCNT_CODE;

ACCNT_CODE 定序為:Chinese_Taiwan_Stroke

ACNT_CODE  定序為:Latin1_General_BIN

將ACNT_CODE 對照為Chinese_Taiwan_Stroke_CI_AS 即可解決
```
### SQL SERVER設定區分大小寫
```
DROP INDEX TREFERNCE on dbo.APS020PF

ALTER TABLE dbo.APS020PF
ALTER COLUMN TREFERNCE nvarchar(30)
COLLATE Chinese_Taiwan_Stroke_CS_AS
```
### SQL Developer字體調整
```
功能列表字體:
C:\Users\jeff_cheng\AppData\Roaming\SQL Developer\system19.2.1.247.2212\o.sqldeveloper/ide.properties
Ide.FontSize=18
Ide.FontSize.Aqua=8


編輯區字體: 
Windows/Preferences/Fonts


設定英文版:
C:\Users\asgard\Desktop\sqldeveloper-19.2.1.247.2212-no-jre\sqldeveloper\sqldeveloper\bin

AddVMOption -Duser.language=en
AddVMOption -Duser.country=US
```
### 建立暫存資料表 (Oracle可自行建立欄位及內容)
* SQL Server
```
Select * into [#ABC] from [資料表名稱] where 條件
```
* Oracle 
```
Create Global Temporary Table ABC (
  NAME VARCHAR2(25)
, CLASS VARCHAR2(25)
);

INSERT INTO ABC VALUES('JEFF','EA103');
INSERT INTO ABC VALUES('JIM','EA104');
```
### 建立檢視表VIEW (需使用其他Table資料)
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
