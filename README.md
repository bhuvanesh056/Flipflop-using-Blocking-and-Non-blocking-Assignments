# Flipflop-using-Blocking-and-Non-blocking-Assignments
Exp 3 -Write and simulate D, SR, JK, T Flipflops using Blocking and Non blocking Assignments
   Aim: To design and simulate D, SR, JK, T Flipflops using Blocking and Non blocking Assignments in Verilog HDL and verify its functionality through a testbench using the Vivado 2023.1 simulation environment.
   
  Apparatus Required:
  Vivado 2023.1
Procedure:

Launch Vivado Open Vivado 2023.1 by double-clicking the Vivado icon or searching for it in the Start menu. 
Create a New Project Click on "Create Project" from the Vivado Quick Start window. In the New Project Wizard: Project Name: Enter a name for the project (e.g., Mux4_to_1). 
Project Location: Select the folder where the project will be saved. Click Next. 
Project Type: Select RTL Project, then click Next. Add Sources: Click on "Add Files" to add the Verilog files (e.g., mux4_to_1_gate.v, mux4_to_1_dataflow.v, etc.). 
Make sure to check the box "Copy sources into project" to avoid any external file dependencies. 
Click Next.
Add Constraints: Skip this step by clicking Next (since no constraints are needed for simulation). 
Default Part Selection: You can choose a part based on the FPGA board you are using (if any). 
If no board is used, you can choose any part, for example, xc7a35ticsg324-1L (Artix-7). 
Click Next, then Finish.
Add Verilog Source Files In the "Sources" window, right-click on "Design Sources" and select Add Sources if you didn't add all files earlier.
Add the Verilog files and the testbench. 
Check Syntax Expand the "Flow Navigator" on the left side of the Vivado interface. 
Simulate the Design In the Flow Navigator, under "Simulation", click on "Run Simulation" → "Run Behavioral Simulation". 
Vivado will open the Simulations Window, and the waveform window will show the signals defined in the testbench. 
View and Analyze Simulation Results Adjust Simulation Time To run a longer simulation or adjust timing, go to the Simulation Settings by clicking "Simulation" → "Simulation Settings". Under "Simulation", modify the Run Time (e.g., set to 1000ns).
Generate Simulation Report Once the simulation is complete, you can generate a simulation report by right-clicking on the simulation results window and selecting "Export Simulation Results".
Save the report for reference in your lab records. Save and Document Results Save your project by clicking File → Save Project.
Take screenshots of the waveform window and include them in your lab report to document your results. 
You can include the timing diagram from the simulation window showing the correct functionality of the Seven Segment across different select inputs and data inputs. 
Close the Simulation Once done, by going to Simulation → "Close Simulation

Input/Output Signal Diagram:

D FF 
<br>
<img width="300" height="123" alt="image" src="https://github.com/user-attachments/assets/7433fdf3-eee4-43e8-8409-e3cf97dd8094" /> 
<br>
<img width="174" height="156" alt="image" src="https://github.com/user-attachments/assets/9e460b9f-836a-4e04-9a23-440c129f685b" />
<br>



SR FF
<br>
<img width="272" height="559" alt="image" src="https://github.com/user-attachments/assets/4d40056a-d495-45b6-ba1c-3abfbb1731c8" />
<br>

JK FF
<br>
<img width="387" height="647" alt="image" src="https://github.com/user-attachments/assets/9c6cab9a-9a84-4861-b2f2-0d226dd8a692" />
<br>

T FF
<br>
<img width="300" height="143" alt="image" src="https://github.com/user-attachments/assets/195613ee-3fd1-4d7c-9087-777505f487f9" /> 
<br>
<img width="300" height="127" alt="image" src="https://github.com/user-attachments/assets/dfd8f91f-5161-43d6-b670-627dd53ddcce" />
<br>



RTL Code:

D Flip Flop
```
module dff(clk,rst,d,dout);
input clk, rst, d;
output reg dout;
always @(posedge clk)
begin
   if (rst)
       dout <= 1'b0;
   else
       dout <= d;
   end
endmodule
```
T Flip Flop
```
module tff(clk,rst,t,t_out);
input clk,rst,t;
output reg t_out;
always @(posedge clk)
begin   
   if (rst)
       t_out <= 1'b0;
   else if (t)
       t_out <= ~t_out;
   else
       t_out <= t_out;
   end
endmodule

```
SR Flip Flop
```
module srff (s,r,clk,rst,out);
input s, r, clk, rst;
output reg out ;
always @ (posedge clk)
begin 
   if (rst)
       out <= 1'b0;
   else if (s & ~r)
       out <= 1'b1;
   else if (~s & r)
       out <= 1'b0;
   else 
       out <= 1'bx;
end
endmodule

```
JK Flip Flop
```module jkff (clk,rst,j,k,out);
input clk, rst, j,k;
output reg out;
always @(posedge clk)
begin
    if (rst)
        out <= 1'b0;
    else if (j & ~k)
        out <= 1'b1;
    else if (~j & k)
        out <= 1'b0;
    else
        out <= ~out;
end
endmodule
```

TestBench:

D Flip Flop
```
module dff_tb;
reg clk_t,rst_t,d_t;
wire dout_t;
d_flip dut (.clk(clk_t),.rst(rst_t),.d(d_t),.dout(dout_t));
initial
begin
    d_t = 1'b0;
    clk_t = 1'b0;
    rst_t = 1'b1;
    #20
    rst_t = 0;
    d_t = 1'b0;
    #20
    d_t = 1'b1;
end
always
    #20 
    clk_t = ~clk_t;
endmodule
```

T Flip Flop
```
module tff_tb;
reg clk_t, rst_t, t_t;
wire tout_t;
t_flip dut(.clk(clk_t),.rst(rst_t),.t(t_t),.t_out(tout_t));
initial
begin
    clk_t = 1'b0;
    rst_t = 1'b1;
    #20
    rst_t = 1'b0;
    t_t = 1'b0;
    #20
    t_t = 1'b1;
    end
    always 
    #10
clk_t = ~clk_t;
endmodule
```

SR Flip Flop
```
module srff_tb;
reg clk_t,rst_t,s_t,r_t;
wire out_t;

sr_flip dut(.clk(clk_t),.rst(rst_t),.s(s_t),.r(r_t),.out(out_t));

initial
begin
    clk_t=1'b0;
    rst_t = 1'b1;
    s_t=1'b0;
    r_t= 1'b0;
    #20
    rst_t = 1'b0;
    s_t = 1'b1;
    r_t = 1'b0;
    #20
    s_t=1'b0;
    r_t= 1'b1 ;
    #20
    s_t = 1'b0;
    r_t = 1'b0;
    #20
    s_t = 1'b1 ;
    r_t = 1'b1 ;
end
always #10
clk_t = ~clk_t;

endmodule

```
JK Flip Flop
``` 
module jkff_tb;
reg clk_t,rst_t,j_t,k_t;
wire out_t;
jkFlipFlop dut(.clk(clk_t),.rst(rst_t),.j(j_t),.k(k_t),.out(out_t));

initial 
begin
    clk_t = 1'b0;
    rst_t = 1'b1;
    j_t = 1'b0;
    k_t = 1'b0;
    #20
    rst_t = 1'b0;
    j_t= 1'b1;
    k_t=1'b0;
    #20
    j_t= 1'b0;
    k_t = 1'b1;
    #20
    j_t=1'b0;
    k_t=1'b0;
    #20
    j_t = 1'b1;
    k_t = 1'b1;
end
always #10
clk_t = ~clk_t;

endmodule

```


Output waveform:

D Flip Flop:
<br>
<img width="1919" height="1078" alt="image" src="https://github.com/user-attachments/assets/15fb271a-1dcc-47ad-b0e8-635ad7cdf1a8" />
<br>

T Flip Flop:
<br>
<img width="1919" height="1077" alt="image" src="https://github.com/user-attachments/assets/f662a6e9-847e-4957-9a31-af1f2f7ec584" />
<br>

SR Flip Flop:
<br>
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/49c2a9e6-18b1-435c-ade0-69be4af34076" />
<br>

JK Flip Flop:
<br>
<img width="1910" height="1079" alt="image" src="https://github.com/user-attachments/assets/20a50fee-3917-400a-a08d-6012a47489f2" />
<br>


Conclusion:

In this experiment, the design and simulation of SR, JK, D, and T flip-flops were successfully implemented using Verilog HDL. Each flip-flop was verified with appropriate testbenches and their characteristic behaviors were observed. The SR flip-flop showed the basic set–reset operation with an invalid state, while the JK flip-flop overcame this problem by introducing a toggle feature. The D flip-flop transferred the input directly to the output at each clock edge, and the T flip-flop toggled the output when the input was high. Thus, the experiment demonstrated the working principles of the fundamental flip-flops, which serve as the basic building blocks for sequential circuits and memory design.


