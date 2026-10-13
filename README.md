# 🗂️ File System — Operating Systems Fundamentals

<p>
  <img alt="C" src="https://img.shields.io/badge/C-1f2328?style=flat-square&logo=c&logoColor=white">
  <img alt="Course" src="https://img.shields.io/badge/Course-Operating%20Systems%20Fundamentals%20(FSO)-1f2328?style=flat-square">
  <img alt="Year" src="https://img.shields.io/badge/2024%2F25-2nd%20year%2C%201st%20semester-1f2328?style=flat-square">
</p>

Mini-project of *Fundamentos de Sistemas de Operação* (Operating Systems Fundamentals), Computer Science degree at **NOVA School of Science and Technology (FCT NOVA)**.

## About

A small **UNIX-like file system** stored on a simulated disk (a regular file split into 2 KB blocks). The disk has a superblock, a bitmap of free blocks, an **inode table** and data blocks holding file contents and directories. A shell (`fso-sh`) lets you explore a disk image.

The course provided the disk driver, the bitmap, the shell and the on-disk structures. Our job was to complete the file system in `fs.c`:

- **Path resolution** — walk directories from the root inode to find the inode of a path like `/dir1/file2`
- **`ls`** — list a directory's entries with their inode number, type and size
- **`open`, `close` and `read`** — an open-file table and reading a file's contents through its **11 direct block indexes and one indirect index block**

## Running it

Needs a C compiler and `make` (Linux or macOS).

```bash
make
./fso-sh small.dsk
```

```text
fso-sh> ls
listing dir / (inode 0):
ino:type bytes name
  1:D      128 dir1
  2:F      530 file1
  5:F     5562 file2
fso-sh> ls /dir1
listing dir /dir1 (inode 1):
ino:type bytes name
  3:D        0 dir1.1
  4:F      273 file2
fso-sh> copyout /file2 file2.txt
fso-sh> debug        ← superblock, block bitmap and inodes in use
fso-sh> exit
```

Other commands: `cat <path>`, `help`.

## What I learned

- How a file system lays out its data on disk: superblock, free-block bitmap, inodes and directory entries
- Mapping a byte offset in a file to a disk block through direct and indirect indexes
- Low-level C: packed structures, raw block I/O and careful buffer handling

## Credits

- **Miguel Carmo** ([@MCCProgrammer](https://github.com/MCCProgrammer))
- **Tomás Ramos Alves** ([@Alvesss04](https://github.com/Alvesss04))

`fso-sh.c`, `disk.c`/`disk.h`, `bitmap.c`/`bitmap.h`, `fs.h`, the `Makefile` and the `small.dsk` disk image were provided by the FSO teaching staff; `fs.c` was completed by us.

---

<sub>The assignment statement is not included in this repository, as it belongs to the course's teaching staff. This is a student project shared for portfolio purposes.</sub>
