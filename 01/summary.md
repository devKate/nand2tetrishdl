# Boolean Algebra in Computing
The most basic component of a computer is a boolean logic gate, the physical hardware representation of a boolean function. The gate itself can be constructed in a variety of ways as long as the logic it implements is consistent with the function being represented. Early gates were created with tubes and vacuums. Today, logic gates are typically built as electronic switches etched into silicon, with flowing current representing 1, and no current representing 0.

Hardware design is done at a level of abstraction above these circuits. The specification for a logic gate is laid out in a hardware description language, and a company specializing in chip fabrication will handle mass production of the devices themselves. As long as the hardware designers are aware of functionality provided by existing chips, they can compose these together to create their own logic.

### Boolean Algebra
Computer hardware is based entirely on the manipulation of boolean values. With the physical creation of chips delegated to fabrication companies, hardware design begins with the analysis of boolean functions, called boolean algebra. Unlike regular algebra, which represents numeric relations, boolean algebra describes logical relations.  The main operations are conjunction, disjunction, and negation, which are actualized as AND gates, OR gates, and NOT gates in hardware.

A boolean function can be represented in 3 ways:

1) Truth Tables
The specification for a boolean function can be laid out as an enumeration of all possible input values and their resulting output values. They're easy to understand but not the most concise.
```
x	y	z
1	1	1									0
1	1	0									1
1	0	1									0
1	0	0									1
0	1	1									0
0	1	0									1
0	0	1									0
0	0	0									0
```

2) Boolean Expressions
The same function can be specified by using basic boolean operations on the input variables - typically AND, OR, and NOT.
` (x + y) * !z`

3) Canonical Representation
Canonical representation of a boolean function is essentially a list of all inputs to the function that produce an output of 1.

For example, given the boolean expression
`(x + y) * !z`
the sets of input that produce a true value are as follows:
`1, 0, 0`
`0, 1, 0`
`1, 1, 0`

This is represented canonically as
`(x * !y * !z)  + (!x * y * !z) + (x * y * !z)`.

The individual terms and their negations, `x`, `!x`, `y`, `!y`, `!z` are called literals, and they are combined into the above three expressions using logical AND. OR is then used to express that any one of these combinations is a valid input.

Though this format is needlessly verbose, it is significant because it offers proof that any boolean function can be represented using only the operations AND, OR, and NOT.  This trait is called "functional completeness".

### Functional Completeness
A set of boolean operators is functionally complete if it can be used to represent all possible outputs for a set of inputs. In other words, if a set of operators can implement any boolean function, that set is functionally complete. At this point, it would appear that the fundamental operations of boolean logic are AND, OR, and NOT. It has been demonstrated that any boolean function can be expressed using this set of operators, but there exists an even smaller functionally complete set. The singleton sets {NAND} and {NOR} are both functionally complete, their operators can be used to create implementations of AND, OR, NOT, and thus any boolean function of arbitrary complexity.
```
x	y	x NAND y
0	0		1
0	1		1
1	0		1
1	1		0

x OR y => (x NAND x) NAND (y NAND y)
0 or 0 => (0 NAND 0) NAND (0 NAND 0) => 1 NAND 1 => 0
0 or 1 => (0 NAND 0) NAND (1 NAND 1) => 1 NAND 0 => 1
1 or 0 => (1 NAND 1) NAND (0 NAND 0) => 0 NAND 1 => 1
1 or 1 => (1 NAND 1) NAND (1 NAND 1) => 0 NAND 0 => 1

x AND y => (x NAND y) NAND (x NAND y)
0 or 0 => (0 NAND 0) NAND (0 NAND 0) => 1 NAND 1 => 0
0 or 1 => (0 NAND 1) NAND (0 NAND 1) => 1 NAND 1 => 0
1 or 0 => (1 NAND 0) NAND (1 NAND 0) => 1 NAND 1 => 0
1 or 1 => (1 NAND 1) NAND (1 NAND 1) => 0 NAND 0 => 1

NOT x => x NAND x
0 => (0 NAND 0) => 1
1 => (1 NAND 1) => 0
```

```
x	y	x NOR y
0	0		1
0	1		0
1	0		0
1	1		0

x AND y => (x NOR x) NOR (y NOR y)
0 or 0 =>  (0 NOR 0) NOR (0 NOR 0) => 1 NOR 1 => 0
0 or 1 =>  (0 NOR 0) NOR (1 NOR 1) => 1 NOR 0 => 0
1 or 0 =>  (1 NOR 1) NOR (0 NOR 0) => 0 NOR 1 => 0
1 or 1 =>  (1 NOR 1) NOR (1 NOR 1) => 0 NOR 0 => 1

x OR y => (x NOR y) NOR (x NOR y)
0 or 0 =>  (0 NOR 0) NOR (0 NOR 0) => 1 NOR 1 => 0
0 or 1 =>  (0 NOR 1) NOR (0 NOR 1) => 0 NOR 0 => 1
1 or 0 =>  (1 NOR 0) NOR (1 NOR 0) => 0 NOR 0 => 1
1 or 1 =>  (1 NOR 1) NOR (1 NOR 1) => 0 NOR 0 => 1

NOT x => x NOR x
0 => (0 NOR 0) => 1
1 => (1 NOR 1) => 0
```





## Inputs and Outputs
A set of n binary variables will have 2^n possible combinations of values, because there are only two potential values for each variable. The n variables will have 2^(2^n) boolean functions which can be defined over them because there are 2^n possible combinations of inputs and two potential values for each output.
```
vars    input combinations   boolean functions
1       	2					4
3       	8					256 (2^8)
4       	16					65536 (2^16)
n       	2^n					2^(2^n)
```




