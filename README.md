
# Detail Report of 5 days workshop in RTL design Verilog with SKY130 Technology.
-![image](https://user-images.githubusercontent.com/100168693/155199764-54463945-84e3-4304-ba8b-169961a0827f.png)
## Table Of Contents 
* [Day 1: Introduction to iverilog and Yosys](https://github.com/fahr-khadija/phd#day-1)
* [Preliminary Tasks](https://github.com/fahr-khadija/phd#preliminary-tasks)
* ### [Project Scope](https://github.com/Fahr-khadija/phd#project-scope)
  * ### [Getting Started](https://github.com/Fahr-khadija/phd#getting-started)
  * ### [Introduction to Verilog RTL Design & Synthesis](https://github.com/Fahr-khadija/phd#day-1----introduction-to-verilog-rtl-design-and-synthesis)
    * #### [Setting up libraries & lab instances](https://github.com/Fahr-khadija/phd#part-1----setup-the-lab-instance-with-libraries-and-verilog-files)
    * #### [iverilog Simulation of 2:1 MUX RTL Design](https://github.com/Fahr-khadija/phd#part-2---simulation-using-iverilog-simulator---21-multiplexer-rtl-design)
    * #### [Synthesis using YOSYS Tool](https://github.com/Fahr-khadija/phd#part-3----synthesis-using-yosys-open-source-tool)
  * ### [Timing libs, Hierarchical vs Flat Synthesis & Efficient FlipFlop coding styles](https://github.com/Fahr-khadija/phd#day-2---timing-libs-hierarchical-vs-flat-synthesis--efficient-flipflop-coding-styles)
    * #### [The .lib file](https://github.com/Fahr-khadija/phd#part-1---more-about-the-lib-file)
    * #### [Hierarchical vs Flat Synthesis](https://github.com/Fahr-khadija/phd#part-2---hierarchical-vs-flat-synthesis)
    * #### [Efficient Flipflop Coding Styles & Optimizations](https://github.com/Fahr-khadija/phd#part-3---efficient-flip-flop-coding-styles-and-optimizations)
  * ### [Combinational & Sequentail Optimizations](https://github.com/Fahr-khadija/phd#day-3---combinational-and-sequential-optimizations)
    * #### [Intro to Combinational Logic Optimizations](https://github.com/Fahr-khadija/phd#part-1---intro-to-combinational-logic-optimizations)
    * #### [Intro to Sequential Logic Optimizations](https://github.com/Fahr-khadija/phd#part-2---intro-to-sequential-logic-optimizations)
    * #### [Sequential Logic Optimizations of Un-used Outputs](https://github.com/Fahr-khadija/phd#part-3---sequential-logic-optimizations-of-un-used-outputs)



## Day 1
  ### Preliminary Tasks
 The first day covers the basics of RTL Design, Testbench, Simulation and Synthesis. Open-Source softwares like iverilog (simulator) and YOSYS (Synthesis) are provided through remote access in the portal to practice labs.

RTL Design -  It consists of an actual verilog code / a set of verilog codes that have the functionality to meet the required design specifications of the circuit
TestBench - Testbench is a setup that one uses to apply a set of stimuli (test-case vector) to check the functional working of the design file

We do the above processes using a simulator software. The simulator is loaded with the design and its respective testbench file after which it looks for changes in the input signals and depending on the change, the output is evaluated. These changes in input and corresponding output values are dumped in a special format file called "value change dump" (.vcd) file. This file can be pictorially represented in waveforms using a waveform tool like gtkwave. 

### Part 1 -  Setup the lab instance with libraries and verilog files

Firstly, we have to clone 2 separate repositories namely [vsdflow](https://github.com/kunalg123/vsdflow) and [sky130RTLDesignAndSynthesisWorkshop](https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop) which contain the required library files and verilog design files to perform the simulations and logic synthesis parts of the workshop. It can be done using basic linux command gitclone ex: git clone https://github.com/kunalg123/vsdflow.git .

  ![Capture28](../main/images/Capture28.PNG)

  The second part of this day involves simulation of 2:1 Mux. The following images contain verilog behavioral file and testbench of the 2:1 Mux which can be read in linux by running the following command:
  ```
  gvim tb_good_mux -o good_mux
  ```
  
  ![This is an image](../main/images/Capture29.PNG)
  
  ![This is an image](../main/images/Capture30.PNG)
    
  ### Simulation of 2:1 Mux using iverilog
  Iverilog is a simulator. It takes in a behavioural model of a design and corresponding testbench as its arguments. The testbench generates necessary stimulus in the design (which is basically changes in primary inputs over time) and paves way for observing primary output changes. Iverilog then makes sense of this and generates an executable file (.out or .vvp file) which upon execution, dumps a .vcd file (Value Change Dump). This can later be read by gtkwave to visually observe the stimulus as waveforms.
  
  This sounds complicated but actually doing this involves only a few commands in linux:
  ```
  iverilog good_mux.v tb_good_mux.v
  ./a.out
  gtkwave tb_good_mux.vcd
  ```
  
  The following images contain the execution of all the above commands and the waveforms in the gtkwave viewer.
  
  ![This is an image](../main/images/Capture31.PNG)
  
  ![This is an image](../main/images/Capture32.PNG)
  
  ### Synthesis of 2:1 Mux using Yosys
  Yosys is a popular opensource synthesis tool. Synthesis tools like Yosys specifically require the RTL design file and .lib file. The RTL Design file is remodelled using logic gates (standard cells) provided in the .lib file. The remodelled gate-level version of the design file is called a "netlist". Before delving deep into the implementation in Yosys, let's take our time to check out the gates in a .lib file.
  
  A .lib file consists of various logic gates like AND2, OR2, NOR2, NAND2, XOR2, etc. There are various versions of the same gate as well, some of which are faster and others slower! This begs the question: <ins>what's the point in having different variations?</ins> There are very specific and harsh timing requirements gate-level circuits should meet (for example, setup time and hold time is the amount of time required for the input to a Flip-Flop to be stable before and after a clock edge respectively). If not, metastability might happen. In order to avoid this scenario, both slow and fast gates are required. But then, there are other consequences as well because the speed of a circuit depends on capacitance at the load; the wider the transistors in a gate, the less delay it will have but that'd mean more area and power (the inverse is also true). This is why proper constraint files should be supplied so that the synthesizer does its task properly and efficiently.
  
  Now, as for the implementation, it is pretty straightforward. First type the following in the terminal:
  
  ```
  yosys
  
  ```
  This opens up the Yosys prompt. After this, we'll have to execute several commands in the said prompt, all of which is mentioned below.
  
  <details><summary><b><u><ins>Click here to check the yosys commands with explanations!</ins></u></b></summary>
  <p>

  ```
  read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib   (To read .lib file)
  
  read_verilog good_mux.v                                             (To read a verilog design file)
    
  synth -top good_mux                                                 (To synthesize the design as top module; to be explained later)
  ```

  ![This is an image](../main/images/Capture34.PNG)
  
  ```
  abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib        (To map the technology and generate gate-level netlist)
  
  show                                                                (To view the generated netlist)
  ```
  
  ![This is an image](../main/images/Capture35.PNG)
  
  ![This is an image](../main/images/Capture36.PNG)
  
  Note that good_mux is synthesized as a cell named `sky130_fd_sc_hd__mux2_1` which basically is a 2:1 Multiplexer.
  
  ```
  write_verilog good_mux_netlist.v                                     (To write a verilog file)

  !gvim good_mux_netlist.v                                             (To view a file inside yosys prompt)
  ```
  
  ![This is an image](../main/images/Capture37.PNG)
  
  ![This is an image](../main/images/Capture38.PNG)
  
  </p>
  </details>


   -![image](https://user-images.githubusercontent.com/100168693/155184443-8ceef1a1-2310-48ed-a48e-a52f2a902ad3.jpeg)

    
 - LAB activity:
   - Git cloning from repositories(sky130RTLDesignAndSynthesisWorkshop)
 - code 
   ```
   https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
   # RTL Design  in Verilog using SKY130 Technology
   
    -![image](https://user-images.githubusercontent.com/100168693/155184443-8ceef1a1-2310-48ed-a48e-a52f2a902ad3.jpeg)
    ![image](https://user-images.githubusercontent.com/100168693/155176773-e2b41a89-1276-4a54-8c96-bcfc22b68bbc.jpg)



