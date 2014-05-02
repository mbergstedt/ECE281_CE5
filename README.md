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

Initial attempts to connect the waveform to show the values from through the given file produce an ISIM with nothing on
the screen inside of it.
