ECE281_CE5
==========

##Task 1
Below is the code for task 1:

```vhdl
addi $s0, $0, 44    # adds value 44 to 0 and stores in $s0
addi $s1, $0, -37   # adds value -37 to 0 and stores in $s1
add $s2, $s0, $s1    # adds together values in $s0 and $s1 and stores them in $s2
sw $s2, 0x54($0)    # stores value from $s2 into the zero register with the offset of the hex value,
                      so it stores it in that hex address
```

##Task 2
Below are the hex values for the above intructions:

1st instruction: 0x2010002C

2nd instruction: 0x2011FFDB

3rd instruction: 0x02119020

4th instruction: 0xAC120054

The simulation of the instructions is below.  The screenshot shows the registers that are used:
![alt text](https://github.com/mbergstedt/ECE281_CE5/blob/master/registers_screenshot.JPG?raw=true)

The simulation works because register 16, or $s0, is given the assigned value of 44, register 17, or $s1, is given the
assigned value -37, and register 18, or $s2, has the value of 7, which is 44 plus -37.

##Task 3
Below are the adjusments made to the schematic and the truth tables for the ori instruction:
![alt text](https://github.com/mbergstedt/ECE281_CE5/blob/master/schematic.JPG?raw=true)
![alt text](https://github.com/mbergstedt/ECE281_CE5/blob/master/main_decoder_truthtable.JPG?raw=true)
![alt text](https://github.com/mbergstedt/ECE281_CE5/blob/master/alu_decoder_truthtable.JPG?raw=true)

When I initially tried to rewrite the vhdl code for the ori instruction, I tried using my own extra signal.  However, I forgot 
to add the signal as an input to the datapath.  Because of this, the code would did not end up recieving the signal and it
would always execute the zero extend.  After looking at the truth tables at the back of the exercise handout, I changed my
signal to the a 2 bit alusrc.  Upon making the adjustments to the vhd file, the code worked the first time I ran it.

To change the code to perform like the schematic, I first went through and changed all alusrc inputs and outputs to
```vhdl STD_LOGIC_VECTOR(1 downto 0)``` to be able to hold the additional control signal.  Next in the main decoder portion, I
went in and changed the controls signal to 10 bit rather than 9 bit.  I also added a condition for when op is 
```vhdl "001101"``` which is the opcode for an ori instruction.  In this condition, the controls signal was assigned the values
from the main decoder truth table above, with the exception being that the jump signal came before the alu opcode.  In the alu
decoder, I had the alu perform an or operation for an aluop of ```vhdl "11"```.  Then, I added a zero extend component that
only performed ```vhdl X"0000" & a``` where a was the value being extended.  Next, in the logic portion, I added two signals
for the zero immediate, which was the zero extended value, and for the final immediate.  I had the code go through the zero
extend in the same way as the sign extend, and stored the value in ```vhdl zeroimm```.  I then added a mux that chose between
the sign immediate and the zero immediate based on the bit 1 of alusrc, and then stored it into ```vhdl imm```.  This last
signal was used in the alu mux that determined source b.  Lastly I inserted the hex code for the instruction into the
testbench.  The code for that part was:
```vhdl
		instr <= X"36538000";
		wait for clk_period;
```

The testbench waveform looked as below in the registers that were used in instructions:
![alt text](https://github.com/mbergstedt/ECE281_CE5/blob/master/task3_screenshot.JPG?raw=true)

The value that is in register 19 corresponds to the hex value 0x00008007, which is the value that results from performing the
or operation on hex value 0x8000 and the signed value 7.
