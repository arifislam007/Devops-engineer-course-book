# **Chapter 3: Shell Scripting Fundamentals**  

## **Introduction**  
Shell scripting is a powerful way to automate repetitive tasks, streamline system administration, and manage configurations in Linux environments. Bash (Bourne Again Shell) is the most widely used shell for scripting in Linux.  

In this chapter, we will cover:  
- Basics of Bash scripting  
- Creating and executing scripts  
- Using variables and user input  
- Implementing conditional statements and loops  
- Writing functions for modular scripts  

---

## **3.1 Introduction to Bash Scripting**  
A **shell script** is a text file containing a sequence of commands that can be executed as a program. Bash scripts help automate tasks such as system monitoring, backups, and software installations.  

### **Why Use Shell Scripting?**  
- Automates repetitive tasks  
- Simplifies complex commands  
- Reduces human error  
- Improves efficiency in DevOps workflows  

### **Creating and Running a Shell Script**  
1. Open a terminal and create a new script file using a text editor:  
   ```bash
   nano myscript.sh
   ```
2. Add the following lines:  
   ```bash
   #!/bin/bash
   echo "Hello, World!"
   ```
   - `#!/bin/bash` is called a **shebang** and specifies the interpreter for the script.  
3. Save the file (`CTRL + X`, then `Y`, then `Enter`).  
4. Give execute permission to the script:  
   ```bash
   chmod +x myscript.sh
   ```
5. Run the script:  
   ```bash
   ./myscript.sh
   ```
   Output:  
   ```
   Hello, World!
   ```

---

## **3.2 Using Variables in Bash**  
Variables in Bash store values that can be reused in the script.  

### **Defining Variables**  
```bash
name="Arif"
echo "Hello, $name!"
```
Output:  
```
Hello, Arif!
```

### **Reading User Input**  
```bash
echo "Enter your name: "
read user_name
echo "Welcome, $user_name!"
```

### **Using Command Substitution**  
```bash
current_date=$(date)
echo "Today's date is: $current_date"
```

---

## **3.3 Conditional Statements in Bash**  
Conditional statements allow scripts to make decisions.  

### **If-Else Statement**  
```bash
#!/bin/bash
echo "Enter a number: "
read num
if [ $num -gt 10 ]; then
    echo "The number is greater than 10."
else
    echo "The number is 10 or less."
fi
```

### **Comparison Operators**  
| Operator | Description |
|----------|------------|
| `-eq`   | Equal to  |
| `-ne`   | Not equal to  |
| `-gt`   | Greater than  |
| `-lt`   | Less than  |
| `-ge`   | Greater than or equal to  |
| `-le`   | Less than or equal to  |

---

## **3.4 Loops in Bash**  
Loops are used to execute a block of code multiple times.  

### **For Loop**  
```bash
for i in 1 2 3 4 5; do
    echo "Iteration: $i"
done
```

### **While Loop**  
```bash
count=1
while [ $count -le 5 ]; do
    echo "Count: $count"
    count=$((count + 1))
done
```

---

## **3.5 Functions in Bash**  
Functions allow reusability of code.  

### **Defining a Function**  
```bash
greet() {
    echo "Hello, $1!"
}
greet "Arif"
```
Output:  
```
Hello, Arif!
```

### **Function with Return Value**  
```bash
add_numbers() {
    result=$(( $1 + $2 ))
    echo $result
}
sum=$(add_numbers 5 10)
echo "Sum: $sum"
```

---

## **3.6 Hands-on Exercises**  
1. Write a script that asks for a username and prints a personalized greeting.  
2. Create a script that checks if a file exists and prints an appropriate message.  
3. Write a script to display numbers from 1 to 10 using a loop.  
4. Develop a script that takes two numbers as input and returns their sum.  

---

## **Conclusion**  
In this chapter, we explored the fundamentals of Bash scripting, including variables, user input, conditional statements, loops, and functions. Mastering shell scripting is crucial for automation and system administration.  

In the next chapter, we will dive into **System Administration**, where we will learn about package management, process management, and system monitoring.
