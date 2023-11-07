# Lab 2: Signal Generation and Capture

## Task 1
The first step of this task is to create a 256x8 ROM module (256 locations of size 8 bits), this ROM module must be initialized with the sine wave values stored in the ```sinerom.mem``` file.
My code for this module can be seen below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/2bc6c0da-f5a0-4a42-89c9-3e60c49c31a0)

Next I need to use this initialized ROM module to create a module that iterates through the values of the sine wave.
This can be done by linking the ROM module, with a counter module, as shown below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/79cdd2bd-84c8-4102-93e1-1d304732f404)

The counter module used in this design has an additional output that the counter designed in Lab 1 does not have.
This is the ```incr``` signal, an 8-bit value which defines the increment with which the counter counts.

I started by modifying the ```counter.cv``` module made in lab 1 to include this functionality as shown:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/a48db2d3-1803-4359-be6e-199a40018a5c)

The only difficult part of this process was modifying the mechanism through which the enable line works, which required the addition of an if/else statement in the always block.

Next, I defined the top-level module ```sinegen.sv``` to connect ```rom.sv``` and ```counter.sv```, the code for this can be seen below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/deaf77b6-0272-447c-9cfc-7b552233df94)

Then, I created the testbench file for my module, entitled ```sinegen_tb.cpp```, at the moment it is very simple, just plotting the value of the module's output to Vbuddy.
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/7f482bad-678c-4e50-8f2d-bb3e67556dcc)

I can then create a new shell script to build my new project:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/23212131-8731-4daf-9207-7cbbfbd99c5c)










