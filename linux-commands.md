
# Linux Shell Command Summary

```
pwd ---> It will show present working directory
cd ---> to change the directory
cat ---> to open any file
touch <file name> ---> To create a file
vim <file name> ---> It creates and open the file
cat > <filename> ---> To enter text in the file It will conatin only present text
cat >> <filename> ---> To enter text but it will keep present and before text in the file
ls -l ---> long listing format in alphabatical order
ls -lr ---> long listing format in reverse order
ls -la ---> It will show all hidden files and floders
ls -lt ---> latest fies and floder on top
ls -ltr ---> latest files and floders on bottom
ls -lrth ---> convert bytes into kilo bytes
free -g ---> It will show memory usage
dh -h ---> It will show disk storage
mkdir <floder-name> ---> It creates floder
rmdir <floder-name> ---> It deletes the floder
rm -f <filename> ---> It removes the files 
rm -rf <floder-name> ---> It deletes the all files and floders with that floder
cp <source location > <destination location> ---> It copies floder and files from source to destination. Original files remains
mv <source location> <destination location> ---> It moves the files and floders. Original files/floders will be removed
wget <url> ---> It download the files with original name. The file will store under the present working directory
curl -o <filename> <url> ---> It will download and store the content with the provided name instaed of original name
curl <url> ---> It will show output in the terminal
curl -o <url> ---> It will download and store the output with original file name
head <filename> ---> It will give 10 lines from the top
tail <filename> ---> It will give bottom 10 lines 
cat <filename> | head -n2 ---> top 2 records
cat <filename> | tail -n2 ---> bottom 2 records

# Difference between curl <url> and wget
wget ---> Simpler for downloading files and automatically saves the files
curl ---> It is useful for complex tranfer. It supports CURD operations

# grep : It is used for searching text in the file
cat <filename> | grep <word> ---> It will open the file and it assign the output of the file to pipe it will take the output and search for the word you want to search
cat <filename> | grep -i <word> ---> It will give case sensitive and not case sensitive words
grep <word> <filename> ---> It will search the word

# From the url you want to take particular part. we can do using cut command
echo <url> | cut -d "/" -f1 ---> It will give 1st part from the url

echo ---> It will print the data in the file
| ---> It passes output to the next command
-d ---> This is delimiter
-f1 ---> select the 1st field

# AWK command
It reads input line by line. It do operation like filtering,calculations,printing and searching. It splites the lines into fields

awk 'pattern {action}' <filename>
action ---> Operation to perform
$0 ---> It will show entire file
$1,$2 ---> It will show 1st and 2nd field
NF ---> Number of fields
NR ---> It will show number of line
FS ---> Field separator
OFS ---> Output separator

awk '{print $0}' <filename> ---> It will show all records
awk '{print $1,$2}' <filename> ---> It will show 1st and 2nd records
awk '{print NF}' ---> It shows number of fileds
awk '{print NR}' ---> It will show number of lines
echo <url> | awk -F "/" '{print $1}' ---> It will give 1st filed fom the url
```
# VIM Editor

They are 3 types of modes  
1. Esc mode  
2. Insert mode  
3. Colon `:` mode  

---

## Command Mode

- `vim <filename>` → Create and open file  
- `:q!` → Exit file without saving  
- `:wq!` → Save the modified content and exit  
- `:set hlsearch` → Highlight the searched word  
- `:nohlsearch` → Remove the highlight  
- `:/<searchword>` → Search word from **top**  
- `:?<searchword>` → Search word from **bottom**  
- `:noh` → Remove highlight  
- `:set nu` → Enable line numbers  
- `:set nonu` → Disable line numbers  
- `<line number>d` → Delete a specific line  
- `%d` → Delete all content in the file  
- `<line-number>s/<searchword>/<replace-word>/` → Replace first occurrence in the line  
- `<line-number>s/<searchword>/<replace-word>/g` → Replace all occurrences in the line  
- `:%s/<searchword>/<replace-word>/g` → Replace all occurrences in the entire file  

---

## ESC Mode

- `u` → Undo the changes
- `gg`→ It will take to top of the file
- `shift+g`→ Takes to the bottom of the file
