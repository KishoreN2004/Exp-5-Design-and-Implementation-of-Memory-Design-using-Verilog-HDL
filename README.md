# Exp-5-Design-and-Simulate the-Memory-Design-using-Verilog-HDL
#Aim
To design and simulate a RAM,ROM,FIFO using Verilog HDL, and verify its functionality through a testbench in the Vivado 2023.1 environment.
Apparatus Required
Vivado 2023.1
Procedure
1. Launch Vivado 2023.1
Open Vivado and create a new project.
2. Design the Verilog Code
Write the Verilog code for the RAM,ROM,FIFO
3. Create the Testbench
Write a testbench to simulate the memory behavior. The testbench should apply various and monitor the corresponding output.
4. Create the Verilog Files
Create both the design module and the testbench in the Vivado project.
5. Run Simulation
Run the behavioral simulation to verify the output.
6. Observe the Waveforms
Analyze the output waveforms in the simulation window, and verify that the correct read and write operation.
7. Save and Document Results
Capture screenshots of the waveform and save the simulation logs. These will be included in the lab report.

# Code
# RAM

# Code

```
module ram(
input clk,rst,en,
input [7:0] din,
input [9:0] address,
output reg [7:0] dout);
reg [7:0] ram [1023:0];
always@(posedge clk)
begin
 if(rst)
   dout <= 0;
 else if(en)
   ram[address] <= din;       
 else
   dout <= ram[address];      
end
endmodule
```

# Test bench

```
module ram_tb;
reg clk_t,rst_t,en_t;
reg [7:0] din_t;
reg [9:0] address_t;
wire [7:0] dout_t;
ram dut(.clk(clk_t),.rst(rst_t),.en(en_t),.din(din_t),.address(address_t),.dout(dout_t));
initial
begin
clk_t=1'b0;
rst_t=1'b1;
en_t=1'b0;
din_t=8'd0;
address_t=10'd0;
#100 rst_t=1'b0; 
en_t=1'b1; address_t=10'd955; din_t=8'd45;
#50;
en_t=1'b1;
address_t=10'd1000;
din_t=8'd115;
#50;
en_t=1'b0;
address_t=10'd1000;
#50;
en_t=1'b0;
address_t=10'd955;
#50;
$finish;
end
always #10 clk_t = ~clk_t;
endmodule
```

# Output Waveform

<img width="1556" height="784" alt="Screenshot 2025-09-24 102942" src="https://github.com/user-attachments/assets/79c38564-6955-49d1-a2f7-24bf8a0191c9" />



# ROM

 # Code

```
module rom(
input clk,rst,
input[9:0]address,
output reg [9:0]dout );

reg[7:0] rom[1023:0];

initial 
begin
rom[10'd1000]=8'd100;
rom[10'd1021]=8'd125;
rom[10'd1023]=8'd105;
end
always@(posedge clk)
begin
if(rst)
dout<=8'b0;
else
dout<=rom[address];
end
endmodule
```
 
 # Test bench

```
module rom_tb;
reg clk_t,rst_t;
reg [9:0] address_t;
wire [7:0] dout_t;
rom dut(.clk(clk_t),.rst(rst_t),.address(address_t),.dout(dout_t));
initial
begin
clk_t=1'b0;
rst_t=1'b1;
address_t=10'd0;
#50 rst_t=1'b0;
address_t=10'd1000;
#100;
address_t=10'd1021;
#100
address_t=10'd1023;
#100;
$finish;
end
always #10 clk_t=~clk_t;
endmodule
```

# output Waveform

<img width="1565" height="812" alt="image" src="https://github.com/user-attachments/assets/b6893d87-c24e-485f-9f3e-8ffae6958a10" />


 # FIFO
 
 # write verilog code for FIFO
 
 # Test bench

# output Waveform


# Conclusion
The RAM, ROM, FIFO memory with read and write operations was designed and successfully simulated using Verilog HDL. The testbench verified both the write and read functionalities by simulating the memory operations and observing the output waveforms. The experiment demonstrates how to implement memory operations in Verilog, effectively modeling both the reading and writing processes.
 
 

