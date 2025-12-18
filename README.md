# Digital-Logic-Design-Project-2
## Part 2: Combinational Logic & Arithmetic Circuits
**Course:** CompEng 2DI4 - Laboratory 2
**Objective:** Establish proficiency in combinational logic design, Boolean minimization via Karnaugh Maps (K-Maps), and the implementation of binary arithmetic units.

### 1. Boolean Minimization & NAND Implementation
- **Assumptions**: The system utilizes High-Speed CMOS (HC) logic gates. Inverters are implemented using NAND gates by tying inputs together, as $(x \cdot x)' = x'$.
- [cite_start]**Conditions**: The target function is defined by the minterm set $F(a,b,c,d) = \Sigma(0,2,5,7,8,10,13,15)$[cite: 917, 942].
- [cite_start]**K-Map Reduction**: Grouping minterms $(0,2,8,10)$ and $(5,7,13,15)$ results in the minimized expression $F = b'd' + bd$[cite: 862].
- **Logical Reasoning**: This function represents the XNOR (equivalence) operation between inputs $b$ and $d$. [cite_start]To implement this using only NAND gates, DeMorgan’s Theorem is applied to transform the Sum-of-Products (SOP) into a NAND-NAND structure[cite: 915].
- [cite_start]**Experimental Result**: Verified Milestone 1 by implementing $F = ((bd)' \cdot (b'd')')'$ on the breadboard[cite: 862].

### 2. Data Routing with Multiplexers (MUX)
- [cite_start]**Component Selection**: Implemented a 4:1 MUX using a combination of AND, OR, and NOT logic to direct one of four data lines ($D_0 \dots D_3$) to output $Y$[cite: 945, 959].
- [cite_start]**Variable Definition**: Select lines $S_1$ and $S_0$ act as the binary address for the data lines ($2^2 = 4$ unique states)[cite: 946].
- [cite_start]**Functional Verification**: Confirmed via Table 2 that when $\{S_1, S_0\} = \{0, 1\}$, output $Y = D_1$[cite: 948, 949].

### 3. Binary Arithmetic: Adders and Subtractors
- [cite_start]**Half Adder Implementation**: Verified fundamental computation where Sum $S = A \oplus B$ and Carry $C_{out} = A \cdot B$[cite: 962].
- [cite_start]**Full Adder Engineering**: Combined two half-adders with an OR gate to accommodate a Carry-in ($C_{in}$), allowing for serial or parallel n-bit addition[cite: 969, 970].
- [cite_start]**Adder/Subtractor Logic**: Used the **cd74HC283** 4-bit parallel adder with XOR gates on the $B$ inputs[cite: 1033].
- **The "Why" of Subtraction**: When control signal $S=1$, the XOR gates act as conditional inverters, producing the 1's complement of $B$. [cite_start]By simultaneously setting $C_{in} = 1$, the circuit performs 2's complement subtraction ($A + B' + 1$)[cite: 1034, 1035].

### 4. Visualizing Data: BCD and 7-Segment Displays
- [cite_start]**Conversion Process**: Integrated the adder output with the **cd74HC4511** BCD-to-7-segment encoder[cite: 1078].
- [cite_start]**Circuit Protection**: Adhered to strict current-limiting requirements; inputs were never connected directly to ground or VCC to prevent device destruction[cite: 1056].
- [cite_start]**Experimental Observation**: Successfully displayed summed results in decimal format, verifying the bridge between binary arithmetic and human-readable output[cite: 1058, 1075].

### Mathematical Foundations (LaTeX)
#### Boolean Reduction (K-Map)
The minterms are grouped to eliminate variables $a$ and $c$:
[cite_start]$$F = \underbrace{b'd'}_{m_0, m_2, m_8, m_{10}} + \underbrace{bd}_{m_5, m_7, m_{13}, m_{15}}$$ [cite: 862]

#### NAND-Only Transformation
[cite_start]$$F = (b'd' + bd)'' = ( (b'd')' \cdot (bd)' )'$$ [cite: 862]

#### Full Adder Sum and Carry
[cite_start]$$S = A \oplus B \oplus C_{in}$$ [cite: 865]
[cite_start]$$C_{out} = AB + BC_{in} + AC_{in}$$ [cite: 865]

### ⚠️ Potential Pitfalls
- **Ripple Carry vs. Look-Ahead**: While ripple carry adders are simple, their delay is proportional to $n$ bits. [cite_start]The **cd74HC283** used here utilizes internal carry look-ahead to minimize this propagation delay[cite: 982, 984].
- [cite_start]**7-Segment Polarity**: The display is lit by pulling inputs **LO**; incorrectly driving the encoder can lead to ghosting or dark segments[cite: 1054].
- [cite_start]**Unsigned Overflow**: In 4-bit addition, a $C_4 = 1$ indicates an unsigned overflow (result $> 15$)[cite: 987, 866].

***
*Results verified by TA Milestones 1-4.*
