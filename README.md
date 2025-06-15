# TryHackMe — Reversing-ELF Writeup

## Task 1
To start off, lets download the task file 

![Screenshot From 2025-06-15 13-45-50](https://github.com/user-attachments/assets/3fee2c1c-1c68-4457-9e5d-cac925069fb0)
This is an ELF executable, its a type of binary file used primarily on Linux and UNIX-like systems. ELF stands for **Executable and Linkable Format**.

Lets make it executable and execute it to see what happens

![Screenshot From 2025-06-15 13-46-07](https://github.com/user-attachments/assets/4cb2ee5e-59e3-494f-a535-c4435c952c64)
For task 1, we get the flag straightaway, simply by executing the ELF executable, quite easy : D


## Task 2
Once again, we shall download the task file and execute it to see what happens

![Screenshot From 2025-06-15 13-46-38](https://github.com/user-attachments/assets/2ecb5d80-81fb-4d82-be38-233a6ccf0f64)

It requires a password, which we need to find

I used the ```strings``` command to to extract readable text strings from the binary 

![Screenshot From 2025-06-15 13-47-09](https://github.com/user-attachments/assets/df668cc9-eedb-408c-944a-408bd7e04e94)
This seems to be the password

![Screenshot From 2025-06-15 13-47-31](https://github.com/user-attachments/assets/6df62abc-4c06-48f2-8ed7-b2085657a292)
