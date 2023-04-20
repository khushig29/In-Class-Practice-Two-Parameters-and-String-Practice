#Khushi Gupta 
#CS 2640.01
#April 19, 2023 
#In-Class Practice: Two Parameters and String Practice 
#Goal = Complete the in-class exercise for writing a macro that takes in two parameters and write a program that uses 'aString'. Use the given information as follows: 
#	Task 1
# - Macros can also take in multiple parameters. Define a macro that:
# - Takes in two parameters
# - An int and a string
# - Doubles the int
# - Calls another macro to print the string
# - Define the int and string in the program
#	Task 2
# - Using the ‘aString’ macro we defined on the previous slide, write a MIPS program that passes the programmer’s defined string to the macro, uses a loop to print the string 3 times (each on a new line), and then exits the program.

# Task 1 - Macro Definition
.macro doubleAndPrint num, str
    li $t0, 2
    mul $a0, $t0, \num
    la $a1, \str
    jal printString
.end_macro

# Task 2 - Macro Definition
.macro aString str
    la $a0, \str
    jal printString
.end_macro

# Print String Macro Definition
printString:
    li $v0, 4
    syscall
    jr $ra

# Data Part
.data
myString: .asciiz "Hello, world!"

# Text Part
.text
main:
    # Task 1
    li $s0, 5
    doubleAndPrint $s0, myString
    li $s1, 10
    doubleAndPrint $s1, myString

    # Task 2
    li $s0, 0      # counter initialized to 0
print_loop:
    beq $s0, 3, exit_program  # if counter reaches 3, exit the program
    aString myString         # calling macro to print string
    addi $s0, $s0, 1         # increment counter
    j print_loop             # jump back to print_loop

exit_program:
    li $v0, 10
    syscall
