# 函数式编程之我知我见

---

**函数式编程**是一种编程范式，就是跟我们上大学的时候，大学老师总是挂在嘴边的“面向对象”，“面向过程”等等是一个东东。
既然是**函数式编程**编程，那么“函数”是少不了的了。能够实现“函数式编程”的语言，函数必须是该语言的“一等公民”，即函数是可以直接声明调用的，而不是需要在类中声明成方法（没错，我说的是Java）。
例如，python中：
```python
def f(x):
     return x+3
g=f
print g(4)
#output  7
```
例子中，f直接就代表了函数f(x)，可以赋值给其他的变量。这就是“一等公民”。
当然，仅仅是满足这一点是不行，基本需要如下几点：
> 1,函数是“一等公民”
> 2,函数可以作为函数的返回值
> 3,函数可以做函数的参数

---
##高阶函数
前面已经说过，**函数式编程**中函数是可以作为函数的返回值和参数的，那么满足这两个条件之一的函数，就是**高阶函数**。鉴于数学和计算机科学的基友性质，函数和高阶函数的概念都是从数学中引申而来的。举一个在令我们头疼的微积分课的例子，有个老是出现的玩意就是高阶函数，那玩意叫**导数**。
python高阶函数示例：
```python
def f(x):
    return x + 3

def g(function, x):
    return function(x) * function(x)

print g(f, 7)
```
--
##闭包
曾经面试官让我解释“闭包”，我只说一句“**里面的可以用外面的，外面的不能用里面的**。”用更通俗易懂的话来说，就是“**你的就是我的，我的还是我的。**”
这里牵扯出一个作用域的问题，就是我们在写很多语言的时候，那个“**{}**”（大python中用缩进）。
```python
def f(x):
     def g(x):
          return x+3
     return x

print g(4)
```
会输出什么？会是7吗？
No,会报错。找不到g函数，只有在函数f的作用域（函数体内）才能调用它。
但是，函数式编程的时候，是可以将函数作为返回值的，所以可以通过这样的方式来使用：
```python
def f():
     def g(x):
          return x+3
     return g

p=f()
print p(4)
#output 7
```
ok，完了。就这样完了？没错，太过深奥的概念不需要说太多，说了有时候也无法理解。了解了函数式编程基本概念和高阶函数，就可以非常飘逸的运用起来，比如“装饰设计”。

---
##装饰设计
在日常工作中，我们写好了一个函数，结果产品经理屁颠屁颠过来说，改需求了（万恶产品狗）！这个函数运行时得加上日志，那么没经验的时候的做法，就是苦逼到这个函数里面改代码，结果牵一发而动全身，整个模块都要改！！！
设计模式中装饰模式，可以很灵活的解决这个问题。如果利用高阶函数的话，则可以更好的实现装饰模式。
```python
def f(x):
      return x+3

def logo(f,x):
      print "函数f开始计算"
      f(x)
      print "函数f计算完毕"

print logo(f,3)
#output
函数f开始计算
6
函数f计算完毕
```
