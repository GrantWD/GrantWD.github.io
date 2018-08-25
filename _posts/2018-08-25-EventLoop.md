---
layout: post
title: 'Event Loop'
subtitle: '并发模型与事件循环'
date: 2018-08-25
categories: JavaScript
tags: JavaScript
---

## 浏览器中的异步
JavaScript是单线程的，同一时间只能做一件事。因为JavaSctipt主要是用来操作DOM的，如果是多线程的，浏览器，就不知道该做哪个了。虽然是单线程的，但是可以模拟多线程。

#### 异步
异步：不会阻塞主线程，等待主线程的代码执行完毕后才会执行异步的代码。常见的异步操作```callback（DOM事件）,setTimeout,setInterval,Promise等等```

js中分为```堆内存(heap)```和```栈内存(stack)```,堆内存中保存了声明的```object```类型的数据，栈内存中保存了```基本数据类型，对象的引用```,以及```函数执行时的运行空间(需要了解)```同步的代码放在执行栈中，异步代码，在浏览器中会将异步代码放到一个队列中，等待执行栈中的所有代码执行完毕后，才会执行队列中的代码。
```javascript
	console.log(1);
	setTimeout(()=>{
		console.log(2)
	},0)
	console.log(3);
	// 上面代码的打印结果是1 3 2，虽然设置了是0秒后执行，但是还是会在主线程的代码执行完毕后再执行
```
#### Promise异步
异步任务分为```微任务(microtask)```和```宏任务(task)```,执行的顺序是```执行栈中的代码=>微任务=>宏任务```。

- 微任务(microtask)
	- promise MutationObserver等等
- 宏任务(task)
	- setTimeout setInterval setImmediate messageChannel
当```执行栈```中的任务执行完毕后，会在执行```宏任务队列```之前在```微任务队列```中有没有任务,并且在每次执行宏任务队列中的每个任务之前都会在```微任务队列 ```中查看有没有添加新的微任务，如果没有继续执行```宏任务```,如果有那么就执行```微任务队列```。

<!-- ## Node中的Event Loop
Node.js是基于V8引擎(VM虚拟机)的js运行环境,就是让js可以在服务器端运行,但是Node中的Event Loop是用libuv模拟的，他将不同的任务分配给不同的线程，形成一个Event Loop ,以异步的方式将任务的执行结果返回给V8引擎。具体的请看libuv Node文档,Node还不是很熟悉见谅!!! -->


