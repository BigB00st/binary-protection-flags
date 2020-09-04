# GCC Protections
A table that lists and describes gcc flags that deal with protection mechanisms.


#

|  Flag |  Description  |
| ------------ | ------------ |
|  -fno-stack-protector | Disable stack canary  |
|  -no-pie |  Binary will not be **P**osition **I**ndependent **E**xecutable |
|  -Wl,-z,norelro |  Relocation read-only will be disabled |
| -z execstack | Stack will be executable, NX is disabled |
