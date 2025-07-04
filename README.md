# test1
# 1. Classes and Objects
class Book:
    def __init__(self, title, author, isbn):
        self.title = title
        self.author = author
        self.__isbn = isbn  
        self.available = True

    def display_info(self):
        print(f"Title: {self.title}, Author: {self.author}, ISBN: {self.__isbn}, Available: {self.available}")

    def get_isbn(self):
        return self.__isbn

    def set_isbn(self, new_isbn):
        self.__isbn = new_isbn


class Member:
    def __init__(self, name, membership_id):
        self.name = name
        self.__membership_id = membership_id 
        self.borrowed_books = []

    def borrow_book(self, book):
        if book.available:
            self.borrowed_books.append(book)
            book.available = False
            print(f"{self.name} borrowed '{book.title}'")
        else:
            print(f"'{book.title}' is not available.")

    def return_book(self, book):
        if book in self.borrowed_books:
            self.borrowed_books.remove(book)
            book.available = True
            print(f"{self.name} returned '{book.title}'")
        else:
            print(f"{self.name} doesn't have '{book.title}' to return.")


    def get_membership_id(self):
        return self.__membership_id

    def set_membership_id(self, new_id):
        self.__membership_id = new_id

class StaffMember(Member):
    def __init__(self, name, membership_id, staff_id):
        super().__init__(name, membership_id)
        self.staff_id = staff_id

    def add_book(self, library, title, author, isbn):
        new_book = Book(title, author, isbn)
        library.append(new_book)
        print(f"{self.name} added '{title}' to the library.")

library = []
book1 = Book("Python Basics", "John Doe", "123456")
book2 = Book("Advanced Python", "Jane Smith", "789101")
library.extend([book1, book2])
member1 = Member("Ali", "M001")
staff1 = StaffMember("Nora", "S001", "ST123")
member1.borrow_book(book1)
member1.return_book(book1)
staff1.add_book(library, "Data Science", "Dr. Data", "112233")
