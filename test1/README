# 实验1：SQL语句的执行计划分析与优化指导
## 实验目的
分析SQL执行计划，执行SQL语句的优化指导。理解分析SQL语句的执行计划的重要作用。
## 实验内容
·对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。

·首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。

·设计自己的查询语句，并作相应的分析，查询语句不能太简单。

## 实验过程
1.教材中的查询

    set autotrace on

    SELECT d.department_name,count(e.job_id)as "部门总人数",avg(e.salary)as "平均工资"
    from hr.departments d,hr.employees e
    where d.department_id = e.department_id
    and d.department_name in ('IT','Sales')
    GROUP BY d.department_name;

 查询结果截图：

  ![t1](t1.png)

 实验结果分析：

 该SQL语句的执行计划为：2214196163。它的physical reads为0，说明从磁盘请求到Buffer Cache的数据量很少，意味着不需要从系统库存里大量全表扫描SQL语句。它的consistent gets为9，意味着它需要从Buffer cache中读取的undo数据的block数据为9，相较于第二条SQL语句读取数据更少，效率更高。
 该SQL语句执行效率较优执行优化指导

  ![result](result1.png)



2.教材中的查询：

    set autotrace on
    SELECT d.department_name,count(e.job_id)as "部门总人数",avg(e.salary)as "平均工资"
    FROM hr.departments d,hr.employees e
    WHERE d.department_id = e.department_id
    GROUP BY d.department_name
    HAVING d.department_name in ('IT','Sales');
  
 查询结果截图：

 ![t2](t2.png)

 实验结果分析：
  
  该SQL语句的执行计划为2270224988。它的physical reads为0，说明从磁盘请求到Buffer Cache的数据量很少，意味着不需要从系统库存里大量全表扫描SQL语句。虽然它physical reads数量同样为0，但是它的consistent gets为13，意味着它需要从Buffer cache中读取的undo数据的block数据为13，相较于第一条SQL语句来说读取数据更多，效率相对也会变得更低


3.自定义查询：
    SELECT d.department_name,count(e.job_id)as "部门总数",avg(e.salary)as "平均工资",max(e.salary)as "最高工资",min(e.salary)as "最低工资"
    from hr.departments d,hr.employees e
    where d.department_id=e.department_id
    GROUP BY d.department_name;
    
  查询结果：
  ![t3](t3.png)

  ![t4](t4.png)

  ![t5](t5.png)

  查询结果分析:
   在元查找部门总数和平均工资的基础上，新添加查找最高工资最低工资的查询语句，新填查询语句后physical gets等于19，说明在新增加查询语句后从数据库扫描SQL语句量增多。

