# 实验一

## 教材中的查询语句及其运行结果

查询1：
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
运行结果:
![]()
优化结果:
![]()

查询2:
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
```
运行结果：
![]()
优化结果:
![]()

分析：
查询1和查询2都是能够从数据库中成功查询到我们所需要的信息，区别在与一个用的where,一个用得是having，而Where”是一个约束声明，在查询数据库的结果返回之前对数据库中的查询条件进行约束，即在结果返回之前起作用，且where后面不能使用“聚合函数”；“Having”是一个过滤声明，所谓过滤是在查询数据库的结果返回之后进行过滤，即在结果返回之后起作用，并且having后面可以使用“聚合函数”，两者之间性能区别不大。

## 自定义查询

查询3
```SQL
SELECT d.department_name，count(e.job_id)as "部门总人数",
avg(e.salary)as "平均工资"
FROM hr.departments d left outer join hr.employees e
on d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
```
运行结果:
![]()
分析：
查询3用的是左外连接，左外连接不但返回符合连接和查询条件的数据行，还返回左表中不符合连接条件单符合查询条件的数据行，从运行结果来看，显然存在一些左表
不符合的数据行，从而使得显现不出来所有的结果，还有所欠缺。
