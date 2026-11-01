---
layout:     post
title:      "C String Operations"
subtitle:   "language learning"
date:       2026-11-01 16:35
author:     "J2Fish"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - C
    - notebook
---
In the C language class at school, I realized that my I/O operations and basic string operation are quite weak. Thus I decided to learn them at that time. The following are my learning notes.

## **string operation in C language usually need `include <string.h>`**

1. A char array can only be initialized to string constant with "=". To assign a whole char array to it,we should use `strcpy(to, from)`.However, it won't check whether buffer is big enough to hold th source. If the source is bigger , it will lead to buffer overflow.
2. A char array can't be compared as an whole. We should use `strcmp(str1, str2)`

```C
strcmp(str1, str2) -> int
// thus, when str1 < str2 , it will return an integer < 0
// str1 > str2 -> int > 0
// str1 == str2 -> an int == 0
```

3. To find any char in char array, `strcspn(str, obj_char)` is a perfect choice. It will return the index of the char.
4. To slice an char array on a given delimiter, we can use ` strtok(str, obj_char)`

```C

//strtok() usage
//initialization
char* tk = strtok(str, obj_char);
//next tk
tk = strtok(NULL, obj_char); // NULL tells the func to coninue with the previous string
//Notably, strtok will cut the origin char array. If you don't want to revise your origin array, please copy an operate the ectype
```

## **The following are I/O operations**

1. **scanf(format, address)/printf(format, buf)**
   - Both of them need a format specifier `%[*][width][h/l/ll/L]type` the “*” in scanf means discard it after reading.
   - When we use scanf, be careful to "%s". Without a width limitation, buffer will overflow
   - scanf will ignore all blank characters untill meet an not blank character.
2. **sscanf(buf, format)** - the scanf used in char array, has all the features of scanf
3. **fgets(buf, sizeof buf, stdin)**  should always be used in read whole line.
   - It won't ignore any  blank characters, including "\n" "\\t" and so on and it will retain them.
   - Additionally, if the line longer than sizeof buf, it will be cut down
   - When it come to end ,it will return NULL.