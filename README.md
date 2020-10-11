# libbpf-build-template

This repository serves as a template to help eBPF developers build tools written using libbpf. It has been pulled out of [bcc](github.com/iovisor/bcc) for the sake of simplicity. 

## How to use this template

- Generate your own `vmlinux.h` file:
    - `bpftool...`

- Place your bpf code in a file called `tools/<name>.bpf.c` extension. 

- Place your userspace code in a file called `tools/<name>.c`

- Include `<name>.skel.h` in your userspace code.

- Include `vmlinux.h` in your bpf code

- Add `<name>` to `'APPS'` in `Makefile`

- `make` from tools

- Your compiled binary will be compiled and placed in `tools`

## How this build works

The Makefile is complicated if you're not familiar with GNU Make. Here's a breakdown of what it's doing:

- Goes into `src/cc/libbpf` (loaded as a git submodule)


## Further reading
