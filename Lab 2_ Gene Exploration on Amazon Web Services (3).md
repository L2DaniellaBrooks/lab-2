# Lab 2: Gene Exploration on Amazon Web Services

# Part I: Get Set up on AWS

Most bioinformatics software runs on Linux or unix (including Mac) operating systems. For this class we will work in a Linux environment. We will run Linux in a virtual cloud environment. [What is Linux?](https://www.linux.com/what-is-linux)

Specifically we will use [Amazon Web Services (AWS)](https://aws.amazon.com/). AWS is a cloud computing resource provider. We will run virtual Linux machines on AWS servers and then connecting through a text-based terminal. It is possible to connect to your AWS instance from computers anywhere in the world.

AWS is not free, but as a student in this class you get a $100 credit. 


## Get to the EC2 Dashboard in the AWS Conole
You will have recieved an invitation to AWS Academy. [Read more about AWS academy.](https://towardsaws.com/what-is-aws-academy-16f4f46a76da) 
Follow the invitation to sign up and sign in.

Go to our course: **AWS Academy Learner Lab - Foundation Services [18419]**
Select Module to start the course:
![](https://i.imgur.com/hrJCNNb.png)

Select "Learner Lab - Foundational Services":
![](https://i.imgur.com/B2eu4f7.png)

Click "Start Lab". 
Wait until it starts, then click the "AWS" button on the left:
![](https://i.imgur.com/VR0mSI7.png)
[The AWS button has a red dot next to it when you session is stopped, a yellow dot while it is starting, and a green dot when it is running.]

A new tab will open with the AWS Console!


## Creating your BIO312 instance

Click on the button:
![](https://i.imgur.com/xNPZNCK.png)
(You can also click on "EC2" or "EC2 Dashboard" and then "Launch Instance")
**Note: Next time you visit, you will *start* the instance we are going to *launch* today. The same instance will be used for all labs.**

Search for the Bio312 community AMI by typing "bio312":
![](https://i.imgur.com/Q9quEZc.png)

Select "Bio312-Summer2022" 
![](https://i.imgur.com/0BCpoXV.png)

**Change instance type to "t2.medium"**

![](https://i.imgur.com/iFtS0na.png)

Click: "Create new key pair"
![](https://i.imgur.com/OuaxIBd.png)

Give the key pair a name. For example, I called my key "summerKey". Click "create key pair."
![](https://i.imgur.com/YOhIhCE.png)


You will be asked to save this file to your computer.**SAVE IT SOMEWHERE THAT YOU CAN FIND IT!** You can save it in a few places, email it to yourself, etc. **You will need to access the saved file in later labs, but you won't be able to generate it again! This is your only chance to save it in a place you can find again!** My file is called summerKey.pem

> [GitHub]: What is the name of your key?
> bio312keypair 
> emailed to personal 

> [GitHub]: Where on your computer did you store your key? Will you be able to find it again? 
> downloads (on tads computer, emailed to sbu email)

Note: you should have 100GB of storage selected.

Check your settings and then click "Launch instance:"
![](https://i.imgur.com/WlWgaeT.png)

Click on the instance ID, on "instances" or on "view all instances."


![](https://i.imgur.com/7hfpPpF.png)

Once your instance state says "running", click on the instance id:
![](https://i.imgur.com/0kPtKse.png)
You may need to click refresh.

## Fastest way to access your instance: EC2 instance connect
Once your instance is running, you can click the "Connect" button to access EC2 instance connect.
![](https://i.imgur.com/9ttdzWr.png)

Be sure to change the user name to "ec2-user".
Then click connect.
![](https://i.imgur.com/nYmKtqx.png)

## Logging into your instance with AWS Cloudshell (or any other SSH terminal software)

If you are already logged in, you can skip to **START A SCREEN SESSION**.

Look for the public IP address and copy it:
![](https://i.imgur.com/DfjALzT.png)
In the pictured example, the public IP address is 34.230.81.106.
> [GitHub] What is your public IP address?

*Unless you attach a permanent IP address (which we will skip for now), the IP address will change every time you start your instance.*

### To launch AWS Cloudshell
There are lots of ways to connect to your instance. One relatively easy interface called AWS cloudshell. To access the cloudshell, click on the console icon at the top of the screen, circled in red here:
![](https://i.imgur.com/2V9DYP5.png)

Now, we need to upload your key.
Click "Actions" and then select "upload file":
![](https://i.imgur.com/Gkqn6rq.png)
Select the pem file that you created. For example, I called my key "summerKey.pem". Then, click "upload."

Note: EC2 instance connect and AWS Cloudshell do not produce very stable connections. In addition, they can't be used for transferring files.

### On Cloudshell or any other SSH Terminal software, continue here
*If you are using AWS Cloudshell ssh software such as terminal (on a mac) or [bitvise on a pc](https://www.bitvise.com/download-area) continue here.

#### For mac, linux, or cloudshell users:
After the file has uploaded, check that it is in your work area by typing the linux command "ls" and hitting return:
![](https://i.imgur.com/8xOSY37.png)

We can see all the file in your work area. For example, here summerKey.pem is listed.

Now, change the permissions of your pem file by typing:
```
chmod 400 yourKeyFile.pem
```
But replace yourKeyFile.pem with the name of *your* key file. For example:
![](https://i.imgur.com/S4uUnJ4.png)


Now, you can log into your instance using the command:
```
ssh -i yourKeyFile.pem ec2-user@public-ip-address
```
But, replace yourKeyFile.pem with the name of your key file.
Replace public-ip-address with the ip address of your instance.
For example:

 ![](https://i.imgur.com/KXX8Ygi.png)

and hit return.

**When asked if you want to accept the keypair, type "yes".**


## START A SCREEN SESSION
After logging into your instance, you should see:
![](https://i.imgur.com/O2FcinK.png)
Congratulations! You are logged into your instance!

In case you are disconnected from you session, please start a screen session by typing:
```
screen -dRR
```
and hitting return.
If you get locked out of a session and need to log back in or refresh, typing this again ``screen -dRR`` again will help you resume where you left off.


# Part II: Welcome to the Shell! Intro to navigation and some shell commands.

 - These are the commands we will learn in Part II: 

       pwd
       ls
       cd
       cat

In this lab, you will want to type (or copy and paste) anything that is in a code box into your terminal.
This needs to be typed at the prompt, which is waiting for input. Your prompt may look like this:

**Try copying and pasting (or typing) the following command (and then hitting return):** 

    echo 'Hello World'

That command is the traditional first command used in a computer science class. Congratulations!
Let's try another command, just for fun (and then hit return):

    cowsay 'Bio 312 is super fun!'

> [Blackboard] 1. What is the result of the above command?
it made a cow emoji 
Let's look at your command prompt again:
[ec2-user@ip-172-31 ~]
Note that the IP address shown for you (ip-###) is your private  address; it's not reachable over the Internet. You could use the private address for communication between instances, if you were running more than one (not something we will do).

Let’s find out where we are by running a command called **pwd** (which stands for “print working directory”). At any moment, our current working directory is our current default directory, i.e., the directory that the computer assumes we want to run commands in, unless we explicitly specify something else. 

	pwd

Here, the computer’s response is `/home/ec2-user`, which is the top level directory within your user directory: (You are the user ec2-user)

Let’s look at how our file system is organized. We can see what files and subdirectories are in this directory by running ls, which stands for “listing”. ls prints the names of the files and directories in the current directory in alphabetical order, arranged neatly into columns. Type the following command, and then hit return:

     ls

>[Blackboard] 2. What is the result of the above command?
>data  labs  miniconda3  tools

The command to change locations in our file system is `**cd**`, followed by a directory name to change our working directory. cd stands for “change directory”. Let’s say we want to change to the data directory that Dr. Rest set up. We can use the following command to get there (and then hit return):

    cd data

Type the command `**ls**` (followed by return) to list the contents of the directory. 

     ls

You should see one file, `animal.txt` 

A useful command to view the contents of a file is `cat`. 
 Take a look at what is in the file animal.txt with the following command (and then hitting return):

     cat animal.txt

>[Blackboard] 3. What is in the file animal.txt?
its an imge of a wolf made of keyboard characters 
Navigate back to your home directory by typing just cd (and hitting return):

    cd


# Part III: Use Git to clone this lab's repository to the local instance

Today, we will use git to clone a copy of this lab repository to your local machine (i.e. on aws). You will than push any changes you make, or files you add to the repository, back to your repository on GitHub. In addition, you can use this connection to transfer files to your instance.

First, copy and paste the following commands at the command prompt. But, replace "your username" with your username, for example "charlesdarwin123" (in quotes). [This will make your life easier going forward.]

    git config --global user.name "L2daniellabrooks" 
    git config --global credential.helper store  
    git config --global credential.helper cache 
    git config --global core.editor nano 


Next, you need to generate a PAT (personal access token).  In your web browser:

 1. Navigate to: https://github.com/settings/tokens    
 2. Click "Generate new token"    
 3. Add a note (e.g. for my Amazon instance),     
 4. select an expiration date (at least till the end of the semester.    
 5. check the box  "repo" under scopes    
 6. click "Generate token"   
 7.  Copy your token to the clipboard, and save it in a safe place. YOU WILL NEED TO ACCESS IT IN FUTURE LABS.

Now, on the command line, clone the lab2 repository. Look at the URL, above, of this GitHub repository. It will look something like: https://github.com/Bio312/lab2-myusername
Use the following command to **clone** the repository, which means downloading a local copy to work on.:
**NOTE again that myname below is your github username. **

	cd ~/labs
    git clone https://github.com/Bio312/lab2-L2daniellabrooks
  
You will be asked to enter your GitHub username and password. **Use the token you generated instead of your password.**

Git will now clone a copy of today's lab into a folder called lab2-myusername (where myname is your GitHub username). Go there (recall myusername is your github username):

    cd lab2-myusername

Take a look at what is in the folder using the `ls` command. You will see that this readme.md is present. A little later in the lab, you will add some more files . At the end of the lab, you will push the changes and files back into the online repository.

**Do all the work for this lab in this new folder you have cloned.** 


# Part IV - commands and command flags
You already know several commands. For example, you just used `ls` to look at the files in the lab2 directory. What if you want to list the files a different way? For example, what if you want to also see the size, modified date and time, and owner of the file? If you read the manual for the ls command, you will discover there is an option for this (`-l`):  [ls](https://www.cs.bu.edu/teaching/unix/reference/commands.html#ls)
To invoke this option we need to add a some information to the ls command - this is called a command flag. You will be using lots of command flags today!  Flags **modify the operation of a command**.
(from https://www.cs.bu.edu/teaching/unix/reference/vocab.html)

Command flags are typed at the prompt as part of a command. An example would be:

    ls -l

in which case the flag `-l` (minus ell, not one) gives a longer set of information. Flags alter the default behavior of commands. For example, the command, by default, just lists the names of files. With the `-l` flag, it gives you more information about each file (or directory).

Flags normally start with a minus sign (-) and consist of a single letter, like `-l` (i.e., ell) or a whole word, as in `-debug`. For commands that take only single letter flags, more than one flags can often, but not always, be combined. For example, `-l` and `-F` could be typed as `-l<SPACE>-F` or `-lF`. 

Because some flags turn features on/off, flags are sometimes called switches. In addition, they may be called options.

[Blackboard] 4. Use the command `cowsay` with and without the `-d` command flag. How does it change the appearance of the resulting image? Note: you must specify some dialogue; review question 1 above.
i had to enter it in as cowsay -d 'hello' the stuff in quotes is the dialogue you need
the cow died (xx tongue out)
# Part V. Exploring Hox-C5, as in Lab 1, but using a computer.

## Download the Genbank file for the entire scaffold that the gene is found on (NEMVEscaffold_61; NW_001834353.1)

 We will use the program `ncbi-acc-download` to grab files from Genbank

Read about it [here](https://github.com/kblin/ncbi-acc-download).

Or, type the following to learn about the command flags available: 

    ncbi-acc-download -h

Type the following command to download the Genbank file for the entire scaffold:

    ncbi-acc-download -F genbank NW_001834353.1

[Blackboard] 5. What did the `-F` flag do in the above command? (Hint: read through the help file to figure this out by using the -h command flag). 
it downloaded the file 
List the files you have in your directory.

    ls

### Use the `less` command to look at a file
Here is a new program to use: `less`. This is a really useful program!
Use the `less` command to look at the Genbank file. Press the space bar to go down, `p` to go up, or `q` to quit.

    less NW_001834353.1.gbk

>[Blackboard] 6. How does this file compare with the Genbank file for the scaffold you looked at in lab 1?
no feature annotations 
## Download the scaffold in FASTA format 
Another file format we will use this semester is called FASTA or fasta format. This usually contains just sequence information, rather than annotations or coordinates. The format is simple. For example:
```
>name of sequence
ACTGACTGACTGACTGACTG
``` 
**This is a format that will be on your midterm and final. So take a look at it again!**

Use the "fasta" uption to download the FASTA file for the scaffold:

    ncbi-acc-download -F fasta NW_001834353.1

> [Blackboard] 7. Try each of the following commands. Which commands work to look at the FASTA file you just downloaded? Choose all correct answers. 
> Why are these correct or incorrect? [GitHub]
> 
> ``more NW_001834353.1``
> failed 
> ``more NW_001834353.1.fa``
> worked 
> ``less NW_001834353.1.FA``
failed  
> ``less NW_001834353.1.fa``
> worked 
> ``cat NW_001834353.1.fa``
worked 
**Hints: use the space bar to scroll in ``more`` and ``less`` and use the letter ``q`` to quit.** 

## Download the scaffold annotations in GFF format 
GFF file format contains just information about the coordinates of the features. It doesn't include any sequence. Read about the GFF format [here](https://en.wikipedia.org/wiki/General_feature_format).
Download the GFF file for this scaffold:

    ncbi-acc-download -F gff3 NW_001834353.1

### Filter the GFF scaffold annotations for only for a single gene and single transcript  

We will use short script that Dr. Rest wrote to keep only lines in the GFF file that contain our gene of interest, LOC5514051 (which is the gene symbol for Hox-C5 in Nematostella). The name of the script is `filterGFF`. It expects two things after the command: gene symbol (in our case, LOC5514051), and the name of the scaffold's GFF file.  (Note: it doesn't use command flags)
Run this command:

    filterGFF LOC5514051 NW_001834353.1.gff
    
This will output three new GFF files: (1) a file with  the coordinates of all features for the gene of interest; (2) a file further filtered to just transcript variant X1 for our gene; (3) a file further fitered with only the CDS features.

## Use genometools to quantify exon and intron lengths

Let's use the useful package genometools. Read about it [here](http://genometools.org). We will use the stat functions of genometools (gt) to count some interesting characteristics of the gene we are interested in, such as the lengths of the introns (-intronlengthdistri) and exons (-exonlengthdistri). See more by typing `gt stat -help`

First, sort the gff file. In gt, the -o flag specifies the name o the output file. (You can read about the other flags by looking at the help file.)

    gt gff3 -sort  -tidy -force -o LOC5514051.sorted.gff LOC5514051.X1.gff
[you can safely ignore the warnings]
Then, ask gt to calculate the desired lengths. You can see we are requesting output for the distribution of gene lengths, exon lengths, etc.. 

    gt stat -genelengthdistri -exonlengthdistri -intronlengthdistri -cdslengthdistri -addintrons -force  -o LOC5514051.sorted.counts.gff LOC5514051.sorted.gff

The output file is specified by the `-o` flag. In the output, the exons are ordered by length, rather than where they fall in the genome. Look at the results using `less`.

> [Blackboard] 8. What is the length of the shortest exon? What is the length of the longest exon? What is the length of the shortest intron? What is the length of the longest intron?
asked Nabil: enter in less LOC5514051.sorted.counts.gff 
shortest exon:376
longest exon: 2080
shortest into: 2138
longest intron: 3590

  You can find more details about the output [here](http://genometools.org/libgenometools.html).

### Use genometools to count genes on the entire scaffold
Repeat the same analysis (i.e. gt stat to see the length distributions) for the full scaffold NW_001834353.1. 

    gt gff3 -sort -tidy -o NW_001834353.1.sorted.gff NW_001834353.1.gff
    
    gt stat -genelengthdistri -exonlengthdistri -intronlengthdistri -cdslengthdistri -addintrons -force -o NW_001834353.1.counts.txt NW_001834353.1.sorted.gff

Answer the following questions:

> [Blackboard] 9. How many genes are on the scaffold?
> 1073712
 How many of these genes are protein coding?
33307
 How many protein coding mRNAs are there?
 31794
*Hints: Look at the commands you used. You want to look at the output of the gt stat command. The output file is specified by the command option -o. Once you have figured out the name of the file, use the less command to look at the contents.*

> [Blackboard] 10. Why are there more mRNAs than genes? 


## Use bedtools to retrieve sequence of our desired regions
In Lab 1, you looked at the translation of the gene. Let's perform the same analysis at the command line from the raw scaffold file and annotations. This will involve two steps: retrieving the sequence, and then translating it.

Lets subset our isoform-specific GFF file to lines that contain the word "CDS"

    grep CDS LOC5514051.X1.gff > LOC5514051.X1.cds.gff


Let's retrieve the corresponding sequence into a FASTA file. As we will talk about more throughout this semester, FASTA format is another format to store sequences. You need to know this format for the midterm and final. Read about it [here](https://en.wikipedia.org/wiki/FASTA_format).

Bedtools are used for a wide variety of genome-scale analyses. Read about them [here](https://bedtools.readthedocs.io/en/latest/).
Here, we will use the command getfasta to retrieve the CDS sequence from the scaffold fasta, using the annotations from the GFF file. To get help for this command, type `bedtools getfasta`

    bedtools getfasta -s -fi NW_001834353.1.fa -fo LOC5514051.X1.cds.fa -bed LOC5514051.X1.cds.gff

Look at the output:

    less LOC5514051.X1.cds.fa

> [Blackboard] 11. What is the -s flag for? 
  
## Use functions from emboss to compile and translate the sequence
After looking at the fasta file, you will notice that the CDS sequence is split up by exon. Lets concatenate these all together using the union command from emboss (type `union -h` for info)

    union LOC5514051.X1.cds.fa -outseq LOC5514051.X1.cds.union.fa

Then run another emboss function called transeq:

    transeq LOC5514051.X1.cds.union.fa -outseq LOC5514051.X1.aa.fa

> [Blackboard] 12. What did the transeq function do?

Use `less` to look at the resulting file. Do you see the result that you expect? Compare it to what is found on Genbank. Is it the same? 

# Part VI. Save your history and push your files into the repository.

Save your command history:

      history > lab2.commandhistory.txt

 
Now, use the following commands to push all the files you have generated or changed to your remote repository:
 
     git add .
     git commit -a -m "Adding all new data files I generated in AWS to the repository."
     git pull --no-edit

And then:

```git push ```

Congratulations! You are now a bash warrior!


## Your remote repository will be graded.
Check your remote repository on github.com. Are all the files that you pushed from your instance there? You will be graded on whether they are all there!
In addition, be sure that you answered any [GitHub] questions in this markdown file, and that it is up to date in your repository.


# Step VII. Stop your instance

1.  Click instances on the left hand corner and select your running instance
    
2.  Click Actions then Instance State and then Stop
    
3.  When you are ready to work on your instance again change the state to Start!