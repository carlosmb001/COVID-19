#include <iostream>
#include <fstream>
#include <vector>
  
 using namespace std;
void printintro();

 class patientRegistry {
     
 public:
     void setName(string n){
         name = n;
     }
     void setAddressStreet(string a){
         addressStreet = a;
     }
     void setAddressCity(string c){
         addressCity = c;
     }
      void setZipcode(int z){
            zipcode = z;
     }
     void setBirthday(string b){
         birthday = b;
     }
     void setPhoneNumber (int n){
         phoneNumber = n;
     }
     string getName() const {
         return name;
     }
     string getAddressStreet() const{
         return addressStreet;
     }
     string getAddressCity() const{
     return addressCity;
     }
     int getZipcode() const{
     return zipcode;
     }
     string getBirthday() const{
         return birthday;
     }
     int getPhoneNumber() const{
         return phoneNumber;
     }
     void printintro(){
         cout << "This program will ask you a series of questions to determine if you are eligible for COVID-19 testing.\n";
         cout << "If your're eligible, we'll ask for some information and contact you with further instructions and information.\n";
         cout << "For the following questions answer Y for Yes, N for No.\n";
     }
     
     
 private:
     string name;
     string addressStreet;
     string addressCity;
     int zipcode;
     string birthday;
     int phoneNumber;
 };

  
 int main () {
       
    int numtimes = 0;
     string n;
     string a;
     string b;
     string c;
     string s;
     int z;
     string line;
     patientRegistry pr;
     
     vector<string> covidSym;
     covidSym.push_back("cough");
      covidSym.push_back("shortness of breath");
      covidSym.push_back("fever");
      covidSym.push_back("chills");
      covidSym.push_back("muscle pain");
      covidSym.push_back("sore throat");
      covidSym.push_back("lose sense of smell or taste");
     
     pr.printintro();// Displays the intro for the program
    
     
     for ( int i =0; i < covidSym.size() ; ++i)// will ask the patient a series of questions
     {
         char patientAns;
         cout << "In the past 14 days have to experienced " << covidSym.at(i) << "?";
         cout << "(Y/N)\n";
         cin >> patientAns;
         if (patientAns == 'y' || patientAns == 'Y')
         {
             numtimes = numtimes +1;
         }
            else if (patientAns == 'n' || patientAns == 'N')
            {
                 cout << "Noted.\n";
             }
                else
                {
                    cout << "Invalid input, try again (Y/N)? \n";
                    cin >> patientAns;
                    
                }
         cout << numtimes << endl;
     }
     
      if (numtimes >= 2){
             
             cout << "You have two or more symptoms of Coronavirus we are going to ask for your some information to store in our file system." << endl;
             
             cout << "What is your name?" << endl;
             getline(cin, n);
             pr.setName(n);
          
          
            cout << "When were you born? (MM/DD/YY)" << endl;
            getline(cin, b);
            pr.setBirthday(b);
                  
             cout << "What is your street address?" << endl;
             getline(cin, a);
             pr.setAddressStreet(a);
          
            cout << "What is your City address?" << endl;
            getline(cin, c);
            pr.setAddressCity(c);
          
            cout << "What is your Zipcode?" << endl;
            cin >> z;
            pr.setZipcode(z);
          
            cout << "What is your Phone Number?" << endl;
            cin >> z;
            pr.setPhoneNumber(z);
          
             
             fstream dataFile("Patient.txt", ios::out);
             
             dataFile << "Name: " << pr.getName() << endl;
             dataFile << "Birthday: " << pr.getBirthday() << endl;
             dataFile << "Street Address: " << pr.getAddressCity() << endl;
             dataFile << "City: " << pr.getAddressStreet() << endl;
             dataFile << "Zipcode: " << pr.getZipcode() << endl;
             dataFile << "Phone Number: " << pr.getPhoneNumber() << endl;
             
             cout << "Your personal information has been sucessfully saved in our file system." << endl;
             dataFile.close();
             
             dataFile.open("Patient.txt", ios::in);
             
             cout << "Here is how your personal information looks in our system: " << endl;
             while (getline(dataFile, line)){
                 cout << line << endl;
         }
             dataFile.close();
             
         }
         else {
             cout << "You do not have any Coronavirus symptoms. Thank you for visiting and wish you the best!" << endl;
         }
         
         return 0;
     }

