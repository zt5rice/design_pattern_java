# Adapter

## Type 1. Adapter implemented through Interface

## Convert 220V to 110V power
### Result
```
(220V 10W) now in 110V
```

### Code
1. Observe Adaptee
2. Encapsulate desired method into Target interface
3. In adapter, extends Adaptee and implements interface. In constructor of adapter, pass the input to adaptee through super.
4. In client, generate Adapter object in Target interface. Then it's fine to call Adaptee through Target method.

```java
public class Client {
    public static void main(String[] args) {
        Target adapterImp = new Adapter("10W");
        adapterImp.use110Vpower();
    }
}

class Adaptee {
    private String string;
    public Adaptee(String string) {
        this.string = string;
    }
    
    public void use220Vpower() {
        System.out.print("(220V " + string + ")");
    }
}

interface Target {
    public abstract void use110Vpower();
}

class Adapter extends Adaptee implements Target {
    public Adapter(String string) {
        super(string);
    }
    public void use110Vpower() {
        use220Vpower();
        System.out.println(" now in 110V");
    }
}

```

## Type 2. Adapter implemented through Object
### Result
```
(220V 10W) now in 110V
```
### Code
1. Observe Adaptee
2. Encapsulate desired method of Adaptee as abstract method in Abstract class Target
3. In adapter, set a Adpatee attribute.
   Use adapter constructor to generate Adaptee object
4. In client, generate Adapter object with input. Use adapter object to call adaptee object.

```java
public class Client {
    public static void main(String[] args) {
        Adapter adapterImp = new Adapter("10W");
        adapterImp.use110Vpower();
    }
}

class Adaptee {
    private String string;
    public Adaptee(String string) {
        this.string = string;
    }
    
    public void use220Vpower() {
        System.out.print("(220V " + string + ")");
    }
}

abstract class Target {
    public abstract void use110Vpower();
}

class Adapter extends Target {
    private Adaptee adaptee;
    
    public Adapter(String string) {
        this.adaptee = new Adaptee(string);
    }
    public void use110Vpower() {
        adaptee.use220Vpower();
        System.out.println(" now in 110V");
    }
}

```