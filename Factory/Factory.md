# Factory pattern

## Step:
1. Creat product interface with common functions in products
2. Inplement product class with override common methods in product interface
3. [SIMPLE FACTORY] create factory (static) class to get Types of product(for product class info)

```java
// "static void main" must be defined in a public class.
public class Demo {
    public static void main(String[] args) {
        ShapeFactory sf = new ShapeFactory();
        Shape square = sf.getShape("Square");
        square.draw();
    }
}

interface Shape {
    void draw();
}

class Square implements Shape {
    // Write your code here
    public void draw() {
        System.out.println(" ----");
        System.out.println("|    |");
        System.out.println("|    |");
        System.out.println(" ----");
    }
}

class ShapeFactory {
    /**
     * @param shapeType a string
     * @return Get object of type Shape
     */
    public Shape getShape(String shapeType) {
        // Write your code here
        if (shapeType.equals("Square")) {
            return new Square();
        } else if (shapeType.equals("Triangle")) {
            return new Triangle();
        } else {
            return new Rectangle();
        }
    }
}

/*

class Triangle implements Shape {
    public void draw() {...}
}


class Rectangle implements Shape {
    public void draw() {...}
}

*/
```