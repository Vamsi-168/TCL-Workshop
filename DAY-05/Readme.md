# DAY 5: Advanced scripting techniques and Quality of Results generation

### Synthesis main file scripting and output file editing :

![image](https://github.com/user-attachments/assets/e2f330f3-aafc-4dde-9ab9-0e014e4fdb3f)

- Now synth commands are adde for YOSYS tool
- Open another fieId in write mode and dump the lines
- Command where synthesis command will be running
     a. In the same .ys file, the new commands will be added
![image](https://github.com/user-attachments/assets/7f2a5889-67b8-4366-ba77-d0de377570e5)

- In shell, need to use 'exec', it will run the .ys file
     a. "catch" is used for error checks. Make the .log to .err file if required
![image](https://github.com/user-attachments/assets/85c4eb93-fd8a-4266-a63d-b0ccccf8b528)

   NOTE: grep -i error --> -i is case insensitive character check

### Need and script to edit Yosys output netlist :

  - SDC to format[2] task
![image](https://github.com/user-attachments/assets/d4d7eac7-474a-4527-a5e2-e7d91b507bfb)
  - YOSYS dumps synthesized netlist
       a. Has redundent lines in output file
       b. Remove the lines
![image](https://github.com/user-attachments/assets/9cf9a627-b396-4d55-ae1c-aa58fc3ae51d)

  - grep -v -w '*' <filename>
       a. grep data where '*' character is not there
  - grep the "\" and replace it with "" null character
![image](https://github.com/user-attachments/assets/4c582f33-a2a8-40ff-984f-f1430b37b19e)
![image](https://github.com/user-attachments/assets/6f435dee-e7cd-485b-bc1a-26976ed2180c)

---
   
## World of 'Procs'

### Redirect stdout proc and demo of TCL array command :
  ![image](https://github.com/user-attachments/assets/063bb882-284c-4035-8ed7-83edbd7634d9)
  1. Close the std screen log and open new file in write mode. Any new puts statement added will be dumped in this file
  2. For multicpu threading: ![image](https://github.com/user-attachments/assets/576e77b3-e6c4-47cf-8052-cfc32b63e9ec) . Used for distribution in EDA tools
     ![image](https://github.com/user-attachments/assets/36d35d74-3917-401c-aeb0-a191e949e0a4)
     a. Using the args and values of the args, the same will be activated with options for user. It can include details for the user to correct and execute the proc
     b. array set option work as variable and its corresponding value ![image](https://github.com/user-attachments/assets/2506ba4f-dc60-4880-99f4-89f5ea3ced83)
     c. "-help" is "null"
     d. As per this:
     ![image](https://github.com/user-attachments/assets/6a66beb6-351f-4b56-81a8-1c622113f9bb)
       i. Will be able to map to args and give the options
       ![image](https://github.com/user-attachments/assets/9145928f-6c0f-4757-a0f3-a6ccf7c2c348)


### 'set_multi_cpu_usage' proc :
Ex: for arg = 8
  1. ![image](https://github.com/user-attachments/assets/c7c37efe-4795-44ea-aa1a-76ede7c313b4)
  2. The arg value will be mapped for the value provided in the arg
  3. The switch is the options that the user wants to provide for use
  4. "-glob" will try to take the 0th element from the array
     ![image](https://github.com/user-attachments/assets/707ea9bb-dac8-49ae-b25e-7ed878e4428d)
     ![image](https://github.com/user-attachments/assets/aee5f38a-440d-4b6d-b8df-2f511e1a57e8)
  5. Now when both the option is used, the llength 3 is updated
     ![image](https://github.com/user-attachments/assets/6f87d322-7b94-4faf-bb40-ad84b48264b1)
  6. Options is an array and the variables and the value for the array as string is the options that we are providing
  7. Need to convert this proc to be understood by EDA tools
  8. As the value null has no options/ switch for the usage, it comes out of the loop


### read_lib and read_verilog proc demo :

  ![image](https://github.com/user-attachments/assets/03799bae-7b29-4df9-ba38-10bfbac93066)


### Read SDC file and replace square brackets by 'null' :

  ![image](https://github.com/user-attachments/assets/1e18cc6d-4ced-4b2f-9518-9b2f24e6ac70)


### Evaluate clock period and clock port name from processed SDC :
  ![image](https://github.com/user-attachments/assets/065b04e3-e289-48e9-8362-801a4bbd3863)

  1. Converting create_clock constraints
  ![image](https://github.com/user-attachments/assets/f1f55136-fc4d-484e-b8c2-585fe82d7d01)
  2. Elements mapped to index
     ![image](https://github.com/user-attachments/assets/83bfaff5-6145-49c8-82b7-9da7770e2bc7)
     ![image](https://github.com/user-attachments/assets/adb156ac-7454-4a85-a330-ba8853ff3cfe)
  3. Waveform calculation
     ![image](https://github.com/user-attachments/assets/d8e93323-5cc6-48eb-b913-635946a1c7d1)


### Evaluate duty cycle and create clock in opentimer format :

  1. Clock period and calculate using the duty cycle calculation
     ![image](https://github.com/user-attachments/assets/261cd027-4059-4627-bede-6b53f3262ba8)
  2. The expression will use the waveform creation for the selected ports
     ![image](https://github.com/user-attachments/assets/b4be2ddb-4e9f-470f-8087-4a3775351c0f)
     ![image](https://github.com/user-attachments/assets/5cc12554-9703-4afd-959d-40ad78bc9420)
  3. This will be able to be used in the openTimer tool
  4. The space separated line is put into a list
  5. Since there are 2 clocks, the create_clock is created like this:
     ![image](https://github.com/user-attachments/assets/fd5e88fe-d2a8-4c29-bf95-2285b42e8488)
  6. This format will be used by the tool
     ![image](https://github.com/user-attachments/assets/0ec9bd5a-15a3-431e-bd33-f969d1b307b0)


## read_sdc proc - interpret IO delays and transition constraints

### Grep clock latency and port name from SDC file
  1. Similar to create clock constraints, create the file for opentimer
     ![image](https://github.com/user-attachments/assets/42336675-e2d9-429e-909a-8f36d07c9c26)
  2. Intermediate file to be used ![image](https://github.com/user-attachments/assets/9f4eb092-a4a8-4c14-9a5c-88bf3490db13)
  3. Dummy port name to reduce the repeated lines to reduce runtime
  4. Go through each and every element of the lines
    ![image](https://github.com/user-attachments/assets/897466d6-e180-4df7-8bfe-30728800df4c)
  5. Check the port name from the list, if it does not match, the loop will continue. This sets dummy port name to current port name. Append them in single line using join
     ![image](https://github.com/user-attachments/assets/51418c41-20d4-4d10-b296-e6768c1a99dd)
     

### Convert set_clock_latency SDC to opentimer format
  1. Need to get the list for the delay
     ![image](https://github.com/user-attachments/assets/d0d4248d-1f19-4d56-849a-07c4eb90feda)
  2. Move through each element as per the {} characters which is 4. Now need to loop through each and every one
  3. Delay value will be taken as per the get_clocks, by which we can navigate it using the index. Append the value from the list
     ![image](https://github.com/user-attachments/assets/9085a8ac-d5b2-4f44-8ec0-4ed954832a14)
  4. Repeat this for all the elements in the loop
  5. Arrange the values ![image](https://github.com/user-attachments/assets/6a51a407-e26e-40a1-a2ac-79fde7581bc1)
  6. For the second clock, the new port name and the current name is same
     ![image](https://github.com/user-attachments/assets/8661f6e0-e989-4e5c-8b78-790e59e85a57)
  7. So it will not enter into the loop as the value will be same and give a null value
  8. Close the tmp file


### Script for convert transtion and input delay to opentimer format
![image](https://github.com/user-attachments/assets/d2ffd8f1-d080-42a5-8d92-339e03f42245)
  1. Similar to the previous ones, only it has updated the slew from arrival to set_input_transition

### Script for convert output delay to opentimer format
![image](https://github.com/user-attachments/assets/24d063b9-39be-419e-89b6-7c4ba2038305)
  1. Model the load for the output capacitance
  2. It is a single value that needs to be set
     ![image](https://github.com/user-attachments/assets/de82fac0-328a-4954-87dd-a3f37ef1b90d)
  3. Only the search pattern changes, others remain the same
     ![image](https://github.com/user-attachments/assets/1abe5c3d-3d0d-4c32-bf31-5b6c46a9ca74)


## Process bussed ports and configuration file creation

### Script to convert all bussed constraints to bit-blasted
![image](https://github.com/user-attachments/assets/392cb5e4-3b14-4c30-9c16-8bec1a9ebce5)
  1. The load also needs to be added for bit-blasted data
  2. Output will be visible like this:
     ![image](https://github.com/user-attachments/assets/0ff91aa0-679b-4593-9690-f8965d1a4640)


### Opentimer configuration file creation
  1. This format is required by Opentimer tool to execute the timing reports
     ![image](https://github.com/user-attachments/assets/ef96a6ea-ba6b-42fd-bf4f-ee228af7de9f)
  2. The .conf file will be input to the tool to generate STA data
  3. Will be creating spefs for sampling to the tool
     ![image](https://github.com/user-attachments/assets/f4ff7436-4eed-4417-93be-67ae80b40b00)
       a. This will create a blank SPEF using the data
       b. Then will append in the .conf file. Using appnd mode, it will add new data in the existing file
       c. Add the new commands for analysis for the deisgn
       d. Parasitics will give output like this:
       ![image](https://github.com/user-attachments/assets/dfd71e78-005a-4255-8947-017a1030d62a)
       e. The further commands appends are added at the last
       ![image](https://github.com/user-attachments/assets/a1eb73f1-698c-4803-9744-4842a605c228)


## Quality of results (QoR) generation algorithm

### Script to obtain STA runtime
  1. As per EDA vendors, there are different formats
     ![image](https://github.com/user-attachments/assets/5b355a51-243e-4587-b1ec-89241c073809)
  2. For runtime extraction for opentimer tool. Same can be done for entier flow as well. It depends on the CPU , memory availablity
  3. 'time" is a tcl command to check the time in micro-seconds (us)
  4. Now need to convert it to preferred format
     ![image](https://github.com/user-attachments/assets/962aca2f-5989-4ba4-9181-3472cd6928cc)
  5. Print the puts command for information to the user to understand
  6. Since we are redirecting the whole opentimer command to the .results area, we are displaying for the user to check for warnings and errors in the file
     ![image](https://github.com/user-attachments/assets/7ea9e5f9-b71a-4f52-a25f-47a87c76a5a6)

### Script to obtain WNS and FEP for reg2out violations
  1. Results that will be displayed for the STA
     ![image](https://github.com/user-attachments/assets/c27c2e8c-9aca-49c6-8d50-4d919de29052)

  2. RAT will display the slack data. SO this keyword in the results file will have all the slack data. So to calculate, the worst RAT / WNS, will be able to check easily
  ![image](https://github.com/user-attachments/assets/88277481-4080-441a-9e01-0b5725e1018e)
  3. Need a while loop to check the worst value
     ![image](https://github.com/user-attachments/assets/6d184ac7-b55d-41e3-b103-29faeb625bc9)
     a. If there are no violations, need to pront "-"
     b. Check for the regexp for the RAT in the file that is being read
     c. Print the RAT in "ns"
     d. Read the line for RAT, increment the count for the while loop
     ![image](https://github.com/user-attachments/assets/f72cbf65-2e9b-4e95-a623-05d8c3d5862f)

### Script for instance count, WNS and FEP for setup and hold
  1. Same loop can be used by reading the results file as per the pattern
     Instance count:
     ![image](https://github.com/user-attachments/assets/61f5f2b7-10f7-4624-8af2-619108eebca1)
     Setup violations:
     ![image](https://github.com/user-attachments/assets/3bae3875-6b40-4c18-81a6-e79fe46661f6)
     Hold Violations:
     ![image](https://github.com/user-attachments/assets/e9a60708-ed4a-4093-ad99-d4e9160c02cb)

### Script for report formatting
  ![image](https://github.com/user-attachments/assets/b727272d-574f-46f8-8eb6-52e276112e8e)
  1. %15s is a conversion specifier. FOr string, %s is string and 15 is spacing
  2. Now align the data as list and feed it to the table
     ![image](https://github.com/user-attachments/assets/15253e4b-d337-4aa3-be84-9f985afa9a23)
  3. Use the string separator as per the headings
     ![image](https://github.com/user-attachments/assets/aa5d29a8-0bae-4e1b-b8c3-01cb0a792d0a)
     ![image](https://github.com/user-attachments/assets/27849bd3-1e94-469e-aa1d-08204c32e6e0)
