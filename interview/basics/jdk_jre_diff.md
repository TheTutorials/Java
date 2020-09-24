# JDK 和 JRE 之间的区别

* `JDK` (Java Development Kit)

    Java 开发工具包

* `JRE` (Java Virtual Machine)

    Java 虚拟机

> 作为 Java 语言的 `SDK`，普通用户并不需要安装 `JDK` 来运行 Java 程序，而只需要安装 `JRE`（Java Runtime Environment）。而程序开发者必须安装 `JDK` 来编译、调试程序。

注意: `JDK` 中包含了 `JRE`, 并且包含了一系列开发 Java 应用程序所需要的工具，如 `javac` `java` 等, 请看下面这个目录

`JDK/bin`
```
appletviewer   jar            javac          javah          jcmd           jdeps          jjs            jps            jstack         jvisualvm      orbd           rmic           schemagen      tnameserv      wsimport
extcheck       jarsigner      javadoc        javap          jconsole       jhat           jmap           jrunscript     jstat          keytool        pack200        rmid           serialver      unpack200      xjc
idlj           java           javafxpackager javapackager   jdb            jinfo          jmc            jsadebugd      jstatd         native2ascii   policytool     rmiregistry    servertool     wsgen
```