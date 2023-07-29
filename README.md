# DIGISIM-PS1-
## Implementation of Singly Linked List using Digital Circuit

**Problem Statement**

- The basic problem statement is traversing a linked list and finding the maximum value smaller than an input number X.
- The linked list is fed in the form of a binary file through a ROM starting from address 0, where address A holds the node value and address A+1 stores the address of the next node.
- The entire circuit has to be made using the 7400 IC series which includes IC's like Multiplexers, Registers, Counters, Flip Flops, combinational gates etc. [(Entire Problem Statement)](https://github.com/Fangzzxx/DIGISIM-PS1-/blob/main/Digisim'21_PS1%20(1).pdf)

**Approach**

The circuit was designed on Proteus EDA software.
- On a high level, the basic approach is to iterate over the entire linked list and check if the current node value is smaller than the input X and then update the maximum such value.
- The linked list will be read through the ROM which takes an address as input and returns the data stored at that address.
- Since the hardware cost for the ROM is high only one ROM was used to read both the node value and the address of the next node.
- Thus there will be two types of data as the ROM output, the node value which will be then proccessed using combinational logic and the address of the next node which will be fed back to the ROM and the cycle goes on until the ROM output is 255(end of list)

The data of the ROM can be changed by using this [python file](https://github.com/Fangzzxx/DIGISIM-PS1-/blob/main/create_bin_file.py). Running this script will a bin file which can be loaded into the ROM.

**Traversing through Linked-List**

- An adder was used to increase the current address by 1 and then give that address to the ROM.
- The ADDER has two input lines - current address and current address + 1/0, and a select line which is the current mode.
- Mode 0 maps to the ROM output being the current node value while Mode 1 corresponds to the ROM output being the address of the next node.
- This mode toggles on every cycle, therefore the time taken to move to the next node is 2 clock cycles.

**Calculation**

Now, we just have to calculate the maximum bank amount which Harshad Mehta can repay.
-	When the mode is 0 it means the ROM output is a node value so this value is then sent to the combinational logic.
-	The node value is compared with the current holdings of Harshad (X) using a comparator, if this value is less than or equal to X then it is further compared with the maximum such node value encountered so far stored in a register and accordingly this register is updated.
-	Once we have the final answer, we will convert it to 12-bit BCD and display the answer on a seven-segment display.
-	For 7 segment display we have used **Shift Add 3/Double Dabble Algorithm**. You can read about it [here](https://www.youtube.com/watch?v=IBgiB7KXfEY).

Here in this circuit instead of combinational logic, we used an RTL design technique using registers to shift and add for the conversion.

