Download Link: https://assignmentchef.com/product/solved-cs3423-systems-programming-assignment-7
<br>
: File I/O

For this assignment, you will use <strong>C</strong>’s I/O functions to create a simple course catalog database for administrators to update the details of each course offered by the CS department. The system will store basic information about each course, allowing the user to create, read, update, and delete them. All information for all courses will be stored as <strong>binary records in a <em>single file</em></strong>.

This assignment requires only the utilities used so far in the I/O lecture notes. <strong>Do not </strong>use bash, sed, awk, find, grep, Python, or any programming languages or utilities besides the C binary functions used in class. Only binary I/O functions should be used to store data to the filesystem (it is OK to use other functions when prompting the user).

<strong>Note: </strong>While this assignment is similar to Assignment 1, it is <em>not exactly the same</em>. You should thoroughly read all of these instructions.

<h1>Storing Course Information</h1>

All course information will be stored in a single binary structure as records of the following structure, where <strong><sub>courseName </sub></strong>is the name of the course (which may contain spaces), <strong><sub>courseSched </sub></strong>represents the course schedule (either strings <sub>MWF </sub>or <sub>TR</sub>), <strong><sub>courseHours </sub></strong>is the number of credit hours for the course, and <strong><sub>courseSize </sub></strong>is the number of students currently enrolled in the course.

<ul>

 <li>typedef struct</li>

 <li><sub>{</sub></li>

 <li>char courseName[64]; 4 char courseSched[4];</li>

 <li>unsigned int courseHours;</li>

 <li>unsigned int courseSize;</li>

 <li>} COURSE;</li>

</ul>

The program will store all courses using the above <sub>struct </sub>in a single file called <strong><sub>courses.dat</sub></strong>, located within the same directory as the program (this file is provided to you). All courses will be referenced using their course number as their index (e.g., course <strong><em>i </em></strong>will be located in the data file at relative byte off <strong><em>i </em></strong><sub>* sizeof(COURSE)</sub>. Course records will be stored in <strong><sub>courses.dat </sub></strong>in coursenumber order. Note that the course numbers will be specified by the user when a course is entered, and will not necessarily be sequential. If <strong><sub>courses.dat </sub></strong>does not exist, it should be created by the program <strong><em>in the current directory</em></strong>. You must use the files located at:

<strong>/usr/local/courses/ssilvestro/cs3423/Fall19/assign7</strong>; specifically, <strong>data/courses.dat </strong>shall be used as the starting point for your database (i.e., you must use this file for all operations, not a blank/empty/zero-byte data file, nor any other file).

<h1>Program Execution</h1>

When the program is executed, the following actions should occur. <strong>All program output should appear exactly as it appears below.</strong>

<ol>

 <li>Upon running your program, the user should be presented with the following menu:</li>

</ol>

<strong>Enter one of the following actions or press CTRL-D to exit.</strong>

<ul>

 <li><strong>– create a new course record</strong></li>

</ul>

<strong>R – read an existing course record</strong>

<strong>U – update an existing course record</strong>

<ul>

 <li><strong>– delete an existing course record</strong></li>

</ul>

<ol start="2">

 <li>The user then enters a one-character action (either upper or lowercase), leading to one of the following.</li>

</ol>

<ul>

 <li><strong><sub>C</sub></strong>: a course is created</li>

</ul>

(a) From the terminal, read the following one line at a time:

<ol>

 <li>Course number (<strong>zero-indexed </strong>integer)</li>

 <li>Course name (string possibly containing whitespace)</li>

</ol>

<ul>

 <li>Course schedule (string <em>∈{</em>MWF<em>,</em>TR<em>}</em>) iv. Course credit hours (unsigned integer)</li>

</ul>

<ol>

 <li>Course enrollment (unsigned integer)</li>

</ol>

<ul>

 <li>Using the values entered by the user, create a new entry in the data file based on the instructions above.</li>

 <li>If the course already exists, print the following error and continue with the program.</li>

</ul>

<strong>The program should detect this and respond immediately after reading the course number.</strong>

<strong>ERROR: course already exists</strong>

<ul>

 <li><strong><sub>R</sub></strong>: read an existing course’s information</li>

 <li>Prompt the user for a course number: (e.g., “<sub>3423</sub>”)</li>

</ul>

<strong>Enter a CS course number:</strong>

<ul>

 <li>Search for the specified course using the provided course number (e.g., “<sub>3423</sub>”).</li>

 <li>Print the course information in the following format:</li>

</ul>

<strong>Course number: <em>course number</em></strong>

<strong>Course name: <em>courseName</em></strong>

<strong>Scheduled days: <em>courseShed</em></strong>

<strong>Credit hours: <em>courseHours</em></strong>

<strong>Enrolled Students: <em>courseSize</em></strong>

<ul>

 <li>If the course is not found, print the following error instead and continue with the program.</li>

</ul>

<strong>ERROR: course not found</strong>

<ul>

 <li><strong><sub>U</sub></strong>: update an existing course record</li>

</ul>

(a) Prompt the user for the following one at a time:

<ol>

 <li>Course number (<strong>zero-indexed </strong>integer)</li>

 <li>Course name (string possibly containing whitespace)</li>

</ol>

<ul>

 <li>Course schedule (string <em>∈{</em>MWF<em>,</em>TR<em>}</em>) iv. Course credit hours (unsigned integer)</li>

</ul>

<ol>

 <li>Course enrollment (unsigned integer)</li>

</ol>

<ul>

 <li>Update each of the corresponding fields for the course based on the user’s input. <strong>If</strong></li>

</ul>

<strong>the user input is blank for a particular field (except course number), maintain the original value from the file.</strong>

<ul>

 <li>If the course record is not found, print the following error and continue with the program. <strong>You should detect this and respond immediately after reading the course number.</strong></li>

</ul>

<strong>ERROR: course not found</strong>

<ul>

 <li><strong><sub>D</sub></strong>: delete an existing course</li>

 <li>Prompt the user for a course number (e.g., “<sub>3423</sub>”):</li>

</ul>

<strong>Enter a course number:</strong>

<ul>

 <li>Delete the specified course’s record.</li>

</ul>

<strong>Hint: </strong>You may assume the<strong><sub>creditHours </sub></strong>field will never be zero for a valid course.

<ul>

 <li>Print the following message to standard output with the course’s number: <strong><em>course number </em></strong><strong>was successfully deleted.</strong></li>

 <li>If the course is not found, print the following error instead and continue with the program.</li>

</ul>

<strong>ERROR: course not found</strong>

<ul>

 <li>If an invalid character is entered, print the following error and continue with the program.</li>

</ul>

<strong>ERROR: invalid option</strong>

<ol start="3">

 <li>After an action is completed, display the menu again. This should proceed indefinitely until <strong>CTRL-D </strong>is read, or the end of the file is reached.</li>

</ol>

<h1>Locating Data</h1>

For the above functionality, <strong><sub>courses.dat </sub></strong>should not be read sequentially to search for courses. The location of the course in <strong><sub>courses.dat </sub></strong>should be calculated immediately and directly accessed without performing a search (i.e., <strong>no looping!</strong>).

<h1>Assignment Data</h1>

Input files for testing can be found in <strong>/usr/local/courses/ssilvestro/cs3423/Fall19/assign7 </strong>including an existing <sub>.dat </sub>file and input for stdin. Copy these to your own assignment’s directory.

<strong>Important: </strong>The input file assumes you are using the provided <sub>.dat </sub>file. Furthermore, each time you use the input file, you should refresh the <sub>.dat </sub>file to its original state.

<h1>Compiling Your Program</h1>

Your submission will include a makefile so the following command can be used to compile your code.

<strong>$ make assign7</strong>

<h1>Program Files</h1>

Your program should consist of up to three files:

<ul>

 <li><strong><sub>c </sub></strong>– the main file which is compiled <strong>(required)</strong></li>

 <li><strong><sub>h </sub></strong>– an optional header file, if necessary</li>

 <li><strong><sub>makefile </sub></strong>– the makefile to make the <strong><sub>assign7 </sub></strong>executable <strong>(required)</strong></li>

</ul>

<h1>Verifying Your Program</h1>

Your program must work with the input provided in <strong><sub>a7Input.txt </sub></strong>and <strong><sub>courses.dat</sub></strong>. To test it:

<ol>

 <li>Place <strong><sub>dat </sub></strong>in the same directory as your compiled program.</li>

 <li>Execute your compiled program and <strong>redirect </strong><strong><sub>txt </sub></strong>into it. You should not be copying or typing the contents of <strong><sub>a7Input.txt </sub></strong>into your terminal. <u>Redirection must work.</u></li>

 <li>Verify that the output is correct based on the input commands.</li>

 <li>Execute your program again and use your program’s menu to test that the information was correctly written to <strong><sub>dat</sub></strong>.</li>

</ol>


