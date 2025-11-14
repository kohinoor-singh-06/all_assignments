# modifying script

## original script

```
#!/bin/bash        ---shebang
a="kohinoor"           ---taking vansh in the variable a
b=40                 ---taking 40 in the variable b

if [ $a="kohinoor" ] && [ $b -gt 18 ]; then      ---checking conditions and using an opreator and(&&)
    echo " you are adult "                     ---printing you are adult
fi

if [ $a=" akshat" ] && [ $b -lt 18 ]; then       ---checking conditions and using an opreator and(&&)
    echo "you are minor"                         --- printing you are minor
fi

```
<img width="660" height="238" alt="Screenshot from 2025-11-14 16-51-58" src="https://github.com/user-attachments/assets/a156c5e9-84f8-4e35-b514-367ee5262b4e" />


<img width="574" height="74" alt="Screenshot from 2025-11-14 16-54-50" src="https://github.com/user-attachments/assets/7f2df5dd-9c63-46e5-bef3-85a5d2ffa5cd" />



##  modified script

```
#!/bin/bash 
# prompt user for input

read -p "enter your name: " name      --- taking name from the user
read -p "enter your age: " age        --- taking age from the user

if [ $name="kohinoor" ] && [ $age -gt 18 ]; then    --- checking conditions with if and opreator and(&&)     
    echo " you are adult "                     --- printing (you are adult)
fi

if [ $name=" akshat" ] && [ $age -lt 18 ]; then  ----  checking conditions with if and opreator and(&&)      
    echo "you are minor"                         ---- printing (you are minor)
fi
```
## the difference between the original and modified script is that in the first one we check for fixed value and in the next case we check for all cases .

<img width="586" height="259" alt="Screenshot from 2025-11-14 17-00-55" src="https://github.com/user-attachments/assets/1474cf67-6071-4173-af10-c73ef2332153" />



## checking with differnt examples
#### output is :
<img width="580" height="310" alt="Screenshot from 2025-11-14 17-01-39" src="https://github.com/user-attachments/assets/f34c67e0-1ae5-4648-8d7e-eb89109871ac" />



### Q1=differnce between $1,$@ and $# in bash?

Ans-- 0 $1= this refers to positional parameters
         $@= represents all arguments passed to the script
         $#= returns the number of arguments passed

### Q2=what does exit 1 mean in the script
    
Ans-- general error (something went wrong) Or exit with error.
