# Common Vulerabilites guide for C programmers
    most vulnerabilities in C are related to buffer overflows and string manipulation.
    
# gets()
## problem: gets() does not check for buffer length and always results in a vulnerability
    ```
#include <stdio.h>
int main () {
    char username[8];
    int allow = 0;
    printf external link("Enter your username, please: ");
    gets(username); // user inputs "malicious"
    if (grantAccess(username)) {
        allow = 1;
    }
    if (allow != 0) { // has been overwritten by the overflow of the username.
        privilegedAction();
    }
return 0;
}
    ```
     it does not know how big the array is, and it is impossible to determine this from the pointer alone. When the user enters their text, gets() will read all available data into the array, this will be fine if the user is sensible and enters less than 99 bytes. However, if they enter more than 99, gets() will not stop writing at the end of the array. Instead, it continues writing past the end and into memory it doesn't own.
## resultion: using fgets()

# strcpy
## problem: not check buffer lengths and may overwrite memory zone next to the zone.
## solution: using strncpy

# sprintf()
## problem: not check buffer
## solution: using snprinf

# printf and friends
##  problem:   all functions that take a "format string" as argument
        ```
        #FormatString.c
        #include <stdio.h>
        
        int main(int argc, char **argv) {
            char *secret = "This is a secret!\n";
        
            printf external link(argv[1]);
        
            return 0;
        }
        ```
## sultion: hardcode the format string. At least, never let it come directly from adny user's input.

# file opening
https://research.cs.wisc.edu/mist/presentations/kupsch_miller_secse08.pdf
https://arstechnica.com/information-technology/2015/08/how-security-flaws-work-the-buffer-overflow/
https://insecure.org/stf/smashstack.html
https://cs155.stanford.edu/papers/formatstring-1.2.pdf
http://phrack.org/issues/60/10.html
https://www.geeksforgeeks.org/memory-layout-of-c-program/
