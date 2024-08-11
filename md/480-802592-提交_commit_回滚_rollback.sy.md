---
show: step
version: 1.0
enable_checker: true
---

# psycopg3

## 回忆

- 上次使用了psycopg3的一句话模式


```
import psycopg

conninfo = "postgres://postgres:oeasypg@localhost:5432/oeasydb"
print(psycopg.connect(conninfo).execute("SELECT * FROM test").fetchall())
```

- 可以快速地执行sql语句
- psycopg推荐怎样的编程方式呢？🤔

### Conn 作为上下文管理器

- 原来with方式的好处
	- 是结束时会自动关闭网络连接

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20221230-1672366495124)

- 红框中的代码
	- 可以将conn作为上下文的管理器
	- 从而回滚或提交代码
	- 最终关闭网络连接



### 编写代码

```
import psycopg
conninfo = "postgres://postgres:oeasypg@localhost:5432/oeasydb"
with psycopg.connect(conninfo) as conn:
    print("connect!")
    try:
        with conn.cursor() as cur:
            cur.execute("INSERT INTO test(num,data) VALUES('111','abc');")
            cur.close()
    except BaseException:
        print("rollback")
        conn.rollback()
    else:
        print("commit")
        conn.commit()
    finally:
        conn.close()
```

- 执行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680776235468)

- 数据是否真的插入了数据库呢？

### 观察

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680776459759)

- 这是怎么一个流程呢？

### 流程

- 红色部分全都顺利执行完成
- 然后进入绿色部分
	- 输出commit
	- 并且提交

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680776534012)

- 如果让他执行一些错误代码会如何呢？

### 错误代码

- 红色部分全都顺利执行完成
- 然后进入黄色部分
	- 输出rollback
	- 并且提交

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680776739181)

- 执行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230330-1680187146502)

- 报了错误
	- 进行了回滚
- 可以把报错信息输出出来吗？

### 修改代码

```
import traceback
import psycopg
conninfo = "postgres://postgres:oeasypg@localhost:5432/oeasydb"
with psycopg.connect(conninfo) as conn:
    print("connect!")
    try:
        with conn.cursor() as cur:
            cur.execute("SOMETHING WRONG!")
            cur.close()
    except BaseException as e:
        print("rollback", e)
        traceback.print_exc()
        conn.rollback()
    else:
        print("commit")
        conn.commit()
    finally:
        conn.close()
```

- 运行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680776973637)

- 如果前面的语句SQL语句能执行
- 后面报错了
- 那前面执行的还算数吗？

### 修改代码

```
import traceback
import psycopg
conninfo = "postgres://postgres:oeasypg@localhost:5432/oeasydb"
with psycopg.connect(conninfo) as conn:
    print("connect!")
    try:
        with conn.cursor() as cur:
            cur.execute("INSERT INTO test(num,data) VALUES('222','efg');")
            cur.execute("SOMETHING WRONG!")
            cur.close()
    except BaseException as e:
        print("rollback", e)
        traceback.print_exc()
        conn.rollback()
    else:
        print("commit")
        conn.commit()
    finally:
        conn.close()
```

- 运行结果

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680777173223)

- INSERT INTO test(num,data) VALUES('222','efg');
	- 这句成功了吗？

### 查询数据

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680777237286)

- 并没有插入成功！

### rollback的含义

- 所谓rollback
	- 回滚

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680777427460)

- 在上一次回滚(rollback)或者提交(commit)之后
	- 会执行很多sql事物(transaction)
- 如果没有问题
	- 进入else子句
	- 执行确认commit
	- 全部确认

![图片描述](https://doc.shiyanlou.com/courses/uid1190679-20230406-1680777631154)

- 否则的话
	- 进入except子句
	- 执行回滚rollback
	- 全部作废

### 总结

- 这次使用了psycopg3的标准模式
	- 如果成功的话
		- 就提交
	- 否则就回滚
	- 最终关闭数据库连接
- 关于传递参数有什么推荐吗？🤔
- 下次再说！👋