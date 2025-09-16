# Introduction to TCL Workshop 

Welcome to the Day-01 of the Tcl workshop by VLSI System Design(VSD).

In this workshop, we will be going to cover right from the Tcl fundamentals to some advanced scripting skills, which are going to help automate the digital design flows whether it is RTL/Synthesis/STA/Physical design.

These are some of the skills that are going to be gained using this workshop :

- TCL script fundamentals and advanced procedures.
- Constraint file genration (CSV,SDC to Opentimer).
- Yosys flow integration and RTL Synthesis.
- Hierarchical design checking and error scripts.
- QoR metric analysis (WNS,FEP).

# Day-01 : Introduction to Tcl and VSDSYNTH Toolbox Usage 

## 1) Introduction to Tcl task
### Task : 
- Task is to build a user interface that takes excel sheet as an input and provide the output as datasheet.

- Given below is the excel sheet, which is the input to our TclBox and also the output datasheet.
  
<div align="center">
<img width="1247" height="587" alt="image" src="https://github.com/user-attachments/assets/84fa28c7-a0fb-4773-b5f3-d40d13766893" />
</div>

- This Input and Output to the TclBox can also be represented as below :

<img width="1101" height="626" alt="image" src="https://github.com/user-attachments/assets/53db6c68-f203-4244-aa59-46466e6945c2" />


- We are going to design this Tclbox using a shell script, written in a file on linux which looks like below :

<img width="1087" height="645" alt="image" src="https://github.com/user-attachments/assets/540e008f-e6b8-42b6-89d9-070c12b37adb" />

---

## 2) Sub task and Tools needed
### 2.1) Create command (vsdsynth) and pass .csv from UNIX shell to TCL script as shown below :
<div align="center">
  <img src="https://github.com/user-attachments/assets/3aa3d9ec-396c-4027-b5a6-aa66ea1f9f6b" alt="GTKWave Example" width="70%">
</div>

### 2.2) Convert all inputs to format[1] & SDC format, and pass to the synthesis tool 'Yosys'
#### 2.2.1 Converting excel sheet into format[1] as shown below :
<div align="center">
  <img src="https://github.com/user-attachments/assets/1e1518de-5d77-4efe-b5d2-459b54b6201e" alt="GTKWave Example" width="70%">
</div>

#### 2.2.2 Converting the .csv file into SDC format as shown below :
<div align="center">
  <img src="https://github.com/user-attachments/assets/2134a08f-93cb-47ae-ad16-035c7464ed86" alt="GTKWave Example" width="70%">
</div>

### 2.3) Convert format[1] & SDC to format[2] and pass it to Opentimer, this tool will accept commands like this :
<div align="center">
  <img src="https://github.com/user-attachments/assets/48223a3b-5a67-4785-a3de-916c5254b4ed" alt="GTKWave Example" width="40%">
</div>

### 2.4) Generate the final Output report as shown below :
<div align="center">
  <img src="https://github.com/user-attachments/assets/d5c047b8-7f5e-4f6a-b3aa-bfd72af6e1a8" alt="GTKWave Example" width="100%">
</div>


---

## 3) Scenario 1: User does not provide an input csv file

- This scenario describes what need to be done when user does not provide any .csv file while executing the tclbox(vsdsynth).
- In this case, it should give out an error/info message saying that no csv file is provided.
  
<div align="center">
  <img src="https://github.com/user-attachments/assets/8b67de41-2ca2-4de3-9d2f-adfd9303a753" alt="GTKWave Example" width="70%">
</div>

- This can be implemented using shell script with the help of a if condition :

<div align="center">
  <img src="https://github.com/user-attachments/assets/2bdf94d2-43be-4a5e-8e87-77f990edb536" alt="GTKWave Example" width="70%">
</div>

---

## 4) Scenario 2 & 3: Provide a csv file which does not exist

- In this case, if user is providing any .csv file which does not exist, then it should through out an error message mentioning the same.
  
<div align="center">
  <img src="https://github.com/user-attachments/assets/62b54946-6e5e-4f7d-aedc-d5508706edeb" alt="GTKWave Example" width="70%">
</div>
   
- Last scenrio is about when user enters -help inorder to find out the usage of the script :

<div align="center">
  <img src="https://github.com/user-attachments/assets/29af6b34-fd77-4228-97b5-6e10641b9565" alt="GTKWave Example" width="70%">
</div>
<div align="center">
  <img src="https://github.com/user-attachments/assets/6a5a354c-2360-4134-b7ea-437a45d1cf39" alt="GTKWave Example" width="70%">
</div>

- More of the practical examples of these scenarios can be seen in the labs_snapshot.md file.

