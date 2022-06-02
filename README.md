

```java
// "static void main" must be defined in a public class.
// not working
/*
Line 26: error: BookShelf is not abstract and does not override abstract method interator() in Aggregate [in Main.java]
class BookShelf implements Aggregate {
^
*/
public class Main {
    public static void main(String[] args) {
        BookShelf bookShelf = new BookShelf(4);
        bookShelf.appendBook(new Book("A"));   
        bookShelf.appendBook(new Book("B"));
        bookShelf.appendBook(new Book("C"));
        bookShelf.appendBook(new Book("D"));
        IteratorP it = bookShelf.iterator();
        while (it.hasNext()) {
            Book book = (Book) it.next();
            System.out.println(book.getName());
        }
    }
}

interface Aggregate {
    public abstract IteratorP interator();
}

interface IteratorP {
    public abstract boolean hasNext();
    public abstract Object next();
}

class BookShelf implements Aggregate {
    private Book[] books;
    private int last = 0;
    
    public BookShelf(int maxsize) {
        this.books = new Book[maxsize];
    }
    
    public Book getBookAt(int index) {
        return books[index];
    }
    
    public int getLength() {
        return last;
    }
    
    public void appendBook(Book book) {
        this.books[last] = book;
        last++;
    }

    public IteratorP iterator() {
        return new BookShelfIterator(this);
    }
}

class Book {
    private String name;
    public Book(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
}

class BookShelfIterator implements IteratorP {
    private BookShelf bookShelf;
    private int index;
    
    public BookShelfIterator(BookShelf bookShelf) {
        this.bookShelf = bookShelf;
        this.index = 0;
    }
    
    public boolean hasNext() {
        if (index < bookShelf.getLength()) {
            return true;
        } else {
            return false;
        }
    }
    
    public Object next() {
        Book book = bookShelf.getBookAt(index);
        index++;
        return book;
    }
}

```
