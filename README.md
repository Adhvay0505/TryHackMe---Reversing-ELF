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



## Task 3
We shall use the ```strings``` command to extract text strings from the ELF executable

![Screenshot From 2025-06-15 13-48-24](https://github.com/user-attachments/assets/58caa39b-8d5c-431b-8620-0037d282a40b)

This seems to be a base64 encoded string, we need to decode it

![Screenshot From 2025-06-15 13-48-46](https://github.com/user-attachments/assets/bceba113-051c-460e-8140-38f7b825bcdd)



## Task 4
After downloding the task file and executing it, we find that it requires a password, that we have to reverse engineer

![Screenshot From 2025-06-15 13-50-08](https://github.com/user-attachments/assets/b41757fb-ac3c-4a1b-8d5a-9d29509caf49)

the string is hidden, we need to reverse engineer the binary, I used ```ltrace``` for this

![Screenshot From 2025-06-15 13-50-26](https://github.com/user-attachments/assets/17cc9240-9ea2-41a8-85d9-6f1d1dee6ec3)



## Task 5
We need to get the output ```Good game``` upon running the executable

![Screenshot From 2025-06-15 13-51-16](https://github.com/user-attachments/assets/24ad2d6b-c728-4aa0-aade-8abf38fd87a4)


Once again, we can try to reverse engineer this binary using ```ltrace``` 

![Screenshot From 2025-06-15 13-53-34](https://github.com/user-attachments/assets/34f918f4-cf5a-4e52-b1d2-67ec3c4ec5c3)

That reveals the input needed to get the output ```Good game```

![Screenshot From 2025-06-15 15-40-35](https://github.com/user-attachments/assets/33e985d1-cb9c-421f-85fd-f4a3536857dc)



## Task 6
It seems we need to read the source code to find the password

![Screenshot From 2025-06-15 13-54-08](https://github.com/user-attachments/assets/8eeb7338-7fb7-48e5-b82e-8c9d5dc34c11)

I used Ghidra to reverse engineer this binary and read the source

-Analyse the executable in Ghidra

-In the Symbol Tree window, we can see my_secure_test under the functions drop down menu, this seems interesting

![Screenshot From 2025-06-15 13-56-09](https://github.com/user-attachments/assets/6b48e001-86bd-48e5-9436-d65eaea7a2a6)

Decompile this file and it seems that the characters provided in the conditional statements could be the password, lets try it out

![Screenshot From 2025-06-15 13-56-32](https://github.com/user-attachments/assets/c4479f60-cfc7-48d8-b12f-79504b394518)



## Task 7
Running this executable provides a menu with 3 options

![Screenshot From 2025-06-15 13-57-22](https://github.com/user-attachments/assets/301dc9d7-ea67-4ce5-bbaa-760ef6fcd351)

Upon analysing this in Ghidra, we can see the main function under the functions dropdown menu contains an interesting ```else if``` statement

![Screenshot From 2025-06-15 13-58-32](https://github.com/user-attachments/assets/c1c15060-024e-4af0-b964-c1b0c5581f81)

This is a hexadecimal string, we can convert this to decimal using many tools, I decided to use RapidTables

![Screenshot From 2025-06-15 16-02-43](https://github.com/user-attachments/assets/4bc718f6-832f-4427-a949-65744e1dd9cf)

![Screenshot From 2025-06-15 13-59-32](https://github.com/user-attachments/assets/c956ce41-9fa9-4f04-84a1-1873b4fd6691)

This reveals the flag 🥂



## Task 8

Symbol Tree window > function drop down > main

![Screenshot From 2025-06-15 14-00-52](https://github.com/user-attachments/assets/b35f64fe-991f-4a93-86ce-5fb2be74401b)

This hexadecimal string grants access, we need to convert it to decimal format

![Screenshot From 2025-06-15 14-01-19](https://github.com/user-attachments/assets/bb5a5860-1ce6-4f7e-8441-a3ac29ec5175)

![Screenshot From 2025-06-15 14-01-37](https://github.com/user-attachments/assets/579e7714-dfce-4a29-93be-b0144b9168f5)

> *"The quieter you become, the more you are able to hear."*

