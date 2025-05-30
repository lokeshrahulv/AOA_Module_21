# EX 3D Pattern Matching
## AIM:
To write a python program to implement pattern matching on the given string using Brute Force algorithm.



## Algorithm
1. Start checking each letter of s1 with the first letter of s
2. If letters match, keep checking the next letters.
3. If letters don't match, move one step forward in s1 and restart checking.
4. If all letters of s2 match, return the starting position.
5. If no match is found till the end, return 0.  

## Program:
```
/*
Program to implement the Pattern Matching.
Developed by: ASHWIN KUMAR S
Register Number: 212222240013
*/
```
```py
def BF(s1,s2):
    i = 0
    j = 0
    while(i < len(s1) and j < len(s2)):
        if(s1[i] ==  s2[j]):
            i += 1
            j += 1
        else:
            i = i - j + 1
            j = 0
    if(j >= len(s2)):
        return i - len(s2)
    else:
        return 0
    #End here
if __name__ == "__main__":
    a1=input() 
    a2=input() 
    b=BF(a1,a2)
    print(b)
```

## Output:
![image](https://github.com/user-attachments/assets/a2f4fb17-09f0-4aab-9106-2705993bcb0a)





## Result:
The brute force substring search program executed successfully and returned the starting index of the match or 0 if no match was found.
