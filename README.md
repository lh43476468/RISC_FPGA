RISC_FPGA 基于FPGA的简单16位RISC系统复现
===================================

简介
-----------------------------------
此项目为Xilin暑期学校工程<br>
仿真环境：vivado 2018.3<br>
硬件：SEA-BOARD(Spartan-7)<br>

实现功能
-----------------------------------
✔ALU算术模块<br>
✔指令存储器模块<br>
✔控制模块<br>
✔寄存器模块<br>
✔ROM存储模块<br>
✔针对各个模块的完整封装处理<br>
✔对SEA-BOARD(Spartan-7)的适配约束文件<br>
✔简单的功能测试文件<br>


系统各部分功能
-----------------------------------
* 总处理器  `RISC_Processor.v`<br>
在总的处理器中我们对整体的输入输出做了定义，并且包含了控制和数据处理两个模块。<br>
由于在测试文件 `testbench.v` 中只使用了两个led，因此只输出两个led。<br>
  * 控制模块  `RISC_Control_1.v`<br>
  在控制模块中我们定义了八个指令，包括ADD、SUB、INPUT、OUTPUT、LDR、STO、INV、JNE，具体的代码段在文件中有注释。<br>
  除此之外，对不同处理状态进行了标志位处理。<br> 
  * 数据处理模块  `RISC_DataPath.v`<br>
  数据处理模块包含了ALU算术模块、ALU控制模块、指令存储模块、数据存储模块、寄存器模块。<br>
  其中还定义了跳转、程序指针变化、寄存器/存储空间读写、以及程序具体机器码的操作。<br>
    * ALU算术模块  `RISC_ALU.v`<br>
    ALU算术模块定义了加、减、反转等操作。<br>
    * ALU控制模块  `RISC_Control_2.v`<br>
    通过五位指令信号转化成ALU应该执行的操作类型。<br>
    * 指令存储模块  `RISC_InstructionMemory.v`<br>
    用于存放编辑好的程序的指令存储空间。<br>
    * 数据存储模块  `RISC_DataMemory.v`<br>
    用于存放编辑好的数据的存储空间。<br>
    * 寄存器模块  `RISC_Register.v`<br>
    对寄存器的访问存储提供控制。<br>
* 测试文件`testbench.v`<br>
调用程序存储器内指令，生产01/10的循环输出。<br>
* 约束文件`system.xdc`<br>
约束时钟和led输出。<br>
