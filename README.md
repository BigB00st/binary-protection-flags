# Protection Mechanisms Cheat Sheet
Tables that list and describe gcc and linker flags that deal with protection mechanisms of linux binaries.


### Stack Protection (Canary)

| Flag | Description | 
| ------------ | ------------ |
| -fno-stack-protector | Canary is disabled |
| -fstack-protector | Canary is enabled for functions with potential vulnerable objects (default) | 
| -fstack-protector-all | Canary is enabled for all functions|

### Data Execution Prevention

|  Flag |  Description  |
| ------------ | ------------ |
| -z noexecstack | data is not executable (default) |
| -z execstack | Disable NX, data is executable |


### Position Independent Executable

|  Flag |  Description  |
| ------------ | ------------ |
|  -no-pie |  Binary will **not** be **P**osition **I**ndependent **E**xecutable |
| -pie | Binary will be **P**osition **I**ndependent **E**xecutable (default) |

### RELRO

|  Flag |  Description  |
| ------------ | ------------ |
|  -Wl,-z,norelro |  Relocation read-only will be disabled |
| -Wl,-z,relro | Partial RELRO, forces the GOT to come before the BSS in memory (default) |
| -Wl,-z,relro,-z,now | Full Relro, GOT will be read-only |


### Note
Flags passed with `-z`, are sent directly to the linker.

### Examples:
Compile binary with **NX** disabled:
```
gcc target.c -o target -z execstack
```

Compile binary without canary:
```
gcc target.c -o target -fno-stack-protector
```



