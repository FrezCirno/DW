# oy学长介绍

1. 根据事实表, 提取维度表

例:   
    Review
    /     \
   /       \
user_dim    movie_dim

DAG-based数据开发

建立Galaxy schema

工具: Airflow, DolphinScheduler 等等

2. 为Data Market生成数据

从维度表中提取

例: 
- Top 10 电影
- Helpfulness of user

3. 开发工具

- Apache zeppelin (类似一个大数据版的jupyter notebook)

- DataGrip



文件夹目录

```
.
├─data    -----   数据文件夹
│  ├─amazon  -----   爬取网页的数据
│  ├─snap    -----   8G 的文本文件
│  ├─task1   -----   Task 1 使用的数据文件
│  └─task2   -----   Task 2 使用的数据文件
├─final   -----   **期末项目文件夹 (本次作业!!!)**
│  └─images
├─task1   -----   Task 1 代码
├─referenve  -----   (参考项目!!!)
└─task2   -----   Task 2 代码
```

数据仓库大项目：

1. 数据来源：[http://snap.stanford.edu/data/web-Movies.html (Links to an external site.)](http://snap.stanford.edu/data/web-Movies.html)

2.  项目要求：

   1.  针对电影及其周边信息，建立基于关系型数据仓库、分布式文件型数据仓库系统和图数据库的数据仓库系统，建立数据治理体系，并进行系统性能比对

      - 能够从数据来源处获取数据，进行数据预处理  -> 
      - 建立关系型数据仓库存储模型，存储数据      -> 
      - 建立分布式文件系统存储模型，存储数据      -> 
      - 建立图数据库存储模型，存储数据            -> neo4j
      - 在数据展现的界面上能够执行数据应用中的**查询**，并将在三种不同存储模型上的**执行时间**以**数值**的方式和**图表**的方式显示在界面
      - 建立数据治理体系

   2.  数据来源：数据来源自 Snap 的文本文件和 Amazon 网站，数据包括但不限于以下信息：

      - [x] 电影ID，评论用户ID，评论用户ProfileName，评论用户评价Helpfulness，评论用户Score，评论时间Time，评论结论Summary，评论结论Text
      
      - [ ] 电影演员，电影上映时间，电影风格，电影导演，电影主演，电影演员，电影版本等信息

   3. 数据应用：常见查询及统计（占总查询数目 = 80%）：

      - 按照时间进行查询及统计（例如XX年有多少电影，XX年XX月有多少电影，XX年XX季度有多少电影，周二新增多少电影等）
    
         - 数据库设计: 

            - 电影Movie表 := 电影id(asin), 电影名字, 电影上映时间-年, 电影上映时间-月, 电影上映时间-日

         - 查询语句:

            - 按年查询 : SELECT COUNT(1) WHERE (...) FROM Movie; 

            - 按年+月查询 : SELECT COUNT(1) WHERE (...) FROM Movie; 

            - 按年+季度查询 : SELECT COUNT(1) WHERE (...) FROM Movie; 

            - 按星期几查询 : SELECT COUNT(1) WHERE (...) FROM Movie; 

      - 按照电影名称进行查询及统计（例如 XX电影共有多少版本等）

         - 查询语句:

            - 按名称查询 : SELECT COUNT(1) WHERE Movie.name like '%...%' FROM Movie; 

      - 按照导演进行查询及统计（例如 XX导演共有多少电影等）

         - 数据库设计: 

            - 电影Movie表 += 电影导演

         - 查询语句:

            - 按名称查询 : SELECT COUNT(1) WHERE (Movie.director...) FROM Movie; 

      - 按照演员进行查询及统计（例如 XX演员主演多少电影，XX演员参演多少电影等）

         - 数据库设计: 

            - 演员表Actor := 演员id(自动生成), 演员名字

            - 电影演员表Actin += 电影id, 演员id, 是否是主演(true/false)

         - 查询语句:

            - 按名称查询 : SELECT COUNT(1) WHERE (Actin.actor_id...) FROM Actin; 
   
      - 按照演员和导演的关系进行查询及统计（例如经常合作的演员有哪些，经常合作的导演和演员有哪些）

         - 使用Neo4j数据库
         
         - TODO: ???

      - 按照电影类别进行查询及统计（例如 Action电影共有多少，Adventure电影共有多少等）

         - 数据库设计: 

            - 电影Movie表 += 电影题材genre

         - 查询语句:

            - 按类别查询 : SELECT COUNT(1) WHERE (Movie.genre...) FROM Movie; 

      - 按照用户评价进行查询及统计（例如用户评分3分以上的电影有哪些，用户评价中有正面评价的电影有哪些等）

         - 数据库设计: 

            - 评价Review表 += 电影题材genre

         - 查询语句:

            - 按类别查询 : SELECT COUNT(1) WHERE (Movie.genre...) FROM Movie; 


      - 按照上述条件的组合查询和统计

         - TODO: 构造拼接查询条件?

   4. 溯源查询：

      - 在过程中，我们找出了多少非电影的数据？
      - 在ETL和数据预处理中，我们找到多少哈利波特系列的电影？这个电影有多少版本？有多少网页？哈利波特第一部我们合并了多少个不同的网页？

3.  提交内容

   1. ETL脚本

   2. 数据存储设计说明文件，包括以下内容

      - E-R图

      - 逻辑存储模型和物理存储模型

      - 分布式文件系统存储模型（schema定义文件）

      - 图数据库存储模型

      - 数据表的test case

   3. 查询和统计程序

   4.  项目报告

      - 对每种存储方式结合本项目说明各自适用于处理什么查询，针对本项目在存储优化中做了什么工作，优化前后的比较结果是怎样的

      - 如何保证数据质量？哪些情况会影响数据质量？

      - 数据血缘的使用场景有哪些？

   5. 答辩ppt，说明组员信息和分配比例