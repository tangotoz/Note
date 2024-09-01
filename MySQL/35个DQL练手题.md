---
date: 2024-08-14
tags:
  - 数据库
text: 练习题
---
## 第一题
1. 取得每个部门最高薪水的人员名称
我的做法：
```SQL
SELECT deptno, MAX(sal) AS maxsal, SUBSTRING_INDEX(GROUP_CONCAT(ename ORDER BY sal DESC), ',', 1) AS ename FROM emp GROUP BY deptno;
```
错误，拥用最高工资的人可能有2个。
答案：
第一步：取得每个部门的最高薪水
```SQL
SELECT deptno, MAX(sal) AS maxsal FROM emp GROUP BY deptno;
```
第二步：将上面的查询结果当作临时表t，t和emp e进行连接，条件：e.deptno = t.deptno and e.sal =t.maxsal
```SQL
SELECT 
t.*, e.ename
FROM
(SELECT deptno, MAX(sal) AS maxsal FROM emp GROUP BY deptno) t
INNER JOIN
emp e
ON
t.deptno = e.deptno AND t.maxsal = e.sal;
```
## 第二题
2. 那些人的薪水在部门的平均薪资之上。
第一步：找出每个部门的平均薪资。
```SQL
SELECT deptno, AVG(sal) AS avgsal FROM emp GROUP BY deptno;
```
第二步：将上述查询结果作为临时表t，t和emp e连接，条件：t.deptno = e.deptno and e.sal > t.avgsal
```SQL
SELECT e.ename, e.sal, t.* FROM (SELECT deptno, AVG(sal) AS avgsal FROM emp GROUP BY deptno) t
INNER JOIN
emp e
ON
t.deptno = e.deptno AND t.avgsal < e.sal;
```
## 第三题
3. 取得每个部门的平均薪资的等级。
第一步：取得每个部门平均薪水
```SQL
SELECT deptno, AVG(sal) avgsal FROM emp GROUP BY deptno;
```
第二步：以上查询结果作为临时表t，和salgrade s表进行拼接，条件：t.avgsal BETWEEN s.losal AND s.hisal。
```SQL
SELECT
t.*, s.grade 
FROM
(SELECT deptno, AVG(sal) avgsal FROM emp GROUP BY deptno) t
INNER JOIN
salgrade s
ON
t.avgsal BETWEEN s.losal AND s.hisal;
```
## 第四题
4. 取得部门中（所有人的）平均的薪水等级 每个部门中薪水等级的平均值。
第一步：找出每个人的薪水等级
```SQL
SELECT e.deptno, e.ename, e.sal, s.grade FROM emp e INNER JOIN salgrad
e s ON e.sal BETWEEN s.losal AND s.hisal;
```
第二步：基于上述结果继续按照deptno进行分组，对grade求平均值。
```SQL
SELECT
t.deptno, AVG(t.grade)
FROM
(SELECT e.deptno, e.ename, e.sal, s.grade FROM emp e INNER JOIN salgrade s ON e.sal BETWEEN s.losal AND s.hisal) t 
GROUP BY
deptno;
```

