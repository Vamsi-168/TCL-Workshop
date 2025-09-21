# DAY 3: Processing Clock and Input Constraints

---

## SubTask 2 - From CSV to format[1] and SDC - Processing clock constraints

### Algorithm to identify the column number for clock latency constraints

![image](https://github.com/user-attachments/assets/e15d3a41-27e4-435c-ad54-53bb1dfc8820)

  - Basic algorithm is to find the column number for early_rise_delay and loop it
    
     ![image](https://github.com/user-attachments/assets/6b0f1d05-1593-4066-84aa-459ed16b8408)
    
  - While going through the loop, need to fill the values
    
  - Finally display the contents of the cell
    
     ![image](https://github.com/user-attachments/assets/12dfff65-5bca-4f57-bd80-688535d671dc)
    
  - Will break the command to small pieces. [] are tcl commands. Search the csv for the respective column for a small area of the file
    
     ![image](https://github.com/user-attachments/assets/85efdeb2-edcb-41cd-b9c7-a77c15a23ce7)
    
  - Ex: The expr inside {} is 11 - 1 for evaluation. The search space is restricted, so the starting value with check the rect that it will start from the CLOCK section only and check for columns with only early_rise_delay file
    
    ![image](https://github.com/user-attachments/assets/7124ed01-e3d6-4f8e-a7c8-d6bd7472efd6)
    
  - Now if we access the 0th index of this list, we wll get the clock_early_rise_delay_start = 3
    
  - Now we can continue to loop through the entirely
    
     ![image](https://github.com/user-attachments/assets/12bc99dd-b400-4be7-8161-23c4270f862e)

    ---

### Start writing clock latemcy contraints in SDC file

  ![image](https://github.com/user-attachments/assets/5acd071e-4f9b-4c54-8253-b7a2a6e73127)
  
  - In the loop, check if the entire clock constraints are read
    
     ![image](https://github.com/user-attachments/assets/07cb1282-5fe3-4c8c-8fa6-df3259f70240)
    
  - This line will now create the command for clock latency by getting the values from the constraints file
    
  - The newLine command with -nonewline will print one by one as the loop proceeds
    
  - Now evaluate the values from the matrix and print it for 3,1 matrix location
    
     ![image](https://github.com/user-attachments/assets/cc94ee0f-eb77-4cbf-b471-81314f006824)
    
  - To differ between the tcl [] and this command is using "\"
    
     ![image](https://github.com/user-attachments/assets/3214ab31-d466-4b78-a548-5e0d1515173a)
     ![image](https://github.com/user-attachments/assets/2764bbe8-619d-4e48-b5e3-6906771b50ee)

    ---

### Complete clock latency constraints and clock slew constraints in SDC file

  - Now complete the early_fall_delay. Update the rect value
    
     ![image](https://github.com/user-attachments/assets/9e9dad91-6920-4ca9-b108-9e5455ae3f95)
    
  - Add the remaining lines by changing the contraint value
    
     ![image](https://github.com/user-attachments/assets/5bd16eb9-5323-4d08-8f5b-4d3fdcf51b8f)
    
  - The slew values can also be updated for keyword update
    
     ![image](https://github.com/user-attachments/assets/e9d1dbc8-f838-42a6-92c7-5acea6db26fd)
     ![image](https://github.com/user-attachments/assets/debd3040-ac78-431a-9d42-8810ff45dc6c)
    
  - For slew, clock_transtion wil be required for the command to be used
    
     ![image](https://github.com/user-attachments/assets/293e1c08-a497-4079-a4aa-3115c042ba40)

    ---

### Code to create clock constraints with clock period and duty cycle
![image](https://github.com/user-attachments/assets/24c83c9d-fda2-4434-9ee4-c3b2d320b974)
  - To get the clock name from file, can use this ![image](https://github.com/user-attachments/assets/5780dbe5-d746-440d-8f1f-60b206330e4e) or hardcode the value in the command
  - For the waveform have to be formulated as per the duty cycle of the clock period
     ![image](https://github.com/user-attachments/assets/24212ef8-9afa-43ec-a005-d631a27c7910)
  - The expr use from the matrix for the cell values, will give us the waveform. As duty cycle is 50%, the first expression will give 1500 and the second gives 50. The arithmetic calculation will give the value. Once the i is incremented, it will update for the rest
  ![image](https://github.com/user-attachments/assets/2e2f501c-b8e7-42e6-8c59-a9959ec538dd)
  - File open in write mode for sdc, the below command will be consolidated
    ![image](https://github.com/user-attachments/assets/48be5057-e709-4b4b-b7b3-aa398ef0f0ae)


NOTE: for the command to understand the {} as character, "\" is used before

---

### SubTask 2 - From CSV to format[1] and SDC - Processing input constraints

### Introduction to the task of differentiating between bits and a bus

Ex: ![image](https://github.com/user-attachments/assets/09917a87-23d7-4165-9662-52aec8d3e8ab)
![image](https://github.com/user-attachments/assets/7a24fb49-3692-4fa4-83e5-5b5e816fade8)

  - The inputs are mostly bus values, i.e they are mutibit.
    
  - Need to identify these multibits data for EDA tool to process
    
  - In n-bit bus, '*' is added so that this will be taken for all the bits
    
  - This will open the verilog file and take the data from top level

  - Loop to read multibit ports
    
  - Update the search rectangle from INPUT to scan_mode row
  
  - Related clock to be searched for the IO ports that we are trying to find data for
    
  ![image](https://github.com/user-attachments/assets/1f103a2d-73e3-4fea-99e0-50bffe955b6d)
  
   Input spaced by multiple characters
   String element count
   ![image](https://github.com/user-attachments/assets/c7fdc1b0-08a0-4f9e-8d32-98c420f02557)

---

### Algorithm to categorize input ports as bits and bussed

  - Globing - identifying the wildcards in directories by searching and get all the .v files in the directory. Similar to ls -lrt
    
     ![image](https://github.com/user-attachments/assets/769a1b3e-4c65-4d7c-a4e1-da25a041528a)
    
  - tmp file created and is destroyed after use
  
  ![image](https://github.com/user-attachments/assets/1d1f4ed0-2e02-45b4-942d-7935a45ad1f4)
    
  - The space separated path in the netlist directory will be assigned to the "f" variable in the foreach loop.
    
     NOTE: If no "w" is given the default file will be opened in read mode
    
  - The while loop will read every line till the end of line. (-1) refers to end of line

    ![image](https://github.com/user-attachments/assets/1971589a-2360-40c1-8d74-0c36a11674bb)
    
  - "" is used for pattern creation. As .v file has an extension of ";" , so adding it in the pattern
  
    ![image](https://github.com/user-attachments/assets/0b390513-79a1-4fb6-a0b0-b861cdc6f3e6)
    ![image](https://github.com/user-attachments/assets/07c1cb20-b581-4328-b049-cb9303e7119f)

---

### File access and pattern creation steps

  - regexp is regular expression trying to find the pattern in each line from the netlist that it is reading from
    
  - If the pattern is not found in one file, it will move ahead to the next file
    
     ![image](https://github.com/user-attachments/assets/d768bcd8-17f2-486e-a504-2affa8de91c3)
    
  - The "\S+" to get multiple spaces and get the elements around the spaces in the pattern2
    
  - The new string pattern will be created and get inside the loop
    
     ![image](https://github.com/user-attachments/assets/9f7d498e-c72f-42b5-b5fc-fa8c04b0536f)
    
  - The count is < 2, so no * is added at the end
    
  - Now added this to the temp file without the multiple spaces for easier evaluation
    
  - regsub having multiple spaces will now evaluate and put it in the temp file with a new string name ![image](https://github.com/user-attachments/assets/30e3ea6a-a256-4dbf-ae66-83e5774037da)
    
  - Close the netlist and the temp file and the temp file should have the data
    
     ![image](https://github.com/user-attachments/assets/9ebb2535-a663-4497-85be-8f94bac82fc0)
    
     -> Need to sort this repeated values

### Regular expression and regular substitute to get fixed space strings
Check the data LAB part on how the regexp help to remove the extra spaces between them

---

### Read, split, uniquify, sort and join input ports to remove duplication

  - The created tmp file will be read which contains the output data from all the verilog  files. Since $i is till 5, only the cou_en will be displayed and dumped.
    
  - Now open another tmp2 file in write mode
    
     ![image](https://github.com/user-attachments/assets/1eda392e-51e6-4b5c-841e-f61b66e95161)
    
  - Now for data to be dumped in tmp2 file:
    
      a. Read  contents of tmp1 and split them with "\n" as delimiter as the data is pronted   in newlines.
     ![image](https://github.com/user-attachments/assets/8d75f220-6c16-4dca-9525-23d97260643f)
      b. Since \n was dumped in the tmp1 as the 1st element, the output will have {} as the start. ![image](https://github.com/user-attachments/assets/1ca8ce4d-51f5-46a5-a5cd-d1aa3eee0911)
      c. Uniquify the element in the same list and sort it. ![image](https://github.com/user-attachments/assets/df52c448-b6f0-4a1d-9f21-39eaeffe4e99)
      d. Now join them as "\n" delimiter. ![image](https://github.com/user-attachments/assets/8a311861-a347-4c6d-b326-80616418db33)
      e. There will be no duplication and unique data will be saved in tmp2 file
      f. Now if the $i is > 5, the multi bit data will be taken.
         i. NOw there will be more elements in the data that is finally dumped in tmp2
          ![image](https://github.com/user-attachments/assets/92cb182f-d063-4499-87e4-fb14a6bd615a)
      g. Close the tmp and tmp2 files ![image](https://github.com/user-attachments/assets/e5bf3fb6-afd5-49e3-93b1-7d12b09e254e)

---

### Evaluate the length of the string
  - Open the tmp2 file in read mode which was closed after the unique daat was dumped
    
     ![image](https://github.com/user-attachments/assets/099d2579-3609-4b19-9fe1-daf0e2994f43)
    
  - The cound with get the lngth of the lines in tmp2
    
  - Concat the data if > 2 , i.e. Multibit data
  - 
     ![image](https://github.com/user-attachments/assets/353cf962-23b4-46a8-aa9f-f79d3e8e3438)
   
   NOTE: TCL can read the file only once. So commented out after use.

  - Step by step the process can be shown and be visible in LAB sections. Be it reading, sorting, uniquifying and joining the data.
    
  - This will show the content of the tmp2 file.
    
  - Now concat the multibit data by putting * at the end

---

### Input constraints generation

![image](https://github.com/user-attachments/assets/a4212cbc-69ed-43f0-89d3-4bdb9d88e434)

![image](https://github.com/user-attachments/assets/cad5098a-8454-4515-ad8a-0ee9847bf6d2)

![image](https://github.com/user-attachments/assets/7739f434-7dd5-4823-87e4-731b1aa6413b)

![image](https://github.com/user-attachments/assets/673e4e38-a63e-4e14-ada5-e0ab55a4d28f)

