Despite the fact that it took me a day to realize, this challenge has really nothing fancy going on.

The bug is here:

```c
if(fd=open("/home/mistake/password",O_RDONLY,0400) < 0){
                printf("can't open password %d\n", fd);
                return 0;
        }
```

The assignment sets fd to the result of the comparison, which is either 0 or 1. So if the file opens successfully, fd will be 0, which 
is stdin!

That means that the original password of pw_buf is read from the stdin.
Then we just need the second one to be the first one XORed with 0x1. (like a bit flip).

We also need it to be 10 characters long
we can for example do

AAAAAAAAAA
@@@@@@@@@@