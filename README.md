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
// Source Code
#include<iostream>
#include<fstream>
#include<string>
#include<cstdio>
#include<chrono>
#include<thread>
#include<conio.h>

using namespace std;
struct User {
	
	string user_name;
	string password;
	int phone_number;
	string issued_book1;
	string issued_book2;
	string issued_book3;
};

struct Books {
	std::string author_name;
	std::string book_Name;
	int book_ID;
	float Price;
	int Quantity;
};
void check_user_details();
void issue_book(string file_id,string book_name);
void user_login(string );
void new_user(string );
void search_book(Books,string );
void Remove_book(int U);
float Bookprice(int book_no);
void show_book();
void Addbook();
//__________________
//User Details
// -----------------
void check_user_details() {
	string w,user_id,X;a:char x,ch;
	cout << "Please enter your user ID :";cin>> user_id;
	ifstream user;User u;
	user.open(user_id);
	if (!user.is_open()) {
		cout << "Invalid User ID\n";cout << "Quit (Q)\t\t|\t\t Enter user ID again(E) \n";cin >> x;
		if (x == 'E' || x == 'e') { this_thread::sleep_for(std::chrono::seconds(1));goto a; }
		else if (x == 'Q' || x == 'q')
		{
			system("cls");cout << "Exiting ";this_thread::sleep_for(std::chrono::seconds(1));return;

		}

	}
	
	user >> u.user_name >> u.password >> u.phone_number >> u.issued_book1 >> u.issued_book2 >> u.issued_book3;
	cout << "Enter Passwrd :";

	while ((ch = _getch()) != '\r') {
		if (ch == '\b') {
			if (!u.password.empty()) {
				u.password.pop_back();
				std::cout << "\b \b";
			}
		}
		else {
			X += ch;
			std::cout << '*';
		}
	}
	cout << "\n\n\t\tUser Details\n";
	cout << "================================================================\n";
	cout << "\t\tUser Name :" << u.user_name << endl;
	cout << "\t\tPhone Number :" << u.phone_number << endl;
	cout << "\n\t\t Issued Book 1 :" << u.issued_book1 << endl;
	cout << "\t\tIssued Book 2 :" << u.issued_book2 << endl;
	cout << "\t\tIssued Book 3 :" << u.issued_book3 << endl;
	cout << "================================================================\n";
	user.close();
	
}

//____________________
// ISSUE BOOK FUNCTION
//--------------------


void issue_book(string File_ID, string book_name) {
	system("cls");char z;
	ofstream F("LIB.TXT", ios::app);
	ifstream f("library.txt");
	User u;Books book;
	
	ifstream File;File.open(File_ID);File >> u.user_name >> u.password >> u.phone_number >> u.issued_book1 >> u.issued_book2 >> u.issued_book3;
	if (u.issued_book3 != "") {
		cout << "\n\n\t\t-------------------\n";
		cout << "\tYou cant have more than 3 books issued to your name\n\t----------------------------------------------\n";
		this_thread::sleep_for(std::chrono::seconds(1));return;
	}
	if (!File.is_open()) { cout << "\t\t-------------------\n\tError file does'nt open(user read)\n"; }
	ofstream file;
	file.open(File_ID, ios::app);
	if (!file.is_open()) {
		cout << "\t\t-------------------\n\tError file does not open!!\n";
	}
	else {

		while (f >> book.author_name >> book.book_Name >> book.book_ID >> book.Price >> book.Quantity) {
			if (book_name == book.book_Name) {
				if (book.Quantity <=0) {
					cout << "\t\t----------------------\n" << book.book_Name << " is not currently available(out of stock)\n ";
					cout << "enter any button to quit\n";cin.ignore();return;
				}
			
				else 
				{
					file << book_name << " ";book.Quantity -=1;
					F << book.author_name <<"\n" << book.book_Name << "\n"<< book.book_ID << "\n" << book.Price << "\n" << book.Quantity << "\n";
					
				}
			}
			else {
				F << book.author_name << "\n" << book.book_Name << "\n" << book.book_ID << "\n" << book.Price << "\n" << book.Quantity << "\n";
			}
		}
		file.close();File.close();F.close();f.close();
	}
	

	//const char* file_path = "library.txt";
	///const char file_path2 = "LIB.TXT";*/
	//int chk = removeFile(file_path);
	
	remove("library.txt");
	/*rename("LIB.TXT","library.txt");*/
	
	if (rename("LIB.TXT","library.txt") == -1) {
		cout << "\t\t-------------------\n\tError renaming file lib.txt to library.txt\n";
	}
	else {
		system("cls");
		cout << "\n\n\t\t=================================\n\t\tBook issuance successful!\n";
	}
	File.open(File_ID);
	{cout << "\n\n\t\t==================================\n\t\t";
		File >> u.user_name >> u.password >> u.phone_number >> u.issued_book1 >> u.issued_book2 >> u.issued_book3;
		if (u.issued_book1 != "") {
			if (u.issued_book2 == "" && u.issued_book3 == "") {
				cout << "\tUser Details\n\t\t==================================\n\t\t Name :" << u.user_name << "\n\t\t Phone number:" << u.phone_number << "\n" << "\t\t Issued Book :"  << u.issued_book1<<"\n"<<"==================================\n\n";
			}
			else if (u.issued_book3 == "") {
				cout << "\tUser Details\n\t\t==================================\n\t\t Name :" << u.user_name << "\n\t\tPhone number:" << u.phone_number << "\n" << "\t\t Issued Books :" << u.issued_book1 << "  | " << u.issued_book2<<"\n"<<"==================================\n\n";
			}
			else cout << "\tUser Details\n\t\t==================================\n\t\t Name :" << u.user_name << "\n\t\t Phone number: " << u.phone_number << "\n" << "\t\t Issued Books :" << u.issued_book1 << "  | " << u.issued_book2 << "  | " << u.issued_book3<<"\n"<<"==================================\n\n";
		}
		
	}
	File.close();



}
//-________________________
//  User login function
//_------------------------

using namespace std;
void user_login(string file_Id) {
	int n = 1;
	Books b;char ch;
	string x,z;char X,Y;User user;
	ifstream file;a:
	file.open(file_Id);
	while (!file.is_open()) {
		cout << "Error !! incorrect file ID \n";  n++;if (n > 2) {
			cout << "\t\tdont have an account??\npress (A) to create new account :";cin >> Y;
			if (Y == 'A' || Y == 'a') {
				system("CLS");cout << "\n\n\t\tMoving to NEW USER REGISTRATION..........";this_thread::sleep_for(std::chrono::seconds(1));
				cout << "\n\t\t\t\t\tNEW USER REGISTRATION\n";
				cout << "\n\n\t\t\tCreate User ID :";cin >> z;new_user(z);system("cls");cout << "\n\n\t\tMoving Back to User login...........";this_thread::sleep_for(std::chrono::seconds(1));cout << "\n\t\t\tLOGIN PLEASE \n";
			}
			else cout << "\n\t\t\twrite User ID:";cin >> file_Id;goto a;
		}else cout << "\n\t\t\twrite User ID:";cin >> file_Id;goto a;
		}
	
		file >> user.user_name >> user.password >> user.phone_number;
		cout << "\n\t\t\tPassword :";

		while ((ch = _getch()) != '\r') {
			if (ch == '\b') { 
				if (!x.empty()) {
					x.pop_back(); 
					std::cout << "\b \b"; 
				}
			}
			else {
				x += ch; 
				std::cout << '*'; 
			}
		}while (x != user.password) {
			cout << "Invalid password!!\nwrite Again";cin >> x;
		}cout << "\n\n\t\t\tLogged in succesfully\n";this_thread::sleep_for(std::chrono::seconds(1));system("cls");cout << "\n\n\t\tMoving to MAIN MENU...........";this_thread::sleep_for(std::chrono::seconds(1));
		

		file.close();
	}
//____________________
//New user function
//--------------------

using namespace std;
void new_user(string file_id) {
	;
	User user;
New:system("CLS");int x, y, z;char A, B, Q;
		
	char ch;
		std::cout << "\n\tYour  user name :";
		cin >> user.user_name;
		std::cout << "\n\tCreate your password :";

		while ((ch = _getch()) != '\r') {
			if (ch == '\b') { 
				if (!user.password.empty()) {
					user.password.pop_back(); 
					std::cout << "\b \b"; 
				}
			}
			else {
				user.password += ch; 
				std::cout << '*'; 
			}
		}
		std::cout << "\t Write  your Phone number (only integers )) :";
		cin >> user.phone_number;

		ofstream file;
		file.open(file_id);
		if (file.is_open()) {
			file << user.user_name << "\n" << user.password << "\n" << user.phone_number<<"\n";
			file.close();
			system("cls");std::cout << user.user_name << " has been successfully registered in our library \n\t\t\t Dont forget your User ID ( " << file_id << " )and Password****\n";

		}

		
}

//_________________________
// Search book function   |  
//-------------------------


void search_book(Books book, string file_id) {
t:
	s:system("cls");cout << "\t\t\t\t||SEARCH  BOOK||\n\n";
	char x;std::cout << "\tSearch by BookName Press(N)\n\tSearch by Book ID Press (I)\n\tSearch by Book Author Press (A)\n";
	string z;
	cin >> x;

	if (x == 'N' || x == 'n') {
		ifstream file("library.txt");
		system("cls");cout << "\t\t\t||SEARCH BY BOOK NAME||\n\t\t-------------------------------\n";
		char y;string N;std::cout << "\t\t\tWrite book name... :";cin >> N;system("cls");cout << "\n\n\t\tSearching book for you...........";this_thread::sleep_for(std::chrono::seconds(2));
		bool book_found = false;
		while (file >> book.author_name >> book.book_Name >> book.book_ID >> book.Price >> book.Quantity) {
			
			string Name = book.book_Name;if (N == Name) {
				book_found = true;
				std::cout << endl << "\t\tBook found" << "\n---------------------------------\n" << "\t\t\tAuthor Name : " << book.author_name << endl;
				std::cout << "\t\t\tBook Name : " << book.book_Name << endl;
				std::cout << "\t\t\tBook ID : " << book.book_ID << endl;
				std::cout << "\t\t\tBook price :" << book.Price << endl;
				std::cout << "\t\t\tCopies Available:" << book.Quantity << endl;
				std::cout << "-----------------------------------\n\t\tPress Y to confirm book issue. \n";
				cout << "\t\tPress (S)search Book Again \n";
				cout << "\t\tPress (Q) to Quit\n";
				cin >> y;
				if (y == 'y' || y == 'Y') {
					file.close();

					issue_book(file_id, book.book_Name);
				}
				else if (y == 'S' || y == 's') { goto s; }
				else { file.close();return; }
			}
		}
		if (!book_found) {
			system("cls");cout << "\n\n\t\tBOOK NOT FOUND !! Search Again...........";this_thread::sleep_for(std::chrono::seconds(2)); { goto t; }
	}
	}




	else if (x == 'A' || x == 'a') {
		ifstream file("library.txt");
		
		system("cls");cout << "\t\t ***||SEARCH BY AUTHOR NAME||***\n\t\t-------------------------------\n";
		string N;std::cout << "Write author name... :\n";cin >> N;system("cls");cout << "\n\n\t\tSearching book for you...........";this_thread::sleep_for(std::chrono::seconds(2));
		char y;bool book_found = false;
		while (file >> book.author_name >> book.book_Name >> book.book_ID >> book.Price >> book.Quantity) {
			
			string Name = book.author_name;if (N == Name) {
				book_found = true;
				std::cout << endl << "\t\tBook found" << "\n---------------------------------\n" << "\t\t\tAuthor Name : " << book.author_name << endl;
				std::cout << "\t\t\tBook Name : " << book.book_Name << endl;
				std::cout << "\t\t\tBook ID : " << book.book_ID  << endl;
				std::cout << "\t\t\tBook price :" << book.Price << endl;
				std::cout << "\t\t\tCopies Available:" << book.Quantity << endl;
				std::cout << "-----------------------------------\n\t\tPress Y to confirm book issue. \n";
				cout << "\t\tPress (S)search Book Again \n";
				cout << "\t\tPress (Q) to Quit\n";
				cin >> y;
				if (y == 'y' || y == 'Y') {
					file.close();

					issue_book(file_id,book.book_Name);
				}
				else if (y == 'S' || y == 's') { goto s; }
				else { file.close();exit(1); }
			}
		}if (!book_found) {
			system("cls");cout << "\n\n\t\tBOOK NOT FOUND !! Search Again...........";this_thread::sleep_for(std::chrono::seconds(2)); { goto t;}
		}
	}
	else if (x == 'I' || x == 'i') {
		
		ifstream file("library.txt");
		system("cls");cout << "\t\t-*** ||SEARCH BY BOOK ID|| ***-\n\t\t-------------------------------\n";
		int N;std::cout << "Write BOOK ID :";cin >> N;
		char y;bool book_found = false;
		while (file >> book.author_name >> book.book_Name >> book.book_ID >> book.Price >> book.Quantity) {
			
			int id = book.book_ID;if (N == id) {
				book_found = true;
				
				std::cout << endl << "\t\tBook found" << "\n---------------------------------\n" << "\t\t\tAuthor Name : " << book.author_name << endl;
				std::cout << "\t\t\tBook Name : " << book.book_Name << endl;
				std::cout << "\t\t\tBook ID : " << book.book_ID << endl;
				std::cout << "\t\t\tBook price :" << book.Price << endl;
				std::cout << "\t\t\tCopies Available:" << book.Quantity << endl;
				std::cout << "-----------------------------------\n\t\tPress Y to confirm book issue. \n";
				cout << "\t\tPress (S)search Book Again \n";
				cout << "\t\tPress (Q) to Quit\n";
				cin >> y;
				if (y == 'y' || y == 'Y') {
					file.close();

					issue_book(file_id, book.book_Name);
				}
				else if (y == 'S' || y == 's') { goto s; }
				else { file.close();return; }
			}
		}if (!book_found) {
			system("cls");cout << "\n\n\t\tBOOK NOT FOUND !! Search Again...........";this_thread::sleep_for(std::chrono::seconds(2));  goto t; }

	}
	else
	{	system("cls");std::cout << "Please select only A,I or N\n";goto t;
	}

	}
//_____________________
// Remove book function
//_____________________
void Remove_book(int U) {
	Books rbook;
	int b = 1, u = 1;

	ifstream file;
	file.open("library.txt");
	ofstream file1("temp.txt");

	if (!file.is_open()) {
		cout << "ERROR! file doesnt open\n";
	}
	else {

		while (file >> rbook.author_name >> rbook.book_Name >> rbook.book_ID >> rbook.Price>>rbook.Quantity) {
			if (U != u) {
				file1 << rbook.author_name << "\n" << rbook.book_Name << "\n" << rbook.book_ID << "\n" << rbook.Price << "\n"<<rbook.Quantity<<"\n";
			}


			u++;
		}file.close();
	}remove("library.txt");file1.close();

	if (rename("temp.txt", "library.txt") != 0) { perror("Error renaming file\n"); }
	else
		system("CLS");
	cout << "book no:" << U << " has been succesfully Removed\n";
	cout << "Books in the library now are \n";
	ifstream file2("library.txt");
	while (getline(file2, rbook.author_name)) {
		std::cout << "\n";
		std::cout << "Book No." << b++ << endl;
		std::cout << "Author Name : " << rbook.author_name << endl;
		getline(file2, rbook.book_Name);
		std::cout << "Name of the Book : " << rbook.book_Name << endl;
		file2 >> rbook.book_ID;
		file2.ignore();
		std::cout << "Book ID : " << rbook.book_ID << endl;
		file2 >> rbook.Price;
		file2.ignore();
		std::cout << "Book Price : " << rbook.Price << endl;
		file2 >> rbook.Quantity;
		file2.ignore();
		std::cout << "Quantity :" << rbook.Quantity << endl << endl;

	}cout << "book no:" << U << " has been succesfully Removed\n";file2.close();
}
//__________________________
//function for book price
//------------------------
float Bookprice(int book_no) {
	float a;
	ofstream F("LIB.TXT",ios::app);
	Books book;
	ifstream show("library.txt");
	if (!show.is_open()) {
		std::cout<<"error:file doesnt open\n";
		return -1;
	}
	else {
		
		
		int i = 1;bool bok_found=false;
		while (show >> book.author_name >> book.book_Name >> book.book_ID >> book.Price >> book.Quantity) {
			
			if (i == book_no) {
				bok_found = true;
				
				a = book.Price;
				F << book.author_name <<"\n" << book.book_Name <<"\n" << book.book_ID <<"\n" << book.Price <<"\n" << book.Quantity-1<<"\n";
				if (book.Quantity < 1) {

					char x;
					cout << book.book_Name << " is NOT AVAILABLE!!(whole stock has either be issued or sold) \n";
					 
				}

			}else {
				F << book.author_name << "\n" << book.book_Name << "\n" << book.book_ID << "\n" << book.Price << "\n" << book.Quantity << "\n";

				i++;
			}


		}if (!bok_found) { system("cls");cout << "\n\n\t\tBOOK NOT FOUND !! Invalid Button entered...........";this_thread::sleep_for(std::chrono::seconds(1)); return 0; };
	}F.close();show.close();remove("library.txt");if (rename("LIB.TXT", "library.txt") != 0) { cout << "Error\n"; }return a;
	}
		//----------------------------------
		//show book function definition//
			//-------------------------------
		void show_book() {
			system("cls");
			Books book;int b=1;
			std::cout << "E - Library Books\n";
			ifstream show("library.txt");
			if (!show.is_open()) {
				std::cout << "Error! File doesn't open\n";

			}
			else
				while (getline(show, book.author_name)) {
					std::cout << "\n";
					std::cout << "Book # " << b++ << endl;
					std::cout << "Author Name : " << book.author_name << endl;
					getline(show, book.book_Name);
					std::cout << "Name of the Book : " << book.book_Name << endl;
					show >> book.book_ID;
					show.ignore();
					std::cout << "Book ID : " << book.book_ID << endl;
					show >> book.Price;
					show.ignore();
					std::cout << "Book Price : " << book.Price << endl;
					show >> book.Quantity;
					show.ignore();
					cout << "Quantity Available :" << book.Quantity << endl << endl;
					

				}
			show.close();
		}
	
		
		//________________________
        //Add book function definition
		//-------------------------

		void Addbook() {
			ifstream file("library.txt");
		a:	system("cls");
			
				Books book,chck;
				cout << "\n\t\t\tADD BOOK\n";
				cout << "Enter Book author Name: ";
				std::cin >> book.author_name ;
				cout << "Enter Book Name: ";
				std::cin >> book.book_Name;
				{
					std::ifstream file("library.txt");
					Books chck;

					while (file >> chck.author_name >> chck.book_Name >> chck.book_ID >> chck.Price >> chck.Quantity) {
						if (book.book_Name == chck.book_Name) {
							system("CLS");
							std::cout << "\n\n\n\t\tThis Book is already Available | Add any other book";
							file.close(); 
							std::this_thread::sleep_for(std::chrono::seconds(2));
							goto a;
						}
					}
					file.close();
				}
				cout << "Enter book ID: ";
				std::cin >> book.book_ID;
				cout << "Set Book Price: ";
				std::cin >> book.Price;
				std::cout << "Set Quantity: ";
				std::cin >> book.Quantity;
				ofstream lib("library.txt", ios::app);
				lib << book.author_name << "\n";
				lib << book.book_Name << "\n";
				lib << book.book_ID << "\n";
				lib << book.Price << "\n";
				lib << book.Quantity << "\n";
				lib.close();
				cout << book.book_Name << " \thas beenAdded to the LIBRARY\n";

			}
			
    	//__________________
		//Main 
		//--------------

		using namespace std;
		int main()
		{

			

			float sum = 0;
			char  A, M, z,ch;
			char opt;

			cout << "\t\t\t**********************************************************\n";
			cout << "\t\t\t*  *  |_| * |_| * LIBRARY MANAGEMENT SYSTEM * |_| * |_|  *\n";
			cout << "\t\t\t**********************************************************\n\n";
			cout << "\t\t\t\t******************************************\n";
			cout << "\t\t\t\t* ||* Muhammad Taha  &  Moin Bukhari *|| *\n";
			cout << "\t\t\t\t******************************************\n\n\n";/*Mein:*/
			cout << "\t\t \t\t\tpress ENTER to continue \n\t----------------------------------------------------------------------------------------------\n\t\t\t\t\t-->";
			
			cin.ignore();
			do {
			Main:system("CLS");
				cout << "\t\t|#####################################################################|\n";
				cout << "\t\t|     M   M            **           ******              *   *         |\n";
				cout << "\t\t|    M M M M          A__A            **                **  *         |\n";
				cout << "\t\t|   M   M   M         A  A            **                * * *         |\n";
				cout << "\t\t|   M   M   M         A  A          ******              *  **         |\n";
				cout << "\t\t|#####################################################################|\n";

				cout << "\n\n\t\t|^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^|\n";
			    cout << "\t\t|                      ____________          |\n";
				cout << "\t\t|                     ( *          *         |\n";
                cout << "\t\t| (U) User Login       * *          *        |\n";
				cout << "\t\t| (N) Sign up           * *          *       |\n";
				cout << "\t\t| (C) Check User Account * *          *      |\n";
				cout << "\t\t| (A) Admin Sign in       * *__________*     |\n";
				cout << "\t\t|                          *(         (      |\n";
	            cout<<  "\t\t|                            ^^^^^^^^^^^     |\n";
				cout<<  "\t\t|********************************************|\n";
				                                 
				                                 
				std::cin >> opt;
				while (opt != 'u' && opt != 'U' && opt != 'a' && opt != 'A' && opt != 'n' && opt != 'N'&& opt!='c' && opt!='C') {
				MainMenu:
					system("CLS");cout << "invalid key entered!! Enter Again\n";

					cout << "\n\n\t\t|^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^|\n";
					cout << "\t\t|                      ____________          |\n";
					cout << "\t\t|                     ( *          *         |\n";
					cout << "\t\t| (U) User Login       * *          *        |\n";
					cout << "\t\t| (N) Sign up           * *          *       |\n";
					cout << "\t\t| (C) Check User Account * *          *      |\n";
					cout << "\t\t| (A) Admin Sign in       * *__________*     |\n";
					cout << "\t\t|                          *(         (      |\n";
					cout << "\t\t|                            ^^^^^^^^^^^     |\n";
					cout << "\t\t|********************************************|\n";
					std::cin >> opt;
				}
				 if (opt == 'C' || opt == 'c')
				 {
					 string w;
					 system("cls");
					check_user_details();
					cout << "press any button to go back\n";cin >> w;if (w != "p32") { goto Main; }
				}
				else if (opt == 'A' || opt == 'a') {
				adminMenu:system("CLS");

					//___________________
					// Admin section
                    //-------------------
					cout << "\n\n\n\t\t\tEntering in admin section.................\n";this_thread::sleep_for(std::chrono::seconds(1));system("cls");
					cout << "\t\t\t* * -ADMIN SECTION- * *\n";
					cout << "\t\t\t_________________________\n";
					string p;cout << "Enter Admin password\n";
					

					while ((ch = _getch()) != '\r') {
						if (ch == '\b') { 
							if (!p.empty()) {
								p.pop_back(); 
								std::cout << "\b \b"; 
							}
						}
						else {
							p += ch; 
							std::cout << '*'; 
						}
					}while (p != "password") { cout << "!!Wrong Password\nEnter Again";std::cin >> p; }
					do {
						cout << "\tADD A BOOK (A)\n\tREMOVE A BOOK  (R)\n";
						std::cin >> A;

						if (A == 'A' || A == 'a') {
						Addbookagain:cout << "\t\tAdd a Book\n";
							Addbook();
						}
						else if (A == 'R' || A == 'r') {
							int x;remove_book_again:system("cls");
							show_book();
							cout << "PLEASE SELECT A BOOK TO REMOVE\n!write Book no.!!\n";
							std::cin >> x;
							Remove_book(x);
						} {
							do {
								cout << "\t\tRemove another (R) \nAdd another book (A)\n";
								cout << "\t\tAdmin Menu     (M) \n";
								cout << "\t\tMain Menu (N)\n\t\tENTER: ";
								std::cin >> z;
								if (z == 'r' || z == 'R') { goto remove_book_again; }
								else if (z == 'a' || z == 'A') { goto Addbookagain; }
								else if (z == 'm' || z == 'M') { system("cls");cout << "\n\n\t\tMoving Back to ADMIN MENU...........";this_thread::sleep_for(std::chrono::seconds(1)); goto adminMenu; }
								else if (z == 'n' || z == 'N') { system("cls");cout << "\n\n\t\tMoving Back to  MENU...........";this_thread::sleep_for(std::chrono::seconds(1));goto Main; }
								else cout << "PLease Enter correct Key\n";
							} while (z != 'r' || z != 'R' && z != 'a' || z != 'A' && z != 'm' || z != 'M');

							/*else { exit(1); }*/


						}

					} while (A != 'A' && A != 'a' || A != 'r' && A != 'R');
					//_____________________
					// USER SECTION
			//-----------------------------
				}
				else if (opt == 'u' || opt == 'U')
				{
					system("cls");cout << "\n\n\t\tMoving to USER LOGIN...........";this_thread::sleep_for(std::chrono::seconds(1));
					system("cls");cout << "\n\t\t\t\t|| USER LOGIN ||\n\n";
					char y, h, a;User u;
					string file_id;
					cout << "\n\t\t\t User ID : ";cin >> file_id;
					user_login(file_id);

					system("CLS");char X;Books b;
					cout << "\t\t\tWELCOME TO OUR E-LIBRARY\n\n";
					cout << "\n\t\tSearch a book (S)\t|\tSee All available books(A)\t|\tQuit(Q)\n\t\t\t-->";
					cin >> X;
					switch (X) {
					case 'a': {
						
							 {
								system("cls");cout << "\n\n\t\tCOLLECTING BOOKS FOR YOU...........";this_thread::sleep_for(std::chrono::seconds(1));
							A:	show_book();
								
								int num;//book no. entered by user
								
								
									User u;string a;Books book;int x = 1;
								
									cout << "\t\tWrite Book # : ";cin >> num;
									ifstream file;
									file.open("library.txt");
									while (file >> book.author_name >> book.book_Name >> book.book_ID >> book.Price >> book.Quantity) {
										if (num == x) {
											a = book.book_Name;
										}
										x++;
									}if (a == "") {system("cls");cout << "\n\n\t\tWrong button Entered...........";this_thread::sleep_for(std::chrono::seconds(1));goto A; }

									file.close();
									issue_book(file_id, a);

								
							}cout << "\t\t(Y) Lend another book   \n\t\t(M) Main Menu " << endl;
							cin >> h;
							while (h != 'y' && h != 'Y' && h != 'M' && h != 'm') { cout << "Please Enter only M or Y :";cin >> h; }
							if (h == 'y' || h == 'Y') { system("cls");cout << "Moving to lend book Again......";this_thread::sleep_for(std::chrono::seconds(1));goto y; }
							else if (h == 'M' || h == 'm') { system("cls");cout << "Moving to Main Menu.......";this_thread::sleep_for(std::chrono::seconds(1)); goto Main; }



						
					}break;
					case'A': {y:system("cls");cout << "\n\n\t\tCOLLECTING BOOKS FOR YOU...........";this_thread::sleep_for(std::chrono::seconds(1));
						
							 
								show_book();
						{int num;
							User u;string a;Books book;int x = 1;
						
							cout << "\t\tWrite Book Number : ";cin >> num;
							ifstream file;
							file.open("library.txt");
							while (file >> book.author_name >> book.book_Name >> book.book_ID >> book.Price >> book.Quantity) {
								if (num == x) {
									a = book.book_Name;
								}
								x++;
							}
							if (a == "") { system("cls");cout << "\n\n\t\tWrong button Entered...........";this_thread::sleep_for(std::chrono::seconds(1));goto A; }

							file.close();
							issue_book(file_id, a);

						}cout << "\t\t(Y) Lend another book   \n\t\t(M) Main Menu " << endl;
						cin >> h;
						while (h != 'y' && h != 'Y' && h != 'M' && h != 'm') { cout << "Please Enter only M or Y :";cin >> h; }
						if (h == 'y' || h == 'Y') { system("cls");cout << "Moving to lend book Again......";this_thread::sleep_for(std::chrono::seconds(1));goto y; }
						else if (h == 'M' || h == 'm') { system("cls");cout << "Moving to Main Menu.......";this_thread::sleep_for(std::chrono::seconds(1)); goto Main; }

					
					}break;
					
					case 's': {

						search_book(b, file_id);
					}break;
					case 'S': {

						search_book(b, file_id);
						break;}
					case'q': {
						return 0;
						break;}
					case 'Q': {return 0;
					}

					}


				}
				//____________
				// New user
				//------------

				else if (opt == 'n' || opt == 'N')
				{
					char B;N:
				string file_id;system("cls");
				std::cout << "\n\n\t\t\tAre you from air university (Y) for Yes (N) for NO: ";
				cin >> A;if (A == 'N' || A == 'n') {
					std::cout << "\t\tSorry you are not eligible to be a member of This library\n";

				w:std::cout << "\t\tchange preference (N)\n\t\tExit program (E)\n\t\tMain Menu press (M)";
					cin >> B;if (B == 'N' || B == 'n') { goto N; }
					else if (B == 'E' || B == 'e') { return 0; }
					else if (B == 'm' || B == 'M') {
						system("cls");cout << "\n\n\t\tMoving to MAIN MENU...........";this_thread::sleep_for(std::chrono::seconds(1));system("cls");goto Main;
					}
					else {
						cout << "\t\tWrong button pressed !! ";goto w;
					}
				}
				else if (A == 'Y' || A == 'y') {
					system("cls");

					cout << "\n----------------------------------------------------------------------------------------------------\n";
					std::cout << "\n\t\t\t\tNew User Registration\n\n";
					cout << "\t\t\t==================================\n";
					std::cout << "\t\t\t Please Enter your details \n";

					cout << "\t\t\tCreate a Unique User ID \t\t(i.e :taha456)\n\n\t\t\tCREATE USER ID:";

					cin >> file_id;
					new_user(file_id);
				}
				else {
					system("cls");cout << "\t\t\tplease select Only from N and Y\n";this_thread::sleep_for(std::chrono::seconds(2));system("cls");goto N;
				}

				}
				/*else if (opt == 'C' || opt == 'c') 
				{
					void check_user_details();
				}*/
				else cout << " \t\tMain Menu press (M)   |   Exit press (E)\n";
				std::cin >> M;if (M == 'e' || M == 'E') { return 0; }
				} while (M == 'm' || M == 'M');
			}
