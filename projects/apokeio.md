---
layout: project
type: project
image: img/PokeIcon.png
title: "Pokemon I/O function showcase in C"
date: 2024
published: true
labels:
  - Vim
  - Unix
  - C
summary: "A showcase of example Input/Output functions in C to read and write data from a .txt file."
---

<div class="text-center p-4">
  <img width="200px" src="../img/bulbasaur.png" class="img-thumbnail" >
  <img width="200px" src="../img/charmander.png" class="img-thumbnail" >
  <img width="200px" src="../img/squirtle.png" class="img-thumbnail" >
</div>

This project was about building an C application that can both read and write a particular user-defined Pokemon's information (name and level) to and from a .txt file. Through a menu interface, the user could specify which file that they want to write the Pokemon information that they created to, which file that they want to read the Pokemon information stored on the file from, and also an option to exit from the application.  

My role in this project was its creation in its entirety. I implemented this application through the UH Unix interface in the Vim text editor program where I was responsible for 100% of the work. 

In this project I gained experience with the C programming language as well as implementing a functional I/O application for importing and exporting information to and from a user-defined file. 

Here is some example code of my readfile function:

```

/*****************************************************************
//
//  Function name: readfile
//
//  DESCRIPTION:   This function will read the data from a text
//                 file and store it in the array called by
//                 "pokearray"
//
//  Parameters:    pokearray (struct pokemon[]) : The array of
//                                                pokemon data
//                                                where the data
//                                                from the
//                                                specified file
//                                                will be read
//                                                into.
//                 num (int*) : A pointer to an integer
//                              representing the maximum number
//                              of pokemon the array can hold.
//                              It will then be updated with
//                              the number of pokemon read into
//                              the array.
//                 filename (char[]) : A character array that
//                                     contains the name of the
//                                     file to read from.
//
//  Return values:  0 : The file was successfully opened by the
//                      function.
//                 -1 : The file has failed to be opened by the
//                      function.
//
****************************************************************/

int readfile(struct pokemon pokearray[], int* num, char filename[])
{

    /*Declare a file pointer named file what will be used to
    access the file being read from.*/
    /*Declare an integer "j" which acts as a counter.*/
    /*Declare a integer maxNum with the value pointed to by
    parameter "num", which stores the maximum number of pokemon
    that can be read into the array.*/

    FILE *file;
    int j = 0;
    int maxNum = *num;

 
    /*Open the file specified by filename in the "r" mode
    (read from file only). Function fopen will will return a
    pointer to the file if successfully executed, or NULL if
    unsuccessful.*/

    file = fopen(filename, "r");

    /*If the fopen function has failed to open the file, return
    "-1" to signify failure.*/

    if (file == NULL)
    {
         return -1;
    }

    /*While counter integer "j" has not reached maxNum (the
    maximum number of pokemon allowed in the array) and the file
    still contains more valid pokemon entries, function fscanf
    will read formatted data from the file; A number that
    represents the pokemon's level and its string name
    (character array). Function fscanf will return "2" if it
    successfully reads both elements. If unsuccessful, the loop
    will terminate.*/

    while (j < maxNum && fscanf(file, "%d\n%[^\n]\n", &pokearray[j].level, pokearray[j].name) == 2)
    {
        j++;
    }

    /*Update the value of *num to j, which represents the total
    number of pokemon that were read from the file.*/

    *num = j;

    /*Properly close the file and ensure the data stored in a
    buffer is written to the file, also ensuring that the
    resources associated with the file are preperly freed.*/

    fclose(file);

    return 0;
}

```

Notice how I love to provide long and descriptive comments on how my code works. I have always taken pride in explaining code thorughly to other people through commenting, and I plan to continue coding in this system for all future personal projects. 
