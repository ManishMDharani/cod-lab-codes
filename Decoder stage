module instruction_decode(
    input logic [31:0] instr,

    output logic [4:0] rs1, rs2, rd,
    output logic [31:0] imm,
    output logic reg_write, mem_read, mem_write,
    output logic mem_to_reg, alu_src, pc_src,
    output logic [3:0] alu_ctrl
);

logic [6:0] opcode;
logic [2:0] funct3;
logic [6:0] funct7;

always_comb begin

    opcode = instr[6:0];
    rd     = instr[11:7];
    funct3 = instr[14:12];
    rs1    = instr[19:15];
    rs2    = instr[24:20];
    funct7 = instr[31:25];

    imm        = 32'b0;
    reg_write  = 1'b0;
    mem_read   = 1'b0;
    mem_write  = 1'b0;
    mem_to_reg = 1'b0;
    alu_src    = 1'b0;
    pc_src     = 1'b0;
    alu_ctrl   = 4'b0000;

    case (opcode)

        // R-type
        7'b0110011: begin
            reg_write = 1'b1;
            case (funct3)
                3'b000:
                    if (funct7 == 7'b0100000)
                        alu_ctrl = 4'b0001; // SUB
                    else
                        alu_ctrl = 4'b0000; // ADD
                3'b111: alu_ctrl = 4'b0010; // AND
                3'b110: alu_ctrl = 4'b0011; // OR
                default: alu_ctrl = 4'b0000;
            endcase
        end

        // ADDI
        7'b0010011: begin
            reg_write = 1'b1;
            alu_src   = 1'b1;
            imm = {{20{instr[31]}}, instr[31:20]};
        end

        // LW
        7'b0000011: begin
            reg_write  = 1'b1;
            mem_read   = 1'b1;
            mem_to_reg = 1'b1;
            alu_src    = 1'b1;
            imm = {{20{instr[31]}}, instr[31:20]};
        end

        // SW
        7'b0100011: begin
            mem_write = 1'b1;
            alu_src   = 1'b1;
            imm = {{20{instr[31]}}, instr[31:25],
                   instr[11:7]};
        end

        // BEQ
        7'b1100011: begin
            pc_src = 1'b1;
            imm = {{19{instr[31]}}, instr[31],
                   instr[7], instr[30:25],
                   instr[11:8], 1'b0};
            alu_ctrl = 4'b0100;
        end

        default: begin
        end

    endcase
end

endmodule
