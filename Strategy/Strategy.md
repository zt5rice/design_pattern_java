

# Steps
1. Use Strategy interface to encapsulate all common methods;
2. implements all concrete strategies

3. In context class, initiate with strategy, write method to execute methods from input strategy.

``` java
// "static void main" must be defined in a public class.
public class Demo {
    public static void main(String[] args) {
      Context context = new Context(new OperationAdd());    
      System.out.println("10 + 5 = " + context.executeStrategy(10, 5));
 
      context = new Context(new OperationSubtract());      
      System.out.println("10 - 5 = " + context.executeStrategy(10, 5));        
    }
}

interface Strategy {
   public int doOperation(int num1, int num2);
}

class OperationAdd implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 + num2;
   }
}

class OperationSubtract implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 - num2;
   }
}

class Context {
   private Strategy strategy;
 
   public Context(Strategy strategy){
      this.strategy = strategy;
   }
 
   public int executeStrategy(int num1, int num2){
      return strategy.doOperation(num1, num2);
   }
}



```