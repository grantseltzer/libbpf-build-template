# libbpf-build-template

This repository serves as a template to help eBPF developers build tools written using libbpf. It has been pulled out of [bcc](github.com/iovisor/bcc) for the sake of simplicity. 

## How to use this template

- Generate your own `vmlinux.h` file:
    - `bpftool...`

- Place your bpf code in a file called `tools/<name>.bpf.c` extension. 

- Place your userspace code in a file called `tools/<name>.c`

- Include `<name>.skel.h` in your userspace code.

- Include `vmlinux.h` in your bpf code.

- Add `<name>` to `'APPS'` in `Makefile`.

- `make` from tools.

- Your compiled binary will be compiled and placed in `tools`.

- Follow `tools/example.*` if you get confused.

## How this build works

The Makefile is complicated if you're not familiar with GNU Make. Here's a breakdown of what it's doing:

- Goes into `src/cc/libbpf` (loaded as a git submodule)

- Creates `tools/.output/libbpf/staticobjs`

- Creates a handful of static objects from libbpf.

- Creates an archive of all those static objects called `libbpf.a`

- Installs libbpf header files to `tools/.output/bpf`

- Installs the libbpf package config file to `tools/.output/libbpf/libbpf.pc`

- Compiles bpf code to an object file using clang
`clang -g -O2 -target bpf -D__TARGET_ARCH_x86 -I.output -c example.bpf.c -o .output/example.bpf.o`

- Generates a skeleton of the bpf object file
`bin/bpftool gen skeleton .output/example.bpf.o > .output/example.skel.h`

- Compiles helper function object files with gcc

- Compiles your bpf userspace code and links it against the helper function object files

## Further reading

[BPF Portability and CO-RE](https://nakryiko.com/posts/bpf-portability-and-co-re/) by Andrii Nakryiko
