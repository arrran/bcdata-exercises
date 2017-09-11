# bcdata-exercises
A collection of exercises completed during the BCDATA Workshop
#Bash

Bash shell
The Bash shell is the user interface for the GNU/Linux operating system. Bash is a command line interface (CLI) where a user types commands which are then executed by the computer. We use Bash commands and its programming language to:
navigate the file system
create, delete, edit, search, and view files and directories
manage users, permissions and networks
... and much more
The symbol $ denotes the Bash shell prompt in the examples below. See the following resources for more information about Linux and Bash:
GNU Bash official webpage
Introduction to Linux - A Hands on Guide by Machtelt Garrels
File system and paths
The file system in a GNU/Linux machine is a tree with the root directory (denoted by a slash /) at the top. A path is a unique location of a file or directory in the file system. An absolute path is a location traced from the root directory and begins with the slash /. A relative path is traced from the working directory in the Bash shell and does not begin with the slash /.
For example, suppose the top of my file system is:
/
bin
git
python
vim
boot
dev
etc
home
patrick
bcdata-workshop
day-1
math210
lib
The abolute path of the directory day-1 is /home/patrick/bcdata-workshop/day-1.
If the working directory of the Bash shell is /home/patrick, then the relative path of day-1 is bcdata-workshop/day-1.
The slashes within a path (ie. excluding the root) are called separators (since they separate the directory names in the path).
Common operations involve the working (current) directory, its parent directory, or the home directory and so we have convenient shortcuts to refer to these directories:
Shortcut	Directory
.	working (current) directory
..	parent directory
~	home directory
-	previous directory
For example, if the working directory of the Bash shell is /home/patrick/bcdata-workshop, then the path of math210 can be written as ../math210 and also ~/bcdata-workshop.
Bash commands
There are many powerful features of the Bash shell but, at the moment, we will only consider the most common Bash commands. For more information, see the Bash manual or A-Z Index of Bash commands.
Command	Description
pwd	print working directory
ls	list contents of directory
cd	change working directory
mkdir	create new directory
mv	move file to directory
cp	copy file to directory
rm	delete file (immediately and permanently!)
cat	show contents of file
less	scroll through the contents of file (press q to exit)
head	show top 10 lines in file
tail	show last 10 lines in file
wc	show number of lines, words, and bytes in a file
sort	sort lines in a file
curl	retrieve and output the contents of the file located at the specified URL
echo	display messages to screen
Many commands can be modified using options (or flags). For example, head displays the top 10 lines of a file but we can use the option -20 (or -n for any integer n) to display the top 20 lines:
$ head -20 file.txt
Use the option -l with wc to display the number of lines only in a file:
$ wc -l file.txt
Use the option -r with rm to remove the contents of a directory called my_directory:
$ rm -r my_directory
Use the option --help to display more information about a command. For example, to see more about information about ls, type the command:
$ ls --help
Standard input and output, pipes and redirections
The input to a Bash command is called standard input. The output of a Bash command is called standard output. Read more about standard input and output.
Use the pipe operator | to use the standard output of a command as the standard input into another command.
For example, to count the number of files and directories contained in the directory /bin (which contains program files), we can pipe the output of ls into the command wc -l:
$ ls /bin | wc -l
Use the > operator to write the standard output of a command to a file.
For example, to fetch a webpage from the internet and write the contents to a file, we can redirect the output of curl to a file called math.html:
$ curl http://www.math.ubc.ca > math.html
Use the >> operator to append the standard output of a command to a file.
For example, we can write lines to a file using echo:
$ echo "This is the first line" > file.txt
$ echo "Now we append another line" >> file.txt
Bash scripts
A Bash script is simply a text file (with extension .sh) containing Bash commands. We run a Bash script in the terminal using the bash command:
$ bash my_script.sh
We can also pass (positional) arguments into the script and refer to them in the script as $1, $2, etc. The variable $0 in the script refers to the file name of the script.
For example, create my_script.sh:
# This line is a comment
# my_script.sh
echo ...Running $0...
echo Creating directory $1
mkdir $1
echo Creating file $1/$2
touch $1/$2
echo Done!
Run the script:
$ bash my_script.sh test file.txt
The output is:
...Running my_script.sh...
Creating directory test
Creating file test/file.txt
Done!
and the result is a new directory named test containing an empty file file.txt.
More commands and wildcards
There are many more Bash commands. See the A-Z Index of Bash commands. A few very helpful commands are:
Command	Description
grep	search a file for specific text
find	search for files
cut	divide file into parts (columns)
rev	reverse lines of a file
Finally, we can apply Bash commands to more than one file at a time using the wildcard *. For example, we can simultaneously remove files named data-1.txt, data-2.txt, data-3.txt, data-4.txt,data-5.txt and data-6.txt:
$ rm data-*.txt
For more information, see http://www.linfo.org/wildcard.html.
Exercises
Exercise: Complete works of Shakespeare
Create a new directory calles shakespeare and navigate into it using cd.
Use curl and a redirection > to save the collected works of Shakespeare as a text file called complete_works.txt from the URL
https://www.math.ubc.ca/~pwalls/data/shakespeare.txt
Use grep and a redirection > to save all lines containing the word love as a text file called love.txt. How many lines are there? What is the first line? What is the last line? (Use the option grep -i to ignore uppercase/lowercase.)
Use grep and a redirection > to save all lines containing the word death as a text file called death.txt. How many lines are there? What is the first line? What is the last line?(Use the option grep -i to ignore uppercase/lowercase.)
Use grep and a redirection > to save all lines containing the word war as a text file called war.txt. How many lines are there? What is the first line? What is the last line?(Use the option grep -i to ignore uppercase/lowercase.)
Exercise: Headline news
Write a Bash script called headlines.sh which takes two parameters category and filename and fetches the headlines from that category from the CBC RSS feeds: http://www.cbc.ca/rss/. The script should write the result to a file named filename.txt
For example:
bash headlines.sh sports-nba new_sports_headlines
writes the file new_sports_headlines.txt:
Canada's Andrew Wiggins in line for $148M payday from T-Wolves
Steph Curry rebounds from strange start in pro golf debut
Canadian basketball star R.J. Barrett to jump a year ahead to enter college next year
3,459 kids help Kevin Durant land in the Guinness Book of World Records
Canada squeaks into semis at FIBA U-19 Women's World Cup
Cavaliers owner tries to diffuse Kyrie Irving trade demand
Lakers re-sign Canadian guard Tyler Ennis
Warriors' Draymond Green sued over alleged assault
Aislinn Konig catches fire as Canada upends Latvia at FIBA U19 Women's World Cup
Former MVP Derrick Rose agrees to deal with Cavs
Kyrie Irving wants out of Cleveland, asks for trade
John Wall, Wizards agree to $170M, 4-year extension
Pau Gasol agrees to 3-year deal with Spurs
Grizzlies sign Canadian forward Dillon Brooks
Manu Ginobili returns to Spurs for 16th season
Raptors happy to have 'sniper' Miles in the fold
NBA, Nike shelving home and road jersey designations
Masai Ujiri taking Giants of Africa camp to 6 countries
Raptors' restructuring continues; team makes Cory Joseph trade official
Raptors' restructuring officially begins with trade of Carroll
Hints:
Fetch and save the raw XML file using curl and >.
The headlines contain the tags <title>. Use grep to find them.
Use cut and rev and pipes | to trim the beginning and end of each line.
Save the result and print it to the screen.

