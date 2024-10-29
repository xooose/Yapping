---
date: 2024-01-31
authors:
  - Xooose
categories:
    - Programming
tags:
    - Tutorial
    - C#
---

<figure markdown="span">
  ![alt text](images/Classicube/cover.png)
  <figcaption>
  Test
  </figcaption>
</figure>

<!-- more -->

解释器的作用是接受指定的输入，执行相应的过程。

解释流程
词法分析。
语法分析。
语义分析。
解释执行。可以看到，解释器和编译器的实现都包括解析器，即需要实现源代码到抽象语法树的转换，区别在于最终如何处理抽象语法树。一般解释器的实现中，抽象语法树的每个节点都会存在一个eval方法，eval方法将会递归调用该节点的子节点的eval方法，并根据它们的返回值计算自身的返回值，因此我们只需要调用抽象语法树根节点的eval方法就可以执行这颗树所代表的动作。
一般如果想要自己实现简易的解释器的话，以这种AST解释器为目标或许是个不错的选择。而实际上许多主流的语言（如Java、JavaScript）的内部实现使用的并不是AST解释器，而是字节码解释器。以JavaScript（V8引擎）为例，它会首先把JavaScript解析成AST、再生成对应的字节码、之后再通过内部的Ignition解释器对字节码解释执行。

相较于使用编译器直接生成二进制产物，交由CPU直接加载执行；使用解释器的本质是CPU会先加载解释器自身的二进制代码，执行的过程中会把输入的内容解释成二进制代码再给CPU执行；如果我们使用解释器去实现解释器，比如使用JavaScript（V8引擎）实现Python，如node interpreter.js source.py，本质上来说CPU会先加载V8的代码，之后V8会把interpreter.js解释成二进制代码交给CPU执行，这段代码的执行又会把source.py解释成二进制代码交给CPU执行，由此可见为了执行这样的一段代码我们启用了两个解释器，效率明显是比较低的。

假设我们使用Rust实现字节码的解释器，从实现上看我们实现了字节码到Rust的解释，但考虑到Rust代码会被编译成二进制，所以从运行上看我们实现的是字节码到机器码的解释
假设我们使用Rust实现JavaScript的解释器，从实现上看我们实现了JavaScript到Rust的解释，但考虑到Rust代码会被编译成二进制，所以从运行上看我们实现的是JavaScript到机器码的解释
假设我们使用JavaScript实现Python的解释器，从实现上看我们实现了Python到JavaScript的解释，但考虑到JavaScript代码会被解释成二进制，所以从运行上看我们实现的是Python到机器码的解释