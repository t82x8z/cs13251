java c
CS 2110 - Fall 2024
Project 3: Assembly Programming
Due:  10/28/2024 @ 11:59 PM
1    General
1.1    IntroductionHello and welcome to Project 3! In this project, you’ll need to prepare for your upcoming technical interview by solving LeetCode questions!  Unfortunately, for unknown reasons,  almost every programming language has been banished to the shadow realm, so you will have to complete these problems in the only language you can: LC-3 Assembly! This project has been divided into various methods that you need to implement.
Please read through the entire document before starting. Often times we elaborate on instructions
later on in the document. Start early and if you get stuck, there’s always Piazza or office hours.
1.2    General Instructions
• You can create your own labels and fill them with data as you see fit. However, if you have two labels corresponding to the same memory location (e.g., two labels without an instruction between them) this may cause autograder errors.
• You can modify the values stored in some of the helper labels we provide you if you think it’ll make it easier for you to program with.
•  Take a look at Section 8 for details on the LC-3 Assembly Programming requirements that you must adhere to.
1.3    Running the Autograder
Take a look at section 7 for information on how to run the autograder, and how to debug your code.  For this project, we will be using LC3Tools, which can be downloaded from Canvas files.
2    LeetCode EasyTo help prepare for your interviews, we’ll start with some warm up LeetCode easy questions before we get to the harder methods of the project.  You will be implementing various methods that manipulate arrays, strings, and values.
2.1    Minimum of Array (#153.5)
Here you will implement a program that calculates the minimum value of an array. Assumptions:
•  −2110 ≤ arr[i] ≤ 2110 (for all elements arr[i]). Relevant Labels:
•  ARRAY which holds the address of the first element of the array.
•  LENGTH which contains the number of elements present in that array.
•  ANSWERADDR which holds the address  of where you will store your result.
• MAX which contains the largest possible integer value (2110).
Example:
array  =  [1,3,-4,-2]
minArray(array)  ->  -4
Please write your code in minArray .asm.  Please do not modify the  .orig address as it will cause issues in the autograder.
Suggested Pseudocode:
answer  =  2110; i  =  0;
arrLength  =  LENGTH;
while  (arrLength  >  0)  { currNum  =  arr[i];
if  (currNum  <  answer)  { answer  =  currNum;
}
i++;
arrLength-- ; }
mem[mem[ANSWERADDR]]  =  answer;
2.2    Two Sum (#1)
The classic LeetCode question.  Here, given an array of integers nums  and an integer target, return indices of the two numbers in nums  such that they add up to target.
Assumptions:


• You may assume a solution exists.
• You may assume each input array has exactly one solution.
• You may not use the same element twice.
Relevant Labels:
•  ARRAY which contains the address of the first element of the array.
•  LENGTH which contains the number of elements present in that array.
•  TARGET which contains the target sum integer value.
•  ANSWER which holds the location of where you will store your pair of answers.
Example:
nums  =  [2,7,11,15]
target  =  9
twoSum(nums,  target)  ->  [0,  1]
Please write your code in twoSum .asm.  Please do not modify the .orig address as it will cause issues in the autograder.
Suggested Pseudocode:
n  =  LENGTH;
for  (i  =  0;  i  <  n;  i++)  {
for  (j  =  i  +  1;  j  <  n;  j++)  {
if  (array[i]  +  array[j]  ==  target)  {
mem[ANSWER]  =  [i,  j]; return;
} }
}
2.3    OR Adjacent Elements (#3173)
Here, given an array nums of length n, return an array answer of length n - 1 such that: answer[i] = array[i] | array[i + 1]
where  |  is the bitwise OR operation. Relevant Labels:
•  ARRAY which contains the address of the first element of the array.
•  LENGTH which contains the number of elements present in the given array.
•  TARGET which contains the address of the first element of the resulting array.
Example:


nums  =  [1,3,7,15]
orAdj(nums)  ->  [3,7,15]
Hint:  Think about how we can use the LC-3’s ALU operations to perform. a bitwise OR operation.
Please write your code in orAdj .asm.  Please do not modify the .orig address as it will cause issues in the autograder.
Suggested Pseudocode:
n  =  LENGTH;
result  =  TARGET; nums  =  ARRAY;
for  (i  =  0;  i  <  n  -  1;  i++)  {
result[i]]  =  nums[i]  |  nums[i  +  1];
}
3    LeetCode MediumNow that you have gotten your confidence up with those LeetCode Easies, let’s do some actual interview preparation with LeetCode Mediums.  In this section, we will focus on LeetCode questions dealing with string manipulation.
3.1    Octal String to Integer (#8.5)Given  an  octal  number  encoded  as  a  string,  translate  it  to  its  numerical  value.    The  value  stored  at RESULTADDR represents another different address.   Store  your numerical value result  at this different ad- dress.
Assumptions:
•  0 ≤ octalString[i] ≤ 7 (for all elements octalString[i]).
•  The provided octal string will be nonnegative.
• We do not have to worry about overflow.
Relevant Labels:
•  OCTALSTRING which holds the starting address of the octal string.
•  LENGTH which holds the length of the octal string.
•  RESULTADDR which holds the address of where you will store your numerical value result.
•  NEGATIVE_ASCII_ZERO which holds the value -48 (48 is the ASCII code for  ‘0’). Example:
OCTALSTRING  =   "2110"
octalToInteger(OCTALSTRING)  ->  1096
Hint:  Recall how we interpret characters using ASCII (ASCII table listed in Ap代 写CS 2110 - Fall 2024 Project 3: Assembly ProgrammingPython
代做程序编程语言pendix). You might find the ASCII label useful.
Implement your assembly code in octalStringToInt .asm. Please do not modify the .orig address as it will cause issues in the autograder.
Suggested Pseudocode:
octalString  =  OCTALSTRING; length  =  LENGTH;
value  =  0; i  =  0;
while  (i  <  length)  { leftShifts  =  3;
while  (leftShifts  >  0)  { value  +=  value;
leftShifts-- ;
}
digit  =  octalString[i]  -  48; value  +=  digit;
i++; }
mem[mem[RESULTADDR]]  =  value;
3.2    Snake Case to Camel Case (#1023.5)
Given a string encoded in Snake Case convert it into Camel Case. Assumptions:
•  snakeCase[i]  is either a lower case letter or an underscore.
•  A singular underscore exists in the given string and is not the first character.
•  The first letter of the second word in the Camel Case should be capitalized.
Relevant Labels:
•  SNAKESTRING which holds the starting address of the Snake Case string.
•  LENGTH which holds the length of the Snake Case string.
•  RESULTADDR which holds the address of where you will store your Camel Case string result.
•  UNDERSCORE which holds the value of an ASCII underscore.
Example:
snake_case  =  "snake_case"
snakeToCamel(snake_case)  ->  "snakeCase"
Hint:  Recall how we interpret characters using ASCII (ASCII table listed in Appendix).
Implement your assembly code in snakeToCamel .asm.  Please  do not modify the  .orig address as it will cause issues in the autograder.
Suggested Pseudocode:
capitalizeNext  =  0;
underscore  =  UNDERSCORE; length  =  LENGTH;
snakeString  =  SNAKESTRING; camelIndex  =  0;
camelString  =  RESULTADDR;
for(i  =  0;  i  <  length;  i++)  {
char  = mem[snakeString  +  i]; if  (char  ==  underscore)  {
capitalizeNext  =  1; }  else  {
if  (capitalizeNext  ==  1)  {
mem[camelString  +  camelIndex]  =  toUpper(char); capitalizeNext  =  0;
camelIndex++; }    else  {
mem[camelString  +  camelIndex]  =  char; camelIndex++;
}
} }
mem[camelString  +  camelIndex]  =  ’\0’;
4    LeetCode HardAfter doing the mediums, you still don’t quite feel ready for your big interview, so we will be doing some LeetCode Hards in this section.  We want to build up to a Binary Search, but first we need to implement another function to do so.
4.1    Right Shift (#29.1)For this section, you will implement a right bit-shift in LC-3 assembly as a subroutine. As such, values for bit shifting will no longer be placed at label values, but rather, passed in through registers.  Results will also be stored in registers. You will be given a value, and an amount of bits to shift by. Note that this will be a logical (unsigned) shift; in other words, you should fill in with zeroes for the right shift.  We will not be sign extending.
Assumptions:
•  The number of bits to shift is non-negative (amt ≥ 0)
•  The operands will be passed in through 2 registers, R0 for the value and R1 for the shift amount.
•  The result should be stored at R0.
• You will not have to handle overflow.
•  Be careful with reusing registers from BinarySearch.  Either use different temporary registers, or initialize R6 with the stack in BinarySearch and use it to store and restore registers in RightShift.
Example:
val  =  10,  amt  =  3
rightShift(val,  amt)  ->  2
Implement your code in binarySearch.asm,  under the appropriate sections and  .orig tags  (x3100 for RIGHTSHIFT). Please do not modify the .orig address as it will cause issues in the autograder.
Suggested Pseudocode:
val  =  R0;
amt  =  R1;
result  =  0;
while  (amt  <  16)  {
result  =  result  +  resu< if  (val  <  0)  {
result  =  result++; }
val  =  val  +  val; amt++;
}
R0  =  resu<
4.2    Binary Search (#704)You’re almost done with your preparation  (yay!!!).   Our last LeetCode question we will be solving is an iterative Binary Search. The method will take in a sorted array, a target value, and will return the index of the value (or -1 if not found).
Assumptions:
• You must use the RIGHTSHIFT subroutine to implement this program.
• You do not need to use stack buildup or teardown to call RIGHTSHIFT, just use JSR/JSRR and RET.
•  The target number is not guaranteed to exist in the given array.
•  Be careful with reusing registers from RightShift.  Either use different temporary registers, or initialize R6 with the stack in BinarySearch and use it to store and restore registers in RightShift.
Relevant Labels:
•  ARRAY which holds the starting address of the integer array.
•  LENGTH which holds the length of the array.
•  TARGET which holds the value of the number we are searching for.
• RESULT which holds the location of where you will store your numerical value result.
•  STACK which holds the starting address  of the stack.
Example:
array  =  [-5,  -3,  1,  4,  5,  6],  target  =  -3 binarySearch(array,  target)  ->  1
Implement your assembly code in binarySearch .asm.   As  always,  please  do  not  modify  the  .orig address as it will cause issues in the autograder.
Suggested Pseudocode:
low  =  0;
high  =  LENGTH  -  1;
while  (low  <=  high)  { sum  =  low  +  high;
mid  =  RIGHTSHIFT(sum,  1);
if  (arr[mid]  ==  TARGET)  { mem[RESULT]  =  mid;
return;
}  else  if  (arr[mid]  <  TARGET)  {
low  = mid  +  1; }  else  {
high  = mid  -  1;
} }
mem[RESULT]  =  -1;
5    Deliverables
Turn in the files minArray .asm, twoSum .asm, orAdj .asm, octalStringToInt .asm, snakeToCamel.asm, and binarySearch .asm to Gradescope by the due date.Note:  Please do not wait until the  last minute to run/test your project, history has proved that last minute turn-ins will result in long queue times for grading on Gradescope. You have been warned.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
