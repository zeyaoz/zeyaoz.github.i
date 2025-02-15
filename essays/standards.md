---
layout: essay
type: essay
title: "Making sure I understand"
# All dates must be YYYY-MM-DD format!
date: 2025-01-22
published: true
labels:
  - Computer Science
  - Software Engineering
  - Learning
---

<img width="100px" class="rounded float-start pe-4" src="../img/lightbulb.jpg">

```
//Understanding used to be easy.
```

Programming class back in high school was so very simple compared to now. Starting in html, basic programming principles went by with a breeze. Website project? Done with no difficulty. If only I had known what more I had to learn to be employable...

The early programming courses at the university were an extension of my high school class. Basic data structures were learned, variables, data types, functions, etc. However, as I was opened up to more complex topics such as discrete math and program structure, I found myself taking more time than ever to finish assignments. I asked myself this question: how could I ever remember all of these topics? 

The option to create comments in my code had always been a feature I utilized when programming. The contrast in text color between the rigid, discrete elements of programming and the articulate, understandable sentences of my comments always made my code easier to understand, and gave me hope in firmly comprehending these subjects. 

As the assignments got more complicated, the time I spent understanding topics increased. How could I prove to not only myself but to everyone else that I truly understood these topics? 

```
void printAllRecords(struct record *start)
{

    /*Initialize a pointer to a record set to the start of the
    heap list.*/

    struct record *current = start;

    /*[DEBUG] mode information verification output.*/

    if (debugmode)
    {
        printf("\n[DEBUG]: Function called: printAllRecords\n\n");
    }

    /*If there are no records in the heap list,*/

    if (current == NULL)
    {
        printf("\nNo records found in database.\n");
    }

    /*Otherwise, the heap list must contain 1 or more records.*/

    else
    {

        /*While the end of the heap list has not been reached,*/

        while (current != NULL)
        {

            /*Print the records to the user in a specificly
            formatted way:
            <accountno>
            <name>
            <address>
            ...
            <address>
            <blank line>
            <accountno>
            ...
            and so on.*/

            printf("\nAccount Number: %d\n", current -> accountno);
            printf("Name: %s\n", current -> name);
            printf("Address: %s\n\n", current -> address);

            /*Set the current record to the next record in the
            heap list.*/

            current = current -> next;
        }
    }
}
```

Again and again I found myself explaining how each component of my code worked. This way, I will know exactly what everything does at a glance.

Was it necessary?

To learn a topic is extremely easy. Just take a glance and you have seen it. I could probably even get through the entirety of university with this method.

But will this make me a educated, experienced, and employable? 

I want to have fun. I want all of my assignments to go through smoothly. But, I also take pride in creating something that not only me but anyone else can see and then understand. 

Taking the time to comment my thoughts into the code will make sure that I preserve the understanding in that program so it may one day benefit someone else in their work.

I love software engineering. I sincerely want to take in all of the topics that are out there in the starry sky, understand them, and then move on to more. Taking the time to properly curate comments in my code is an experience I cherish every time I put my hands on the keyboard. 

Developing skills is simply a product of understanding a topic deeply. I will strive to understand all that I can so that my skills may be developed and put forward in my future career. 

I may not remember a topic after a while, I may forget, but I will make sure that I can understand it again.

I understand it now.

```
//Understanding it again might not be easy, but I will make it easy.
```
