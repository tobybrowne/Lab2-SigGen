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
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/b0921792-9f34-4b77-9559-3c3ffd4d4f5e)

I can then create a new shell script to build my new project:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/23212131-8731-4daf-9207-7cbbfbd99c5c)

Simulating my module, yielded the expected results, as shown below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/8215a0d5-113f-4bf8-aa32-107d3857f388)

### Challenge
The challenge for this task is to allow the rotary encoder of Vbuddy to change the frequency of the sine wave displayed.
The inclusion of the ```incr``` input makes this very easy.
The following line:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/d2e2abab-5b62-48bd-83b5-a97a0d6975d8)
Allows the rotary encoder to specify the address gap between ROM reads, essentially specifying the sine waves frequency, allowing for the generation of higher frequency waves as shown below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/1dc6f02f-001b-4856-a6d1-7cc5b288b891)

## Task 2
The goal of this task is to generate two sinusoids, for which the phase offset is determined by the value of the rotary encoder.

I started by making a "dual ROM module", which will allow me to read from two different addresses simultaneously, the code for this module, entitled ```dualrom.sv``` is shown below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/00e815e9-5079-451a-8d7a-c194cd75ed4a)

Next, I modified the top-level ```singeen.sv``` module by adding a new input signal called ```offset```, new outputs ```out1``` and ```out2```, as well as changing the internal circuitry for the desired offset behaiviour.
This module can be seen below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/6ae213de-69f7-4d3b-9ade-37b914ca3d15)

Then I modified the testbench, so that both of the modules' outputs would be plotted and so that the value of the ```offset``` input was tied to the rotary encoder. The testbench can be seen below:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/de041ad8-8319-4a54-8a5a-9786b99308d0)

Shown below is a photo of Vbuddy simulating this module. As you can see, the rotary encoder is set to a value of 64, which is giving us a wave offset of 90 degrees, as expected:
![image](https://github.com/tobybrowne/Lab2-SigGen/assets/135706062/17875a0e-9c5f-4d71-848e-2767f24d2443)

## Task 3
The aim of this task is to capture data from Vbuddy's microphone and write it to a RAM module. At the same time, the module should be reading these values back from memory at an offset determined by the rotary encoder.
Both the read and write data should be plotted.



























