# 1.SIMULATION OF LOGIC GATES ,ADDERS AND SUBTRACTORS

# AIM: 
To simulate Logic Gates ,Adders and Subtractors using Vivado 2023.1.

# APPARATUS REQUIRED: 
VIVADO 2023.1

# PROCEDURE: 

1. Open Vivado: Launch Xilinx Vivado software on your computer.

2. Create a New Project: Click on "Create Project" from the welcome page or navigate through "File" > "Project" > "New".

3. Project Settings: Follow the prompts to set up your project. Specify the project name, location, and select RTL project type.

4. Add Design Files: Add your Verilog design files to the project. You can do this by right-clicking on "Design Sources" in the Sources window, then selecting "Add Sources". Choose your Verilog files from the file browser.

5. Specify Simulation Settings: Go to "Simulation" > "Simulation Settings". Choose your simulation language (Verilog in this case) and simulation tool (Vivado Simulator).

6. Run Simulation: Go to "Flow" > "Run Simulation" > "Run Behavioral Simulation". This will launch the Vivado Simulator and compile your design for simulation.

7. Set Simulation Time: In the Vivado Simulator window, set the simulation time if it's not set automatically. This determines how long the simulation will run.

8. Run Simulation: Start the simulation by clicking on the "Run" button in the simulation window.

9. View Results: After the simulation completes, you can view waveforms, debug signals, and analyze the behavior of your design.

# Logic Diagram :

Logic Gates:
![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/ee17970c-3ac9-4603-881b-88e2825f41a4)


Half Adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/0e1ecb96-0c25-4556-832b-aeeedfdfe7b9)


Full adder:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/9bb3964c-438f-469d-a3de-c1cca6f323fb)


Half Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/731470b7-eb4e-49f8-8bb7-2994052a7184)



Full Subtractor:

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/d66f874b-c1f2-44b3-a035-7149b56430c1)



8 Bit Ripple Carry Adder

![image](https://github.com/navaneethans/VLSI-LAB-EXPERIMENTS/assets/6987778/7385a408-40a5-4203-8050-b72818622d79)



# VERILOG CODE:
# Full Adder:
```
module fulladder (sum, cout, a,b,c);
input a,b,c;
output sum, cout;
wire w1,w2,w3,w4,w5;
xor x1(w1,a,b);
xor x2(sum,w1,c);
and al(w2,a,b);
and a2(w3,b,c);
and a3(w4,a,c);
or o1(w5,w2,w3); or o2(cout,w5,w4);
endmodule
```
# Full Subractor:
```
module full_subtractor(a, b, c,D, Bout);
input a, b, c;
output D, Bout;
assign D = a^b^c;
assign Bout = (~a & b) | (~(a^ b) & c);
endmodule
```

# Half Adder:
```
module half_adder(a,b,sum,carry);
input a,b;
output sum,carry;
or(sum,a,b);
and(carry,a,b);
endmodule
```

# Half Subractor:
```
module half_subtractor(D,Bo,A,B);
input A,B;
output D,Bo;
assign D=A^B;
assign Bo=(~A)&B;
endmodule
```
# Logic Gates:
```
module logicgates(a,b,andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate);
input a,b;
output andgate,orgate,xorgate,nandgate,norgate,xnorgate,notgate;
and(andgate,a,b);
or(orgate,a,b);
xor(xorgate,a,b);
nand(nandgate,a,b);  
nor(norgate,a,b);
xnor(xnorgate,a,b);
not(notgate,a);
endmodule
```
# Ripple Carry Adder 4Bit:
```
module rippe_adder(S, Cout, X, Y,Cin);
 input [3:0] X, Y;// Two 4-bit inputs
 input Cin;
 output [3:0] S;
 output Cout;
 wire w1, w2, w3;fulladder u1(S[0], w1,X[0], Y[0], Cin);
 fulladder u2(S[1], w2,X[1], Y[1], w1);
 fulladder u3(S[2], w3,X[2], Y[2], w2);
 fulladder u4(S[3], Cout,X[3], Y[3], w3);
endmodule
module fulladder(S, Co, X, Y, Ci);
  input X, Y, Ci;
  output S, Co;  
  wire w1,w2,w3;  
  xor G1(w1, X, Y); 
  xor G2(S, w1, Ci);
  and G3(w2, w1, Ci);
  and G4(w3, X, Y);
  or G5(Co, w2, w3);
endmodule
```
# Ripple Carry Adder 8bit
```
module fulladder(a,b,c,sum,carry);
input a,b,c;
output sum,carry;
wire w1,w2,w3;
xor(w1,a,b);
xor(sum,w1,c);
and(w2,w1,c);
and(w3,a,b);
or(carry,w2,w3);
endmodule

module rca_8bit(a,b,cin,s,cout);
input [7:0]a,b;
input cin;
output [7:0]s;
output cout;
wire [7:1]w;
fulladder f1(a[0], b[0], cin, s[0], w[1]);
fulladder f2(a[1], b[1], w[1], s[1], w[2]);
fulladder f3(a[2], b[2], w[2], s[2], w[3]);
fulladder f4(a[3], b[3], w[3], s[3], w[4]);
fulladder f5(a[4], b[4], w[4], s[4], w[5]);
fulladder f6(a[5], b[5], w[5], s[5], w[6]);
fulladder f7(a[6], b[6], w[6], s[6], w[7]);
fulladder f8(a[7], b[7], w[7], s[7], cout);
endmodule
```
# OUTPUT:

# Full Adder
![Full Adder](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/78ebcf71-8ed3-4710-ae0e-47d9b794d7a5)

# Full Subractor
![Full Subtractor](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/d511498e-58e7-40ff-9fd9-6987e5e15247)

# Half Adder
![Half Adder](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/8b7a2be1-30e9-4911-b375-bc6628810f42)

# Half Subractor
![Half Subtractor](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/1cb3367d-390f-44d9-9b5c-34024cef9ad1)

# Logic Gates
![Logic Gates](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/bead9dfd-0b4d-4f86-a485-7886a157954a)

# Ripple Carry Adder 4bit
![Ripple Carry Adder](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/c379253c-3654-49b6-80ff-6adba9a515a6)

# Ripple Carry Adder 8bit
![Ripple Carry Adder8bit](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/5f580fee-30ea-4256-bc0c-1390963ed0b3)

# RTL Design:

# Full Adder
![Full Adder RTL](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/a00a1428-41f1-419f-9c2c-09a19dc02593)

# Full Subractor
![Full Subtractor RTL](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/6aaf5330-2db0-4045-9357-5ba03e7187ae)

# Half Adder
![Half Adder RTL](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/9599b9cb-8f41-4321-9a66-4c63f99e90d7)

# Half Subractor
![Half Subtractor RTL](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/44ef62e2-f75f-467b-bd39-00ed3cad081c)

# Logic Gates
![Logic Gates RTL](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/ad868688-74fe-4070-a086-8eb25dfcec8c)

# Ripple Carry Adder 4bit
![Ripple Carry Adder RTL](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/f68c9678-9f0e-4caa-b93f-35261722fe55)

# Ripple Carry Adder 8bit
![Ripple Carry Adder8bit RTL](https://github.com/RCKcharan10/VLSI-LAB-EXP-1/assets/117891438/ca0d8db1-719e-466d-bcf7-0c199390f62a)


# Result:

Thus the Simulation of Logic Gates ,Adders and Subtractors is done and verified.
