# Processor Emulator

1. **LOAD_CONST**<br>
Value in the first byte of instruction = opcode = 0x00
<br>This instruction loads the constant in the third byte of the 
     instruction to the register referenced by the second byte.
<br>*Eg.* 00 00 80 => loads the constant 0x80 (= 128) to r0

2. **ADD_CONST**
<br>opcode = 0x01
<br>This instruction adds the constant in the third byte of the 
     instruction to the register referenced by the second byte.
<br>*Eg.* 01 00 80 => adds the constant 0x80 (= 128) to r0 (If the
       value of the register was 0x01, the new value would be 0x81)

3. **SUB_CONST**
<br>opcode = 0x02
<br>This instruction subtracts the constant in the third byte of the 
     instruction to the register referenced by the second byte.
<br>*Eg.* 02 00 80 => subtracts the constant 0x80 (= 128) from r0

4. **ADD**
<br> opcode = 0x03
<br> This instruction adds the values stored in the registers 
     referenced by the second and third byte of the instruction and 
     stores it back in the register referenced by the second byte.
<br>*Eg.* 03 07 01 => stores value of r7+r1 into r1

5. **SUB**
<br>opcode = 0x04
<br>This instruction subtracts the values stored in the register
     referenced by the second byte from the register referenced by 
     the third byte of the instruction and stores it back in the
     register referenced by the second byte.
<br>*Eg.* 04 02 03 => stores value of r2-r3 into r2

6. **PRINT**
<br>opcode = 0x05
<br>This instruction prints the ASCII character corresponding to the 
     value stored in the register referenced by the second byte. 
     The third byte's value has no significance to the instruction.
<br>*Eg.* 05 06 00 => if r6 stores 0x41 (= 65), 'A' is printed on the
       screen.

7. **JUMP_IF_NOT_ZERO** (JNZ)
<br>opcode = 0x06
<br>Usually, after the execution of an instruction, the processor 
     moves on to execute the instuction stored next (adjacent) in memory. 
     The JNZ instruction modifies the control flow of the program based on 
     the value of the register referenced by the second byte. If the
     value is not zero, the processor jumps to the byte referenced by
     the third byte of the instruction and starts reading and executing
     instructions from there. If the value if zero, no jump occurs and
     the processor executes the instructions stored next in memory.
<br>*Eg.* 06 02 09 => If the value in r2 is non-zero, processor sets the 
       instruction pointer to 10th byte in memory (address 0x00 
       corresponds to the first byte of memory)

8. **JUMP_IF_ZERO** (JZ)
<br>opcode = 0x07
<br>Same, as JUMP_IF_NOT_ZERO but the jump instead happens when the value 
     stored in the register referred by the second byte is zero.
     
9. **LOAD**
<br>opcode = 0x08
<br>This instruction loads the byte stored at the address specified by
     the value in register referred by the third byte of the instruction
     to the register referred by the second byte.
<br>*Eg.* 08 03 00 => If the value in r0 is 7, this instruction stores the
   value at address 7 in memory into r3 i.e. r3 = memory[7]

10. **STORE**
<br>opcode = 0x09
<br>This instruction stores the value in the register referred by the 
     third byte of the instruction to the memory location whose address 
     is given by the value of the register reffered by the second byte.
<br>*Eg.* 09 03 00 => If the value in r3 is 4 and r0 is 7, this instruction
   stores 7 into address 4 of memory i.e. memory[4] = 7

11. **HALT**
<br>opcode = 0xff
<br>This instruction halts the processor. The processor is done for the day at this point.<br>
