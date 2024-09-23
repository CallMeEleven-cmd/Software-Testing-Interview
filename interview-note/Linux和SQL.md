# Linux和SQL

# Linux

### 文件夹相关：

新建touch mkdir、编辑vi vim nano、删除rm -rf 、查看cat less more、复制移动cp mv，压缩解压tar gzip

搜索指定字符串grep、指定目录下查找find

修改权限chown

### 网络：

下载wget curl 、连接ssh、测试ping

查看网络状态netstat（`netstat -tuln` 显示 TCP 和 UDP 的监听端口）

查看网络配置接口ifcofig（`ifconfig eth0` 显示 `eth0` 接口的信息）

### 日志查看

**cat**

```bash
查看日志打印行号
cat -n demo.log

输出重定向
cat -n demo.log > demo2.log
```

A ：相当于-vET的整合，可列出一些特殊字符而不是空白而已；
-b ：列出行号，仅针对非空白行做出行号显示，空白行不标行号；
-E ：将结尾的换行符\$显示出来；
-n ：打印出行号，连同空白行也会有行号，与-b的选项不同；
-T ：将\[tab]按键以^I显示出来 ；
-v ：列出一些看不出来的特殊字符；

tac

```bash
倒过来查看文件内容
tac demo.log
```

more

```bash
more demo.log
一页一页翻动，显示百分比

more +3 demo.log
从第三行开始输出

more +/ERROR demo.log
查找第一个ERROR出现的行，从前两行开始显示

```

less

```bash
less demo.log
空格滚动一页 回车翻动一行

less demo1.log  demo2.log
查看多个文件，输入：n切换到demo2.log ，再输入 :p 后，切换到demo.log

输入/ERROR，高亮显示关键字
```

head

```bash
head -100 demo.log
显示前100行内容

```

tail

```bash
tail -f demo.log
实时显示文件内容

tail -n 5 demo.log
显示文件末尾5行内容

```

grep

```bash
grep "ERROR" demo.log
查出含“ERROR”关键词的行

grep ITester* demo.log
查出以ITester开头的关键词的行
```

sed

sed 命令是利用脚本来处理文本文件,依照脚本的指令来处理、编辑文本文件。

```bash
sed -n '/2021-05-20 10:53:26/,/2021-05-20 10:54:28/p' demo.log>demo3.log
查出某个时间段的日志内容，并将结果保存到指定文件。

sed -n '5,7p' demo.log
查出第5到7行的内容。
```





### Linux查看系统负载

#### 1.top命令

![image-20240919120443020](/Users/shiyi/Library/Application Support/typora-user-images/image-20240919120443020.png)

第一行：

看load average：系统1分钟 5分钟 15分钟 的CPU负载信息

表示单位时间段内CPU或者的进程数，如果是单核，这个值小于1，代表系统没有负载压力



第二行：

Tasks: 108 total, 1 running, 107 sleeping, 0 stopped, 0 zombie
108 total：当前有108个任务
1 running：1个任务正在运行
107 sleeping：107个进程处于睡眠状态
0 stopped：停止的进程数
0 zombie：僵死的进程数

第三行：

0.1%us：用户态进程占用CPU时间百分比
0.2%sy：内核占用CPU时间百分比
0.2%ni：renice值为负的任务的用户态进程的CPU时间百分比。nice是优先级的意思
99.4%id：空闲CPU时间百分比
0.0%wa：等待I/O的CPU时间百分比
0.0%hi：CPU硬中断时间百分比
0.0%si：CPU软中断时间百分比

第四行解释：
KiB Mem : 3882172 total, 1079980 free, 1684652 used, 1117540 buff/cache
3882172 k total：物理内存总数
1684652k used： 使用的物理内存
1079980k free：空闲的物理内存
1117540k cached：用作缓存的内存

第五行解释：
KiB Swap: 0 total, 0 free, 0 used. 1871412 avail Mem
0k total：交换空间的总量
0k used： 使用的交换空间
0k free：空闲的交换空间
1871412k cached：缓存的交换空间

最后一行：
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
PID：进程ID
USER：进程的所有者
PR：进程的优先级
NI：nice值
VIRT：占用的虚拟内存
RES：占用的物理内存
SHR：使用的共享内存
S：进行状态 S：休眠 R运行 Z僵尸进程 N nice值为负
%CPU：占用的CPU
%MEM：占用内存
TIME+： 占用CPU的时间的累加值
COMMAND：启动命令

总结关注参数：

- **系统负载 (`load average`)**：`top` 和 `uptime` 命令中的 `load average` 参数。
- **CPU使用率**：`top`、`vmstat`、`mpstat` 命令中的 `%us`、`%sy`、`%id`、`%iowait` 参数。
- **内存使用情况**：`top` 命令中的 `Mem` （物理内存）和 `Swap`（交换空间） 行。
- **磁盘I/O**：`iostat` 命令中的 `%util`（设备利用率）、`tps`（每秒传输次数即I/O操作数）、`kB_read/s`、`kB_wrtn/s` 参数。



### 什么是交换空间？

交换空间是一种虚拟内存，通常位于硬盘上。当系统的物理内存不足时，操作系统会将一些不常用的数据从物理内存中移到交换空间，从而腾出物理内存供其他进程使用。这个过程称为“交换”或“分页”。



# 数据库SQL

[SQL常见面试题总结（1） | JavaGuide 「Java学习 + 面试指南」一份涵盖大部分 Java 程序员所需要掌握的核心知识。准备 Java 面试，首选 JavaGuide！ https://javaguide.cn/database/sql/sql-questions-01.html#过滤数据](https://javaguide.cn/database/sql/sql-questions-01.html#过滤数据 "SQL常见面试题总结（1） | JavaGuide 「Java学习 + 面试指南」一份涵盖大部分 Java 程序员所需要掌握的核心知识。准备 Java 面试，首选 JavaGuide！ https://javaguide.cn/database/sql/sql-questions-01.html#过滤数据")

### mysql基本增删改查

### 1. 创建表 (Create)

要创建一个表，你需要使用 `CREATE TABLE` 语句定义表的结构：

```sql
CREATE TABLE employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50),
    email VARCHAR(100),
    hire_date DATE
);

```

### 2. 插入数据 (Insert)

向表中插入新记录可以使用 `INSERT INTO` 语句：

```sql
INSERT INTO employees (first_name, last_name, email, hire_date)
VALUES ('John', 'Doe', 'john.doe@example.com', '2021-01-01');

```

### 3. 查询数据 (Select)

从表中检索数据使用 `SELECT` 语句：

```sql
-- 查询所有员工的信息
SELECT * FROM employees;

-- 查询特定条件下的数据
SELECT first_name, last_name
FROM employees
WHERE hire_date > '2020-01-01';

```

### 4. 更新数据 (Update)

更新已存在的数据使用 `UPDATE` 语句：

```sql
UPDATE employees
SET email = 'johndoe@newemail.com'
WHERE id = 1;

```

### 5. 删除数据 (Delete)

删除表中的行使用 `DELETE` 语句：

```sql
DELETE FROM employees
WHERE id = 1;

```

### 其他注意事项：

- 在执行任何修改数据的操作之前，请确保你有足够的权限，并且考虑是否需要备份数据。
- 使用 `LIMIT` 和 `OFFSET` 可以分页查询结果：
  ```sql
  SELECT * FROM employees LIMIT 10 OFFSET 20;
  
  ```
- 使用 `ORDER BY` 可以对查询结果排序：
  ```sql
  SELECT * FROM employees ORDER BY hire_date DESC;
  
  ```

以上就是 MySQL 中基本的增删改查操作。如果你有更具体的需求或者问题，欢迎继续提问！

### 平均成绩大于60的学生, HAVING过滤

```bash
SELECT student_id, AVG(score) AS average_score
FROM grades
GROUP BY student_id
HAVING average_score > 60;

#SELECT student_id, AVG(score) AS average_score: 选择学生ID和成绩的平均值。
#FROM grades: 指定数据来自 grades 表。
#GROUP BY student_id: 按学生ID进行分组，以便为每个学生计算平均成绩。
#HAVING average_score > 60: 过滤结果，只保留那些平均成绩大于60分的学生记录。
```

`DISTINCT` 用于返回列中的唯一不同值。

```sql
SELECT DISTINCT prod_id
FROM OrderItems
```

从 `Customers` 中检索所有的顾客名称（`cust_name`），并按从 Z 到 A 的顺序显示结果。

```sql
SELECT cust_name
FROM Customers
ORDER BY cust_name DESC

#升序
ORDER BY cust_name ASC
```

从 `Products` 表中检索产品 ID（`prod_id`）和产品名称（`prod_name`），只返回价格为 9.49 美元的产品。

```sql
SELECT prod_id, prod_name
FROM products
WHERE prod_price = 9.49
```

编写 SQL 语句，返回 `Products` 表中所有价格在 3 美元到 6 美元之间的产品的名称（`prod_name`）和价格（`prod_price`），然后按价格对结果进行排序。

```sql
SELECT prod_name, prod_price
FROM Products
WHERE prod_price BETWEEN 3 AND 6
ORDER BY prod_price
```
