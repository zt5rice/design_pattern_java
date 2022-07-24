


``` java
public class Main {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        coffee = new WithMilk(coffee);
        System.out.println(coffee.getCosts());
        System.out.println(coffee.getIngredients());
    }
}


// 创建一个接口：
interface Coffee {
    public double getCosts();
    public String getIngredients();
}

// 创建实现接口的实体类
class SimpleCoffee implements Coffee { 
	///@Override
	public double getCosts() {
		// TODO Auto-generated method stub
		return 2;
	}
	//@Override
	public String getIngredients() {
		// TODO Auto-generated method stub
		return "Plain Coffee";
	}
}

// 创建实现了  接口的抽象装饰类。
abstract class CoffeeDecorator implements Coffee {
    protected final Coffee decoratedCoffee;
    
    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }
    
    public double getCosts() {
        return decoratedCoffee.getCosts();
    }
    
    public String getIngredients() {
        return decoratedCoffee.getIngredients();
    }
}

// 使用 抽象装饰类 来装饰 对象。
class WithMilk extends CoffeeDecorator {
    public WithMilk(Coffee coffee) {
        super(coffee);
    }
    public double getCosts() {
        return super.getCosts() + 0.5;
    }
    public String getIngredients() {
        return super.getIngredients() + ", Milk";
    }
}
```