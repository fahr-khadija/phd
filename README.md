
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






* ## DAY 1
 ### Introduction to iverilog and Yosys
 - RTL design:it is set of Verilog code which has intended functionality to meet with the required specification.
 - Iverilog simulator flow:
    -![image](https://user-images.githubusercontent.com/100168693/155184443-8ceef1a1-2310-48ed-a48e-a52f2a902ad3.jpeg)

    
 - LAB activity:
   - Git cloning from repositories(sky130RTLDesignAndSynthesisWorkshop)
 - code 
   ```
   https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
   # RTL Design  in Verilog using SKY130 Technology
   
    -![image](https://user-images.githubusercontent.com/100168693/155184443-8ceef1a1-2310-48ed-a48e-a52f2a902ad3.jpeg)
    ![image](https://user-images.githubusercontent.com/100168693/155176773-e2b41a89-1276-4a54-8c96-bcfc22b68bbc.jpg)



