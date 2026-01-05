module alu #(

&nbsp;   parameter N = 32

)(

&nbsp;   input  wire \[N-1:0] A,

&nbsp;   input  wire \[N-1:0] B,

&nbsp;   input  wire \[2:0]   opcode, // 000:ADD, 001:SUB, 010:AND, 011:OR, 100:NOT

&nbsp;   input  wire         cin,    // external carry-in (optional, use 0 if not chaining)

&nbsp;   output reg  \[N-1:0] Y,

&nbsp;   output reg          Z,      // zero

&nbsp;   output reg          Nf,     // negative (MSB)

&nbsp;   output reg          C,      // carry-out (valid for ADD/SUB)

&nbsp;   output reg          V       // overflow (valid for ADD/SUB)

);



&nbsp;   // Decode

&nbsp;   wire is\_add = (opcode == 3'b000);

&nbsp;   wire is\_sub = (opcode == 3'b001);

&nbsp;   wire is\_and = (opcode == 3'b010);

&nbsp;   wire is\_or  = (opcode == 3'b011);

&nbsp;   wire is\_not = (opcode == 3'b100);



&nbsp;   // Subtraction via two's complement

&nbsp;   wire \[N-1:0] B\_eff = is\_sub ? ~B : B;

&nbsp;   wire         ci    = is\_sub ? 1'b1 : cin;



&nbsp;   // Arithmetic

&nbsp;   wire \[N:0] sum\_ext = {1'b0, A} + {1'b0, B\_eff} + ci;

&nbsp;   wire \[N-1:0] sum   = sum\_ext\[N-1:0];

&nbsp;   wire         cout  = sum\_ext\[N];



&nbsp;   // Overflow detection (signed)

&nbsp;   // For ADD: V = (~(A\[N-1] ^ B\_eff\[N-1])) \& (A\[N-1] ^ sum\[N-1])

&nbsp;   // For SUB: B\_eff = ~B; same formula holds since SUB is ADD with B\_eff and ci=1

&nbsp;   wire ovf = (~(A\[N-1] ^ B\_eff\[N-1])) \& (A\[N-1] ^ sum\[N-1]);



&nbsp;   // Logic

&nbsp;   wire \[N-1:0] logic\_and = A \& B;

&nbsp;   wire \[N-1:0] logic\_or  = A | B;

&nbsp;   wire \[N-1:0] logic\_not = ~A;



&nbsp;   // Result select

&nbsp;   always @\* begin

&nbsp;       // Default

&nbsp;       Y = {N{1'b0}};

&nbsp;       C = 1'b0;

&nbsp;       V = 1'b0;



&nbsp;       if (is\_add || is\_sub) begin

&nbsp;           Y = sum;

&nbsp;           C = cout;

&nbsp;           V = ovf;

&nbsp;       end else if (is\_and) begin

&nbsp;           Y = logic\_and;

&nbsp;       end else if (is\_or) begin

&nbsp;           Y = logic\_or;

&nbsp;       end else if (is\_not) begin

&nbsp;           Y = logic\_not;

&nbsp;       end else begin

&nbsp;           Y = {N{1'b0}}; // undefined opcode -> safe default

&nbsp;       end



&nbsp;       Z  = (Y == {N{1'b0}});

&nbsp;       Nf = Y\[N-1];

&nbsp;   end



endmodule

