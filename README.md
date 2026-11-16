# win-kernel-av

WIP custom Windows antivirus built from scratch. I started this project mainly to learn about Windows kernel development, OS internals, and how commercial AVs actually work under the hood without triggering PatchGuard.

**Disclaimer:** This is Ring 0 code. It will BSOD. Do not run the `.sys` file on your main machine, use a VM for testing.

## how it works

The architecture is split into two parts so the system doesn't freeze while scanning:

- **Driver (`/driver`):** A file system minifilter written in C. It hooks `IRP_MJ_CREATE` to intercept file executions, blocks the thread, and asks user-mode what to do.
- **Service (`/service`):** A C++ user-mode daemon. It gets the file path from the kernel, does the actual scanning (hashes/heuristics), and sends back an allow/block verdict.

## building

You'll need:
- Visual Studio 2022 (with C++ desktop dev)
- Windows SDK 
- Windows Driver Kit (WDK)

*Note: Make sure your SDK and WDK versions match exactly.*

## status
Just starting out. Setting up the minifilter skeleton and the communication ports. Code is messy.
