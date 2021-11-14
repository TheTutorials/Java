# JDBC 访问基础

## JDBC配置

<details>
<summary>例题: 加载JDBC驱动<br/>
</summary>

``` java
Class.forName("com.mysql.cj.jdbc.Driver");
```
</details>
注意: 新版本JDBC驱动可以省略这一步

<details>
<summary>例题: 获取链接<br/>
</summary>

``` java
String url = "jdbc:mysql://localhost:3306/db?characterEncoding=UTF8";
String username = "root";
String password = "112233";
Connection connection = DriverManager.getConnection(url, username, password);
```
</details>

## 增删改查

<details>
<summary>例题: 创建表<br/>
</summary>

``` java
Connection connection = DriverManager.getConnection(url, username, password);

String sql = """
        CREATE TABLE user
        (
            id       INT PRIMARY KEY AUTO_INCREMENT,
            name     VARCHAR(20) NOT NULL,
            password VARCHAR(20) NOT NULL
        );           
        """;
Statement statement = connection.createStatement();
```
</details>

<details>
<summary>例题: 遍历结果集<br/>
</summary>

``` java
public class User {
  private int id;
  private String username;
  private String password;

  public User(int id, String username, String password) {
    this.id = id;
    this.username = username;
    this.password = password;
  }

  @Override
  public String toString() {
    return "User{" +
            "id=" + id +
            ", username='" + username + '\'' +
            ", password='" + password + '\'' +
            '}';
  }
}

public static void main(String[] args) {
    String url = "jdbc:mysql://localhost:3306/db?characterEncoding=UTF8";
    String username = "root";
    String password = "112233";
    String sql = "SELECT * FROM user";
    try (Connection connection = DriverManager.getConnection(url, username, password);
            Statement statement = connection.createStatement();
            ResultSet resultSet = statement.executeQuery(sql)) {
        List<User> users = new ArrayList<>();
        while (resultSet.next()) {
            User newUser = new User(
                    resultSet.getInt("id"),
                    resultSet.getString("name"),
                    resultSet.getString("password")
            );
            users.add(newUser);
        }
        System.out.println(users);
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```
</details>

<details>
<summary>例题: JDBC工具类<br/>
</summary>

``` java
public class JDBCUtils {
  private static final String DRIVER = "com.mysql.cj.jdbc.Driver";
  private static final String url = "jdbc:mysql://localhost:3306/db?characterEncoding=UTF-8";
  private static final String username = "root";
  private static final String password = "112233";
  private static Connection connection;
  static {
    try {
      Class.forName(DRIVER);
      connection = DriverManager.getConnection(url, username, password);
    } catch (ClassNotFoundException | SQLException e) {
      e.printStackTrace();
    }
  }

  public static Connection getConnection() {
    return connection;
  }

  public static Statement getStatement() {
    try {
      return Objects.requireNonNull(getConnection()).createStatement();
    } catch (SQLException e) {
      e.printStackTrace();
    }
    return null;
  }

  public static void close(Connection connection) {
    try {
      connection.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  public static void close(Statement statement) {
    try {
      statement.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  public static void close(ResultSet resultSet) {
    try {
      resultSet.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  public static void close(Connection connection, Statement statement) {
    close(connection);
    close(statement);
  }

  public static void close(Connection connection, Statement statement, ResultSet resultSet) {
    close(connection, statement);
    close(resultSet);
  }
}
```
</details>

<details>
<summary>例题: JDBC实现插入操作<br/>
</summary>

``` java
@Test
void testInsert() {
    String sql = """
            INSERT INTO user(id, name, password)
            VALUES (NULL, '刘德华', '112233');
            """;
    try (Statement statement = JDBCUtils.getStatement()) {
        assert statement != null;
        int effectRows = statement.executeUpdate(sql);
        System.out.println("共影响了" + effectRows + "行");
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```
</details>

<details>
<summary>例题: JDBC实现删除操作<br/>
</summary>

``` java
@Test
void testDelete() {
    String sql = """
            DELETE
            FROM user
            WHERE name = '刘德华';
            """;
    try (Statement statement = JDBCUtils.getStatement()) {
        assert statement != null;
        int effectRows = statement.executeUpdate(sql);
        System.out.println("共影响了" + effectRows + "行");
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```
</details>

<details>
<summary>例题: JDBC实现修改操作<br/>
</summary>

``` java
@Test
void testUpdate() {
    String sql = """
            UPDATE user
            SET name = '杜远超'
            WHERE id = 1;
            """;
    try (Connection connection = JDBCUtils.getConnection();
            Statement statement = JDBCUtils.getStatement()) {
        assert statement != null;
        int effectRows = statement.executeUpdate(sql);
        System.out.println("共影响了" + effectRows + "行");
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```
</details>

<details>
<summary>例题: JDBC实现查询操作<br/>
</summary>

``` java
@Test
void testQuery() {
    String sql = """
            SELECT *
            FROM user
            where id > 1;
            """;
    try (Connection connection = JDBCUtils.getConnection();
            Statement statement = JDBCUtils.getStatement();
            ResultSet resultSet = statement.executeQuery(sql)) {
        List<User> users = new ArrayList<>();
        while (resultSet.next()) {
            User user = new User(
                    resultSet.getInt("id"),
                    resultSet.getString("name"),
                    resultSet.getString("password")
            );
            users.add(user);
        }
        System.out.println(users);
    } catch (SQLException e) {
        e.printStackTrace();
    }
}
```
</details>

## SQL 注入
* 请输入用户名:`hacker`
* 请输入密码:`hacker' OR '1`
``` java
  public static void main(String[] args) {
    try (Connection connection = JDBCUtils.getConnection();
         Statement statement = JDBCUtils.getStatement()) {
      Scanner scanner = new Scanner(System.in);
      System.out.print("请输入用户名:");
      String name = scanner.nextLine();
      System.out.print("请输入密码:");
      String password = scanner.nextLine();
      String sql = "SELECT * FROM user WHERE name = '" + name + "'" + " AND " + "password = '" + password + "'";
      System.out.println(sql);
      assert statement != null;
      ResultSet resultSet = statement.executeQuery(sql);
      if (resultSet.next()) {
        System.out.println("登陆成功");
      } else {
        System.out.println("登陆失败");
      }
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
```

## PreparedStatement 预处理

<details>
<summary>例题: 使用PreparedStatement 防止SQL注入<br/>
</summary>

``` java
  public static void main(String[] args) {
    try (Connection connection = JDBCUtils.getConnection()) {
      String sql = "SELECT * FROM user WHERE name = ? AND password = ?";
      PreparedStatement preparedStatement = connection.prepareStatement(sql);
      Scanner scanner = new Scanner(System.in);
      System.out.print("请输入用户名:");
      String name = scanner.nextLine();
      System.out.print("请输入密码:");
      String password = scanner.nextLine();
      preparedStatement.setString(1, name);
      preparedStatement.setString(2, password);
      ResultSet resultSet = preparedStatement.executeQuery();
      if (resultSet.next()) {
        System.out.println("登陆成功");
      } else {
        System.out.println("登陆失败");
      }
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
```
</details>

特点
* 增加CRUD效率
* 防止SQL注入
* 预先编译SQL，提高效率

## JDBC控制事务

<details>
<summary>例题: 控制事务<br/>
</summary>

``` java
Connection connection = JDBCUtils.getConnection();
connection.setAutoCommit(false); //手动提交事务
connection.commit(); //提交事务
connection.rollback(); //回滚
```
</details>

## DBCP 数据库连接池

<details>
<summary>例题: DBCP数据库连接池工具类<br/>
</summary>

``` java
public class DBCPUtils {
  private static final String DRIVER = "com.mysql.cj.jdbc.Driver";
  private static final String URL = "jdbc:mysql://localhost:3306/db?characterEncoding=UTF-8";
  private static final String USERNAME = "root";
  private static final String PASSWORD = "112233";

  private static BasicDataSource basicDataSource = new BasicDataSource();
  static {
    basicDataSource.setDriverClassName(DRIVER);
    basicDataSource.setUrl(URL);
    basicDataSource.setUsername(USERNAME);
    basicDataSource.setPassword(PASSWORD);
  }

  public static Connection getConnection() {
    try {
      return basicDataSource.getConnection();
    } catch (SQLException e) {
      e.printStackTrace();
    }
    return null;
  }

  public static void close(Connection connection, Statement statement) {
    if (connection == null || statement == null) {
      return;
    }
    try {
      statement.close();
      connection.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  public static void close(Connection connection, Statement statement, ResultSet resultSet) {
    close(connection, statement);
    if (resultSet == null) {
      return;
    }
    try {
      resultSet.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
}
```
</details>


<details>
<summary>例题: DBCP工具类测试<br/>
</summary>

``` java
public class TestDBCPPool {
  public static void main(String[] args) {
    Connection connection = DBCPUtils.getConnection();
    Statement statement = null;
    ResultSet resultSet = null;
    try {
      assert connection != null;
      statement = connection.createStatement();
      String sql = "SELECT * FROM user";
      resultSet = statement.executeQuery(sql);
      System.out.println("编号\t姓名\t密码\n");
      while (resultSet.next()) {
        int id = resultSet.getInt("id");
        String name = resultSet.getString("name");
        String password = resultSet.getString("password");
        System.out.println(id + "\t" + name + "\t" + password);
      }
    } catch (SQLException e) {
      e.printStackTrace();
    }finally {
      DBCPUtils.close(connection, statement, resultSet);
    }
  }
}
```
</details>

## C3P0 数据库连接池

<details>
<summary>例题: c3p0-config.xml<br/>
</summary>

``` java
<c3p0-config>
    <named-config name="mysql">
        <property name="driverClass">com.mysql.cj.jdbc.Driver</property>
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/db?characterEncoding=UTF-8</property>
        <property name="user">root</property>
        <property name="password">112233</property>
        <property name="initialPoolSize">10</property>
        <property name="maxIdleTime">30</property>
        <property name="maxPoolSize">100</property>
        <property name="minPoolSize">10</property>
    </named-config>
</c3p0-config>
```
</details>


<details>
<summary>例题: C3P0工具类<br/>
</summary>

``` java
public class C3P0Utils {
  private static ComboPooledDataSource comboPooledDataSource = new ComboPooledDataSource("mysql");

  public static Connection getConnection() {
    try {
      return comboPooledDataSource.getConnection();
    } catch (SQLException e) {
      e.printStackTrace();
    }
    return null;
  }

  public static void close(Connection connection, Statement statement) {
    if (connection == null || statement == null) {
      return;
    }
    try {
      statement.close();
      connection.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  public static void close(Connection connection, Statement statement, ResultSet resultSet) {
    close(connection, statement);
    if (resultSet == null) {
      return;
    }
    try {
      resultSet.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
}
```
</details>

## Druid 数据库连接池

<details>
<summary>例题: druid.properties<br/>
</summary>

```  properties
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost:3306/db?characterEncoding=UTF-8
username=root
password=112233
initialSize=10
maxActive=10
maxWait=3000
```
</details>


<details>
<summary>例题: Druid工具类<br/>
</summary>

``` java
public class DruidUtils {
  private static DataSource dataSource;
  static {
    try {
      Properties properties = new Properties();
      properties.load(DruidUtils.class.getClassLoader().getResourceAsStream("druid.properties"));
      dataSource = DruidDataSourceFactory.createDataSource(properties);
    } catch (Exception e) {
      e.printStackTrace();
    }
  }

  public static Connection getConnection() {
    try {
      return dataSource.getConnection();
    } catch (SQLException e) {
      e.printStackTrace();
    }
    return null;
  }

  public static void close(Connection connection, Statement statement) {
    if (connection == null || statement == null) {
      return;
    }
    try {
      statement.close();
      connection.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }

  public static void close(Connection connection, Statement statement, ResultSet resultSet) {
    close(connection, statement);
    if (resultSet == null) {
      return;
    }
    try {
      resultSet.close();
    } catch (SQLException e) {
      e.printStackTrace();
    }
  }
}
```
</details>