---
layout: project
type: project
image: img/CppLogo.png
title: "Bank Database application in C++"
date: 2024
published: True
labels:
  - Vim
  - Unix
  - C++
summary: "A bank database application that I converted from the C programming language to the C++ programming language."
---

<img width="200px" class="img-fluid" src="../img/bank.png">

This project was about transforming a prior C application that can take, store, and modify user accounts of a bank through storing the information in a .txt file into a C++ application that was functionally the same. Through a large menu interface, the user could specify if they wanted to add a new record to the database, print all records from the database, find a record with a specific account number, delete a specific record from the database, or quit the application. On startup, the database information would be automatically loaded in from a specific .txt file and on quit, the databse information would be automatically written to a specific .txt file. 

My role in this project was its creation in its entirety. I implemented this application through the UH Unix interface in the Vim text editor program where I was responsible for 100% of the work.

In this project, I gained experience with the connection between the C and C++ programming language, transforming C code to its C++ equivalent as well as implementing a complete bank databse application that covers many aspects of C++ programming which includes but is not limited to dynamically allocating memory on the heap that mimics a linked list data structure.

Here is some example code of an overloaded operator "<<" that I used in my application:

```

/*****************************************************************
//
//  Function name: operator<<
//
//  DESCRIPTION:   This function overloads the "<<"
//                 operator in order to allow all records of this
//                 database to be printed directly without using
//                 the printAllRecords() class.
//
//  Parameters:    os (ostream &) : Contains the reference to the
//                                  output stream, where the
//                                  formatted output will be sent.
//                 list (const llist&) : The constant reference to
//                                       the other llist object,
//                                       ensuring the other object
//                                       is not modified during
//                                       the process.
//
//  Return values: ostream & : Contains the same output stream
//                             after appending the formatted data.
//
****************************************************************/

std::ostream& operator<<(std::ostream& os, const llist& list)
{

    /*[DEBUG] mode information verification outout.*/

    #ifdef DEBUG
        std::cout << "\n[DEBUG]: Overloaded (<<) operator of the llist class called.\n";
    #endif

    /*Initialize a pointer to the first node of the other linked
    list.*/

    record* current = list.start;

    /*If the current record is NULL, the datbase must be empty.*/

    if (current == NULL) {
        os << "\nNo records found in database.\n";
    }
    else
    {

        /*While the current record is not NULL,*/

        while (current != NULL)
        {

            /*Append the details of the formatted current record
            to the output stream, then move to the next node.*/

            os << "\nAccount Number: " << current -> accountno << "\nName: " << current -> name << "\nAddress:\n" << current -> address << "\n\n";
            current = current -> next;
        }
    }

    /*Return the reference to the formatted output stream
    containing all of the records.*/

    return os;
}

```

Notice how I love to provide long and descriptive comments on how my code works. I have always taken pride in explaining code thorughly to other people through commenting, and I plan to continue coding in this system for all future personal projects.
