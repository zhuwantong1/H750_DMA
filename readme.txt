/****************************************/
这个文件使用H750做为主控进行DMA串口的发送，H750使用DMA串口输出时，像这种类似声明变量的语句要放在SCB_EnableDCache();语句之前才能保证不出错，或者关闭Dcache。或者可以学习正点原子的操作方法，开启强制透写SCB->CACR|=1<<2; //强制 D-Cache 透写,如不开启,实际使用中可能遇到各种问题
而且DMA串口输出时，H7系列不用在意是哪个通道DMA1_Stream0，DMA1_Stream1...
至于使用哪个通道，中断也要改成相应通道。见H750开发指南P200。
/****************************************/
可以使用正点原子的printf重定义函数，不需要选择 use MicroLIB，也可以完成printf的输出。
/****************************************/
另外关于DMA不能访问ITCM和DTCM，但是可以访问AXI_SRAM的问题去看这个链接https://www.jianshu.com/p/ba1034136ae8
IRAM1和IRAM2两个都打勾也能行
