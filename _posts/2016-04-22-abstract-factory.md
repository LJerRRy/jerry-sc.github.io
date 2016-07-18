---
layout: post
title: 【JAVA设计模式】抽象工厂模式（Abstract Factory）
date: 2016-04-22
author: Jerry
header-img: img/blue.png
catalog: true
tags:
- Java
- 设计模式
---

## 定义
> 提供一个创建一系列相关或相互依赖对象的接口，而无需指定他们具体的类。

*PS：* 最后一个涉及工厂的模式了，[简单工厂模式](http://shenchao.me/2016/04/18/%E7%AE%80%E5%8D%95%E5%B7%A5%E5%8E%82%E6%A8%A1%E5%BC%8F/) 和 [工厂方法模式](http://shenchao.me/2016/04/21/%E5%B7%A5%E5%8E%82%E6%96%B9%E6%B3%95%E6%A8%A1%E5%BC%8F/) 请点此链接前往。这三个模式实在好像。

## 案例
生活中常见的一个例子，我们在组装电脑的时候，通常要选择一系列配件，比如CPU，硬盘，内存，主板等等，这里为了方便，我们只拿CPU和主板做例子。
事实上，CPU有一系列品牌，主频，针脚数目等；主板也是一样。对于装机人员来说，他只知道组装一台电脑，至于具体用什么配件，由客户说了算。虽然由客户说了算，但是仍然存在一个前提，那就是要考虑兼容性，用户选择的CPU要能够和主板相配，如果CPU针脚数和主板提供的CPU插口不兼容，那么也就无法组装成一台电脑。
接下来，我们模拟这一过程：

## 未使用模式的情况
对于客户而言，选择自己需要的CPU和主板，然后告诉装机人员自己的选择。
对于装机人员而言，只是知道CPU和主板的接口，不知道具体实现，那么可以使用简单工厂或者工厂方法模式来实现。为了方便，我们使用简单工厂模式。

{% highlight java %}
/**
 * CPU 接口
 * Created by jerry on 16-4-22.
 */
public interface CPUApi {
    /**
     * cpu具有计算功能
     */
    public void calculate();
}
{% endhighlight %}
{% highlight java %}
/**
 * 主板接口
 * Created by jerry on 16-4-22.
 */
public interface MainBoardApi {

    /**
     * 主板具有安装CPU的功能
     */
    public void installCPU();
}
{% endhighlight %}
{% highlight java %}
/**
 * Intel 的 CPU
 * Created by jerry on 16-4-22.
 */
public class IntelCPU implements CPUApi {

    /**
     * CPU 的针脚数
     */
    private int pins;

    public IntelCPU(int pins) {
        this.pins = pins;
    }

    @Override
    public void calculate() {
        System.out.println("Intel CPU 针脚数：" + pins);
    }
}
{% endhighlight %}
{% highlight java %}
/**
 * AMD 的 CPU
 * Created by jerry on 16-4-22.
 */
public class AMDCPU implements CPUApi {

    /**
     * CPU 的针脚数
     */
    private int pins;

    public AMDCPU(int pins) {
        this.pins = pins;
    }

    @Override
    public void calculate() {
        System.out.println("AMD CPU 针脚数：" + pins);
    }
}
{% endhighlight %}
{% highlight java %}
/**
 * 技嘉主板
 * Created by jerry on 16-4-22.
 */
public class GAMainBoard implements MainBoardApi {

    /**
     * CPU 插槽孔数
     */
    private int cpuHoles;

    public GAMainBoard(int cpuHoles) {
        this.cpuHoles = cpuHoles;
    }

    @Override
    public void installCPU() {
        System.out.println("技嘉主板CPU插孔数：" + cpuHoles);
    }
}
{% endhighlight %}
{% highlight java %}
/**
 * 微星主板
 * Created by jerry on 16-4-22.
 */
public class MSIMainBoard implements MainBoardApi {

    /**
     * CPU 插槽孔数
     */
    private int cpuHoles;

    public MSIMainBoard(int cpuHoles) {
        this.cpuHoles = cpuHoles;
    }

    @Override
    public void installCPU() {
        System.out.println("微星主板CPU插孔数：" + cpuHoles);
    }
}
{% endhighlight %}
创建CPU和主板的工厂类
{% highlight java %}
/**
 * 创建CPU的简单工厂
 * Created by jerry on 16-4-22.
 */
public class CPUFactory {

    public static CPUApi createCPUApi(int type) {
        CPUApi cpu = null;

        if (type == 1) {
            cpu = new IntelCPU(1156);
        } else if (type == 2) {
            cpu = new AMDCPU(939);
        }
        return cpu;
    }
}
{% endhighlight %}
{% highlight java %}
/**
 * 创建主板的简单工厂
 * Created by jerry on 16-4-22.
 */
public class MainBoardFactory {

    public static MainBoardApi createMainBoardApi(int type) {
        MainBoardApi mainBoard = null;

        if (type == 1) {
            mainBoard = new GAMainBoard(1156);
        } else if (type == 2) {
            mainBoard = new MSIMainBoard(939);
        }
        return mainBoard;
    }
}
{% endhighlight %}
{% highlight java %}
/**
 * 装机人员类,接受用户需求，组装计算机
 * Created by jerry on 16-4-22.
 */
public class ComputerEngineer {

    private CPUApi cpu;
    private MainBoardApi mainBoard;

    public void makeComputer(int cpuType, int mainBoardType) {
        //组装计算机
        initComponent(cpuType, mainBoardType);
        // 测试计算机
        // ...
    }

    /**
     * 组装计算机
     * @param cpuType 客户选择的cpu类型
     * @param mainBoardType 客户选择的主板类型
     */
    private void initComponent(int cpuType, int mainBoardType) {
        this.cpu = CPUFactory.createCPUApi(cpuType);
        this.mainBoard = MainBoardFactory.createMainBoardApi(mainBoardType);

        //运行配件是否可以用
        this.cpu.calculate();
        this.mainBoard.installCPU();
    }
}
{% endhighlight %}
客户调用：
{% highlight java %}
/**
 * 客户端调用,模拟客户
 * Created by jerry on 16-4-22.
 */
public class Client {

    public static void main(String[] args) {
        // 告诉装机人员自己的需求
        ComputerEngineer engineer = new ComputerEngineer();
        engineer.makeComputer(1,1);
    }
}
{% endhighlight %}

当我们选择Intel的CPU和技嘉的主板时，运行如下：

```
Intel CPU 针脚数：1156
技嘉主板CPU插孔数：1156
```

## 问题
似乎运行良好，但当我们选择Intel的CPU和微星的主板时，运行如下：

```
Intel CPU 针脚数：1156
微星主板CPU插孔数：939
```
发现CPU和主板的接口是不合的，也就是说，他们根本不能组装在一起的。

**所以当我们需要创建一系列相关的对象时，这时我们就需要抽象工厂模式。**
而简单工厂和工厂方法模式中，创建的对象则可以是任意的，没有任何限制。还记得吗，在简单工厂模式的介绍中，我们又称简单工厂是`万能工厂`。

## 使用模式的情况
新建抽象工厂接口，虽然有抽象二字，但是通常情况下，抽象工厂是一个接口
{% highlight java %}
/**
 * 抽象工厂接口，虽然它叫抽象工厂，但通常其不是一个抽象类，而是一个接口
 * Created by jerry on 16-4-22.
 */
public interface AbstractFactory {
    public CPUApi createCPUApi();
    public MainBoardApi createMainBoardApi();
}
```
只要实现此接口，就可以限制子类之间的关系：
```
/**
 * 装机方案一： 使用Intel 的CPU 和 技嘉的主板
 * Created by jerry on 16-4-22.
 */
public class Schema1 implements AbstractFactory {

    @Override
    public CPUApi createCPUApi() {
        return new IntelCPU(1156);
    }

    @Override
    public MainBoardApi createMainBoardApi() {
        return new GAMainBoard(1156);
    }
}
{% endhighlight %}
{% highlight java %}
/**
 * 装机方案二： 使用AMD 的CPU 和 微星的主板
 * Created by jerry on 16-4-22.
 */
public class Schema2 implements AbstractFactory {

    @Override
    public CPUApi createCPUApi() {
        return new AMDCPU(939);
    }

    @Override
    public MainBoardApi createMainBoardApi() {
        return new MSIMainBoard(939);
    }
}
{% endhighlight %}
此时告诉装机人员的是一套装机方案了，而不是任意类型，从而保证了兼容性
{% highlight java %}

/**
 * 装机人员类,接受装机方案，组装计算机
 * Created by jerry on 16-4-22.
 */
public class ComputerEnginee2 {

    private CPUApi cpu;
    private MainBoardApi mainBoard;

    public void makeComputer(AbstractFactory schema) {
        //组装计算机
        initComponent(schema);
        // 测试计算机
        // ...
    }

    /**
     * 组装计算机
     * @param cpuType 客户选择的cpu类型
     * @param mainBoardType 客户选择的主板类型
     */
    private void initComponent(AbstractFactory schema) {
        this.cpu = schema.createCPUApi();
        this.mainBoard = schema.createMainBoardApi();
        //运行配件是否可以用
        this.cpu.calculate();
        this.mainBoard.installCPU();
    }
}
{% endhighlight %}
客户端调用时，用户传入一套装机方案：
{% highlight java %}
/**
 * 客户端调用,模拟客户
 * Created by jerry on 16-4-22.
 */
public class Client {

    public static void main(String[] args) {
        // 告诉装机人员自己的需求
       /* ComputerEngineer engineer = new ComputerEngineer();
        engineer.makeComputer(1,2);*/

        ComputerEnginee2 enginee2 = new ComputerEnginee2();
        AbstractFactory schema = new Schema1();
        enginee2.makeComputer(schema);
    }
}
{% endhighlight %}
由于抽象工厂定义的一系列对象通常是相关或者相互依赖的，这些产品对象就构成了一个产品簇，也就是定义了一个产品簇。这就带来非常大的灵活性，切换一个产品簇的时候，只要提供不同的抽象工厂实现就可以了，也就是说现在是以产品簇作为一个整体被切换了。

## 总结
本质：**选择产品簇的实现**

何时使用抽象工厂模式：
1. 如果一个系统由多个产品系列中的一个来配置的时候，即可以动态切换产品簇的时候。
2. 如果要强调一系列相关产品的接口，以便联合使用它们的时候。


----------

**Github: https://github.com/jerry-sc/designPattern**

*Reference：《研磨设计模式》*


