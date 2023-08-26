# IPL_Ticket_Generator
This is a project built in C++, generates an 'IPL 2021 Ticket .txt' file which contains the user data like the Name of the user, and Teams playing in that match, the timing of the match. I have globally declared the variables for storing teams and venues. This program uses mainly conditional statements and file handling techniques.
#include<iostream>
#include<string>
#include<vector>
#include<conio.h>
#include<windows.h>
#include<fstream>
using namespace std;

//stores the team names and venue names globally
//declared a vector matches and will fill the vector with match fixtures in 'print_matches' function
//stored the name of the user globally
vector<string> teams{"Chennai Super Kings (CSK)","Delhi Captials (DC)","Kings XI Punjab (KXIP)","Kolkata Knight Riders (KKR)","Mumbai Indians (MI)",
                    "Rajasthan Royals (RR)","Royal Challengers Bangalore (RCB)","Sunrisers Hyderabad (SRH)"};
vector<string> venue{"M.A Chidambaram Stadium, Chennai","Arun Jaitley Stadium, New Delhi","IS Bindra Stadium (PCA), Mohali","Eden Gardens, Kolkata",
                    "Wankhede Stadium, Mumbai","Swami Mansingh Stadium, Jaipur","M. Chinnaswamy Stadium, Bangalore",
                    "Rajiv Gandhi International Cricket Stadium, Hyderabad"};
vector<string> matches{"0"};
string name;

void setcolorandbackground(int textc,int backg){//with this we can set text color and background color
    WORD color = ((backg & 0x0F)<<4) + (textc & 0x0F);
    SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE),color);
}

void title(){//prints title of the program
    system("CLS");
    cout << endl;
    setcolorandbackground(9,0);
    cout << "\t\t\t|-------------------------------|" << endl;
    cout << "\t\t\t|";
    setcolorandbackground(6,0);
    cout << "\tIPL Ticket Booking";
    setcolorandbackground(9,0);
    cout << "\t|" << endl;
    cout << "\t\t\t|-------------------------------|\n" << endl;
}

void print_mainmenu(){//Function for printing Main menu options
    setcolorandbackground(6,0);
    cout << "\n\n\t\t";
    setcolorandbackground(14,13);
    cout << "MAIN MENU";
    setcolorandbackground(9,0);
    cout << "\n\n\t1.Teams Playing IPL 2021" << endl;
    cout << "\n\t2.IPL 2021 Venues" << endl;
    cout << "\n\t3.Book a ticket" << endl;
    cout << "\n\tPress '0' to Exit this program...." << endl;
    cout << "\n\tEnter your Choice: ";
    setcolorandbackground(15,0);
}

void print_teams(){//function for printing teams
    title();
    cout <<"\n";
    setcolorandbackground(14,13);
    cout << "\t\tTEAMS PARTICIPATING IN IPL 2021";
    setcolorandbackground(15,0);
    cout << "\n";
    for(int i=0;i<8;i++){
        setcolorandbackground(15,0);
        cout << "\n\t" << i+1 << ". ";
        setcolorandbackground(3,0);
        cout << teams[i]<<endl;
    }
    setcolorandbackground(10,0);
    cout << "\n\n\tPress '0' to go back to main menu....";
    setcolorandbackground(15,0);
    return;
}

void print_venue(){//function for printing venues
    title();
    cout << "\n";
    setcolorandbackground(14,13);
    cout << "\t\tVENUES FOR IPL 2021";
    setcolorandbackground(15,0);
    cout << "\n";
    for(int i=0;i<8;i++){
        setcolorandbackground(15,0);
        cout << "\n\t" << i+1 << ". ";
        setcolorandbackground(3,0);
        cout << venue[i] <<endl;
    }
    setcolorandbackground(10,0);
    cout << "\n\n\tPress '0' to go back to main menu....";
    setcolorandbackground(15,0);
    return;
}

void print_matches(){//function for printing match fixtures
    int sno=1,high=1,low=0;
    title();
    cout << "\n";
    setcolorandbackground(14,13);
    cout << "\t\tMATCH FIXTURES FOR IPL 2021";
    setcolorandbackground(0,0);
    cout << "\n";
    while(low<7){//pushing elements into matches variable one by one and printing the matches too in O(1) time complexity
        matches.push_back(teams[low] + " vs " + teams[high] + " at " + venue[low]);
        setcolorandbackground(15,0);
        cout << "\n\t" << sno++ << ". ";
        setcolorandbackground(10,0);
        cout << teams[low];
        setcolorandbackground(15,0);
        cout << " vs ";
        setcolorandbackground(9,0);
        cout << teams[high];
        setcolorandbackground(15,0);
        cout << " at ";
        setcolorandbackground(6,0);
        cout << venue[low] << endl;
        matches.push_back(teams[high] + " vs " + teams[low] + " at " + venue[high]);
        setcolorandbackground(15,0);
        cout << "\n\t" << sno++ << ". ";
        setcolorandbackground(10,0);
        cout << teams[high];
        setcolorandbackground(15,0);
        cout << " vs ";
        setcolorandbackground(9,0);
        cout << teams[low];
        setcolorandbackground(15,0);
        cout << " at ";
        setcolorandbackground(6,0);
        cout << venue[high] << endl;
        high++;
        if(high>7){
            low++;
            high = low+1;
        }
    }
    setcolorandbackground(5,0);
    cout << "\n\n\tPress '1' to book tickets.....";
    setcolorandbackground(12,0);
    cout << "\n\n\tOr else Press '0' to go back to main menu....\n\t";
    setcolorandbackground(15,0);
    return;
}

void print_ticket(int a){//genearates a file and prints the input in that file
    ofstream myfile("IPL 2021 Ticket.txt");
    myfile<<"\n******************************************** IPL TICKET, 2021 ********************************************\n";
    myfile<<"\n\tNAME: ";
    myfile<< name << endl;
    myfile<<"\n\tMatch No.: " << a << endl;
    myfile<<"\n\tMatch:\n\n\t";
    myfile<< matches[a] << endl;
    myfile<<"\n\tTime: 8.00PM\n";
    myfile<<"\n**********************************************************************************************************";
    myfile.close();
    setcolorandbackground(2,0);
    cout << "\n\tIPL Ticket generated Successfully:)";
    return;
}

void head(){
    cout << "\n\tPlease, Enter your Name: " ;
    setcolorandbackground(15,0);
    getline(cin,name);
    setcolorandbackground(10,0);
    cout << "\n\n\tHello there, " << name << "! Welcome to IPL ticket booking"<< endl;
}

void start(){
    bool print_name = true;
    while(1){
        title();
        while(print_name){
            head();
            print_name=false;
        }
        print_mainmenu();
        int choice;
        cin >> choice;
        if(choice==1){//print all teams if choice is 1
            print_teams();
            char ch;
            cin >> ch;
            while(ch!='0'){
                setcolorandbackground(10,0);
                cout << "\tPlease press '0' to go back to main menu....";
                setcolorandbackground(15,0);
                cin >> ch;
            }
            continue;
        }else if(choice==2){//print all venues if choice is 2
            print_venue();
            char ch;
            cin >> ch;
            while(ch!='0'){
                setcolorandbackground(10,0);
                cout << "\tPlease press '0' to go back to main menu....";
                setcolorandbackground(15,0);
                cin >> ch;
            }
            continue;
        }else if(choice==3){//print all match fixtures if choice is 3
            print_matches();
            char ch;
            cin >> ch;
            while(ch!='0' and ch!='1'){
                setcolorandbackground(10,0);
                cout << "\tPlease press '0' to go back to main menu....";
                setcolorandbackground(15,0);
                cin >> ch;
            }
            if(ch=='0'){
                continue;
            }else{//ch=1
                int choice;//stores the match number
                cout << "\n\n\tEnter the match you want to book tickets for: ";
                cin >> choice;
                print_ticket(choice);
                setcolorandbackground(15,0);
                cout << "\n\n\tPress '0' to go to main menu.....\t";
            }
            char c;
            cin >> c;
            while(c!='0'){
                setcolorandbackground(10,0);
                cout << "\tPlease press '0' to go back to main menu....";
                setcolorandbackground(15,0);
                cin >> c;
            }
            continue;
        }else if(choice==0){//exit the program
            break;
        }else{
            cout << "\n\tPlease select a valid option!" << endl;
        }
    }
}

int main(){
    start();
    return 0;
}
