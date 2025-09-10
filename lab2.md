# 🔧understanding how existing scripts in repo work

# 🔧script 1

  ```
 #!/bin/bash      - shebang
 echo "hello world!"     - printing hello world
 name="kohinoor singh"   - taking kohinoor singhvin variable name
 age=18    -  taking 18 in variable age 

 echo "My name is $name ansd I am $age year old."  - printing name and age
```
#### OUTPUt 
<img width="730" height="346" alt="Screenshot from 2025-09-10 22-01-16" src="https://github.com/user-attachments/assets/f0e5ae08-d6cc-4c90-88ea-5adf6471025d" />


![image](<Screenshot from 2025-09-10 22-02-35.png>)


# 🔧 script 2

```
#!/bin/bash        -shebang
a="kohinoor singh"           -taking kohinoor singh in the variable a
b=40                 -taking 40 in the variable b

if [ $a=kohinoor singh" ] && [ $b -gt 18 ]; then      -checking conditions and using an opreator and(&&)
    echo " you are adult "                     - printing you are adult
fi

if [ $a=" kohinoor singh" ] && [ $b -lt 18 ]; then       -checking conditions and using an opreator and(&&)
    echo "you are minor"                         - printing you are minor
fi

```
![image](<Screenshot from 2025-09-10 22-07-22.png>)
![image](<Screenshot from 2025-09-10 22-09-59.png>)


### 🔧 Q1 what is the purpose of #!/bin/bash at the top of the script

ANS-- the shebang line at the top of a script specifies the interpreter that should be used to the run the script.

### 🔧 Q2 how do you make a script executable?
ANS-- 1. add the shebang at the top
          2. give permission using the chmod command
          3. run the code.
