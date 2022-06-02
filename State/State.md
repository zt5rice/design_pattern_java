



- 主要解决：对象的行为依赖于它的状态（属性），并且可以根据它的状态改变而改变它的相关行为。

- 何时使用：代码中包含大量与对象状态有关的条件语句。

- 如何解决：将各种具体的状态类抽象出来。

- 关键代码：
1. 通常命令模式的接口中只有一个方法。而状态模式的接口中有一个或者多个方法。
2. 而且，状态模式的实现类的方法，一般返回值，或者是改变实例变量的值。也就是说，状态模式一般和对象的状态有关。实现类的方法有不同的功能，覆盖接口中的方法。状态模式和命令模式一样，也可以用于消除 if...else 等条件选择语句。

- 优点： 
1. 封装了转换规则。 
2. 枚举可能的状态，在枚举状态之前需要确定状态种类。 
3. 将所有与某个状态有关的行为放到一个类中，并且可以方便地增加新的状态，只需要改变对象状态即可改变对象的行为。 
4. 允许状态转换逻辑与状态对象合成一体，而不是某一个巨大的条件语句块。 
5. 可以让多个环境对象共享一个状态对象，从而减少系统中对象的个数。

缺点： 
1. 状态模式的使用必然会增加系统类和对象的个数。 
2. 状态模式的结构与实现都较为复杂，如果使用不当将导致程序结构和代码的混乱。 
3. 状态模式对"开闭原则"的支持并不太好

```java
public class Demo {
    public static void main(String[] args) {
      Context context = new Context();
 
      StartState startState = new StartState();
      startState.doAction(context);
 
      System.out.println(context.getState().toString());
 
      StopState stopState = new StopState();
      stopState.doAction(context);
 
      System.out.println(context.getState().toString());
   }       
}


//1.
interface State {
   public void doAction(Context context);
}

//2.
class StartState implements State {
   public void doAction(Context context) {
      System.out.println("Player is in start state");
      context.setState(this); 
   }
   public String toString(){
      return "Start State";
   }
}

class StopState implements State {
   public void doAction(Context context) {
      System.out.println("Player is in stop state");
      context.setState(this); 
   }
   public String toString(){
      return "Stop State";
   }
}

//3.
class Context {
   private State state; 
   public Context(){
      state = null;
   } 
   public void setState(State state){
      this.state = state;     
   } 
   public State getState(){
      return state;
   }
}

```
REF: 
1. https://www.runoob.com/design-pattern/state-pattern.html
2. https://www.runoob.com/w3cnote/state-vs-strategy.html

