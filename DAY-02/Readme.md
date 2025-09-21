# DAY 2 : Variable Creation and Processing Constraints from CSV

## SubTask 2 : Converting CSV to format[1] and SDC - Variable Creation

### 2.1. Tasks involved in format conversion :
  -  Create Variables for the corresponding inputs provided in the excel sheet
    
     ![image](https://github.com/user-attachments/assets/2696ae6f-05a9-4cca-b5a8-80344bb2221e)

  -  Check if dirc and files mentioned in .,csv exists or not

     <img width="551" height="340" alt="image" src="https://github.com/user-attachments/assets/f067e7ae-4ec8-4b2c-8081-6a23a01e17ed" />

  -  This will help the user to correct any input paths or files provided is the above loop is unable to find them as the tool will exit with prompt and the reason. If path is found it will also inform the user.
    
  -  "puts" function is to echo in the shells and is like prointing any statements that is required to be conveyed
    
  -  Next is Read "COnstraints FIle" for the .csv and convert to SDC format(Universal constraint caled Synopsys Design COnstraint) to be used by PNR and STA tool
    
     <img width="742" height="217" alt="image" src="https://github.com/user-attachments/assets/8413dbe0-c023-49e4-8c0c-13c309a56607" />

  -  Read all files in "Netlist Directory"
    
     <img width="516" height="148" alt="image" src="https://github.com/user-attachments/assets/81c27944-313f-48bb-95f0-f8c83ea07384" />

  -  Create main synthesis script in format[2] for the "Yosys" tool to be used
    
     <img width="952" height="148" alt="image" src="https://github.com/user-attachments/assets/74b7a6af-a372-43a6-9ca2-57e219669260" />

  -  Pass this script to Yoysys
     
     <img width="822" height="175" alt="image" src="https://github.com/user-attachments/assets/e7bd5c21-82ca-4f42-b526-c659b03c9d29" />

  -  Variables helps to brigde and make a very streemlined flow so it reads inputs

---

### 2.2. Auto-Create variables using matrix and arrays

  -  Pass csv file to the tcl

     <img width="792" height="151" alt="image" src="https://github.com/user-attachments/assets/a748253c-2fe2-42fd-8929-52f2c0f8025e" />

  -  The arguements will be passed from the vsdsynth file to the .tcl file to access the each value using index[x]. The ndexes help to add more arguements as per requirement. Inside the sq brack needs to be executed. The set filename will now be the value from the [lindex $argv0]
    
     <img width="806" height="260" alt="image" src="https://github.com/user-attachments/assets/514ec87e-3f97-4cc9-8697-dc7f17d1aa86" />

  -  Auto creating variable. Will help to be independent of the files/ directory location.
    
  -  2x6 matrix is used and converted to array
    
   <img width="636" height="701" alt="image" src="https://github.com/user-attachments/assets/0490e22d-1e61-4d49-a905-eb02b36679f6" />

  -  Now processing the array is easy as it acts like a address for the data to be addressed. Own logic can be used for the varaibale auto creation
    
  -  set  the new variable name and link it to the array. This linking will help the tool to access the original value that is provided in the .csv file which is the csv filename
    
   <img width="1155" height="723" alt="image" src="https://github.com/user-attachments/assets/ad1b5345-56a7-4915-bfb0-2383b70a8859" />

  -  Loop through the remaining array variables

---

### 2.3. Initialize variables for auto-creation variables task

![image](https://github.com/user-attachments/assets/5a9d9e85-1693-42c3-9538-3f83ecdfb4bf)

  - Package for csv and matrix to be installed
    
  - The struct::matrix object will be used to store the values in a matrix form.
    
  - Open is file attribute to open the filename and stores in variable
    
  - csv (comma separated value) - the file will look like beofw in vim
    
     ![image](https://github.com/user-attachments/assets/13c97425-b136-4a83-965f-60d42790f662)
    
  - The "," will be used to sepaerat the values into the matrix and identify the size also
    
  - csv::read2matrix is commands from the cpackages to exectue the intruction
    
  - close $f will close the file
    
  - Column and row values will taken. Instead of $columns or $row, if value is directly given then the respective columns and rows will be created
    
  - Then link my_arr will convert this colunxrow format into array. THe array will act like a coordinate to extract and store data
    
  - A counter increment is required to access all the data using a loop

---

### 2.4. Auto creation of the first variable - DesignName and Completion 

  -  Variables set to for the filename, matrix , columns , rows and counter
    
     ![image](https://github.com/user-attachments/assets/f43aae70-677d-46a3-a8eb-acb6eae1981b)
     
  -  Enter into a loop. Put a meessage for the array value. With each increment of the value i, the array data will be displayed for the user. (\n is new line)
    
     [image](https://github.com/user-attachments/assets/d180b262-b484-4d3e-8e33-98bf88eb267b)

    
  -  In the first step, chars inside [] like the string map {_PS _TCL} learn_PS -> learn_TCL
    ![image](https://github.com/user-attachments/assets/c4552114-91dd-427a-bde8-f9d24c9df1a3)

  -  In our file, we will be replacing the space with "_" using the string map
    
  -  DesignName is the frst valriable set , when given, $DesignName will give out the file name
    
  -  tcl command [expr {$i+1}] the expr is expression. it will evaluate the values inside the {} brackets.
    
  -  Now the "i" value as passed on the top to the while condition

  -  For DesignName, the output directory will be shown
    
  ![image](https://github.com/user-attachments/assets/c611a1a7-d430-4138-9083-c353a699c093)
  
  -  Now in the else loop, the variable and the value also is another command to be processed
    
  ![image](https://github.com/user-attachments/assets/24bd3c56-6437-4a5b-a8a4-40b960cf6162)

  -  Now the normalize is another set of sommand to process the absolute value for the directory
    
  ![image](https://github.com/user-attachments/assets/417fd2e5-599d-4688-8b61-a9b1997a6175)
  
  -  Now this will be saved in the OutPutDirectory as an absolute value
    
  ![image](https://github.com/user-attachments/assets/1be11230-8b62-425f-b2ee-7c990188d1ff)

  -  Now if we increment the "i" value, then the array address is updated and the coressponding value is assigned to it for the rest of the path values from the .csv file
    
  ![image](https://github.com/user-attachments/assets/df268191-e967-4cd7-9d64-d6cf75c84145)
  
  -  Data will be assigned as below
    
  ![image](https://github.com/user-attachments/assets/f3c450cc-6bc3-4f6e-a75d-211672f60bbb)




## Sub-Task 2 : From CSV to format[1] and SDC - Processing constraints, CSV

### 2.5. Checking the existence of files and folders mentioned in design_details.csv 

  ![image](https://github.com/user-attachments/assets/c5b1587d-6411-436b-b2c3-ce498237fc62)
  
  - If the conditions fulfil in if, then it will create directory
    
  - Else it will display the output directory path

     ![image](https://github.com/user-attachments/assets/9822981a-1196-45f4-9b83-667386965038)
    
  - In this the if else has covered conditions for the user, however for the netlist dorectory, that information is mandatory to move forward, so the information will be passed to user to correct and update the required files and the command will exit
    
  ![image](https://github.com/user-attachments/assets/aed0eb89-d536-4590-bc60-9be49c7debd2)
  
  - As the above was checking the directory, it was using isdirectory check. Now to check file for the lib files, it needs to check using "exists"
    
  ![image](https://github.com/user-attachments/assets/f098babd-780e-4cc5-ae4a-50c5bea42587)
  
  
### 2.6. Convert constraints.csv file to a matrix object

  ![image](https://github.com/user-attachments/assets/03fa6e85-996e-4be3-87c3-272fd648567a)
  
  - The data can be in bus format, in that case have to go to the netlist and check the data
     
  ![image](https://github.com/user-attachments/assets/06f306da-302a-4be6-b45a-a80ea2703045)
  
  - Dumping of SDC constriants and read from the csv file above and create the rows and columns as per the "," characters
     
  - chan is an identifier for the file opening the csv file
     
     

### 2.7. Compute row number using complex matrix processing

  - Inside square commands becomes a tcl command
    
  - contraints is the name of the matrix and the rows and columns for the matrix will be read. The struct::matrix contraints object is the name given to the matrix
    
  - In future, if required, $rows and $columns can be used
    
     ![image](https://github.com/user-attachments/assets/064bdad1-64f8-42b7-9509-59e39e275130)
    
  - Process the clock, inputs and outputs separately
    
  - "search all" is from the package and check the character "CLOCKS"
    
     ![image](https://github.com/user-attachments/assets/d3c20efd-449a-47ab-9806-7fab3667f857)
    
  - Breakdown of lists that comes in {}
    
  - Check for inputs. Will start with 4
    
     ![image](https://github.com/user-attachments/assets/a6ae0351-20d3-4360-9b9a-8477c6325497)
    
  - Similarly for outputs. Will startt with 27
    
     ![image](https://github.com/user-attachments/assets/3860b027-da2d-4320-97d0-ed596ce670be)
     ![image](https://github.com/user-attachments/assets/2a0c0eba-8a7b-4139-b483-985e9bace63f)
    
  - The start point is to be defined in order for the data to be separated and retrieve from the csv file
