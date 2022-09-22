# sta_opentimer:
### Using Opentimer for timing analysis:


### Technical terms:

Arrival Time: The time which signal tp <b>takes</b> to go from start point to end point is called arrival time.<br>
Require time: The <b>expected time</b> for signal to arrive at end point. is called require time.<br>

## Slack:

The difference between arrival time and require time is called slack.<br>
Slack = RAT - AAT<br>
When we use maximum require time, the slack is called maximum slack.<br>
When we use miniimum require time, the slack is called minimum slack.<br>



### Static timing Analysis using Opentimer:

## Installation:<br>

To install this tool, write following commands in terminal:
```
$ git clone https://github.com/OpenTimer/OpenTimer.git
$ cd OpenTimer
$ mkdir build
$ cd build
$ cmake ../
$ make 
$ make test

```
If the test run is successfull, we can start the analysis.<br>

Now, cd to opentimer directory and run the following command:
```
./bin/ot-shell
```
It will open opentimer tool in your terminal.<br>

## Creating constaraints:

Create a new directory for your project.<br>
Then create the following files in that directory.<br>

my_netlist.timing<br>
```
clock clk 1000 50
at clk 0 500 0 500
at in 50 50 100 100
slew clk 70 50 70 50
slew in 150 100 150 100
load out 40
rat out 160 160 180 180
```
my_netlist.v<br>
```
module my_module (
in,
clk,
out
);

// primary inputs
input in;
input clk;

// primary outputs
output out;

// wires
wire n1;
wire n2;
wire n3;
wire n4;
wire n5;
wire n6;
wire in;
wire clk;
wire out;

// cells
my_dff_xsize80 f1 (.d(in), .ck(clk), .q(n1));
my_inv_xsize1 u3 (.a(n1), .o(n2));
my_inv_xsize2 u4 (.a(n2), .o(n3));
my_nand2_xsize1 u6 ( .a(n1), .b(n3), .o(n4));
my_nand4_xsize1 u5 ( .a(n3), .b(n2), .o(n5));
my_nor2_xsize1 u7 ( .a(n4), .b(n5), .o(n6) );
my_dff_xsize80 f2 ( .d(n6), .ck(clk), .q(out) );

endmodule

```
blank.spef<br>
```
*SPEF "IEEE 1481-1998"
*DESIGN "my_module"
*DATE "Tue Sep 25 11:51:50 2012"
*VENDOR "TAU 2015 Contest"
*PROGRAM "Benchmark Parasitic Generator"
*VERSION "0.0"
*DESIGN_FLOW "NETLIST_TYPE_VERILOG"
*DIVIDER /
*DELIMITER :
*BUS_DELIMITER [ ]
*T_UNIT 1 PS
*C_UNIT 1 FF
*R_UNIT 1 KOHM
*L_UNIT 1 UH
```
my_run.tcl<br>
```
set_num_threads 1
set_early_celllib my_early.lib
set_late_celllib my_late.lib
set_spef blank.spef
set_verilog my_netlist.v
set_timing my_netlist.timing
init_timer
```
and other files my_early.lib and my_late.lib files which are uploaded in this repository.<br>

Now, to run he simulation
open your proect directory and type the following in terminal:
```
$ ./../OpenTimer/bin/ot-shell
$ cd ..
$ cd projret_dir (enter your project directory name) 
```
It will open the ot shell in your terminal.<br>
Now, copy your my_run.tcl file contains and paste in that shell.<br>

The output will look like this:
<p align="left">
  <img src="opentimer_run/ot1.png">
</p>
