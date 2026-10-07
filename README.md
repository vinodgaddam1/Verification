# 🔬 Chapter 1 — Verification Guidelines

## 📌 1.1.2 The Verification Plan

A **Verification Plan** defines what needs to be verified, how it will be verified, and how we will determine whether the design is sufficiently tested.

### 🧪 Main Verification Techniques

🔹 **Directed Testing**
Specific test scenarios are created to verify known and important behaviors.

🔹 **Random Testing**
Inputs are generated randomly to explore a wider range of possible scenarios and uncover unexpected bugs.

🔹 **Assertions**
Assertions continuously check whether specific design properties or rules are satisfied during simulation.

### 💡 Simple Examples

**Example 1 — Directed Test:**
For a FIFO, explicitly write data until it becomes **FULL**, then verify that another write is rejected.

**Example 2 — Random Test:**
Generate random **read/write operations** and compare the DUT output against a reference model.

🎯 A good verification plan combines multiple techniques rather than relying on only one.

---

# 📚 1.2 The Verification Methodology Manual (VMM)

The **Verification Methodology Manual (VMM)** introduced a structured approach to developing reusable and scalable verification environments.

🔹 VMM techniques were originally developed for use with the **OpenVera** language.

🔹 In **2005**, these techniques were extended for **SystemVerilog**.

🔹 VMM was preceded by the **Reference Verification Methodology (RVM)** for Vera.

### 🔗 Key Point

VMM helped establish systematic verification practices such as:

* 🧩 Reusable verification components
* 🧪 Constrained-random testing
* 📊 Functional coverage
* 🔍 Structured test environments
* 🎯 Scalable verification methodologies

### 💡 Why Methodologies Matter

Without a methodology, a large verification environment can become difficult to maintain and reuse.

**Example 1:**
A reusable bus verification component can be used across multiple projects.

**Example 2:**
A standardized test structure makes it easier for multiple verification engineers to work on the same project.

🚀 **Next:** Understanding how verification methodologies evolved toward modern **SystemVerilog/UVM-based verification**.

# 🔬 1.3 Basic Testbench Functionality

The primary purpose of a **testbench** is to determine the **correctness of the Design Under Test (DUT)**.

A testbench accomplishes this through the following steps:

### 🧪 Basic Testbench Steps

**1️⃣ Generate Stimulus**
Create input transactions that exercise the DUT.

**2️⃣ Apply Stimulus to the DUT**
Drive the generated inputs into the DUT.

**3️⃣ Capture the Response**
Observe and collect the DUT's outputs.

**4️⃣ Check for Correctness**
Compare the actual response with the expected response and identify errors.

**5️⃣ Measure Progress Against Verification Goals**
Determine how much of the design functionality has been exercised and whether the verification objectives are being achieved.

---

### ⚙️ Automatic vs Manual Tasks

Not every verification activity is performed automatically.

🔹 Some steps can be **automated by the testbench**, such as stimulus generation, monitoring, and checking.

🔹 Other decisions are **manually determined by the verification engineer**, such as defining scenarios, expected behavior, and verification goals.

📌 **The verification methodology you choose determines how these activities are structured and carried out.**

-----------------------------------------------------------------------------------------------------------------

### 💡 Example 1 — ALU

`Generate → Apply → Capture → Check`

For an ALU, the testbench may:

* 🎯 Generate random operands and operations
* 📥 Apply them to the ALU
* 📤 Capture the result
* 🔍 Compare it with a reference model
* 📊 Track which operations have been verified

### 💡 Example 2 — FIFO

For a FIFO, the testbench may:

* 📝 Generate read/write transactions
* 📥 Apply them to the FIFO
* 👀 Monitor output data and status flags
* 🔍 Compare read data against expected data
* 📊 Track coverage of **FULL, EMPTY, READ, and WRITE** scenarios

### 📌 Key Takeaway

> **Generate → Apply → Capture → Check → Measure**

-----------------------------------------------------------------------------------------------------------------

📌 1.4 Directed Testing

Directed testing is a verification approach where you study the hardware specification and create a verification plan containing a list of specific tests.

Each test focuses on a particular set of related features of the DUT.
<img width="797" height="327" alt="Screenshot 2026-09-06 222210" src="https://github.com/user-attachments/assets/eeba16a3-bad4-4890-8e12-85e7039de0eb" />

<img width="860" height="411" alt="Screenshot 2026-09-06 222611" src="https://github.com/user-attachments/assets/706da15a-099c-4d50-9a6a-16544a4178ad" />



🎯 Basic Approach

Specification → Verification Plan → Test Cases → DUT → Check Results

🔹 Identify the features from the specification.
🔹 Create specific test cases for those features.
🔹 Apply the required stimulus.
🔹 Check whether the DUT behaves correctly.

💡 Example 1 — UART

Suppose the UART specification has:

Start-bit detection
8-bit data transmission
Parity
Stop-bit detection

You could create separate directed tests:

🧪 Test 1 → Verify start-bit detection
🧪 Test 2 → Verify different data patterns
🧪 Test 3 → Verify parity
🧪 Test 4 → Verify stop-bit detection
💡 Example 2 — FIFO

For a FIFO, directed tests could target:

🧪 Write until FULL
🧪 Read until EMPTY
🧪 Attempt write when FULL
🧪 Attempt read when EMPTY
📊 Directed vs Random Testing

In the first image, the dashed line represents random testing and the solid line represents directed testing.

The important idea is that random testing can reach different coverage points quickly, while directed testing progresses through explicitly planned scenarios.

📌 Key Point:
Directed testing is predictable and targeted, but writing enough directed tests for a complex design can become time-consuming.


1.4.1 Constrained-Random Stimulus:
Although you want the simulator to generate the stimulus, you don’t want totally random values. You use the SystemVerilog language to describe the format of the stimulus (“address is 32-bits; opcode is ADD, SUB or STORE; length < 32 bytes”), and the simulator picks values that meet the constraints.

<img width="807" height="738" alt="Screenshot 2026-09-06 222501" src="https://github.com/user-attachments/assets/a9d8ac58-2f8b-4af1-b3fa-9b6c3bb58588" />

-----------------------------------------------------------------------------------------------------------------
 
📌 1.5 Methodology Basics

🔹 1. Constrained-Random Stimulus 🎲

🔹 2. Functional Coverage 📊

🔹 3. Layered Testbench Using Transactors 🧩

🔹 4. Common Testbench for All Tests ♻️

🔹 5. Keep Test-Specific Code Separate 🧩

📌 Key Takeaway:

A good verification methodology is not just about finding bugs. It is about creating a reusable and measurable process for demonstrating that the DUT meets its specification.

-----------------------------------------------------------------------------------------------------------------

📌 1.6 What Should You Randomize?

🔹 1. Device Configuration ⚙️

🔹 2. Environment Configuration 🌐

🔹 3. Input Data 📥

🔹 4. Protocol Exceptions ⚠️

🔹 5. Errors and Violations 🚨

🔹 6. Delays ⏱️

📌 Key Takeaway

Don't simply randomize everything.

The useful strategy is:

🎲 Randomize → 🔒 Constrain → 🧪 Stimulate → 🔍 Check → 📊 Measure Coverage

-----------------------------------------------------------------------------------------------------------------

🔬 1.7 The Testbench — Design Environment

The testbench wraps around the Design Under Test (DUT), similar to how a hardware tester connects to a physical chip.
           🧪 TESTBENCH
       
  🎯 Basic Testbench Function

The testbench performs two main activities:

📥 Provide Stimulus → Sends inputs to the DUT
📤 Capture Responses → Observes and checks DUT outputs    


-----------------------------------------------------------------------------------------------------------------

📌 1.8 Testbench Components — Bus Functional Models (BFMs)

   A testbench can contain multiple Bus Functional Models (BFMs).
   For example,
     🔵 AMBA
     🟢 USB
     🟠 PCI
     🟣 SPI

📌 Key Takeaway

Testbench = More than just stimulus

A well-structured testbench can contain:

🎯 Tests → 📦 Transactions → 🔄 Transactors/BFMs → 🔌 DUT Interface → 🔍 Monitors → 📊 Checkers

-----------------------------------------------------------------------------------------------------------------

 💡 A Flat Testbench :
When you fi rst learned Verilog and started writing tests, they probably looked like the low-level code inSample  1.1  , which does a simplifi ed APB (AMBA Peripheral Bus) Write. (VHDL users may have written similar code). 


🧪 Sample 1.1 — Driving the APB Pins

This example demonstrates a basic low-level Verilog testbench that directly drives APB signals, performs a write operation, and checks the result.

module test(PAddr, PWrite, PSel, PWData, PEnable, Rst, clk);

    // Port declarations omitted...

    initial begin

        // 🔄 Drive reset
        Rst <= 0;
        #100 Rst <= 1'b1;

        // 🎯 Drive the APB control bus
        @(posedge clk);
        PAddr  <= 16'h50;
        PWData <= 32'h50;
        PWrite <= 1'b1;
        PSel   <= 1'b1;

        // ⏱️ Enable APB access
        @(posedge clk);
        PEnable <= 1'b1;

        @(posedge clk);
        PEnable <= 1'b0;

        // 🔍 Check the result
        if (top.mem.memory[16'h50] == 32'h50)
            $display("Success");
        else
            $display("Error, wrong value in memory");

        $finish;
    end

endmodule
📌 Description
🔄 Reset: Initializes the DUT into a known state.
🎯 APB Control Bus: Drives address, data, write, and select signals.
⏱️ PEnable: Enables the APB access for one clock cycle.
🔍 Result Check: Verifies that 32'h50 was correctly written to address 16'h50.
🛑 $finish: Ends the simulation.

👉 Key Point: This is pin-level testing, where the testbench directly controls the DUT's interface signals.

-----------------------------------------------------------------------------------------------------------------


🧪 Sample 1.2 — Task to Drive APB Pins

A task is used to make APB write operations reusable.

task write(reg [15:0] addr, reg [31:0] data);
    @(posedge clk);
    PAddr  <= addr;
    PWData <= data;
    PWrite <= 1'b1;
    PSel   <= 1'b1;

    @(posedge clk);
    PEnable <= 1'b1;

    @(posedge clk);
    PEnable <= 1'b0;
endtask

📌 Key Point:
Instead of driving APB pins repeatedly, simply call:

write(16'h50, 32'hABCD);

👉 Task = Reusable APB write operation.

-----------------------------------------------------------------------------------------------------------------

🧪 Sample 1.3 — Low-Level Verilog Test

This example shows a simple Verilog test using the tasks from Sample 1.2.

🔹 Test Flow
Reset → Write Data → Check Result → Finish
🔄 reset() → Resets the DUT.
✍️ write(16'h50, 32'h50) → Writes data into memory.
🔍 Checks whether memory location 16'h50 contains 32'h50.
✅ Match → Success
❌ Mismatch → Error
🛑 $finish → Ends simulation.

📌 Key Point:
Sample 1.3 is called a low-level Verilog test because the test still directly depends on Verilog tasks and DUT-level details.

👉 Sample 1.1: Directly drives APB pins
👉 Sample 1.2: Encapsulates pin driving into a task
👉 Sample 1.3: Uses the task to create a complete test case


🔌 The Signal and Command Layers

📌 1. Signal Layer

📌 2. Command Layer

🚗 Driver → Converts commands into DUT input signals.
👀 Monitor → Observes DUT output signals and groups them into commands.
🎯 Assertions → Check individual signals and behavior across complete commands.

<img width="757" height="217" alt="Screenshot 2026-09-06 221110" src="https://github.com/user-attachments/assets/c3f03809-c96a-4492-9f66-993ab00d8053" />

🔬 Figure 1.10 — Testbench with Functional Layer
The Functional Layer is added above the Command and Signal layers to work with high-level functionality.

📌 Functional Layer Components
⚙️ Agent → Connects the functional layer with the command layer.
📊 Scoreboard → Compares expected results with actual results.
🔍 Checker → Determines whether the DUT behavior is correct.

<img width="805" height="305" alt="Screenshot 2026-09-06 221328" src="https://github.com/user-attachments/assets/8e8aa154-e574-4065-aebf-19d7b017db1a" />


🎯 The Scenario Layer
The Scenario Layer is the highest layer of the testbench. It is driven by the Generator and defines complete, realistic operations that the DUT should perform.

📌 What is a Scenario?

A scenario is a sequence of operations that represents a particular use case or task.

For example, in a music player:

🎵 Play music from storage
📥 Download a new song
🔊 Adjust volume
⏩ Change tracks
<img width="777" height="350" alt="Screenshot 2026-09-06 221430" src="https://github.com/user-attachments/assets/841d3c96-1c79-4c27-8144-20ba74f9c087" />


🔬 Fig. 1.12 — Full Testbench with All Layers

This figure shows a complete layered testbench, including the Scenario, Functional, Command, and Signal layers.

📌 Main Components
🧪 Test → Starts and controls the verification scenario.
🎯 Generator → Generates scenarios/transactions.
⚙️ Agent → Connects the generator to the lower-level components.
🚗 Driver → Converts transactions into DUT signals.
🔍 Assertions → Check signal-level and protocol behavior.
👀 Monitor → Observes DUT signals and collects responses.
📊 Scoreboard → Compares expected and actual results.
✅ Checker → Determines whether the DUT behavior is correct.
📈 Functional Coverage → Measures which required functionality has been exercised.
<img width="835" height="400" alt="Screenshot 2026-09-06 221554" src="https://github.com/user-attachments/assets/a5169279-cce0-4f7a-9e0e-6cd9568cecb7" />


🧪 Exercise 1 — ALU Verification Plan
📌 DUT Specifications
🔄 Reset: Asynchronous, active HIGH
⏱️ Clock: Input clock
📥 A: 4-bit signed input
📥 B: 4-bit signed input
📤 C: 5-bit signed registered output
⚙️ C updates: Positive edge of clock
🔢 Opcodes: 4 operations

solution:
module alu (
    input  logic clk,
    input  logic reset,
    input  logic signed [3:0] A,
    input  logic signed [3:0] B,
    input  logic [1:0] opcode,
    output logic signed [4:0] C
);

    always_ff @(posedge clk or posedge reset) begin
        if (reset)
            C <= 5'sd0;
        else begin
            case (opcode)
                2'b00: C <= A + B;
                2'b01: C <= A - B;
                2'b10: C <= ~A;
                2'b11: C <= |B;
            endcase
        end
    end

endmodule


module alu_tb;

    logic clk;
    logic reset;
    logic signed [3:0] A, B;
    logic [1:0] opcode;
    logic signed [4:0] C;

    // Opcode definitions
    localparam ADD    = 2'b00;
    localparam SUB    = 2'b01;
    localparam INV    = 2'b10;
    localparam RED_OR = 2'b11;

    // DUT
    alu dut (
        .clk    (clk),
        .reset  (reset),
        .A      (A),
        .B      (B),
        .opcode (opcode),
        .C      (C)
    );

    // Clock generation
    always #5 clk = ~clk;

    initial begin
        clk   = 0;
        reset = 0;
        A     = 0;
        B     = 0;
        opcode = ADD;

        // Asynchronous active-high reset
        #2 reset = 1;
        #2 reset = 0;

        // ADD
        A = 4'sd5;
        B = 4'sd3;
        opcode = ADD;
        @(posedge clk);
        #1 $display("ADD: A=%0d B=%0d C=%0d", A, B, C);

        // SUB
        A = 4'sd7;
        B = 4'sd3;
        opcode = SUB;
        @(posedge clk);
        #1 $display("SUB: A=%0d B=%0d C=%0d", A, B, C);

        // INVERT A
        A = 4'b1010;
        opcode = INV;
        @(posedge clk);
        #1 $display("INV: A=%b C=%b", A, C);

        // REDUCTION OR B
        B = 4'b0001;
        opcode = RED_OR;
        @(posedge clk);
        #1 $display("RED_OR: B=%b C=%b", B, C);

        $finish;
    end

endmodule

-----------------------------------------------------------------------------------------------------------------
📘 Chapter 2 — SystemVerilog Data Types

SystemVerilog provides improved data types and data structures for better performance, less memory, and easier verification.

🔹 Key Features
⚡ Two-State Types → bit, int → better performance & less memory
📦 Queues → Variable-size storage with built-in push/pop
📊 Dynamic Arrays → Size decided at runtime
🔑 Associative Arrays → Key-based storage & searching
🏗️ Classes & Structures → Organize complex data
🔄 Unions & Packed Structures → Multiple views of same data
📝 Strings → Built-in text handling
🔢 Enumerated Types → Readable and meaningful values
🎯 Main Benefit

SystemVerilog = Flexible + Efficient + Verification-friendly data structures 🚀

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

📘 2.1 — Built-In Data Types

SystemVerilog provides several built-in data types for storing different kinds of data.

🔹 Main Categories
🔢 Integer Types → bit, logic, reg, int, integer
🔤 String Type → string
🔢 Enumerated Type → enum
📦 Structure Type → struct
🔄 Union Type → union
⭐ Important Classification

2-State:
bit, byte, shortint, int, longint

➡️ Stores only 0 and 1 ⚡

4-State:
logic, reg, integer, time

➡️ Stores 0, 1, X, Z 🔬

🎯 Remember

2-state → 0, 1
4-state → 0, 1, X, Z

int i;           // 32-bit, 2-state, signed
int unsigned ui; // 32-bit, 2-state, unsigned

byte b8;         // 8-bit signed
shortint s;      // 16-bit signed
longint l;       // 64-bit signed

integer i4;      // 32-bit, 4-state signed
time t;          // 64-bit, 4-state unsigned
real r;          // floating-point

| Type           | States  |                  Size | Signed?    |
| -------------- | ------- | --------------------: | ---------- |
| `bit`          | 2-state |                 1 bit | ❌ Unsigned |
| `bit [31:0]`   | 2-state |                32 bit | ❌ Unsigned |
| `int unsigned` | 2-state |                32 bit | ❌ Unsigned |
| `int`          | 2-state |                32 bit | ✅ Signed   |
| `byte`         | 2-state |                 8 bit | ✅ Signed   |
| `shortint`     | 2-state |                16 bit | ✅ Signed   |
| `longint`      | 2-state |                64 bit | ✅ Signed   |
| `integer`      | 4-state |                32 bit | ✅ Signed   |
| `time`         | 4-state |                64 bit | ❌ Unsigned |
| `real`         | 2-state | 64-bit floating point | —          |

🧠 Easy Memory Trick
2-state: 0, 1 ⚡
4-state: 0, 1, X, Z 🔬
Signed: Can represent ➕ positive and ➖ negative numbers.

<img width="762" height="193" alt="Screenshot 2026-09-07 220434" src="https://github.com/user-attachments/assets/bddd2335-58ca-45e1-aa89-9797bd2cdec6" />
<img width="755" height="210" alt="Screenshot 2026-09-07 220427" src="https://github.com/user-attachments/assets/aac9e4c7-5c8e-461f-aa47-3820c6ad7b16" />

📘 2.2 Fixed-Size Arrays
Fixed-size array = Array whose size is known at compile time and cannot change during simulation. 📦

<img width="547" height="122" alt="Screenshot 2026-09-07 220720" src="https://github.com/user-attachments/assets/7d381a81-1b6d-410c-b125-fc28a83a11c2" />

SystemVerilog has the  $clog2()  function that calculates the ceiling of log base 2, 

<img width="756" height="165" alt="Screenshot 2026-09-07 220831" src="https://github.com/user-attachments/assets/b009416b-eb9f-4618-946d-f1bab41e5f3c" />
<img width="730" height="142" alt="Screenshot 2026-09-07 220906" src="https://github.com/user-attachments/assets/56a3e152-3e92-4d62-9827-09a8f91b11af" />
<img width="782" height="267" alt="Screenshot 2026-09-07 221000" src="https://github.com/user-attachments/assets/166e125a-4a02-47c1-9e1a-d89e2d599ff2" />

📘 2.2.2 — Array Literal

An array literal is a way to initialize an array with values directly using '{' and '}'. 🧩
<img width="807" height="276" alt="Screenshot 2026-09-07 221121" src="https://github.com/user-attachments/assets/a45a9512-ea02-40c3-8b9a-7d6f1d323f8a" />

<img width="743" height="225" alt="Screenshot 2026-09-07 221137" src="https://github.com/user-attachments/assets/2541223f-c491-41ec-a7a5-d856224c0fac" />

📘 2.2.3 — Basic Array Operations: for & foreach
Both for and foreach are used to access array elements. 🔢

 <img width="823" height="335" alt="Screenshot 2026-09-07 221239" src="https://github.com/user-attachments/assets/b55d63e4-ff62-4ee4-be3d-b265bafe5d7f" />

 <img width="832" height="348" alt="Screenshot 2026-09-07 221259" src="https://github.com/user-attachments/assets/28c2c09a-75d1-4263-b73f-37b0bcd33ff5" />

 <img width="788" height="397" alt="Screenshot 2026-09-07 221324" src="https://github.com/user-attachments/assets/fe80d73e-451d-47f1-b5ae-89fc9f2419c2" />
 
<img width="837" height="726" alt="Screenshot 2026-09-07 221413" src="https://github.com/user-attachments/assets/2878ac1a-41d5-46d4-9d34-5f45e1aa15e9" />

📘 Basic Array Operations — Copy & Compare

<img width="811" height="618" alt="Screenshot 2026-09-07 222207" src="https://github.com/user-attachments/assets/783d992e-d76b-422c-8414-3835026f5627" />


📘 Bit and Array Subscripts — Together at Last

SystemVerilog allows you to combine bit/part-selects with array indexes. 🔢

<img width="740" height="205" alt="Screenshot 2026-09-07 222702" src="https://github.com/user-attachments/assets/b46a9e35-f353-4b9e-9c9c-f6f6c64df080" />

Verilog-2001 Improvement — Double Comma in $display

This is a small but useful improvement in Verilog-2001. 🛠️

🔹 Double Comma ,,

In a $display statement, using two commas inserts a space in the output.

Example 1️⃣
$display("Hello",,"World");

Output:

Hello World
Example 2️⃣
int a = 10;
int b = 20;

$display("a =",a,,"b =",b);

📘 2.2.6 — Packed Arrays

A packed array is a collection of bits stored continuously next to each other in memory. 🔢

<img width="842" height="565" alt="Screenshot 2026-09-07 222922" src="https://github.com/user-attachments/assets/12497485-95ec-48a6-962a-627dac5fa80c" />


<img width="823" height="452" alt="Screenshot 2026-09-07 223026" src="https://github.com/user-attachments/assets/857d5509-c192-4b20-9fbf-9684e94ef717" />


 With a single subscript, you get a word of data,  barray[0] .With two subscripts, you get a byte of data,  barray[0][3] . With three subscripts, you can access a single bit,  barray[0][1][6] . Because one dimension is specifi ed after the name, barray[5] , that dimension is unpacked, so you must always give at least one subscript. 

📘 2.2.8 — Choosing Between Packed and Unpacked Arrays

The choice depends on what you want the array to represent. 🔢

🔹 Waiting for Array Changes

The @ operator can be used with scalar values and packed arrays.

For example:

logic [7:0] barray[4];

@(barray[0]);  // ✅ Legal

But:

@(barray);     // ❌ Not legal

because barray is an unpacked array.

To wait for any element of the unpacked array to change:

@(barray[0] or barray[1] or
  barray[2] or barray[3]);
🧠 Remember
🔢 Packed array → useful for scalar conversion and @ event control.
📦 Unpacked array → useful for storing separate elements/memory.
⏳ @ works with scalars and packed arrays, not an entire unpacked array.


📘 2.3 — Dynamic Arrays

 A dynamic array is an array whose size can be decided and changed at runtime. 🔄

 A dynamic array is declared with empty word subscripts  [] . This means that you do not specify the array size at compile time; instead, give it at run time. The array is initially empty, so you must call the  new[]  constructor to allocate space, passing in the number of entries in the square brackets. If you pass an array name to the  new[]  constructor, 

 <img width="820" height="368" alt="Screenshot 2026-09-07 225153" src="https://github.com/user-attachments/assets/79f4f71d-8c9c-485f-b353-3a21a6749a1f" />


<img width="757" height="356" alt="Screenshot 2026-09-07 225444" src="https://github.com/user-attachments/assets/471c39d5-c0cd-415d-832a-e5da7b61126f" />

<img width="797" height="447" alt="Screenshot 2026-09-07 225547" src="https://github.com/user-attachments/assets/4890db2c-2edb-4416-a98d-8621581cfa49" />


📘 2.4 — Queues

A queue is a variable-size array that stores elements in a specific order. 📦A queue is declared with word subscripts containing a dollar sign:  [$] . The elements of a queue are numbered from 0 to $


if you put a $ on the left side of a range, such as  [$:2] , the  $  stands for the minimum value,  [0:2] . A  $  on the right side, as in  [1:$] , stands for the maximum value,  [1:2] 

<img width="802" height="485" alt="Screenshot 2026-09-07 231132" src="https://github.com/user-attachments/assets/19661791-c6be-47d1-917c-82a34f87111d" />

<img width="857" height="617" alt="Screenshot 2026-09-07 231238" src="https://github.com/user-attachments/assets/ff78d2de-4452-4caa-a2f2-518946e06190" />

📘 Chapter 2.5 — Associative Arrays in SystemVerilog 🔬
🧠 1. What is an Associative Array?

An Associative Array is an unpacked array where elements are accessed using a key/index instead of a fixed size. 🔑

It is useful when:

📌 You don't know the number of elements in advance.
🔑 You want to access data using meaningful keys.
💾 You want to avoid allocating unused memory.
✍️ Syntax
data_type array_name [index_type];

<img width="797" height="181" alt="Screenshot 2026-09-08 220016" src="https://github.com/user-attachments/assets/da33f280-2e55-4d84-9b99-3442077d9e6b" />

<img width="801" height="357" alt="Screenshot 2026-09-08 222130" src="https://github.com/user-attachments/assets/3cf2ea5a-1e0a-4b43-9153-e2687f617c1d" />

<img width="786" height="762" alt="Screenshot 2026-09-08 222120" src="https://github.com/user-attachments/assets/a9235c64-05eb-4e6c-b2ae-ed6b0b048b45" />

<img width="802" height="626" alt="Screenshot 2026-09-08 222107" src="https://github.com/user-attachments/assets/e476746c-10f0-4b11-9c8c-6a5dc26c160d" />

📘 Chapter 2.6 — Array Methods in SystemVerilog 🔬
SystemVerilog provides built-in array methods to search, sort, locate, count, and manipulate array elements. 🛠️

🧩 1. Types of Array Methods

Array methods can be broadly divided into:

Category	Methods
🔍 Searching	find(), find_index(), find_first(), find_last()
🔢 Counting	sum(), count()
📊 Sorting	sort(), rsort()
🔀 Ordering	reverse(), shuffle()
🧮 Reduction	sum(), product(), and(), or(), xor()
📦 Size/Manipulation	size(), delete()

<img width="795" height="637" alt="Screenshot 2026-09-08 222408" src="https://github.com/user-attachments/assets/2b274532-1bdb-4186-8e41-82baacdc3648" />

<img width="752" height="390" alt="Screenshot 2026-09-08 222948" src="https://github.com/user-attachments/assets/a9a4a978-7ad2-42a7-afa9-e57271e82162" />

<img width="791" height="593" alt="Screenshot 2026-09-08 223042" src="https://github.com/user-attachments/assets/f0aeddb2-3a6c-436c-b23f-6cab8c1a9726" />

<img width="802" height="531" alt="Screenshot 2026-09-08 223154" src="https://github.com/user-attachments/assets/d4c6a8c3-6a2c-4c30-bcf0-4fd7532a9c4a" />

<img width="798" height="441" alt="Screenshot 2026-09-08 224800" src="https://github.com/user-attachments/assets/a7027785-cf3d-4eb1-ae45-1d0843f752cb" />

<img width="721" height="172" alt="Screenshot 2026-09-08 224752" src="https://github.com/user-attachments/assets/a2e327dd-5eae-435a-9919-f46e598befa2" />

<img width="796" height="692" alt="Screenshot 2026-09-08 225554" src="https://github.com/user-attachments/assets/d09718fb-d76b-49fa-9566-b33747c1c5d6" />

<img width="827" height="423" alt="Screenshot 2026-09-08 225544" src="https://github.com/user-attachments/assets/e9709ef9-92e5-4071-9936-fb22686f14d5" />

📘 2.6.3 — Array Sorting and Ordering 🔢

SystemVerilog provides built-in methods to sort, reverse, and randomly rearrange array elements. These methods are very useful in verification for organizing transactions and test data. 🧪

The main methods are:

Method	Purpose
sort()	⬆️ Ascending order
rsort()	⬇️ Descending order
reverse()	🔄 Reverse existing order
shuffle()	🎲 Randomly rearrange

<img width="788" height="345" alt="Screenshot 2026-09-08 230123" src="https://github.com/user-attachments/assets/d541863f-fc24-4b88-9702-44586b80682f" />

<img width="800" height="247" alt="Screenshot 2026-09-08 230114" src="https://github.com/user-attachments/assets/3aa695aa-3792-40f0-99bd-7b12f0d344f8" />


#SYSTEMVERILOG ASSIGNMENT
<img width="1167" height="767" alt="Screenshot 2026-09-30 183811" src="https://github.com/user-attachments/assets/5582fafc-8d3b-45e1-94cd-4d5b77da078a" />

Answers:


a. Byte in systemVerilog is 8-bit signed by default
-128 to +127

b. my_integer = 32’b0000_1111_xxxx_zzzz;
my_int = my_integer;
binary = 0000_0000_0000_0000_0000_1111_0000_0000
hex = 00000f00

c. my_bit =16’h8000;
16'h8000 = 1000 0000 0000 0000  2^15 = 32768

d.my_short_int1 = my_bit;
binary = 0000_1000_0000_0000  =  decimal 2048

c. my_short_int2 = my_short_int1 - 1;
binary in 2’complement form = 0111_1111_1111_1111
 decimal = 32767

 <img width="1087" height="791" alt="Screenshot 2026-10-01 184043" src="https://github.com/user-attachments/assets/a58cbe2e-a597-4851-a40f-d38da728731e" />
module top;

  bit [7:0] my_mem[3];
  
  logic [3:0] my_logicmem[4];
  
  logic [3:0] my_logic;

  initial begin
    
  my_mem  = '{default : 8'hA5};
  
  my_logicmem =  '{0,1,2,3};
  
  my_logic = 4'hf;
  
  my_mem[2]  =  my_logicmem[4];
    
    
    // a. mem_mem[2] = my_logicmem[4]
    $display("%p",my_mem); //decimal
    $display("%0h", my_mem[0]);
    $display("%0h", my_mem[1]);
    $display("%0h", my_mem[2]);
    
    
    
    //b. my_logic  = my_logicmem[4]
    my_logic  = my_logicmem[4];
    $display("%p",my_logic);
    
    
    
    //c. my_logicmem[3]  = my_mem[3]
    my_logicmem[3]  = my_mem[3];
    $display("%p",my_logicmem);
    
    
     //d. my_mem[3]  = my_logic
     my_mem[3]  = my_logic;
     $display("%p",my_mem);
    
    //e. my_logic  = my_logicmem[1];
     my_logic  = my_logicmem[1];
    $display("%p",my_logic);
    
    
    //f. my_logic  = my_mem[1];
    my_logic  = my_mem[1];
    $display("%p",my_logic);
    
    
    
    //g. my_logic  = my_logicmem[my_logicmem[41]];
    my_logic  = my_logicmem[my_logicmem[41]];
    $display("%p",my_logic);
    
  end
endmodule


<img width="1040" height="482" alt="Screenshot 2026-10-02 182635" src="https://github.com/user-attachments/assets/4f1cece4-bea6-4bc4-8766-fb58ca1208ac" />

//Complete Code:

module top;

  // a. 2-state array holding four 12-bit values
  bit [11:0] my_array [0:3];

  initial begin

    // b. Initialize the array
    my_array[0] = 12'h012;
    my_array[1] = 12'h345;
    my_array[2] = 12'h678;
    my_array[3] = 12'h9AB;


    // c. Traverse using for loop
    $display("Using FOR loop:");

    for (int i = 0; i < 4; i++) begin
      $display("my_array[%0d] = %03h, bits[5:4] = %02b",
               i, my_array[i], my_array[i][5:4]);
    end


    // c. Traverse using foreach loop
    foreach (my_array[i]) begin
      $display("my_array[%0d] = %03h, bits[5:4] = %02b",
               i, my_array[i], my_array[i][5:4]); //%03h this is means I want 3 – digits with hex 
    end
  end
endmodule


<img width="1107" height="353" alt="Screenshot 2026-10-03 191434" src="https://github.com/user-attachments/assets/5867b059-8349-4941-9f51-64d4869ed040" />


Code:

module array_example;

    // 5 x 31 multi-dimensional unpacked array
    // Each element is a 4-state value
    logic my_array1 [5][31];

    initial begin

        // =====================================================
        // (a) Check the assignments
        // =====================================================

        // Legal assignment
        my_array1[4][30] = 1'b1;

        // Illegal: index 29 is outside first dimension (0 to 4)
        // my_array1[29][4] = 1'b1;

        // Illegal: my_array1[4] is an unpacked array of 31 elements,
        // but 32'b1 is a 32-bit packed value.
        // my_array1[4] = 32'b1;


        // =====================================================
        // (b) Draw / display my_array1
        // =====================================================

        $display("\nArray contents:");

        for (int i = 0; i < 5; i++) begin

            $write("Row %0d: ", i);

            for (int j = 0; j < 31; j++) begin
                $write("%b ", my_array1[i][j]);
            end

            $display();
        end


        // Display the position containing 1
        $display("\nNon-zero element:");
        $display("my_array1[4][30] = %b", my_array1[4][30]);

    end

endmodule

<img width="1167" height="327" alt="Screenshot 2026-10-04 175157" src="https://github.com/user-attachments/assets/2f078813-e801-4b15-b979-52a14b23f40f" />
Code:
 
For Example:
module packed_array_example;

    // 5 × 31 packed 2-state array
    bit [4:0][30:0] my_array2;

    initial begin

        // 1. Legal: [4] is within 0:4, [30] within 0:30
        my_array2[4][30] = 1'b1;

        // 2. Illegal: first dimension is only 0 to 4
        // my_array2[29][4] = 1'b1;

        // 3. Legal: my_array2[3] selects the entire 31-bit slice
        // 32'b1 is truncated to 31 bits
        my_array2[3] = 32'b1;

        // Display
        $display("my_array2[4][30] = %b", my_array2[4][30]);
        $display("my_array2[3]    = %b", my_array2[3]);

    end

endmodule


<img width="855" height="510" alt="Screenshot 2026-10-05 191017" src="https://github.com/user-attachments/assets/80e2a354-0326-4930-acda-14723ccf5e92" />

 

Answer:
Street[0] = Tejon
Street[2] = Platte
Street[2] = Bijou
pop_back = Boulder
street.size = 4

<img width="905" height="383" alt="Screenshot 2026-10-06 185651" src="https://github.com/user-attachments/assets/4d8fe768-f598-4757-8d72-91b1c5912191" />
Key points
Word width: 24 bits → logic [23:0]
Address width: \(2^{20}\) words → 20-bit address → logic [19:0]
Reset PC: 0
Program starts: 20'h00400
Maximum address: \(2^{20}-1 = 20'hFFFFF\)
ISR: 20'hFFFFF
Only 4 memory locations are actually occupied, so an associative array is appropriate.

 Answers:
module associative_memory;

  // 24-bit word
  // 20-bit address
  logic [23:0] memory [logic [19:0]];

  // Addresses
  localparam logic [19:0] RESET_PC  = 20'h00000;
  localparam logic [19:0] MAIN_CODE = 20'h00400;
  localparam logic [19:0] ISR_ADDR  = 20'hFFFFF;

  initial begin

  
    // Fill memory with instructions
    // Reset address 0: Jump to main code at 0x400
    memory[RESET_PC] = 24'hA50400;

    // Main program
    memory[20'h00400] = 24'h123456;
    memory[20'h00401] = 24'h789ABC;

    // ISR at maximum address
    memory[ISR_ADDR] = 24'h0F1E2D;

    // Print memory contents


    $display("====================================");
    $display("       ASSOCIATIVE ARRAY MEMORY");
    $display("========================================");

    foreach (memory[address]) begin
      $display("Address = 20'h%05h : Data = 24'h%06h",
                address, memory[address]);
    end

    // Number of elements
    $display("----------------------------------------");
    $display("Number of elements = %0d", memory.num());


    $finish;
  end

endmodule


<img width="922" height="316" alt="Screenshot 2026-10-07 181744" src="https://github.com/user-attachments/assets/0868e5b1-c29a-477e-b6e0-7574906b7b8d" />


module queue_example;

    // 3-byte queue initialized with 2, -1, and 127
    byte q[$] = '{2, -1, 127};

    int i;
    int sum;

    initial begin

        // Display original queue
        $display("Original Queue : %p", q);

        // ------------------------------------------------
        // b. Print sum of queue in decimal radix
        // ------------------------------------------------
        sum = q.sum();

        $display("Sum            : %0d", sum);

        // ------------------------------------------------
        // c. Print min and max values
        // ------------------------------------------------
        $display("Minimum        : %0d", q.min());
        $display("Maximum        : %0d", q.max());

        // ------------------------------------------------
        // d. Sort all values in ascending order
        // ------------------------------------------------
        q.sort();

        $display("Sorted Queue   : %p", q);

        // ------------------------------------------------
        // e. Print index of any negative values
        // ------------------------------------------------
        foreach (q[i]) begin
            if (q[i] < 0)
                $display("Negative value : %0d at index %0d", q[i], i);
        end

        // ------------------------------------------------
        // f. Print positive values
        // ------------------------------------------------
        foreach (q[i]) begin
            if (q[i] > 0)
                $display("Positive value : %0d", q[i]);
        end

        // ------------------------------------------------
        // g. Reverse sort all values
        // ------------------------------------------------
        q.rsort();

        $display("Reverse Sorted : %p", q);

    end

endmodule


Expected output
Original Queue : '{2, -1, 127}
Sum            : 128
Minimum        : -1
Maximum        : 127
Sorted Queue   : '{-1, 2, 127}
Negative value : -1 at index 0
Positive value : 2
Positive value : 127
Reverse Sorted : '{127, 2, -1}



