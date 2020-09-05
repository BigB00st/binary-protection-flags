# Binary Protection Flags
Tables that list and describe gcc and linker flags that deal with protection mechanisms of linux binaries.


### Canary

| Flag | Description | 
| ------------ | ------------ |
| `-fno-stack-protector` | Canary is disabled |
| `-fstack-protector` | Canary is enabled for functions with potential vulnerable objects (default) | 
| `-fstack-protector-all` | Canary is enabled for all functions |

[Canary Reference](https://ctf-wiki.github.io/ctf-wiki/pwn/linux/mitigation/canary/)

### NX

|  Flag |  Description  |
| ------------ | ------------ |
| `-z noexecstack` | Data is not executable (default) |
| `-z execstack` | Disable NX, data is executable |


### PIE

|  Flag |  Description  |
| ------------ | ------------ |
| `-no-pie` |  Binary will **not** be **P**osition **I**ndependent **E**xecutable |
| `-pie` | Binary will be **P**osition **I**ndependent **E**xecutable (default) |

[PIE Reference](https://access.redhat.com/blogs/766093/posts/1975793)

### RELRO

|  Flag |  Description  |
| ------------ | ------------ |
| `-Wl,-z,norelro` |  **Rel**ocation **r**ead-**o**nly will be disabled |
| `-Wl,-z,relro` | Partial RELRO, forces the GOT to come before the BSS in memory (default) |
| `-Wl,-z,relro,-z,now` | Full RELRO, GOT will be read-only |

[RELRO Reference](https://www.redhat.com/en/blog/hardening-elf-binaries-using-relocation-read-only-relro)

### Fortify
|  Flag |  Description  |
| ------------ | ------------ |
| `-D_FORTIFY_SOURCE=0 -O0` | Disabled (default) |
| `-D_FORTIFY_SOURCE=1 -O1` | Perform checks on string and memory manipulation functions at compile time |
| `-D_FORTIFY_SOURCE=2 -O2` | Enabled, perform extra checks when employing various string and memory manipulation functions at run time |

Note: `-On` sets compiler optimization level **n**.
  
[Fortify Reference](https://access.redhat.com/blogs/766093/posts/1976213)

### ASLR
This is not a flag, but I decided to place this here either way. The commands below set ASLR for the entire system.

**Enable:**
```
echo 2 | sudo tee /proc/sys/kernel/randomize_va_space
```
**Disable:**
```
echo 0 | sudo tee /proc/sys/kernel/randomize_va_space
```

### Notes
 * Use [checksec](https://github.com/slimm609/checksec.sh) to view the protections of an existing binary.
 * Flags passed with `-Wl` and `-z`, are sent directly to the linker.

### Examples:
Compile binary with **NX** disabled:
```
gcc target.c -o target -z execstack
```

Compile binary without canary:
```
gcc target.c -o target -fno-stack-protector
```



