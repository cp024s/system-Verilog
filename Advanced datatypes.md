## 1. Structs

### Definition
A **struct** (short for structure) is a composite data type that groups related variables (called members or fields) into a single entity. Each member can have different data types.

### Characteristics
- **Syntax**:
  ```systemverilog
  typedef struct {
      data_type member1;
      data_type member2;
      // Additional members
  } struct_name;
  ```
- **Accessing Members**: Members of a struct are accessed using the dot (`.`) operator.
- **Fixed Size**: The size of a struct is determined by the sizes of its individual members, along with any necessary padding.

### Usage
- **Grouping Related Data**: Useful for representing complex data types and logically grouping related variables.
- **Modeling Entities**: Commonly used to model hardware entities, such as registers or packets.

### Example
```systemverilog
module struct_example;
    typedef struct {
        logic [7:0] data;   // 8-bit data
        logic [3:0] addr;   // 4-bit address
    } packet_t;             // Define a struct type

    packet_t my_packet;     // Declare a variable of type packet_t

    initial begin
        my_packet.data = 8'hA5; // Assign values to struct members
        my_packet.addr = 4'hF;

        // Display the struct members
        $display("Packet Data: %h", my_packet.data); // Outputs: A5
        $display("Packet Address: %h", my_packet.addr); // Outputs: F
    end
endmodule
```

### Execution Flow
1. A struct type `packet_t` is defined, containing a data member and an address member.
2. A variable `my_packet` of type `packet_t` is declared.
3. The members of `my_packet` are assigned values and then displayed.

---

## 2. Unions

### Definition
A **union** is a special data type that allows storing different data types in the same memory location. All members of a union share the same memory space, meaning only one member can contain a valid value at any given time.

### Characteristics
- **Syntax**:
  ```systemverilog
  typedef union {
      data_type member1;
      data_type member2;
      // Additional members
  } union_name;
  ```
- **Memory Efficiency**: Unions are memory efficient since they use the size of the largest member.
- **Accessing Members**: Like structs, members of a union are accessed using the dot (`.`) operator.

### Usage
- **Memory-Constrained Designs**: Useful in situations where you need to save memory and can represent data in multiple formats.
- **Type-Punning**: Allows interpreting the same data in different ways (e.g., interpreting a bit pattern as both an integer and a floating-point number).

### Example
```systemverilog
module union_example;
    typedef union {
        logic [7:0] byte_value;     // 8-bit value
        logic [15:0] half_word_value; // 16-bit value
    } data_union_t;                 // Define a union type

    data_union_t my_data;           // Declare a variable of type data_union_t

    initial begin
        my_data.byte_value = 8'hFF;  // Assign to byte_value
        $display("Byte Value: %h", my_data.byte_value); // Outputs: FF
        my_data.half_word_value = 16'hABCD; // Assign to half_word_value
        $display("Half Word Value: %h", my_data.half_word_value); // Outputs: ABCD

        // Note that byte_value now contains an undefined value
        $display("Byte Value After Half Word Assignment: %h", my_data.byte_value); // Outputs an undefined value
    end
endmodule
```

### Execution Flow
1. A union type `data_union_t` is defined, containing a byte member and a half-word member.
2. A variable `my_data` of type `data_union_t` is declared.
3. The `byte_value` member is assigned a value and displayed.
4. When the `half_word_value` member is assigned a new value, the `byte_value` becomes undefined because both members share the same memory.

---

## Summary

### Structs
- **Definition**: A composite data type that groups related variables into a single entity.
- **Syntax**: 
  ```systemverilog
  typedef struct { 
      data_type member1; 
      data_type member2; 
  } struct_name;
  ```
- **Usage**: Grouping related data and modeling hardware entities.
- **Example**: Declaring a `packet_t` struct with `data` and `addr` members.

### Unions
- **Definition**: A data type that allows different data types to share the same memory location.
- **Syntax**:
  ```systemverilog
  typedef union { 
      data_type member1; 
      data_type member2; 
  } union_name;
  ```
- **Usage**: Memory-constrained designs and type-punning.
- **Example**: Declaring a `data_union_t` union with `byte_value` and `half_word_value`.

Both **structs** and **unions** provide essential mechanisms for organizing data in SystemVerilog, enabling more effective modeling and design of digital systems. Structs are suitable for grouping related data, while unions offer memory-efficient alternatives for storing different types of data in the same location.
