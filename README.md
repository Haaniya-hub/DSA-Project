#include<iostream>
#include<limits>
#include<string>

using namespace std;

struct Doctor
{
int doctorID;
string name;
string specialization;
string contact;

double fee;
Doctor* next;
Dotor* prev;

Doctor(int id, string dName, string dSpec, string dContact, double dFee = 2500.0)
{
doctorID = id;
name = dName;
specialization = dSpec;
contact = dContact;
fee= dFee;

next = NULL;
prev = NULL;
}
};

class DoctorManagement 
{
private:

Doctor * head;
Doctor * tail;
int nextId;

public:
DoctorManagement()
{
head=NULL;
tail=NULL;
nextId=1;
}

bool isEmpty() const
{
return head == NULL;
}

Doctor* findDoctor(int id) const
{
Doctor* current = head;
while(current!=NULL)
{
if(current->doctorID ==id)
{
  return current;
  }
  return NULL;
  }

  int insertDoctor(string name, string specialization ,string contact ,double fee = 2500.0)
  {
  int assignedId = nextId++;
  Doctor* newDoctor = new Doctor(assignedId, name, specialization, contact,fee)

  {
  if (head==NULL)
  {
  head = tail = newDoctor;
  }
  else
  {
  tail->next = newDoctor;
  newDoctor->prev = tail;
  tail = newDoctor;
  }
  return assignedId;
  }

  bool updateDoctorById(int id, string newName, string newSpec, string newContact)
  {
  Doctor* target = findDoctor(id);
  if(target == NULL)
  {
  return false;
  }
  target->name = newName;
  target->specialization = newSpec;
  target->contact = newContact;
  return true;
  }

  bool updateDoctorFeeById(int id,double newFee)
  {
  Doctor* target = findDoctor(id);
  if(target == NULL)
  {
  return false;
  }

  target->fee = newFee;
  return true;
}

bool deleteDoctorById(int id)
{
if (isEmpty())
{
return false;
}

Doctor* current = findDoctor(id);
if(current == NULL)
{
return false;
}

if(current == head && current == tail)
{
     head = NULL;
     tail = NULL;
}

else if ( current == head)
{
 head = head->next;
if(head != NULL)
{ 
  head-> prev = NULL;
}
}

else if (current == tail)
{
tail = tail->prev;

if (tail != NULL)
{
   tail->next =NULL;

}
}
else
{
  current->prev->next = current->next;
  current->next->prev = current->prev;
}

delete current;
return true;
}

void displayDoctors() const
{
     if(isEmpty())
     {
        cout<<"\n No Doctor record found\n";
        return;
     }

     Doctor* current = head;
     cout<<"\n All Doctor Records\n";

     while( current != NULL)
     {
      cout<<"\nID: "<< current->doctorID <<endl;
      cout<<"\nName: "<< current->name <<endl;
      cout<<"\nSpecilization: "<< current->specialization <<endl;
      cout<<"\nContact: "<< current->contact <<endl;
      cout<<"\n Fee: "<< current->fee <<endl;

      current = current-> next;
      }
      }

 ~DoctorManagement()
 {
 Doctor* current = head;
 while( current!= NULL)
 {
   Doctor* temp = current;
   current = current-> next;
   delete temp;
   }

   head = NULL;
   tail = NULL;
   }
   };

namespace
{
void clearInvalidInput()
{
cin.clear();
cin.ignore(numeric_limits<streamsize>::max(), '\n');
}
}

      
      
      

      
     









  
  
  






//======================================================
//MODULE 3: PATIENT MANAGEMENT ( SINGLY LINKED LIST)
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

//=====================================================
MODULE 2: APPOINTMENT MANAGEMENT (QUEUE / LINKED LIST)
//=====================================================

//Node structure storing appointment details along with linked patient & doctor info
struct Appointment {
       int appointmentID;
       int patientID;
       string patientName;
       string patientDisease;
       int doctorID;
       string doctorSpecialization;
       string day;
       string time;
       double fee;
       Appointment* next; //Pointer to next appointment in FIFO queue

// Constructor to intialize all appointment fields 
Appointment(int appId, int pId, string pNamee, string pDisease, int dId, string dSpec, string appDay, string appTime, double appFee) {
       appointmentID = appId;
       patientID = pId;
       patientName = pNmae;
       patientDisease = pDisease;
       doctorID = dId;
       doctorSpecialization = dSpec;
       day = appDay;
       time = appTime;
       fee = appFee;
       next = NULL;
}
};

// Manages appointments using a FIFO Linked Queue 
class AppointmentManagement{
private:
       Appointment* front;   //Front of the queue 
       Appointment* rear;    //Rear of the queue
       int nextAppointmentID; //Auto incrementing appointment ID starting at 101

// Prints formatted details of a single appointment node
void printAppointmentRecord(const Appointment* current) const{
       cout<<"\n App ID:" <<current ->appointmentID; 
       cout<<"\n Patient ID:" <<current ->patientID;
       cout<<"\n Patient Name:" <<current ->patientName;
       cout<<"\n Disease:" << current ->patientDisease;
       cout<<"\n Doctor ID:" << current ->doctorID;
       cout<<"\n Specialization:" <<current ->doctorSpecialization;
       cout<<"\n Day:" <<current ->day;
       cout<<"\n Time:" <<current ->time;
       cout<<"\n Fee:" <<current ->fee;
       cout<<"\n---------------------\n";
}

public:
// Initializes an empty appointment queue

AppointmentManagement() {
       front = NULL;
       rear = NULL;
       nextAppointmentID = 101;
}

//Frees all dynamically allocated appointment nodes 
~AppointmentManagement() {
       while(front!=NULL) {
       Appointment* temp = front;
       front = front ->next;
       delete temp;
}
       rear = NULL;
}

// Books (enqueues) a new appointment after verifying patient and doctor IDs 
void insertAppointment(PatientLinkedList* patientList = NULL, DoctorManagement* doctorList = NULL) {
       int pId, dId;
       string day, time;
       
// Ensure at least one doctor exists before booking 
if(doctorList == NULL || doctorList ->isEmpty()) {
       cout<<"\n No doctors available! Please add a doctor first. \n";
       return;
}
       cout<<"\n Enter Patient ID:";
       cin>> pId;
       if(cin.fail()) {
       clearInvalidInput();
       cout<<"\n Invalid Patient ID! \n";
       return;
}
// Fetch patient record automatically using patient ID
Patient* pat = (patientList != NULL) ? patientList ->searchPatient(pId) : NULL;
if(pat == NULL) {
       cout<< " Patient ID" <<pId<< "does not exist. Add the Patient first. \n ";
       return;
}

//show available doctors so user can pick a Doctor ID
doctorList ->displayDoctors();

cout<<" Enter Doctor ID:";
cin>> dId;
if(cin.fail()) {
        clearInvalidInput();
        cout<<"\n Invalid Doctor ID! \n";
        return;
}
// Fetch doctor record automatically using Doctor ID
Doctor* doc = doctorList->findDoctor(dId);
if(doc == NULL) {
        cout<<" Doctor ID" << dId <<" does not exist. Add the doctor first. \n";
        return;
}
cin.ignore(numeric_limits<streamsize>::max(), '\n');

cout<<" Enter Day:";
getline(cin, day);

cout<<" Enter Time:";
getline(cin, time);

// Pull patient and doctor attributes for the appointment record 
string pName = pat->name;
string pDisease = pat->disease;
string dSpec = doc->specialization;
double appFee = doc->fee;

Appointment* newAppointment = new Appointment(
        nextAppointmentID++,
        pId,
        pName,
        pDisease,
        dId,
        dSpec,
        day,
        time,
        appFee,
);

// Enqueue at rear
if (front == NULL) {
        front = rear = newAppointment;
} else 
{
        rear-> next = newAppointment;
        rear = newAppointment;
}
        cout<< "\n Appointment Added Successfully! Auto ID:"<<newAppointment->appointmentID <<"\n";
}
// Searches appointments by Appointment ID or Patient ID
void searchAppointment() const {
        int choice, id;

        cout<< "\n Search by:\n 1. Appointment ID\n2. Patient ID\n Enter Choice:";
        cin>> choice;

        if(cin.fail()) {
        clearInvalidInput();
        cout<< "\n Invalid search choice! \n";
        return;
}

Appointment* current = front;
bool found = false;

if( choice ==  1) {
        cout<<" Enter Appointment ID to Search:";
        cin>>id;
if(cin.fail()) {
        clearInvalidInput();
        cout<<"\n Invalid ID! \n";
        return;
}
while(current!= NULL) {
        if(current->appointmentID == id) {
        cout<<"\n Appointment Found!\n";
        printAppointmentRecord(current);
        found= true;
        break;
}
        current= current->next;
}
} else if (choice == 2) {
        cout<<" Enter Patient ID to Search:";
        cin>>id;
        if(cin.fail()) {
        clearInvalidInput();
        cout<< "\n Invalid ID!\n";
        return;
}
While(current != NULL) {
        if(current-> patientID == id) {
        cout<<"\n Appointment Found!\n";
        found = true;
}
        current= current->next;
}
} else {
        cout<<"\n Invalid search choice! \n";
        return;
}
if(!found) {
        cout<<"\n No matching appointment found!\n";
}
}
// Updates an existing appointment's linked patient, doctor, day, and time
void updateAppointment(PatientLinkedList* patientList = NULL, DoctorManagement* doctorList = NULL)
{
int id;
cout<<"\n Enter Appointment ID to Update:";
cin>>id;
if(cin.fail()) {
clearInvalidInput();
cout<<"\n Invalid ID! \n";
return;
}
Appointment* current = front;
while(current!= NULL) {
            if(current->appointmentID == id) {
            int newPId, newDId;

            cout<<"\n Enter New Patient ID:";
            cin>>newPId;
            if(cin.fail()) {
            clearInvalidInput();
            cout<<"\n Invalid Patient ID!\n";
            return;
}
            if(doctorList!= NULL && !doctorList->isEmpty()) {
               doctorList->displayDoctors();
}
            cout<<" Enter New Doctor ID:";
            cin>>newDId;
            if(cin.fail()) {
            clearInvalidInput();
            cout<<"\n Invalid Doctor ID!\n";
            return;
}
Patient* pat = (patientList !=NULL) ? patientList->searchPatient(newPId) : NULL;
if(pat== NULL) {
            cout<<" Patient ID" << newPId <<" does not exist. Appointment not updated. \n";
            return;
}
Doctor* doc =(doctorList != NULL) ? doctorList->findDoctor(newDId) : NULL;
if(doc == NULL) {
            cout<<"Doctor ID" << newDId << " does not exist. Appointment not updated. \n";
            return;
}
cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout<<"Enter New Day:";
            getline(cin, current->day);
    
            cout<<"Enter New Time:";
            getline(cin, current->time);
// Refresh snapshot fields from updated patient and doctor records
            current->patientID = newPId;
            current->patientName = pat->name;
            current->patientDisease = pat->disease;
            current->doctorID = newDId;
            current->doctorSpecialization = doc->specialization;
            current->fee = doc->fee;

            cout<<'\n Appointment Updated Successfully!\n";
            return;
}
           current= current->next;
}
            cout<<"\n Appointment Not Found!\n";
}

// Dequeue the front from appointment
void deleteAppointment() {
             if(front == NULL) {
             cout<<"\n No Appointments Available!\n";
             return;
}
   Appointment* temp = front;
   front = front->next;

   // Reset rear pointer if queue become empty
   if(front == NULL) {
   rear = NULL;
   }

   delete temp;
   cout<<"\n Appointment Removed Successfully!\n";
} 
// Traverses and displays all queued appointments from front to rear
void displayAppointment() const {
if(front == NULL) {
        cout<<"\n No Appointment Records Found! \n";
        return;
}
Appointment* current = front;
cout<<"\n ====== ALL APPOINTMENT RECORDS ==========\n";

while(current!= NULL) {
    printAppointmentRecord(current);
    current= current-> next;
}
}
};

// Interactive menu for Appointment Management operations
void appointmentModuleMenu(AppointmentManagement& appointmentSystem, PatientLinnkedList& patients, DoctorManagement& doctors) {
     int appointmentChoice;

do{
    cout<<"\n========== APPOINTMENT MANAGEMENT=================";
    cout<<"\n1. Insert Appointment";
    cout<<"\n2. Search Appointment";
    cout<<"\n3. Update Appointment";
    cout<<"\n4. Delete Appointment";
    cout<<"\n5. Display Appointment";
    cout<<"\n6. Back/ Exit";

    cout<<"\n Enter Choice:";
    cin>>appointmentChoice;
    
   if(cin.fail()) {
   clearInvalidInput();
   cout<<"\n Invalid choice! Please try again.\n";
   continue;
}

switch(appointmentChoice) {
       case 1:
       appointmentSystem.insertAppointment(&patients, &doctors);
       break;
       case 2:
       appointmentSystem.searchAppointment();
       break;
       case 3:
       appointmentSystem.updateAppointment(&patients, &doctors);
       break;
       case 4:
       appointmentSystem.deleteAppointment();
       break;
       case 5:
       appointmentSystem.displayAppointments();
       break;
       case 6:
       cout<<"\n Exiting Appointment Management...\n";
       break;
       default:
       cout<<"\n Invalid Choice! Please try again.\n";
       break;
       }
       }
       while(appointmentChoice !=6);
}

        







