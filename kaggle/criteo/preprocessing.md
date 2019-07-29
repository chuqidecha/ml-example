# criteo数据集预处理和分析

criteo的train数据解压之后10G+，由于数据量很大，无法直接读取到内存中，将数据导入sqlite进行简单的统计分析。

## 数据导入sqlite
1. 创建train表

```sql
CREATE TABLE train (
    LABEL              INTEGER,
    NUMERIC_COL_01     INTEGER,
    NUMERIC_COL_02     INTEGER,
    NUMERIC_COL_03     INTEGER,
    NUMERIC_COL_04     INTEGER,
    NUMERIC_COL_05     INTEGER,
    NUMERIC_COL_06     INTEGER,
    NUMERIC_COL_07     INTEGER,
    NUMERIC_COL_08     INTEGER,
    NUMERIC_COL_09     INTEGER,
    NUMERIC_COL_10     INTEGER,
    NUMERIC_COL_11     INTEGER,
    NUMERIC_COL_12     INTEGER,
    NUMERIC_COL_13     INTEGER,
    CATEGORICAL_COL_01 CHAR (32),
    CATEGORICAL_COL_02 CHAR (32),
    CATEGORICAL_COL_03 CHAR (32),
    CATEGORICAL_COL_04 CHAR (32),
    CATEGORICAL_COL_05 CHAR (32),
    CATEGORICAL_COL_06 CHAR (32),
    CATEGORICAL_COL_07 CHAR (32),
    CATEGORICAL_COL_08 CHAR (32),
    CATEGORICAL_COL_09 CHAR (32),
    CATEGORICAL_COL_10 CHAR (32),
    CATEGORICAL_COL_11 CHAR (32),
    CATEGORICAL_COL_12 CHAR (32),
    CATEGORICAL_COL_13 CHAR (32),
    CATEGORICAL_COL_14 CHAR (32),
    CATEGORICAL_COL_15 CHAR (32),
    CATEGORICAL_COL_16 CHAR (32),
    CATEGORICAL_COL_17 CHAR (32),
    CATEGORICAL_COL_18 CHAR (32),
    CATEGORICAL_COL_19 CHAR (32),
    CATEGORICAL_COL_20 CHAR (32),
    CATEGORICAL_COL_21 CHAR (32),
    CATEGORICAL_COL_22 CHAR (32),
    CATEGORICAL_COL_23 CHAR (32),
    CATEGORICAL_COL_24 CHAR (32),
    CATEGORICAL_COL_25 CHAR (32),
    CATEGORICAL_COL_26 CHAR (32),
    ID                 INTEGER   PRIMARY KEY AUTOINCREMENT
);
```
2. 从csv文件中导入数据
```sql
.separator "\t"
.import csv-file-path table-name
```
   

同样的方法，将test数据也导入sqlite。

## 类别特征分析
1. 创建一张表存储各个类别特征的出现次数。
```sql
CREATE TABLE train_stat(              
    ID INTEGER PRIMARY KEY AUTOINCREMENT, 
    COL_NAME CHAR(32),                    
    COL_VALUE CHAR(32),                   
    VALUE_COUNT INTEGER                   
);                                    
```
2. 使用sql统计训练集各类别特征的出现次数
```sql
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_01' AS COL_NAME, CATEGORICAL_COL_01,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_01;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_02' AS COL_NAME, CATEGORICAL_COL_02,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_02;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_03' AS COL_NAME, CATEGORICAL_COL_03,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_03;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_04' AS COL_NAME, CATEGORICAL_COL_04,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_04;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_05' AS COL_NAME, CATEGORICAL_COL_05,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_05;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_06' AS COL_NAME, CATEGORICAL_COL_06,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_06;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_07' AS COL_NAME, CATEGORICAL_COL_07,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_07;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_08' AS COL_NAME, CATEGORICAL_COL_08,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_08;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_09' AS COL_NAME, CATEGORICAL_COL_09,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_09;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_10' AS COL_NAME, CATEGORICAL_COL_10,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_10;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_11' AS COL_NAME, CATEGORICAL_COL_11,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_11;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_12' AS COL_NAME, CATEGORICAL_COL_12,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_12;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_13' AS COL_NAME, CATEGORICAL_COL_13,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_13;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_14' AS COL_NAME, CATEGORICAL_COL_14,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_14;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_15' AS COL_NAME, CATEGORICAL_COL_15,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_15;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_16' AS COL_NAME, CATEGORICAL_COL_16,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_16;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_17' AS COL_NAME, CATEGORICAL_COL_17,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_17;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_18' AS COL_NAME, CATEGORICAL_COL_18,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_18;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_19' AS COL_NAME, CATEGORICAL_COL_19,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_19;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_20' AS COL_NAME, CATEGORICAL_COL_20,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_20;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_21' AS COL_NAME, CATEGORICAL_COL_21,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_21;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_22' AS COL_NAME, CATEGORICAL_COL_22,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_22;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_23' AS COL_NAME, CATEGORICAL_COL_23,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_23;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_24' AS COL_NAME, CATEGORICAL_COL_24,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_24;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_25' AS COL_NAME, CATEGORICAL_COL_25,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_25;
INSERT INTO train_stat(COL_NAME,COL_VALUE,VALUE_COUNT) SELECT 'CATEGORICAL_COL_26' AS COL_NAME, CATEGORICAL_COL_26,COUNT(*)  FROM train GROUP BY CATEGORICAL_COL_26;
```
在sqlite里执行脚本统计：
```
.read sql-file-path
```
3. 每个类别的特征值个数
```
select COL_NAME,COUNT(*) as count from train_stat group by COL_NAME order by count;
```
执行结果：
|COL_NAME|COUNT
|-------|---
|CATEGORICAL_COL_09|3
|CATEGORICAL_COL_20|4
|CATEGORICAL_COL_17|10
|CATEGORICAL_COL_23|15
|CATEGORICAL_COL_22|18
|CATEGORICAL_COL_06|24
|CATEGORICAL_COL_14|27
|CATEGORICAL_COL_25|105
|CATEGORICAL_COL_05|305
|CATEGORICAL_COL_02|583
|CATEGORICAL_COL_08|633
|CATEGORICAL_COL_01|1460
|CATEGORICAL_COL_19|2173
|CATEGORICAL_COL_13|3194
|CATEGORICAL_COL_18|5652
|CATEGORICAL_COL_11|5683
|CATEGORICAL_COL_07|12517
|CATEGORICAL_COL_15|14992
|CATEGORICAL_COL_10|93145
|CATEGORICAL_COL_26|142572
|CATEGORICAL_COL_24|286181
|CATEGORICAL_COL_04|2202608
|CATEGORICAL_COL_16|5461306
|CATEGORICAL_COL_21|7046547
|CATEGORICAL_COL_12|8351593
|CATEGORICAL_COL_03|10131227
从上表可以看出，`CATEGORICAL_COL_03`特征值个数接近总样本数的1/4（总样本数45840617）有较的特征值仅出现过一次。
```
sqlite> select VALUE_COUNT,COUNT(*) from train_stat where COL_NAME = "CATEGORICAL_COL_03" group by VALUE_COUNT order by VALUE_COUNT limit 10;
1|8585335
2|751373
3|253210
4|127735
5|78196
6|52255
7|37927
8|28570
9|22678
10|18168
```