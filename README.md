# Iterator

## Comment:
0. Achieve an array iterator
1. Iterator duplicates the java Iterator, so I rename with IteratorP(ersonal)
2. Reference: https://www.runoob.com/design-pattern/iterator-pattern.html

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
