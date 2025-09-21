# DAY 4: Complete Scripting and Yosys Synthesis Introduction

## Full script for download and Conclusion

### Constraints generation logic for the output port and Conclusion :

  - Similar to input constraints
    
     ![image](https://github.com/user-attachments/assets/24413375-c05c-4540-93bd-619def6e5182)
    
  - Now need to update the rect for searching the cells in the constraints matrix
    
  - Since now the search area will start from the output cell and end in the final row number. The search rect now will require the number of rows as end point for the data to be read
    
  - The output will only contain delays and load. It does not consists the slew/ transition data. These are standard constraints for the input and output for the SDC format creation
    
    ![image](https://github.com/user-attachments/assets/a6da11e9-2981-46c0-8230-35e7df35275d)
    
  - With this the TCL first part is concluded for the SDC creation as per the standard format

---

# Introduction to Yosys synthesis tool usage :

### Example of a memory module RTL description  

  - Now will pass the SDC created previously to 'Yosys' tool
    
  - Ex: The memory module creation with CLK, ADDR, DIN, DOUT
    
    ![image](https://github.com/user-attachments/assets/75719571-633d-4f6c-a74b-8f4fea7077d1)
    
      a. The word sze changes will determine the bit size. Input and output can be updated for the behaviotal code
      b. This will now create a gate level netlist
      ![image](https://github.com/user-attachments/assets/710b51c8-f982-4e83-996e-35f29da2eab6)
      c. Tool has command called "show command" to show the implemented code
      d. The module will look like this. If WordSize is 1, then it can store 1 bit data in 0 and 1. ![image](https://github.com/user-attachments/assets/a465b720-a5f4-42e2-931a-51f2c14d77f6)
      e. Convert the binary to decimal to resolve the address size of memory
      ![image](https://github.com/user-attachments/assets/dec4a744-a544-4951-ba14-f5b5ae88cc43)
      f. Clock input port parameters are based on the edge change of the clock period

     
### Memory functionality and Synthesis using Yosys :

  - Process memory for the posedge of the clock. mem[ADDR] wll direct to the address of the memory
    
     ![image](https://github.com/user-attachments/assets/3688694d-bc58-494a-b7b2-5dd0bf790528)
    
  - For the second clock edge, it is same and DIN data will be updated. So for DOUT <= mem[ADDR] is din value as it is assigned
    
  - For addr[0] & [1], the functionality changes. DIN will go and sit in the memory

  - Add the memory verilog code in memory.v
    
  - Create a yosys file for the behavioural process for Yosys
    
     ![image](https://github.com/user-attachments/assets/b0623fe2-c83d-4515-8dc5-749a4fdfecf0)

  - RTL Gate level Synthesis will be visible at the last for the memory module
    
     ![image](https://github.com/user-attachments/assets/d42d4ad7-e010-4b43-8923-5f8e7aedf6d5)


### Components and Gate level netlist description of Synthesiszed memory :

  - Real Gates to be fed with right inputs
       a. set ADDR[0] to access data in the address
       b. In each mem[], X is put (undefined)
    
  - INV, NAND, OAI(OR,AND,INV), NOR - truth table is used
    
![image](https://github.com/user-attachments/assets/d4091906-de64-429b-bd13-f4dd60f2f5be)

  - Diamond shaped representation of mem refers to a bus
    
![image](https://github.com/user-attachments/assets/65876147-f4df-4f63-b281-f76ce1510011) 


### Memory Write operation discussed in detail :

Final output to the D FF and at the pos edge, data updates / write out and read in

![image](https://github.com/user-attachments/assets/15ced796-4872-4dd6-bf23-f9a5b7081059) 
![image](https://github.com/user-attachments/assets/57cdc413-ab6d-4de8-bbb7-9770fb291a7f)

### Memory Read operation :

![image](https://github.com/user-attachments/assets/cb04eee8-6495-4d24-b9ae-3c01802ce93a)

  - Now will check for the 2nd clk edge
       a. INV -> DIN_bar
       b. NAND -> 1
    
  - Output will have the Inputs for OAI
    
  - For A | C = 0 | 0 as per Truth table
       a. Output is complmentary of Input -> A_bar
    
  - Now the D->Q mem read scenario from the OAI output data
    
  - Select will determine the read/ write mode of the memory
    
  - At 2nd clock edge, new read data will come and the DOUT will write the DIN of previous clock out

### TCL scripting agenda

  - Automation of RTL in YOSYS tool and to get the gate level netlist
  - Hierarchical checks
  ![image](https://github.com/user-attachments/assets/2a1b97ce-9edd-44b9-9808-c460f8312460)
  - Need to make sure that the csv is connected and the output .v is given to YOSYS with aytomation and to give gate level netlist
  - .csv --> .v

![image](https://github.com/user-attachments/assets/d9a360d3-9e03-43ff-8b6c-b3b429180fed)

---

### Hierarchy check and error handling script creation for Yosys

#### Script to do a hierarchy check :

  - Output is synthesized netlist required
  - Provide Info statement for user to check
  ![image](https://github.com/user-attachments/assets/4716230c-9f10-4779-b599-95cba571b8db)

  - CHecks for hierarchy misses in the .v file
  - read_liberty -lib
       a. YOSYS tool commans
       b. To convert RTL to gate level netlist
![image](https://github.com/user-attachments/assets/df2538da-80b4-4f15-a53e-88890fd8db99)

#### Error handling script for hierarchy check :

![image](https://github.com/user-attachments/assets/6156d0d0-efeb-4fe1-9f91-bf7411320f7e)
  - Referred in module - changes with tool to tool
       a. YOSYS has referred in module only for error check
       b. Found in log file
     ![image](https://github.com/user-attachments/assets/0396a499-ea69-4307-abf6-dfc12c554c3c)
       c. Update keyword as per the EDA tools
![image](https://github.com/user-attachments/assets/6f723526-9781-4154-b2e0-902db2e7f72b)

