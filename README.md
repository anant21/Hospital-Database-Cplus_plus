# Hospital-Database-Cplus_plus

//                              *^*^*^*^*
//                               PROJECT
//                              *^*^*^*^*

#include<iostream.h>
#include<conio.h>
#include<stdlib.h>
#include<stdio.h>
#include<fstream.h>
#include<string.h>
#include<dos.h>

class eye
{ char id[30];
  char name[20];
  char dname[20];
  char gender[10];
  char eyecon[30];
  int age;
  double phone;

  public:
  eye()
  { strcpy(id,NULL);
    strcpy(name,NULL);
    strcpy(dname,NULL);
    strcpy(gender,NULL);
    strcpy(eyecon,NULL);
    age=0;
    phone=0;
  }

  void getdata()
  { cout<<"\nEnter Patient's Details\n";
    cout<<"-------------------------\n";

    cout<<"\nPatient ID : ";
    cin>>id;
    cout<<"\nPatient Name : ";
    gets(name);
    cout<<"\nAge : ";
    cin>>age;
    cout<<"\nGender : ";
    gets(gender);
    cout<<"\nEye Condition : ";
    gets(eyecon);
    cout<<"\nSuitable Doctor : ";
    gets(dname);
    cout<<"\nMobile : ";
    cin>>phone;
  }

  void showdata()
  {
    cout<<"\nPatient ID : "<<id;
    cout<<"\nPatient Name : "<<name;
    cout<<"\nAge : "<<age;
    cout<<"\nGender : "<<gender;
    cout<<"\nEye Condition : "<<eyecon;
    cout<<"\nDoctor chosen : "<<dname;
    cout<<"\nMobile : "<<phone;
    cout<<"\n\n";
  }

  char *i()
  {return id;}

}e;

void followup();
void search();
void del();
void modify();
void EoM();
void num_of_records();
void treatments();
void eyecondition();
void doctor();
void cataract();
void lasik();
void retina();
void aboutus();

ofstream fout;
ifstream fin;

void add_record()
{ clrscr();
  fout.open("records.txt",ios::binary | ios::app);
  e.getdata();
  fout.write((char *)&e, sizeof(e));
  fout.close();
}

void show_record()
{
  fin.open("records.txt",ios::binary | ios::in);
  while(fin.read((char *)&e, sizeof(e)))
   { e.showdata();}
  fin.close();
  getch();
}

char id1[20];
void search()
{ cout<<"\nSEARCH RECORD";
  cout<<"------------";
  cout<<"\nEnter the Patient's ID : ";
  gets(id1);
  int i=0;
  while(i<2)
 { clrscr();
   cout<<"\n\n\n\t\t\tFetching Data"; delay(900);
   cout<<"."; delay(700); cout<<"."; delay(700); cout<<".";
   delay(700); cout<<".";
   i++;
 }
  clrscr();
  fin.open("records.txt", ios::binary | ios::in);
  while(fin.read((char *)&e, sizeof(e)))
  { if(strcmp(id1,e.i())==0)
     { e.showdata(); }
  }
 fin.close();
 getch();

}

void del()
{ clrscr(); char id2[10];
  cout<<"Enter the Patient ID : ";
  gets(id2);
  fin.open("records.txt", ios::binary | ios::in);
  fout.open("records1.txt", ios::binary | ios::out);

  while(fin.read((char *)&e, sizeof(e)))
  { if(strcmp(e.i(),id2)!=0)
     { fout.write((char *)&e, sizeof(e));
     }
  }
  fout.close();
  fin.close();

  remove("records.txt");
  rename("records1.txt","records.txt");
 /* fin.open("records1.txt", ios::binary | ios::in);
  fout.open("records.txt", ios::binary | ios::out);

  while(fin.read((char *)&e, sizeof(e)))
   {
     fout.write((char *)&e, sizeof(e));
   }


   fout.close();
   fin.close();

  remove("records1.txt");    */

}

void modify()
{ clrscr();
  fstream f;
  f.open("records.txt", ios::binary | ios::in | ios::out);
  cout<<"\nEnter the Patient ID : ";
  gets(id1);
  while(f.read((char*)&e, sizeof(e)))
  { if(strcmp(id1,e.i())==0)
     { clrscr();
       f.seekg(0,ios::cur);
       cout<<"\nEnter New Record..\n";
       e.getdata();
       f.seekp(f.tellg() - sizeof(e));
       f.write((char *)&e, sizeof(e));
     }
  }
  f.close();
}

void EoM()
{ clrscr();
  int p;
  cout<<"Edit or Modify Records\n";
  cout<<"----------------------\n\n";
  cout<<"1. Modify\n";
  cout<<"2. Delete\n";
  cout<<"3. No. of Patient Records\n";
  cout<<"4. Exit\n\n";
  cin>>p;
  switch(p)
  { case 1: modify(); break;
    case 2: del(); break;
    case 3: num_of_records(); break;
    default:exit(0);
  }
}


void num_of_records()
{ int z,z1,nr;
  fstream f;

  f.open("records.txt", ios::binary | ios::in | ios::out);
  f.seekg(0, ios::end);  //to move the pointer to the end.
  z=f.tellg();
  z1=sizeof(e);
  nr=z/z1;
  cout<<"\nTotal No. of Records : "<<nr;
  cout<<"\n";
}

void follow_up()
{ eyecondition();
  doctor();
  getch();
  add_record();
}


void doctor()
{ clrscr();
  int d1;
  cout<<"\nSelect the Specialty\n";
  cout<<"\n--------------------\n";
  cout<<"\n1. Cataract";
  cout<<"\n2. LASIK & Refractive Surgery ";
  cout<<"\n3. Retina & Uvea services ";
  cout<<"\n\n";
  cin>>d1;


  switch(d1)
  { case 1: cataract(); break;
    case 2: lasik(); break;
    case 3: retina(); break;
    default:exit(9);
  }
  getch();
}

void cataract()
{ clrscr();
  cout<<"Cataract\n";
  cout<<"--------\n\n";
  cout<<"1. Dr. Hemlata Gupta \n\n";
  cout<<"2. Dr. Swati Singh \n\n";
  cout<<"3. Dr. Mahipal S. Sachdev \n\n";
  cout<<"\n\n";
}

void lasik()
{ clrscr();
  cout<<"LASIK & Refractive Surgery \n";
  cout<<"--------------------------\n\n";
  cout<<"1. Dr. V.K. Dadu \n\n";
  cout<<"2. Dr. Poonam Jain \n\n";
  cout<<"3. Dr. Shilpi Diwan \n\n";
  cout<<"4. Dr. Ritika Sachdeva \n\n";
  cout<<"\n\n";
}

void retina()
{ clrscr();
  cout<<"Retina & Uvea Services \n";
  cout<<"----------------------\n\n";
  cout<<"1. Dr. Avnindra Gupta \n\n";
  cout<<"2. Dr. Lalit Gupta \n\n";
  cout<<"3. Dr. Dinesh Talwar \n\n";
  cout<<"4. Dr. Prachi Dave \n\n";
  cout<<"\n\n";
}

void treatments()
{ clrscr();
  cout<<"TREATMENTS\n";
  cout<<"----------\n\n";
  cout<<"1. Laser Eye Surgery \n";
  cout<<"2. Laser Cataract Surgery \n";
  cout<<"3. Laser Refractive Lens Exchange \n";
  cout<<"4. Implantable Contact Lenses \n";
  cout<<"5. Keratoconus Treatments \n";
  cout<<"6. Dry Eye \n";
  cout<<"7. Vitreolysis Laser Treatment of Floaters \n";
  cout<<"8. Centrasight \n";
  cout<<"\n\n";
  getch();
}

void eyecondition()
{ clrscr();
  cout<<"Eye Conditions\n";
  cout<<"---------------------\n\n";
  cout<<"1. Cataract - Ct\n";
  cout<<"2. Fuchs Endothelial Dystrophy - FED\n";
  cout<<"3. Kevato-conus - Kc\n";
  cout<<"4. Dry Eye - DE\n";
  cout<<"5. Flashes and Floaters - FF\n";
  cout<<"6. Macular Degeneration - MD\n";
  cout<<"7. Stemcell Deficiency - SD\n";
  cout<<"8. Filaucoma - Fc\n";
  cout<<"9. Herpes Simplex - HS\n";
  cout<<"10.Retina - Rt\n";
  getch();
}

void aboutus()
{ clrscr();
  cout<<"About Us:\n";
  cout<<"--------\n\n";
  cout<<"Opening hours: \nMon - Fri -> 9 AM -6 PM\n"
      <<"Sun -> 9 AM - 1:30 PM \n\n";
  cout<<"Email: centreforsight.com\n\n";
  cout<<"Contact: 011-45738888\n\n";
  cout<<"Address: B-5/24, Safdarjung Enclave,\n\t Block B-7, Deer Park, Green Park(METRO),\n\t New Delhi-110029";
  getch();
}

void main()
{ clrscr();
  cout<<"\t\t\t*******************************\n";
  cout<<"\t\t\tWELCOME  TO  CENTRE  FOR  SIGHT\n";
  cout<<"\t\t\t*******************************\n\n";
  cout<<"\t\t\t* Every Eye Deserves the Best *\n\n\n";
  cout<<"\t\t    +Branch : Safdajung Enclave, New Delhi\n";
  cout<<"\t\t     ------\n\n";
  cout<<"\t\t    +FreePhone : 08081154696 \n";
  cout<<"\t\t     ---------\n\n";
  getch();

  int c;

while(c!=0)
{
  clrscr();
  cout<<"\n1. Follow Up \n";
  cout<<"2. Find a Doctor \n";
  cout<<"3. Eye Conditions \n";
  cout<<"4. Treatments Available \n";
  cout<<"5. Show Records \n";
  cout<<"6. Edit or Modify Record \n";
  cout<<"7. About Us \n";
  cout<<"8. Exit-> '0'\n\n";
  cin>>c;
  switch(c)
  { case 1: follow_up(); break;
    case 2: doctor(); break;
    case 3: eyecondition(); break;
    case 4: treatments(); break;
    case 5: {int r;
	     cout<<"RECORDS\n";
	     cout<<"-------";
	     cout<<"\n\n1. Particular Record ";
	     cout<<"\n\n2. All Records \n\n";
	     cin>>r;
	     clrscr();
	     switch(r)
	     { case 1: search(); break;
	       case 2: show_record();  break;
	       default:exit(11);
	     }
	     getch();
	    } break;
    case 6: EoM(); break;
    case 7: aboutus(); break;
    default:cout<<"Try Again !";
	    exit(11);
  }
}
  getch();
}
