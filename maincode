#include<fstream>
#include<iostream>
#include<stdio.h>
#include<string.h>
#include <stdlib.h>
using namespace std;
class hotel
{
    char fname[20];      //Stores First Name
    char lname[20];     //Stores Last Name
    int dd1;           //Stores Day
    int mm1;          //Stores Month
    int yyyy1;       //Stores Year
    int nights;     //Stores Number of nights
    int roomno;    //Stores the room numbers
    int price;
    int status;

    char facname[30];
    char facilities[30];
    char level;
    char cost;
    int facnum;
    char facmode[30];

public:
    void reserve();                //Allows user to enter data
    //void booking();               //Displays the bookings
    void calc_price();           //Calculates total price
    void disp_available();      //Dipslays all available rooms
    int checkroom(int);        //Checks if a room is occupied or not
    void searchbyname();
    void deleterecords();
    void changestatus();

    hotel();
    int level_combfast;
    int level_spamassage;
    int level_cosmetics;
    int level_spool;
    int level_rservice;
    void check_fac(char[],int&);
    void add();
    void show();
    int retlevel(char[]);
    void changelevel(char[]);

};


//Mayank Rastogi's code starts
void hotel::searchbyname()
{
    hotel ht;
    char gname[20];
    int flag=0;
    cout<<"Enter first name: "<<endl;
    cin>>gname;
    ifstream fin("hotel.dat", ios::binary);
    while(!fin.eof())
    {
        if(strcmp(fname,gname)==0)
        {
            cout<<"Room number: "<<roomno<<endl;
            cout<<"Name: "<<fname<<" "<<lname<<endl;
            cout<<"Check in date: "<<dd1<<"/"<<mm1<<"/"<<yyyy1<<endl;
            cout<<"Number of nights: "<<nights<<endl;
            flag=1;
            break;
        }
        else if(flag==0)
            cout<<"Record not found!\n";
    }
    fin.close();
}
void hotel::reserve()
{
    hotel ht;
    int flag=0,rno;
    ofstream fout("hotel.dat", ios::app|ios::binary);
    status=0;
    cout<<"TYPES OF ROOMS:\n";
    cout<<"Single (Room Number 1)\n";
    cout<<"Double (Room Number 2)\n";
    cout<<"King (Room Number 3)\n";
    cout<<"Twin (Room Number 4)\n";
    cout<<"Suite (Room Number 5)\n";

    cout<<"Please enter the room number of the type of room required\n";
    cin>>rno;
    if(rno<1||rno>5)
        cout<<"Invlaid Choice\n";
    else
    {

        flag=ht.checkroom(rno);

        if(flag==1)
        {
            cout<<"The room is already booked\n";
            cout<<"Please try again later\n";
        }

        else
        {
            cout<<"Please Enter the details of your Stay:\n";

            cout<<"Enter First Name:  ";
            cin>>fname;
            cout<<"Enter Last Name :  ";
            cin>>lname;

            cout<<"Please Enter Check in Date (DD MM YYYY Format)\n";
            cin>>dd1>>mm1>>yyyy1;

            cout<<"Please Enter number of nights\n";
            cin>>nights;
            roomno=rno;         //asigning private member, the value of rno
            fout.write((char*)&ht, sizeof(hotel));
            cout<<"Room successfully booked!\n";
            status=1;
        }

        fout.close();

    }
}
int hotel::checkroom(int rno)
{
    hotel ht;
    int checkr=0;
    ifstream fin("hotel.dat", ios::in);
    while(!fin.eof())
    {
        fin.read((char*)&ht,sizeof(hotel));
        if(roomno==rno)
        {
            checkr=1;
            break;
        }
        else
            status=0;

    }
    fin.close();
    return(checkr);
}

/*void hotel::booking()
{
    hotel ht;
    int rno,flag=0;
    ifstream fin("hotel.dat",ios::in);
    cout<<"Please enter the room number: ";
    cin>>rno;
    while(!fin.eof())
    {
        fin.read((char*)&ht,sizeof(hotel));
        flag=checkroom(rno);
        cout<<"sdihbf"<<status<<endl;
        if(status==1)
        {
            cout<<"\n GUEST DETAILS"<<endl;
            cout<<"----------------"<<endl;
            cout<<"CHECK IN DATE:   "<<dd1<<"/"<<mm1<<"/"<<yyyy1<<endl;
            cout<<"NUMBER OF NIGHTS:    "<<nights<<endl;
            cout<<"TYPE OF ROOM REQUESTED:  ";
            switch(roomno)
            {
                case 1: cout<<"Single\n";
                    break;
                case 2: cout<<"Double\n";
                    break;
                case 3: cout<<"King\n";
                    break;
                case 4: cout<<"Twin\n";
                    break;
                case 5: cout<<"Suite\n";
                    break;
            }
            cout<<endl;
            flag=1;
            break;
        }
    }
    if(status==0)
        cout<<"No rooms found.\n";
    fin.close();
}
*/
void hotel::disp_available()    //Dipslays all available rooms
{
    hotel ht;
    int flag=0;
    ifstream fin("hotel.dat", ios::in);
    fin.read((char*)&ht,sizeof(hotel));
    cout<<"\t\tAVAILABLE ROOMS\n";
    cout<<"**********************************";
    for(int i=1;i<6;++i)
    {
        flag=checkroom(i);
        if(status==0)
        {
            cout<<endl;
            switch(i)
            {
                case 1: cout<<"Room Type: Single"<<endl;
                    cout<<"Room Number: 1"<<endl;
                    break;
                case 2: cout<<"Room Type: Double"<<endl;
                    cout<<"Room Number: 2"<<endl;
                    break;
                case 3: cout<<"Room Type: King"<<endl;
                    cout<<"Room Number: 3"<<endl;
                    break;
                case 4: cout<<"Room Type: Twin"<<endl;
                    cout<<"Room Number: 4"<<endl;
                    break;
                case 5: cout<<"Room Type: Suite"<<endl;
                    cout<<"Room Number: 5"<<endl;
                    break;
            }
        }

    }

}
void hotel::changestatus()
{
    if (status==1)
        status=0;
}

void hotel::deleterecords()
{
    hotel ht;
    int room,found=0;
    char ans;
    cout<<"Enter room number: ";
    cin>>room;
    ifstream fin("hotel.dat", ios::in|ios::binary);
    ofstream fout("temp.dat", ios::out|ios::binary);
    while(fin.read((char*)&ht, sizeof(hotel)))
    {
        found=checkroom(room);
        if(found==0)
            fout.write((char*)&ht, sizeof(hotel));
        else if(found==1)
        {
            cout<<"Room number: "<<roomno<<endl;
            cout<<"Name: "<<fname<<" "<<lname<<endl;
            cout<<"Check in date: "<<dd1<<"/"<<mm1<<"/"<<yyyy1<<endl;
            cout<<"Do you wish to delete this record? (y/n)"<<endl;
            cin>>ans;
            if(ans=='y')
            {
                cout<<"RECORDS DELETED"<<endl;
                changestatus();
                if(ans=='n')
                {
                    fout.write((char*)&ht, sizeof(hotel));

                }
            }

        }
        fin.close();
        fout.close();
        remove("hotel.dat");
        rename("temp.dat","hotel.dat");

    }
}

    void hotel::calc_price()
    {
        hotel ht;
        int rno;
        int flag=0;
        cout<<"\t\tRATES FOR ROOMS:\n";
        cout<<"------------------------------------------\n";
        cout<<"Single --> 200 DHS\n";
        cout<<"Double --> 300 DHS\n";
        cout<<"King --> 400 DHS\n";
        cout<<"Twin --> 250 DHS\n";
        cout<<"Suite --> 500 DHS\n";

        cout<<"Enter room number to generate guest bill: \n";
        cin>>rno;
        flag=ht.checkroom(rno);

        if(flag==0)
        {
            cout<<"The room is not booked\n";
            cout<<"Please try again later\n";
        }

        else
        {
            switch(rno)
            {
                case 1: price=nights*200;
                    break;
                case 2: price=nights*300;
                    break;
                case 3: price=nights*400;
                    break;
                case 4: price=nights*250;
                    break;
                case 5: price=nights*500;
                    break;
            }

            cout<<endl<<"The bill for room number "<<rno<<" for "<<nights<<" nights is: "<<price<<" DHS"<<endl;
        }
    }

    //Mayank Rastogi's code ends


    //ABISHEK VENKATARAMAN's code starts
    hotel::hotel()
    {
        level=0;
        level_combfast=1;
        level_spamassage=1;
        level_cosmetics=1;
        level_spool=1;
        level_rservice=1;
    }
    int hotel::retlevel(char kx[20])
    {
        if(strcmp(kx,"combfast")==0)
        {
            return level_combfast;
        }
        if(strcmp(kx,"spamassage")==0)
        {
            return level_spamassage;
        }
        if(strcmp(kx,"cosmetics")==0)
        {
            return level_cosmetics;
        }
        if(strcmp(kx,"spool")==0)
        {
            return level_spool;
        }
        if(strcmp(kx,"rservice")==0)
        {
            return level_rservice;
        }
        else return 0;
    }


    void hotel::changelevel(char kx[30])
    {
        if(strcmp(kx,"combfast")==0)
        {
            level_combfast=0;
        }
        if(strcmp(kx,"spamassage")==0)
        {
            level_spamassage=0;
        }
        if(strcmp(kx,"cosmetics")==0)
        {
            level_cosmetics=0;
        }
        if(strcmp(kx,"spool")==0)
        {
            level_spool=0;
        }
        if(strcmp(kx,"rservice")==0)
        {
            level_rservice=0;
        }
    }

    void hotel::check_fac(char kx[],int&key)
    {
        if(retlevel(kx)==1)
        {
            cout<<"Facilities are available\n";
            key=1;

        }
        else
        {
            cout<<"Sorry the facilities are not available at the moment\n";
            key=0;
        }
    }


    void hotel::add()
    {
        int key=0;
        cout<<" Kindly enter required facility to be used ";
        cin>>facname;
        cout<<" Kindly enter  extra number of facilities to be used ";
        cin>>facnum;
        cout<<"Kindly enter mode of facility to be used\n";
        cin>>facmode;
        check_fac(facmode,key);
        changelevel(facmode);
        if(key==0)
        {
            cout<<"Sorry kindly try again\n";
        }

    }

    void hotel::show()
    {
        cout<<"Intoduction to the Facilities";
        cout<<"Name of facilities"<<facname<<endl;


        cout<<"Number of Facilities"<<facnum<<endl;

        cout<<"$MODES OF FACILITIES$"<<facmode<<endl;
    }

    void fac_availability()
    {
        hotel pt;
        char response;
        ofstream fout("hotel.dat",ios::app|ios::binary);
        do
        {
            cout<<"Kindly enter your desired facility\n";
            pt.add();
            fout.write((char*)&pt,sizeof(hotel));
            cout<<"\nNeed another facility? (y/n)\n";
            cin>>response;
        }
        while(response=='y');
        fout.close();
        }



    void removefac()
    {
        hotel o;
        char facmode[30];
        cout<<"Kindly enter mode of facility: ";
        cin>>facmode;
        ifstream fin("hotel.dat",ios::in|ios::binary);
        ofstream fout("temp.dat",ios::out|ios::binary);
        while(fin.read((char*)&o,sizeof(hotel)))
        {
            if(o.retlevel(facmode)==0)
                fout.write((char*)&o,sizeof(hotel));
        }
        fin.close();
        fout.close();
        remove("hotel.dat");
        rename("temp.dat","hotel.dat");
        cout<<"All facilities removed";
    }


    //ABISHEK VENKATARAMAN's code ends

    void hotelservices();
    void guestservices();


    int main()
    {

        int ans1=0;
        char ans2=0;
        cout<<"********** WELCOME TO THE HOTEL MANAGEMENT SYSTEM **********\n";
        do
        {
            cout<<"--------------------------------------------------------------\n";
            cout<<"                          MENU                                \n";
            cout<<"--------------------------------------------------------------\n";
            cout<<"PRESS 1 for using the Hotel Services\n";
            cout<<"PRESS 2 for using the Guest Services\n";
            cout<<"PRESS 3 for exiting\n";
            cin>>ans1;

            switch(ans1)
            {
                case 1: hotelservices();
                    cout<<"Do you require any further service? (y/n)\n";
                    cin>>ans2;
                    break;

                case 2: guestservices();
                    cout<<"Do you require any further service? (y/n)\n";
                    cin>>ans2;
                    break;
                case 3:cout<<"Thank you for visiting us. Hope to see you soon!\n";
                    exit(0);
                default: cout<<"Invalid Option. Please try again later\n";
            }
        }
        while(ans2=='y');
        cout<<"**************************************************************\n";
        cout<<"Thank you!\n";
        cout<<"See you again soon :)\n";
        cout<<"**************************************************************\n";



    }


    //Mayank's Subcode starts
    void hotelservices()
    {

        int opt;
        char ans=0;
        hotel ht;

        cout<<"********** WELCOME TO THE HOTEL MANAGEMENT SYSTEM **********\n";
        do
        {
            cout<<"--------------------------------------------------------------\n";
            cout<<"                          MENU                                \n";
            cout<<"--------------------------------------------------------------\n";
            cout<<"PRESS 1 for making a reservstion\n";
            cout<<"PRESS 2 for displaying available rooms\n";
            cout<<"PRESS 3 for deleting all bookings of a particular room\n";
            cout<<"PRESS 4 for searching the bookings by the name of guest\n";
            cout<<"PRESS 5 for generating the guest's bill\n";
            cout<<"PRESS 6 for exiting\n";

            cout<<"--------------------------------------------------------------\n";
            cout<<"Please enter your choice: ";
            cin>>opt;

            switch(opt)
            {
                case 1:ht.reserve();
                    cout<<"Do you require any further service? (y/n)\n";
                    cin>>ans;
                    break;

                case 2:ht.disp_available();
                    cout<<"Do you require any further service? (y/n)\n";
                    cin>>ans;
                    break;

                case 3:ht.deleterecords();
                    cout<<"Do you require any further service? (y/n)\n";
                    cin>>ans;
                    break;

                case 4: ht.searchbyname();
                    cout<<"Do you require any further service? (y/n)\n";
                    cin>>ans;
                    break;

                case 5:ht.calc_price();
                    cout<<"Do you require any further service? (y/n)\n";
                    cin>>ans;
                    break;

                case 6:ans='n';

                default: cout<<"Invalid Option. Please try again later\n";
            }
        }while(ans=='y');
        cout<<"**************************************************************\n";
        cout<<"Thank you!\n";
        cout<<"See you again soon :)\n";
        cout<<"**************************************************************\n";

    }

    //Mayank's Subcode ends

    //Abishek's Subcode starts


    void guestservices()
    {
        int opt;
        char response=0;
        cout<<"*********WELCOME TO HOTEL MANANGEMENT SYSTEM*********\n";
        cout<<"MODES OF FACILITIES:\n";
        cout<<"combfast"<<endl<<"spamassage"<<endl<<"cosmetics"<<endl<<"spool"<<endl<<"rservice"<<endl;

        do
        {
            cout<<"ENTER 1 FOR CHECKING AVAILABILITY OF FACILITIES\n";
            cout<<"ENTER 2 FOR REMOVING ANY FACILITY\n";
            cout<<"ENTER 3 FOR EXITING\n";
            cout<<"Kindly enter your option:";
            cin>>opt;

            switch(opt)
            {
                case 1:fac_availability();
                    cout<<"Do you wish to continue?(y/n)\n";
                    cin>>response;
                    break;


                case 2:removefac();
                    cout<<" succesfully and done\n";
                    cout<<"Do you wish to continue?(y/n)\n";
                    cin>>response;
                    break;

                case 3:response='n';

                default: cout<<"Invalid Option. Please try again later\n";
            }
        }while(response=='y');
        cout<<"Thanks for visiting!\n";
        cout<<"Hope you enjoyed your stay\n";

    }


    //Abishek's Subcode ends


    //Program ENDS!!


