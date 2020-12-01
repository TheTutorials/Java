# 工厂设计模式

### 前言
工厂设计模式(Factory Design Pattern)属于创建模式之一，工厂设计模式在JDK,Spring,Stuts被广泛使用
![factory-design-pattern](https://user-images.githubusercontent.com/32572119/44469074-44b7da80-a659-11e8-93f5-466432df3e8a.jpg)

当一个类或者接口有多个子类，并且基于输入返回特定的子类，此时会使用工厂设计模式。这种模式负责从客户端到工厂类的实例化。

让我们首先学习如何在java中实现工厂设计模式，然后我们将研究工厂模式的优势,我们将在JDK中看到一些工厂设计模式的使用。请注意，此模式也称为工厂方法设计模式。

### 工厂设计模式: 超类
工厂设计模式中的超类可以是接口，抽象类或普通的java类。对于我们的工厂设计模式示例，我们使用带有重写的`toString()`方法的抽象超类进行测试。

``` java
package com.github.shellhub.model;

public abstract class Computer {

	public abstract String getRAM();
	public abstract String getHDD();
	public abstract String getCPU();

	@Override
	public String toString(){
		return "RAM= "+this.getRAM()+", HDD="+this.getHDD()+", CPU="+this.getCPU();
	}
}
```

### 工厂设计模式： 子类
假设我们有两个子类`PC`和`Server`，具有以下实现。

`PC.java`
``` java
package com.github.shellhub.model;

public class PC extends Computer {

	private String ram;
	private String hdd;
	private String cpu;

	public PC(String ram, String hdd, String cpu){
		this.ram=ram;
		this.hdd=hdd;
		this.cpu=cpu;
	}
	@Override
	public String getRAM() {
		return this.ram;
	}

	@Override
	public String getHDD() {
		return this.hdd;
	}

	@Override
	public String getCPU() {
		return this.cpu;
	}

}
```
`Server.java`
``` java
package com.github.shellhub.model;

public class Server extends Computer {

	private String ram;
	private String hdd;
	private String cpu;

	public Server(String ram, String hdd, String cpu){
		this.ram=ram;
		this.hdd=hdd;
		this.cpu=cpu;
	}
	@Override
	public String getRAM() {
		return this.ram;
	}

	@Override
	public String getHDD() {
		return this.hdd;
	}

	@Override
	public String getCPU() {
		return this.cpu;
	}

}
```

### 工厂类
既然现在我们准备好了超类和子类，我们可以编写工厂类。以下是基本的实现。
``` java
package com.github.shellhub.factory;

import com.github.shellhub.model.Computer;
import com.github.shellhub.model.PC;
import com.github.shellhub.model.Server;

public class ComputerFactory {

    public static Computer getComputer(String type, String ram, String hdd, String cpu) {
        if ("PC".equalsIgnoreCase(type)) {
            return new PC(ram, hdd, cpu);
        } else if ("Server".equalsIgnoreCase(type)) {
            return new Server(ram, hdd, cpu);
        }

        return null;
    }
}
```

### 使用
这是一个简单的测试客户端程序，它使用上面的工厂设计模式实现。
``` java
package com.github.shellhub;

import com.github.shellhub.factory.ComputerFactory;
import com.github.shellhub.model.Computer;

public class TestFactory {

    public static void main(String[] args) {
        Computer pc = ComputerFactory.getComputer("pc", "2 GB", "500 GB", "2.4 GHz");
        Computer server = ComputerFactory.getComputer("server", "16 GB", "1 TB", "2.9 GHz");
        System.out.println("Factory PC Config::" + pc);
        System.out.println("Factory Server Config::" + server);
    }

}
```

Output:
``` java
Factory PC Config::RAM= 2 GB, HDD=500 GB, CPU=2.4 GHz
Factory Server Config::RAM= 16 GB, HDD=1 TB, CPU=2.9 GHz
```

### 工厂设计模式的优点
* 工厂设计模式提供了接口而不是实现的代码方法。
* 工厂模式从客户端代码中删除实际实现类的实例化。工厂模式使我们的代码更健壮，耦合更少，易于扩展。例如，我们可以轻松更改PC类实现，因为客户端程序不知道这一点。
* 工厂模式通过继承提供实现和客户端类之间的抽象。

### 工厂设计模式在JDK中的应用
1. `java.util.Calendar`，`ResourceBundle`和`NumberFormat getInstanc()`方法使用Factory模式。
2. 包装类中的`valueOf()`方法，如`Boolean`，`Integer`等。
