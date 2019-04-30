# 常用命令
## SQLPlus

命令|描述
---|---
desc merchant | 查询表 merchant 结构

# 常用函数

函数|描述
---|---
NVL (expr1, expr2) | expr1为NULL，返回expr2；不为NULL，返回expr1。注意两者的类型要一致    
NVL2 (expr1, expr2, expr3) | expr1不为NULL，返回expr2；为NULL，返回expr3。expr2和expr3类型不同的话，expr3会转换为expr2的类型 .
COALESCE(expre1,expre2,expre3) | 返回参数列表中第一个不为空的参数
NULLIF(expre1,expre2) |参数相等，返回null，如果不相等，返回第一个参数。你能够为第一个参数指定空字符。


# 常用查询案列
> 表 merchant 
1. 查询空值 
```sql
select * from merchant where phone is  null 
```
2. 查询结果拼接
```sql
SELECT '商户号为' || MER_NO || '的商户' test3 FROM MERCHANT WHERE MER_NO = '0000143' 
```
3. 使用伪列rownum，限制返回的行数
```sql
select * from  merchant where rownum <=2 
```
4. 使用列号排序
```sql
select a , b, c from merchant order by b asc 
select a , b, c from merchant order by 2 asc 
```
5. 多字段排序 (b升 c降)
```sql
select a , b, c from merchant order by 2 asc , 3 desc 
```
6. 排序-按照字串
> 实质是增加一个计算列，通过该列排序
```sql
SELECT MER_NO,"SUBSTR"(MER_NO, -4) FROM "QYFTEST"."MERCHANT" ORDER BY 2 ASC;
```
7. 随机返回N条记录
```sql
SELECT MER_NO,id  FROM (
SELECT MER_NO,id FROM "QYFTEST"."MERCHANT"  ORDER BY dbms_random.value()
)
WHERE rownum <= 3
```
8. 替换（TRANSLATE(expr, from_string,to_string)）
```sql
# 替换
SELECT "TRANSLATE"('household', 'abcdefghij', '0123456789')role_id FROM dual;
结果 ： 7ous47ol3

# 去除数字（'-' 不可以去除）
SELECT "TRANSLATE"('household2 123123', '- 0123456789', '-')role_id FROM dual;
结果 ：household
```
9. 更改空值排序
> oracle默认 升序空值在后，降序空值在前
```sql
# nulls first ,更改升序 空值在前
SELECT MER_NO,EX_ROLE_CODES FROM MERCHANT ORDER BY EX_ROLE_CODES ASC nulls first

# nulls last， 更改降序 空值在后
SELECT MER_NO,EX_ROLE_CODES FROM MERCHANT ORDER BY EX_ROLE_CODES DESC nulls last
```
10. 取不同列的值进行排序
> 工资在1000到2000之间的优先排序
```sql
select empno as 编码，ename as 姓名，case when  sal >=1000 and sal <=2000 then 1 else 2 end as 级别，sal as 工资
from merchant
order by 3, 4
# ============== 另一种写法==========
select empno as 编码，ename as 姓名，sal as 工资
from merchant
order by case when  sal >=1000 and sal <=2000 then 1 else 2 end , 3
```
11. 合并多个数据集(UNION ALL)
> 两个数据集结果相加，但是列的数目需要一致；   
UNION ALL不去重，UNION 去重
```sql
SELECT mer_no, role_id FROM MERCHANT
union ALL
SELECT merchant_no,MERCHANT_NAME from MERCHANT_ADDINFO
```
