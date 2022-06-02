# Template Pattern

## Summary
Concrete class extends abstract class
```java
public abstract class Game {
   abstract void initialize(); // require children's implementation
   abstract void startPlay();
   abstract void endPlay();
 
   //模板
   public final void play(){ // combinations of children's implementation
      //初始化游戏
      initialize();
      //开始游戏
      startPlay();
      //结束游戏
      endPlay();
   }
}

```

# Example
Screen print
```
+------------+
|Hello,world.|
|Hello,world.|
|Hello,world.|
|Hello,world.|
|Hello,world.|
+------------+


```

```java
// "static void main" must be defined in a public class.
public class Main {
    public static void main(String[] args) {
        AbstractDisplay d1 = new StringDisplay("Hello,world.");
        d1.display();
    }
}

abstract class AbstractDisplay {
    public abstract void open();    
    public abstract void print();
    public abstract void close();
    public final void display() {
        open();
        for (int i = 0; i < 5; i++) {
            print();
        }
        close();
    }
}

class StringDisplay extends AbstractDisplay {
    private String string;
    private int width;
    public StringDisplay(String string) {
        this.string = string;
        this.width = string.getBytes().length;
    }
    
    public void open() {
        printLine();
    }
    
    public void print() {
        System.out.println("|" + string + "|");
    }
    
    public void close() {
         printLine();       
    }
    
    private void printLine() {
        System.out.print("+");
        for (int i = 0; i < width; i++) {
            System.out.print("-");
        }        
        System.out.println("+");
    }
}

```