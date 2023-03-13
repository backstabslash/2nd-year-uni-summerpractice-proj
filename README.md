
# **COMMAND SYSTEM**
Using the principles of von Neumann, a proprietary educational computer was designed, a system of commands was designed and implemented, which allows input and output of data, performing various arithmetic operations (addition, subtraction, division, multiplication and finding remainders from division), as well as other commands for transferring data from one cell to another, etc. All commands are executed sequentially, except for unconditional and conditional transitions, which can change the standard flow of the program. Their work will be described below. Each command has two operands (addresses) that it can control. For arithmetic commands, the calculation result is written in the line with the address A1. The memory of the learning machine consists of 512 lines with addresses from 1 to 512.

Below is a table of implemented commands, their number (some numbers are not commands, so they do not have a mnemonic equivalent - they are marked with three question marks - ???) and a brief description:

|**№**|**COM**|**DESCRIPTION**|
| :-: | :-: | :-: |
|0|TFR|Transferring value from A2 to A1|
|1|ADR|Addition of real numbers: A1 = A1 + A2|
|2|SBR|Subtraction of real numbers: A1 = A1 - A2|
|3|MLR|Multiplication of real numbers: A1 = A1 × A2|
|4|DVR|Division of real numbers: A1 = A1 ÷ A2|
|5|EAR|Entering an array of real numbers in quantity A2, starting from address A1|
|6|EAI|Entering an array of integers in the amount of A2, starting from the address A1|
|7|???|???|
|8|???|???|
|9|UNT|Unconditional transition from the current line to line A2|
|10|INT|Conversion of real number A1 to integer A2|
|11|ADI|Addition of integers: A1 = A1 + A2|
|12|SBI|Subtraction of integers: A1 = A1 - A2|
|13|MLI|Multiplication of integers: A1 = A1 × A2|
|14|DVI|Division of integers: A1 = A1 ÷ A2|
|15|OAR|Output of the array of real numbers in the quantity A2, starting from the address A1|
|16|OAI|Output of an array of integers in quantity A2, starting from address A1|
|17|???|???|
|18|CZT|Conditional transition: if the flag Z is 0 — transition to line A1, if the flag Z* is 1 — transition to line A2|
|19|CWT|Conditional transition: if the flag 𝜔 is 0 or 2 — transition to line A1, if flag 𝜔* is 1 — transition to line A2|
|20|REA|Conversion of an integer A1 into a real number A2|
|21|???|???|
|…|…|…|
|23|???|???|
|24|MOD|Remainder from division of integers|
|25|???|???|
|…|…|…|
|29|???|???|
|30|ITR|Move A2 (currently used array cell index) at address A1 to A2 elements|
|31|END|Completion of program execution|

***Table 1**. Learning machine command system*

# **REGISTERS AND FLAGS**
Registers are the operands used to execute the current instruction. Registers are divided into the following types according to their logical perception: RK, R1, R2, RA. RK is a register that represents the current command; RA is the address number of the current line; R1 and R2 are the operands on which the instruction is executed.

The flag 𝜔 ("omega"), which changes depending on the result of the operations of addition, subtraction, division, multiplication, is used for conditional transition Yes, its value will be 0 if the result of the operation is zero. If the result of the operation is less than zero, the flag will be set to the value 1, if the result is greater than zero, it will have the value 2. It is used to implement the conditional transition operation.

The S flag is the result sign flag.

Flag C is the flag of the sign of the transfer from the higher order.

The T flag is a turn-by-turn mode flag.

The Z flag is a zero-result flag used to implement a conditional transition operation.

The Err flag is an error flag. It signals the occurrence of an error during the execution of the program. By default, it has a value of 0, which means no errors, but when an error occurs, it changes to 1 and the program crashes.

All registers and flags have been moved to the GUI form panel, so that you can get complete information about the current command and its operands while running the machine in debug mode.

# **IMPLEMENTATION OF EDUCATIONAL** **MACHINE**
**TOOLS**

The emulator of the two-address learning machine was implemented using the C# programming language and using the framework for building applications with a graphical user interface for the platforms of the Windows family of operating systems, which is called the Microsoft WPF .Net Framework. The project was implemented in Microsoft Visual Studio 2022 integrated development environment.

**GRAPHICAL USER INTERFACE**

For the convenience of using the educational machine, a graphical user interface was created. Data is entered using the keyboard, and the emulator is controlled using the mouse. Below is a screenshot of the window, which is the main window with which the user interacts. Numbers from 1 to 6 indicate the interface elements, the functioning and purpose of which is described below.

![mainui](https://github.com/backstabslash/2nd-year-uni-summerpractice-proj/blob/master/EM2/ui.PNG)

***Picture 1**. Graphical user interface*


List and description of interface elements marked in Picture 1:

1. Table with program code. Here, the user can enter and edit program commands for further use. The user is allowed to enter both integers and real numbers. If the user enters incorrect data, when starting the program, a corresponding error will be displayed in the diagnostics window.
2. During the operation of the program, with the help of the corresponding commands specified by the user in the code table, the program can ask the user to enter data (integer or real number). To do this, a window will appear in which you will need to enter a number using the keyboard. If you enter an incorrect value or cancel the input operation, the program will display a corresponding error in the diagnostics window. If the entered value is correct, the program will continue its work, and the entered number will appear in the "Input" window. Thus, the user can remember what data he entered in the program.
3. The result of the program can be an integer or a real number. To display this information, you need to give the training machine one of the appropriate commands, and the number itself will be displayed in the "Output" window.
4. In the interface there is a panel of registers and flags that change during the execution of the program. In step-by-step mode, this panel clearly demonstrates the program execution process.
5. During the execution of the program in the learning machine, some warnings and remarks or unexpected situations may occur. In this case, all messages generated by the program will be displayed in the "Diagnostics" window.
6. The panel displays the path to the open file.
7. At the top of the window there are auxiliary and control buttons: "Save", "Save as", "Open", "Help" and "Cleaning"; "Run" - run the program without debugging, "Start debugging" - start a step-by-step program run, "Step" - go to the next command, "Finish debugging" - end a step-by-step program run.

![](https://github.com/backstabslash/2nd-year-uni-summerpractice-proj/blob/master/EM2/input.png)

***Picture 2**. Window for entering a real number*

![](https://github.com/backstabslash/2nd-year-uni-summerpractice-proj/blob/master/EM2/helpdoc.PNG)

***Picture 3.** Help window*
# **TRAINING MACHINE PROGRAMS**
## **LINEAR CALCULATIONS**
To test the possibility of implementations of linear calculations, we will compile a program for its subsequent launch using the created learning machine emulator.

Task #17: calculate the value of the function y = (4 * x^3 + 10 * z) / (x * z^2), the values of “x” and “z” are set by the user using input operations from the keyboard.

Below is the code of the corresponding program in the form of a table:

|**ADR**|**COM**|**A1**|**A2**|**DESCRIPTION**|
| :-: | :-: | :-: | :-: | :-: |
|1|EAI|15|2|User input of “x” and “z” values in addresses 15 and 16|
|2|TFR|17|15|Forwarding “x” to the 17th address so as not to lose the value later|
|3|TFR|18|16|Forwarding “z” to 18 address so as not to lose the value later|
|4|MLR|17|15|Multiplying “x” by “x” (squaring)|
|5|MLR|17|15|Multiplying “x2” by “x” (cubing)|
|6|MLR|14|17|Multiplication of “x3” by 4, sent in advance to address 14|
|7|MLR|18|16|Multiplying “z” by “z” (squaring)|
|8|MLR|18|15|Multiplication of “z2” by “x” (calculation of the divisor)|
|9|MLR|19|16|Multiplying “z” by 10, sent in advance to address 19|
|10|ADR|14|19|Addition of 4x3 and 10z (calculation of division)|
|11|DVR|14|18|Final division of pre-calculated values|
|12|OAR|14|1|Output of the calculated result of the function|
|13|END|000|000|Stopping program execution|
|14|TFR|000|4|Forwarding to 14 address 4|
|…|…|…|…|…|
|19|TFR|000|10|Forwarding to 19 address 10|

***Table 2**. Linear expression calculation program code*

## **CALCULATION USING CYCLES**
To test the possibility of implementations of cyclic calculations, we will compile a suitable program for its subsequent launch using the created learning machine emulator.

Task #2: calculate the value of the expression (wolfram alpha math input) y = Product[i^3 / (a - b), {i, 1, n}] with the values “*a”* and “b” specified by the user, if a != b, or calculate the value of the expression (a - b) / (a + b) if a = b.

Below is the code of the corresponding program in the form of a table:

|**ADR**|**COM**|**A1**|**A2**|**DESCRIPTION**|
| :-: | :-: | :-: | :-: | :-: |
|1|EAR|40|3|User input of values “a”, “b” and “i” in addresses 40, 41 and 42|
|2|TFR|50|40|Forwarding “a” to 50 address so as not to lose the value later|
|3|TFR|51|41|Forwarding “b” to 51 address so as not to lose the value later|
|4|SBR|40|41|Checking whether a - b is zero (creating a null result flag)|
|5|CZT|8|6|If the flag is now 0 (the result of the operation was not equal to 0), then go to address 8, otherwise - to 6|
|6|UNT|000|20|Unconditional transition to the 20th address for further calculation of the result|
|7|END|000|000|Stopping program execution|
|8|SBR|42|55|We check whether the iterator (stored in address 55) is not greater than the number of iterations required by the user (stored in address 42). We form the flag 𝜔: if the subtraction result is greater than or equal to 0, then 𝜔 = 2 (0), otherwise 𝜔 = 1|
|9|CWT|10|18|If the calculated flag 𝜔 is equal to 0 or 2, then we go to address 10, otherwise (equal to 1) to 18|
|10|ADR|42|55|We return the number of iterations required by the user to the initial value (before the formation of 𝜔)|
|11|TFR|57|55|Forwarding the iterator value to address 57 so as not to lose the value|
|12|MLR|57|55|Multiplying “i” by “i” (squaring)|
|13|MLR|57|55|Multiplying “i2” by “i” (cubing)|
|14|DVR|57|40|Division of i3 by the previously calculated difference a - b|
|15|MLR|512|57|Multiply the result by the just calculated value|
|16|ADR|55|56|We increase the iterator by one|
|17|UNT|000|8|Unconditional jump to address 8 to continue (or end) the cycle|
|18|OAR|512|1|Display the calculation result on the screen|
|19|END|000|000|Stopping program execution|
|20|ADR|50|51|Since a - b has already been calculated in address 4 (the result is 40), it remains to calculate only the sum |
|21|DVR|40|50|We divide the difference a - b by the just calculated sum a + b|
|22|OAR|40|1|We display the calculation result on the screen|
|23|UNT|000|7|Go to address 7 to complete the program|
|…|…|…|….|…|
|55|TFR|000|1|Forwarding to 55 address 1|
|56|TFR|000|1|Forwarding to 56 address 1|
|…|…|…|…|…|
|511|TFR|000|0|Forwarding to 511 address 0, to calculate the amount|
|512|TFR|000|1|Forwarding to 512 address 1, to calculate the product|

***Table 3**. The code of the program for calculating an expression using loops*


## **CALCULATIONS USING CYCLES (ARRAYS)**
To test the possibility of implementations of array calculations using cycles, we will compile a suitable program for its subsequent launch using the created learning machine emulator.

Task No. 11: Compile a program for counting in an integer array the number of zero elements after the element with the number specified by the user.

Below is the code of the corresponding program in the form of a table:

|**ADR**|**COM**|**A1**|**A2**|**DESCRIPTION**|
| :-: | :-: | :-: | :-: | :-: |
|1|EAI|100|5|Filling by the user of an array of 5 elements, starting from 100 address|
|2|EAI|105|1|The user enters the index of the array, starting from which the calculation of the result will take place at address 105|
|3|SBI|105|30|Checking whether the iterator (at address 30) has reached the initial value (entered by the user at address 105) to start calculations. Formation of the null result flag|
|4|CZT|7|5|Conditional transition: if the iterator has not yet reached the initial index (flag equals 0), transition to address 7, otherwise (flag 1) to address 5|
|5|ADI|105|30|We return the initial index to its starting value (which changed after executing the code at address 3)|
|6|UNT|000|11|Unconditional transition to the 11th address|
|7|ADI|105|30|We return the initial index to its starting value (which changed after executing the code at address 3)|
|8|ADI|30|31|The iterator has not yet reached the initial index, we increase it by one|
|9|ITR|14|1|We shift the address (A1) of the required array cell in address 14 by one|
|10|UNT|000|3|Unconditional transition to the 3rd address|
|11|SBI|32|30|We check whether the iterator (stored in address 30) is not greater than the number of elements of the array (stored in address 32)|
|12|CWT|13|22|If the value of the flag 𝜔 is equal to 0 (or 2), then we continue the cycle and go to address 13, otherwise (𝜔 is equal to 1) to address 22|
|13|ADI|32|30|We return the initial number of elements of the array to its starting value (which changed after executing the code at address 11)|
|14|ADI|100|34|I add a zero to the current element of the array (which changes to 1 after executing the code at address 9 and 15). Forming a zero result flag: if the element of the array was zero, then the flag will be equal to 1, otherwise 0|
|15|ITR|14|1|We shift the address (A1) of the required array cell in address 14 by one|
|16|CZT|17|19|Conditional transition: if the null result flag is 0 to address 17, otherwise (the flag is 1) to address 19|
|17|ADI|30|31|I increase the iterator by one |
|18|UNT|000|11|Unconditional transition to address 11|
|19|ADI|30|31|I increase the iterator by one|
|20|ADI|33|31|I increase the number of zeros in the array by one (initially 0 is stored at address 33)|
|21|UNT|000|11|Unconditional transition to address 11|
|22|OAI|33|11|Output of the number of zeros on the screen|
|23|END|000|000|Stopping program execution|
|…|…|…|…|…|
|30|TFR|000|1|Forwarding to 30 addresses 1|
|31|TFR|000|1|Forwarding to 31 address 1|
|32|TFR|000|5|Forwarding to 32 address 5|

***Table 4**. Code of the program for calculating arrays using loops*
