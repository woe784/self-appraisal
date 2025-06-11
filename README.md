
# 数据库课程学习记录（15 周）——基于 MySQL

这是我在数据库课程中的 15 周学习日志与自我评估，全部基于 MySQL 环境。每周记录学习路径、关键知识点、个人反思与示例代码，以便回顾和展示。

---

## 第1周：MySQL 安装与环境搭建

**学习路径 / 学习内容：**

* 借助 CSDN 等博客及官方文档，下载并正确安装 MySQL Server、MySQL Workbench（或使用 DataGrip、phpMyAdmin 等工具）。
* 熟悉 MySQL Server 服务启动/停止、登录方式（命令行 `mysql -u root -p` 或图形工具）。
* 学习数据库基本概念：什么是 Data（数据）、Database（数据库）的定义与类型；DBMS（数据库管理系统）的基本类型（关系型、键值/文档型/列存储型等），及各自优缺点。
* 认识数据库与文件管理系统（File System）的区别与联系，以及文件管理系统的缺陷（一致性、并发、安全性差等）。
* 参考书籍：《Database System Concepts》《数据库系统概念》；同时思考：数据库是一门应用型技术，需要不断实践，借助 AI（如 ChatGPT）可帮助理解基础命令、出题自测、纠正错误、快速掌握。

**自我评估 / 反思：**

* 已成功安装 MySQL Server、配置连接工具，能使用命令行或 GUI 登录并执行基础操作（查看版本、创建/删除数据库）。
* 对数据库与 DBMS、关系型 vs 非关系型等概念有初步认识。
* 意识到可以借助 AI 辅助学习：例如用 AI 帮助设计练习题、给出查询示例并分析执行计划、纠正 SQL 语法与逻辑。
* 需要后续加强对 MySQL 配置（字符集、时区、用户权限管理）的熟悉度。

**示例代码（MySQL 安装无代码，此处展示登录与基础命令）：**

```bash
# 命令行登录示例
mysql -u root -p
# 查看版本
SELECT VERSION();
# 查看当前用户、当前数据库
SELECT USER(), DATABASE();
```

---

##  第2周：基础概念与 SQL 基础 —— DDL/DML 理解

**学习路径 / 学习内容：**

* “调用 API 接口完成挑战题”：可能指练习系统或作业平台通过 RESTful API 与后端数据库交互；重点在于理解前后端如何通过 API 与数据库通信。学习使用 Python/JavaScript 等调用后端 API，并在服务端对接 MySQL 执行 SQL。
* 深入掌握关键概念：`data`、`database` 的定义与类型；DBMS 各种类型及优劣；数据库的应用范围；数据库 vs 文件管理系统的区别与联系；文件管理系统的缺陷（冗余、不一致、并发控制差、事务支持弱等）。
* 学习 Data Model（数据模型）有哪些：关系模型（本学期主要）、网状、层次、面向对象等，对关系型数据库进行重点深入。
* 掌握 DDL（Data Definition Language，如 CREATE、ALTER、DROP）与 DML（Data Manipulation Language，如 INSERT、UPDATE、DELETE、SELECT）的概念与使用场景。
* 理解声明式语言特点：SQL 关注 “What” 而非 “How”。
* 通过广泛查阅资料与博客，深入理解 “关系” 在关系数据库中的含义：relation 对应表（table），tuple 对应行（row），attribute 对应列（column）。

**自我评估 / 反思：**

* 能区分数据库与文件系统，用实例理解二者区别。
* 熟悉 DDL 与 DML 基本概念，知道如何在 MySQL 中创建/修改表结构与操作数据。
* 对关系模型的基本术语（relation、tuple、schema、instance、key 等）有初步认识，需要在实践中多加巩固。
* API 调用方面对 RESTful 与数据库交互流程有概念，但需进一步练习完整流程：前端请求 → 后端 API → SQL 操作 → 返回 JSON。

**示例代码（MySQL DDL/DML 基础）：**

```sql
-- 创建数据库与表
CREATE DATABASE IF NOT EXISTS school;
USE school;

CREATE TABLE Students (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Age INT,
    EnrolledDate DATE
);

-- 插入数据
INSERT INTO Students (Name, Age, EnrolledDate)
VALUES ('Alice', 20, '2025-01-15'), ('Bob', 22, '2025-02-01');

-- 查询示例
SELECT * FROM Students WHERE Age >= 21;

-- 修改表（示例添加约束或列）
ALTER TABLE Students ADD COLUMN Email VARCHAR(255);
```

---

## 第3周：关系理论与关系代数基础

**学习路径 / 学习内容：**

* 学习关系数据库基础理论：关系（relation）是元组（tuple）的集合；关系模式（schema） vs 关系实例（instance）；attribute、domain；key（super key、candidate key、primary key）、外键（foreign key）。
* 理解元组在表中的体现：数据库表中每一行即一个元组；关系模式示例：`Instructor(id, name, dept_name, salary)`。
* 区分超码、候选码、主键；理解笛卡尔积、选择（select）、投影（project）、连接（join）、并、交、差等关系代数运算；掌握其符号和组合写法。
* 关系代数与后续 SQL 查询的联系：SQL 查询可视为关系代数运算的实现，理解代数有助于编写正确且高效的查询。
* 同时熟悉 Markdown 撰写，以便记录与展示。

**自我评估 / 反思：**

* 能结合实例区分超码、候选码、主键，并在设计表时谨慎选取。
* 理解关系代数各运算，能够手写逻辑过程并尝试将其转为 SQL 查询。
* 需要进一步在复杂场景下练习：例如多表连接后再过滤、使用投影选择所需列。
* Markdown 记录笔记更加清晰，有助于整理思路。

**示例（关系代数到 SQL 的示例思考）：**

* 关系代数：σ\_{salary > 5000}(Instructor) 相当于 SQL `SELECT * FROM Instructor WHERE salary > 5000;`
* 关系代数：π\_{name, dept\_name}(σ\_{salary > 5000}(Instructor)) 相当于 `SELECT name, dept_name FROM Instructor WHERE salary > 5000;`
* 笛卡尔积再筛选、连接示例：`Instructor ⋈_{Instructor.dept_name = Department.name} Department` 相当于：

```sql
SELECT i.name, d.location
FROM Instructor i
JOIN Department d ON i.dept_name = d.name;
```

---

##  第4周：数据类型与基本 DDL/DML 操作、NULL/UNKNOWN 语义

**学习路径 / 学习内容：**

1. MySQL 常见数据类型：整型（INT、TINYINT、BIGINT 等）、浮点/定点（FLOAT、DOUBLE、DECIMAL）、字符（CHAR、VARCHAR）、文本（TEXT）、日期时间（DATE、DATETIME、TIMESTAMP）、布尔（通常用 TINYINT(1) 实现）、其他（ENUM、SET 等）；特别理解 DECIMAL 在存储精度场景下的用途。
2. 在 CREATE TABLE 中根据业务需求设定列类型及约束：PRIMARY KEY、NOT NULL、DEFAULT、CHECK（MySQL 8.0+ 支持 CHECK 但可根据需求使用触发器代替）、唯一索引 UNIQUE 等。
3. 基本 DML 操作：INSERT、DELETE、UPDATE、SELECT；熟悉 WHERE 子句中常用比较：!=、<>、>、<、>=、<=；DISTINCT、ORDER BY + ASC/DESC；重命名列/表（SELECT ... AS ...）、别名（alias）。
4. NULL/UNKNOWN 处理：MySQL 中 NULL 逻辑，注意 `IS NULL`、`IS NOT NULL`；布尔表达式中 NULL 与 TRUE/FALSE 的组合逻辑（例如 `TRUE AND NULL` 结果为 NULL，过滤 WHERE 时 NULL 不满足 TRUE）；避免用 `=` 比较 NULL。
5. 模糊查询：LIKE 语法，通配符 `%`、`_`；转义字符 `\`；字符串拼接：MySQL 用 `CONCAT()`，在 ANSI 模式下也可用 `||` 但默认 MySQL 使用 `CONCAT`。
6. MySQL 客户端（如 mysql shell）常用命令：`SHOW DATABASES; SHOW TABLES; USE <db>; DESCRIBE <table>;`；DataGrip/Workbench 登录配置：输入 host、port、用户名、密码，连接测试；运行 .sql 脚本文件（例如 `source script.sql` 或图形界面导入）。
7. 练习 DML：创建/删除表、清空数据（DELETE、TRUNCATE）、多表查询（JOIN）。
8. 额外思考：MySQL 中与 NULL 相关的特殊逻辑：`IFNULL(expr, default)` 等；布尔值处理（MySQL 将非零当 TRUE，0 当 FALSE）。

**自我评估 / 反思：**

* 熟悉常见数据类型及其场景；能够为列选择合适类型，理解 DECIMAL 精度存储的优势。
* 能写 CREATE/DROP/ALTER 语句，并进行基础数据操作；对 NULL 语义有清晰认识，谨慎编写 WHERE 条件。
* 在 MySQL 客户端与 GUI 工具中熟练使用基本查看命令。
* 需要巩固模糊查询、字符串拼接与转义等细节，并注意不同存储引擎对数据类型支持的差异。

**示例代码（MySQL）：**

```sql
-- 创建示例表
CREATE TABLE Products (
    ProductID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Price DECIMAL(10,2) NOT NULL,
    Description TEXT,
    CreatedAt DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- 插入示例
INSERT INTO Products (Name, Price, Description)
VALUES ('Widget', 19.99, 'A useful widget'), ('Gadget', NULL, 'Unknown price');

-- NULL 逻辑示例
SELECT * FROM Products WHERE Price IS NULL;
SELECT Name, IFNULL(Price, 0) AS PriceOrZero FROM Products;

-- 模糊查询
SELECT * FROM Products WHERE Name LIKE 'W%' ESCAPE '\\';

-- 多条件查询
SELECT * FROM Products
WHERE Price BETWEEN 10 AND 50
  AND (Name LIKE '%get' OR Description LIKE '%useful%')
ORDER BY CreatedAt DESC;
```

---

## 第5周：DataGrip/MySQL Workbench 环境实践 & 聚合与高级过滤

**学习路径 / 学习内容：**

* 在 DataGrip 或 MySQL Workbench 中配置 MySQL 连接：导入已有数据库与脚本；运行 .sql 文件批量建表或插入数据；熟悉导出/导入（mysqldump、导入 CSV 等）。
* 练习基本 SQL 语句撰写并判断错误：注意 MySQL 语法差异（如 LIMIT、RAND()、字符串拼接等）。
* 进一步掌握：

  1. 不等号 `<>`、`!=`：MySQL 都支持。
  2. 模糊匹配 `%`、`_`；NULL 逻辑：IS NULL 与 IS NOT NULL，以及在 WHERE、CASE 中处理。
  3. `IFNULL(expr, default)`、`COALESCE(expr1, expr2, ...)` 用法，例如 `COALESCE(salary, 0)`。
  4. 聚集函数：`MAX()`、`MIN()`、`AVG()`、`SUM()`、`COUNT()`；理解 WHERE vs HAVING：WHERE 先过滤原始行集，不可用聚集函数；HAVING 在 GROUP BY 后进行过滤，可用聚集函数。
  5. 嵌套查询：标量子查询（single-value subquery）、多行子查询结合 `IN`、`EXISTS`；CASE ... WHEN ... THEN ... ELSE ... END 语句；比较运算符与 SOME/ANY/ALL，例如 `> SOME(...)`、`> ALL(...)`；ORDER BY RAND() LIMIT N 用法；理解性能影响。
  6. 深入练习 AVG 等聚合函数、GROUP BY 合法性判断；练习复杂查询。
* MySQL 客户端操作：进入 mysql shell 输入密码；`SHOW DATABASES`、`SHOW TABLES`；`USE university` 切换到指定库；运行查询与脚本。

**自我评估 / 反思：**

* 能够在 GUI/命令行环境中顺利连接并操作数据库，导入/导出数据文件。
* 对聚合函数与分组过滤的语法和逻辑有较好把握；理解 WHERE 与 HAVING 的区别。
* 已能较熟练编写嵌套查询和 CASE 语句，但在大型子查询或复杂逻辑时，需要关注性能优化与索引使用。
* 需要更多练习理解 RAND() LIMIT 的使用场景及其性能影响，尤其在大表时慎用。

**示例代码（MySQL）：**

```sql
USE university;

-- 聚合与过滤
SELECT dept_name, COUNT(*) AS cnt, AVG(salary) AS avg_salary
FROM Instructor
GROUP BY dept_name
HAVING AVG(salary) > 60000;

-- 嵌套查询示例: 找出薪水高于所在系平均薪水的教师
SELECT name, salary, dept_name
FROM Instructor i
WHERE salary > (
    SELECT AVG(salary) FROM Instructor WHERE dept_name = i.dept_name
);

-- CASE 语句示例
SELECT
  student_id,
  grade,
  CASE
    WHEN grade >= 90 THEN 'A'
    WHEN grade >= 80 THEN 'B'
    WHEN grade >= 70 THEN 'C'
    ELSE 'D'
  END AS grade_category
FROM Grades;

-- ORDER BY RAND() LIMIT 示例
SELECT * FROM LargeTable ORDER BY RAND() LIMIT 10;
```

---

## 第6-8周：多表查询深入 & 连接、子查询、CTE、约束、窗口函数等

**学习路径 / 学习内容：**

1. **Join 语句**：

   * 理解并练习 `INNER JOIN`、`LEFT JOIN`、`RIGHT JOIN`；MySQL 不直接支持 `FULL OUTER JOIN`，可用 `LEFT JOIN` 和 `RIGHT JOIN` 并 `UNION` 代替。
   * `NATURAL JOIN` 在 MySQL 中可使用，但需谨慎：自动匹配同名列，往往推荐显式 `JOIN ... ON`。
   * `JOIN ... USING(col)` 语法，可在列名相同时简化写法。
   * 比较 `ON` 与 `WHERE` 过滤顺序与结果：对自然连接可等价，非自然连接需理解区别。
2. **CASE 语句**：

   * 在 SELECT、ORDER BY、WHERE（MySQL 8.0+ 支持在 WHERE 中的子查询里使用 CASE）等位置使用 CASE，处理条件逻辑。
3. **子查询**：

   * 标量子查询、多行子查询；`EXISTS` vs `IN`：当子查询结果较大时，`EXISTS` 通常更优；了解性能差异。
   * CTE（WITH 语句）：MySQL 8.0+ 支持 `WITH ... AS (...)`，用于提高可读性，创建临时结果集。
4. **时间/日期类型与类型转换**：

   * MySQL 中 `DATE`、`DATETIME`、`TIMESTAMP` 等类型；函数 `STR_TO_DATE()`、`DATE_FORMAT()`、时区处理等。
5. **用户/权限与连接**：

   * 创建用户：`CREATE USER 'user'@'host' IDENTIFIED BY 'pwd';`；授权：`GRANT SELECT, INSERT ON db.table TO 'user'@'host';`；理解权限模型。
6. **自增列**：

   * MySQL 使用 `AUTO_INCREMENT` 实现主键自增；了解设置初始值、步长等。
7. **DML 进阶**：

   * `INSERT INTO ... SELECT ...`；批量插入；`UPDATE`、`DELETE`；了解事务中如何回滚。
8. **约束与触发器**：

   * 列级约束（NOT NULL、UNIQUE、CHECK）、表级约束（FOREIGN KEY）；外键级联删除/更新；触发器（TRIGGER）基础。
9. **窗口函数**（MySQL 8.0+ 支持）：

   * `RANK() OVER (PARTITION BY ... ORDER BY ...)`、`ROW_NUMBER()`、`LEAD()/LAG()` 等；在复杂分析查询中使用。
10. **练习示例**：

    * 多表连接示例、子查询与 CTE 的结合；约束的合理设计与测试；使用窗口函数进行排行或累计计算。

**自我评估 / 反思：**

* 对各种 JOIN 类型和 ON vs WHERE 过滤逻辑有较好理解，能在多表查询中正确使用。
* 对 CASE、子查询、EXISTS vs IN 有清晰认识，初步掌握何时使用 CTE 提升可读性。
* 已能创建用户并管理权限；熟悉 AUTO\_INCREMENT 使用；理解约束设计及触发器基本用法。
* 掌握窗口函数基本语法和用途，但需更多场景练习以巩固性能和正确用法。
* 时间/日期处理方面有基础认识，需注意时区与格式转换细节。

**示例代码（MySQL）：**

```sql
-- 多表连接示例
SELECT s.name, c.course_name, sc.score
FROM Students s
JOIN Scores sc ON s.ID = sc.student_id
LEFT JOIN Courses c ON sc.course_id = c.id;

-- FULL OUTER JOIN 替代示例（LEFT UNION RIGHT）
SELECT a.*, b.* 
FROM A a LEFT JOIN B b ON a.id = b.a_id
UNION
SELECT a.*, b.* 
FROM A a RIGHT JOIN B b ON a.id = b.a_id;

-- CTE 示例
WITH DeptAvg AS (
    SELECT dept_name, AVG(salary) AS avg_sal
    FROM Instructor
    GROUP BY dept_name
)
SELECT i.name, i.salary, d.avg_sal
FROM Instructor i
JOIN DeptAvg d ON i.dept_name = d.dept_name
WHERE i.salary > d.avg_sal;

-- 窗口函数示例：部门内薪资排名
SELECT 
  name, dept_name, salary,
  RANK() OVER (PARTITION BY dept_name ORDER BY salary DESC) AS dept_rank
FROM Instructor;

-- 触发器示例：在插入订单时检查库存
DELIMITER //
CREATE TRIGGER before_order_insert
BEFORE INSERT ON Orders
FOR EACH ROW
BEGIN
  DECLARE stock INT;
  SELECT quantity INTO stock FROM Products WHERE id = NEW.product_id;
  IF stock < NEW.quantity THEN
    SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = '库存不足';
  END IF;
END;
//
DELIMITER ;
```

---

##  第9周：中级 SQL 特性、视图、事务、备份与项目实践

**学习路径 / 学习内容：**

1. **视图（VIEW）**：

   * 创建视图简化复杂查询：`CREATE VIEW view_name AS SELECT ...`；了解可更新视图的限制（MySQL 对可更新视图有限制）。
   * 使用视图封装常用查询，控制访问权限。
2. **事务（Transactions）**：

   * 理解 ACID 特性；MySQL 默认存储引擎 InnoDB 支持事务。
   * 使用 `START TRANSACTION` / `BEGIN`、`COMMIT`、`ROLLBACK`；理解隔离级别（READ UNCOMMITTED、READ COMMITTED、REPEATABLE READ、SERIALIZABLE）；演示死锁、锁机制（行锁、表锁）。
3. **备份与恢复**：

   * `mysqldump` 工具：导出整个数据库或表；使用 `mysql` 命令导入；理解逻辑备份与物理备份区别。
   * 学习定期备份策略及恢复流程。
4. **性能优化初探**：

   * 通过 `EXPLAIN` / `EXPLAIN ANALYZE`（MySQL 8.0+ 支持）查看查询执行计划；理解索引使用、全表扫描、范围扫描等。
   * 使用慢查询日志（slow query log）识别性能瓶颈。
5. **项目实践：智能家居系统示例**：

   * 结合 FastAPI（Python）或其它后端框架，使用 MySQL 作为后端数据库。
   * 通过 SQLAlchemy 或 mysql-connector-python/ PyMySQL 进行连接；设计 API 路由，实现增删改查（CRUD）。
   * 在开发中与 AI 协作：说明已有技能（如 Python、SQL 基础、FastAPI）、学习目标、实现步骤；用 AI 辅助生成示例代码、调试思路、测试用例等。
   * 在 FastAPI 中启动：`uvicorn main:app --reload`，访问 `/docs` 自动生成的 Swagger UI；在界面测试 CRUD 接口；若使用前端或可视化，可将查询结果用于绘图等。
6. **其他注意事项**：

   * 环境变量配置（数据库连接字符串）；异常处理；连接池管理。
   * 开发过程中如接口未更新需重启：通常重启服务或清缓存；排查常见问题。

**自我评估 / 反思：**

* 已能创建视图并理解其更新限制；能在事务中正确使用提交/回滚；对隔离级别有初步认识。
* 掌握备份与恢复基础流程，能用 mysqldump 导出/导入测试数据。
* 初步使用 EXPLAIN 分析查询性能；理解索引对查询的影响，需深入在大数据量场景下测试。
* 在项目实践中已完成 FastAPI + MySQL 的基本 CRUD；体验到了 AI 辅助的好处：生成示例、排错思路、优化建议等。
* 需继续关注性能调优、连接池管理、安全（防注入、权限隔离）等高级话题。

**示例代码（MySQL & Python FastAPI 连接示例）：**

```python
# 使用 SQLAlchemy 连接 MySQL 示例
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, declarative_base
from sqlalchemy import Column, Integer, String

DATABASE_URL = "mysql+pymysql://user:password@localhost:3306/mydb"
engine = create_engine(DATABASE_URL, echo=True, future=True)
SessionLocal = sessionmaker(bind=engine, autocommit=False, autoflush=False)
Base = declarative_base()

class Student(Base):
    __tablename__ = "students"
    id = Column(Integer, primary_key=True, index=True)
    name = Column(String(50), nullable=False)

# 在 FastAPI 应用中使用 SessionLocal 来进行 CRUD
```

```bash
# 启动 FastAPI
uvicorn main:app --reload
```

---

##  第10周：E-R 设计与映射到关系模型

**学习路径 / 学习内容：**

* **E-R 图设计**：了解实体（Entity）、属性（Attribute）、联系（Relationship）；E-R 图绘制规范：实体用矩形（或带圆角框），联系用菱形；属性用椭圆；注意弱实体用双线矩形，弱关系用双线菱形；多对多、一对多、一对一关系标注（箭头或基数标记）。
* **基数 (Cardinality) 与参与度 (Participation)**：理解一对一、一对多、多对多的区别与实现；理解全参与 vs 部分参与；在图中正确标注。
* **主码选择**：实体集主码；联系集主码（多对多转为关联表时选择联合主键或自增主键）；弱实体主键依赖强实体主键等。
* **E-R 转关系模式**：将实体、属性映射为表；处理多对多关系生成中间表，添加外键；一对一关系可合并或用外键实现；弱实体映射注意外键与主键的组合。
* **去除冗余**：识别冗余属性或冗余关系；优化设计。
* **绘图工具**：使用 draw\.io、Lucidchart、MySQL Workbench 的模型设计器或专业工具（ERwin、Visio 等）；评估不同工具优劣。
* **实践练习**：根据示例需求画 E-R 图并转换；在 MySQL 中编写相应 CREATE TABLE 语句，添加外键、索引等。

**自我评估 / 反思：**

* 已掌握基本 E-R 图元素及绘制规范，但对一些复杂联系（如自关联、弱实体）依然需要多练习。
* 理解多对多映射、中间表设计，但在实际场景下确定主键与外键方案需谨慎。
* 需要熟悉至少一种画图工具并完成练习项目；同时在 SQL 层面实现对应表结构、外键约束、触发器（如有需要）等。
* 对冗余设计、性能考虑有初步认识，但要结合后续范式与优化内容进一步验证。

**示例代码（MySQL）：**

```sql
-- 假设 E-R 图中：Student 与 Course 是多对多，通过 Enrollment 关联
CREATE TABLE Student (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL
);

CREATE TABLE Course (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(200) NOT NULL
);

CREATE TABLE Enrollment (
    student_id INT NOT NULL,
    course_id INT NOT NULL,
    enrolled_date DATE,
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES Student(id) ON DELETE CASCADE,
    FOREIGN KEY (course_id) REFERENCES Course(id) ON DELETE CASCADE
);
```

---

##  第11-12周：范式与规范化、无损分解

**学习路径 / 学习内容：**

* **范式理论**：了解 1NF、2NF、3NF、BCNF 等范式定义；理解函数依赖（functional dependency）、平凡依赖与非平凡依赖；依赖闭包、候选键推导。
* **无损分解与依赖保持**：学习如何将大模式分解为多个小模式，既保证无损（lossless join），又尽量保持依赖（dependency preservation）；了解在某些情况下无法同时满足两者时如何权衡。
* **BCNF 判定**：模式 R 属于 BCNF 的条件：对 F+ 中所有 α→β，要么 α→β 是平凡依赖，要么 α 是超码；理解示例中的判定过程。
* **练习**：给定示例关系和函数依赖集，手动判断范式、列出候选键；进行分解示例并验证无损和依赖保持；结合 MySQL 实现分解后的表结构，迁移数据并验证查询结果一致。
* **反思**：范式理论较抽象，初学时容易混淆平凡依赖与超码判断，需要借助 AI 或同伴讨论，结合大量练习巩固；同时注意在实际项目中，过度规范化可能带来性能开销，需要根据需求权衡反规范化场景。

**自我评估 / 反思：**

* 对 1NF-3NF 理解较好，能识别部分依赖与传递依赖；对 BCNF 判断开始有思路，但在复杂依赖时需多练习。
* 已尝试用 MySQL 创建分解后表，并验证数据一致性及查询逻辑正确性。
* 理解无损分解与依赖保持的重要性，以及实际应用中可能的反规范化需求，需要在后续项目中结合性能测试进行评估。
* 继续阅读教材示例、查阅博客与论文，使用 AI 帮助理清思路，并做更多练习。

**示例（依赖分析示例无代码或简单 DDL）：**

```text
示例关系 R(A, B, C, D) 及函数依赖集 F = { A→B, B→C, C→A, A→D }。
1. 计算候选键：通过依赖闭包等方法找到所有候选键；判断是否符合 BCNF；若不符合，则分解。
2. 分解并在 MySQL 中创建相应表结构，插入示例数据，验证 JOIN 结果与原表一致。
```

---

##  第13-14周：Python 与 MySQL 连接、数据库实现原理入门

**学习路径 / 学习内容：**

1. **Python 连接 MySQL**：

   * 学习使用 `mysql-connector-python`、`PyMySQL` 或 SQLAlchemy（使用 mysql+pymysql 驱动）进行连接。
   * 环境配置：安装包（`pip install mysql-connector-python` 或 `pip install pymysql sqlalchemy`），配置连接字符串、处理凭证、安全存储（如环境变量）。
   * 基本 CRUD 示例：通过 Python 执行 SELECT、INSERT/UPDATE/DELETE，并处理异常与事务。
2. **数据库存储与实现概念**：

   * MySQL 存储引擎（InnoDB、MyISAM 等）简介：InnoDB 支持事务、行级锁、外键；MyISAM 不支持事务但读性能好。
   * InnoDB 存储结构：页（page）、插入缓冲（insert buffer）、聚簇索引（clustered index）、二级索引原理。
   * 行存储 vs 列存储：MySQL 主要行存储，列存储通常通过插件/其他系统；理解何时选择何种存储模型。
   * 元数据（metadata）查看：使用 INFORMATION\_SCHEMA 或 SHOW TABLE STATUS、SHOW INDEX 等查询表和索引信息。
3. **实践**：

   * 用 Python 创建/连接数据库、创建表、插入测试数据；在代码中实现事务提交/回滚示例。
   * 使用 SQLAlchemy ORM 或原生 SQL，设计数据模型类；在开发项目（如智能家居系统）中实际使用。
   * 了解基础的存储原理：InnoDB page layout、B+ 树索引在存储层面的组织；查询时如何在磁盘/缓存中查找数据。
4. **反思**：

   * 已掌握基本 Python-MySQL 连接与使用方法；对 SQLAlchemy ORM 有初步了解，但需进一步学习复杂查询映射与性能优化。
   * 对存储引擎 InnoDB 基本原理有兴趣，需要深入阅读官方文档或源码分析，如 page 结构、undo log、redo log、事务日志、锁机制等。
   * 已能用 Python 脚本初始化数据库环境、迁移数据并进行测试；后续可尝试自动化脚本与部署流程。

**自我评估 / 反思：**

* Python 与 MySQL 连接已较熟练，能编写脚本进行数据操作与事务管理；体验到 ORM 便利，但要关注生成 SQL 的性能。
* 对 MySQL 存储引擎原理有初步认识，后续可结合示例深入理解页面布局、索引结构、缓冲池、日志系统等。
* 需要持续强化异常处理、安全性（防注入、凭证管理）、连接池优化等生产环境相关内容。

**示例代码（Python + MySQL）：**

```python
import mysql.connector
from mysql.connector import errorcode

config = {
    'user': 'your_user',
    'password': 'your_password',
    'host': '127.0.0.1',
    'database': 'testdb',
    'raise_on_warnings': True
}
try:
    cnx = mysql.connector.connect(**config)
    cursor = cnx.cursor(dictionary=True)
    # 示例查询
    cursor.execute("SELECT * FROM students WHERE age > %s", (18,))
    for row in cursor:
        print(row)
    # 示例插入与事务
    cursor.execute("INSERT INTO students (name, age) VALUES (%s, %s)", ("Carol", 21))
    cnx.commit()
except mysql.connector.Error as err:
    print("Error:", err)
    cnx.rollback()
finally:
    cursor.close()
    cnx.close()
```

---

##  第15周：索引与查询计划、性能优化

**学习路径 / 学习内容：**

* **索引类型**：

  * B-Tree 索引（MySQL InnoDB 默认）、哈希索引（Memory 引擎支持，但 InnoDB 不支持哈希索引作主索引，仅支持自适应哈希缓存）；理解聚簇索引 vs 辅助索引（Secondary Index）。
  * 稠密索引 vs 稀疏索引：InnoDB 聚簇索引通常是稠密索引；辅助索引内部组织方式。
* **索引创建与管理**：

  * 查询现有索引：`SHOW INDEX FROM table_name;`
  * 创建索引：`CREATE INDEX idx_col ON table_name(col);`；唯一索引：`CREATE UNIQUE INDEX ...`；复合索引：`CREATE INDEX idx_multi ON table(col1, col2);`
  * 删除索引：`DROP INDEX idx_col ON table_name;`
  * 了解索引建立成本：大表创建索引时可能锁表或使用 Online DDL（MySQL 8.0 支持 Online DDL），对查询性能影响。
* **查询计划**：

  * 使用 `EXPLAIN`、`EXPLAIN ANALYZE`（MySQL 8.0+）分析查询执行计划：观察 type、possible\_keys、key、rows、extra 等列；理解全表扫描、索引扫描、范围扫描、索引合并等。
  * 通过分析执行计划发现慢查询，调整索引或重写查询。
* **示例 &性能测试**：

  * 在小表与大表对比有无索引查询时间差异；结合 Python 脚本或 MySQL 客户端测试。
  * 了解 LIMIT + ORDER BY 在大表下的影响，考虑索引覆盖或分区表设计。
* **Hash 索引 & 冲突**：

  * Memory 引擎可创建哈希索引，等值查询性能好；注意哈希冲突及适用场景；InnoDB 自适应哈希缓存非用户直接创建。
* **EXPLAIN ANALYZE 示例**：

  * 使用示例表，插入大量数据，通过 EXPLAIN ANALYZE 查看真实执行时间与行数估算差异，学习优化思路。
* **查询优化原则**：

  * 尽量避免 SELECT \*，只选取必要列；避免在 WHERE 中对列做函数操作导致索引失效；使用覆盖索引；分区或分表策略（如大数据量场景）。
  * 对于文本搜索可考虑全文索引（FULLTEXT）；对 JSON 字段可用虚拟列 + 索引。
* **反思**：

  * 已理解索引基本原理及创建方式；初步会用 EXPLAIN 分析查询计划，但需要更多实战练习来识别复杂查询瓶颈。
  * 认识到并非所有查询都适合建索引，如低基数字段；需要根据数据分布与查询模式综合评估。
  * 需进一步学习 Online DDL、分区、读写分离、复制架构对性能的影响。

**自我评估 / 反思：**

* 对 B-Tree 索引与辅助索引原理有较好理解，能创建并分析其对查询的影响；理解稠密/稀疏概念并结合 InnoDB 实践。
* 熟练使用 EXPLAIN/EXPLAIN ANALYZE 找出慢查询并进行索引或 SQL 重写优化；但对大型复杂查询需更多经验。
* 了解哈希索引在 Memory 引擎下的适用和局限；注意 InnoDB 不可直接创建哈希索引。
* 继续在实际项目或大数据集环境下测试索引策略、分区、分表、读写分离、复制等高级优化技术。

**示例代码（MySQL）：**

```sql
-- 创建示例表并插入大量数据（示例）
CREATE TABLE test_index (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100)
) ENGINE=InnoDB;

-- 批量插入（示例，实际可用脚本或 LOAD DATA INFILE）
-- 此处仅演示语法，不实际插入百万行：
INSERT INTO test_index (name)
SELECT CONCAT('user', FLOOR(RAND() * 1000000))
FROM (
    SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4
    -- 重复多次以生成大量行
) AS t1
CROSS JOIN (
    SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4
) AS t2;

-- 查看无索引查询计划
EXPLAIN SELECT * FROM test_index WHERE name = 'Alice';

-- 创建索引后查看
CREATE INDEX idx_name ON test_index(name);
EXPLAIN ANALYZE SELECT * FROM test_index WHERE name = 'Alice';

-- 查看索引信息
SHOW INDEX FROM test_index;

-- 删除索引
DROP INDEX idx_name ON test_index;
```

---

##  整体反思

* **环境搭建与工具**：从 MySQL 安装到 GUI/命令行熟练操作，掌握了数据库日常管理基本技能；了解权限管理与安全配置重要性。
* **SQL 基础与进阶**：从简单创建/查询到复杂多表关联、聚合、子查询、窗口函数，逐步建立扎实基础；理解 SQL 声明式特点及其与关系代数的关联。
* **数据库设计**：E-R 建模、范式理论与规范化、反规范化思考、索引设计与优化等，提升了设计能力；理解不同场景下设计权衡。
* **事务与并发**：掌握事务管理与隔离级别，认识并发问题与锁机制；能在实践中使用提交/回滚和检测死锁。
* **备份恢复与性能优化**：了解 mysqldump、EXPLAIN 分析及慢查询排查；初步掌握索引和查询计划分析，认识大数据量场景下的优化策略。
* **实践项目与 AI 辅助**：完成 FastAPI + MySQL CRUD 实践，体验 AI 辅助学习与开发的效率优势；理解如何与 AI 协作完成任务。
* **存储引擎与底层原理**：对 InnoDB 存储结构、索引实现、日志管理、事务机制有初步认识，为后续深入研究打下基础。
* **持续学习方向**：

  * 深入研究存储引擎源码与原理，如 InnoDB page layout、缓存管理、锁与事务日志机制。
  * 在大规模数据与高并发场景下实践分区表、分库分表、读写分离、复制、负载均衡等架构设计。
  * 安全性：防注入、权限隔离、加密、审计等。
  * 性能：在线 DDL、全文搜索、缓存（Redis 等）、查询重写优化、慢查询分析工具使用。
  * 自动化运维：备份恢复自动化、监控（Prometheus + Grafana）、报警与容量规划。

