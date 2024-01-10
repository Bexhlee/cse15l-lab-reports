# Lab Report 1
## Remote Access and FileSystem (Week 1)

### Commands


1. `cd <path>` - **Used to switch the current working directory to the given path**

    An example using the command with no arguments:
    
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/298b8216-162e-46c7-b64c-84fe0b6dc185">
    
    > **Working Directory:** `/home`
    >
    > *Passing no argument to the `cd` command means that the directory changes to itself and therefore the directory is unchanged, as can be observed on the `~` portion of the prompt.* 
	<br>

    An example with using the command with a path to a directory as an argument:
    
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/aa11be8b-d3ae-4a26-8863-7d0fe9063aff">
    
    > **Working Directory:** `/home`
    >
    > *Passing a path to a valid folder in the working directory to the 'cd' command allows the current directory to change to the listed folder. On the prompt, we can see that the directory has successfully changed to `/lecture1`*
	<br>

    An example of using the command with a path to a file as an argument:
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/2d3be735-af4e-4454-9ec9-bb22731a0e2c">
    > **Working Directory:** `/home/lecture1`
    >
    > *Passing a path to a file to the `cd` command generates an error message because it is not a valid directory. The working directory in the prompt afterwards remains unchanged because the `cd` command terminates due to the error.*
    > <br>

	<br>
	<br>
2. `ls <path>` - **Used to list the files and folders the given path**
  
    An example using the command with no arguments:
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/16ac724d-68c0-4467-90c5-f2965f263b17">
    > **Working Directory:** `/home/lecture1`
    >
    > *Passing no argument to the `ls` command  results in the listing of files and folders in the working directory. This is because a blank path means that the relative path is itself. *
    > <br>


    An example with using the command with a path to a directory as an argument:
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/391fc19e-dafb-486a-bd77-2af9dca3a951">
    > **Working Directory:** `/home/lecture1`
    >
    > *Passing a path to a valid folder in the working directory to the `ls` command  results in the listing of files and folders at the directory in the given path.*
    > <br>


    An example of using the command with a path to a file as an argument:
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/d1740e6a-051d-4113-b08b-e97769caf8e4">
    > **Working Directory:** `home/lecture1`
    >
    > *Passing a path to a file to the `ls` command returns the relative path of the file specified. This is because the only item in the specified relative path is the file itself. *
    > <br>

	<br>
	<br>
3. `cat <path> <path>` - **Used to print the contents of one or more files given by their paths**

    An example using the command with no arguments:
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/76a7cb1f-929b-400b-80c6-8d045c8865e8">
    > **Working Directory:** `/home/lecture1/messages`
    >
    > *Passing no argument to the `cat` command results in the terminal awaiting for more input because the file path(s) not specified. The terminal will proceed to echo back any user input until the user terminates with* **Ctrl + D**. 
    > <br>


    An example with using the command with a path to a directory as an argument:
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/fa3a6a86-5d61-46b6-b6ea-aebcf019443e">
    > **Working Directory:** `/home/lecture1`
    >
    > *Passing a path to a valid folder in the working directory to the `cat` command generates an error message because it is not a valid file. The `cat` command can only be executed on files, not directories.*
    > <br>


    An example of using the command with a path to a file as an argument:
    <img width="666" alt="image" src="https://github.com/Bexhlee/cse15l-lab-reports/assets/152840466/a5bfe347-ef78-43ed-a50a-fb673862b164">
    > **Working Directory:** `/home/lecture1`
    >
    > *Passing a path to a file to the `cat` command generates an error mesage beacuse it is not a valid directory. The working directory in the prompt afterwards remains unchanged because the `cd` command terminates due to the error.*
    > <br>
