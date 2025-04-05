# Library
public class lib1 {
    private String title;
    private String author;
    private int bookId;
    private boolean isAvailable;

    public lib1(int bookId, String title, String author) {
        this.bookId = bookId;
        this.title = title;
        this.author = author;
        this.isAvailable = true;
    }

    public int getBookId() {
        return bookId;
    }

    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void borrowBook() {
        if (isAvailable) {
            isAvailable = false;
            System.out.println("The book \"" + title + "\" is now borrowed.");
        } else {
            System.out.println("Sorry, the book \"" + title + "\" is not available.");
        }
    }

    public void returnBook() {
        isAvailable = true;
        System.out.println("The book \"" + title + "\" is returned.");
    }
}




#2nd fun
import java.util.ArrayList;

public class lib2 {
    private ArrayList<lib1> books;

    public lib2() {
        books = new ArrayList<>();
    }

    public void addBook(lib1 book) {
        books.add(book);
    }

    public void displayBooks() {
        for (lib1 book : books) {
            System.out.println("Book ID: " + book.getBookId() + ", Title: " + book.getTitle() + ", Author: "
                    + book.getAuthor() + ", Available: " + book.isAvailable());
        }
    }

    public lib1 searchBookById(int bookId) {
        for (lib1 book : books) {
            if (book.getBookId() == bookId) {
                return book;
            }
        }
        return null;
    }

}


#3rd fun
import java.util.Scanner;

public class lib3 {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        lib2 library = new lib2(); // Create Library object using lib2

        // Adding sample books to the library
        library.addBook(new lib1(1, "Java Programming", "Author A"));
        library.addBook(new lib1(2, "Data Structures", "Author B"));
        library.addBook(new lib1(3, "Algorithms", "Author C"));

        while (true) {
            System.out.println("\n--- Library Management System ---");
            System.out.println("1. Display Books");
            System.out.println("2. Borrow Book");
            System.out.println("3. Return Book");
            System.out.println("4. Exit");

            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    library.displayBooks();
                    break;
                case 2:
                    System.out.print("Enter Book ID to borrow: ");
                    int borrowId = scanner.nextInt();
                    lib1 borrowBook = library.searchBookById(borrowId); // Using lib1 class
                    if (borrowBook != null) {
                        borrowBook.borrowBook();
                    } else {
                        System.out.println("Book not found.");
                    }
                    break;
                case 3:
                    System.out.print("Enter Book ID to return: ");
                    int returnId = scanner.nextInt();
                    lib1 returnBook = library.searchBookById(returnId); // Using lib1 class
                    if (returnBook != null) {
                        returnBook.returnBook();
                    } else {
                        System.out.println("Book not found.");
                    }
                    break;
                case 4:
                    System.out.println("Exiting the system. Goodbye!");
                    scanner.close();
                    return;
                default:
                    System.out.println("Invalid choice, please try again.");
            }
        }
    }
}
