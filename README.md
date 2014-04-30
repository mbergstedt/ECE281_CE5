ECE281_CE5
==========

##Task 1
Below is the code for task 1:

li $s0, 44    # stores value 44 in $s0

li $s1, -37   # stores value -37 in $s1

add $s2, $s0, $s1    # adds together values in $s0 and $s1 and stores them in $s2

sw $s2, 0x54($0)    # stores value from $s2 into the zero register with the offset of the hex value, so it stores it
in that hex address
