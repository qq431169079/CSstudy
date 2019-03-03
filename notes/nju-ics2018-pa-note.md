# NJU-ICS2018 课设笔记

虽然不是njuer，但是南大这套课程做得真不错，跟ivy接轨了，慕名做做，复习一下计算机体系。

## PA0

对我这种老油条来说，太简单了，mac下一路敲命令搞定，不过如果是windows应该会困难重重，看QA里说不少人windows下的docker有问题。果然程序员还是应该至少熟悉一种Unix类环境才行。

不过我也很理解助教烦躁的心情，因为学计算机与其他理工科不同的一点就是需要极大的折腾之心，纯理论是学不好计算机的，一定要坚持动手折腾。

## PA1

```
/* TODO: Re-organize the `CPU_state' structure to match the register
 * encoding scheme in i386 instruction format. For example, if we
 * access cpu.gpr[3]._16, we will get the `bx' register; if we access
 * cpu.gpr[1]._8[1], we will get the 'ch' register. Hint: Use `union'.
 * For more details about the register encoding scheme, see i386 manual.
 */
```
故意没设置好CPU的结构体，让你重新设置，考验c语言能力。
首先根据[i386手册](http://css.csail.mit.edu/6.858/2013/readings/i386.pdf),查看CPU寄存器的结构：
```
GENERAL REGISTERS
31              23               15                7                0
╔════════════════╪════════════════╬════════════════╧════════════════╗
║                                EAX            AH AX AL            ║ 
╠════════════════╪════════════════╬════════════════╩════════════════╣ 
║                                EDX            DH DX DL            ║ 
╠════════════════╪════════════════╬════════════════╩════════════════╣ 
║                                ECX            CH CX CL            ║ 
╠════════════════╪════════════════╬════════════════╩════════════════╣ 
║                                EBX            BH BX BL            ║ 
╠════════════════╪════════════════╬════════════════╩════════════════╣ 
║                                EBP               BP               ║ 
╠════════════════╪════════════════╬════════════════╪════════════════╣ 
║                                ESI               SI               ║ 
╠════════════════╪════════════════╬════════════════╪════════════════╣ 
║                                EDI               DI               ║ 
╠════════════════╪════════════════╬════════════════╪════════════════╣ 
║                                ESP               SP               ║ 
╚════════════════╪════════════════╬════════════════╪════════════════╝
```
也就是说要实现访问ax[12]，ax[5]实际上就是访问eax[12],ah[5]和al[5], C语言中union的各成员占用相同的内存空间，