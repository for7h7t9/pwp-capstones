#--------------------------------------------------------------------------------------------------
#BEGIN TOME RATER FILE
#--------------------------------------------------------------------------------------------------


#--------------------------------------------------------------------------------------------------
class User:
# A constructor method which takes in self, name, and email.  It should set instance variables self.name, self. email, and self.books.  Name will be a string.  Email will be a string.  Self.books is an empty dictionary that will map a Book object (which we will create!) to this user's rating of the book.
  def __init__(self, name, email):
    self.name = name
    self.email = email
    self.books = {}
  
# A method get_email that returns the email associated with this user.
  def get_email(self):
    return self.email

# A method change_email that takes in a new email and changes the email associated with this user. It should print a message saying the user's email has been updated.
  def change_email(self, address):
    new_email = address
    self.email = new_email
    print("{name}'s email address has been updated to {new_email}.".format(name=self.name, new_email=self.email))
  
# A __repr__ method that returns a string to print out this user object in a meaningful way.  Printing a user named Stephen Hawking, with an email hawking@universe.edu with 7 books read might produce a string like: User Stephen Hawking, email: hawking@universe.edu, books read: 7.
  def __repr__(self):
    self.books_read = 0
    for book in self.books:
      self.books_read = self.books_read + 1
    print("User: {User_name}; Email: {User_email}; Books Read: {User_books_read};".format(User_name=self.name, User_email=self.email, User_books_read=self.books_read))
    

# An __eq__ method to define comparison between users.  A user object should be equal to another User object if they both have the same name and email.
  def __eq__(self, other_user):
    if self.name == other_user.name and self.email == other_user.email:
      return True
    else:
      return False
  
# A method read_book takes in a book and an optional parameter rating, which defaults to None.  It should add a key:value pair to self.books where the key is book and the value is rating.
  def read_book(self, book, rating="None"):
    self.books[book] = rating
  
# A method get_average_rating iterates through all of the values in self.books which are the ratings and calculates the average rating 
  def get_average_rating(self):
    total_value = 0
    total_books = 0
    for rating in self.books.values():
      if rating != "None":
        total_value = total_value + int(rating)
        total_books = total_books + 1
    average_rating = total_value / total_books
    return average_rating

#--------------------------------------------------------------------------------------------------
class Book:
# A constructor method which takes in self, title, and isbn.  It should set instance variables self.title and self.isbn.  It should also set an instance variable self.ratings which will start as an empty list.  Title will be a string.  Isbn will be a number. 
  def __init__(self, title, isbn):
    self.title = title
    self.isbn = isbn
    self.ratings = []
  
# A method get_title that returns the title of the book.  
  def get_title(self):
    return self.title

# A method get_isbn that returns the ISBN of the book.
  def get_isbn(self):
    return self.isbn

# A method set_isbn that takes in a new ISBN and sets the book's isbn to be this new number.  It should also print a message saying that this book's isbn has been updated.  
  def set_isbn(self, new_isbn):
    self.isbn = new_isbn
    print("{book_title}'s ISBN has been updated to {book_isbn}.".format(book_title=self.title, book_isbn=self.isbn))

# A method called add_rating that takes in a rating and adds it to the list self.ratings.  It should only do this if rating is a valid rating (at least 0 and at most 4).  Otherwise, it should print "Invalid Rating".
  def add_rating(self, rating):
    if rating >= 0 and rating <= 4:
      self.ratings.append(rating)
    else:
      print("Invalid Rating")

# An __eq__ method to define comparison between books.  A Book object should be equal to another Book object if they both have the same title and isbn.
  def __eq__(self, other_book):
    if self.title == other_book.title and self.isbn == other_book.isbn:
      return True
    else:
      return False

# get_average_rating, which iterates through all of the values in self.ratings and calculates the average rating.  It should return this average.
  
  def get_average_rating(self):
    total_value = 0
    total_reviews = 0
    average_rating = 0
    for rating in self.ratings:
      if type(rating) == str:
        pass
      else:
        total_value = total_value + int(rating)
        total_reviews = total_reviews + 1
    average_rating = total_value / total_reviews
    return average_rating

# To make our Book hashable we will add a method __hash__ which will return a consistent has for an instance of a book object.
  def __hash__(self):
    return hash((self.title, self.isbn))
  
  def __repr__(self):
    print("{isbn}:  {book_title}.".format(isbn=self.isbn, book_title=self.title))    
#--------------------------------------------------------------------------------------------------
# The Fiction class should inherit from Book.
class Fiction(Book):
# A constructor which takes in self, title, author, and isbn.  It should first call the __init__ of its parent class with title and isbn.  Then, it should set the instance variable self.author.
  def __init__(self, title, author, isbn):
    super().__init__(title, isbn)
    self.author = author
  
# A get_author method which returns the author
  def get_author(self):
    return self.author

# A __repr__ method, which will return the string: {title} by {author}.  For example, the book with title "Alice in Wonderland" and author "Lewis Carroll" would print: Alice in Wonderland by Lewis Carroll.
  def __repr__(self):
    print("{isbn}:  {book_title} by {book_author}.".format(isbn=self.isbn, book_title=self.title, book_author=self.author))


#--------------------------------------------------------------------------------------------------
# The Fiction class should inherit from Book.
class Non_Fiction(Book):
# A constructor which takes in self, title, subject, level and isbn.  It should first call the __init__ of its parent class, with title and isbn.  Then it should set the instance variables self.subject and self.level.  Subject will be a string like "Geology".  Level will be a string like "advanced".
  def __init__(self, title, subject, level, isbn):
    super().__init__(title, isbn)
    self.subject = subject
    self.level = level
  
# A get_subject method which returns the subject.
  def get_subject(self):
    return self.subject
  
# A get_level method which returns the level.
  def get_level(self):
    return self.level
  
# A __repr__ method, which will return the string:  {title} a {level} manual on {subject}.  For example, the book with title "Society of Mind" about beginner Artificial Intelligence would print: Society of Mind, a beginner manual on Artificial Intelligence.
  def __repr__(self):
    print("{isbn}:  {book_title} a {book_level} manual on {book_subject}.".format(isbn=self.isbn, book_title=self.title, book_level=self.level, book_subject=self.subject))
  
#--------------------------------------------------------------------------------------------------
class Tome_Rater:
# A constructor that only takes in self.  It should create: self.users, an empty dictionary that will map a user's email to the corresponding User object; self.books, an empty dictionary that will map a Book object to the number of Users that have read it. 
  def __init__(self):
    self.users = {}
    self.books = {}

# A create_book method, which takes in title and isbn and creates a new book with that title and ISBN.  Returns this Book object.  
  def create_book(self, title, isbn):
    self.book = Book(title, isbn)
    return self.book
  
# A create_novel method, which takes in title, author, and isbn, and creates a new Fiction with that title, author and ISBN.  Returns this Fiction object.
  def create_novel(self, title, author, isbn):
    self.novel = Fiction(title, author, isbn)
    return self.novel

# A create_non_fiction method, which takes in title, subject, level, and isbn, and creates a new Non_Fiction with that title, author and ISBN.  Returns this Non_Fiction object. 
  def create_non_fiction(self, title, subject, level, isbn):
    self.non_fiction = Non_Fiction(title, subject, level, isbn)
    return self.non_fiction
  
# A add_book_to_user method, which takes in book, email and an optional parameter rating, which defaults to None.  It should get the user in self.users with the key email.  If the user doesnt exist, it should print out "No user with email {email}!".  If the user exists, it should:  Call read_book on this user, with book and rating; Call add_rating on book with rating; Check if the book is in Tome_Rater's self.books already.  If it is not, add the key book to self.books with a value of 1 (because one user has read it); if book was already in the catalog, increase the value of it in self.books by 1 because one more user has read it.
  def add_book_to_user(self, book, email, rating = "None"):
    if email in self.users:
      user = self.users.get(email)
      user.read_book(book, rating)
      book.add_rating(rating)
      
      if book in self.books:
        num_book_read = self.books[book]
        self.books[book] = num_book_read + 1
      else:
        self.books[book] = 1
    else:
      print("No user with email {email}!".format(email=email))
    
  
# A add_user method, which takes in name, email, and an optional list of Books user_books that defaults to None.  It should create a new User object from name and email.  Then if user_books is provided, it should loop through the list, and add each Book to the user (using Tome Rater method add_book_to_user).
  def add_user(self, name, email, user_books = "None"):
    self.user = User(name, email)
    self.users[email] = self.user
    if type(user_books) == str:
      pass
    else:
      for book in user_books:
        self.user.read_book(book) #<-- Maybe a problem here
        if book in self.books:
          num_book_read = self.books[book]
          self.books[book] = num_book_read + 1
        else:
          self.books[book] = 1
    
    return self.users

# A print_catalog method, which iterates through all of the keys in self.books (which are Book objects) and prints them.
  def print_catalog(self):
    print("The current catalog of books is as follows:")
    for book in self.books:
      book.__repr__()
    print("\n")
  
# A print_users method, which iterates through all of the values of self.users (which are the User objects) and prints them.
  def print_users(self):
    print("The current list of users is as follows:")
    for i in self.users:
      temp_user = self.users[i]
      temp_user.__repr__()
    print("\n")
  
# A most_read_book method, which should iterate through all of the books in self.books and return the book that has been read the most.  Remember that the keys of self.books are Books, and the values are how many times they've been read.
  def get_most_read_book(self):
    max_value = 0
    for book in self.books:
      temp_value = self.books[book]
      if temp_value > max_value:
        max_value = temp_value
        max_book_title = book.get_title()
    print("The most read book is \"{max_book_title}\" which has been read {max_value} times.".format(max_book_title=max_book_title, max_value=max_value))
    print("\n")
  
# A highest_rated_book method, which should iterate through all of the books in self.books and return the book that has the highest average rating.  Remember that the keys of self.books are Books, and you can call book.get_average_rating() on a Book object book.
  def highest_rated_book(self):
    highest_average_rating = 0
    for book in self.books:
      temp_average_rating = book.get_average_rating()
      if temp_average_rating > highest_average_rating:
        highest_average_rating = temp_average_rating
        highest_average_rating_book_title = book.get_title()
    print("The book with the highest average rating is \"{highest_average_rating_book_title}\" with an average rating of {highest_average_rating}.".format(highest_average_rating_book_title=highest_average_rating_book_title, highest_average_rating=highest_average_rating))
    print("\n")
  
# A most_positive_user, which should iterate through all of the users in self.users and return the user that has the highest average rating.  Remember that the values of self.users are Users, and you can call user.get_average_rating() on a User object user.
  def most_positive_user(self):
    highest_average_rating = 0
    for email in self.users:
      user = self.users[email]
      temp_average_rating = user.get_average_rating()
      if temp_average_rating > highest_average_rating:
        highest_average_rating = temp_average_rating
        highest_average_rating_user_name = user.get_email()
    print("The user with the highest average rating is \"{highest_average_rating_user_name}\" with an average rating of {highest_average_rating}.".format(highest_average_rating_user_name=highest_average_rating_user_name, highest_average_rating=highest_average_rating))
    print("\n")






















#--------------------------------------------------------------------------------------------------
#TEST SECTION
#--------------------------------------------------------------------------------------------------
Tome_Rater = Tome_Rater()
#test_user = User("Steven", "stevenforsyth1@gmail.com")
#test_user2 = User("Steven", "stevenforsyth1@gmail.com")


#print(test_user.get_email())
#test_user.change_email("T_operations@yahoo.com")
#test_user.read_book("my_book1")
#test_user.read_book("my_book2", "1")
#test_user.read_book("my_book3", "3")
#test_user.read_book("my_book4", "7")
#print(test_user.__eq__(test_user2))
#test_user.__repr__()
#print(test_user.get_average_rating())

#book1 = Book("Society of Mind", 12345678)
#book1 = Fiction("Society of Mind", 12345678)
#novel1 = Fiction("Alice In Wonderland", "Lewis Carroll", 12345)
#novel1.set_isbn(9781536831139)
#nonfiction1 = Non_Fiction("Automate the Boring Stuff", "Python", "beginner", 1929452)
#nonfiction2 = Non_Fiction("Computing Machinery and Intelligence", "AI", "advanced", 11111938)
#novel2 = Fiction("The Diamond Age", "Neal Stephenson", 10101010)
#novel3 = Fiction("There Will Come Soft Rains", "Ray Bradbury", 10001000)


#print(book1.title)
#print(book1.isbn)
#book1.set_isbn(87654321)
#book1.add_rating(0)
#book1.add_rating(2)
#book1.add_rating(4)
#book1.add_rating(3)
#print(bookA.__eq__(bookB))
#print(book1.get_average_rating())
#print(novel3.get_author())  
#novel3.__repr__()
#nonfiction2.__repr__()
#--------------------------------------------------------------------------------------------------

#Create some books:
book1 = Tome_Rater.create_book("Society of Mind", 12345678)
book2 = Tome_Rater.create_book("War and Peace", 98765432)
book3 = Tome_Rater.create_book("Grapes of Wrath", 98761234)
novel1 = Tome_Rater.create_novel("Alice In Wonderland", "Lewis Carroll", 12345333)
nonfiction1 = Tome_Rater.create_non_fiction("Automate the Boring Stuff", "Python", "beginner", 19294521)
nonfiction2 = Tome_Rater.create_non_fiction("Computing Machinery and Intelligence", "AI", "advanced", 11111938)
novel2 = Tome_Rater.create_novel("The Diamond Age", "Neal Stephenson", 10101010)
novel3 = Tome_Rater.create_novel("There Will Come Soft Rains", "Ray Bradbury", 10001000)

#Create users:
Tome_Rater.add_user("Alan Turing", "alan@turing.com")
Tome_Rater.add_user("David Marr", "david@computation.org")
Tome_Rater.add_user("Steven Forsyth", "stevenforsyth1@gmail.com")

#Add a user with three books already read:
Tome_Rater.add_user("Marvin Minsky", "marvin@mit.edu", user_books=[book1, novel1, nonfiction1])

#Add books to a user one by one, with ratings:
Tome_Rater.add_book_to_user(book1, "alan@turing.com", 1)
Tome_Rater.add_book_to_user(book2, "david@computation.org", 3)
Tome_Rater.add_book_to_user(book3, "stevenforsyth1@gmail.com", 3)
Tome_Rater.add_book_to_user(novel1, "alan@turing.com", 3)
Tome_Rater.add_book_to_user(nonfiction1, "alan@turing.com", 3)
Tome_Rater.add_book_to_user(nonfiction2, "alan@turing.com", 4)
Tome_Rater.add_book_to_user(novel3, "alan@turing.com", 1)
Tome_Rater.add_book_to_user(novel2, "marvin@mit.edu", 2)
Tome_Rater.add_book_to_user(novel3, "marvin@mit.edu", 2)
Tome_Rater.add_book_to_user(novel3, "david@computation.org", 4)


#Uncomment these to test your functions:
Tome_Rater.print_catalog()
Tome_Rater.print_users()
Tome_Rater.get_most_read_book()
Tome_Rater.highest_rated_book()
Tome_Rater.most_positive_user()

#--------------------------------------------------------------------------------------------------
#END TOME RATER FILE
#--------------------------------------------------------------------------------------------------