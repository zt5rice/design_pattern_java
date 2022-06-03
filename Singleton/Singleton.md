# Singleton





# Methods

1. lazy loading
``` java
public class Main {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2);
    }
}

class Singleton {
    private static Singleton instance;
    private Singleton(){}
    
    public static Singleton getInstance() { // thread safe if change line to: public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}


```

2. Hungry
``` java
public class Main {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2);
    }
}

class Singleton {
    private static Singleton instance = new Singleton();
    private Singleton(){}
    
    public static Singleton getInstance() {
        return instance;
    }
}

```

3. Double-checked Loading
``` java
public class Main {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2);
    }
}

class Singleton {
    private volatile static Singleton instance;
    private Singleton(){}
    
    public synchronized static Singleton getInstance() {
        if (instance == null) {
            synchronized(Singleton.class) {
                if (instance == null) {
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}

```

4. Static inner class
``` java
public class Main {
    public static void main(String[] args) {
        Singleton s1 = Singleton.getInstance();
        Singleton s2 = Singleton.getInstance();
        System.out.println(s1 == s2);
    }
}

class Singleton {
    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
    private Singleton(){}
    
    public static final Singleton getInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

5. Enum
``` java
public class Main {
    public static void main(String[] args) {
        Singleton s1 = Singleton.INSTANCE;
        Singleton s2 = Singleton.INSTANCE;
        System.out.println(s1 == s2);
    }
}

enum Singleton {
    INSTANCE;
    public void whatevermethod(){return;};
}

```