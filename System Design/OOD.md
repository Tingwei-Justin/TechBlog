Reading materials

1. Effective java
2. Java source code



naming convent



1. Complete functionality
2. Easy to use (by others) - think about who use your code
   - Clear, elegant, easy to understand, no ambiguity
   - Prevent users from making mistakes
3. Easy to evolve



Motivation of Object oriented programming

1) structured programming : code + data

2) 只想暴露有限的接口 （interface, API)

- API (application programming interface)
- Internal implementation





### Basic concepts

Class: a blueprint for a data type, scheme

Object: a specific realization of any class, instance



Think about whether variables need final, static or ...





Data Encapsulation (封装)：Data abstrraction and access labels

1) provding only essential information to the outside world and hidng their background details

2) Separate interface and implementation

3) Access Labels: public, private, protected, default



why java need package?

provide namespace, specify the class name belongs to which package



why we need private?

1. easy to evolve (we can not make sure the users not use our code, if we want to evolve the code)
2. hide the detail and increase security



好的程序要让用户缩小出错误的空间



How to select appropriate labels?

给尽量低的权限

![image-20200814204615077](../../../Library/Application Support/typora-user-images/image-20200814204615077.png)



### Inheritance

Base class（父类）, derived class (子类)



Employee -> manager/ programmer

List -> ArrayList/Linkedlist



Interface and Abstract Class



abstract class can not instantiate  ( can not new abstract object)

For example, employee is a abstract class, we cannot directly new Employee(), we should extends it as Manager or Programmer...





1. An abstract class provides a common base class implementation to derived classes. Use abstract class for base class if the derived classes **share common implementation.**
2. Interface helps you to **focus on the API signature definition**
3. Multiple inheritance: implement multiple interfaces
4. The relationship between the interface itself and the clas implementing the interface is not necessarily strong





### Polymorphism and Overriding

- Override: a subclass or child class to provide a specific implementation of a method that is already provided by one of its superclasses or parent classes. (run time)

  Method signiture same, but implementation not same.

- Overload: same method name but different input parameters (compile time)



A call to a member function will cause a difference function to be executed depending on the type of object that invokes the function

what it a polymorphism? 给个例子，然后解释概念

```java
Employee e1 = new Programmer(...);

e1.calculateSalary(0.95);
// ((Programmer) e1).program();

Employee e2 = new Manger(...)

e2.calculateSalary(0.85);
```



