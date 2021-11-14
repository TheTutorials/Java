# DBUtils 使用

<details>
<summary>例题: QueryRunner 使用<br/>
</summary>

``` java
QueryRunner queryRunner = new QueryRunner();
String sql = "INSERT INTO user(id, name, password) VALUES(?, ?, ?)";
Object[] params = {4, "Jim", "abc123"};
Connection connection = DruidUtils.getConnection();
queryRunner.update(connection, sql, params);
DbUtils.closeQuietly(connection);
```
</details>

<details>
<summary>例题: ArrayHandler 使用<br/>
</summary>

``` java
QueryRunner queryRunner = new QueryRunner();
String sql = "SELECT * FROM user WHERE id = ?";
Object[] query = queryRunner.query(DruidUtils.getConnection(), sql, new ArrayHandler(), 1);
System.out.println(Arrays.toString(query));
```
</details>

<details>
<summary>例题: ArrayListHandler 使用<br/>
</summary>

``` java
QueryRunner queryRunner = new QueryRunner();
String sql = "SELECT * FROM user";
List<Object[]> query = queryRunner.query(DruidUtils.getConnection(), sql, new ArrayListHandler());
for (Object[] item : query) {
    System.out.println(Arrays.toString(item));
}
```
</details>

<details>
<summary>例题: BeanHandler 使用<br/>
</summary>

``` java
public class User {
  private int id;
  private String username;
  private String password;

  public User() {
  }

  public User(int id, String username, String password) {
    this.id = id;
    this.username = username;
    this.password = password;
  }

  public int getId() {
    return id;
  }

  public void setId(int id) {
    this.id = id;
  }

  public String getUsername() {
    return username;
  }

  public void setUsername(String username) {
    this.username = username;
  }

  public String getPassword() {
    return password;
  }

  public void setPassword(String password) {
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

QueryRunner queryRunner = new QueryRunner();
String sql = "SELECT * FROM user WHERE id = ?";
User queryUser = queryRunner.query(DruidUtils.getConnection(), sql, new BeanHandler<>(User.class), 1);
System.out.println(queryUser);
```
</details>

<details>
<summary>例题: BeanHandler 使用<br/>
</summary>

``` java
QueryRunner queryRunner = new QueryRunner(DruidUtils.getDataSource());
String sql = "SELECT * FROM user";
List<User> query = queryRunner.query(sql, new BeanListHandler<>(User.class));
System.out.println(query);
```
</details>

<details>
<summary>例题: MapHandler 使用<br/>
</summary>

``` java
QueryRunner queryRunner = new QueryRunner(DruidUtils.getDataSource());
String sql = "SELECT * FROM user WHERE id = 1";
Map<String, Object> query =queryRunner.query(sql, new MapHandler());
Set<Map.Entry<String, Object>> entries = query.entrySet();
for (Map.Entry<String, Object> entry : entries) {
    System.out.println(entry.getKey() + ":" + entry.getValue());
}
```
</details>

<details>
<summary>例题: ScalarHandler 使用<br/>
</summary>

``` java
QueryRunner queryRunner = new QueryRunner(DruidUtils.getDataSource());
String sql = "SELECT MAX(salary) FROM employee";
Double query = queryRunner.query(sql, new ScalarHandler<>());
System.out.println(query);
```
</details>  