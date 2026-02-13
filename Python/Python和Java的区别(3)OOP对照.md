这份是**专门给 Java 工程师**准备的：
# Java OOP → Python OOP 逐行对照速查表
（复制到 IDE 里对照看，半天就能顺过来）
OOP（Object-Oriented Programming）是面向对象编程的缩写，是一种程序设计思想。

---

## 1. 定义类
### Java
```java
public class Person {

}
```

### Python
```python
class Person:
    pass
```

---

## 2. 成员变量 & 构造方法
### Java
```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

### Python
```python
class Person:
    def __init__(self, name: str, age: int):
        self.name = name   # 公开属性
        self.age = age
```
- 构造：`__init__`
- 必须带 `self` = Java 的 `this`
- 没有真正的 `private`

---

## 3. 成员方法
### Java
```java
public void sayHello() {
    System.out.println("Hello, I'm " + name);
}
```

### Python
```python
def say_hello(self):
    print(f"Hello, I'm {self.name}")
```

---

## 4. 私有属性 / 方法（约定）
### Java
```java
private String secret;

private void secretMethod() {
}
```

### Python
```python
self._secret = "约定私有"

def _secret_method(self):
    pass
```
- 一个下划线：**大家别碰**
- 两个下划线 `__secret`：名字改写，不是真安全

---

## 5. Getter / Setter
### Java
```java
public String getName() {
    return name;
}

public void setName(String name) {
    this.name = name;
}
```

### Python（标准写法）
```python
@property
def name(self):
    return self._name

@name.setter
def name(self, value):
    self._name = value
```

---

## 6. 静态方法 & 类方法
### Java
```java
public static void staticMethod() {
}
```

### Python
```python
@staticmethod
def static_method():
    pass

@classmethod
def class_method(cls):
    # cls 是类本身
    pass
```

---

## 7. 继承
### Java
```java
class Student extends Person {
    public Student(String name, int age, String school) {
        super(name, age);
        this.school = school;
    }
}
```

### Python
```python
class Student(Person):
    def __init__(self, name: str, age: int, school: str):
        super().__init__(name, age)
        self.school = school
```

---

## 8. 方法重写
### Java
```java
@Override
public void sayHello() {
    super.sayHello();
    System.out.println("From Student");
}
```

### Python
```python
def say_hello(self):
    super().say_hello()
    print("From Student")
```
- 没有 `@Override`，名字一样就是重写

---

## 9. 创建对象
### Java
```java
Person p = new Person("Tom", 20);
p.sayHello();
```

### Python
```python
p = Person("Tom", 20)
p.say_hello()
```

---

## 10. 访问控制速记
| Java         | Python               | 含义               |
| ------------ | -------------------- | ------------------ |
| public       | `self.name`          | 公开               |
| protected    | `self._name`         | 子类可用，外部别用 |
| private      | `self.__name`        | 名字改写，防意外   |

---

## 11. 完整对照示例（可直接运行）
### Java
```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void sayHello() {
        System.out.println("Hi " + name);
    }

    public static void staticFunc() {
        System.out.println("static");
    }
}

class Student extends Person {
    private String school;

    public Student(String name, int age, String school) {
        super(name, age);
        this.school = school;
    }

    @Override
    public void sayHello() {
        super.sayHello();
        System.out.println("School: " + school);
    }
}
```

### Python
```python
class Person:
    def __init__(self, name: str, age: int):
        self.name = name
        self.age = age

    def say_hello(self):
        print(f"Hi {self.name}")

    @staticmethod
    def static_func():
        print("static")

class Student(Person):
    def __init__(self, name: str, age: int, school: str):
        super().__init__(name, age)
        self.school = school

    def say_hello(self):
        super().say_hello()
        print(f"School: {self.school}")
```

---