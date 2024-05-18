# LibrarySystem
Library System GUI in Tkinter: Explanation Report
Overview:
This report provides a detailed explanation of a Python script that creates a library system graphical user interface (GUI) using the Tkinter library. The system allows users to view a list of books, search for specific books, view details of selected books, submit ratings and comments, and open an external link to a book.

Code Breakdown;
1. Initialization and Configuration
The LibrarySystem class initializes and configures the main window and its components.

class LibrarySystem:					
    def __init__(self, root):				
        self.root = root				
        self.root.title("Library System")		
        self.root.geometry("800x1000")		
        self.root.configure(background='white')

    • Title: Sets the window title to "Library System".
    • Geometry: Sets the window size to 800x1000 pixels.
    • Background: Sets the background color to white.



2. Main Frame and Layout;
The main frame holds all other frames and widgets.

self.main_frame = tk.Frame(self.root)	      
self.main_frame.pack(fill="both", expand=True) 

    • Main Frame: Created to hold all components.
    • Packing: Fills the entire window and allows expansion.
3. Books Frame;
The left side of the GUI displays a list of books.
 
self.books_frame = tk.Frame(self.main_frame, bg="#ee799f") 
self.books_frame.pack(side="left", fill="y")		      

self.books_label = tk.Label(self.books_frame, text="Books", font=("Arial", 24, "bold"), bg="#ee799f", fg="white")
self.books_label.pack(side="top", fill="x")												 

self.book_list_frame = tk.Frame(self.books_frame, bg="#ee799f")  
self.book_list_frame.pack(fill="both", expand=True)			

    • Books Frame: Positioned on the left side with a pink background.
    • Books Label: A label titled "Books" at the top.
    • Book List Frame: Holds the list of books.




4. Book List;
A listbox widget displays the list of books.

self.book_list = tk.Listbox(self.book_list_frame, width=28, height=20, bg="#cd6889", fg="white", font=("Arial", 14))  
self.book_list.pack(fill="both", expand=True)													
self.populate_book_list()																

    • Listbox: A widget to display book titles with specific dimensions and colors.
    • Populating: Calls populate_book_list to add books to the list.

    
5. Book Details Frame;
The right side displays book details and provides a search bar.

self.book_details_frame = tk.Frame(self.main_frame, bg="#ee799f")   
self.book_details_frame.pack(side="right", fill="both", expand=True)

    • Book Details Frame: Positioned on the right side with a pink background.


6. Search Bar;
Allows users to search for books by title.

self.search_frame = tk.Frame(self.book_details_frame, bg="#8b475d", pady=10)                          
self.search_frame.pack(fill="x")                                                                      
                                                                                                      
self.search_label = tk.Label(self.search_frame, text="Search for a book:", bg="#8b475d", fg="white")  
self.search_label.pack(side="left", padx=10)                                                          
                                                                                                      
self.search_entry = tk.Entry(self.search_frame, width=30)                                             
self.search_entry.pack(side="left", padx=10)                                                          
                                                                                                      
self.search_button = tk.Button(self.search_frame, text="Search", command=self.search_book, fg="black")
self.search_button.configure(background='blue')                                                       
self.search_button.pack(side="left", padx=10)                                                         

    • Search Frame: Contains the search bar components.
    • Search Label: Descriptive label.
    • Search Entry: Entry widget for input.
    • Search Button: Button to trigger the search.


7. Book Details Display;
Displays selected book title, image, rating scale, and comment section.

self.book_title_label = tk.Label(self.book_details_frame, text="", font=("Arial", 34), bg="#ee799f", fg="black")
self.book_title_label.pack(pady=20)

self.book_image_label = tk.Label(self.book_details_frame, bg="#ee799f")
self.book_image_label.pack(pady=10, padx=10)

self.rating_label = tk.Label(self.book_details_frame, text="Rating:", bg="#ee799f", fg="white")
self.rating_label.pack(pady=10, padx=20, anchor="w")

self.rating_scale = ttk.Scale(self.book_details_frame, from_=0, to=5, length=200, orient="horizontal")
self.rating_scale.pack(pady=5, padx=20, anchor="w")

self.comment_label = tk.Label(self.book_details_frame, text="Comment:", bg="#ee799f", fg="white")
self.comment_label.pack(pady=10, padx=20, anchor="w")

self.comment_entry = tk.Entry(self.book_details_frame, width=40)
self.comment_entry.pack(pady=5, padx=20, anchor="w", fill="x")

self.submit_button = tk.Button(self.book_details_frame, text="Submit", command=self.submit_review, bg="blue", fg="BLACK")
self.submit_button.pack(pady=10, padx=20, anchor="e")

self.link_button = tk.Button(self.book_details_frame, text="GO TO BOOK", command=lambda: self.open_link("file:///Users/azracebe/Downloads/01%20Harry%20Potter%20and%20The%20Philosopher's%20Stone.pdf"))
self.link_button.pack(pady=10)
    • Title Label: Displays the selected book's title.
    • Image Label: Displays the book's image.
    • Rating Scale: Allows users to rate the book.
    • Comment Entry: Allows users to leave comments.
    • Submit Button: Submits the rating and comment.		Link Button: Opens a PDF file link to the book.


8. Methods;
Several methods handle the functionalities like populating the list, searching, displaying details, submitting reviews, and opening links.
populate_book_list
Populates the listbox with sample books.

def populate_book_list(self):
    self.books = [
        {"title": "  -Harry Potter Sorcerer's Stone", "image_path": "hp1.png"},
        {"title": "  -Harry Potter Chamber of Secrets", "image_path": "hp2.png"},
        {"title": "  -Harry Potter Prisoner of Azkaban", "image_path": "hp3.png"},
        {"title": "  -Harry Potter Goblet of Fire", "image_path": "hp4.png"},
        {"title": "  -Harry Potter Order Of the Phoenix", "image_path": "hp5.png"},
        {"title": "  -Harry Potter Half-Blood Prince", "image_path": "hp6.png"},
        {"title": "  -Harry Potter and the Deathly Hallows", "image_path": "hp7.png"}
    ]
    for book in self.books:
        self.book_list.insert(tk.END, book["title"])
    self.book_list.bind("<<ListboxSelect>>", self.show_book_details)
search_book
Filters the book list based on the search term.

def search_book(self):
    search_term = self.search_entry.get().lower()
    self.book_list.delete(0, tk.END)
    for book in self.books:
        if search_term in book["title"].lower():
            self.book_list.insert(tk.END, book["title"])
show_book_details
Displays details of the selected book.

def show_book_details(self, event):
    selected_index = self.book_list.curselection()[0]
    selected_book = self.books[selected_index]
    self.book_title_label.config(text=selected_book["title"].strip())
    image_path = selected_book.get("image_path")
    if image_path:
        image = tk.PhotoImage(file=image_path)
        image = image.subsample(2)
        self.book_image_label.config(image=image)
        self.book_image_label.image = image
submit_review
Processes the rating and comment.

def submit_review(self):
    rating = self.rating_scale.get()
    comment = self.comment_entry.get()
    print(f"Rating: {rating}")
    print(f"Comment: {comment}")
open_link
Opens a given URL in the web browser.

def open_link(self, url):
    webbrowser.open(url)

    
Conclusion;
This Tkinter-based library system GUI enables users to view, search, rate, and comment on a list of books, as well as access external links to the books. The modular design, clear layout, and defined methods facilitate easy navigation and interaction within the application.
