# Data-Structure

## Introduction
  ### 1. what is Data Structure?
  
    Data structure is organizing in a perticular mannar and storing data in a computer. it is accesible and modifieable 
    efficiently. Data Structure is a collection of data values (like 10,A).

  ### 2. Why need of Data Structure?
  
      Data Structure are used for make it easy to locate and retrieve information. Primitive data structure are simple way of
      for programming language to represent basic values.It can make many things much faster.
      It create once only and it can be used again and again easily
  
  ### 3. which concept do you clare before starting the Data Structure?
  
     You have to know basic syntax of how to define a class, data types, name mangling,work flow. We have to need basic
     idea of programming language in which language do you perforn with it. 
  
  ### 4. Types of data structure
  
      * Leanear Data structure

            Stack,Queue,Linked List.
         
      * Non-Leanear Data structure
      
            Tree  
  
  ### 5. Example of data strucuture 
  
  Linked List
  
  Singly Linear LinkedList
        
        
 ``` C++
        
        #include <iostream>
        
        using namespace std;

        #include <stdlib.h>

        typedef struct node
        {
            int data;
            struct node * next;
        }NODE,*PNODE;

        class SinglyLinear
        {
            private :
                PNODE head,newn,temp;
                int size = 0;

            public :
                void InsertLast(int);
                void FillNode(int);
                void InsertFirst(int);
                void InsertAt(int,int);
                //void DeleteLast(int);
                //void DeleteFirst(int);
                //void DeleteAt(int);

                void Display();
                int Count();
                int Accept();
                void SwitchMenu();


            SinglyLinear()
            {
                head = NULL;
                newn = NULL;
            }
        };

        void SinglyLinear::FillNode(int iNo)
        {
            //cout << "\nAllocating memory for new node\n";
            newn = new NODE;

            if (newn == NULL)
            {
                cout << "\n cant alloacte the memory for new node\n";
                return;
            }
            else
            {
                //cout << " Memory allocated";
                newn->data = iNo;
                newn->next = NULL;
                //cout << " New node filled with data";
            }
        }

        void SinglyLinear::InsertLast(int iNo)
        {
            //cout << "\n Checking if LinkedList is empty\n";
            if(head == NULL)
            {
                FillNode(iNo);
                head = newn;
            }
            else
            {
                //cout << "\n Inside inserting next node \n";
                FillNode(iNo);
                temp = head;
                while(temp->next != NULL)
                {
                    temp = temp -> next;
                }
                temp -> next = newn;
            }
            if(head == NULL)
            {
                cout << "\n Failed \n";
            }
           // cout << "\n Success call of InsertLast \n";
        }

        void SinglyLinear::Display()
        {
            int icnt = 0;
            temp = head;
            if(head == NULL)
            {
                 cout << "\n Empty LinkedList \n";
            }
            while(temp!=NULL)
            {
                icnt++;
                cout << icnt <<"->"<<temp->data<<" ";
                temp = temp->next;
            }
            cout << endl;
        }

        int SinglyLinear::Count()
        {
            int icnt = 0;
            temp = head;
            if(head == NULL)
            {
                cout << "\n Empty LinkedList \n";
            }
            while(temp!=NULL)
            {
                icnt++;
                //cout << icnt <<"->"<<temp->data<<" ";
                temp = temp->next;
            }
            cout << "\n Total nodes : "<<icnt;
            return icnt;
            cout << endl;
        }

        void SinglyLinear::InsertFirst(int iNo)
        {
            //temp = head;
            //cout << "\n Checking if LinkedList is empty\n";

            if(head == NULL)
            {
                FillNode(iNo);
                head = newn;
            }
            else
            {
                FillNode(iNo);
                newn->next = head;
                head = newn;
            }
                //cout << "\n Success call of InsertFirst \n";
            return;
        }

        void SinglyLinear:: InsertAt(int iNo, int iPos) //we can assess class members (like characteristic and behaviour) using  scope resolution operator
        {
            if( (iPos > size+1) && (iPos < 0) )
            {
                cout << "\n ERROR: Invalid position please enter between 1 and %d \n"<<size;
                return;
            }

            if(head == NULL)
            {
                FillNode(iNo);
                head = newn;
            }

            else if(iPos==1)
            {
                iNo = Accept();
                InsertFirst(iNo);
            }

            else if(iPos == size+1)
            {
                iNo = Accept();
                InsertLast(iNo);
            }

            else
            {
                //cout << "\n Inside inserting node \n";
                FillNode(iNo);
                temp = head;
                while(iPos != 2)
                {
                    temp = temp -> next;
                    iPos--;
                }
                temp -> next = newn;
            }
            if(head == NULL)
            {
                cout << "\n Failed \n";
            }
        }

        int display()

        int SinglyLinear::Accept()
        {
            int iNo = 0;
            cout << " Enter Number : ";
            cin>>iNo;

            return iNo;
        }

        void SinglyLinear::SwitchMenu()
        {

            int choice = 0;
            int iNo = 0;
            int place = 0;
            SinglyLinear sl;

            cout << "\n *** Singly Linear Linked List *** \n";
            cout << "\n 1 :  Insert at First";
            cout << "\n 2 :  Insert at Last";
            cout << "\n 3 :  Insert at position";
            cout << "\n 4 :  Delete First Node";
            cout << "\n 5 :  Delete Last Node";
            cout << "\n 6 :  Delete at position";
            cout << "\n 7 :  Display Linked List";
            cout << "\n 8 :  Count total Node";
            cout << "\n 9 :  Exit\n";


            while (1)
            {
                cout << "\n Enter number of function call : ";
                cin>>choice;

                switch (choice)
                {
                    default:  cout << "\n Plz enter choice between above menu \n";
                        break;

                    case 1:
                        iNo = Accept();
                        sl.InsertFirst(iNo);
                        size++;
                        break;

                    case 2:
                        iNo = Accept();
                        sl.InsertLast(iNo);
                        size++;
                        break;

                    case 3:
                        iNo = Accept();
                        cout << " Total nodes  : "<<size;
                        cout << " Enter position : ";
                        cin>>place;
                        sl.InsertAt(iNo,place);
                        size++;
                        break;

                    case 4:
                        cout << "\n WAIT: code is under development \n";
                        break;

                    case 5:
                        cout << "\n WAIT: code is under development \n";
                        break;

                    case 6:
                        cout << "\n WAIT: code is under development \n";
                        break;

                    case 7:
                        sl.Display();
                        break;

                    case 8:
                        sl.Count();
                        break;

                    case 9:
                        exit(0);
                }
            }

        }

        int main()
        {
            SinglyLinear sl;

            sl.SwitchMenu();
            /*
            sl.InsertLast(10);
            sl.InsertLast(11);
            sl.InsertLast(21);

            sl.InsertFirst(9);
            sl.InsertFirst(8);
            sl.InsertFirst(7);

            sl.Display();
             */

            return 0;
        }
        ```
    
 
  
  
