###### CoroutineScope

可以理解为协程本身，是一个接口，其包含了CoroutineContext，即协程包含了上下文；

###### GlobalScope

直接实现CoroutineScope接口，同样表示协程本身

###### CoroutineContext

协程上下文环境，是一些元素的集合，主要包括Job和CoroutineDispatcher元素，可以代表一个协程的场景

###### EmptyCoroutineContext

空的协程上下文

###### CoroutineDispatcher

协程调度器，决定协程所在的线程或者线程池，它可以指定协程运行于特定的一个线程，一个线程池或者不指定任何线程，目前框架中有三种实现：Dispatcher.Default、Dispatcher.IO、Dispatcher.Main、Dispatcher.Unconfined；其中Unconfined就是不指定线程

###### Job&Deferred

都是接口，其具体实现

Deferred继承于Job，Job表示一个任务，封装了协程中要执行的代码，Job执行完并没有返回值(通过)，Deferred执行完则有返回值

:join()       让当前线程等待对应协程对象执行完



##### Coroutine Builders

称为协程构建器，通常有以下几种Builder

###### GlobalScope.launch{}

函数来构建Coroutine Builders，用来创建一个协程，该方法并不会阻塞当前线程，Kotlin中还有其它几种Builder，同样负责创建协程，{}内就是协程要执行的具体逻辑

###### async{}

CoroutineScope.async{}可以实现于launch builder一样的效果，在后台创建一个新的协程，唯一区别就是有返回值，因为CoroutineScope返回的类型是Deferrd类型



###### runBlocking()

其它协程构建器，公共方法，创建一个新的协程同时阻塞当前线程，直到线程结束，该方法很少在协程中使用

###### withContext()

其它协程构建器，公共方法，不会创建新的协程，在指定协程上运行挂起的代码块，并挂起该协程直至代码块运行完成



###### delay()

函数只会阻塞当前协程，不会阻塞当前线程的执行

###### coroutineScope()













通过跟进代码可以发现，GlobalScope继承了CorutineScope类，并重写了coroutineContext成员变量。







CoroutineScope是一个接口，其中只有coroutineContext这个成员变量，通过注释可知，框架不建议直接访问该属性，而是通过Job访问该属性









CoroutineScope是一个上下文，并且不建议直接访问该字段