## 开篇

### 开篇词： 由点及面，搭建你的 Java 并发知识网

​    你好，欢迎学习《Java 并发编程核心 78 讲》，我是讲师徐隆曦，硕士毕业于德国慕尼黑工业大学，现就职于滴滴出行，负责小桔车服驾驶安全平台开发。
扎实的理论基础，宝贵的并发实践经验

![img](http://s0.lgstatic.com/i/image2/M01/A5/3E/CgoB5l3DgLOAN9TxAADOl2eK1YA757.png)

工作期间，因为业务需要，我所开发和负责的场景大多数都是大流量和高并发的，其中有很多是对 Java 并发知识的实际应用。学习如逆旅，从小白成长为并发大神，困难重重，既然不能逃避，那么唯有改变对它的态度。

![img](http://s0.lgstatic.com/i/image2/M01/A5/3E/CgoB5l3DgLOABnQDAAIty53kLZs981.png)

从一开始面对线程池导致的 OOM 问题的不知所措，到后来可以深入剖析 JUC 源码，并精准定位、复现、修复线上的并发问题，再到现在可以应对千万级流量的业务场景，并预判和发现隐藏在其中的线程安全隐患，这期间，我走过一些弯路，踩过一些坑，也积累了很多宝贵的并发经验。

![img](http://s0.lgstatic.com/i/image2/M01/A5/5E/CgotOV3DgLOAELhuAACPIXhX2bY626.png)

此外，在对并发问题的逐个解决过程中，在系统的设计和实施过程中，我详细研读了大量的国内外经典并发书籍和资料，把涉及的代码一一落实、验证，并应用到业务里，这期间让我逐渐建立起了完善的 Java 并发知识体系。
为什么并发编程这么重要呢

随着接触和负责的系统越来越复杂，我逐渐发现，无论是对于优秀的系统设计，还是对于程序员的成长提高、职业发展，并发编程都是必须要跨过去的“坎”，而一旦你跨过了这道“坎”，便会豁然开朗，原来一切都如此简单，职业发展也会更上一层楼。

![img](http://s0.lgstatic.com/i/image2/M01/A5/3E/CgoB5l3DgLOAEMv7AABnabGYURQ993.png)

    并发已经逐渐成为基本技能

流量稍大的系统，随着数据和用户量的不断增加，并发量轻松过万，如果不使用并发编程，那么性能很快就会成为瓶颈。而随着近年来服务器 CPU 性能和核心数的不断提高，又给并发编程带来了广阔的施展拳脚的空间。可谓是有需求，同时又有资源保障，兼具天时地利。


    并发几乎是 Java 面试必考的内容

而随着互联网进入下半场，好公司对程序员的要求也水涨船高，各大互联网公司的岗位描述中，并发几乎是逃不掉的关键词，我们举几个来自拉勾网的 JD 实例。

 ![img](http://s0.lgstatic.com/i/image2/M01/A5/3E/CgoB5l3DgLOAJbveAAHrokwEb7Y378.png)

![img](http://s0.lgstatic.com/i/image2/M01/A5/5E/CgotOV3DgLOAXz5wAAG5iaGUShs303.png)

![img](http://s0.lgstatic.com/i/image2/M01/A5/5E/CgotOV3DgLOALZydAAE1RSJ3cV0452.png)

![img](http://s0.lgstatic.com/i/image2/M01/A5/3E/CgoB5l3DgLOAe7dXAAGloBkIUlw875.png)



你会发现，Java 高级工程师岗位要求中并发编程几乎成为了必须掌握的技能点，而在面经里涉及的并发编程的知识也数不胜数，本专栏各课时涉及的知识点，也正是各大厂 Java 高级工程师面试的高频考题。
如何学好并发编程

在此邀请你做一个小测试，看看目录里的问题，你能否回答全面？相信你看到问题后大部分会感觉很熟悉，但要组织答案却又模棱两可，不敢太确定，那么接下来就带你了解如何学好 Java 高并发并攻克这些难题。

![img](http://s0.lgstatic.com/i/image2/M01/A5/5E/CgotOV3DgLSAHP18AACWVfXCugg682.png)

    Java 编程是众多框架的原理和基础

无论是 Spring、tomcat 中对线程池的应用、数据库中的乐观锁思想，还是 Log4j2 对阻塞队列的应用等，无不体现着并发编程的思想，并发编程应用广泛，各大框架都和并发编程有着千丝万缕的联系。

 

并发编程就像是地基，掌握好以后，可以做到一通百通。


不过，要想学好并发编程，却不是一件容易的事，你有没有以下的感受？

 

    并发的知识太多、太杂了

![img](http://s0.lgstatic.com/i/image2/M01/A5/3E/CgoB5l3DgLSABWlnAAAr88J9c9A926.png)

常见的并发工具类数不尽数：例如，线程池、各种 Lock、synchronized 关键字、ConcurrentHashMap、CopyOnWriteArrayList、ArrayBlockingQueue、ThreadLocal、原子类、CountDownLatch、Semaphore，等等，而它们的原理又包括 CAS、AQS、Java 内存模型等等。

![img](http://s0.lgstatic.com/i/image2/M01/A5/5E/CgotOV3DgLSABkjiAADTiPdaGcM233.png)

从刚才那一长串的名字中可以看出，并发工具的数量很多，而且功能也不尽相同，不容易完全掌握。确实，并发涉及的知识点太琐碎了，大家或多或少都学习过一些并发的知识，但是总感觉一直学不完，东一榔头西一棒槌，很零散，也不知道尽头在哪里，导致学完以后，真正能记住的内容却很少。而且如果学到并发底层原理，就不只涉及 Java 语言，更涉及 JVM、JMM、操作系统、内存、CPU 指令等，令人一头雾水。

 

    不容易找到清晰易懂的学习资料

在我学习的过程中，我总是有一种感受，那就是较少有资料能够把 Java 并发编程讲得非常清楚，例如我们学习一个工具类，希望了解它的诞生背景、使用场景，用法、注意点，最后理解原理，以及它和其他工具类的联系，这一系列的内容其实都是我们需要掌握的。

 

反观现有的网络相关资料，往往水平参差不齐，真伪难辨，而且经常含有错误，如果我们先入为主地接受了错误的观点，那就得不偿失了。

![img](http://s0.lgstatic.com/i/image2/M01/A5/3E/CgoB5l3DgLSAein_AADNovsebTk325.png)

我希望本门课程可以把 Java 并发编程的这些复杂、难理解的概念，用通俗易懂、丰富的图示和例子的方式和大家分享出来，不仅知道怎么用，还能知道背后的原理。

 

利用“全局思维+单点突破”的理念，建立起并发的知识体系，同时又对各种常见的工具类有深刻认识，以后我们的知识就可以从点到线，从线到面，浑然一体。


学习了本门课，你会有以下收获

    你可以建立完整的 Java 并发知识网

通过这门课程，你可以系统地学习 Java 并发编程知识，而不再是碎片化获取，建立起知识脉络后，每一个工具类在我们心中就不再高高在上，而仅仅是我们并发知识体系中的一块块“拼图”，相信你对并发的理解会更深入一个层次。

![img](http://s0.lgstatic.com/i/image2/M01/A5/5E/CgotOV3DgLSAGmEWAADo6Lxf6ww652.png)

建立完整的知识网络后，今后即便是遇到新推出的并发工具类，也可以迅速定位到它应处的位置，并且结合已有的知识，很快就能把它掌握。

 

    你可以掌握常用的并发工具类：

课程中包含了实际生产中常用的大多数并发工具类所对应的并发知识，包括线程池、synchronized、Lock 锁，悲观锁和乐观锁、可重入锁、公平锁和非公平锁、读写锁、ConcurrentHashMap、CopyOnWriteArrayList、ThreadLocal、6 种原子类、CAS 原理、线程协作的 CountDownLatch、CyclicBarrier、Semaphore、AQS 框架、Java 内存模型、happens-before 原则、volatile 关键字、线程创建和停止的正确方法、线程的 6 种状态、如何解决死锁等问题。从用法到原理，再到面试常见问题，一次性掌握透彻。

    面试中获取 Offer 的利器

本课程的各小节，都是从高频常考的面试问题出发，首先给出对应的参考解答，然后引申出背后所关联的知识。不但能够让你回答好面试官的问题，而且还可以在面试问题的基础上，做进一步的升华，让面试官眼前一亮。

 

我还会和你分享面试经验和技巧，如何把面试官往我们的思路上“引导”，最终帮助你拿到心仪的Offer，向更高阶的岗位迈进。

 

可以说并发编程是成为 Java 高级、资深工程师的必经之路。现在几乎所有的程序都或多或少的需要用到并发和多线程，如果你平时只能接触到 CRUD 的项目，想要进一步提高技术水平；或者是长期一线，只是不断地把业务逻辑“翻译”成代码；想要跳槽加薪，面试却屡屡碰壁，那么学习并发将会帮助你突破“瓶颈”，进阶到下一个层级。

 

希望这个专栏可以让 Java 并发编程这个非常难啃的老大难问题，变得“平易近人”、“通俗易懂”、“一点就通”，希望可以让你体会到“哦，原来如此简单！”的感觉，体会到久违的学习的快乐。



## 线程基础升华 

### 第01讲：为何说只有 1 种实现线程的方法？

在本课时我们主要学习为什么说本质上只有一种实现线程的方式？实现 Runnable 接口究竟比继承 Thread 类实现线程好在哪里？

实现线程是并发编程中基础中的基础，因为我们必须要先实现多线程，才可以继续后续的一系列操作。所以本课时就先从并发编程的基础如何实现线程开始讲起，希望你能够夯实基础，虽然实现线程看似简单、基础，但实际上却暗藏玄机。首先，我们来看下为什么说本质上实现线程只有一种方式？

实现线程的方式到底有几种？大部分人会说有 2 种、3 种或是 4 种，很少有人会说有 1 种。我们接下来看看它们具体指什么？2 种实现方式的描述是最基本的，也是最为大家熟知的，我们就先来看看 2 种线程实现方式的源码。
实现 Runnable 接口

复制
public class RunnableThread implements Runnable {

    @Override
    public void run() {
        System.out.println('用实现Runnable接口实现线程');
    }
}

第 1 种方式是通过实现 Runnable 接口实现多线程，如代码所示，首先通过 RunnableThread 类实现 Runnable 接口，然后重写 run() 方法，之后只需要把这个实现了 run() 方法的实例传到 Thread 类中就可以实现多线程。
继承 Thread 类

复制
public class ExtendsThread extends Thread {

    @Override
    public void run() {
        System.out.println('用Thread类实现线程');
    }
}

第 2 种方式是继承 Thread 类，如代码所示，与第 1 种方式不同的是它没有实现接口，而是继承 Thread 类，并重写了其中的 run() 方法。相信上面这两种方式你一定非常熟悉，并且经常在工作中使用它们。
线程池创建线程

那么为什么说还有第 3 种或第 4 种方式呢？我们先来看看第 3 种方式：通过线程池创建线程。线程池确实实现了多线程，比如我们给线程池的线程数量设置成 10，那么就会有 10 个子线程来为我们工作，接下来，我们深入解析线程池中的源码，来看看线程池是怎么实现线程的？

复制
static class DefaultThreadFactory implements ThreadFactory {

    DefaultThreadFactory() {
        SecurityManager s = System.getSecurityManager();
        group = (s != null) ? s.getThreadGroup() :
            Thread.currentThread().getThreadGroup();
        namePrefix = "pool-" +
            poolNumber.getAndIncrement() +
            "-thread-";
    }


    public Thread newThread(Runnable r) {
        Thread t = new Thread(group, r,
                    namePrefix + threadNumber.getAndIncrement(),
0);

        if (t.isDaemon())
            t.setDaemon(false);
        if (t.getPriority() != Thread.NORM_PRIORITY)
            t.setPriority(Thread.NORM_PRIORITY);
        return t;
    }
}

对于线程池而言，本质上是通过线程工厂创建线程的，默认采用 DefaultThreadFactory ，它会给线程池创建的线程设置一些默认值，比如：线程的名字、是否是守护线程，以及线程的优先级等。但是无论怎么设置这些属性，最终它还是通过 new Thread() 创建线程的 ，只不过这里的构造函数传入的参数要多一些，由此可以看出通过线程池创建线程并没有脱离最开始的那两种基本的创建方式，因为本质上还是通过 new Thread() 实现的。

在面试中，如果你只是知道这种方式可以创建线程但不了解其背后的实现原理，就会在面试的过程中举步维艰，想更好的表现自己却给自己挖了“坑”。

所以我们在回答线程实现的问题时，描述完前两种方式，可以进一步引申说“我还知道线程池和Callable 也是可以创建线程的，但是它们本质上也是通过前两种基本方式实现的线程创建。”这样的回答会成为面试中的加分项。然后面试官大概率会追问线程池的构成及原理，这部分内容会在后面的课时中详细分析。
有返回值的 Callable 创建线程

复制
class CallableTask implements Callable<Integer> {

    @Override
    public Integer call() throws Exception {
        return new Random().nextInt();
    }
}

//创建线程池
ExecutorService service = Executors.newFixedThreadPool(10);
//提交任务，并用 Future提交返回结果
Future<Integer> future = service.submit(new CallableTask());

第 4 种线程创建方式是通过有返回值的 Callable 创建线程，Runnable 创建线程是无返回值的，而 Callable 和与之相关的 Future、FutureTask，它们可以把线程执行的结果作为返回值返回，如代码所示，实现了 Callable 接口，并且给它的泛型设置成 Integer，然后它会返回一个随机数。

但是，无论是 Callable 还是 FutureTask，它们首先和 Runnable 一样，都是一个任务，是需要被执行的，而不是说它们本身就是线程。它们可以放到线程池中执行，如代码所示， submit() 方法把任务放到线程池中，并由线程池创建线程，不管用什么方法，最终都是靠线程来执行的，而子线程的创建方式仍脱离不了最开始讲的两种基本方式，也就是实现 Runnable 接口和继承 Thread 类。
其他创建方式
定时器 Timer

复制
class TimerThread extends Thread {
//具体实现
}

讲到这里你可能会说，我还知道一些其他的实现线程的方式。比如，定时器也可以实现线程，如果新建一个 Timer，令其每隔 10 秒或设置两个小时之后，执行一些任务，那么这时它确实也创建了线程并执行了任务，但如果我们深入分析定时器的源码会发现，本质上它还是会有一个继承自 Thread 类的 TimerThread，所以定时器创建线程最后又绕回到最开始说的两种方式。
其他方法

复制
/**
 *描述：匿名内部类创建线程
 */
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println(Thread.currentThread().getName());
    }
}).start();

}
}

或许你还会说，我还知道一些其他方式，比如匿名内部类或 lambda 表达式方式，实际上，匿名内部类或 lambda 表达式创建线程，它们仅仅是在语法层面上实现了线程，并不能把它归结于实现多线程的方式，如匿名内部类实现线程的代码所示，它仅仅是用一个匿名内部类把需要传入的 Runnable 给实例出来。

复制
new Thread(() -> System.out.println(Thread.currentThread().getName())).start();
}

我们再来看下 lambda 表达式方式。如代码所示，最终它们依然符合最开始所说的那两种实现线程的方式。
实现线程只有一种方式

关于这个问题，我们先不聚焦为什么说创建线程只有一种方式，先认为有两种创建线程的方式，而其他的创建方式，比如线程池或是定时器，它们仅仅是在 new Thread() 外做了一层封装，如果我们把这些都叫作一种新的方式，那么创建线程的方式便会千变万化、层出不穷，比如 JDK 更新了，它可能会多出几个类，会把 new Thread() 重新封装，表面上看又会是一种新的实现线程的方式，透过现象看本质，打开封装后，会发现它们最终都是基于 Runnable 接口或继承 Thread 类实现的。

接下来，我们进行更深层次的探讨，为什么说这两种方式本质上是一种呢？

复制

```java
@Override
public void run() {
    if (target != null) {
        target.run();
    }
}
```

首先，启动线程需要调用 start() 方法，而 start() 方法最终还会调用 run() 方法，我们先来看看第一种方式中 run() 方法究竟是怎么实现的，可以看出 run() 方法的代码非常短小精悍，第 1 行代码 if (target != null) ，判断 target 是否等于 null，如果不等于 null，就执行第 2 行代码 target.run()，而 target 实际上就是一个 Runnable，即使用 Runnable 接口实现线程时传给Thread类的对象。

然后，我们来看第二种方式，也就是继承 Thread 方式，实际上，继承 Thread 类之后，会把上述的 run() 方法重写，重写后 run() 方法里直接就是所需要执行的任务，但它最终还是需要调用 thread.start() 方法来启动线程，而 start() 方法最终也会调用这个已经被重写的 run() 方法来执行它的任务，这时我们就可以彻底明白了，事实上创建线程只有一种方式，就是构造一个 Thread 类，这是创建线程的唯一方式。

我们上面已经了解了两种创建线程方式本质上是一样的，它们的不同点仅仅在于实现线程运行内容的不同，那么运行内容来自于哪里呢？

运行内容主要来自于两个地方，要么来自于 target，要么来自于重写的 run() 方法，在此基础上我们进行拓展，可以这样描述：本质上，实现线程只有一种方式，而要想实现线程执行的内容，却有两种方式，也就是可以通过 实现 Runnable 接口的方式，或是继承 Thread 类重写 run() 方法的方式，把我们想要执行的代码传入，让线程去执行，在此基础上，如果我们还想有更多实现线程的方式，比如线程池和 Timer 定时器，只需要在此基础上进行封装即可。
实现 Runnable 接口比继承 Thread 类实现线程要好

下面我们来对刚才说的两种实现线程内容的方式进行对比，也就是为什么说实现 Runnable 接口比继承 Thread 类实现线程要好？好在哪里呢？

首先，我们从代码的架构考虑，实际上，Runnable 里只有一个 run() 方法，它定义了需要执行的内容，在这种情况下，实现了 Runnable 与 Thread 类的解耦，Thread 类负责线程启动和属性设置等内容，权责分明。

第二点就是在某些情况下可以提高性能，使用继承 Thread 类方式，每次执行一次任务，都需要新建一个独立的线程，执行完任务后线程走到生命周期的尽头被销毁，如果还想执行这个任务，就必须再新建一个继承了 Thread 类的类，如果此时执行的内容比较少，比如只是在 run() 方法里简单打印一行文字，那么它所带来的开销并不大，相比于整个线程从开始创建到执行完毕被销毁，这一系列的操作比 run() 方法打印文字本身带来的开销要大得多，相当于捡了芝麻丢了西瓜，得不偿失。如果我们使用实现 Runnable 接口的方式，就可以把任务直接传入线程池，使用一些固定的线程来完成任务，不需要每次新建销毁线程，大大降低了性能开销。

第三点好处在于 Java 语言不支持双继承，如果我们的类一旦继承了 Thread 类，那么它后续就没有办法再继承其他的类，这样一来，如果未来这个类需要继承其他类实现一些功能上的拓展，它就没有办法做到了，相当于限制了代码未来的可拓展性。

综上所述，我们应该优先选择通过实现 Runnable 接口的方式来创建线程。



### 第02讲：如何正确停止线程？为什么 volatile 标记位的停止方法是错误的？

在本课时我们主要学习如何正确停止一个线程？以及为什么用 volatile 标记位的停止方法是错误的？

首先，我们来复习如何启动一个线程，想要启动线程需要调用 Thread 类的 start() 方法，并在 run() 方法中定义需要执行的任务。启动一个线程非常简单，但如果想要正确停止它就没那么容易了。
原理介绍

通常情况下，我们不会手动停止一个线程，而是允许线程运行到结束，然后让它自然停止。但是依然会有许多特殊的情况需要我们提前停止线程，比如：用户突然关闭程序，或程序运行出错重启等。

在这种情况下，即将停止的线程在很多业务场景下仍然很有价值。尤其是我们想写一个健壮性很好，能够安全应对各种场景的程序时，正确停止线程就显得格外重要。但是Java 并没有提供简单易用，能够直接安全停止线程的能力。
为什么不强制停止？而是通知、协作

对于 Java 而言，最正确的停止线程的方式是使用 interrupt。但 interrupt 仅仅起到通知被停止线程的作用。而对于被停止的线程而言，它拥有完全的自主权，它既可以选择立即停止，也可以选择一段时间后停止，也可以选择压根不停止。那么为什么 Java 不提供强制停止线程的能力呢？

事实上，Java 希望程序间能够相互通知、相互协作地管理线程，因为如果不了解对方正在做的工作，贸然强制停止线程就可能会造成一些安全的问题，为了避免造成问题就需要给对方一定的时间来整理收尾工作。比如：线程正在写入一个文件，这时收到终止信号，它就需要根据自身业务判断，是选择立即停止，还是将整个文件写入成功后停止，而如果选择立即停止就可能造成数据不完整，不管是中断命令发起者，还是接收者都不希望数据出现问题。
如何用 interrupt 停止线程

复制
while (!Thread.currentThread().islnterrupted() && more work to do) {
    do more work
}

明白 Java 停止线程的设计原则之后，我们看看如何用代码实现停止线程的逻辑。我们一旦调用某个线程的 interrupt() 之后，这个线程的中断标记位就会被设置成 true。每个线程都有这样的标记位，当线程执行时，应该定期检查这个标记位，如果标记位被设置成 true，就说明有程序想终止该线程。回到源码，可以看到在 while 循环体判断语句中，首先通过 Thread.currentThread().isInterrupt() 判断线程是否被中断，随后检查是否还有工作要做。&& 逻辑表示只有当两个判断条件同时满足的情况下，才会去执行下面的工作。

我们再看看具体例子。

复制
public class StopThread implements Runnable {

    @Override
    public void run() {
        int count = 0;
        while (!Thread.currentThread().isInterrupted() && count < 1000) {
            System.out.println("count = " + count++);
        }
    }
     
    public static void main(String[] args) throws InterruptedException {
        Thread thread = new Thread(new StopThread());
        thread.start();
        Thread.sleep(5);
        thread.interrupt();
    }
}

在 StopThread 类的 run() 方法中，首先判断线程是否被中断，然后判断 count 值是否小于 1000。这个线程的工作内容很简单，就是打印 0~999 的数字，每打印一个数字 count 值加 1，可以看到，线程会在每次循环开始之前，检查是否被中断了。接下来在 main 函数中会启动该线程，然后休眠 5 毫秒后立刻中断线程，该线程会检测到中断信号，于是在还没打印完1000个数的时候就会停下来，这种就属于通过 interrupt 正确停止线程的情况。
sleep 期间能否感受到中断

复制
Runnable runnable = () -> {
    int num = 0;
    try {
        while (!Thread.currentThread().isInterrupted() && 
        num <= 1000) {
            System.out.println(num);
            num++;
            Thread.sleep(1000000);
        }
    } catch (InterruptedException e) {
        e.printStackTrace();
    }
};

那么我们考虑一种特殊情况，改写上面的代码，如果线程在执行任务期间有休眠需求，也就是每打印一个数字，就进入一次 sleep ，而此时将 Thread.sleep() 的休眠时间设置为 1000 秒钟。

复制
public class StopDuringSleep {

    public static void main(String[] args) throws InterruptedException {
        Runnable runnable = () -> {
            int num = 0;
            try {
                while (!Thread.currentThread().isInterrupted() && num <= 1000) {
                    System.out.println(num);
                    num++;
                    Thread.sleep(1000000);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        };
        Thread thread = new Thread(runnable);
        thread.start();
        Thread.sleep(5);
        thread.interrupt();
    }
}

主线程休眠 5 毫秒后，通知子线程中断，此时子线程仍在执行 sleep 语句，处于休眠中。那么就需要考虑一点，在休眠中的线程是否能够感受到中断通知呢？是否需要等到休眠结束后才能中断线程呢？如果是这样，就会带来严重的问题，因为响应中断太不及时了。正因为如此，Java 设计者在设计之初就考虑到了这一点。

如果 sleep、wait 等可以让线程进入阻塞的方法使线程休眠了，而处于休眠中的线程被中断，那么线程是可以感受到中断信号的，并且会抛出一个 InterruptedException 异常，同时清除中断信号，将中断标记位设置成 false。这样一来就不用担心长时间休眠中线程感受不到中断了，因为即便线程还在休眠，仍然能够响应中断通知，并抛出异常。
两种最佳处理方式

在实际开发中肯定是团队协作的，不同的人负责编写不同的方法，然后相互调用来实现整个业务的逻辑。那么如果我们负责编写的方法需要被别人调用，同时我们的方法内调用了 sleep 或者 wait 等能响应中断的方法时，仅仅 catch 住异常是不够的。

复制
void subTas() {
    try {
        Thread.sleep(1000);
    } catch (InterruptedException e) {
        // 在这里不处理该异常是非常不好的
    }
}

我们可以在方法中使用 try/catch 或在方法签名中声明 throws  InterruptedException。
方法签名抛异常，run() 强制 try/catch

我们先来看下 try/catch 的处理逻辑。如上面的代码所示，catch 语句块里代码是空的，它并没有进行任何处理。假设线程执行到这个方法，并且正在 sleep，此时有线程发送 interrupt 通知试图中断线程，就会立即抛出异常，并清除中断信号。抛出的异常被 catch 语句块捕捉。

但是，捕捉到异常的 catch 没有进行任何处理逻辑，相当于把中断信号给隐藏了，这样做是非常不合理的，那么究竟应该怎么处理呢？首先，可以选择在方法签名中抛出异常。

复制
void subTask2() throws InterruptedException {
    Thread.sleep(1000);
}

正如代码所示，要求每一个方法的调用方有义务去处理异常。调用方要不使用 try/catch 并在 catch 中正确处理异常，要不将异常声明到方法签名中。如果每层逻辑都遵守规范，便可以将中断信号层层传递到顶层，最终让 run() 方法可以捕获到异常。而对于 run() 方法而言，它本身没有抛出 checkedException 的能力，只能通过 try/catch 来处理异常。层层传递异常的逻辑保障了异常不会被遗漏，而对 run() 方法而言，就可以根据不同的业务逻辑来进行相应的处理。
再次中断

复制
private void reInterrupt() {
    try {
        Thread.sleep(2000);
    } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
        e.printStackTrace();
    }
}

除了刚才推荐的将异常声明到方法签名中的方式外，还可以在 catch 语句中再次中断线程。如代码所示，需要在 catch 语句块中调用 Thread.currentThread().interrupt() 函数。因为如果线程在休眠期间被中断，那么会自动清除中断信号。如果这时手动添加中断信号，中断信号依然可以被捕捉到。这样后续执行的方法依然可以检测到这里发生过中断，可以做出相应的处理，整个线程可以正常退出。

我们需要注意，我们在实际开发中不能盲目吞掉中断，如果不在方法签名中声明，也不在 catch 语句块中再次恢复中断，而是在 catch 中不作处理，我们称这种行为是“屏蔽了中断请求”。如果我们盲目地屏蔽了中断请求，会导致中断信号被完全忽略，最终导致线程无法正确停止。
为什么用 volatile 标记位的停止方法是错误的

下面我们来看一看本课时的第二个问题，为什么用 volatile 标记位的停止方法是错误的？
错误的停止方法

首先，我们来看几种停止线程的错误方法。比如 stop()，suspend() 和 resume()，这些方法已经被 Java 直接标记为 @Deprecated。如果再调用这些方法，IDE 会友好地提示，我们不应该再使用它们了。但为什么它们不能使用了呢？是因为 stop() 会直接把线程停止，这样就没有给线程足够的时间来处理想要在停止前保存数据的逻辑，任务戛然而止，会导致出现数据完整性等问题。

而对于 suspend() 和 resume() 而言，它们的问题在于如果线程调用 suspend()，它并不会释放锁，就开始进入休眠，但此时有可能仍持有锁，这样就容易导致死锁问题，因为这把锁在线程被 resume() 之前，是不会被释放的。

假设线程 A 调用了 suspend() 方法让线程 B 挂起，线程 B 进入休眠，而线程 B 又刚好持有一把锁，此时假设线程 A 想访问线程 B 持有的锁，但线程 B 并没有释放锁就进入休眠等待唤醒，而对于线程 A 而言，又不会唤醒线程 B，除非拿到锁，这就造成了死锁问题。

正是因为有这样的风险，所以 suspend() 和 resume() 组合使用的方法也被废弃了。那么接下来我们来看看，为什么用 volatile 标记位的停止方法也是错误的？
volatile 修饰标记位适用的场景

复制
public class VolatileCanStop implements Runnable {

    private volatile boolean canceled = false;
     
    @Override
    public void run() {
        int num = 0;
        try {
            while (!canceled && num <= 1000000) {
                if (num % 10 == 0) {
                    System.out.println(num + "是10的倍数。");
                }
                num++;
                Thread.sleep(1);
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
     
    public static void main(String[] args) throws InterruptedException {
        VolatileCanStop r = new VolatileCanStop();
        Thread thread = new Thread(r);
        thread.start();
        Thread.sleep(3000);
        r.canceled = true;
    }
}

什么场景下 volatile 修饰标记位可以让线程正常停止呢？如代码所示，声明了一个叫作 VolatileStopThread 的类， 它实现了 Runnable 接口，然后在 run() 中进行 while 循环，在循环体中又进行了两层判断，首先判断 canceled 变量的值，canceled 变量是一个被 volatile 修饰的初始值为 false 的布尔值，当该值变为 true 时，while 跳出循环，while 的第二个判断条件是 num 值小于1000000（一百万），在while 循环体里，只要是 10 的倍数就打印出来，然后 num++。

接下来，首先启动线程，然后经过 3 秒钟的时间，把用 volatile 修饰的布尔值的标记位设置成 true，这样，正在运行的线程就会在下一次 while 循环中判断出 canceled 的值已经变成 true 了，这样就不再满足 while 的判断条件，跳出整个 while 循环，线程就停止了，这种情况是演示 volatile 修饰的标记位可以正常工作的情况，但是如果我们说某个方法是正确的，那么它应该不仅仅是在一种情况下适用，而在其他情况下也应该是适用的。
volatile 修饰标记位不适用的场景

接下来我们就用一个生产者/消费者模式的案例来演示为什么说  volatile 标记位的停止方法是不完美的。

复制
class Producer implements Runnable {
    public volatile boolean canceled = false;
    BlockingQueue storage;
    public Producer(BlockingQueue storage) {
        this.storage = storage;
    }

    @Override
    public void run() {
        int num = 0;
        try {
            while (num <= 100000 && !canceled) {
                if (num % 50 == 0) {
                    storage.put(num);
                    System.out.println(num + "是50的倍数,被放到仓库中了。");
                }
                num++;
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        } finally {
            System.out.println("生产者结束运行");
        }
    }
}

首先，声明了一个生产者 Producer，通过 volatile 标记的初始值为 false 的布尔值 canceled 来停止线程。而在 run() 方法中，while 的判断语句是 num 是否小于 100000 及 canceled 是否被标记。while 循环体中判断 num 如果是 50 的倍数就放到 storage 仓库中，storage 是生产者与消费者之间进行通信的存储器，当 num 大于 100000 或被通知停止时，会跳出 while 循环并执行 finally 语句块，告诉大家“生产者结束运行”。

复制
class Consumer {
    BlockingQueue storage;
    public Consumer(BlockingQueue storage) {
        this.storage = storage;
    }
    public boolean needMoreNums() {
        if (Math.random() > 0.97) {
            return false;
        }
        return true;
    }
}

而对于消费者 Consumer，它与生产者共用同一个仓库 storage，并且在方法内通过 needMoreNums() 方法判断是否需要继续使用更多的数字，刚才生产者生产了一些 50 的倍数供消费者使用，消费者是否继续使用数字的判断条件是产生一个随机数并与 0.97 进行比较，大于 0.97 就不再继续使用数字。

复制
public static void main(String[] args) throws InterruptedException {
        ArrayBlockingQueue storage = new ArrayBlockingQueue(8);

        Producer producer = new Producer(storage);
        Thread producerThread = new Thread(producer);
        producerThread.start();
        Thread.sleep(500);
    
        Consumer consumer = new Consumer(storage);
        while (consumer.needMoreNums()) {
            System.out.println(consumer.storage.take() + "被消费了");
            Thread.sleep(100);
        }
        System.out.println("消费者不需要更多数据了。");
    
        //一旦消费不需要更多数据了，我们应该让生产者也停下来，但是实际情况却停不下来
        producer.canceled = true;
        System.out.println(producer.canceled);
    }
}

下面来看下 main 函数，首先创建了生产者/消费者共用的仓库 BlockingQueue storage，仓库容量是 8，并且建立生产者并将生产者放入线程后启动线程，启动后进行 500 毫秒的休眠，休眠时间保障生产者有足够的时间把仓库塞满，而仓库达到容量后就不会再继续往里塞，这时生产者会阻塞，500 毫秒后消费者也被创建出来，并判断是否需要使用更多的数字，然后每次消费后休眠 100 毫秒，这样的业务逻辑是有可能出现在实际生产中的。

当消费者不再需要数据，就会将 canceled 的标记位设置为 true，理论上此时生产者会跳出 while 循环，并打印输出“生产者运行结束”。

然而结果却不是我们想象的那样，尽管已经把 canceled 设置成 true，但生产者仍然没有停止，这是因为在这种情况下，生产者在执行 storage.put(num) 时发生阻塞，在它被叫醒之前是没有办法进入下一次循环判断 canceled 的值的，所以在这种情况下用 volatile 是没有办法让生产者停下来的，相反如果用 interrupt 语句来中断，即使生产者处于阻塞状态，仍然能够感受到中断信号，并做响应处理。
总结

好了，本课时的内容就全部讲完了，我们来总结下学到了什么，首先学习了如何正确停止线程，其次是掌握了为什么说 volatile 修饰标记位停止方法是错误的。

如果我们在面试中被问到“你知不知道如何正确停止线程”这样的问题，我想你一定可以完美地回答了，首先，从原理上讲应该用 interrupt 来请求中断，而不是强制停止，因为这样可以避免数据错乱，也可以让线程有时间结束收尾工作。

如果我们是子方法的编写者，遇到了 interruptedException，应该如何处理呢？

我们可以把异常声明在方法中，以便顶层方法可以感知捕获到异常，或者也可以在 catch 中再次声明中断，这样下次循环也可以感知中断，所以要想正确停止线程就要求我们停止方，被停止方，子方法的编写者相互配合，大家都按照一定的规范来编写代码，就可以正确地停止线程了。

最后我们再来看下有哪些方法是不够好的，比如说已经被舍弃的 stop()、suspend() 和 resume()，它们由于有很大的安全风险比如死锁风险而被舍弃，而 volatile 这种方法在某些特殊的情况下，比如线程被长时间阻塞的情况，就无法及时感受中断，所以 volatile 是不够全面的停止线程的方法。



### 第03讲：线程是如何在 6 种状态之间转换的？

本课时我们主要学习线程是如何在 6 种状态之间转换的。
线程的 6 种状态

就像生物从出生到长大、最终死亡的过程一样，线程也有自己的生命周期，在 Java 中线程的生命周期中一共有 6 种状态。

    New（新创建）
    
    Runnable（可运行）
    
    Blocked（被阻塞）
    
    Waiting（等待）
    
    Timed Waiting（计时等待）
    
    Terminated（被终止）

如果想要确定线程当前的状态，可以通过 getState() 方法，并且线程在任何时刻只可能处于 1 种状态。
 New 新创建

![img](http://s0.lgstatic.com/i/image2/M01/A7/06/CgotOV3JD1mAHFh3AAEPE-QJBow134.png)       

下面我们逐个介绍线程的 6 种状态，如图所示，首先来看下左上角的 New 状态。

New 表示线程被创建但尚未启动的状态：当我们用 new Thread() 新建一个线程时，如果线程没有开始运行 start() 方法，所以也没有开始执行 run() 方法里面的代码，那么此时它的状态就是 New。而一旦线程调用了 start()，它的状态就会从 New 变成 Runnable，也就是状态转换图中中间的这个大方框里的内容。
Runnable 可运行

![img](http://s0.lgstatic.com/i/image2/M01/A7/06/CgotOV3JD2mAOODWAAEO8oJ9MYE471.png)

Java 中的 Runable 状态对应操作系统线程状态中的两种状态，分别是 Running 和 Ready，也就是说，Java 中处于 Runnable 状态的线程有可能正在执行，也有可能没有正在执行，正在等待被分配 CPU 资源。

 

所以，如果一个正在运行的线程是 Runnable 状态，当它运行到任务的一半时，执行该线程的 CPU 被调度去做其他事情，导致该线程暂时不运行，它的状态依然不变，还是 Runnable，因为它有可能随时被调度回来继续执行任务。
阻塞状态

![img](http://s0.lgstatic.com/i/image2/M01/A6/E6/CgoB5l3JD3uABxHdAAEOLWcYm5k271.png)

接下来，我们来看下 Runnable 下面的三个方框，它们统称为阻塞状态，在 Java 中阻塞状态通常不仅仅是 Blocked，实际上它包括三种状态，分别是 Blocked(被阻塞）、Waiting(等待）、Timed Waiting(计时等待），这三 种状态统称为阻塞状态，下面我们来看看这三种状态具体是什么含义。 
Blocked 被阻塞

![img](http://s0.lgstatic.com/i/image2/M01/A6/E6/CgoB5l3JD5GAMKq4AAENVwnom-A716.png)

首先来看最简单的 Blocked，从箭头的流转方向可以看出，从 Runnable 状态进入 Blocked 状态只有一种可能，就是进入 synchronized 保护的代码时没有抢到 monitor 锁，无论是进入 synchronized 代码块，还是 synchronized 方法，都是一样。

 

我们再往右看，当处于 Blocked 的线程抢到 monitor 锁，就会从 Blocked 状态回到Runnable 状态。
Waiting 等待

![img](http://s0.lgstatic.com/i/image2/M01/A7/07/CgotOV3JD82AdjsoAAENtGVGU1I263.png)

我们再看看 Waiting 状态，线程进入 Waiting 状态有三种可能性。

    没有设置 Timeout 参数的 Object.wait() 方法。
    
    没有设置 Timeout 参数的 Thread.join() 方法。
    
    LockSupport.park() 方法。

刚才强调过，Blocked 仅仅针对 synchronized monitor 锁，可是在 Java 中还有很多其他的锁，比如 ReentrantLock，如果线程在获取这种锁时没有抢到该锁就会进入 Waiting 状态，因为本质上它执行了 LockSupport.park() 方法，所以会进入 Waiting 状态。同样，Object.wait() 和 Thread.join() 也会让线程进入 Waiting 状态。

 

Blocked 与 Waiting 的区别是 Blocked 在等待其他线程释放 monitor 锁，而 Waiting 则是在等待某个条件，比如 join 的线程执行完毕，或者是 notify()/notifyAll() 。
Timed Waiting 限期等待

![img](http://s0.lgstatic.com/i/image2/M01/A7/07/CgotOV3JEBeAbcVyAAENqvIUUv4926.png)

在 Waiting 上面是 Timed Waiting 状态，这两个状态是非常相似的，区别仅在于有没有时间限制，Timed Waiting 会等待超时，由系统自动唤醒，或者在超时前被唤醒信号唤醒。


以下情况会让线程进入 Timed Waiting 状态。

    设置了时间参数的 Thread.sleep(long millis) 方法；
    
    设置了时间参数的 Object.wait(long timeout) 方法；
    
    设置了时间参数的 Thread.join(long millis) 方法；
    
    设置了时间参数的 LockSupport.parkNanos(long nanos) 方法和 LockSupport.parkUntil(long deadline) 方法。

讲完如何进入这三种状态，我们再来看下如何从这三种状态流转到下一个状态。

![img](http://s0.lgstatic.com/i/image2/M01/A7/07/CgotOV3JED2AMO18AAENVwnom-A844.png)

想要从 Blocked 状态进入 Runnable 状态，要求线程获取 monitor 锁，而从 Waiting 状态流转到其他状态则比较特殊，因为首先 Waiting 是不限时的，也就是说无论过了多长时间它都不会主动恢复。

![img](http://s0.lgstatic.com/i/image2/M01/A6/E7/CgoB5l3JEISAQeg5AAENQ_cejbc532.png)

只有当执行了 LockSupport.unpark()，或者 join 的线程运行结束，或者被中断时才可以进入 Runnable 状态。

![img](http://s0.lgstatic.com/i/image2/M01/A7/08/CgotOV3JEO2AZqEAAAEMluEZ1ig308.png)

如果其他线程调用 notify() 或 notifyAll()来唤醒它，它会直接进入 Blocked 状态，这是为什么呢？因为唤醒 Waiting 线程的线程如果调用 notify() 或 notifyAll()，要求必须首先持有该 monitor 锁，所以处于 Waiting 状态的线程被唤醒时拿不到该锁，就会进入 Blocked 状态，直到执行了 notify()/notifyAll() 的唤醒它的线程执行完毕并释放 monitor 锁，才可能轮到它去抢夺这把锁，如果它能抢到，就会从 Blocked 状态回到 Runnable 状态。

![img](http://s0.lgstatic.com/i/image2/M01/A7/08/CgotOV3JEY6AfIPgAAEKu54VDQM844.png)

同样在 Timed Waiting 中执行 notify() 和 notifyAll() 也是一样的道理，它们会先进入 Blocked 状态，然后抢夺锁成功后，再回到 Runnable 状态。

![img](http://s0.lgstatic.com/i/image2/M01/A7/09/CgotOV3JElWAN_bFAAEOeek8lmo788.png)

当然对于 Timed Waiting 而言，如果它的超时时间到了且能直接获取到锁/join的线程运行结束/被中断/调用了LockSupport.unpark()，会直接恢复到 Runnable 状态，而无需经历 Blocked 状态。
Terminated 终止

![img](http://s0.lgstatic.com/i/image2/M01/A6/E9/CgoB5l3JEmOAWvtrAAENzXqTVYc415.png)

再来看看最后一种状态，Terminated 终止状态，要想进入这个状态有两种可能。

    run() 方法执行完毕，线程正常退出。
    
    出现一个没有捕获的异常，终止了 run() 方法，最终导致意外终止。

注意点

最后我们再看线程转换的两个注意点。

    线程的状态是需要按照箭头方向来走的，比如线程从 New 状态是不可以直接进入 Blocked 状态的，它需要先经历 Runnable 状态。
    
    线程生命周期不可逆：一旦进入 Runnable 状态就不能回到 New 状态；一旦被终止就不可能再有任何状态的变化。所以一个线程只能有一次 New 和 Terminated 状态，只有处于中间状态才可以相互转换。


### 第04讲：wait/notify/notifyAll 方法的使用注意事项？

本课时我们主要学习 wait/notify/notifyAll 方法的使用注意事项。

我们主要从三个问题入手：

    为什么 wait 方法必须在 synchronized 保护的同步代码中使用？
    为什么 wait/notify/notifyAll 被定义在 Object 类中，而 sleep 定义在 Thread 类中？
    wait/notify 和 sleep 方法的异同？

为什么 wait 必须在 synchronized 保护的同步代码中使用？

首先，我们来看第一个问题，为什么 wait 方法必须在 synchronized 保护的同步代码中使用？

我们先来看看 wait 方法的源码注释是怎么写的。

“wait method should always be used in a loop:

复制
 synchronized (obj) {
     while (condition does not hold)
         obj.wait();
     ... // Perform action appropriate to condition
}

This method should only be called by a thread that is the owner of this object's monitor.”

英文部分的意思是说，在使用 wait 方法时，必须把 wait 方法写在 synchronized 保护的 while 代码块中，并始终判断执行条件是否满足，如果满足就往下继续执行，如果不满足就执行 wait 方法，而在执行 wait 方法之前，必须先持有对象的 monitor 锁，也就是通常所说的 synchronized 锁。那么设计成这样有什么好处呢？

我们逆向思考这个问题，如果不要求 wait 方法放在 synchronized 保护的同步代码中使用，而是可以随意调用，那么就有可能写出这样的代码。

复制
class BlockingQueue {
    Queue<String> buffer = new LinkedList<String>();
    public void give(String data) {
        buffer.add(data);
        notify();  // Since someone may be waiting in take
    }
    public String take() throws InterruptedException {
        while (buffer.isEmpty()) {
            wait();
        }
        return buffer.remove();
    }
}

在代码中可以看到有两个方法，give 方法负责往 buffer 中添加数据，添加完之后执行 notify 方法来唤醒之前等待的线程，而 take 方法负责检查整个 buffer 是否为空，如果为空就进入等待，如果不为空就取出一个数据，这是典型的生产者消费者的思想。

但是这段代码并没有受 synchronized 保护，于是便有可能发生以下场景：

    首先，消费者线程调用 take 方法并判断 buffer.isEmpty 方法是否返回 true，若为 true 代表buffer是空的，则线程希望进入等待，但是在线程调用 wait 方法之前，就被调度器暂停了，所以此时还没来得及执行 wait 方法。
    此时生产者开始运行，执行了整个 give 方法，它往 buffer 中添加了数据，并执行了 notify 方法，但 notify 并没有任何效果，因为消费者线程的 wait 方法没来得及执行，所以没有线程在等待被唤醒。
    此时，刚才被调度器暂停的消费者线程回来继续执行 wait 方法并进入了等待。

虽然刚才消费者判断了 buffer.isEmpty 条件，但真正执行 wait 方法时，之前的 buffer.isEmpty 的结果已经过期了，不再符合最新的场景了，因为这里的“判断-执行”不是一个原子操作，它在中间被打断了，是线程不安全的。

假设这时没有更多的生产者进行生产，消费者便有可能陷入无穷无尽的等待，因为它错过了刚才 give 方法内的 notify 的唤醒。

我们看到正是因为 wait 方法所在的 take 方法没有被 synchronized 保护，所以它的 while 判断和 wait 方法无法构成原子操作，那么此时整个程序就很容易出错。

我们把代码改写成源码注释所要求的被 synchronized 保护的同步代码块的形式，代码如下。

复制
public void give(String data) {
   synchronized (this) {
      buffer.add(data);
      notify();
  }
}

public String take() throws InterruptedException {
   synchronized (this) {
    while (buffer.isEmpty()) {
         wait();
       }
     return buffer.remove();
  }
}

这样就可以确保 notify 方法永远不会在 buffer.isEmpty 和 wait 方法之间被调用，提升了程序的安全性。

另外，wait 方法会释放 monitor 锁，这也要求我们必须首先进入到 synchronized 内持有这把锁。

这里还存在一个“虚假唤醒”（spurious wakeup）的问题，线程可能在既没有被notify/notifyAll，也没有被中断或者超时的情况下被唤醒，这种唤醒是我们不希望看到的。虽然在实际生产中，虚假唤醒发生的概率很小，但是程序依然需要保证在发生虚假唤醒的时候的正确性，所以就需要采用while循环的结构。

复制
while (condition does not hold)
    obj.wait();

这样即便被虚假唤醒了，也会再次检查while里面的条件，如果不满足条件，就会继续wait，也就消除了虚假唤醒的风险。
为什么 wait/notify/notifyAll 被定义在 Object 类中，而 sleep 定义在 Thread 类中？

我们来看第二个问题，为什么 wait/notify/notifyAll 方法被定义在 Object 类中？而 sleep 方法定义在 Thread 类中？主要有两点原因：

    因为 Java 中每个对象都有一把称之为 monitor 监视器的锁，由于每个对象都可以上锁，这就要求在对象头中有一个用来保存锁信息的位置。这个锁是对象级别的，而非线程级别的，wait/notify/notifyAll 也都是锁级别的操作，它们的锁属于对象，所以把它们定义在 Object 类中是最合适，因为 Object 类是所有对象的父类。
    因为如果把 wait/notify/notifyAll 方法定义在 Thread 类中，会带来很大的局限性，比如一个线程可能持有多把锁，以便实现相互配合的复杂逻辑，假设此时 wait 方法定义在 Thread 类中，如何实现让一个线程持有多把锁呢？又如何明确线程等待的是哪把锁呢？既然我们是让当前线程去等待某个对象的锁，自然应该通过操作对象来实现，而不是操作线程。

wait/notify 和 sleep 方法的异同？

第三个问题是对比 wait/notify 和 sleep 方法的异同，主要对比 wait 和 sleep 方法，我们先说相同点：

    它们都可以让线程阻塞。
    它们都可以响应 interrupt 中断：在等待的过程中如果收到中断信号，都可以进行响应，并抛出 InterruptedException 异常。

但是它们也有很多的不同点：

    wait 方法必须在 synchronized 保护的代码中使用，而 sleep 方法并没有这个要求。
    在同步代码中执行 sleep 方法时，并不会释放 monitor 锁，但执行 wait 方法时会主动释放 monitor 锁。
    sleep 方法中会要求必须定义一个时间，时间到期后会主动恢复，而对于没有参数的 wait 方法而言，意味着永久等待，直到被中断或被唤醒才能恢复，它并不会主动恢复。
    wait/notify 是 Object 类的方法，而 sleep 是 Thread 类的方法。

以上就是关于 wait/notify 与 sleep 的异同点。



### 第05讲：有哪几种实现生产者消费者模式的方法？

本课时我们主要学习如何用 wait/notify/Condition/BlockingQueue 实现生产者消费者模式。
生产者消费者模式

我们先来看看什么是生产者消费者模式，生产者消费者模式是程序设计中非常常见的一种设计模式，被广泛运用在解耦、消息队列等场景。在现实世界中，我们把生产商品的一方称为生产者，把消费商品的一方称为消费者，有时生产者的生产速度特别快，但消费者的消费速度跟不上，俗称“产能过剩”，又或是多个生产者对应多个消费者时，大家可能会手忙脚乱。如何才能让大家更好地配合呢？这时在生产者和消费者之间就需要一个中介来进行调度，于是便诞生了生产者消费者模式。

![img](http://s0.lgstatic.com/i/image2/M01/A9/03/CgotOV3OJ3iAGcaiAAFrcv5xk9U160.png)

使用生产者消费者模式通常需要在两者之间增加一个阻塞队列作为媒介，有了媒介之后就相当于有了一个缓冲，平衡了两者的能力，整体的设计如图所示，最上面是阻塞队列，右侧的 1 是生产者线程，生产者在生产数据后将数据存放在阻塞队列中，左侧的 2 是消费者线程，消费者获取阻塞队列中的数据。而中间的 3 和 4 分别代表生产者消费者之间互相通信的过程，因为无论阻塞队列是满还是空都可能会产生阻塞，阻塞之后就需要在合适的时机去唤醒被阻塞的线程。

那么什么时候阻塞线程需要被唤醒呢？有两种情况。第一种情况是当消费者看到阻塞队列为空时，开始进入等待，这时生产者一旦往队列中放入数据，就会通知所有的消费者，唤醒阻塞的消费者线程。另一种情况是如果生产者发现队列已经满了，也会被阻塞，而一旦消费者获取数据之后就相当于队列空了一个位置，这时消费者就会通知所有正在阻塞的生产者进行生产，这便是对生产者消费者模式的简单介绍。
如何用 BlockingQueue 实现生产者消费者模式

我们接下来看如何用 wait/notify/Condition/BlockingQueue 实现生产者消费者模式，先从最简单的 BlockingQueue 开始讲起：

复制
public static void main(String[] args) {

  BlockingQueue<Object> queue = new ArrayBlockingQueue<>(10);

 Runnable producer = () -> {
    while (true) {
          queue.put(new Object());
  }
   };

new Thread(producer).start();
new Thread(producer).start();

Runnable consumer = () -> {
      while (true) {
           queue.take();
}
   };
new Thread(consumer).start();
new Thread(consumer).start();
}

如代码所示，首先，创建了一个 ArrayBlockingQueue 类型的 BlockingQueue，命名为 queue 并将它的容量设置为 10；其次，创建一个简单的生产者，while(true) 循环体中的queue.put() 负责往队列添加数据；然后，创建两个生产者线程并启动；同样消费者也非常简单，while(true) 循环体中的 queue.take() 负责消费数据，同时创建两个消费者线程并启动。为了代码简洁并突出设计思想，代码里省略了 try/catch 检测，我们不纠结一些语法细节。以上便是利用 BlockingQueue 实现生产者消费者模式的代码。虽然代码非常简单，但实际上 ArrayBlockingQueue 已经在背后完成了很多工作，比如队列满了就去阻塞生产者线程，队列有空就去唤醒生产者线程等。
如何用 Condition 实现生产者消费者模式

BlockingQueue 实现生产者消费者模式看似简单，背后却暗藏玄机，我们在掌握这种方法的基础上仍需要掌握更复杂的实现方法。我们接下来看如何在掌握了 BlockingQueue 的基础上利用 Condition 实现生产者消费者模式，它们背后的实现原理非常相似，相当于我们自己实现一个简易版的 BlockingQueue：

复制
public class MyBlockingQueueForCondition {

   private Queue queue;
   private int max = 16;
   private ReentrantLock lock = new ReentrantLock();
   private Condition notEmpty = lock.newCondition();
   private Condition notFull = lock.newCondition();


   public MyBlockingQueueForCondition(int size) {
       this.max = size;
       queue = new LinkedList();
   }

   public void put(Object o) throws InterruptedException {
       lock.lock();
       try {
           while (queue.size() == max) {
               notFull.await();
           }
           queue.add(o);
           notEmpty.signalAll();
       } finally {
           lock.unlock();
       }
   }

   public Object take() throws InterruptedException {
       lock.lock();
       try {
           while (queue.size() == 0) {
               notEmpty.await();
           }
           Object item = queue.remove();
           notFull.signalAll();
           return item;
       } finally {
           lock.unlock();
       }
   }
}

如代码所示，首先，定义了一个队列变量 queue 并设置最大容量为 16；其次，定义了一个 ReentrantLock 类型的 Lock 锁，并在 Lock 锁的基础上创建两个 Condition，一个是 notEmpty，另一个是 notFull，分别代表队列没有空和没有满的条件；最后，声明了 put 和 take 这两个核心方法。

因为生产者消费者模式通常是面对多线程的场景，需要一定的同步措施保障线程安全，所以在 put 方法中先将 Lock 锁上，然后，在 while 的条件里检测 queue 是不是已经满了，如果已经满了，则调用 notFull 的 await() 阻塞生产者线程并释放 Lock，如果没有满，则往队列放入数据并利用 notEmpty.signalAll() 通知正在等待的所有消费者并唤醒它们。最后在 finally 中利用 lock.unlock() 方法解锁，把 unlock 方法放在 finally 中是一个基本原则，否则可能会产生无法释放锁的情况。

下面再来看 take 方法，take 方法实际上是与 put 方法相互对应的，同样是通过 while 检查队列是否为空，如果为空，消费者开始等待，如果不为空则从队列中获取数据并通知生产者队列有空余位置，最后在 finally 中解锁。

这里需要注意，我们在 take() 方法中使用 while( queue.size() == 0 ) 检查队列状态，而不能用 if( queue.size() == 0 )。为什么呢？大家思考这样一种情况，因为生产者消费者往往是多线程的，我们假设有两个消费者，第一个消费者线程获取数据时，发现队列为空，便进入等待状态；因为第一个线程在等待时会释放 Lock 锁，所以第二个消费者可以进入并执行 if( queue.size() == 0 )，也发现队列为空，于是第二个线程也进入等待；而此时，如果生产者生产了一个数据，便会唤醒两个消费者线程，而两个线程中只有一个线程可以拿到锁，并执行 queue.remove 操作，另外一个线程因为没有拿到锁而卡在被唤醒的地方，而第一个线程执行完操作后会在 finally 中通过 unlock 解锁，而此时第二个线程便可以拿到被第一个线程释放的锁，继续执行操作，也会去调用 queue.remove 操作，然而这个时候队列已经为空了，所以会抛出 NoSuchElementException 异常，这不符合我们的逻辑。而如果用 while 做检查，当第一个消费者被唤醒得到锁并移除数据之后，第二个线程在执行 remove 前仍会进行 while 检查，发现此时依然满足 queue.size() == 0 的条件，就会继续执行 await 方法，避免了获取的数据为 null 或抛出异常的情况。
如何用 wait/notify 实现生产者消费者模式

最后我们再来看看使用 wait/notify 实现生产者消费者模式的方法，实际上实现原理和Condition 是非常类似的，它们是兄弟关系：

复制
class MyBlockingQueue {

   private int maxSize;
   private LinkedList<Object> storage;

   public MyBlockingQueue(int size) {
       this.maxSize = size;
       storage = new LinkedList<>();
   }

   public synchronized void put() throws InterruptedException {
       while (storage.size() == maxSize) {
           wait();
       }
       storage.add(new Object());
       notifyAll();
   }

   public synchronized void take() throws InterruptedException {
       while (storage.size() == 0) {
           wait();
       }
       System.out.println(storage.remove());
       notifyAll();
   }
}

如代码所示，最主要的部分仍是 take 与 put 方法，我们先来看 put 方法，put 方法被 synchronized 保护，while 检查队列是否为满，如果不满就往里放入数据并通过 notifyAll() 唤醒其他线程。同样，take 方法也被 synchronized 修饰，while 检查队列是否为空，如果不为空就获取数据并唤醒其他线程。使用这个 MyBlockingQueue 实现的生产者消费者代码如下：

复制
/**
* 描述：     wait形式实现生产者消费者模式
*/
public class WaitStyle {

   public static void main(String[] args) {
       MyBlockingQueue myBlockingQueue = new MyBlockingQueue(10);
       Producer producer = new Producer(myBlockingQueue);
       Consumer consumer = new Consumer(myBlockingQueue);
       new Thread(producer).start();
       new Thread(consumer).start();
   }
}

class Producer implements Runnable {

   private MyBlockingQueue storage;

   public Producer(MyBlockingQueue storage) {
       this.storage = storage;
   }

   @Override
   public void run() {
       for (int i = 0; i < 100; i++) {
           try {
               storage.put();
           } catch (InterruptedException e) {
               e.printStackTrace();
           }
       }
   }
}

class Consumer implements Runnable {

   private MyBlockingQueue storage;

   public Consumer(MyBlockingQueue storage) {
       this.storage = storage;
   }

   @Override
   public void run() {
       for (int i = 0; i < 100; i++) {
           try {
               storage.take();
           } catch (InterruptedException e) {
               e.printStackTrace();
           }
       }
   }
}

以上就是三种实现生产者消费者模式的讲解，其中，第一种 BlockingQueue 模式实现比较简单，但其背后的实现原理在第二种、第三种实现方法中得以体现，第二种、第三种实现方法本质上是我们自己实现了 BlockingQueue 的一些核心逻辑，供生产者与消费者使用。



## 究竟什么是线程安全？ 

### 第06讲：一共有哪 3 类线程安全问题？

本课时我们学习 3 类线程安全问题。
什么是线程安全

要想弄清楚有哪 3 类线程安全问题，首先需要了解什么是线程安全，线程安全经常在工作中被提到，比如：你的对象不是线程安全的，你的线程发生了安全错误，虽然线程安全经常被提到，但我们可能对线程安全并没有一个明确的定义。

《Java Concurrency In Practice》的作者 Brian Goetz 对线程安全是这样理解的，当多个线程访问一个对象时，如果不用考虑这些线程在运行时环境下的调度和交替执行问题，也不需要进行额外的同步，而调用这个对象的行为都可以获得正确的结果，那这个对象便是线程安全的。

事实上，Brian Goetz 想表达的意思是，如果某个对象是线程安全的，那么对于使用者而言，在使用时就不需要考虑方法间的协调问题，比如不需要考虑不能同时写入或读写不能并行的问题，也不需要考虑任何额外的同步问题，比如不需要额外自己加 synchronized 锁，那么它才是线程安全的，可以看出对线程安全的定义还是非常苛刻的。

而我们在实际开发中经常会遇到线程不安全的情况，那么一共有哪 3 种典型的线程安全问题呢？

    运行结果错误；
    发布和初始化导致线程安全问题；
    活跃性问题。

运行结果错误

首先，来看多线程同时操作一个变量导致的运行结果错误。

复制
public class WrongResult {

   volatile static int i;

   public static void main(String[] args) throws InterruptedException {
       Runnable r = new Runnable() {
           @Override
           public void run() {
               for (int j = 0; j < 10000; j++) {
                   i++;
               }
           }
       };
       Thread thread1 = new Thread(r);
       thread1.start();
       Thread thread2 = new Thread(r);
       thread2.start();
       thread1.join();
       thread2.join();
       System.out.println(i);
    }
}

如代码所示，首先定义了一个 int 类型的静态变量 i，然后启动两个线程，分别对变量 i 进行 10000 次 i++ 操作。理论上得到的结果应该是 20000，但实际结果却远小于理论结果，比如可能是12996，也可能是13323，每次的结果都还不一样，这是为什么呢？

是因为在多线程下，CPU 的调度是以时间片为单位进行分配的，每个线程都可以得到一定量的时间片。但如果线程拥有的时间片耗尽，它将会被暂停执行并让出 CPU 资源给其他线程，这样就有可能发生线程安全问题。比如 i++ 操作，表面上看只是一行代码，但实际上它并不是一个原子操作，它的执行步骤主要分为三步，而且在每步操作之间都有可能被打断。

    第一个步骤是读取；
    第二个步骤是增加；
    第三个步骤是保存。

那么我们接下来看如何发生的线程不安全问题。

![img](http://s0.lgstatic.com/i/image2/M01/A9/E4/CgoB5l3SU9qAObNeAABrSP1t6qc603.png)

我们根据箭头指向依次看，线程 1 首先拿到 i=1 的结果，然后进行 i+1 操作，但此时 i+1 的结果并没有保存下来，线程 1 就被切换走了，于是 CPU 开始执行线程 2，它所做的事情和线程 1 是一样的 i++ 操作，但此时我们想一下，它拿到的 i 是多少？实际上和线程 1 拿到的 i 的结果一样都是 1，为什么呢？因为线程 1 虽然对 i 进行了 +1 操作，但结果没有保存，所以线程 2 看不到修改后的结果。

然后假设等线程 2 对 i 进行 +1 操作后，又切换到线程 1，让线程 1 完成未完成的操作，即将 i+1 的结果 2 保存下来，然后又切换到线程 2 完成 i=2 的保存操作，虽然两个线程都执行了对 i 进行 +1 的操作，但结果却最终保存了 i=2 的结果，而不是我们期望的 i=3，这样就发生了线程安全问题，导致了数据结果错误，这也是最典型的线程安全问题。
发布和初始化导致线程安全问题

第二种是对象发布和初始化时导致的线程安全问题，我们创建对象并进行发布和初始化供其他类或对象使用是常见的操作，但如果我们操作的时间或地点不对，就可能导致线程安全问题。如代码所示。

复制
public class WrongInit {

    private Map<Integer, String> students;
     
    public WrongInit() {
        new Thread(new Runnable() {
            @Override
            public void run() {
                students = new HashMap<>();
                students.put(1, "王小美");
                students.put(2, "钱二宝");
                students.put(3, "周三");
                students.put(4, "赵四");
            }
        }).start();
     }
     
    public Map<Integer, String> getStudents() {
        return students;
    }
     
    public static void main(String[] args) throws InterruptedException {
        WrongInit multiThreadsError6 = new WrongInit();
        System.out.println(multiThreadsError6.getStudents().get(1));
     
    }
}

在类中，定义一个类型为 Map 的成员变量 students，Integer 是学号，String 是姓名。然后在构造函数中启动一个新线程，并在线程中为 students 赋值。

    学号：1，姓名：王小美；
    学号：2，姓名：钱二宝；
    学号：3，姓名：周三；
    学号：4，姓名：赵四。

只有当线程运行完 run() 方法中的全部赋值操作后，4 名同学的全部信息才算是初始化完毕，可是我们看在主函数 mian() 中，初始化 WrongInit 类之后并没有进行任何休息就直接打印 1 号同学的信息，试想这个时候程序会出现什么情况？实际上会发生空指针异常。

复制
Exception in thread "main" java.lang.NullPointerException
at lesson6.WrongInit.main(WrongInit.java:32)

这又是为什么呢？因为 students 这个成员变量是在构造函数中新建的线程中进行的初始化和赋值操作，而线程的启动需要一定的时间，但是我们的 main 函数并没有进行等待就直接获取数据，导致 getStudents 获取的结果为 null，这就是在错误的时间或地点发布或初始化造成的线程安全问题。
活跃性问题

第三种线程安全问题统称为活跃性问题，最典型的有三种，分别为死锁、活锁和饥饿。

什么是活跃性问题呢，活跃性问题就是程序始终得不到运行的最终结果，相比于前面两种线程安全问题带来的数据错误或报错，活跃性问题带来的后果可能更严重，比如发生死锁会导致程序完全卡死，无法向下运行。
死锁

最常见的活跃性问题是死锁，死锁是指两个线程之间相互等待对方资源，但同时又互不相让，都想自己先执行，如代码所示。

复制
 public class MayDeadLock {

    Object o1 = new Object();
    Object o2 = new Object();
     
    public void thread1() throws InterruptedException {
        synchronized (o1) {
            Thread.sleep(500);
            synchronized (o2) {
                System.out.println("线程1成功拿到两把锁");
           }
        }
    }
     
    public void thread2() throws InterruptedException {
        synchronized (o2) {
            Thread.sleep(500);
            synchronized (o1) {
                System.out.println("线程2成功拿到两把锁");
            }
        }
    }
     
    public static void main(String[] args) {
        MayDeadLock mayDeadLock = new MayDeadLock();
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    mayDeadLock.thread1();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    mayDeadLock.thread2();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }
}

首先，代码中创建了两个 Object 作为 synchronized 锁的对象，线程 1 先获取 o1 锁，sleep(500) 之后，获取 o2 锁；线程 2 与线程 1 执行顺序相反，先获取 o2 锁，sleep(500) 之后，获取 o1 锁。  假设两个线程几乎同时进入休息，休息完后，线程 1 想获取 o2 锁，线程 2 想获取 o1 锁，这时便发生了死锁，两个线程不主动调和，也不主动退出，就这样死死地等待对方先释放资源，导致程序得不到任何结果也不能停止运行。
活锁

第二种活跃性问题是活锁，活锁与死锁非常相似，也是程序一直等不到结果，但对比于死锁，活锁是活的，什么意思呢？因为正在运行的线程并没有阻塞，它始终在运行中，却一直得不到结果。

举一个例子，假设有一个消息队列，队列里放着各种各样需要被处理的消息，而某个消息由于自身被写错了导致不能被正确处理，执行时会报错，可是队列的重试机制会重新把它放在队列头进行优先重试处理，但这个消息本身无论被执行多少次，都无法被正确处理，每次报错后又会被放到队列头进行重试，周而复始，最终导致线程一直处于忙碌状态，但程序始终得不到结果，便发生了活锁问题。
饥饿

第三个典型的活跃性问题是饥饿，饥饿是指线程需要某些资源时始终得不到，尤其是CPU 资源，就会导致线程一直不能运行而产生的问题。在 Java 中有线程优先级的概念，Java 中优先级分为 1 到 10，1 最低，10 最高。如果我们把某个线程的优先级设置为 1，这是最低的优先级，在这种情况下，这个线程就有可能始终分配不到 CPU 资源，而导致长时间无法运行。或者是某个线程始终持有某个文件的锁，而其他线程想要修改文件就必须先获取锁，这样想要修改文件的线程就会陷入饥饿，长时间不能运行。



### 第07讲：哪些场景需要额外注意线程安全问题？

在本课时我们主要学习哪些场景需要额外注意线程安全问题，在这里总结了四种场景。
访问共享变量或资源

第一种场景是访问共享变量或共享资源的时候，典型的场景有访问共享对象的属性，访问 static 静态变量，访问共享的缓存，等等。因为这些信息不仅会被一个线程访问到，还有可能被多个线程同时访问，那么就有可能在并发读写的情况下发生线程安全问题。比如我们上一课时讲过的多线程同时 i++ 的例子：

复制
/**
 * 描述：     共享的变量或资源带来的线程安全问题
 */
public class ThreadNotSafe1 {

    static int i;

    public static void main(String[] args) throws InterruptedException {
        Runnable r = new Runnable() {
            @Override
            public void run() {
                for (int j = 0; j < 10000; j++) {
                    i++;
                }
            }
        };
        Thread thread1 = new Thread(r);
        Thread thread2 = new Thread(r);
        thread1.start();
        thread2.start();
        thread1.join();
        thread2.join();
        System.out.println(i);
    }
}

如代码所示，两个线程同时对 i 进行 i++ 操作，最后的输出可能是 15875 等小于20000的数，而不是我们期待的20000，这便是非常典型的共享变量带来的线程安全问题。
依赖时序的操作

第二个需要我们注意的场景是依赖时序的操作，如果我们操作的正确性是依赖时序的，而在多线程的情况下又不能保障执行的顺序和我们预想的一致，这个时候就会发生线程安全问题，如下面的代码所示：

复制
if (map.containsKey(key)) {
    map.remove(obj)
}

代码中首先检查 map 中有没有 key 对应的元素，如果有则继续执行 remove 操作。此时，这个组合操作就是危险的，因为它是先检查后操作，而执行过程中可能会被打断。如果此时有两个线程同时进入 if() 语句，然后它们都检查到存在 key 对应的元素，于是都希望执行下面的 remove 操作，随后一个线程率先把 obj 给删除了，而另外一个线程它刚已经检查过存在 key 对应的元素，if 条件成立，所以它也会继续执行删除 obj 的操作，但实际上，集合中的 obj 已经被前面的线程删除了，这种情况下就可能导致线程安全问题。

类似的情况还有很多，比如我们先检查 x=1，如果 x=1 就修改 x 的值，代码如下所示：

复制
if (x == 1) {
    x = 7 * x;
}

这样类似的场景都是同样的道理，“检查与执行”并非原子性操作，在中间可能被打断，而检查之后的结果也可能在执行时已经过期、无效，换句话说，获得正确结果取决于幸运的时序。这种情况下，我们就需要对它进行加锁等保护措施来保障操作的原子性。
不同数据之间存在绑定关系

第三种需要我们注意的线程安全场景是不同数据之间存在相互绑定关系的情况。有时候，我们的不同数据之间是成组出现的，存在着相互对应或绑定的关系，最典型的就是 IP 和端口号。有时候我们更换了 IP，往往需要同时更换端口号，如果没有把这两个操作绑定在一起，就有可能出现单独更换了 IP 或端口号的情况，而此时信息如果已经对外发布，信息获取方就有可能获取一个错误的 IP 与端口绑定情况，这时就发生了线程安全问题。在这种情况下，我们也同样需要保障操作的原子性。
对方没有声明自己是线程安全的

第四种值得注意的场景是在我们使用其他类时，如果对方没有声明自己是线程安全的，那么这种情况下对其他类进行多线程的并发操作，就有可能会发生线程安全问题。举个例子，比如说我们定义了 ArrayList，它本身并不是线程安全的，如果此时多个线程同时对 ArrayList 进行并发读/写，那么就有可能会产生线程安全问题，造成数据出错，而这个责任并不在 ArrayList，因为它本身并不是并发安全的，正如源码注释所写的：

复制
Note that this implementation is not synchronized. If multiple threads
access an ArrayList instance concurrently, and at least one of the threads
modifies the list structurally, it must be synchronized externally.

这段话的意思是说，如果我们把 ArrayList 用在了多线程的场景，需要在外部手动用 synchronized 等方式保证并发安全。

所以 ArrayList 默认不适合并发读写，是我们错误地使用了它，导致了线程安全问题。所以，我们在使用其他类时如果会涉及并发场景，那么一定要首先确认清楚，对方是否支持并发操作，以上就是四种需要我们额外注意线程安全问题的场景，分别是访问共享变量或资源，依赖时序的操作，不同数据之间存在绑定关系，以及对方没有声明自己是线程安全的。



### 第08讲：为什么多线程会带来性能问题？

在本课时我们主要学习为什么多线程会带来性能问题？

什么是性能问题     

在上一课时我们已经学习了多线程带来的线程安全问题，但对于多线程而言，它不仅可能会带来线程安全问题，还有可能会带来性能问题，也许你会奇怪，我们使用多线程的最大目的不就是为了提高性能吗？让多个线程同时工作，加快程序运行速度，为什么反而会带来性能问题呢？这是因为单线程程序是独立工作的，不需要与其他线程进行交互，但多线程之间则需要调度以及合作，调度与合作就会带来性能开销从而产生性能问题。

 

首先，我们来了解究竟什么是性能问题？其实性能问题有许多的表现形式，比如服务器的响应慢、吞吐量低、内存占用过多就属于性能问题。我们设计优秀的系统架构、购置更多的 CDN 服务器、购买更大的带宽等都是为了提高性能，提高用户体验，虽然运行速度慢不会带来严重的后果，通常只需要我们多等几秒就可以，但这会严重影响用户的体验。有研究表明，页面每多响应 1 秒，就会流失至少 7% 的用户，而超过 8 秒无法返回结果的话，几乎所有用户都不会选择继续等待。我们引入多线程的一大重要原因就是想提高程序性能，所以不能本末倒置，不能因为引入了多线程反而程序运行得更慢了，所以我们必须要解决多线程带来的性能问题。

为什么多线程会带来性能问题

那么什么情况下多线程编程会带来性能问题呢？主要有两个方面，一方面是线程调度，另一个方面是线程协作。

调度开销

上下文切换      

首先，我们看一下线程调度，在实际开发中，线程数往往是大于 CPU 核心数的，比如 CPU 核心数可能是 8 核、16 核，等等，但线程数可能达到成百上千个。这种情况下，操作系统就会按照一定的调度算法，给每个线程分配时间片，让每个线程都有机会得到运行。而在进行调度时就会引起上下文切换，上下文切换会挂起当前正在执行的线程并保存当前的状态，然后寻找下一处即将恢复执行的代码，唤醒下一个线程，以此类推，反复执行。但上下文切换带来的开销是比较大的，假设我们的任务内容非常短，比如只进行简单的计算，那么就有可能发生我们上下文切换带来的性能开销比执行线程本身内容带来的开销还要大的情况。

缓存失效

不仅上下文切换会带来性能问题，缓存失效也有可能带来性能问题。由于程序有很大概率会再次访问刚才访问过的数据，所以为了加速整个程序的运行，会使用缓存，这样我们在使用相同数据时就可以很快地获取数据。可一旦进行了线程调度，切换到其他线程，CPU就会去执行不同的代码，原有的缓存就很可能失效了，需要重新缓存新的数据，这也会造成一定的开销，所以线程调度器为了避免频繁地发生上下文切换，通常会给被调度到的线程设置最小的执行时间，也就是只有执行完这段时间之后，才可能进行下一次的调度，由此减少上下文切换的次数。

 

那么什么情况会导致密集的上下文切换呢？如果程序频繁地竞争锁，或者由于 IO 读写等原因导致频繁阻塞，那么这个程序就可能需要更多的上下文切换，这也就导致了更大的开销，我们应该尽量避免这种情况的发生。

协作开销       

除了线程调度之外，线程协作同样也有可能带来性能问题。因为线程之间如果有共享数据，为了避免数据错乱，为了保证线程安全，就有可能禁止编译器和 CPU 对其进行重排序等优化，也可能出于同步的目的，反复把线程工作内存的数据 flush 到主存中，然后再从主内存 refresh 到其他线程的工作内存中，等等。这些问题在单线程中并不存在，但在多线程中为了确保数据的正确性，就不得不采取上述方法，因为线程安全的优先级要比性能优先级更高，这也间接降低了我们的性能。



## 线程池 

### 第09讲：使用线程池比手动创建线程好在哪里？

在本课时我们主要学习为什么使用线程池比手动创建线程要好，并讲解具体好在哪里？
为什么要使用线程池

首先，回顾线程池的相关知识，在 Java 诞生之初是没有线程池的概念的，而是先有线程，随着线程数的不断增加，人们发现需要一个专门的类来管理它们，于是才诞生了线程池。没有线程池的时候，每发布一个任务就需要创建一个新的线程，这样在任务少时是没有问题的，如代码所示。

复制
/** 
* 描述：     单个任务的时候，新建线程来执行 
*/ 
public class OneTask { 

    public static void main(String[] args) { 
        Thread thread0 = new Thread(new Task());
        thread0.start();
    } 

    static class Task implements Runnable { 

        public void run() { 
           System.out.println("Thread Name: " + Thread.currentThread().getName());
        } 
    } 
}

在这段代码中，我们发布了一个新的任务并放入子线程中，然后启动子线程执行任务，这时的任务也非常简单，只是打印出当前线程的名字，这种情况下，打印结果显示 Thread Name: Thread-0，即我们当前子线程的默认名字。

![img](https://s0.lgstatic.com/i/image2/M01/AC/D8/CgotOV3bl_OAP8gZAAAYnEDwotE879.png)

我们来看一下任务执行流程，如图所示，主线程调用 start() 方法，启动了一个 t0 的子线程。这是在一个任务的场景下，随着我们的任务增多，比如现在有 10 个任务了，那么我们就可以使用 for 循环新建 10 个子线程，如代码所示。

复制
/** 

* 描述：     for循环新建10个线程 
*/ 
public class TenTask { 

    public static void main(String[] args) { 
        for (int i = 0; i < 10; i++) { 
            Thread thread = new Thread(new Task());
            thread.start();
        } 
    } 

    static class Task implements Runnable { 

        public void run() { 
            System.out.println("Thread Name: " + Thread.currentThread().getName());
        } 
    } 
}

执行结果：

复制
Thread Name: Thread-1
Thread Name: Thread-4
Thread Name: Thread-3
Thread Name: Thread-2
Thread Name: Thread-0
Thread Name: Thread-5
Thread Name: Thread-6
Thread Name: Thread-7
Thread Name: Thread-8
Thread Name: Thread-9

这里你会发现，打印出来的顺序是错乱的，比如 Thread-4 打印在了 Thread-3 之前，这是因为，虽然  Thread-3 比  Thread-4 先执行 start 方法，但是这并不代表  Thread-3 就会先运行，运行的顺序取决于线程调度器，有很大的随机性，这是需要我们注意的地方。

![img](https://s0.lgstatic.com/i/image2/M01/AC/B8/CgoB5l3bmAiAKPcnAAAnuMuAyEc996.png)

我们再看来下线程的执行流程，如图所示，主线程通过 for 循环创建了 t0~t9 这 10 个子线程，它们都可以正常的执行任务，但如果此时我们的任务量突然飙升到 10000 会怎么样？我们先来看看依然用 for 循环的实现方式：

复制
for (int i = 0; i < 10000; i++) { 
    Thread thread = new Thread(new Task());
    thread.start();
}

如图所示，我们创建了 10000 个子线程，而 Java 程序中的线程与操作系统中的线程是一一对应的，此时假设线程中的任务需要一定的耗时才能够完成，便会产生很大的系统开销与资源浪费。

![img](https://s0.lgstatic.com/i/image2/M01/AC/B8/CgoB5l3bmCWACy-0AABGfJcEe18035.png)

创建线程时会产生系统开销，并且每个线程还会占用一定的内存等资源，更重要的是我们创建如此多的线程也会给稳定性带来危害，因为每个系统中，可创建线程的数量是有一个上限的，不可能无限的创建。线程执行完需要被回收，大量的线程又会给垃圾回收带来压力。但我们的任务确实非常多，如果都在主线程串行执行，那效率也太低了，那应该怎么办呢？于是便诞生了线程池来平衡线程与系统资源之间的关系。

我们来总结下如果每个任务都创建一个线程会带来哪些问题：

    第一点，反复创建线程系统开销比较大，每个线程创建和销毁都需要时间，如果任务比较简单，那么就有可能导致创建和销毁线程消耗的资源比线程执行任务本身消耗的资源还要大。
    第二点，过多的线程会占用过多的内存等资源，还会带来过多的上下文切换，同时还会导致系统不稳定。

线程池解决问题思路

针对上面的两点问题，线程池有两个解决思路。

首先，针对反复创建线程开销大的问题，线程池用一些固定的线程一直保持工作状态并反复执行任务。

其次，针对过多线程占用太多内存资源的问题，解决思路更直接，线程池会根据需要创建线程，控制线程的总数量，避免占用过多内存资源。
如何使用线程池

线程池就好比一个池塘，池塘里的水是有限且可控的，比如我们选择线程数固定数量的线程池，假设线程池有 5 个线程，但此时的任务大于 5 个，线程池会让余下的任务进行排队，而不是无限制的扩张线程数量，保障资源不会被过度消耗。如代码所示，我们往 5 个线程的线程池中放入 10000 个任务并打印当前线程名字，结果会是怎么样呢？

复制
/** 
* 描述：     用固定线程数的线程池执行10000个任务 
*/ 
public class ThreadPoolDemo { 

    public static void main(String[] args) { 
        ExecutorService service = Executors.newFixedThreadPool(5);
        for (int i = 0; i < 10000; i++) { 
            service.execute(new Task());
        } 
    System.out.println(Thread.currentThread().getName());
    } 

    static class Task implements Runnable { 

        public void run() { 
            System.out.println("Thread Name: " + Thread.currentThread().getName());
        } 
    } 
}

执行效果：

复制
Thread Name: pool-1-thread-1
Thread Name: pool-1-thread-2
Thread Name: pool-1-thread-3
Thread Name: pool-1-thread-4
Thread Name: pool-1-thread-5
Thread Name: pool-1-thread-5
Thread Name: pool-1-thread-5
Thread Name: pool-1-thread-5
Thread Name: pool-1-thread-5
Thread Name: pool-1-thread-2
Thread Name: pool-1-thread-1
Thread Name: pool-1-thread-5
Thread Name: pool-1-thread-3
Thread Name: pool-1-thread-5

...

如打印结果所示，打印的线程名始终在 Thread Name: pool-1-thread-1~5 之间变化，并没有超过这个范围，也就证明了线程池不会无限制地扩张线程的数量，始终是这5个线程在工作。

![img](https://s0.lgstatic.com/i/image2/M01/AC/D8/CgotOV3bmEOAaIncAABOPHpwdNY412.png)


执行流程如图所示，首先创建了一个线程池，线程池中有 5 个线程，然后线程池将 10000 个任务分配给这 5 个线程，这 5 个线程反复领取任务并执行，直到所有任务执行完毕，这就是线程池的思想。
使用线程池的好处

使用线程池比手动创建线程主要有三点好处。

    第一点，线程池可以解决线程生命周期的系统开销问题，同时还可以加快响应速度。因为线程池中的线程是可以复用的，我们只用少量的线程去执行大量的任务，这就大大减小了线程生命周期的开销。而且线程通常不是等接到任务后再临时创建，而是已经创建好时刻准备执行任务，这样就消除了线程创建所带来的延迟，提升了响应速度，增强了用户体验。
    第二点，线程池可以统筹内存和 CPU 的使用，避免资源使用不当。线程池会根据配置和任务数量灵活地控制线程数量，不够的时候就创建，太多的时候就回收，避免线程过多导致内存溢出，或线程太少导致 CPU 资源浪费，达到了一个完美的平衡。
    第三点，线程池可以统一管理资源。比如线程池可以统一管理任务队列和线程，可以统一开始或结束任务，比单个线程逐一处理任务要更方便、更易于管理，同时也有利于数据统计，比如我们可以很方便地统计出已经执行过的任务的数量。


### 第10讲：线程池的各个参数的含义？

本课时我们主要学习线程池各个参数的含义，并重点掌握线程池中线程是在什么时机被创建和销毁的。

线程池的参数

![img](https://s0.lgstatic.com/i/image2/M01/AD/A3/CgoB5l3eH8mAAoJCAACEOKMHtpw036.png)

首先，我们来看下线程池中各个参数的含义，如表所示线程池主要有 6 个参数，其中第 3 个参数由 keepAliveTime + 时间单位组成。我们逐一看下它们各自的含义，corePoolSize 是核心线程数，也就是常驻线程池的线程数量，与它对应的是 maxPoolSize，表示线程池最大线程数量，当我们的任务特别多而 corePoolSize 核心线程数无法满足需求的时候，就会向线程池中增加线程，以便应对任务突增的情况。

线程创建的时机

![img](https://s0.lgstatic.com/i/image2/M01/AD/A3/CgoB5l3eH-KAAHpkAAC4vEMOXQ4797.png)

接下来，我们来具体看下这两个参数所代表的含义，以及线程池中创建线程的时机。如上图所示，当提交任务后，线程池首先会检查当前线程数，如果此时线程数小于核心线程数，比如最开始线程数量为 0，则新建线程并执行任务，随着任务的不断增加，线程数会逐渐增加并达到核心线程数，此时如果仍有任务被不断提交，就会被放入 workQueue 任务队列中，等待核心线程执行完当前任务后重新从 workQueue 中提取正在等待被执行的任务。

 

此时，假设我们的任务特别的多，已经达到了 workQueue 的容量上限，这时线程池就会启动后备力量，也就是 maxPoolSize 最大线程数，线程池会在 corePoolSize 核心线程数的基础上继续创建线程来执行任务，假设任务被不断提交，线程池会持续创建线程直到线程数达到 maxPoolSize 最大线程数，如果依然有任务被提交，这就超过了线程池的最大处理能力，这个时候线程池就会拒绝这些任务，我们可以看到实际上任务进来之后，线程池会逐一判断 corePoolSize 、workQueue 、maxPoolSize ，如果依然不能满足需求，则会拒绝任务。

corePoolSize 与 maxPoolSize   

通过上面的流程图，我们了解了 corePoolSize 和 maxPoolSize 的具体含义，corePoolSize 指的是核心线程数，线程池初始化时线程数默认为 0，当有新的任务提交后，会创建新线程执行任务，如果不做特殊设置，此后线程数通常不会再小于 corePoolSize ，因为它们是核心线程，即便未来可能没有可执行的任务也不会被销毁。随着任务量的增加，在任务队列满了之后，线程池会进一步创建新线程，最多可以达到 maxPoolSize 来应对任务多的场景，如果未来线程有空闲，大于 corePoolSize 的线程会被合理回收。所以正常情况下，线程池中的线程数量会处在 corePoolSize 与 maxPoolSize 的闭区间内。

![CgotOV3eIA2AY8DaAC4VmOi19V8654](/Users/mk/Downloads/CgotOV3eIA2AY8DaAC4VmOi19V8654.gif)

“长工”与“临时工”

我们可以把 corePoolSize 与 maxPoolSize 比喻成长工与临时工，通常古代一个大户人家会有几个固定的长工，负责日常的工作，而大户人家起初肯定也是从零开始雇佣长工的。假如长工数量被老爷设定为 5 人，也就对应了 corePoolSize，不管这 5 个长工是忙碌还是空闲，都会一直在大户人家待着，可到了农忙或春节，长工的人手显然就不够用了，这时就需要雇佣更多的临时工，这些临时工就相当于在 corePoolSize 的基础上继续创建新线程，但临时工也是有上限的，也就对应了 maxPoolSize，随着农忙或春节结束，老爷考虑到人工成本便会解约掉这些临时工，家里工人数量便会从 maxPoolSize 降到 corePoolSize，所以老爷家的工人数量会一致保持在 corePoolSize 和 maxPoolSize 的区间。

​     

在这里我们用一个动画把整个线程池变化过程生动地描述出来，比如线程池的 corePoolSize 为 5，maxPoolSize 为 10，任务队列容量为 100，随着任务被提交，我们的线程数量会从 0 慢慢增长到 5，然后就不再增长了，新的任务会被放入队列中，直到队列被塞满，然后在 corePoolSize 的基础上继续创建新线程来执行队列中的任务，线程会逐渐增加到 maxPoolSize， 然后线程数不再增加，如果此时仍有任务被不断提交，线程池就会拒绝任务。随着队列中任务被执行完，被创建的 10 个线程现在无事可做了，这时线程池会根据 keepAliveTime 参数来销毁线程，已达到减少内存占用的目的。

​       

通过对流程图的理解和动画演示，我们总结出线程池的几个特点。

    线程池希望保持较少的线程数，并且只有在负载变得很大时才增加线程。
    
    线程池只有在任务队列填满时才创建多于 corePoolSize 的线程，如果使用的是无界队列（例如 LinkedBlockingQueue），那么由于队列不会满，所以线程数不会超过 corePoolSize。
    
    通过设置 corePoolSize 和 maxPoolSize 为相同的值，就可以创建固定大小的线程池。
    
    通过设置 maxPoolSize 为很高的值，例如 Integer.MAX_VALUE，就可以允许线程池创建任意多的线程。

keepAliveTime+时间单位     

第三个参数是 keepAliveTime + 时间单位，当线程池中线程数量多于核心线程数时，而此时又没有任务可做，线程池就会检测线程的 keepAliveTime，如果超过规定的时间，无事可做的线程就会被销毁，以便减少内存的占用和资源消耗。如果后期任务又多了起来，线程池也会根据规则重新创建线程，所以这是一个可伸缩的过程，比较灵活，我们也可以用 setKeepAliveTime 方法动态改变 keepAliveTime 的参数值。

ThreadFactory   

第四个参数是 ThreadFactory，ThreadFactory 实际上是一个线程工厂，它的作用是生产线程以便执行任务。我们可以选择使用默认的线程工厂，创建的线程都会在同一个线程组，并拥有一样的优先级，且都不是守护线程，我们也可以选择自己定制线程工厂，以方便给线程自定义命名，不同的线程池内的线程通常会根据具体业务来定制不同的线程名。

workQueue 和 Handler     

最后两个参数是 workQueue 和 Handler，它们分别对应阻塞队列和任务拒绝策略，在后面的课时会对它们进行详细展开讲解。

 

在本课时，介绍了线程池的各个参数的含义，以及如果有任务提交，线程池是如何应对的，新线程是在什么时机下被创建和销毁等内容，你有没有觉得线程池的设计很巧妙呢？



### 第11讲：线程池有哪 4 种拒绝策略？

本课时我们主要学习线程池有哪 4 种默认的拒绝策略。
拒绝时机

首先，新建线程池时可以指定它的任务拒绝策略，例如：

复制
newThreadPoolExecutor(5, 10, 5, TimeUnit.SECONDS, new LinkedBlockingQueue<>(),
   new ThreadPoolExecutor.DiscardOldestPolicy());

以便在必要的时候按照我们的策略来拒绝任务，那么拒绝任务的时机是什么呢？线程池会在以下两种情况下会拒绝新提交的任务。

    第一种情况是当我们调用 shutdown 等方法关闭线程池后，即便此时可能线程池内部依然有没执行完的任务正在执行，但是由于线程池已经关闭，此时如果再向线程池内提交任务，就会遭到拒绝。
    第二种情况是线程池没有能力继续处理新提交的任务，也就是工作已经非常饱和的时候。

我们具体讲一下第二种情况，也就是由于工作饱和导致的拒绝。比如新建一个线程池，使用容量上限为 10 的 ArrayBlockingQueue 作为任务队列，并且指定线程池的核心线程数为 5，最大线程数为 10，假设此时有 20 个耗时任务被提交，在这种情况下，线程池会首先创建核心数量的线程，也就是5个线程来执行任务，然后往队列里去放任务，队列的 10 个容量被放满了之后，会继续创建新线程，直到达到最大线程数 10。此时线程池中一共有 20 个任务，其中 10 个任务正在被 10 个线程执行，还有 10 个任务在任务队列中等待，而且由于线程池的最大线程数量就是 10，所以已经不能再增加更多的线程来帮忙处理任务了，这就意味着此时线程池工作饱和，这个时候再提交新任务时就会被拒绝。

![img](https://s0.lgstatic.com/i/image2/M01/AE/90/CgoB5l3g0XCAWJKOAABzAQJB4SM657.png)

我们结合图示来分析上述情况，首先看右侧上方的队列部分，你可以看到目前队列已经满了，而图中队列下方的每个线程都在工作，且线程数已经达到最大值 10，如果此时再有新的任务提交，线程池由于没有能力继续处理新提交的任务，所以就会拒绝。

我们了解了线程池拒绝任务的时机，那么我们如何正确地选择拒绝策略呢？Java 在 ThreadPoolExecutor 类中为我们提供了 4 种默认的拒绝策略来应对不同的场景，都实现了 RejectedExecutionHandler 接口，如图所示：

![img](https://s0.lgstatic.com/i/image2/M01/AE/B0/CgotOV3g0WWAVWVlAAEsBI6lEEA162.png)

接下来，我们将具体讲解这 4 种拒绝策略。
拒绝策略

    第一种拒绝策略是 AbortPolicy，这种拒绝策略在拒绝任务时，会直接抛出一个类型为 RejectedExecutionException 的 RuntimeException，让你感知到任务被拒绝了，于是你便可以根据业务逻辑选择重试或者放弃提交等策略。
    第二种拒绝策略是 DiscardPolicy，这种拒绝策略正如它的名字所描述的一样，当新任务被提交后直接被丢弃掉，也不会给你任何的通知，相对而言存在一定的风险，因为我们提交的时候根本不知道这个任务会被丢弃，可能造成数据丢失。
    第三种拒绝策略是 DiscardOldestPolicy，如果线程池没被关闭且没有能力执行，则会丢弃任务队列中的头结点，通常是存活时间最长的任务，这种策略与第二种不同之处在于它丢弃的不是最新提交的，而是队列中存活时间最长的，这样就可以腾出空间给新提交的任务，但同理它也存在一定的数据丢失风险。
    第四种拒绝策略是 CallerRunsPolicy，相对而言它就比较完善了，当有新任务提交后，如果线程池没被关闭且没有能力执行，则把这个任务交于提交任务的线程执行，也就是谁提交任务，谁就负责执行任务。这样做主要有两点好处。
        第一点新提交的任务不会被丢弃，这样也就不会造成业务损失。
        第二点好处是，由于谁提交任务谁就要负责执行任务，这样提交任务的线程就得负责执行任务，而执行任务又是比较耗时的，在这段期间，提交任务的线程被占用，也就不会再提交新的任务，减缓了任务提交的速度，相当于是一个负反馈。在此期间，线程池中的线程也可以充分利用这段时间来执行掉一部分任务，腾出一定的空间，相当于是给了线程池一定的缓冲期。




### 第12讲：有哪 6 种常见的线程池？什么是 Java8 的 ForkJoinPool？

在本课时我们主要学习常见的 6 种线程池，并详细讲解 Java 8 新增的 ForkJoinPool 线程池，6 种常见的线程池如下。

    FixedThreadPool
    CachedThreadPool
    ScheduledThreadPool
    SingleThreadExecutor
    SingleThreadScheduledExecutor
    ForkJoinPool

FixedThreadPool

第一种线程池叫作 FixedThreadPool，它的核心线程数和最大线程数是一样的，所以可以把它看作是固定线程数的线程池，它的特点是线程池中的线程数除了初始阶段需要从 0 开始增加外，之后的线程数量就是固定的，就算任务数超过线程数，线程池也不会再创建更多的线程来处理任务，而是会把超出线程处理能力的任务放到任务队列中进行等待。而且就算任务队列满了，到了本该继续增加线程数的时候，由于它的最大线程数和核心线程数是一样的，所以也无法再增加新的线程了。

![img](https://s0.lgstatic.com/i/image2/M01/AF/A0/CgotOV3kzoeARRniAAAwS8Pup4A734.png)

如图所示，线程池有 t0~t9，10 个线程，它们会不停地执行任务，如果某个线程任务执行完了，就会从任务队列中获取新的任务继续执行，期间线程数量不会增加也不会减少，始终保持在 10 个。
CachedThreadPool

第二种线程池是 CachedThreadPool，可以称作可缓存线程池，它的特点在于线程数是几乎可以无限增加的（实际最大可以达到 Integer.MAX_VALUE，为 2^31-1，这个数非常大，所以基本不可能达到），而当线程闲置时还可以对线程进行回收。也就是说该线程池的线程数量不是固定不变的，当然它也有一个用于存储提交任务的队列，但这个队列是 SynchronousQueue，队列的容量为0，实际不存储任何任务，它只负责对任务进行中转和传递，所以效率比较高。

当我们提交一个任务后，线程池会判断已创建的线程中是否有空闲线程，如果有空闲线程则将任务直接指派给空闲线程，如果没有空闲线程，则新建线程去执行任务，这样就做到了动态地新增线程。让我们举个例子，如下方代码所示。

复制
ExecutorService service = Executors.newCachedThreadPool();
    for (int i = 0; i < 1000; i++) { 
        service.execute(new Task() { 
    });
 }

使用 for 循环提交 1000 个任务给 CachedThreadPool，假设这些任务处理的时间非常长，会发生什么情况呢？因为 for 循环提交任务的操作是非常快的，但执行任务却比较耗时，就可能导致 1000 个任务都提交完了但第一个任务还没有被执行完，所以此时 CachedThreadPool 就可以动态的伸缩线程数量，随着任务的提交，不停地创建 1000 个线程来执行任务，而当任务执行完之后，假设没有新的任务了，那么大量的闲置线程又会造成内存资源的浪费，这时线程池就会检测线程在 60 秒内有没有可执行任务，如果没有就会被销毁，最终线程数量会减为 0。
ScheduledThreadPool

第三个线程池是 ScheduledThreadPool，它支持定时或周期性执行任务。比如每隔 10 秒钟执行一次任务，而实现这种功能的方法主要有 3 种，如代码所示：

复制
ScheduledExecutorService service = Executors.newScheduledThreadPool(10);

service.schedule(new Task(), 10, TimeUnit.SECONDS);

service.scheduleAtFixedRate(new Task(), 10, 10, TimeUnit.SECONDS);

service.scheduleWithFixedDelay(new Task(), 10, 10, TimeUnit.SECONDS);

那么这 3 种方法有什么区别呢？

    第一种方法 schedule 比较简单，表示延迟指定时间后执行一次任务，如果代码中设置参数为 10 秒，也就是 10 秒后执行一次任务后就结束。
    第二种方法 scheduleAtFixedRate 表示以固定的频率执行任务，它的第二个参数 initialDelay 表示第一次延时时间，第三个参数 period 表示周期，也就是第一次延时后每次延时多长时间执行一次任务。
    第三种方法 scheduleWithFixedDelay 与第二种方法类似，也是周期执行任务，区别在于对周期的定义，之前的 scheduleAtFixedRate 是以任务开始的时间为时间起点开始计时，时间到就开始执行第二次任务，而不管任务需要花多久执行；而 scheduleWithFixedDelay 方法以任务结束的时间为下一次循环的时间起点开始计时。

举个例子，假设某个同学正在熬夜写代码，需要喝咖啡来提神，假设每次喝咖啡都需要花10分钟的时间，如果此时采用第2种方法 scheduleAtFixedRate，时间间隔设置为 1 小时，那么他将会在每个整点喝一杯咖啡，以下是时间表：

    00:00: 开始喝咖啡
    00:10: 喝完了
    01:00: 开始喝咖啡
    01:10: 喝完了
    02:00: 开始喝咖啡
    02:10: 喝完了

但是假设他采用第3种方法 scheduleWithFixedDelay，时间间隔同样设置为 1 小时，那么由于每次喝咖啡需要10分钟，而 scheduleWithFixedDelay 是以任务完成的时间为时间起点开始计时的，所以第2次喝咖啡的时间将会在1:10，而不是1:00整，以下是时间表：

    00:00: 开始喝咖啡
    00:10: 喝完了
    01:10: 开始喝咖啡
    01:20: 喝完了
    02:20: 开始喝咖啡
    02:30: 喝完了

SingleThreadExecutor

第四种线程池是 SingleThreadExecutor，它会使用唯一的线程去执行任务，原理和 FixedThreadPool 是一样的，只不过这里线程只有一个，如果线程在执行任务的过程中发生异常，线程池也会重新创建一个线程来执行后续的任务。这种线程池由于只有一个线程，所以非常适合用于所有任务都需要按被提交的顺序依次执行的场景，而前几种线程池不一定能够保障任务的执行顺序等于被提交的顺序，因为它们是多线程并行执行的。
SingleThreadScheduledExecutor

第五个线程池是 SingleThreadScheduledExecutor，它实际和第三种 ScheduledThreadPool 线程池非常相似，它只是 ScheduledThreadPool 的一个特例，内部只有一个线程，如源码所示：

复制
new ScheduledThreadPoolExecutor(1)

它只是将 ScheduledThreadPool 的核心线程数设置为了 1。

![img](https://s0.lgstatic.com/i/image2/M01/AF/80/CgoB5l3kzomAckv5AAAxf6FCPco696.png)

总结上述的五种线程池，我们以核心线程数、最大线程数，以及线程存活时间三个维度进行对比，如表格所示。

第一个线程池 FixedThreadPool，它的核心线程数和最大线程数都是由构造函数直接传参的，而且它们的值是相等的，所以最大线程数不会超过核心线程数，也就不需要考虑线程回收的问题，如果没有任务可执行，线程仍会在线程池中存活并等待任务。

第二个线程池 CachedThreadPool 的核心线程数是 0，而它的最大线程数是 Integer 的最大值，线程数一般是达不到这么多的，所以如果任务特别多且耗时的话，CachedThreadPool 就会创建非常多的线程来应对。

同理，你可以课后按照同样的方法来分析后面三种线程池的参数，来加深对知识的理解。

ForkJoinPool

![img](https://s0.lgstatic.com/i/image2/M01/AF/A0/CgotOV3kzomAflZxAAB99x9-MzI241.png)

最后，我们来看下第六种线程池 ForkJoinPool，这个线程池是在 JDK 8 加入的，它的名字 ForkJoin 也描述了它的执行机制，主要用法和之前的线程池是相同的，也是把任务交给线程池去执行，线程池中也有任务队列来存放任务。但是 ForkJoinPool 线程池和之前的线程池有两点非常大的不同之处。第一点它非常适合执行可以产生子任务的任务。

如图所示，我们有一个 Task，这个 Task 可以产生三个子任务，三个子任务并行执行完毕后将结果汇总给 Result，比如说主任务需要执行非常繁重的计算任务，我们就可以把计算拆分成三个部分，这三个部分是互不影响相互独立的，这样就可以利用 CPU 的多核优势，并行计算，然后将结果进行汇总。这里面主要涉及两个步骤，第一步是拆分也就是 Fork，第二步是汇总也就是 Join，到这里你应该已经了解到 ForkJoinPool 线程池名字的由来了。

举个例子，比如面试中经常考到的菲波那切数列，你一定非常熟悉，这个数列的特点就是后一项的结果等于前两项的和，第 0 项是 0，第 1 项是 1，那么第 2 项就是 0+1=1，以此类推。我们在写代码时应该首选效率更高的迭代形式或者更高级的乘方或者矩阵公式法等写法，不过假设我们写成了最初版本的递归形式，伪代码如下所示：

复制
if (n <= 1) {
    return n;
 } else {
    Fib f1 = new Fib(n - 1);
    Fib f2 = new Fib(n - 2);
    f1.solve();
    f2.solve();
    number = f1.number + f2.number;
    return number;
 }

你可以看到如果 n<=1 则直接返回 n，如果 n>1 ，先将前一项 f1 的值计算出来，然后往前推两项求出 f2 的值，然后将两值相加得到结果，所以我们看到在求和运算中产生了两个子任务。计算 f(4) 的流程如下图所示。

![img](https://s0.lgstatic.com/i/image2/M01/AF/80/CgoB5l3kzoqAZgXiAACbX2rJCR4889.png)

在计算 f(4) 时需要首先计算出 f(2) 和 f(3)，而同理，计算 f(3) 时又需要计算 f(1) 和 f(2)，以此类推。

![img](https://s0.lgstatic.com/i/image2/M01/AF/A0/CgotOV3kzoqAUlPyAADYOKK1PgM516.png)

这是典型的递归问题，对应到我们的 ForkJoin 模式，如图所示，子任务同样会产生子子任务，最后再逐层汇总，得到最终的结果。

ForkJoinPool 线程池有多种方法可以实现任务的分裂和汇总，其中一种用法如下方代码所示。

复制
class Fibonacci extends RecursiveTask<Integer> { 

    int n;
     
    public Fibonacci(int n) { 
        this.n = n;
    } 
     
    @Override
    public Integer compute() { 
        if (n <= 1) { 
            return n;
        } 
    Fibonacci f1 = new Fibonacci(n - 1);
    f1.fork();
    Fibonacci f2 = new Fibonacci(n - 2);
    f2.fork();
    return f1.join() + f2.join();
    } 
 }

我们看到它首先继承了 RecursiveTask，RecursiveTask 类是对ForkJoinTask 的一个简单的包装，这时我们重写 compute() 方法，当 n<=1 时直接返回，当 n>1 就创建递归任务，也就是 f1 和 f2，然后我们用 fork() 方法分裂任务并分别执行，最后在 return 的时候，使用 join() 方法把结果汇总，这样就实现了任务的分裂和汇总。

复制
public static void main(String[] args) throws ExecutionException, InterruptedException { 
    ForkJoinPool forkJoinPool = new ForkJoinPool();
    for (int i = 0; i < 10; i++) { 
        ForkJoinTask task = forkJoinPool.submit(new Fibonacci(i));
        System.out.println(task.get());
    } 
 }

上面这段代码将会打印出斐波那契数列的第 0 到 9 项的值：

复制
0
1
1
2
3
5
8
13
21
34

这就是 ForkJoinPool 线程池和其他线程池的第一点不同。

我们来看第二点不同，第二点不同之处在于内部结构，之前的线程池所有的线程共用一个队列，但 ForkJoinPool 线程池中每个线程都有自己独立的任务队列，如图所示。

![img](https://s0.lgstatic.com/i/image2/M01/AF/80/CgoB5l3kzouAdfLfAAARK97hw4g233.png)

ForkJoinPool 线程池内部除了有一个共用的任务队列之外，每个线程还有一个对应的双端队列 deque，这时一旦线程中的任务被 Fork 分裂了，分裂出来的子任务放入线程自己的 deque 里，而不是放入公共的任务队列中。如果此时有三个子任务放入线程 t1 的 deque 队列中，对于线程 t1 而言获取任务的成本就降低了，可以直接在自己的任务队列中获取而不必去公共队列中争抢也不会发生阻塞（除了后面会讲到的 steal 情况外），减少了线程间的竞争和切换，是非常高效的。

![img](https://s0.lgstatic.com/i/image2/M01/B0/57/CgotOV3nFTCAKmNtAAES7A18i8M873.png)

我们再考虑一种情况，此时线程有多个，而线程 t1 的任务特别繁重，分裂了数十个子任务，但是 t0 此时却无事可做，它自己的 deque 队列为空，这时为了提高效率，t0 就会想办法帮助 t1 执行任务，这就是“work-stealing”的含义。

双端队列 deque 中，线程 t1 获取任务的逻辑是后进先出，也就是LIFO（Last In Frist Out），而线程 t0 在“steal”偷线程 t1 的 deque 中的任务的逻辑是先进先出，也就是FIFO（Fast In Frist Out），如图所示，图中很好的描述了两个线程使用双端队列分别获取任务的情景。你可以看到，使用 “work-stealing” 算法和双端队列很好地平衡了各线程的负载。

![img](https://s0.lgstatic.com/i/image2/M01/B0/37/CgoB5l3nFSOAFOkbAABvJKvhTKk938.png)

最后，我们用一张全景图来描述 ForkJoinPool 线程池的内部结构，你可以看到 ForkJoinPool 线程池和其他线程池很多地方都是一样的，但重点区别在于它每个线程都有一个自己的双端队列来存储分裂出来的子任务。ForkJoinPool 非常适合用于递归的场景，例如树的遍历、最优路径搜索等场景。



### 第13讲：线程池常用的阻塞队列有哪些？

在本课时我们主要学习线程池内部结构，以及线程池中最常见的阻塞队列类型。
线程池内部结构

![img](https://s0.lgstatic.com/i/image3/M01/54/39/CgpOIF3nUryAHhreAAA4T0DXzFI487.png)

线程池的内部结构主要由四部分组成，如图所示。

    第一部分是线程池管理器，它主要负责管理线程池的创建、销毁、添加任务等管理操作，它是整个线程池的管家。
    
    第二部分是工作线程，也就是图中的线程 t0~t9，这些线程勤勤恳恳地从任务队列中获取任务并执行。
    
    第三部分是任务队列，作为一种缓冲机制，线程池会把当下没有处理的任务放入任务队列中，由于多线程同时从任务队列中获取任务是并发场景，此时就需要任务队列满足线程安全的要求，所以线程池中任务队列采用 BlockingQueue 来保障线程安全。
    
    第四部分是任务，任务要求实现统一的接口，以便工作线程可以处理和执行。

阻塞队列

![img](https://s0.lgstatic.com/i/image3/M01/54/39/Cgq2xl3nUryAJBkpAAA0_WFSrB8184.png)

线程池中的这四个主要组成部分最值得我们关注的就是阻塞队列了，如表格所示，不同的线程池会选用不同的阻塞队列。


表格左侧是线程池，右侧为它们对应的阻塞队列，你可以看到 5 种线程池对应了 3 种阻塞队列，我们接下来对它们进行逐一的介绍。
LinkedBlockingQueue     

对于 FixedThreadPool 和 SingleThreadExector 而言，它们使用的阻塞队列是容量为 Integer.MAX_VALUE 的 LinkedBlockingQueue，可以认为是无界队列。由于 FixedThreadPool 线程池的线程数是固定的，所以没有办法增加特别多的线程来处理任务，这时就需要 LinkedBlockingQueue 这样一个没有容量限制的阻塞队列来存放任务。这里需要注意，由于线程池的任务队列永远不会放满，所以线程池只会创建核心线程数量的线程，所以此时的最大线程数对线程池来说没有意义，因为并不会触发生成多于核心线程数的线程。
SynchronousQueue      

第二种阻塞队列是 SynchronousQueue，对应的线程池是 CachedThreadPool。线程池 CachedThreadPool 的最大线程数是 Integer 的最大值，可以理解为线程数是可以无限扩展的。CachedThreadPool 和上一种线程池 FixedThreadPool 的情况恰恰相反，FixedThreadPool 的情况是阻塞队列的容量是无限的，而这里 CachedThreadPool 是线程数可以无限扩展，所以 CachedThreadPool 线程池并不需要一个任务队列来存储任务，因为一旦有任务被提交就直接转发给线程或者创建新线程来执行，而不需要另外保存它们。


我们自己创建使用 SynchronousQueue 的线程池时，如果不希望任务被拒绝，那么就需要注意设置最大线程数要尽可能大一些，以免发生任务数大于最大线程数时，没办法把任务放到队列中也没有足够线程来执行任务的情况。
DelayedWorkQueue       

第三种阻塞队列是DelayedWorkQueue，它对应的线程池分别是 ScheduledThreadPool 和 SingleThreadScheduledExecutor，这两种线程池的最大特点就是可以延迟执行任务，比如说一定时间后执行任务或是每隔一定的时间执行一次任务。DelayedWorkQueue 的特点是内部元素并不是按照放入的时间排序，而是会按照延迟的时间长短对任务进行排序，内部采用的是“堆”的数据结构。之所以线程池 ScheduledThreadPool 和 SingleThreadScheduledExecutor 选择 DelayedWorkQueue，是因为它们本身正是基于时间执行任务的，而延迟队列正好可以把任务按时间进行排序，方便任务的执行。





### 第14讲：为什么不应该自动创建线程池？

在本课时我们主要学习为什么不应该自动创建线程池，所谓的自动创建线程池就是直接调用 Executors 的各种方法来生成前面学过的常见的线程池，例如 Executors.newCachedThreadPool()。但这样做是有一定风险的，接下来我们就来逐一分析自动创建线程池可能带来哪些问题。
FixedThreadPool

首先我们来看第一种线程池 FixedThreadPool， 它是线程数量固定的线程池，如源码所示，newFixedThreadPool 内部实际还是调用了 ThreadPoolExecutor 构造函数。

复制
public static ExecutorService newFixedThreadPool(int nThreads) { 
    return new ThreadPoolExecutor(nThreads, nThreads,0L, TimeUnit.MILLISECONDS,new LinkedBlockingQueue<Runnable>());
}

通过往构造函数中传参，创建了一个核心线程数和最大线程数相等的线程池，它们的数量也就是我们传入的参数，这里的重点是使用的队列是容量没有上限的 LinkedBlockingQueue，如果我们对任务的处理速度比较慢，那么随着请求的增多，队列中堆积的任务也会越来越多，最终大量堆积的任务会占用大量内存，并发生 OOM ，也就是OutOfMemoryError，这几乎会影响到整个程序，会造成很严重的后果。
SingleThreadExecutor

第二种线程池是 SingleThreadExecutor，我们来分析下创建它的源码。

复制
public static ExecutorService newSingleThreadExecutor() { 
    return new FinalizableDelegatedExecutorService (new ThreadPoolExecutor(1, 1,0L, TimeUnit.MILLISECONDS,new LinkedBlockingQueue<Runnable>()));
}

你可以看出，newSingleThreadExecutor 和 newFixedThreadPool 的原理是一样的，只不过把核心线程数和最大线程数都直接设置成了 1，但是任务队列仍是无界的 LinkedBlockingQueue，所以也会导致同样的问题，也就是当任务堆积时，可能会占用大量的内存并导致 OOM。
CachedThreadPool

第三种线程池是 CachedThreadPool，创建它的源码下所示。

复制
public static ExecutorService newCachedThreadPool() { 
    return new ThreadPoolExecutor(0, Integer.MAX_VALUE,60L, TimeUnit.SECONDS,new SynchronousQueue<Runnable>());
}

这里的 CachedThreadPool 和前面两种线程池不一样的地方在于任务队列使用的是 SynchronousQueue，SynchronousQueue 本身并不存储任务，而是对任务直接进行转发，这本身是没有问题的，但你会发现构造函数的第二个参数被设置成了 Integer.MAX_VALUE，这个参数的含义是最大线程数，所以由于 CachedThreadPool 并不限制线程的数量，当任务数量特别多的时候，就可能会导致创建非常多的线程，最终超过了操作系统的上限而无法创建新线程，或者导致内存不足。
ScheduledThreadPool 和 SingleThreadScheduledExecutor

第四种线程池 ScheduledThreadPool 和第五种线程池 SingleThreadScheduledExecutor 的原理是一样的，创建 ScheduledThreadPool 的源码如下所示。

复制
public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize) { 
    return new ScheduledThreadPoolExecutor(corePoolSize);
}

而这里的 ScheduledThreadPoolExecutor 是 ThreadPoolExecutor 的子类，调用的它的构造方法如下所示。

复制
public ScheduledThreadPoolExecutor(int corePoolSize) { 
    super(corePoolSize, Integer.MAX_VALUE, 0, NANOSECONDS,new DelayedWorkQueue());
}

我们通过源码可以看出，它采用的任务队列是 DelayedWorkQueue，这是一个延迟队列，同时也是一个无界队列，所以和 LinkedBlockingQueue 一样，如果队列中存放过的任务，就可能导致 OOM。

你可以看到，这几种自动创建的线程池都存在风险，相比较而言，我们自己手动创建会更好，因为我们可以更加明确线程池的运行规则，不仅可以选择适合自己的线程数量，更可以在必要的时候拒绝新任务的提交，避免资源耗尽的风险。





### 第15讲：合适的线程数量是多少？CPU 核心数和线程数的关系？

在本课时我们主要学习合适的线程数量是多少，以及 CPU 核心数和线程数的关系。


你可能经常在面试中被问到这两个问题，如果想要很好地回答它们首先你需要了解，我们调整线程池中的线程数量的最主要的目的是为了充分并合理地使用 CPU 和内存等资源，从而最大限度地提高程序的性能。在实际工作中，我们需要根据任务类型的不同选择对应的策略。
CPU 密集型任务

首先，我们来看 CPU 密集型任务，比如加密、解密、压缩、计算等一系列需要大量耗费 CPU 资源的任务。对于这样的任务最佳的线程数为 CPU 核心数的 1~2 倍，如果设置过多的线程数，实际上并不会起到很好的效果。此时假设我们设置的线程数量是 CPU 核心数的 2 倍以上，因为计算任务非常重，会占用大量的 CPU 资源，所以这时 CPU 的每个核心工作基本都是满负荷的，而我们又设置了过多的线程，每个线程都想去利用 CPU 资源来执行自己的任务，这就会造成不必要的上下文切换，此时线程数的增多并没有让性能提升，反而由于线程数量过多会导致性能下降。

 

针对这种情况，我们最好还要同时考虑在同一台机器上还有哪些其他会占用过多 CPU 资源的程序在运行，然后对资源使用做整体的平衡。
耗时 IO 型任务    

第二种任务是耗时 IO 型，比如数据库、文件的读写，网络通信等任务，这种任务的特点是并不会特别消耗 CPU 资源，但是 IO 操作很耗时，总体会占用比较多的时间。对于这种任务最大线程数一般会大于 CPU 核心数很多倍，因为 IO 读写速度相比于 CPU 的速度而言是比较慢的，如果我们设置过少的线程数，就可能导致 CPU 资源的浪费。而如果我们设置更多的线程数，那么当一部分线程正在等待 IO 的时候，它们此时并不需要 CPU 来计算，那么另外的线程便可以利用 CPU 去执行其他的任务，互不影响，这样的话在任务队列中等待的任务就会减少，可以更好地利用资源。

 

《Java并发编程实战》的作者 Brain Goetz 推荐的计算方法：

线程数 = CPU 核心数 *（1+平均等待时间/平均工作时间）

通过这个公式，我们可以计算出一个合理的线程数量，如果任务的平均等待时间长，线程数就随之增加，而如果平均工作时间长，也就是对于我们上面的 CPU 密集型任务，线程数就随之减少。

 

太少的线程数会使得程序整体性能降低，而过多的线程也会消耗内存等其他资源，所以如果想要更准确的话，可以进行压测，监控 JVM 的线程情况以及 CPU 的负载情况，根据实际情况衡量应该创建的线程数，合理并充分利用资源。
结论     

综上所述我们就可以得出一个结论：

    线程的平均工作时间所占比例越高，就需要越少的线程；
    
    线程的平均等待时间所占比例越高，就需要越多的线程；
    
    针对不同的程序，进行对应的实际测试就可以得到最合适的选择。




### 第16讲：如何根据实际需要，定制自己的线程池？

在本课时我们主要学习如何根据自己的实际需求设置线程池的各个参数来定制自己的线程池。
核心线程数

第一个需要设置的参数往往是 corePoolSize 核心线程数，在上一课时我们讲过，合理的线程数量和任务类型，以及 CPU 核心数都有关系，基本结论是线程的平均工作时间所占比例越高，就需要越少的线程；线程的平均等待时间所占比例越高，就需要越多的线程。而对于最大线程数而言，如果我们执行的任务类型不是固定的，比如可能一段时间是 CPU 密集型，另一段时间是 IO 密集型，或是同时有两种任务相互混搭。那么在这种情况下，我们可以把最大线程数设置成核心线程数的几倍，以便应对任务突发情况。当然更好的办法是用不同的线程池执行不同类型的任务，让任务按照类型区分开，而不是混杂在一起，这样就可以按照上一课时估算的线程数或经过压测得到的结果来设置合理的线程数了，达到更好的性能。
阻塞队列

对于阻塞队列这个参数而言，我们可以选择之前介绍过的 LinkedBlockingQueue 或者 SynchronousQueue 或者 DelayedWorkQueue，不过还有一种常用的阻塞队列叫 ArrayBlockingQueue，它也经常被用于线程池中，这种阻塞队列内部是用数组实现的，在新建对象的时候要求传入容量值，且后期不能扩容，所以 ArrayBlockingQueue 的最大的特点就是容量是有限的。这样一来，如果任务队列放满了任务，而且线程数也已经达到了最大值，线程池根据规则就会拒绝新提交的任务，这样一来就可能会产生一定的数据丢失。

但相比于无限增加任务或者线程数导致内存不足，进而导致程序崩溃，数据丢失还是要更好一些的，如果我们使用了 ArrayBlockingQueue 这种阻塞队列，再加上我们限制了最大线程数量，就可以非常有效地防止资源耗尽的情况发生。此时的队列容量大小和 maxPoolSize 是一个 trade-off，如果我们使用容量更大的队列和更小的最大线程数，就可以减少上下文切换带来的开销，但也可能因此降低整体的吞吐量；如果我们的任务是 IO 密集型，则可以选择稍小容量的队列和更大的最大线程数，这样整体的效率就会更高，不过也会带来更多的上下文切换。
线程工厂

对于线程工厂 threadFactory 这个参数，我们可以使用默认的 defaultThreadFactory，也可以传入自定义的有额外能力的线程工厂，因为我们可能有多个线程池，而不同的线程池之间有必要通过不同的名字来进行区分，所以可以传入能根据业务信息进行命名的线程工厂，以便后续可以根据线程名区分不同的业务进而快速定位问题代码。比如可以通过com.google.common.util.concurrent.ThreadFactory

Builder 来实现，如代码所示。

复制
ThreadFactoryBuilder builder = new ThreadFactoryBuilder();
ThreadFactory rpcFactory = builder.setNameFormat("rpc-pool-%d").build();

我们生成了名字为 rpcFactory 的 ThreadFactory，它的 nameFormat 为 "rpc-pool-%d" ，那么它生成的线程的名字是有固定格式的，它生成的线程的名字分别为"rpc-pool-1"，"rpc-pool-2" ，以此类推。
拒绝策略

最后一个参数是拒绝策略，我们可以根据业务需要，选择第 11 讲里的四种拒绝策略之一来使用：AbortPolicy，DiscardPolicy，DiscardOldestPolicy 或者 CallerRunsPolicy。除此之外，我们还可以通过实现 RejectedExecutionHandler 接口来实现自己的拒绝策略，在接口中我们需要实现 rejectedExecution 方法，在 rejectedExecution 方法中，执行例如打印日志、暂存任务、重新执行等自定义的拒绝策略，以便满足业务需求。如代码所示。

复制
private static class CustomRejectionHandler implements RejectedExecutionHandler { 
    @Override
    public void rejectedExecution(Runnable r, ThreadPoolExecutor executor) { 
        //打印日志、暂存任务、重新执行等拒绝策略
    } 
}

总结

所以定制自己的线程池和我们的业务是强相关的，首先我们需要掌握每个参数的含义，以及常见的选项，然后根据实际需要，比如说并发量、内存大小、是否接受任务被拒绝等一系列因素去定制一个非常适合自己业务的线程池，这样既不会导致内存不足，同时又可以用合适数量的线程来保障任务执行的效率，并在拒绝任务时有所记录方便日后进行追溯。



### 第17讲：如何正确关闭线程池？shutdown 和 shutdownNow 的区别？

在本课时我们主要学习如何正确关闭线程池？以及 shutdown() 与 shutdownNow() 方法的区别？首先，我们创建一个线程数固定为 10 的线程池，并且往线程池中提交 100 个任务，如代码所示。

复制
ExecutorService service = Executors.newFixedThreadPool(10);
 for (int i = 0; i < 100; i++) { 
    service.execute(new Task());
 }

那么如果现在我们想关闭该线程池该如何做呢？本课时主要介绍 5 种在 ThreadPoolExecutor 中涉及关闭线程池的方法，如下所示。

    void shutdown;
    boolean isShutdown;
    boolean isTerminated;
    boolean awaitTermination(long timeout, TimeUnit unit) throws InterruptedException;
    List<Runnable> shutdownNow;

下面我们就对这些方法逐一展开。
shutdown()

第一种方法叫作 shutdown()，它可以安全地关闭一个线程池，调用 shutdown() 方法之后线程池并不是立刻就被关闭，因为这时线程池中可能还有很多任务正在被执行，或是任务队列中有大量正在等待被执行的任务，调用 shutdown() 方法后线程池会在执行完正在执行的任务和队列中等待的任务后才彻底关闭。但这并不代表 shutdown() 操作是没有任何效果的，调用 shutdown() 方法后如果还有新的任务被提交，线程池则会根据拒绝策略直接拒绝后续新提交的任务。
isShutdown()

第二个方法叫作 isShutdown()，它可以返回 true 或者 false 来判断线程池是否已经开始了关闭工作，也就是是否执行了 shutdown 或者 shutdownNow 方法。这里需要注意，如果调用 isShutdown() 方法的返回的结果为 true 并不代表线程池此时已经彻底关闭了，这仅仅代表线程池开始了关闭的流程，也就是说，此时可能线程池中依然有线程在执行任务，队列里也可能有等待被执行的任务。
isTerminated()

第三种方法叫作 isTerminated()，这个方法可以检测线程池是否真正“终结”了，这不仅代表线程池已关闭，同时代表线程池中的所有任务都已经都执行完毕了，因为我们刚才说过，调用 shutdown 方法之后，线程池会继续执行里面未完成的任务，不仅包括线程正在执行的任务，还包括正在任务队列中等待的任务。比如此时已经调用了 shutdown 方法，但是有一个线程依然在执行任务，那么此时调用 isShutdown 方法返回的是 true ，而调用 isTerminated 方法返回的便是 false ，因为线程池中还有任务正在在被执行，线程池并没有真正“终结”。直到所有任务都执行完毕了，调用 isTerminated() 方法才会返回 true，这表示线程池已关闭并且线程池内部是空的，所有剩余的任务都执行完毕了。
awaitTermination()

第四个方法叫作 awaitTermination()，它本身并不是用来关闭线程池的，而是主要用来判断线程池状态的。比如我们给 awaitTermination 方法传入的参数是 10 秒，那么它就会陷入 10 秒钟的等待，直到发生以下三种情况之一：

    等待期间（包括进入等待状态之前）线程池已关闭并且所有已提交的任务（包括正在执行的和队列中等待的）都执行完毕，相当于线程池已经“终结”了，方法便会返回 true；
    等待超时时间到后，第一种线程池“终结”的情况始终未发生，方法返回 false；
    等待期间线程被中断，方法会抛出 InterruptedException 异常。

也就是说，调用 awaitTermination 方法后当前线程会尝试等待一段指定的时间，如果在等待时间内，线程池已关闭并且内部的任务都执行完毕了，也就是说线程池真正“终结”了，那么方法就返回 true，否则超时返回 fasle。

我们则可以根据 awaitTermination() 返回的布尔值来判断下一步应该执行的操作。
shutdownNow()

最后一个方法是 shutdownNow()，也是 5 种方法里功能最强大的，它与第一种 shutdown 方法不同之处在于名字中多了一个单词 Now，也就是表示立刻关闭的意思。在执行 shutdownNow 方法之后，首先会给所有线程池中的线程发送 interrupt 中断信号，尝试中断这些任务的执行，然后会将任务队列中正在等待的所有任务转移到一个 List 中并返回，我们可以根据返回的任务 List 来进行一些补救的操作，例如记录在案并在后期重试。shutdownNow() 的源码如下所示。

复制
public List<Runnable> shutdownNow() { 
    List<Runnable> tasks;
    final ReentrantLock mainLock = this.mainLock;
    mainLock.lock();

    try { 
        checkShutdownAccess();
        advanceRunState(STOP);
        interruptWorkers();
        tasks = drainQueue();
    } finally { 
        mainLock.unlock();
    } 
     
    tryTerminate();
    return tasks;
 }

你可以看到源码中有一行 interruptWorkers() 代码，这行代码会让每一个已经启动的线程都中断，这样线程就可以在执行任务期间检测到中断信号并进行相应的处理，提前结束任务。这里需要注意的是，由于 Java 中不推荐强行停止线程的机制的限制，即便我们调用了 shutdownNow 方法，如果被中断的线程对于中断信号不理不睬，那么依然有可能导致任务不会停止。可见我们在开发中落地最佳实践是很重要的，我们自己编写的线程应当具有响应中断信号的能力，正确停止线程的方法在第 2 讲有讲过，应当利用中断信号来协同工作。

在掌握了这 5 种关闭线程池相关的方法之后，我们就可以根据自己的业务需要，选择合适的方法来停止线程池，比如通常我们可以用 shutdown() 方法来关闭，这样可以让已提交的任务都执行完毕，但是如果情况紧急，那我们就可以用 shutdownNow 方法来加快线程池“终结”的速度。





### 第18讲：线程池实现“线程复用”的原理？

在本课时我们主要学习线程复用的原理，以及对线程池的 execute 这个非常重要的方法进行源码解析。
线程复用原理

我们知道线程池会使用固定数量或可变数量的线程来执行任务，但无论是固定数量或可变数量的线程，其线程数量都远远小于任务数量，面对这种情况线程池可以通过线程复用让同一个线程去执行不同的任务，那么线程复用背后的原理是什么呢？

线程池可以把线程和任务进行解耦，线程归线程，任务归任务，摆脱了之前通过 Thread 创建线程时的一个线程必须对应一个任务的限制。在线程池中，同一个线程可以从 BlockingQueue 中不断提取新任务来执行，其核心原理在于线程池对 Thread 进行了封装，并不是每次执行任务都会调用 Thread.start() 来创建新线程，而是让每个线程去执行一个“循环任务”，在这个“循环任务”中，不停地检查是否还有任务等待被执行，如果有则直接去执行这个任务，也就是调用任务的 run 方法，把 run 方法当作和普通方法一样的地位去调用，相当于把每个任务的 run() 方法串联了起来，所以线程数量并不增加。

我们首先来复习一下线程池创建新线程的时机和规则：

![img](https://s0.lgstatic.com/i/image3/M01/58/3A/CgpOIF33U12AesvCAAC4vEMOXQ4044.png)

如流程图所示，当提交任务后，线程池首先会检查当前线程数，如果此时线程数小于核心线程数，比如最开始线程数量为 0，则新建线程并执行任务，随着任务的不断增加，线程数会逐渐增加并达到核心线程数，此时如果仍有任务被不断提交，就会被放入 workQueue 任务队列中，等待核心线程执行完当前任务后重新从 workQueue 中提取正在等待被执行的任务。此时，假设我们的任务特别的多，已经达到了 workQueue 的容量上限，这时线程池就会启动后备力量，也就是 maxPoolSize 最大线程数，线程池会在 corePoolSize 核心线程数的基础上继续创建线程来执行任务，假设任务被不断提交，线程池会持续创建线程直到线程数达到 maxPoolSize 最大线程数，如果依然有任务被提交，这就超过了线程池的最大处理能力，这个时候线程池就会拒绝这些任务，我们可以看到实际上任务进来之后，线程池会逐一判断 corePoolSize 、workQueue 、maxPoolSize ，如果依然不能满足需求，则会拒绝任务。

我们接下来具体看看代码是如何实现的，我们从 execute 方法开始分析，源码如下所示。

复制
public void execute(Runnable command) { 
    if (command == null) 
        throw new NullPointerException();
    int c = ctl.get();
    if (workerCountOf(c) < corePoolSize) { 
        if (addWorker(command, true)) 
            return;
        c = ctl.get();
    } 
    if (isRunning(c) && workQueue.offer(command)) { 
        int recheck = ctl.get();
        if (! isRunning(recheck) && remove(command)) 
            reject(command);
        else if (workerCountOf(recheck) == 0) 
            addWorker(null, false);
    } 
    else if (!addWorker(command, false)) 
        reject(command);
}

线程复用源码解析

这段代码短小精悍，内容丰富，接下来我们具体分析代码中的逻辑，首先看下前几行：

复制
//如果传入的Runnable的空，就抛出异常
if (command == null) 
    throw new NullPointerException();

execute 方法中通过 if 语句判断 command ，也就是  Runnable 任务是否等于 null，如果为 null 就抛出异常。

接下来判断当前线程数是否小于核心线程数，如果小于核心线程数就调用 addWorker() 方法增加一个 Worker，这里的 Worker 就可以理解为一个线程：

复制
if (workerCountOf(c) < corePoolSize) { 
    if (addWorker(command, true)) 
        return;
        c = ctl.get();
}

那 addWorker 方法又是做什么用的呢？addWorker 方法的主要作用是在线程池中创建一个线程并执行第一个参数传入的任务，它的第二个参数是个布尔值，如果布尔值传入 true 代表增加线程时判断当前线程是否少于 corePoolSize，小于则增加新线程，大于等于则不增加；同理，如果传入 false 代表增加线程时判断当前线程是否少于 maxPoolSize，小于则增加新线程，大于等于则不增加，所以这里的布尔值的含义是以核心线程数为界限还是以最大线程数为界限进行是否新增线程的判断。addWorker() 方法如果返回 true 代表添加成功，如果返回 false 代表添加失败。

我们接下来看下一部分代码：

复制
if (isRunning(c) && workQueue.offer(command)) { 
    int recheck = ctl.get();
    if (! isRunning(recheck) && remove(command)) 
        reject(command);
    else if (workerCountOf(recheck) == 0) 
        addWorker(null, false);
}

如果代码执行到这里，说明当前线程数大于或等于核心线程数或者 addWorker 失败了，那么就需要通过 if (isRunning(c) && workQueue.offer(command)) 检查线程池状态是否为 Running，如果线程池状态是 Running 就把任务放入任务队列中，也就是 workQueue.offer(command)。如果线程池已经不处于 Running 状态，说明线程池被关闭，那么就移除刚刚添加到任务队列中的任务，并执行拒绝策略，代码如下所示：

复制
if (! isRunning(recheck) && remove(command)) 
    reject(command);

下面我们再来看后一个 else 分支：

复制
else if (workerCountOf(recheck) == 0) 
    addWorker(null, false);

能进入这个 else 说明前面判断到线程池状态为 Running，那么当任务被添加进来之后就需要防止没有可执行线程的情况发生（比如之前的线程被回收了或意外终止了），所以此时如果检查当前线程数为 0，也就是 workerCountOf**(recheck) == 0，那就执行 addWorker() 方法新建线程。

我们再来看最后一部分代码：

复制
else if (!addWorker(command, false)) 
    reject(command);

执行到这里，说明线程池不是 Running 状态或线程数大于或等于核心线程数并且任务队列已经满了，根据规则，此时需要添加新线程，直到线程数达到“最大线程数”，所以此时就会再次调用 addWorker 方法并将第二个参数传入 false，传入 false 代表增加线程时判断当前线程数是否少于 maxPoolSize，小于则增加新线程，大于等于则不增加，也就是以 maxPoolSize 为上限创建新的 worker；addWorker 方法如果返回 true 代表添加成功，如果返回 false 代表任务添加失败，说明当前线程数已经达到 maxPoolSize，然后执行拒绝策略 reject 方法。如果执行到这里线程池的状态不是 Running，那么 addWorker 会失败并返回 false，所以也会执行拒绝策略 reject 方法。

可以看出，在 execute 方法中，多次调用 addWorker 方法把任务传入，addWorker 方法会添加并启动一个 Worker，这里的 Worker 可以理解为是对 Thread 的包装，Worker 内部有一个 Thread 对象，它正是最终真正执行任务的线程，所以一个 Worker 就对应线程池中的一个线程，addWorker 就代表增加线程。线程复用的逻辑实现主要在 Worker 类中的 run 方法里执行的 runWorker 方法中，简化后的 runWorker 方法代码如下所示。

复制
runWorker(Worker w) {
    Runnable task = w.firstTask;
    while (task != null || (task = getTask()) != null) {
        try {
            task.run();
        } finally {
            task = null;
        }
    }
}

可以看出，实现线程复用的逻辑主要在一个不停循环的 while 循环体中。

    通过取 Worker 的 firstTask 或者通过 getTask 方法从 workQueue 中获取待执行的任务。
    直接调用 task 的 run 方法来执行具体的任务（而不是新建线程）。

在这里，我们找到了最终的实现，通过取 Worker 的 firstTask 或者 getTask方法从 workQueue 中取出了新任务，并直接调用 Runnable 的 run 方法来执行任务，也就是如之前所说的，每个线程都始终在一个大循环中，反复获取任务，然后执行任务，从而实现了线程的复用