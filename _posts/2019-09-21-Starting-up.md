## NOTEBOOK SECTION1: USING THE CLUSTER IN WINDOWS 

During the semester we will be using the cluster supported by UCCON Health Center, thus we need to know how to access to it. In this case I will be working in a PC. The following instructions are for other PC's users, and also reviewing some basic commands.

## A) GETTING INTO THE CLUSTER
1. Install Putty for access to the cluster, it can be found in: https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html
2. Access the cluster with the following: (note that mcbusr11 is the user name assigned at class) “mcbusr11@xanadu-submit-ext.cam.uchc.edu”
2. Ask for Host key .. -> Yes
3. Type password: xxxxxx 

### Out of the head node
<p> Once into the cluster we have to move out of the head node by requiring a place where to run commands in the cluster, to do it we use the following command: </p>
  
    Bash$: ssrun --pty -p mcbstudent --qos=mcbstudent --mem=2G bash

### Changing the password:

    Bash$: passwd

the password won’t show up, but it still will receive the information, just follow the instructions
<img align="center" width="50%" height="50%" src="/IMAGES/psswdchange.PNG"/></a>

### Locating where I am:

At this point we are located at the usr11 directory, located into the mcb5896 directory allocated into the CAM directory in the cluster.
Every time we want to know our location type
        
    Bash$: pwd

<img align="center" src="/IMAGES/pwd.PNG"/></a>

### mkd and ls commands

Is important to allways keep the files and directories organized, to do so we can create directories with

    Bash$: mkdir MiSeq_SOP
  
note: you can name the directory as you please

check the creation of the directory with "ls"

    Bash$: ls

<img align="center" src="/IMAGES/mk_ls.PNG"/></a>


### Copying a directory with files from one location to another

<p> To copy a group of files located in a Directory to other we need to specify the path after the “cp -a” command. The first part following the command specifies the location of the files to be copied, the second part specifies where the directory with the files will end up. We created before a directory with the same name inside the directory that will receive the copy, thus all the files of the original directory will end up in it. If we don’t have a directory with the same name, the command will create the directory and then move the files into it. Note that we are copying without going outside the present location (mcb5896/urs11).
After copying we will verify that the files were copied into mcb5896/usr11/MiSeq_SOP </p>

<img align="center" src="/IMAGES/copyingfigure.PNG"/></a>


## B) SECURE COPY FROM THE CLUSTER TO COMPUTER

We can copy files and directories from the cluster to our own files in our working station using different programs like FileZilla or WinSCP. The following demonstration has been done using WinSCP.

    To log use mcb5896usr11 as username
    The host domain will be transfer.cam.uchc.edu
    
After logging in, we will have to find the folder in our local computer where we want to place the directories coming from the cluster.
We are transferring the "transferthistext.txt" file from the cluster (path:  ~/mcb5896/classFiles/)

<table style="width:100%">
  <tr>
    <th><img align="center" src="/IMAGES/transferwiscp.PNG"/></a></th>
    <th><img align="center" src="/IMAGES/transfer2.PNG"/></a></th>
 </table>

In the figure we can see that we have a copy of the *txt file in our local folder
<img align="center" width="50%" height="50%" src="/IMAGES/transferconfirmation.PNG"/></a>

We can also send it to other location in the cluster, this time we are copying it into the usr11 directory. Using the terminal we can check that the file is now in our cluster directory /mcb5896/usr11/

<img align="center" src="/IMAGES/chekingtrasnferintocluster.PNG"/></a>


### C) HOMEWORK

**TASK: In the directory usr11 create a directory with the name chipmunk_fastq (using “mkdir” command), and check it with "ls" command  **

To copy the directory "chipmunk_fastq" and its content from " mcb5896/classFiles to ~/mcb5896/usr11" we use the code:

    Bash$: cp -a /home/CAM/mcb5896/classFiles/chipmunk_fastq/ /home/CAM/mcb5896/usr11/
    
In the image we can see that the directory has been copied

<img align="center" src="/IMAGES/chipmunkdir.PNG"/></a>

Check the content of the ~/usr11/chipmunk_fastq with “ls” command
We will be using this dataset for the next analysis using mothur

Content created on: November 21, 2019
