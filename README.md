#include<iostream>
#include<limits>
#include<string>

using namespace std;

//======================================================
//MODULE 2: PATIENT MANAGEMENT ( SINGLY LINKED LIST)
//======================================================

//Node structure representing a single patient in the singly linked list 
struct Patient {
int id;
string name;
int age;
string disease;
Patient* next;  //Pointer to the next patient node

//Constructor to initialize patient fields 
Patient (int pId , string pName , int pAge , string pDisease ){
id = pId;
name = pName ;
age = pAge ;
disease = pDisease ;
next = nullptr ;
}
};

//Manages patient records dynamically sing singly linked list 
class PatientLinkedList {
private:
Patient* head;  //First patient node in the list
int nextId;     //Auto-incrementing ID generator for new patients

public:
//Initializes an empty singly linked list 
PatientLinkedList() {
head = nullptr;
nextId = 1;
}

//Frees all dynamically allocated patient nodes
~PatientLinkedList() {
Patient* curr = head;
while (curr != nullptr ) {
Patient * temp = curr;
curr = curr->next;
delete temp;
}
head = nullptr;
}

// Checks if a patient ID already exists in the list 
bool idExists (int id) const {
Patient* curr = head ;
while ( curr != nullptr ){
if ( curr-> id == id) {
return true ;
}
curr = curr->next;
}
return false ;
}

//Appends a new patient node at the end of the singly linked list 
bool addPatient ( string name , int age , string disease ) {
Patient* newNode = new Patient ( nextId , name , age disease );
nextId++;

if(head==nullptr ) {
head = newNode ;
return true ;
}

Patient* curr = head;
while ( curr->next != nullptr) {
curr = curr->next ;
}

curr->next = newNode ;
return true ;
}

//Searches for a patient by Id 
Patient* searchPatient(int id) const {
Patient* curr = head ;
while (curr!= nullptr){
if (curr->id == id){
return curr;
}
curr = curr->next ;
}
return nullptr;
}

//Update patient name , age , disease by ID 
bool updatePatientById( int id,string newName , int newAge, string newDisease) {
Patient* target = searchPatient(id);
if (target == nullptr ) {
return false;
}

target->name = newName ;
target->age = newAge ;
target->disease = newDisease;
return true ;
}

//Delete a patient node by ID 
bool deletePatientById  int id ) {
if (head == nullptr ) {
return false ;
}

//Case 1: Target node is at the head 
if ( head->id == id ) {
Patient* temo = head ;
head = head->next ;
delete temo ;
return true ;
}

//Case 2: Target node is after head 
Patient* prev = head ;
Patient* curr = head->next ;
while(curr != nullptr ) {
if ( curr->id == id ){
prev->next = curr->next ;
delete curr;
return true ;
}
prev =curr;
curr = curr->next;
}

return false ;

//Traverses and prints all patients records from head to end 
void traversePatients() const {
if (head ==nulllptr ){
cout <<" No patient records found ( list is empty ).\n";
return ;
}

Patient* curr=head ;
cout <<"\m---Patient Records---\n";
while (curr!= nullptr ){
cout << "ID : " <<curr->id
     << " | Name : " <<curr->name 
     << " | Age : " <<curr->age
     << " | Disease : " <<curr->disease<<"\n";
     curr = curr->next ;
     }
  }
};

//Interactive menu for Patient Management Operations 
void PatientModuleMenu(PatientLinkedList & patients) {
int choice ;

do{
cout<<"\n==========PATIENT MODULE MENU ========== \n";
cout << "1.Add Patient (Auto ID )\n";
cout << "2. Search Patient by ID \n";
cout << "3. Update Patient by ID \n";
cout << "4. Delete Patient by ID \n";
cout<<" 5. Display All Patients (Traversal )\n";
cout<< " 0. Back to the main menu / Exit\n";
cout<<" Enter choice ";
cin>>choice ;

id (cin.fail()){
clearInvaludInput();
cout<" Invalid input ! Please enter a number .\n";
continue;
}

if (choice == 1) {
string name , disease ;
int age;

cin.ignore ();
cout<<"Enter Name :" ;
getline(cin,name);

cout<<"Enter Age : ";
cin>> age ;
if (cin.fail ()) {
clearInvalidInput();
cout<<"Invalid age ! Please enter a number \n";
continue ;
}
if (age <=0){
cin.ignore(numeric_limits<streamsize>::max(), '\n');
cout<<"Age must be greater than 0 \n";
continue;
}
cin.ignore(numeric_limits<streamsize>::max() , '\n');
Cout<<" Enter Disease :";
getline(cin,disease);

if (patients.addPatient(name, age , disease )) {
cout << " Patient added successfully !\n";
}else{
cout<<"Failed to add patient \n";
}
}else if (choice == 2){
int id;
cout <<"Enter PAtient ID to Search " ;
cin>>id;

if (cin.fail()) {
clearInvalidInput();
cout<< " Invalid Id ! Please enter a number \n";
continue;
}

Patient* p = patients.searchPatient(id);
if (p!=nullptr) {
cout << "Found -> ID : " << p->id
     <<" | Name : " << p->name 
     << " | Age : " << p->age 
     << " | Disease : " << p->disease << "\n" ;
     }else{
     cout<<"PAtient with ID " << id << " not found \n";
     }
     }else if (choice == 3){
     int id;
     cout <<" Enter Patiemt Id to update : " ;
     cin>> id;

if (cin.fail ()) {
clearInvalidInput():
cout<< " Invalid ID ! Please enter a number \n";
continue ;
}

Patient* target = patients.searchPatient(id);
if (target==nullptr) {
cout<< " Patient with ID " << id << " not found \n ";
}else{
int upChoice ;
cout<<" \n What you want to update ? \n" ;
cout<< " 1. Name\n";
cout<< " 2. Age\n";
cout<< " 3. Disease\n";
cout<< " 4. All (Name , Age , Disease )\n";
cout<< " Enter choice " ;
cin >> upChoice ;

if(cin.fail()) {
clearInvalidInput ();
cout<< "Invalid choice !\n";
continue;
}

if(upChoice == 1 ) {
cin.ignore();
cout<<" Enter new name : ";
getline ( cin,target->name );
cout<<"Name updated !\n";
}else if(upChoice== 2) {
int newAge ;
cout<< "Enter new age " ;
cin>> newAge ;
if (cin.fail()) {
clearInvalidInput();
cout<< " Invalid age ! Please enter a number \n" ;
cintinue ;
}
target->age=newAge ;
cout<<"Age updated ! \n" ;
} else if(upChoice == 3) {
cin.ignore ();
cout << "Enter  new disease " ;
getline ( cin, target->disease);
cout<< " Disease updated ! \n" ;
} else if ( upChoice == 4 ) {
string newName , newDisease;
int newAge ;

cin.ignore();
cout<< " Enter new name " ;
getline ( cin , newName );

cout <<" Enter new age " ;
cin >> newAge ;
if ( cin.fail ()) {
clearInvalidInput();
cout << " Invalid age ! Please enter a number \n";
continue ;
}
if (newAge <= 0) {
cout << " Age must be greater than 0 \n " ;
continue ;
}

cin.ignore(numeric_limits<streamsize>::max(), '\n') ;
cout << " Enter new disease : ";
getline ( cin, newDisease ) ;

if ( patients.updatePatientById(id, newName, newAge, newDisease )) {
cout << "All details updated ! \n";
} 
}else{
cout << "Invalid update option ! \n";
}
}
} else if (choice == 4 ) {
int id ;
cout< "enter Patient ID to delete : " ;
cin>> id;

if ( cin.fail()) {
clearInvalidInput();
cout<<" Invalid ID ! Please enter a number \n ";
continue;
}

if (patients.deletePatientById (id)) {
cout << " Patient Deleted successfully \n";
}else{
cout<< " Patient not found \n ";
}
}else if (choice == 5) {
patients.traversePAtients();
}else if(choice== 0){
cout <<" Exiting Patient Module .. \m";
}else{
cout <<" Invalid choice ! Try again \n ";
}

}while (choice != 0);
}
