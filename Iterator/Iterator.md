# Iterator

## Comment:
0. Achieve an array iterator
1. Iterator duplicates the java Iterator, so I rename with IteratorP(ersonal)
2. Reference: https://www.runoob.com/design-pattern/iterator-pattern.html

## 介绍
- 意图：提供一种方法顺序访问一个聚合对象中各个元素, 而又无须暴露该对象的内部表示。
- 主要解决：不同的方式来遍历整个整合对象。

## 优点： 
1. 它支持以不同的方式遍历一个聚合对象。 
2. 迭代器简化了聚合类。 
3. 在同一个聚合上可以有多个遍历。 
4. 在迭代器模式中，增加新的聚合类和迭代器类都很方便，无须修改原有代码。

## 缺点：
由于迭代器模式将存储数据和遍历数据的职责分离，增加新的聚合类需要对应增加新的迭代器类，类的个数成对增加，这在一定程度上增加了系统的复杂性。

## 使用场景： 
1. 访问一个聚合对象的内容而无须暴露它的内部表示。 
2. 需要为聚合对象提供多种遍历方式。 
3. 为遍历不同的聚合结构提供一个统一的接口。

## 注意事项：
迭代器模式就是分离了集合对象的遍历行为，抽象出一个迭代器类来负责，这样既可以做到不暴露集合的内部结构，又可让外部代码透明地访问集合内部的数据。

```java

public class Main {
    public static void main(String[] args) {
      String[] names = {"Robert" , "John" ,"Julie" , "Lora"};
      NameRepository namesRepository = new NameRepository(names);
 
      for(IteratorP iter = namesRepository.getIterator(); iter.hasNext();){
         String name = (String) iter.next();
         System.out.println("Name : " + name);
      } 
    }
}

interface IteratorP {
   public boolean hasNext();
   public Object next();
}

interface Container {
   public IteratorP getIterator();
}

class StringArrayIterator implements IteratorP{
    NameRepository nameRepository;
    int index = 0;
    
    public StringArrayIterator(NameRepository nameRepository){
        this.nameRepository = nameRepository;      
    }

    @Override
    public boolean hasNext(){
        if(index < nameRepository.getNames().length){
            return true;
        }
        return false;
    }

    @Override
    public Object next(){
        if(index < nameRepository.getNames().length){
            return nameRepository.getNames()[index++];
        }
        return null;
    } 
}

class NameRepository implements Container {  
    private String[] names;
    public NameRepository(String[] names) {
        this.names = names;
    }
    
    public String[] getNames() {
        return names;
    }
    
    @Override 
    public IteratorP getIterator() { 
        return new StringArrayIterator(this);
    }  
}

```
