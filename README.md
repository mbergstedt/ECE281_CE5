ECE281_CE5
==========

##Task 1
Below is the code for task 1:

```mips
addi $s0, $0, 44    # adds value 44 to 0 and stores in $s0
addi $s1, $0, -37   # adds value -37 to 0 and stores in $s1
add $s2, $s0, $s1    # adds together values in $s0 and $s1 and stores them in $s2
sw $s2, 0x54($0)    # stores value from $s2 into the zero register with the offset of the hex value, so it stores it in that hex address
```

##Task 2
Below are the hex values for the above intructions:

1st instruction: 0x2010002C

2nd instruction: 0x2011FFDB

3rd instruction: 0x02119020

4th instruction: 0xAC120054

The simulation of the instructions is below.  The screenshot shows the registers that are used:
[!alt text](https://github.com/mbergstedt/ECE281_CE5/blob/master/registers_screenshot.JPG?raw=true)

The simulation works because register 16, or $s0, is given the assigned value of 44, register 17, or $s1, is given the
assigned value -37, and register 18, or $s2, has the value of 7, which is 44 plus -37.
