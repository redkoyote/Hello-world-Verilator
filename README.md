# Hello-world-Verilator
Objective: The intention of this project is to start using verilator simulator.
           There might be some improvements to do in the verilator compilation step.
           For now the aim of this project is to get familiar with verilator with a existing verilog project.
           
1.-Clone the git project https://github.com/riscv-mcu/e203_hbirdv2
git clone https://github.com/riscv-mcu/e203_hbirdv2

2.-cd e203_hbirdv2/vsim

3.-Edit the tb_top.v under tb. Add the following code to generate the waveform.
  initial begin
          $display("Verilator used");
          $dumpfile("tb_top.vcd");
          $dumpvars(0, tb_top);
  end

Note: You can visualize the resulting waveform with GTKwave

4.-Addionally, edit the line 
$readmemh({testcase, ".verilog"}, itcm_mem);
for
$readmemh({"rv32ui-p-add.verilog"}, itcm_mem);

5.-Copy the memory file rv32ui-p-add.verilog to sim directory
cp ../riscv-tools/riscv-test/isa/generated/rv32ui-p-add.verilog ./

6.-Run verilator
verilator --binary --exe --build 
/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../tb/tb_top.v 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/core 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/soc 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/subsys 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/general 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/debug 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips 
/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/general/sirv_gnrl_dffs.v 
/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/general/sirv_gnrl_bufs.v 
/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/general/sirv_gnrl_icbs.v 
/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips/sirv_spi_flashmap.v 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/fab 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/mems 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips/apb_gpio 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips/apb_uart 
/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips/apb_uart/apb_uart.v 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips/apb_spi_master 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips/apb_i2c 
-I/home/cortesc/proj/verilator/e203_hbirdv2/vsim/../rtl/e203/perips/apb_adv_timer 
--top-module tb_top -o simv --trace -Wno-WIDTHEXPAND -Wno-WIDTHTRUNC -Wno-CASEINCOMPLETE -Wno-INITIALDLY -Wno-LATCH -Wno-UNOPTFLAT

7.-Execute simulation
./obj_dir/simv
