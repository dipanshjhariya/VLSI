module ram #(
    parameter ADDR_WIDTH = 4,   // 16 memory locations
    parameter DATA_WIDTH = 8    // 8-bit data
)(
    input  wire                  clk,
    input  wire                  we,      // write enable
    input  wire [ADDR_WIDTH-1:0] addr,
    input  wire [DATA_WIDTH-1:0] din,
    output reg  [DATA_WIDTH-1:0] dout
);

    // Memory array
    reg [DATA_WIDTH-1:0] mem [0:(1<<ADDR_WIDTH)-1];

    always @(posedge clk) begin
        if (we) begin
            mem[addr] <= din;   // synchronous write
        end
        dout <= mem[addr];      // synchronous read
    end

endmodule