
# Hierarchical Modelling Concept

### Module
Module is the basic building block in verilog
```Verilog
module <module_name> (<module_terminal_list>);
...
<module_internals>
...
endmodule
```
Verilog is both behavioral and structural language. Internals of each module can be defined at four level of abstraction depending upon the need of the design. The module behave identically with the external environment irrespective of the level of abstraction at which the module is described. The internals of the module are hidden from the environment. Thus the level of abstraction to describe a module can be changed without any changes in the environment.
 - Behavioral or Algorithmic level : A module can be implemented in terms of desired design algorithm without concern for the hardware implementation details
 - Dataflow level : At this level the module is designed by specifying the data flow. The designer is aware of how data flows between hardware registers and how the data is processed in the design
 - Gate level : The module is implemented in terms of logic gates and interconnection between these gates. Design at this level is similar to describing a design in terms of gate-level logic diagram
 - Switch level : This is the lowest level of abstraction provided by Verilog. A module can be implemented in terms of switches, storage nodes, and interconnections between them. Design at this level requires knowledge of switch lever implementation details

In design community the term register transfer level `RTL` is frequently used for a Verilog description that uses a combination of behavioral and dataflow constructs and is acceptable to logic synthesis tools.

### Components of a Simulation 
The functionality of the design block can be tested by applying stimulus and checking results. We call such a block the stimulus block. The stimulus block is also commonly called a test bench. 
Two styles of stimulus application is possible
- In the first style the stimulus block instantiates the design block and directly drives the signals in the design block.
- The second style of applying stimulus is to instantiate both the stimulus and the design block in a top level dummy module. The stimulus block interacts with the design block only through the interface

# Basic Concepts

### Lexical Convections 
There are two types of number specification in Verilog : sized and unsized

sized numbers are represented as `<size> ' <base format> <number>` eg: 4'b1111 , 12'habc 
unsized numbers are numbers that are specified without a base format eg: 23456 , 'hc3 'o21 they are 32 bit by default 
#### x or z values 
verilog has two symbols for unknown and high impedance values. These values are very important for modelling real circuits. An unknown value is denoted by an `x`. A high impedance value is denoted by `z` 

An x or z sets four bits for a number in the hexadecimal base , three bits for a number in the octal base and one bit for a number in the binary base. If the most significant bit of a number is 0,x,z the number is automatically extended to fill the most significant bits, respectively with 0,x or z. This makes it easy to assign x or z to whole vector. If the most significant digit is 1, then it is also zero extended.

#### Negative numbers
Negative number can be specified by putting a minus sign before the size for a constant number. 
It is illegal to have a minus sign between <base_format> and <number_> 
eg : (doubt) -6'd3 // 8-bit negative number stored as 2's complement of 3
4'd-2 // illegal specification

#### Underscore characters and question marks
Underscore is allowed anywhere in a number except for the first character just to improve readability
A question mark "?" is the verilog HDL alternative for z in the context of numbers
eg: 4'b10?? // equivalent to 4'b10zz 

#### Strings 
Similar to C 

### Data Types

#### Nets
- Nets represent connection between hardware elements. Just as in real circuits, nets have values continuously driven on them by outputs of devices that they are connected to.
- Nets are declared primarily with the keyword `wire`. Nets are one-bit values by default unless they are declared explicitly as vectors.
- The default value of a net is z (except the `trigreg` net which defaults to x)
- Nets get the output value of their drives. If a net has no driver, it gets the value z

#### Registers
-  Registers represent data storage elements. Registers retain value until another value is placed onto them .
- Do not confuse the term registers in verilog with hardware registers built from edge-triggered flip-flops in real circuits.
- Register data type are commonly declared by the keyword reg. The default value of reg data type is x.

#### Vectors 
- Nets or reg data type can be declared as vectors (multiple bit widths). If bit width is not specified , the default is scalar (1-bit)
- Vectors can be declared at [high#:low#] or [low#:high#] , but the left number in the squared bracket is always the most significant bit of the vector.
	- eg : reg [0 : 40] bus

#### Integer, Real , and Time Register Data Types 
- Integer
	- An integer is a general purpose register data type used for manipulating quantities. Integers are declared by the keyword integer.
	- The default width for an integer is the host-machine word size, which is implementation specific but is at least 32 bits.
	- Registers declared with data type reg store values as unsigned quantities where as integer stores values as signed quantities
- Real 
	- Real number constants and real register data types are declared with the keyword real. They can be specified in decimal notation or in scientific notation. Real number cannot have a range declaration and the default value is 0
- Time
	- Verilog simulation is done with respect to simulation time. A special time register data type is used in verilog to store simulation time. A time variable is declared with the keyword time. The width for the time register data type is implementation specific but is at least 64 bits. 
	- The system function `$time` is invoked to get the current simulation time

#### Arrays
- Arrays are allowed in veilog for `reg , integer , time` and `vector` register data types
- Arrays are not allowed for real variables 
- Arrays are accessed by <array_name>[<subscript_>] 
- (doubt) Multidimensional arrays are not permitted in Verilog

#### (doubt)Memories
- In digital simulation, one often needs to model register files, RAMs,  and ROMs.
- Memories are modeled in Verilog simply as array of registers. Each element in the array is known as a word.

#### Parameter
-  Verilog allows constants to be defined in a module by the keyword `parameter` Parameter cannot be used as variables. Parameter values for each module instance can be overridden individually at compile time.
- Hardcoded number should be avoided

### System tasks and compiler directives

#### System Tasks
- Verilog provides standard system tasks to do certain routine operations. All system tasks appear in the form `$<keyword>` 
- `$display` is the main system task for displaying values of variables or strings or expressions.
- Verilog provides a mechanism to monitor a signal when its value changes. This facility is provided by the `$monitor` task
	- Only one monitoring list can be active at a time. If there are more than one monitor statement in your simulation , the last monitor statement will be the active statement. The earlier monitor statements will be overridden
	- Two tasks are used to switch monitoring on and off : $monitoron and $monitoroff
- The task `$stop` is provided to stop during a simulation
	- The stop tasks put the simulation in an interactive mode
- The `$finish` task terminates the simulation

#### Compiler Directives
- Compiler directives are provided in verilog. All compiler directive are defined by using the '<keyword_> 
- `' define` : The 'define directive is used to define text macros in verilog. This is similar to `#define` constructs in C
- `' include` : The include directive allows you to include entire content of a Verilog source file in another Verilog file during compilation. similar to `#include` in C
  
# Modules and Ports

### Module
Port list and port declaration are present only if the module has any ports to interact with the external environment. The five components within a module are - variable declarations, dataflow statements, instantiation of lower modules, behavioral blocks and tasks or functions. 

### Ports 
- Ports provide the interface by which a module can communicate with its environment. For example, the input/output pins of an IC chips are its ports. The environment can interact with the module only through its ports.
- Note that all port declaration are implicitly declared as wire in Verilog. Thus, if a port is intended to be a wire, it is sufficient to declare it as output, input, or inout. 

#### Connecting Ports to External Signals
-  Connecting by the ordered list : The signals to be connected must appear in module instantiation in the same order as the ports in the port list in the module definition
	- eg fullAdd4(sum, c_out, A , B, c_in)
- Verilog provides the capability to connect external signal to ports by the port names, rather than by position
	- eg: fullAdd4(.c_out(C_OUT) , .sum(SUM), .a(A), .b(B), .c_in(C_IN))


# Gate-Level Modeling

### Gate Types
- Verilog supports basic logic gates as predefined primitives. These primitives are instantiated like modules except that they are predefined in Verilog and do not need a module definition.
- There are two classes of basic gates : `and/or` gates and `buf/not` gates

#### And/Or Gates
- And/Or gates have one scalar output and multiple scalar inputs. The first terminal in the list of gate terminals is an output and the other terminals are inputs.
- (doubt) regarding the x z in the truth table
  
#### Buf/Not Gates
- Buf/Not gates have one scalar input and one or more scalar outputs. The last terminal in the port list is connected to the input. Other terminals in the port list is connected to the outputs.
- eg : buf b1(OUT1 , OUT2, IN);

#### Buffif/notif
- Gates with an additional control signal on buf and not gates are also available and are called as bufif/notif
- These gates propagate only if their control signal is asserted. They propagate z if their control signal is deasserted.
- eg : buffif1 b1(out , in , ctrl)

### Gate Delays
- In real circuit , logic gates have delays associated with them. Gate delays allow the Verilog user to specify delays through the logic circuit. Pin-to-pin delays can also be specified in Verilog.
#### Rise, Fall, and Turn-off Delays
- Rise Delay
	- The rise delay is associated with a gate output transition to a 1 from another value
- Fall Delay
	- The fall delay is associated with a gate output transition to a 0 from another value
- Turn-off delay
	- The turn-off delay is associated with a gate output transition to a high impedance value (z) from another value
	- If the value changes to (x) the minimum of the three delays is considered
- eg : buffif0 #(3 , 4 , 5) b1(out, in, control) // rise = 3, fall = 4, turn-off=5

#### Min/Typ/Max Values
- Verilog provides an additional level of control for each type of delay monitored above. For each type of delay - three values, min, typ, and max can be specified.
- These values are used to model devices whose delays vary within a minimum and maximum range because of the IC fabrication process variations.
- Min Value
	- The min value is the minimum delay value that the designer expects the gate to have
- Typ Value
	- The typ value is the typical delay value that the designer expects the gate to have
- Max Value
	- The max value is the maximum delay value that the designer expects the gate to have
- eg and #(2:3:4 , 3:4:5 , 4:5:6) a3(out , in , control)
- > veilog test.v +maxdelays -> invoke simulation with maximum delays
  
# Dataflow Modeling
- For smaller circuits the gate-level modeling approach works very well because the number of gates is limited and the designer can instantiate and connect every gate individually. However in complex designs the number of gates is very large.
- Dataflow modeling provides a powerful way to implement a design. Verilog allows a circuit to be designed in terms of the data flow between registers and how a design process data rather than instantiation of individual gates.
- Currently automated tools are used to create a gate-level circuit from a dataflow design description. This process is called logic synthesis.
- This approach allows the designer to concentrate on optimizing the circuit in terms of data flow.
- In digital design community, the term RTL ( Register Transfer Level ) design is commonly used for a combination of dataflow modeling and behavioral modeling

### Continuous Assignments
- A continuous assignment is the most basic statement in dataflow modeling, used to drive a value onto a net. A continuous assignment replaces gates in the description of the circuit and describes the circuit at a higher level of abstraction.
- A continuous assignment statement starts with the keyword `assign`
```
<continious_assign> ::= assign <drive_strength> ? <delay> ? <list_of_assignments>;
```
- The left hand side of an assignment must always be a scalar or vector net or a concatenations of scalars and vector nets. I can not be a scalar or vector register
- Continuous assignments are always active. The assignment expression is evaluated as soon as one of the right hand side operands changes and the value is assigned to the left hand side net
- eg : assign out = i1 & i2 ; // i1 and i2 are nets out is a net
#### Implicit continuous assignment
- Instead of declaring a net and then writing a continuous assignment on the net, Verilog provides a shortcut by which a continuous assignment can be placed on a net when it is declared. There can be only one implicit declaration assignment per net because a net is declared only once.
``` Verilog
// Regular continuous assignment
wire out;
assign out = in1 & in2;

// Same effect is achieved by an implicit continuous assignment
wire out = in1 & in2;
```

### Delays
- Delay values control the time between the change in a right hand side operand and when the new value is assigned to the left hand side.
- Three ways - regular assignment delay, implicit continuous assignment delay and net declaration delay
#### Regular assignment delay
- The delay value is specified after the keyword assign
- Any change in values of in1 and in2 will result in a delay of 10 time units before recomputation of the expression in1 & in2 
- If in1 or in2 changes value again before 10 time units when the result propagates to out , the values in in1 and in2 at the time of recomputation are considered.
- This property is called inertial delay . An input pulse that is shorter than the delay of the assignment statement does not propagate to the output
#### Implicit Continuous assignment delay
- An equivalent method to use and implicit continuous assignment to specify both a delay and an assignment on the net
#### Net Declaration delay
- A delay can be specified on a net when it is declared without putting a continuous assignment on the net. If a delay is specified on a net out , then any value change applied to net out , is delayed accordingly.
- Net declaration delays can also be used in gate level modeling
- eg : wire #10 out;

### Expressions, Operators and Operands
- Dataflow modeling describes the design in terms of expression instead of primitive gates. Expressions, operators, and operands form the basis of dataflow modeling.

### Operators
#### Equality Operators
- logical equality `==`  a equals to b, result unknown if x or z in a or b
- case equality `===` a equals to b , including x and z
#### Bitwise Operators
z is treated as x in bitwise operation
#### Reduction Operators
` and (&) nand(~&) or(|) nor(~|) , xor(^) , xnor(~^,^~) `
#### Concatenation Operator
- The concatenation operator ( { , } ) provides a mechanism to append multiple operands. The operands must be sized . Unsized operands are not allowed because the size of each operand must be known for computation of the size of the result
- Can be thought as like it concating the string
#### Replication Operator
- Repetitive concatenation of the same number can be expressed by using a replication constant.
- Replication_constant{ }
- eg A = 1'b1 ; Y={4{A}} ; // Y is 4'b1111

# Behavioral Modeling
- Verilog Provides designers the ability to describe design functionality in an algorithmic manner. 
- Designer describes the behavior of the circuit. Thus , behavioral modeling represents the circuit at a very high level of abstraction.
### Structured Procedures
- There are two structured procedure statements in Verilog : `always` and `initial`.
- Verilog is a concurrent programming language unlike the C programming language that is sequential in nature
- Each always and initial statement represents a separate activity flow in Verilog. 
- Each activity flow starts at simulation time 0.
- The statements always and initial cannot be nested.
#### initial Statement
- An initial block starts at time 0, executes once during a simulation, and then does not execute again. 
- If there are multiple initial blocks , each block starts to execute concurrently at time 0.
- Each block finishes execution independently of other blocks.
- Multiple behavioral statements must be grouped, typically using the keyword `begin` and `end`
- The initial blocks are typically for initialization , monitoring, waveforms and other processes that must be executed only once during the entire simulation run.
#### always Statement
- The `always` statement starts at time 0 and executes the statements in the always block continuously in a looping fashion.
- The activity is stopped only by power off `$ finish` or interrupt `$ stop`
### Procedural Assignments
- Procedural assignments update values of reg, integer, real or time variables. 
- The value will placed on a variable will remain unchanged until another procedural assignment updates to the variable with a different value.
#### Blocking Assignments
- Blocking assignment statement are executed in the order they are specified in a sequential block. 
- A blocking assignment will not block the execution of statements that follow in a parallel block
#### Nonblocking Assignments
- Nonblocking assignments allow scheduling of assignments without blocking execution of the statement that follow in a sequential block.
- A <= operator is used to specify the nonblocking assignments
#### Advantages of Nonblocking Assignments
- Think simple as the operation in non blocking assignment occurs concurrently
``` Verilog
// in seqnetial block with blocking calls
swap(a,b){
tempa = a;
tempb = b;
a=tempb;
b=tempa;
}

// using nonblocking assignments
a<=b
b<=a
they are scheduled at the same time
first read operation followed by the write operation
```
### Timing Controls
- Timing controls provide a way to specify the simulation time at which procedural statement will execute. There are three methods of timing control : delay-based timing control , event-based timing control and level-sensitive timing control
#### Delay based Timing control
- Delay-based timing control in an expression specifies the time duration between when the statement is encountered and when it is executed.
- Delays are specified by the symbol # .
- Regular delay control
- Intra - assignment control delay
	- y = #5 x+z // take values of x and z at time = 0 , evaluate x+z and then wait 5 time units to assign value to y
- Zero delay control
	- Procedural statements in different always-initial blocks may be evaluated a the same simulation time . The order of execution of these statements in different always-initial blocks is nondeterministic. Zero delay control is a method to ensure that a statement is executed last, after all other statements in that simulation time are executed
``` Verilog
inital 
begin 
#0 x=1;
#0 y=1;
end
```
#### Event based timing control
- An event is the change in the value on a register or a net . Events can be utilized to trigger execution of a statement or a block of statements.
- There are four types of event based timing control
- Regular event control
	- The @ symbol is used to specify an event control. Statements can be executed on changes in signal value or at a positive or negative transition of the signal value
- Named event control 
	- Verilog provides the capability to declare an event and then trigger and recognize the occurence of that event
``` Verilog
event e
always @(posedge clock)
begin
	if(last_data_packet)
		->e;
end

always @(e)
begin
...
end
```
- Event OR control
	- Sometimes a transition on any one of multiple signals or events can trigger the execution of a statements or a block of statements.
	- eg always @( reset or clock or d )
#### Level Sensitive Timing Control
- Verilog also allows level sensitive timing control , that is , the ability to wait for certain condition to be true before a statement or a block of statement is executed.
- The keyword `wait` is used for level sensitive constructs
``` Verilog
always
	wait(count_enable) #20 count = count+1;
```

### casex, casez keywords
- casez treats all z values in the case alternatives to the case expression as don't care.
- casex treats all x and z values in the case item or the case expression as don't care.
### Loops
- 4 types of looping statements in verilog
- All looping statements can appear only inside an initial or always block
#### while loop 
- Similar to C
#### for loop
- similar to C
#### repeat loop
- Repeat x number of times where x must be a number
#### forever loop
- runs forever until the `$ finish` task is encountered
- A forever loop can be exited by use of `disable` statement
### Sequential and Parallel Blocks
- Block statements are used to group multiple statements to act together as one.
#### Block Types
- Sequential Blocks
	- The keyword begin and end are used to group statements into sequential blocks 
	- The statements in a sequential block are processed in the order they are specified.
	- If delay or event control is specified , it is relative to the simulation time when the previous statement in the block completed execution
- Parallel Blocks
	- Parallel blocks specified by keywords `fork` and `join`.
	- Statements in a parallel blocks are executed concurrently
	- Ordering of statements is controlled by the delay or event control assigned to each statement
	- If delay or event control is specified, it is relative to the time the block was entered
	- All statements start at simulation time 0. The order in which the statements will execute is not known. Which introduces race condition among the statements and ultimately leads to non-deterministic output
	- The keyword fork can be viewed as splitting a single flow into independent flows
	- The keyword join can be seen as joining the independent flows back into a single flow.
#### Special Features of Blocks
- Nested blocks
	- Sequential and parallel blocks can be mixed / nested.
- Named blocks
	- Local variables can be declared for the named block.
	- Variables in a named block can be accessed by using hierarchical name referencing 
	- Named blocks can be disabled, i.e., their execution can be stopped