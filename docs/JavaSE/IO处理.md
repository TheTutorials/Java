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

## 文件流
* 字节流
* 字符流
* 输入流
* 输出流

## FileWriter类

<details>
<summary>例题: 写入字符A和B到文件中，分两次 <br/>
</summary>

``` java
String fileName = "example.txt";
try (Writer writer = new FileWriter(fileName)) {
    writer.write('A');
    writer.write(66); //write B
}
```
</details>


<details>
<summary>例题: 写入字符串到文件中 <br/>
</summary>

``` java
String fileName = "example.txt";
try (Writer writer = new FileWriter(fileName)) {
    writer.write("hello");
}
```
</details>

<details>
<summary>例题: 写入字符数组到文件中 <br/>
</summary>

``` java
char[] letters = {'J', 'a', 'v', 'a'};
String fileName = "example.txt";
try (Writer writer = new FileWriter(fileName)) {
    writer.write(letters);
}
```
</details>

<details>
<summary>例题: 写入字符数组的一部分内容 <br/>
</summary>

``` java
char[] letters = {'J', 'a', 'v', 'a'};
String fileName = "example.txt";
try (Writer writer = new FileWriter(fileName)) {
    writer.write(letters, 1, 2);
}
assertEquals("av", FileReaderExample.read(fileName));
Files.deleteIfExists(Paths.get(fileName));
```
</details>

## FileReader类

<details>
<summary>例题: 一次读取单个字符 <br/>
</summary>

``` java
String filename = "example.txt";
try (Writer writer = new FileWriter(filename)) {
    writer.write("Java");
}
try (Reader reader = new FileReader(filename)) {
    assertEquals('J', reader.read());
    assertEquals('a', reader.read());
    assertEquals('v', reader.read());
    assertEquals('a', reader.read());
    assertEquals(-1, reader.read());
}
Files.deleteIfExists(Paths.get(filename));
```
</details>

<details>
<summary>例题: 循环读取所有字符 <br/>
</summary>

``` java
String filename = "example.txt";
try (Writer writer = new FileWriter(filename)) {
    writer.write("Java");
}
try (Reader reader = new FileReader(filename, StandardCharsets.UTF_8)) {
    char[] letter = new char[4];
    int index = 0;
    int ch;
    while ((ch = reader.read()) != -1) {
    letter[index++] = (char)ch;
    }
    assertEquals("Java", new String(letter));
}
```
</details>

<details>
<summary>例题: 逐个读取文件里面的所有字符 <br/>
</summary>

``` java
String filename = "example.txt";
try (Writer writer = new FileWriter(filename)) {
    writer.write("I love\n");
    writer.write("Java");
}
try (Reader reader = new FileReader(filename, StandardCharsets.UTF_8)) {
    char[] buffer = new char[1024];
    int len;
    StringBuilder builder = new StringBuilder();
    while ((len = reader.read(buffer)) != -1) {
    builder.append(StringUtils.toString(buffer, 0, len));
    }
    assertEquals("I love\nJava", builder.toString());
}
```
</details>

<details>
<summary>例题: 复制文本文件 <br/>
</summary>

``` java
String filename = "pom.xml";
String newFile = "pom_bk.xml";
try (Writer writer = new FileWriter(newFile); Reader reader = new FileReader(filename)) {
    int ch;
    while ((ch = reader.read()) != -1) {
    writer.write(ch);
    }
    writer.flush();
    assertEquals(new File(filename).length(), new File(newFile).length());
}finally {
    Files.deleteIfExists(Paths.get(newFile));
}
```
</details>

## FileInputStream及FileOutputStream
<details>
<summary>例题: 复制二进制文件 <br/>
</summary>

``` java
String srcPath = "pom.xml";
String destPath = "pom.xml.bk";
try (InputStream inputStream = new FileInputStream(srcPath);
    OutputStream outputStream = new FileOutputStream(destPath)) {
    byte[] bytes = new byte[1024];
    int readBytes;
    while ((readBytes = inputStream.read(bytes)) != -1) {
    outputStream.write(bytes, 0, readBytes);
    }
    assertEquals(new File(srcPath).length(), new File(destPath).length());
}
```
</details>

## BufferedInputStream、BufferedOutputStream 缓冲流

<details>
<summary>例题: 缓冲区复制文件 <br/>
</summary>

``` java
String filename = "pom.xml";
String newFileName = "pom_bk.xml";
try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream(filename));
        BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(newFileName))) {
    byte[] buffer = new byte[1024];
    int readBytes;
    while ((readBytes = bis.read(buffer)) != -1) {
        bos.write(buffer, 0, readBytes);
        bos.flush();
    }
    assertEquals(new File(filename).length(), new File(newFileName).length());
}
```
</details>

## BufferWriter、BufferReader 文本缓冲流
<details>
<summary>例题: 拷贝文本文件 <br/>
</summary>

``` java
String filename = "pom.xml";
String newFileName = "pom_bk.xml";
try (BufferedReader bufferedReader = new BufferedReader(new FileReader(filename));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(newFileName))) {
    String line = bufferedReader.readLine();
    while (line != null) {
    String nextLine = bufferedReader.readLine();
    bufferedWriter.write(line);
    if (nextLine != null) {
        bufferedWriter.write(System.lineSeparator());
    }
    bufferedWriter.flush();
    line = nextLine;
    }
    assertEquals(new File(filename).length(), new File(newFileName).length());
}
```
</details>

## PrintStream 类
<details>
<summary>例题: 输出字符串到文件 <br/>
</summary>

``` java
String filename = "example.txt";
PrintStream printStream = new PrintStream(filename);
printStream.writeBytes("Java".getBytes(StandardCharsets.UTF_8));
assertEquals("Java", FileReaderExample.read(filename));
```
</details>

## DataOutputStream、DataInputStream 类
<details>
<summary>例题: 基本数据类型的读写 <br/>
</summary>

``` java
String filename = "example.txt";
try (DataOutputStream dataOutputStream = new DataOutputStream(new FileOutputStream(filename));
    DataInputStream dataInputStream = new DataInputStream(new FileInputStream(filename))) {
dataOutputStream.writeInt(97);
dataOutputStream.flush();

assertEquals(97, dataInputStream.readInt());
```
</details>

## RandomAccessFile

<details>
<summary>例题: 文件随机访问 <br/>
</summary>

``` java
String filename = "example.txt";
try(PrintStream printStream = new PrintStream(new FileOutputStream(filename));
    RandomAccessFile randomAccessFile = new RandomAccessFile(filename, "rw")) {
    printStream.write("Java".getBytes(StandardCharsets.UTF_8));
    printStream.flush();

    assertEquals('J', randomAccessFile.read());
    randomAccessFile.seek(2);
    assertEquals('v', randomAccessFile.read());
    randomAccessFile.write("123".getBytes(StandardCharsets.UTF_8));
    randomAccessFile.seek(0);
    assertEquals("Jav123", randomAccessFile.readLine());
}
assertTrue(Files.deleteIfExists(Paths.get(filename)));
```
</details>