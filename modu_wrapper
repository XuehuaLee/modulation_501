# modulation_501
`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date:    13:06:16 02/24/2016 
// Design Name: 
// Module Name:    modu_core_app 
// Project Name: 
// Target Devices: 
// Tool versions: 
// Description: 
//
// Dependencies: 
//
// Revision: 
// Revision 0.01 - File Created
// Additional Comments: 
//
//////////////////////////////////////////////////////////////////////////////////
module modu_core_app(
	input			da_clk_280MHz,
	input			rst_n,
	//pcie interface
	input			pcie_data_ready_i,
	output			pcie_data_rden_o,
	output			pcie_rd_clk_o,
	input	[7:0]	pcie_data_in_i,
	
	output	[15:0]	modu_left_o
	//output	[15:0]	modu_right_o
    );
	
	
wire clk_fc_70MHz;
assign 	pcie_rd_clk_o = clk_fc_70MHz;
clock_manager clock_manager(
		.da_clk_280MHz(da_clk_280MHz),
		.rst_n(rst_n),
		.symbol_rate_rden(symbol_rate_rden),
		.clk_fc_70MHz(clk_fc_70MHz)
    );

wire [11:0] modu_data_out;
rs_encoder_wrapper rs_encoder_wrapper(
		.clk_70MHz(clk_fc_70MHz),
		.da_clk_280MHz(da_clk_280MHz),
		.rst_n(rst_n),
		.pcie_data_ready_i(pcie_data_ready_i),				//PCIe缓存中有数据的标志位
		.pcie_data_in_i(pcie_data_in_i),				//PCIe缓存输入数据
		.pcie_data_rden_o(pcie_data_rden_o),				//PCIe缓存读使能信号
		
		.symbol_rate_rden(symbol_rate_rden),
		.modu_data_out_o(modu_data_out),			//调制数据输出
		.modu_data_out_nd_o(modu_data_out_nd)		//调制数据输出有效指示信号
    );

modulation modulation(
		.rst_n(rst_n),
		.clk_280MHz(da_clk_280MHz),
		.data_in(modu_data_out),
		.data_in_rfd(modu_data_out_nd),
		
		.modu_left(modu_left_o)
		//.modu_right(modu_right_o)
    );	

endmodule
