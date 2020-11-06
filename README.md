# Lab11 Guide
## Getting Started

Please watch the [Lab11 Walkthough Video](https://www.youtube.com/playlist?list=PLvnIObHoMl8eSDyLlPG-tHfFyBn8qSIY_).

### Code Style Requirements
Please review the [CS253 Style Guide](https://docs.google.com/document/d/1zKIpNfkiPpDHEvbx8XSkZbUEUlpt8rnZjkhCSvM-_3A/edit?usp=sharing) and apply it in all lab warmups, lab activities and projects this semester. Coding Style will assessed as part of your lab and project grades.

### Code Quality Requirements
- Code must compile without warnings using the provided Makefile
- Programs must handle unexpected user input and either reprompt (loops) or gracefully exit with a non-zero exit status.
- Programs must handle error conditions gracefully, without crashing, ideally by checking function returns codes (if available) and returning a non-zero exit status.
- Programs should be free of memory related errors, buffer overflows, stack smashing, leaks, etc... Whether the program crashes or not. This will be validated using valgrind.

## Lab Warmup - File System Scanner (part 1)
### Problem Description
Part 1 of the File System Scanner will take the lecture example of the File System Scanner, extend it to use getopt to process command line arguments, and stub out options to allow the user to specify sort and filter options from the commandline. A copy of the File System Scanner example has been provided int he LabWarmup directory.

<br />
1. Modify the File System Scanner to use getopt() functionality
<br /><br />
Maintain existing functionality, however instead of directly reading an optional directory directly from argv[], add a "-d" option with an argument to getopt(). Below is the expected -d usage:

Ex: Listing contents of student home directory using -d
```
./myprog -d /home/student

```
  
<br />
2. Add a "-s" option to enable/disable alphabetical sorting
<br /><br />

Ex: List the contents of student home directory, sorted alphabetically
```
./myprog -s -d /home/student
```

Ex: List the contents of student home directory, unsorted
```
./myprog -d /home/student
```

Ex: List the contents of the current directory, sorted alphabetically
```
./myprog -s
```

<br />
3. Release allocated memory. The scandir allocates memory internally that must be freed by the caller to prevent memory leaks. Also make certain to close any files that were opened. Be certain to test all possible commandline enabled/disabled options.
<br /><br />

Ex: Run program in valgrind to verify no memory errors exist
```
valgrind --tool=memcheck --leak-check=yes --show-reachable=yes ./myprog -s -d /usr/bin 
==89619== Memcheck, a memory error detector
==89619== Copyright (C) 2002-2017, and GNU GPL'd, by Julian Seward et al.
==89619== Using Valgrind-3.15.0 and LibVEX; rerun with -h for copyright info
==89619== Command: ./myprog -s -d /usr/bin 

<<<<<<<< PROGRAM OUTPUT REMOVED >>>>>>>>

==89614== 
==89614== HEAP SUMMARY:
==89614==     in use at exit: 0 bytes in 0 blocks
==89614==   total heap usage: 919 allocs, 919 frees, 126,372 bytes allocated
==89614== 
==89614== All heap blocks were freed -- no leaks are possible
==89614== 
==89614== For lists of detected and suppressed errors, rerun with: -s
==89614== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 0 from 0)
```


### Implementation Guide
1. Expand the folder named LabWarmup and open main.c
2. Enter the program code to create an application as described in the Problem Description.
3. Test the program to ensure it functions as expected.
4. Run the program with valgrind to catch any memory leaks or errors
5. Commit the changes to your local repository with a message stating that LabWarmup is completed.
6. Push the changes from your local repository to the github classroom repository.
7. Update the Coding Journal with an entry describing your experience using the steps outlined below.


## Lab Activity - File System Scanner (part 2)
### Problem Description
This is a continuation of the File System Scanner from the LabWarmup.  Begin by copying main.c from the LabWarmup into LabActivity.  



<br />
1. Add a "-x" option and a custom filter function to enable/disable displaying hidden files.
<br /><br />
Modify the default filter function to prevent displaying hidden files.  Hidden files are any files or directories whose name begins with a '.'.   Add filter function called showHidden() to display hidden files when the user passes the "-x" option.

Ex: List the contents of student home directory, without hidden files displayed
```
./myprog -d /home/student
```

Ex: List the contents of the current directory, with hidden files displayed
```
./myprog -d /home/student -x
```

<br />
2. Add a "-f" option and a custom filter function to enable/disable displaying directories
<br /><br />
Add filter function called showFilesOnly() to only display regular files when the user passes the "-f" options

Ex: List the contents of student home directory, showing regular files and directories (and all other dirent types) except those that are hidden. 
```
./myprog -d /home/student
```

Ex: List the contents of the current directory, showing only regular files except those that are hidden.
```
./myprog -d /home/student -f
```

NOTE: The expected behavior is that the user will only specify a single filter option([x|f]) at a time from the command-line. If both the -x and -f filter options are specified at the same time, the behavior is undefined.

<br />
3. Add a "-r" and a custom comparison function to sort the list alphabetically, but in the reverse order from the "-s" option.
<br /><br />

Ex: List the contents of student home directory, sorted alphabetically in ascending order
```
./myprog -d /home/student -s 
```

Ex: List the contents of student home directory, sorted alphabetically in descending order
```
./myprog -d /home/student -r
```
<br />
4. Add a "-h" option and a custom usage function that displays all command-line options with short descriptions of each and exits with an exit status of 0.
<br /><br />

Ex: Display a simple help dialog and exist with an exit status of zero
```
./myprog -h
```


### Implementation Guide
1. Expand the folder named LabActivity and copy main.c from LabWarmup
2. Enter the program code to create an application as described in the Problem Description.
3. Test the program to ensure it functions as expected.
4. Run the program with valgrind to catch any memory leaks or errors
5. Commit the changes to your local repository with a message stating that LabActivity is completed.
6. Push the changes from your local repository to the github classroom repository.
7. Update the Coding Journal with an entry describing your experience using the steps outlined below.

## Coding Journal
Keep a journal of your activities as you work on this lab. Many of the best engineers that I have worked with professionally have kept some sort of engineering journal. I personally packed notebooks around with me for nearly 8 years before I began keeping my notes electronically.   

Your journal can track ideas, bugs, cool links, code snippets, shell commands, rants, or simply a reflection on what worked well or not-so-well with this lab activity. I will not be grading the content of your journal, but I will expect at least two date-stamped journal entries of at least a paragraph each added to the provided Journal.md file.

### Implementation Details
1. Add an entry to the provided Journal.md located in the CodingJournal folder, formatted using markdown notation. You can find a reference at the bottom of this guide.

2. Commit the changes to your local repository with a message stating an entry has been added to the journal.
3. Push the changes from your local repository to the github classroom repository.
4. Repeat for reach additional journal entry
## Markdown Resources
Markdown is a notation that is used to format text documents.  It is widely used in Software Development shops around the world, which is why we're asking you to use it in your lab documentation.  

Github provides a guide for getting started:  [Mastering Markdown](https://guides.github.com/features/mastering-markdown/)
