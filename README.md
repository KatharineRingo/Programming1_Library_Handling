# Programming1_Library_Handling
#Project final for COP 2006 - Natalie Herrera, Katharine Ringo, and Maria Sebastian Tomas 

#include <iostream>
#include <vector>
#include <string>
#include <cstdlib>
#include <ctime>

using namespace std;

struct Book {
    string title;
    string author;
    string genre;
    int year;

    // Constructor 
    Book(string t, string a, int y, string g) : title(t), author(a), year(y), genre(g) {}
};

class BookDatabase {
private:
    vector<Book> books;

public:
    // Add a new book to the database
    void addBook(const Book& book) {
        books.push_back(book);
    }

    // Display all books in the database
    void displayBooks() const {
        if (books.empty()) {
            cout << "No books in the database.\n";
            return;
        }

        cout << "\nBooks in the database:\n";
        for (const auto& book : books) {
            cout << "Title: " << book.title << ", Author: " << book.author << ", Year: " << book.year << ", Genre: " << book.genre << "\n";
        }
    }

    // Search for books by author
    void searchByAuthor(const string& authorName) const {
        bool found = false;
        cout << "\nBooks by " << authorName << ":\n";
        for (const auto& book : books) {
            if (book.author == authorName) {
                cout << "Title: " << book.title << ", Year: " << book.year << ", Genre: " << book.genre << "\n";
                found = true;
            }
        }

        if (!found) {
            cout << "No books found by " << authorName << ".\n";
        }
    }

    // Search for books by title
    void searchByTitle(const string& titleName) const {
        bool found = false;
        cout << "\nBooks with title containing '" << titleName << "':\n";
        for (const auto& book : books) {
            if (book.title.find(titleName) != string::npos) {
                cout << "Title: " << book.title << ", Author: " << book.author << ", Year: " << book.year << ", Genre: " << book.genre << "\n";
                found = true;
            }
        }

        if (!found) {
            cout << "No books found with the title containing '" << titleName << "'.\n";
        }
    }

    //Search for books by genre
    void searchByGenre(const string& genreName) const {
        bool found = false;
        //cout << "Genres you can search for: Coming of Age, Dystopian Fiction, Southern Gothic Fiction, Tragedy, Adventure Fiction, Historical Adventure Novel, Science Fantasy, and Young Adult";
        cout << "\nBooks of " << genreName << " genre: \n";
        for (const auto& book : books) {
            if (book.genre.find(genreName) != string::npos) {
                cout << "Title: " << book.title << ", Author: " << book.author << ", Year: " << book.year << ", Genre: " << book.genre << "\n";
                found = true;
            }
        }

        if (!found) {
            cout << "No books found with genre " << genreName << ".\n";
        }
    }

    void randomBooks() const {
        srand(time(0));

        // Generate a random index within the database size
        int randomFind = rand() % books.size();

        // Pick the random item
        Book randomBook = books[randomFind];

        cout << "Here's a random suggestion for you!: " << randomBook.title << ", Author: " << randomBook.author << ", Year: " << randomBook.year << ", Genre: " << randomBook.genre << "\n";
        cout << "\n";
    }

};

int main() {
    BookDatabase db;

    // Adding books to the database
    db.addBook(Book("The Catcher in the Rye", "J.D. Salinger", 1951, "Coming of Age"));
    db.addBook(Book("1984", "George Orwell", 1949, "Dystopian Fiction"));
    db.addBook(Book("To Kill a Mockingbird", "Harper Lee", 1960, "Southern Gothic Fiction"));
    db.addBook(Book("The Great Gatsby", "F. Scott Fitzgerald", 1925, "Tragedy"));
    db.addBook(Book("Moby-Dick", "Herman Melville", 1851, "Adventure Fiction"));
    db.addBook(Book("The Count of Monte Cristo", "Alexandre Dumas", 1844, "Historical Adventure Novel"));
    db.addBook(Book("Little Women", "Louisa May Alcott", 1868, "Coming of Age"));
    db.addBook(Book("A Wrinkle in Time", "Madeleine L'Engle", 1962,"Science Fantasy"));
    db.addBook(Book("Hatchet", "Gary Paulsen", 1987, "Young Adult"));

    // Interacting with the database
    int choice;
    do {
        cout << "Menu:\n";
        cout << "1. Display all books\n";
        cout << "2. Search books by author\n";
        cout << "3. Search books by title\n";
        cout << "4. Search books by genre\n";
        cout << "5. Input your own book\n";
        cout << "6. Let us give you a random recommendation!\n";
        cout << "7. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;
        cin.ignore(); 

        switch (choice) {
            case 1: {
                db.displayBooks();
                cout << "\n";
                break;
            }

            case 2: {
                string author;
                cout << "Enter author's name: ";
                getline(cin, author);
                db.searchByAuthor(author);
                cout << "\n";
                break;
            }

            case 3: {
                string title;
                cout << "Enter book title or part of title: ";
                getline(cin, title);
                db.searchByTitle(title);
                cout << "\n";
                break;
            }

            case 4: {
                string genre;
                cout << "Genres you can search for: \nComing of Age, Dystopian Fiction, Southern Gothic Fiction, Tragedy, Adventure Fiction, Historical Adventure Novel, Science Fantasy, and Young Adult\n";
                cout << "Enter the genre: ";
                getline(cin,genre);
                db.searchByGenre(genre);
                cout << "\n";
                break;
            }

            case 5: { 
                char* title = new char[100];
                char* author = new char[100];
                char* genre = new char[100];
                int year;

                cout << "Enter the details of a new book: \n";
                cout<<"Title: ";
                cin.getline(title, 100);
                cout<<"Author: ";
                cin.getline(author, 100);
                cout<<"Year: ";
                cin>>year;
                cin.getline(genre, 100);
                cout<<"Genre: ";
                cin>>genre;
                db.addBook(Book(title, author, year, genre));
                }
                cout << "\n";
                break;

            case 6: {
                db.randomBooks();
                break;
            }

            case 7:
                cout << "Exiting program...\n";
                break;
                
            default:
                cout << "Invalid choice. Please try again.\n";
        }
    } while (choice != 7);

    return 0;
};
