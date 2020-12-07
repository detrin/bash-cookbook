# bash-cookbook

My personal cookbook for bash scripting.

## Links
https://wiki.bash-hackers.org/

## Basics

### Variables
```bash
NAME="Daniel"
echo $NAME
echo "$NAME"
echo "${NAME}!"
```
### Functions
```bash
get_name() {
  echo "Daniel"
}

echo "You are $(get_name)"
```
### Conditionals
```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi

```
### String manipulation
```bash
name="Daniel"
echo ${name}
echo ${name/D/d}    #=> "daniel" (substitution)
echo ${name:0:2}    #=> "Da" (slicing)
echo ${name::2}     #=> "Da" (slicing)
echo ${name::-1}    #=> "Danie" (slicing)
echo ${name:(-1)}   #=> "l" (slicing from right)
echo ${name:(-2):1} #=> "e" (slicing from right)
echo ${food:-Bread} #=> $food or "Bread"

length=2
echo ${name:0:length}  #=> "Da"

SRC="/path/to/foo.cpp"
BASE=${SRC##*/}   #=> "foo.cpp" (basepath)
DIR=${SRC%$BASE}  #=> "/path/to/" (dirpath)

${#FOO} 	#=> Length of $FOO

STR="HELLO WORLD!"
echo ${STR,}   #=> "hELLO WORLD!" (lowercase 1st letter)
echo ${STR,,}  #=> "hello world!" (all lowercase)

STR="hello world!"
echo ${STR^}   #=> "Hello world!" (uppercase 1st letter)
echo ${STR^^}  #=> "HELLO WORLD!" (all uppercase)

```
### Comments
```bash
# Single line comment
: '
This is a
multi line
comment
'
```
### Loops
```bash
# Basic for loop
for i in /etc/rc.*; do
  echo $i
done
# C-like for loop
for ((i = 0 ; i < 100 ; i++)); do
  echo $i
done
# Ranges
for i in {1..5}; do
    echo "Welcome $i"
done
for i in {5..50..5}; do
    echo "Welcome $i"
done
# Reading lines
cat file.txt | while read line; do
  echo $line
done
# Forever
while true; do
  ···
done
```
### Printf
```bash
printf "Hello %s, I'm %s" Sven Olga
#=> "Hello Sven, I'm Olga

printf "1 + 1 = %d" 2
#=> "1 + 1 = 2"

printf "This is how you print a float: %f" 2
#=> "This is how you print a float: 2.000000"
```
### Reading input
```bash
echo -n "Proceed? [y/n]: "
read ans
echo $ans

read -n 1 ans    # Just one character
```

## Jobs execution

### xargs
```bash
echo {1..10} | tr ' ' '\n' | xargs -I{} echo {}
echo {1..10} | tr ' ' '\n' | xargs -I{} -P4 echo {}
echo {1..10} | tr ' ' '\n' | xargs -I{} -P4 bash -c "sleep .$[ ( $RANDOM % 10 ) + 1 ]s; echo {}"
```
