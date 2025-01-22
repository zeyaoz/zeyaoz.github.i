---
layout: project
type: project
image: img/CLogo.png
title: "Bank Database application in C"
date: 2024
published: true
labels:
  - Vim
  - Unix
  - C
summary: "A bank database application that I developed for ICS 212 in the C programming language."
---

<img width="200px" class="img-fluid" src="../img/bank.png">

This project was about creating a C application that can take, store, and modify user accounts of a bank through storing the information in a .txt file. Through a large menu interface, the user could specify if they wanted to add a new record to the database, print all records from the database, find a record with a specific account number, delete a specific record from the database, or quit the application. On startup, the database information would be automatically loaded in from a specific .txt file and on quit, the databse information would be automatically written to a specific .txt file.

My role in this project was its creation in its entirety. I implemented this application through the UH Unix interface in the Vim text editor program where I was responsible for 100% of the work.

In this project, I gained experience with the major operations of the C programming language as well as implementing a complete bank databse application that covers many aspects of C programming which includes but is not limited to dynamically allocating memory on the heap that mimics a linked list data structure.

Here is some example code of the findRecord function that I used in my application:

```

/*****************************************************************
//
//  Function name: findRecord
//
//  DESCRIPTION:   Finds a user's record with the specified
//                 account number.
//
//  Parameters:    start (struct record *) : A pointer of struct
//                                           record. Represents
//                                           the start of the list
//                                           of records.
//                 accountno (int) : This integer represents the
//                                   account number of the record
//                                   being searched for.
//
//  Return values: 0 : Record was found successfully.
//                -1 : Record could not be found.
//
****************************************************************/

int findRecord(struct record *start, int accountno)
{

    /*Initialize a pointer to a record set to the start of the
    heap list.*/

    struct record *current = start;

    /*Initialize integer variables "isFound" to determine if a
    record has been found in the heap list and "result" to return
    the integer output of the function, currently set to -1
    (unsuccessful)*/

    int isFound = 0;
    int result = -1;

    /*[DEBUG] mode information verification output.*/

    if (debugmode)
    {
        printf("\n[DEBUG]: Function called: findRecord\n");
        printf("[PARAMETER]: accountno, Value: %d\n\n", accountno);
    }

    /*While the end of the heap list has not been reached:*/

    while (current != NULL)
    {

        /*if the accountno of the current record matches the
        accountno being searched for,*/

        if (current -> accountno == accountno)
        {

            /*Print the record information to the user, and set
            the integer variables accordingly to let the function
            know that the record as been found successfully.*/

            printf("\nAccount Number: %d\n", current -> accountno);
            printf("Name: %s\n", current -> name);
            printf("Address: %s\n\n", current -> address);
            isFound = 1;
            result = 0;
        }

        /*Set the current record to the next record in the
        heap list.*/

        current = current -> next;
    }

    /*If the record was not found, notify the user.*/

    if (!isFound)
    {
        printf("\nRecord not found with account number %d\n", accountno);
    }
    return result;
}

```

Notice how I love to provide long and descriptive comments on how my code works. I have always taken pride in explaining code thorughly to other people through commenting, and I plan to continue coding in this system for all future personal projects.

