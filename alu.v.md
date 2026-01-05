`timescale 1ns/1ps



module tb\_alu;

&nbsp;   reg  \[31:0] A, B;

&nbsp;   reg  \[2:0]  opcode;

&nbsp;   reg         cin;

&nbsp;   wire \[31:0] Y;

&nbsp;   wire        Z, Nf, C, V;



&nbsp;   // Instantiate ALU

&nbsp;   alu #(32) uut (

&nbsp;       .A(A), .B(B), .opcode(opcode), .cin(cin),

&nbsp;       .Y(Y), .Z(Z), .Nf(Nf), .C(C), .V(V)

&nbsp;   );



&nbsp;   initial begin

&nbsp;       $dumpfile("waves.vcd");   // for GTKWave

&nbsp;       $dumpvars(0, tb\_alu);



&nbsp;       $display("time | opcode | A | B | Y | Z | Nf | C | V");



&nbsp;       // ADD

&nbsp;       A = 32'h00000001; B = 32'h00000001; opcode = 3'b000; cin = 0; #10;

&nbsp;       // SUB

&nbsp;       A = 32'h00000005; B = 32'h00000003; opcode = 3'b001; cin = 0; #10;

&nbsp;       // AND

&nbsp;       A = 32'hF0F0F0F0; B = 32'h0F0F0F0F; opcode = 3'b010; #10;

&nbsp;       // OR

&nbsp;       A = 32'hF0F0F0F0; B = 32'h0F0F0F0F; opcode = 3'b011; #10;

&nbsp;       // NOT

&nbsp;       A = 32'hAAAAAAAA; opcode = 3'b100; #10;



&nbsp;       $finish;

&nbsp;   end

endmodule

