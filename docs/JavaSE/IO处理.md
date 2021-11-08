# IO处理

## File 文件对象

<details>
<summary>例题: 构造文件对象 <br/>
</summary>

``` java
File file = new File("pom.xml");
file = new File("/root/example_dir/example_file.txt");
```
</details>

<details>
<summary>例题: getName方法 <br/>
</summary>

``` java
File file = new File("pom.xml");
assertEquals("pom.xml", file.getName());
```
</details>

<details>
<summary>例题: length方法 <br/>
</summary>

``` java
File file = new File("pom.xml");
assertTrue(file.length() >= 0); // return file bytes
```
</details>

<details>
<summary>例题: lastModified方法 <br/>
</summary>

``` java
File file = new File("pom.xml");
long lastModified = file.lastModified();
String date = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss").format(new Date(lastModified));
System.out.println(date); // 2021-08-31 09:27:21
```
</details>

<details>
<summary>例题: exists方法 <br/>
</summary>

``` java
File file = new File("pom.xml");
assertTrue(file.exists());
file = new File("pom_bk.xml");
assertFalse(file.exists());
```
</details>



<details>
<summary>例题: delete方法 <br/>
</summary>

``` java
File file = new File("pom_bk.xml");
assertTrue(file.createNewFile());
assertTrue(file.exists());
assertTrue(file.delete());
assertFalse(file.exists());
```
</details>

## 目录操作

<details>
<summary>例题: 目录创建及删除 <br/>
</summary>

``` java
File file = new File("temp");
assertTrue(file.mkdir());
assertTrue(file.delete());
assertFalse(file.exists());
```
</details>

<details>
<summary>例题: 文件过滤器过滤文件 <br/>
</summary>

``` java
File file = new File(".");
File[] files = file.listFiles((dir, name) -> name.endsWith(".xml"));
assert files != null;
assertEquals(1, files.length);
assertEquals("pom.xml", files[0].getName());
```
</details>

<details>
<summary>例题: 递归遍历所有文件(包含子文件夹的文件) <br/>
</summary>

``` java
public static void printFiles(File dir) {
    System.out.print("\t");
    if (dir.isFile()) {
        System.out.println(dir.getName());
    } else {
        System.out.println(dir.getName() + "/");
        for (File file : Objects.requireNonNull(dir.listFiles())) {
            printFiles(file);
        }
    }
}
```
</details>
