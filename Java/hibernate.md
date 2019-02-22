#### Hibernate中SessionFactory和Session是线程安全的吗？这两个线程是否能够共享同一个Session？
SessionFactory:
* `SessionFactory`对应Hibernate的一个数据存储的概念，它是`线程安全`的，`可以被多个线程并发访问`。
* SessionFactory一般只会在启动的时候构建。
* 对于应用程序，最好将SessionFactory通过单例模式进行封装以便于访问。

Session:
* `Session`是一个轻量级`非线程安全`的对象（线程间`不能共享`session），它表示与数据库进行交互的一个工作单元。
* Session是由SessionFactory创建的，在任务完成之后它会被关闭。
* Session是持久层服务对外提供的主要接口。Session会延迟获取数据库连接（也就是在需要的时候才会获取）。
* 为了避免创建太多的session，可以使用ThreadLocal将session和当前线程绑定在一起，这样可以让同一个线程获得的总是同一个session。
* Hibernate 3中SessionFactory的getCurrentSession()方法就可以做到。
