# Library_Management_System
//Library_management_system is a mini  C++ project ,developed by me without object oriented programming.
 
Developed by MUHAMMAD TAHA 

Project: library Management system

Overview:
This project is developed using only C++ with its integrated libraries. It only allows registered users to use the system and also has the functionality to add new users .It has a functionality to add and remove books that is only handled by admin.

Main Features :

•	New user registration
•	User authentication
•	Admin authentication
•	Book issuance
•	Search functionality
•	Shows user info and issued books
•	Functionality to Add a book and remove a book
•	Save every info in file
Management system has three pages
Admin page :
Admin has two options after he/she verify its authority by entering password.
Remove a Book : it asks user  for book number after showing  all books and as user enter a book number it removes the book and shows user books again . 

Add a Book : It asks user for everything related to the book he or she want to add and then save it in file.
User page : 
User page will first confirm whether the user is the registered user by asking file id and password ,
After that system will give him two main options
Search a book or see all the available books
In search a book there are further 3 option search by name ,search by book id and search by book author name and as book is found it let user confirm book issuance once confirmed it will show user its issued books.
Note that system has put the validation of entering only three books maximum more than 3 books entrance will show the message of books issuance limitation.  

New user page 
New user page is for registration where it ask user about its bio and ask if user is Air university student if he is it will allow user to make his account.
Functions (made by us) :
•	User login
•	New user login
•	Add a book
•	Remove a book
•	Issue book
•	Search a book

Libraries we used:
#include<iostream>
#include<fstream>
#include<string>
#include<cstdio>
#include<chrono>
#include<thread>
