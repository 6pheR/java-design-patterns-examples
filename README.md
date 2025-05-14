# Java Design Patterns — Complete Cheatsheet & Examples

---

## 📌 About

This repository provides a complete cheatsheet of the most useful **Java design patterns**, categorized and explained with **clear and practical code examples**.

---

## 🔧 1. Creational Patterns

### ✅ Singleton

```java
class Singleton {
    private static Singleton instance;
    private Singleton() {}
    public static Singleton getInstance() {
        if (instance == null) instance = new Singleton();
        return instance;
    }
}
```

### ✅ Builder

```java
class Car {
    private String engine;
    private int wheels;
    public static class Builder {
        private String engine;
        private int wheels;
        public Builder setEngine(String e) { engine = e; return this; }
        public Builder setWheels(int w) { wheels = w; return this; }
        public Car build() {
            Car c = new Car();
            c.engine = engine; c.wheels = wheels;
            return c;
        }
    }
}
```

### ✅ Factory Method

```java
interface Animal { void speak(); }
class Dog implements Animal {
    public void speak() { System.out.println("Woof!"); }
}
class AnimalFactory {
    public static Animal createAnimal(String type) {
        return "dog".equals(type) ? new Dog() : null;
    }
}
```

---

## 🧱 2. Structural Patterns

### ✅ Adapter

```java
class OldPrinter {
    void printOld(String msg) { System.out.println(msg); }
}
interface NewPrinter { void print(String msg); }
class AdapterPrinter implements NewPrinter {
    OldPrinter old = new OldPrinter();
    public void print(String msg) { old.printOld(msg); }
}
```

### ✅ Decorator

```java
interface Coffee {
    String getDescription();
    double cost();
}
class SimpleCoffee implements Coffee {
    public String getDescription() { return "Simple"; }
    public double cost() { return 5; }
}
class MilkDecorator implements Coffee {
    private Coffee coffee;
    public MilkDecorator(Coffee c) { coffee = c; }
    public String getDescription() { return coffee.getDescription() + ", Milk"; }
    public double cost() { return coffee.cost() + 1.5; }
}
```

### ✅ Composite

```java
interface Component { void show(); }
class Leaf implements Component {
    String name;
    public Leaf(String n) { name = n; }
    public void show() { System.out.println(name); }
}
class Composite implements Component {
    List<Component> children = new ArrayList<>();
    public void add(Component c) { children.add(c); }
    public void show() {
        for (Component c : children) c.show();
    }
}
```

### ✅ Proxy

```java
interface Service { void request(); }
class RealService implements Service {
    public void request() { System.out.println("Real service"); }
}
class ProxyService implements Service {
    private RealService real = new RealService();
    public void request() {
        System.out.println("Via proxy"); real.request();
    }
}
```

---

## 🤖 3. Behavioral Patterns

### ✅ Strategy

```java
interface PaymentStrategy { void pay(int amount); }
class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) { System.out.println("Credit: " + amount); }
}
class ShoppingCart {
    PaymentStrategy strategy;
    public ShoppingCart(PaymentStrategy s) { strategy = s; }
    public void checkout(int amount) { strategy.pay(amount); }
}
```

### ✅ Observer

```java
interface Observer { void update(String msg); }
class EmailNotifier implements Observer {
    public void update(String msg) { System.out.println("Email: " + msg); }
}
class Subject {
    List<Observer> observers = new ArrayList<>();
    public void add(Observer o) { observers.add(o); }
    public void notifyAll(String msg) {
        for (Observer o : observers) o.update(msg);
    }
}
```

### ✅ Command

```java
interface Command { void execute(); }
class Light { void turnOn() { System.out.println("On"); } }
class LightOnCommand implements Command {
    Light light;
    public LightOnCommand(Light l) { light = l; }
    public void execute() { light.turnOn(); }
}
class Remote {
    Command command;
    public void set(Command c) { command = c; }
    public void press() { command.execute(); }
}
```

### ✅ State

```java
interface State { void handle(); }
class OpenState implements State {
    public void handle() { System.out.println("Open"); }
}
class ClosedState implements State {
    public void handle() { System.out.println("Closed"); }
}
class Door {
    State state;
    public void set(State s) { state = s; }
    public void request() { state.handle(); }
}
```

### ✅ Template Method

```java
abstract class Game {
    public final void play() {
        start(); playTurn(); end();
    }
    abstract void start();
    abstract void playTurn();
    abstract void end();
}
class Chess extends Game {
    void start() { System.out.println("Start Chess"); }
    void playTurn() { System.out.println("Playing..."); }
    void end() { System.out.println("Game Over"); }
}
```

### ✅ Mediator

```java
interface Mediator {
    void notify(Component sender, String event);
}
abstract class Component {
    protected Mediator mediator;
    public Component(Mediator m) { mediator = m; }
}
class Button extends Component {
    public Button(Mediator m) { super(m); }
    public void click() {
        System.out.println("Button Clicked");
        mediator.notify(this, "click");
    }
}
class TextBox extends Component {
    public TextBox(Mediator m) { super(m); }
    public void show() { System.out.println("Textbox visible"); }
}
```

---

## 👤 Author

[CipheR_](https://github.com/your-username)

---

⭐️ **If this project helped you, feel free to give it a star!**
