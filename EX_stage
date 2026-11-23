module ex_stage (
    input  logic [31:0] rs1_data,
    input  logic [31:0] rs2_data,
    input  logic [31:0] imm_out,
    input  logic [31:0] address,       // current PC
    input  logic        branch,
    input  logic        alu_src,       // 0 = rs2_data, 1 = imm_out
    input  logic        fn7_5,
    input  logic        mux_inp,       // 1 = JALR
    input  logic [2:0]  fn3,
    input  logic [6:0]  imm11_5,
    input  logic [2:0]  aluop,
    input  logic [6:0]  opcode,
    output logic        and_out_ex,    // branch / jump taken
    output logic [31:0] alu_out,
    output logic [31:0] pc_ex_out      // branch / jump target
);
