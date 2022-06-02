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

Simple factory pattern violates the Open-Close principle. It can be improved if factory interface is used instead.

```java
/**
 Print:: Square
 Print:: Triangle
*/
/********factory folder************/
interface Shape {
    void draw();
}

interface Factory {
    public Shape getShape();
}

/********factory implementation folder************/
class Square implements Shape {
    public void draw() {
        System.out.println(" Print:: Square");
    }
}

class Triangle implements Shape {
    public void draw() {
        System.out.println(" Print:: Triangle");
    }
}

class SquareShapeFactory implements Factory{
    public Shape getShape() {
      return new Square();
    }
}

class TriangleShapeFactory implements Factory{
    public Shape getShape() {
      return new Triangle();
    }
}

/********Demo************/
public class Demo {
    public static void main(String[] args) {
        Factory squarefactory = new SquareShapeFactory();
        squarefactory.getShape().draw();
        Factory trianglefactory = new TriangleShapeFactory ();
        trianglefactory.getShape().draw();

    }
}
```

## Abstract factory
See reference: https://github.com/JamesZBL/java_design_patterns/tree/master/abstract-factory
