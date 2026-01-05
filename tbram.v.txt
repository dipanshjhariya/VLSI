`timescale 1ns/1ps

module tb_ram;
    reg clk;
    reg we;
    reg [3:0] addr;
    reg [7:0] din;
    wire [7:0] dout;

    // Instantiate RAM
    ram #(4,8) uut (
        .clk(clk),
        .we(we),
        .addr(addr),
        .din(din),
        .dout(dout)
    );

    // Clock generation
    always #5 clk = ~clk;

    initial begin
        $dumpfile("waves.vcd");
        $dumpvars(0, tb_ram);

        clk = 0; we = 0; addr = 0; din = 0;

        // Write sequence
        #10 we = 1; addr = 4'h0; din = 8'hAA;
        #10 addr = 4'h1; din = 8'h55;
        #10 addr = 4'h2; din = 8'hFF;
        #10 we = 0;

        // Read sequence
        #10 addr = 4'h0;
        #10 addr = 4'h1;
        #10 addr = 4'h2;

        #20 $finish;
    end
endmodule