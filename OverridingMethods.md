Overriding Methods

### Main Class()
```
public class Main {
    public static void main(String[] args) {

        //Constuct instances with data
        Book favorite = new Book("The Hobbit", "J. R. R. Tolkien", "George Allen and Unwin", "21 September 1937");
        Encyclopedia textbook = new Encyclopedia("The Illustrated Encyclopedia of the Universe", "Ian Ridpath", "Watson-Guptill", "2001", "2nd", 384);

        //Print
        favorite.printInfo();
        textbook.printInfo();
    }
}
```

### Book Class()
```
public class Book {
    private String bookTitle;
    private String bookAuthor;
    private String bookPublisher;
    private String bookPublicationDate;

    public Book(String title, String author, String publisher, String pubDate){
        bookTitle = title;
        bookAuthor = author;
        bookPublisher = publisher;
        bookPublicationDate = pubDate;
    }
    public void setBookTitle(String title){
        bookTitle = title;
    }
    public String getBookTitle(){
        return bookTitle;
    }
    public void setBookAuthor(String author){
        bookAuthor = author;
    }
    public String getBookAuthor(){
        return bookAuthor;
    }
    public void setBookPublisher(String publisher){
        bookPublisher = publisher;
    }
    public String getBookPublisher(){
        return bookPublisher;
    }
    public void setBookPublicationDate(String date){
        bookPublicationDate = date;
    }
    public String getBookPublicationDate(){
        return bookPublicationDate;
    }

    public void printInfo(){
        System.out.println("Book Information: ");
        System.out.println("\tBook Title: " + bookTitle);
        System.out.println("\tAutho: " + bookAuthor);
        System.out.println("\tPublisher: " + bookPublisher);
        System.out.println("\tPublication Date: " + bookPublicationDate);
    }
}
```

### Encyclopedia Class()
```
public class Encyclopedia extends Book{
    private String bookEdition;
    private int bookPages;

    public Encyclopedia(String title, String author, String publisher, String pubDate, String edition, int pages) {
        super(title, author, publisher, pubDate);
        bookEdition = edition;
        bookPages = pages;
    }

    public void setBookEdition(String title){
        bookEdition = title;
    }
    public String getBookEdition(){
        return bookEdition;
    }

    public void setPages(int pages){
        bookPages = pages;
    }
    public int getPages(){
        return bookPages;
    }

    public void printInfo(){
        System.out.println("Book Information: ");
        System.out.println("\tBook Title: " + getBookTitle());
        System.out.println("\tAuthor: " + getBookAuthor());
        System.out.println("\tPublisher: " + getBookPublisher());
        System.out.println("\tPublication Date: " + getBookPublicationDate());
        System.out.println("\tEdition: " + bookEdition);
        System.out.println("\tNumber of Pages: " + bookPages);
    }

}
```

## Challenges
  - The printInfo() method takes no input. The overloaded version for the Encylopedia Class required reusing some of the same data.
  - The overloaded constructor takes additional input and threfore works properly

## Flowchart
![Overiding_Methods](https://github.com/suddy00/CISC_191_Int_Java/assets/17439019/5ca109e8-fe73-40e5-9810-6642d819c8f1)

