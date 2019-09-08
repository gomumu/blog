---
layout: post
title:  "Chapter 2. Instructions: Language of the Computer"
author: gomumu
categories: Computer_Architecture
---

<h2 id="headings">개요</h2>
<p>
목표 : Instructions을 이해 할 수 있다.<br>
강의 정보 : http://www.kocw.net/home/search/kemView.do?kemId=1125218<br>
참고 자료 : https://en.wikibooks.org/wiki/MIPS_Assembly/Instruction_Formats<br>
</p>
<hr>

<h2 id="headings">Instruction Set</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/instruction.PNG" | relative_url }}' >
사진은 CPU-Z라는 프로그램을 통해 여러 CPU의 Instruction Set을 비교한 것이다. <br>
Instruction Set이란 cpu에 정의되어있는 명령어들의 집합이다.<br>
즉 cpu는 이 명령어가 왔을 때 어떻게 동작시켜야는지 알고 있다는 것이다.<br>
사진을 보면 서로 다른 cpu들의 instruction set이 거의 비슷하지만 약간씩 다른 것을 볼 수 있다. <br>
<br>
</p>
<hr>

<h2 id="headings">Instruction Set Architecture(ISA)</h2>
<p>
<img data-action="zoom" src='{{ "/assets/post/isa.jpg" | relative_url }}' >

<b>ISA</b>란 하드웨어와 소프트웨어 사이의 인터페이스이다. 프로세서가 실행할 수 있는 모든 명령어들을 포함하고 있다.<br>
각 명령어 마다 비트 단위로 분할하여 기능에 맞게 의미를 부여하고 숫자화 되어있다.<br>
</p>
<hr>

<h2 id="headings">MIPS operation</h2>
<p>
스탠포드 대학에서 MIPS를 제안했고, MIPS Technologies에서 상용화 했다.<br>
operation(instruction) : 하나 이상의 input으로 output을 만든다.<br>
operands : operation을 구성하는 레지스터의 피연산자를 말한다.<br>
데이터가 Big Endian으로 저장된다. <br>
주소는 byte형식이다.<br>
워드 단위(32bit)로 접근하기 때문에 주소는 4의 배수이다.<br>
MIPS operation은 크게 R-Type, I-Type, J-Type으로 나뉘어진다.<br>
</p>
<hr>

<h2 id="headings">MIPS operation - R Instructions</h2>
<p>
명령어가 사용하는 모든 데이터 값이 레지스터에 있을 때 사용된다.<br>
<fieldset>
<b>OP rd, rs, rt</b>
</fieldset>
<b>OP</b>는 특정 명령어의 mnemonic이다.
<b>rs</b>, <b>rt</b> 는 소스 레지스터이고 <b>rd</b>는 대상 레지스터이다.<br>

OP가 <b>add</b> mnemonic인 경우 다음과 같이 나타낸다.<br>
<fieldset>
<b>add $s1,</b><b> $s2,</b> <b> $s3</b>
</fieldset>
<b>$s2</b>와 <b>$s3</b>의 값이 더해져 <b>$s1</b>에 저장된다.<br><br>

<b>R Format</b>은 다음과 같다.
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>opcode</th><th>rs</th><th>rt</th><th>rd</th><th>shift(shamt)</th><th>funct</th>
  </tr>
  <tr>
    <td>6 bits</td><td>5 bits</td><td>5 bits</td><td>5 bits</td><td>5 bits</td><td>6 bits</td>
  </tr>
</table>
<b>opcode</b>는 기계어 레벨로 표현 되어 있으며 instruction mnemonic을 나타낸다.<br>
관련된 instruction은 같은 opcode를 가질수도 있다.<br>
필드의 길이는 6비트(26~ 31)이다.<br><br>

<b>rs, rt, rd</b>는 소스 레지스터 및 대상 레지스터의 피연산자(operands).<br>
0과 31사이의 숫자이며 레지스터에 <b>$X</b> 형식으로 저장된다.<br>
각 필드의 길이는 5bit이다. <b>rs</b>(25 ~ 21), <b>rt</b>(20 ~ 16), <b>rd</b>(15 ~ 11)<br>
* rs = register source<br>
* rt = register target<br>
* rd = register destination<br><br>

<b>Shift (shamt)</b> 시프트 및 회전 정보를 담는 공간이다.<br>
회전되거나 이동되는 rs의 양을 나타낸다.<br>
필드의 길이는 5비트(6~10)이다.<br><br>

<b>Funct</b>는 같은 opcode를 공유하는 instruction을 구분하기위한 제어 코드를 가지고있다.<br>
Funct의 길이는 6비트(0~5)이다.<br>
예를 들어 Opcode 0x00는 ALU에 액세스하고 funct는 사용할 ALU 기능을 선택한다.<br><br>

다음은 <b>R-Type</b>의 <b>opcode</b>의 종류이다.<br>
<details>
<summary>opcode</summary>
<p>
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>Mnemonic</th><th>Meaning</th><th>Opcode</th><th>Funct</th>
  </tr>
  <tr>
    <td>add</td><td>Add</td><td>0x00</td><td>0x20</td>
  </tr>
  <tr>
    <td>addu</td><td>Add Unsigned</td><td>0x00</td><td>0x21</td>
  </tr>
  <tr>
    <td>and</td><td>Bitwise AND</td><td>0x00</td><td>0x24</td>
  </tr>
  <tr>
    <td>div</td><td>Divide</td><td>0x00</td><td>0x1A</td>
  </tr>
  <tr>
    <td>divu</td><td>Unsigned Divide</td><td>0x00</td><td>0x1B</td>
  </tr>
  <tr>
    <td>jr</td><td>Jump to Address in Register</td><td>0x00</td><td>0x08</td>
  </tr>
  <tr>
    <td>mfc0</td><td>Move from Coprocessor 0</td><td>0x10</td><td>NA</td>
  </tr>
  <tr>
    <td>mfhi</td><td>Move from HI Register</td><td>0x00</td><td>0x10</td>
  </tr>
  <tr>
    <td>mflo</td><td>Move from LO Register</td><td>0x00</td><td>0x12</td>
  </tr>
  <tr>
    <td>mthi</td><td>Move to HI Register</td><td>0x00</td><td>0x11</td>
  </tr>
  <tr>
    <td>mtlo</td><td>Move to LO Register</td><td>0x00</td><td>0x13</td>
  </tr>
  <tr>
    <td>mult</td><td>Multiply</td><td>0x00</td><td>0x18</td>
  </tr>
  <tr>
    <td>multu</td><td>Unsigned Multiply</td><td>0x00</td><td>0x19</td>
  </tr>
  <tr>
    <td>nor</td><td>Bitwise NOR (NOT-OR)</td><td>0x00</td><td>0x27</td>
  </tr>
  <tr>
    <td>or</td><td>Bitwise OR</td><td>0x00</td><td>0x25</td>
  </tr>
  <tr>
    <td>sll</td><td>Logical Shift Left</td><td>0x00</td><td>0x00</td>
  </tr>
  <tr>
    <td>slt</td><td>Set to 1 if Less Than</td><td>0x00</td><td>0x2A</td>
  </tr>
  <tr>
    <td>sltu</td><td>Set to 1 if Less Than Unsigned</td><td>0x00</td><td>0x2B</td>
  </tr>
  <tr>
    <td>sra</td><td>Arithmetic Shift Right (sign-extended)</td><td>0x00</td><td>0x03</td>
  </tr>
  <tr>
    <td>srl</td><td>Logical Shift Right (0-extended)</td><td>0x00</td><td>0x02</td>
  </tr>
  <tr>
    <td>sub</td><td>Subtract</td><td>0x00</td><td>0x22</td>
  </tr>
  <tr>
    <td>subu</td><td>Unsigned Subtract</td><td>0x00</td><td>0x23</td>
  </tr>
  <tr>
    <td>xor</td><td>Bitwise XOR (Exclusive-OR)</td><td>0x00</td><td>0x26</td>
  </tr>
</table>
</p>
</details>
</p>
<hr>

<h2 id="headings">MIPS operation - I Instructions</h2>
<p>
I Instructions은 명령어가 즉시 레지스터에 작동해야 하는 경우 사용된다.<br>
최대 16비트에 접근하여 값을 바꿀 수 있으며 그 이상은 연산 할 수 없다.<br>
다음과 같이 사용되며 opcode에 따라 다르게 호출되기도 한다.<br>
<fieldset>
<b>OP rt, IMM(rs)</b><br><br>
<b>OP  rs, rt, IMM</b>
</fieldset>
rt, rs는 레지스터에 저장된 값이며 IMM은 최대 16비트를 가지는 즉시 저장되는 필드이다. 
addi 명령어의 경우 다음과 같이 사용된다.
<fieldset>
<b>addi $s1,</b> <b>$s2, 100</b>
</fieldset>

<b>I Format</b>은 다음과 같다.
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>opcode</th><th>rs</th><th>rt</th><th>IMM</th>
  </tr>
  <tr>
    <td>6 bits</td><td>5 bits</td><td>5 bits</td><td>16 bits</td>
  </tr>
</table>
<b>opcode</b>는 기계어 레벨로 표현 되어 있으며 instruction mnemonic을 나타낸다.<br>
I-Type instruction에서의 mnemonic은 opcode와 1:1 관계를 가진다.<br>
동일한 opcode를 구별하기위한 funct 매개 변수가 없기 때문이다.<br>
필드의 길이는 6비트(26~ 31)이다.<br><br>

<b>rs, rt</b>는 소스 레지스터 및 대상 레지스터 operands.<br>
0과 31사이의 숫자이며 레지스터에 <b>$X</b> 형식으로 저장된다.<br>
각 필드의 길이는 5bit이다. <b>rs</b>(25 ~ 21), <b>rt</b>(21 ~ 16)<br>

<b>IMM</b>은 즉시 계산되는 값이다.<br>
일반적으로 여러 명령어에서 오프셋 값으로 사용되며 명령어에 따라 2의 보수로 표현되기도 한다.<br>
필드의 길이는 16bit(0~15)이다.<br><br>

다음은 <b>I-Type</b>의 <b>opcode</b>의 종류이다.<br>
<details>
<summary>opcode</summary>
<p>
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>Mnemonic</th><th>Meaning</th><th>Opcode</th><th>Funct</th>
  </tr>
  <tr>
    <td>addi</td><td>Add Immediate</td><td>0x08</td>
  </tr>
  <tr>
    <td>addiu</td><td>Add Unsigned Immediate</td><td>0x09</td>
  </tr>
  <tr>
    <td>andi</td><td>Bitwise AND Immediate</td><td>0x0C</td>
  </tr>
  <tr>
    <td>beq</td><td>Branch if Equal</td><td>0x04</td>
  </tr>
  <tr>
    <td>bgtz</td><td>Branch on Greater Than Zero</td><td>0x07</td>
  </tr>
  <tr>
    <td>blez</td><td>Branch if Less Than or Equal to Zero</td><td>0x06</td>
  </tr>
  <tr>
    <td>bne</td><td>Branch if Not Equal</td><td>0x05</td>
  </tr>
  <tr>
    <td>lb</td><td>Load Byte</td><td>0x20</td>
  </tr>
  <tr>
    <td>lbu</td><td>Load Byte Unsigned</td><td>0x24</td>
  </tr>
  <tr>
    <td>lhu</td><td>Load Halfword Unsigned</td><td>0x25</td>
  </tr>
  <tr>
    <td>lui</td><td>Load Upper Immediate</td><td>0x0F</td>
  </tr>
  <tr>
    <td>lw</td><td>Load Word</td><td>0x23</td>
  </tr>
  <tr>
    <td>ori</td><td>Bitwise OR Immediate</td><td>0x0D</td>
  </tr>
  <tr>
    <td>sb</td><td>Store Byte</td><td>0x28</td>
  </tr>
  <tr>
    <td>sh</td><td>Store Halfword</td><td>0x29</td>
  </tr>
  <tr>
    <td>slti</td><td>Set to 1 if Less Than Immediate</td><td>0x0A</td>
  </tr>
  <tr>
    <td>sltiu</td><td>Set to 1 if Less Than Unsigned Immediate</td><td>0x0B</td>
  </tr>
  <tr>
    <td>sw</td><td>Store Word</td><td>0x2B</td>
  </tr>  
</table>
</p>
</details>
</p>
<hr>

<h2 id="headings">MIPS operation - J Instructions</h2>
<p>
J Instructions은 jump를 수행한다.<br>
J Instructions은 즉시 계산되는 값을 위한 공간이 제일 많다.<br>
<fieldset>
<b>OP LABEL </b><br>
</fieldset>
OP는 특정 Jump명령의 instruction mnemonic이며 LABEL은 이동할 대상 주소이다.

<b>J Format</b>은 다음과 같다.
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>opcode</th><th>Pseudo-Address</th>
  </tr>
    <tr>
    <td>6 bit</td><td>26 bit</td>
  </tr>  
</table>

<b>opcode</b>는 jump 명령의 instruction mnemonic이다.<br>
필드의 길이는 6비트(26-31)이다. 
<br><br>

<b>Address</b>는 대상의 25bit(0~25) 단축 주소이다.<br>
2개의 하위비트, 4개의 최상위 비트가 제거되며 현재 명령어의 주소와 동일한 것으로 가정한다.<br><br>

다음은 <b>J-Type</b>의 <b>opcode</b>의 종류이다.<br>
<details>
<summary>opcode</summary>
<p>
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>Mnemonic</th><th>Meaning</th><th>Opcode</th><th>Funct</th>
  </tr>
  <tr>
    <td>j</td><td>Jump to Address</td><td>0x02</td>
  </tr>
  <tr>
    <td>jal</td><td>Jump and Link</td><td>0x03</td>
  </tr>
</table>
</p>
</details>
</p>
<hr>

<h2 id="headings">MIPS operation - FR Instructions</h2>
<p>
<b>FR instructions</b>는 부동소수점 숫자와 함께 사용하도록 한것이며 나머지는 R명령어와 같다.
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>opcode</th><th>fmt</th><th>ft</th><th>fs</th><th>fd</th><th>funct</th>
  </tr>
</table>
</p>
<hr>

<h2 id="headings">MIPS operation - FI Instructions</h2>
<p>
<b>FI instructions</b>는 부동소수점 숫자와 함께 사용하도록 한것이며 나머지는 I명령어와 같다.
<table cellspacing="0" cellpadding="0">
  <tr>
    <th>opcode</th><th>fmt</th><th>ft</th><th>IMM</th>
  </tr>
</table>
</p>
<hr>