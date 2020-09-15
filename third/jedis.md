> 订阅 [TheTutorials/Java](https://github.com/TheTutorials/Java) 学习更多 Java 相关的知识
# Java 中使用 redis
redis 在开发中非常实用，本章节讲解如何在 `Java` 中实用 `redis`, 我们主要实用的工具是 `jedis` ,如果对 `redis`不熟悉的同学可以看看看下面这个教程

[`Redis` 教程](https://github.com/TheTutorials/Redis)

## 什么是 jedis
> Jedis is a blazingly small and sane Redis java client.<br/>

Jedis 其实就是 Redis 的 Java 客户端

## 添加 `Jedis` 依赖到项目中
* 直接下载并添加 `jar` 包
    ``` java
    https://repo1.maven.org/maven2/redis/clients/jedis/3.3.0/jedis-3.3.0.jar
    ```
* `Maven` 依赖
    ``` xml
    <dependencies>
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
            <version>3.3.0</version>
            <type>jar</type>
            <scope>compile</scope>
        </dependency>
    </dependencies>
    ```
* `Grandle` 依赖
    ``` gradle
    compile group: 'redis.clients', name: 'jedis', version: '3.3.0'
    ```

## 使用 `Jedis`
* 构造函数
    ``` java
    String host = "127.0.0.1";
    int post = 6666; /* 默认端口号6379 */
    Jedis jedis = new Jedis(host, post);
    ```
* 链接 `redis`
    ``` java
    if (!jedis.isConnected()) {
        jedis.connect(); /* 如果 redis 链接断开重新链接*/
    }
    ```
* `String` 的使用
    ``` java
    jedis.set("name", "TheTutorials");
    jedis.set("age", "23");
    assert jedis.get("name").equals("TheTutorials");
    assert jedis.get("age").equals("23");
    ```
* `List` 的使用
    ``` java
    jedis.lpush("TheTutorials", "Android");
    jedis.lpush("TheTutorials", "Python");
    jedis.rpush("TheTutorials", "Java");

    assert jedis.lpop("TheTutorials").equals("Python");
    assert jedis.rpop("TheTutorials").equals("Java");
    assert jedis.llen("TheTutorials") == 1;
    ```
* 无序 `Sets` 集合
    ``` java
    String host = "127.0.0.1";
    int post = 6666; /* 默认端口号6379 */
    Jedis jedis = new Jedis(host, post);

    jedis.sadd("languages", "Python");
    jedis.sadd("languages", "C");
    jedis.sadd("languages", "Java");
    jedis.sadd("languages", "C");
    assert jedis.sismember("languages", "Python");

    /* output: [Java, Python, C] */
    System.out.println(jedis.smembers("languages").toString());
    ```