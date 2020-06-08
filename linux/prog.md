# Linux Programming Notes
📅 [2020-05-31](https://arunsah.github.io/meta/changelog#2020-05-31) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

---

## Table of Content

Chapter 1: History and Standards
- 1.1 A Brief History of UNIX and C
- 1.2 A Brief History of Linux
- 1.2.1 The GNU Project
- 1.2.2 The Linux Kernel
- 1.3 Standardization
- 1.3.1 The C Programming Language
- 1.3.2 The First POSIX Standards
- 1.3.3 X/Open Company and The Open Group
- 1.3.4 SUSv3 and POSIX.1-2001
- 1.3.5 SUSv4 and POSIX.1-2008
- 1.3.6 UNIX Standards Timeline
- 1.3.7 Implementation Standards
- 1.3.8 Linux, Standards, and the Linux Standard Base
- 1.4 Summary

Chapter 2: Fundamental Concepts
- 2.1 The Core Operating System: The Kernel
- 2.2 The Shell
- 2.3 Users and Groups
- 2.4 Single Directory Hierarchy, Directories, Links, and Files
- 2.5 File I/O Model
- 2.6 Programs
- 2.7 Processes
- 2.8 Memory Mappings
- 2.9 Static and Shared Libraries
- 2.10 Interprocess Communication and Synchronization
- 2.11 Signals
- 2.12 Threads
- 2.13 Process Groups and Shell Job Control
- 2.14 Sessions, Controlling Terminals, and Controlling Processes
- 2.15 Pseudoterminals
- 2.16 Date and Time
- 2.17 Client-Server Architecture
- 2.18 Realtime
- 2.19 The /proc File System
- 2.20 Summary

Chapter 3: System Programming Concepts
- 3.1 System Calls
- 3.2 Library Functions
- 3.3 The Standard C Library; The GNU C Library (glibc)
- 3.4 Handling Errors from System Calls and Library Functions
- 3.5 Notes on the Example Programs in This Book
- 3.5.1 Command-Line Options and Arguments
- 3.5.2 Common Functions and Header Files
- 3.6 Portability Issues
- 3.6.1 Feature Test Macros
- 3.6.2 System Data Types
- 3.6.3 Miscellaneous Portability Issues
- 3.7 Summary
- 3.8 Exercise

Chapter 4: File I/O: The Universal I/O Model
- 4.1 Overview
- 4.2 Universality of I/O
- 4.3 Opening a File: open()
- 4.3.1 The open() flags Argument
- 4.3.2 Errors from open()
- 4.3.3 The creat() System Call
- 4.4 Reading from a File: read()
- 4.5 Writing to a File: write()
- 4.6 Closing a File: close()
- 4.7 Changing the File Offset: lseek()
- 4.8 Operations Outside the Universal I/O Model: ioctl()
- 4.9 Summary
- 4.10 Exercises

Chapter 5: File I/O: Further Details
- 5.1 Atomicity and Race Conditions
- 5.2 File Control Operations: fcntl()
- 5.3 Open File Status Flags
- 5.4 Relationship Between File Descriptors and Open Files
- 5.5 Duplicating File Descriptors
- 5.6 File I/O at a Specified Offset: pread() and pwrite()
- 5.7 Scatter-Gather I/O: readv() and writev()
- 5.8 Truncating a File: truncate() and ftruncate()
- 5.9 Nonblocking I/O
- 5.10 I/O on Large Files
- 5.11 The /dev/fd Directory
- 5.12 Creating Temporary Files
- 5.13 Summary
- 5.14 Exercises

Chapter 6: Processes
- 6.1 Processes and Programs
- 6.2 Process ID and Parent Process ID
- 6.3 Memory Layout of a Process
- 6.4 Virtual Memory Management
- 6.5 The Stack and Stack Frames
- 6.6 Command-Line Arguments (argc, argv)
- 6.7 Environment List
- 6.8 Performing a Nonlocal Goto: setjmp() and longjmp()
- 6.9 Summary
- 6.10 Exercises

Chapter 7: Memory Allocation
- 7.1 Allocating Memory on the Heap
- 7.1.1 Adjusting the Program Break: brk() and sbrk()
- 7.1.2 Allocating Memory on the Heap: malloc() and free()
- 7.1.3 Implementation of malloc() and free()
- 7.1.4 Other Methods of Allocating Memory on the Heap
- 7.2 Allocating Memory on the Stack: alloca()
- 7.3 Summary
- 7.4 Exercises

Chapter 8: Users and Groups
- 8.1 The Password File: /etc/passwd
- 8.2 The Shadow Password File: /etc/shadow
- 8.3 The Group File: /etc/group
- 8.4 Retrieving User and Group Information
- 8.5 Password Encryption and User Authentication
- 8.6 Summary
- 8.7 Exercises

Chapter 9: Process Credentials
- 9.1 Real User ID and Real Group ID
- 9.2 Effective User ID and Effective Group ID
- 9.3 Set-User-ID and Set-Group-ID Programs
- 9.4 Saved Set-User-ID and Saved Set-Group-ID
- 9.5 File-System User ID and File-System Group ID
- 9.6 Supplementary Group IDs
- 9.7 Retrieving and Modifying Process Credentials
- 9.7.1 Retrieving and Modifying Real, Effective, and Saved Set IDs
- 9.7.2 Retrieving and Modifying File-System IDs
- 9.7.3 Retrieving and Modifying Supplementary Group IDs
- 9.7.4 Summary of Calls for Modifying Process Credentials
- 9.7.5 Example: Displaying Process Credentials
- 9.8 Summary
- 9.9 Exercises

Chapter 10: Time
- 10.1 Calendar Time
- 10.2 Time-Conversion Functions
- 10.2.1 Converting time_t to Printable Form
- 10.2.2 Converting Between time_t and Broken-Down Time
- 10.2.3 Converting Between Broken-Down Time and Printable Form
- 10.3 Timezones
- 10.4 Locales
- 10.5 Updating the System Clock
- 10.6 The Software Clock (Jiffies)
- 10.7 Process Time
- 10.8 Summary
- 10.9 Exercise

Chapter 11: System Limits and Options
- 11.1 System Limits
- 11.2 Retrieving System Limits (and Options) at Run Time
- 11.3 Retrieving File-Related Limits (and Options) at Run Time
- 11.4 Indeterminate Limits
- 11.5 System Options
- 11.6 Summary
- 11.7 Exercises

Chapter 12: System and Process Information
- 12.1 The /proc File System
- 12.1.1 Obtaining Information About a Process: /proc/PID
- 12.1.2 System Information Under /proc
- 12.1.3 Accessing /proc Files
- 12.2 System Identification: uname()
- 12.3 Summary
- 12.4 Exercises

Chapter 13: File I/O Buffering
- 13.1 Kernel Buffering of File I/O: The Buffer Cache
- 13.2 Buffering in the stdio Library
- 13.3 Controlling Kernel Buffering of File I/O
- 13.4 Summary of I/O Buffering
- 13.5 Advising the Kernel About I/O Patterns
- 13.6 Bypassing the Buffer Cache: Direct I/O
- 13.7 Mixing Library Functions and System Calls for File I/O
- 13.8 Summary
- 13.9 Exercises

Chapter 14: File Systems
- 14.1 Device Special Files (Devices)
- 14.2 Disks and Partitions
- 14.3 File Systems
- 14.4 I-nodes
- 14.5 The Virtual File System (VFS)
- 14.6 Journaling File Systems
- 14.7 Single Directory Hierarchy and Mount Points
- 14.8 Mounting and Unmounting File Systems
- 14.8.1 Mounting a File System: mount()
- 14.8.2 Unmounting a File System: umount() and umount2()
- 14.9 Advanced Mount Features
- 14.9.1 Mounting a File System at Multiple Mount Points
- 14.9.2 Stacking Multiple Mounts on the Same Mount Point
- 14.9.3 Mount Flags That Are Per-Mount Options
- 14.9.4 Bind Mounts
- 14.9.5 Recursive Bind Mounts
- 14.10 A Virtual Memory File System: tmpfs
- 14.11 Obtaining Information About a File System: statvfs()
- 14.12 Summary
- 14.13 Exercise

Chapter 15: File Attributes
- 15.1 Retrieving File Information: stat()
- 15.2 File Timestamps
- 15.2.1 Changing File Timestamps with utime() and utimes()
- 15.2.2 Changing File Timestamps with utimensat() and futimens()
- 15.3 File Ownership
- 15.3.1 Ownership of New Files
- 15.3.2 Changing File Ownership: chown(), fchown(), and lchown()
- 15.4 File Permissions
- 15.4.1 Permissions on Regular Files
- 15.4.2 Permissions on Directories
- 15.4.3 Permission-Checking Algorithm
- 15.4.4 Checking File Accessibility: access()
- 15.4.5 Set-User-ID, Set-Group-ID, and Sticky Bits
- 15.4.6 The Process File Mode Creation Mask: umask()
- 15.4.7 Changing File Permissions: chmod() and fchmod()
- 15.5 I-node Flags (ext2 Extended File Attributes)
- 15.6 Summary
- 15.7 Exercises

Chapter 16: Extended Attributes
- 16.1 Overview
- 16.2 Extended Attribute Implementation Details
- 16.3 System Calls for Manipulating Extended Attributes
- 16.4 Summary
- 16.5 Exercise

Chapter 17: Access Control Lists
- 17.1 Overview
- 17.2 ACL Permission-Checking Algorithm
- 17.3 Long and Short Text Forms for ACLs
- 17.4 The ACL_MASK Entry and the ACL Group Class
- 17.5 The getfacl and setfacl Commands
- 17.6 Default ACLs and File Creation
- 17.7 ACL Implementation Limits
- 17.8 The ACL API
- 17.9 Summary
- 17.10 Exercise

Chapter 18: Directories and Links
- 18.1 Directories and (Hard) Links
- 18.2 Symbolic (Soft) Links
- 18.3 Creating and Removing (Hard) Links: link() and unlink()
- 18.4 Changing the Name of a File: rename()
- 18.5 Working with Symbolic Links: symlink() and readlink()
- 18.6 Creating and Removing Directories: mkdir() and rmdir()
- 18.7 Removing a File or Directory: remove()
- 18.8 Reading Directories: opendir() and readdir()
- 18.9 File Tree Walking: nftw()
- 18.10 The Current Working Directory of a Process
- 18.11 Operating Relative to a Directory File Descriptor
- 18.12 Changing the Root Directory of a Process: chroot()
- 18.13 Resolving a Pathname: realpath()
- 18.14 Parsing Pathname Strings: dirname() and basename()
- 18.15 Summary
- 18.16 Exercises

Chapter 19: Monitoring File Events
- 19.1 Overview
- 19.2 The inotify API
- 19.3 inotify Events
- 19.4 Reading inotify Events
- 19.5 Queue Limits and /proc Files
- 19.6 An Older System for Monitoring File Events: dnotify
- 19.7 Summary
- 19.8 Exercise

Chapter 20: Signals: Fundamental Concepts
- 20.1 Concepts and Overview
- 20.2 Signal Types and Default Actions
- 20.3 Changing Signal Dispositions: signal()
- 20.4 Introduction to Signal Handlers
- 20.5 Sending Signals: kill()
- 20.6 Checking for the Existence of a Process
- 20.7 Other Ways of Sending Signals: raise() and killpg()
- 20.8 Displaying Signal Descriptions
- 20.9 Signal Sets
- 20.10 The Signal Mask (Blocking Signal Delivery)
- 20.11 Pending Signals
- 20.12 Signals Are Not Queued
- 20.13 Changing Signal Dispositions: sigaction()
- 20.14 Waiting for a Signal: pause()
- 20.15 Summary
- 20.16 Exercises

Chapter 21: Signals: Signal Handlers
- 21.1 Designing Signal Handlers
- 21.1.1 Signals Are Not Queued (Revisited)
- 21.1.2 Reentrant and Async-Signal-Safe Functions
- 21.1.3 Global Variables and the sig_atomic_t Data Type
- 21.2 Other Methods of Terminating a Signal Handler
- 21.2.1 Performing a Nonlocal Goto from a Signal Handler
- 21.2.2 Terminating a Process Abnormally: abort()
- 21.3 Handling a Signal on an Alternate Stack: sigaltstack()
- 21.4 The SA_SIGINFO Flag
- 21.5 Interruption and Restarting of System Calls
- 21.6 Summary
- 21.7 Exercise

Chapter 22: Signals: Advanced Features
- 22.1 Core Dump Files
- 22.2 Special Cases for Delivery, Disposition, and Handling
- 22.3 Interruptible and Uninterruptible Process Sleep States
- 22.4 Hardware-Generated Signals
- 22.5 Synchronous and Asynchronous Signal Generation
- 22.6 Timing and Order of Signal Delivery
- 22.7 Implementation and Portability of signal()
- 22.8 Realtime Signals
- 22.8.1 Sending Realtime Signals
- 22.8.2 Handling Realtime Signals
- 22.9 Waiting for a Signal Using a Mask: sigsuspend()
- 22.10 Synchronously Waiting for a Signal
- 22.11 Fetching Signals via a File Descriptor
- 22.12 Interprocess Communication with Signals
- 22.13 Earlier Signal APIs (System V and BSD)
- 22.14 Summary
- 22.15 Exercises

Chapter 23: Timers and Sleeping
- 23.1 Interval Timers
- 23.2 Scheduling and Accuracy of Timers
- 23.3 Setting Timeouts on Blocking Operations
- 23.4 Suspending Execution for a Fixed Interval (Sleeping)
- 23.4.1 Low-Resolution Sleeping: sleep()
- 23.4.2 High-Resolution Sleeping: nanosleep()
- 23.5 POSIX Clocks
- 23.5.1 Retrieving the Value of a Clock: clock_gettime()
- 23.5.2 Setting the Value of a Clock: clock_settime()
- 23.5.3 Obtaining the Clock ID of a Specific Process or Thread
- 23.5.4 Improved High-Resolution Sleeping: clock_nanosleep()
- 23.6 POSIX Interval Timers
- 23.6.1 Creating a Timer: timer_create()
- 23.6.2 Arming and Disarming a Timer: timer_settime()
- 23.6.3 Retrieving the Current Value of a Timer: timer_gettime()
- 23.6.4 Deleting a Timer: timer_delete()
- 23.6.5 Notification via a Signal
- 23.6.6 Timer Overruns
- 23.6.7 Notification via a Thread
- 23.7 Timers That Notify via File Descriptors: The timerfd API
- 23.8 Summary
- 23.9 Exercises

Chapter 24: Process Creation
- 24.1 Overview of fork(), exit(), wait(), and execve()
- 24.2 Creating a New Process: fork()
- 24.2.1 File Sharing Between Parent and Child
- 24.2.2 Memory Semantics of fork()
- 24.3 The vfork() System Call
- 24.4 Race Conditions After fork()
- 24.5 Avoiding Race Conditions by Synchronizing with Signals
- 24.6 Summary
- 24.7 Exercises

Chapter 25: Process Termination
- 25.1 Terminating a Process: _exit() and exit()
- 25.2 Details of Process Termination
- 25.3 Exit Handlers
- 25.4 Interactions Between fork(), stdio Buffers, and _exit()
- 25.5 Summary
- 25.6 Exercise

Chapter 26: Monitoring Child Processes
- 26.1 Waiting on a Child Process
- 26.1.1 The wait() System Call
- 26.1.2 The waitpid() System Call
- 26.1.3 The Wait Status Value
- 26.1.4 Process Termination from a Signal Handler
- 26.1.5 The waitid() System Call
- 26.1.6 The wait3() and wait4() System Calls
- 26.2 Orphans and Zombies
- 26.3 The SIGCHLD Signal
- 26.3.1 Establishing a Handler for SIGCHLD
- 26.3.2 Delivery of SIGCHLD for Stopped Children
- 26.3.3 Ignoring Dead Child Processes
- 26.4 Summary
- 26.5 Exercises

Chapter 27: Program Execution
- 27.1 Executing a New Program: execve()
- 27.2 The exec() Library Functions
- 27.2.1 The PATH Environment Variable
- 27.2.2 Specifying Program Arguments as a List
- 27.2.3 Passing the Caller’s Environment to the New Program
- 27.2.4 Executing a File Referred to by a Descriptor: fexecve()
- 27.3 Interpreter Scripts
- 27.4 File Descriptors and exec()
- 27.5 Signals and exec()
- 27.6 Executing a Shell Command: system()
- 27.7 Implementing system()
- 27.8 Summary
- 27.9 Exercises

Chapter 28: Process Creation and Program Execution in More Detail
- 28.1 Process Accounting
- 28.2 The clone() System Call
- 28.2.1 The clone() flags Argument
- 28.2.2 Extensions to waitpid() for Cloned Children
- 28.3 Speed of Process Creation
- 28.4 Effect of exec() and fork() on Process Attributes
- 28.5 Summary
- 28.6 Exercise

Chapter 29: Threads: Introduction
- 29.1 Overview
- 29.2 Background Details of the Pthreads API
- 29.3 Thread Creation
- 29.4 Thread Termination
- 29.5 Thread IDs
- 29.6 Joining with a Terminated Thread
- 29.7 Detaching a Thread
- 29.8 Thread Attributes
- 29.9 Threads Versus Processes
- 29.10 Summary
- 29.11 Exercises

Chapter 30: Threads: Thread Synchronization
- 30.1 Protecting Accesses to Shared Variables: Mutexes
- 30.1.1 Statically Allocated Mutexes
- 30.1.2 Locking and Unlocking a Mutex
- 30.1.3 Performance of Mutexes
- 30.1.4 Mutex Deadlocks
- 30.1.5 Dynamically Initializing a Mutex
- 30.1.6 Mutex Attributes
- 30.1.7 Mutex Types
- 30.2 Signaling Changes of State: Condition Variables
- 30.2.1 Statically Allocated Condition Variables
- 30.2.2 Signaling and Waiting on Condition Variables
- 30.2.3 Testing a Condition Variable’s Predicate
- 30.2.4 Example Program: Joining Any Terminated Thread
- 30.2.5 Dynamically Allocated Condition Variables
- 30.3 Summary
- 30.4 Exercises

Chapter 31: Threads: Thread Safety and Per-Thread Storage
- 31.1 Thread Safety (and Reentrancy Revisited)
- 31.2 One-Time Initialization
- 31.3 Thread-Specific Data
- 31.3.1 Thread-Specific Data from the Library Function’s Perspective
- 31.3.2 Overview of the Thread-Specific Data API
- 31.3.3 Details of the Thread-Specific Data API
- 31.3.4 Employing the Thread-Specific Data API
- 31.3.5 Thread-Specific Data Implementation Limits
- 31.4 Thread-Local Storage
- 31.5 Summary
- 31.6 Exercises

Chapter 32: Threads: Thread Cancellation
- 32.1 Canceling a Thread
- 32.2 Cancellation State and Type
- 32.3 Cancellation Points
- 32.4 Testing for Thread Cancellation
- 32.5 Cleanup Handlers
- 32.6 Asynchronous Cancelability
- 32.7 Summary

Chapter 33: Threads: Further Details
- 33.1 Thread Stacks
- 33.2 Threads and Signals
- 33.2.1 How the UNIX Signal Model Maps to Threads
- 33.2.2 Manipulating the Thread Signal Mask
- 33.2.3 Sending a Signal to a Thread
- 33.2.4 Dealing with Asynchronous Signals Sanely
- 33.3 Threads and Process Control
- 33.4 Thread Implementation Models
- 33.5 Linux Implementations of POSIX Threads
- 33.5.1 LinuxThreads
- 33.5.2 NPTL
- 33.5.3 Which Threading Implementation?
- 33.6 Advanced Features of the Pthreads API
- 33.7 Summary
- 33.8 Exercises

Chapter 34: Process Groups, Sessions, and Job Control
- 34.1 Overview
- 34.2 Process Groups
- 34.3 Sessions
- 34.4 Controlling Terminals and Controlling Processes
- 34.5 Foreground and Background Process Groups
- 34.6 The SIGHUP Signal
- 34.6.1 Handling of SIGHUP by the Shell
- 34.6.2 SIGHUP and Termination of the Controlling Process
- 34.7 Job Control
- 34.7.1 Using Job Control Within the Shell
- 34.7.2 Implementing Job Control
- 34.7.3 Handling Job-Control Signals
- 34.7.4 Orphaned Process Groups (and SIGHUP Revisited)
- 34.8 Summary
- 34.9 Exercises

Chapter 35: Process Priorities and Scheduling
- 35.1 Process Priorities (Nice Values)
- 35.2 Overview of Realtime Process Scheduling
- 35.2.1 The SCHED_RR Policy
- 35.2.2 The SCHED_FIFO Policy
- 35.2.3 The SCHED_BATCH and SCHED_IDLE Policies
- 35.3 Realtime Process Scheduling API
- 35.3.1 Realtime Priority Ranges
- 35.3.2 Modifying and Retrieving Policies and Priorities
- 35.3.3 Relinquishing the CPU
- 35.3.4 The SCHED_RR Time Slice
- 35.4 CPU Affinity
- 35.5 Summary
- 35.6 Exercises

Chapter 36: Process Resources
- 36.1 Process Resource Usage
- 36.2 Process Resource Limits
- 36.3 Details of Specific Resource Limits
- 36.4 Summary
- 36.5 Exercises

Chapter 37: Daemons
- 37.1 Overview
- 37.2 Creating a Daemon
- 37.3 Guidelines for Writing Daemons
- 37.4 Using SIGHUP to Reinitialize a Daemon
- 37.5 Logging Messages and Errors Using syslog
- 37.5.1 Overview
- 37.5.2 The syslog API
- 37.5.3 The /etc/syslog.conf File
- 37.6 Summary
- 37.7 Exercise

Chapter 38: Writing Secure Privileged Programs
- 38.1 Is a Set-User-ID or Set-Group-ID Program Required?
- 38.2 Operate with Least Privilege
- 38.3 Be Careful When Executing a Program
- 38.4 Avoid Exposing Sensitive Information
- 38.5 Confine the Process
- 38.6 Beware of Signals and Race Conditions
- 38.7 Pitfalls When Performing File Operations and File I/O
- 38.8 Don’t Trust Inputs or the Environment
- 38.9 Beware of Buffer Overruns
- 38.10 Beware of Denial-of-Service Attacks
- 38.11 Check Return Statuses and Fail Safely
- 38.12 Summary
- 38.13 Exercises

Chapter 39: Capabilities
- 39.1 Rationale for Capabilities
- 39.2 The Linux Capabilities
- 39.3 Process and File Capabilities
- 39.3.1 Process Capabilities
- 39.3.2 File Capabilities
- 39.3.3 Purpose of the Process Permitted and Effective Capability Sets
- 39.3.4 Purpose of the File Permitted and Effective Capability Sets
- 39.3.5 Purpose of the Process and File Inheritable Sets
- 39.3.6 Assigning and Viewing File Capabilities from the Shell
- 39.4 The Modern Capabilities Implementation
- 39.5 Transformation of Process Capabilities During exec()
- 39.5.1 Capability Bounding Set
- 39.5.2 Preserving root Semantics
- 39.6 Effect on Process Capabilities of Changing User IDs
- 39.7 Changing Process Capabilities Programmatically
- 39.8 Creating Capabilities-Only Environments
- 39.9 Discovering the Capabilities Required by a Program
- 39.10 Older Kernels and Systems Without File Capabilities
- 39.11 Summary
- 39.12 Exercise

Chapter 40: Login Accounting
- 40.1 Overview of the utmp and wtmp Files
- 40.2 The utmpx API
- 40.3 The utmpx Structure
- 40.4 Retrieving Information from the utmp and wtmp Files
- 40.5 Retrieving the Login Name: getlogin()
- 40.6 Updating the utmp and wtmp Files for a Login Session
- 40.7 The lastlog File
- 40.8 Summary
- 40.9 Exercises

Chapter 41: Fundamentals of Shared Libraries
- 41.1 Object Libraries
- 41.2 Static Libraries
- 41.3 Overview of Shared Libraries
- 41.4 Creating and Using Shared Libraries—A First Pass
- 41.4.1 Creating a Shared Library
- 41.4.2 Position-Independent Code
- 41.4.3 Using a Shared Library
- 41.4.4 The Shared Library Soname
- 41.5 Useful Tools for Working with Shared Libraries
- 41.6 Shared Library Versions and Naming Conventions
- 41.7 Installing Shared Libraries
- 41.8 Compatible Versus Incompatible Libraries
- 41.9 Upgrading Shared Libraries
- 41.10 Specifying Library Search Directories in an Object File
- 41.11 Finding Shared Libraries at Run Time
- 41.12 Run-Time Symbol Resolution
- 41.13 Using a Static Library Instead of a Shared Library
- 41.14 Summary
- 41.15 Exercise

Chapter 42: Advanced Features of Shared Libraries
- 42.1 Dynamically Loaded Libraries
- 42.1.1 Opening a Shared Library: dlopen()
- 42.1.2 Diagnosing Errors: dlerror()
- 42.1.3 Obtaining the Address of a Symbol: dlsym()
- 42.1.4 Closing a Shared Library: dlclose()
- 42.1.5 Obtaining Information About Loaded Symbols: dladdr()
- 42.1.6 Accessing Symbols in the Main Program
- 42.2 Controlling Symbol Visibility
- 42.3 Linker Version Scripts
- 42.3.1 Controlling Symbol Visibility with Version Scripts
- 42.3.2 Symbol Versioning
- 42.4 Initialization and Finalization Functions
- 42.5 Preloading Shared Libraries
- 42.6 Monitoring the Dynamic Linker: LD_DEBUG
- 42.7 Summary
- 42.8 Exercises

Chapter 43: Interprocess Communication Overview
- 43.1 A Taxonomy of IPC Facilities
- 43.2 Communication Facilities
- 43.3 Synchronization Facilities
- 43.4 Comparing IPC Facilities
- 43.5 Summary
- 43.6 Exercises

Chapter 44: Pipes and FIFOs
- 44.1 Overview
- 44.2 Creating and Using Pipes
- 44.3 Pipes as a Method of Process Synchronization
- 44.4 Using Pipes to Connect Filters
- 44.5 Talking to a Shell Command via a Pipe: popen()
- 44.6 Pipes and stdio Buffering
- 44.7 FIFOs
- 44.8 A Client-Server Application Using FIFOs
- 44.9 Nonblocking I/O
- 44.10 Semantics of read() and write() on Pipes and FIFOs
- 44.11 Summary
- 44.12 Exercises

Chapter 45: Introduction to System V IPC
- 45.1 API Overview
- 45.2 IPC Keys
- 45.3 Associated Data Structure and Object Permissions
- 45.4 IPC Identifiers and Client-Server Applications
- 45.5 Algorithm Employed by System V IPC get Calls
- 45.6 The ipcs and ipcrm Commands
- 45.7 Obtaining a List of All IPC Objects
- 45.8 IPC Limits
- 45.9 Summary
- 45.10 Exercises

Chapter 46: System V Message Queues
- 46.1 Creating or Opening a Message Queue
- 46.2 Exchanging Messages
- 46.2.1 Sending Messages
- 46.2.2 Receiving Messages
- 46.3 Message Queue Control Operations
- 46.4 Message Queue Associated Data Structure
- 46.5 Message Queue Limits
- 46.6 Displaying All Message Queues on the System
- 46.7 Client-Server Programming with Message Queues
- 46.8 A File-Server Application Using Message Queues
- 46.9 Disadvantages of System V Message Queues
- 46.10 Summary
- 46.11 Exercises

Chapter 47: System V Semaphores
- 47.1 Overview
- 47.2 Creating or Opening a Semaphore Set
- 47.3 Semaphore Control Operations
- 47.4 Semaphore Associated Data Structure
- 47.5 Semaphore Initialization
- 47.6 Semaphore Operations
- 47.7 Handling of Multiple Blocked Semaphore Operations
- 47.8 Semaphore Undo Values
- 47.9 Implementing a Binary Semaphores Protocol
- 47.10 Semaphore Limits
- 47.11 Disadvantages of System V Semaphores
- 47.12 Summary
- 47.13 Exercises

Chapter 48: System V Shared Memory
- 48.1 Overview
- 48.2 Creating or Opening a Shared Memory Segment
- 48.3 Using Shared Memory
- 48.4 Example: Transferring Data via Shared Memory
- 48.5 Location of Shared Memory in Virtual Memory
- 48.6 Storing Pointers in Shared Memory
- 48.7 Shared Memory Control Operations
- 48.8 Shared Memory Associated Data Structure
- 48.9 Shared Memory Limits
- 48.10 Summary
- 48.11 Exercises

Chapter 49: Memory Mappings
- 49.1 Overview
- 49.2 Creating a Mapping: mmap()
- 49.3 Unmapping a Mapped Region: munmap()
- 49.4 File Mappings
- 49.4.1 Private File Mappings
- 49.4.2 Shared File Mappings
- 49.4.3 Boundary Cases
- 49.4.4 Memory Protection and File Access Mode Interactions
- 49.5 Synchronizing a Mapped Region: msync()
- 49.6 Additional mmap() Flags
- 49.7 Anonymous Mappings
- 49.8 Remapping a Mapped Region: mremap()
- 49.9 MAP_NORESERVE and Swap Space Overcommitting
- 49.10 The MAP_FIXED Flag
- 49.11 Nonlinear Mappings: remap_file_pages()
- 49.12 Summary
- 49.13 Exercises

Chapter 50: Virtual Memory Operations
- 50.1 Changing Memory Protection: mprotect()
- 50.2 Memory Locking: mlock() and mlockall()
- 50.3 Determining Memory Residence: mincore()
- 50.4 Advising Future Memory Usage Patterns: madvise()
- 50.5 Summary
- 50.6 Exercises

Chapter 51: Introduction to POSIX IPC
- 51.1 API Overview
- 51.2 Comparison of System V IPC and POSIX IPC
- 51.3 Summary

Chapter 52: POSIX Message Queues
- 52.1 Overview
- 52.2 Opening, Closing, and Unlinking a Message Queue
- 52.3 Relationship Between Descriptors and Message Queues
- 52.4 Message Queue Attributes
- 52.5 Exchanging Messages
- 52.5.1 Sending Messages
- 52.5.2 Receiving Messages
- 52.5.3 Sending and Receiving Messages with a Timeout
- 52.6 Message Notification
- 52.6.1 Receiving Notification via a Signal
- 52.6.2 Receiving Notification via a Thread
- 52.7 Linux-Specific Features
- 52.8 Message Queue Limits
- 52.9 Comparison of POSIX and System V Message Queues
- 52.10 Summary
- 52.11 Exercises

Chapter 53: POSIX Semaphores
- 53.1 Overview
- 53.2 Named Semaphores
- 53.2.1 Opening a Named Semaphore
- 53.2.2 Closing a Semaphore
- 53.2.3 Removing a Named Semaphore
- 53.3 Semaphore Operations
- 53.3.1 Waiting on a Semaphore
- 53.3.2 Posting a Semaphore
- 53.3.3 Retrieving the Current Value of a Semaphore
- 53.4 Unnamed Semaphores
- 53.4.1 Initializing an Unnamed Semaphore
- 53.4.2 Destroying an Unnamed Semaphore
- 53.5 Comparisons with Other Synchronization Techniques
- 53.6 Semaphore Limits
- 53.7 Summary
- 53.8 Exercises

Chapter 54: POSIX Shared Memory
- 54.1 Overview
- 54.2 Creating Shared Memory Objects
- 54.3 Using Shared Memory Objects
- 54.4 Removing Shared Memory Objects
- 54.5 Comparisons Between Shared Memory APIs
- 54.6 Summary
- 54.7 Exercise

Chapter 55: File Locking
- 55.1 Overview
- 55.2 File Locking with flock()
- 55.2.1 Semantics of Lock Inheritance and Release
- 55.2.2 Limitations of flock()
- 55.3 Record Locking with fcntl()
- 55.3.1 Deadlock
- 55.3.2 Example: An Interactive Locking Program
- 55.3.3 Example: A Library of Locking Functions
- 55.3.4 Lock Limits and Performance
- 55.3.5 Semantics of Lock Inheritance and Release
- 55.3.6 Lock Starvation and Priority of Queued Lock Requests
- 55.4 Mandatory Locking
- 55.5 The /proc/locks File
- 55.6 Running Just One Instance of a Program
- 55.7 Older Locking Techniques
- 55.8 Summary
- 55.9 Exercises

Chapter 56: Sockets: Introduction
- 56.1 Overview
- 56.2 Creating a Socket: socket()
- 56.3 Binding a Socket to an Address: bind()
- 56.4 Generic Socket Address Structures: struct sockaddr
- 56.5 Stream Sockets
- 56.5.1 Listening for Incoming Connections: listen()
- 56.5.2 Accepting a Connection: accept()
- 56.5.3 Connecting to a Peer Socket: connect()
- 56.5.4 I/O on Stream Sockets
- 56.5.5 Connection Termination: close()
- 56.6 Datagram Sockets
- 56.6.1 Exchanging Datagrams: recvfrom() and sendto()
- 56.6.2 Using connect() with Datagram Sockets
- 56.7 Summary

Chapter 57: Sockets: UNIX Domain
- 57.1 UNIX Domain Socket Addresses: struct sockaddr_un
- 57.2 Stream Sockets in the UNIX Domain
- 57.3 Datagram Sockets in the UNIX Domain
- 57.4 UNIX Domain Socket Permissions
- 57.5 Creating a Connected Socket Pair: socketpair()
- 57.6 The Linux Abstract Socket Namespace
- 57.7 Summary
- 57.8 Exercises

Chapter 58: Sockets: Fundamentals of TCP/IP Networks
- 58.1 Internets
- 58.2 Networking Protocols and Layers
- 58.3 The Data-Link Layer
- 58.4 The Network Layer: IP
- 58.5 IP Addresses
- 58.6 The Transport Layer
- 58.6.1 Port Numbers
- 58.6.2 User Datagram Protocol (UDP)
- 58.6.3 Transmission Control Protocol (TCP)
- 58.7 Requests for Comments (RFCs)
- 58.8 Summary

Chapter 59: Sockets: Internet Domains
- 59.1 Internet Domain Sockets
- 59.2 Network Byte Order
- 59.3 Data Representation
- 59.4 Internet Socket Addresses
- 59.5 Overview of Host and Service Conversion Functions
- 59.6 The inet_pton() and inet_ntop() Functions
- 59.7 Client-Server Example (Datagram Sockets)
- 59.8 Domain Name System (DNS)
- 59.9 The /etc/services File
- 59.10 Protocol-Independent Host and Service Conversion
- 59.10.1 The getaddrinfo() Function
- 59.10.2 Freeing addrinfo Lists: freeaddrinfo()
- 59.10.3 Diagnosing Errors: gai_strerror()
- 59.10.4 The getnameinfo() Function
- 59.11 Client-Server Example (Stream Sockets)
- 59.12 An Internet Domain Sockets Library
- 59.13 Obsolete APIs for Host and Service Conversions
- 59.13.1 The inet_aton() and inet_ntoa() Functions
- 59.13.2 The gethostbyname() and gethostbyaddr() Functions
- 59.13.3 The getservbyname() and getservbyport() Functions
- 59.14 UNIX Versus Internet Domain Sockets
- 59.15 Further Information
- 59.16 Summary
- 59.17 Exercises

Chapter 60: Sockets: Server Design
- 60.1 Iterative and Concurrent Servers
- 60.2 An Iterative UDP echo Server
- 60.3 A Concurrent TCP echo Server
- 60.4 Other Concurrent Server Designs
- 60.5 The inetd (Internet Superserver) Daemon
- 60.6 Summary
- 60.7 Exercises

Chapter 61: Sockets: Advanced Topics
- 61.1 Partial Reads and Writes on Stream Sockets
- 61.2 The shutdown() System Call
- 61.3 Socket-Specific I/O System Calls: recv() and send()
- 61.4 The sendfile() System Call
- 61.5 Retrieving Socket Addresses
- 61.6 A Closer Look at TCP
- 61.6.1 Format of a TCP Segment
- 61.6.2 TCP Sequence Numbers and Acknowledgements
- 61.6.3 TCP State Machine and State Transition Diagram
- 61.6.4 TCP Connection Establishment
- 61.6.5 TCP Connection Termination
- 61.6.6 Calling shutdown() on a TCP Socket
- 61.6.7 The TIME_WAIT State
- 61.7 Monitoring Sockets: netstat
- 61.8 Using tcpdump to Monitor TCP Traffic
- 61.9 Socket Options
- 61.10 The SO_REUSEADDR Socket Option
- 61.11 Inheritance of Flags and Options Across accept()
- 61.12 TCP Versus UDP
- 61.13 Advanced Features
- 61.13.1 Out-of-Band Data
- 61.13.2 The sendmsg() and recvmsg() System Calls
- 61.13.3 Passing File Descriptors
- 61.13.4 Receiving Sender Credentials
- 61.13.5 Sequenced-Packet Sockets
- 61.13.6 SCTP and DCCP Transport-Layer Protocols
- 61.14 Summary
- 61.15 Exercises

Chapter 62: Terminals
- 62.1 Overview
- 62.2 Retrieving and Modifying Terminal Attributes
- 62.3 The stty Command
- 62.4 Terminal Special Characters
- 62.5 Terminal Flags
- 62.6 Terminal I/O Modes
- 62.6.1 Canonical Mode
- 62.6.2 Noncanonical Mode
- 62.6.3 Cooked, Cbreak, and Raw Modes
- 62.7 Terminal Line Speed (Bit Rate)
- 62.8 Terminal Line Control
- 62.9 Terminal Window Size
- 62.10 Terminal Identification
- 62.11 Summary
- 62.12 Exercises

Chapter 63: Alternative I/O Models
- 63.1 Overview
- 63.1.1 Level-Triggered and Edge-Triggered Notification
- 63.1.2 Employing Nonblocking I/O with Alternative I/O Models
- 63.2 I/O Multiplexing
- 63.2.1 The select() System Call
- 63.2.2 The poll() System Call
- 63.2.3 When Is a File Descriptor Ready?
- 63.2.4 Comparison of select() and poll()
- 63.2.5 Problems with select() and poll()
- 63.3 Signal-Driven I/O
- 63.3.1 When Is “I/O Possible” Signaled?
- 63.3.2 Refining the Use of Signal-Driven I/O
- 63.4 The epoll API
- 63.4.1 Creating an epoll Instance: epoll_create()
- 63.4.2 Modifying the epoll Interest List: epoll_ctl()
- 63.4.3 Waiting for Events: epoll_wait()
- 63.4.4 A Closer Look at epoll Semantics
- 63.4.5 Performance of epoll Versus I/O Multiplexing
- 63.4.6 Edge-Triggered Notification
- 63.5 Waiting on Signals and File Descriptors
- 63.5.1 The pselect() System Call
- 63.5.2 The Self-Pipe Trick
- 63.6 Summary
- 63.7 Exercises

Chapter 64: Pseudoterminals
- 64.1 Overview
- 64.2 UNIX 98 Pseudoterminals
- 64.2.1 Opening an Unused Master: posix_openpt()
- 64.2.2 Changing Slave Ownership and Permissions: grantpt()
- 64.2.3 Unlocking the Slave: unlockpt()
- 64.2.4 Obtaining the Name of the Slave: ptsname()
- 64.3 Opening a Master: ptyMasterOpen()
- 64.4 Connecting Processes with a Pseudoterminal: ptyFork()
- 64.5 Pseudoterminal I/O
- 64.6 Implementing script(1)
- 64.7 Terminal Attributes and Window Size
- 64.8 BSD Pseudoterminals
- 64.9 Summary
- 64.10 Exercises

Appendix
- Appendix A: Tracing System Calls
- Appendix B: Parsing Command-Line Options
- Appendix C: Casting the NULL Pointer
- Appendix D: Kernel Configuration
- Appendix E: Further Sources of Information
- Appendix F: Solutions to Selected Exercises


## Chapter 0. Hello World C Program

```c
#include<stdio.h>
int main()
{
   int a, b, c;
   printf("Enter two numbers to add, separated by a space: ");
   scanf("%d%d",&a,&b);
   c = a + b;
   printf("The sum of equals %d\n",c);
   return 0;
}
// gcc hello.c -o hello
// ./hello

```

```shell

$ gcc hello.c -o hello
mario@mario:~/dev/sysprog/linuxproginterface/introduction$ ./hello 
Enter two numbers to add, separated by a space: 1 3
The sum of equals 4
mario@mario:~/dev/sysprog/linuxproginterface/introduction$ ^C
```

[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 1: History and Standards
📅 [2020-06-08](https://arunsah.github.io/meta/changelog#2020-06-08) 🖊️ [@arunsah](https://github.com/arunsah) 🧭 [Pune, India](https://en.wikipedia.org/wiki/Hinjawadi)

### 1.0 Introduction
- Linux is a member of UNIX family of OS.
- UNIX was not controlled by single entity by group of orgs (commercial and non-commercial) who contributed to its growth.
	- It leads to divergences of features which happens the portability of program.
	- Later standards was derived.
	- Classic UNIX were Bell Lab UNIX and its branches System V and BSD.
- UNIX denotes OS which passes the official conformance test for Single UNIXSpecification (SUS) , rights are granted by The Open Group (UNIX trademark holder) to those OS to be branded as UNIX.
	- FreeBSD and Linux (free UNIX implementations) have not obtained this branding.
	- UNIX may also mean to denote systems that are like classic UNIX such as Linux

### 1.1 A Brief History of UNIX and C
- 1969, Ken Thompson (Bell Lab, AT&T division) implemented UNIX in ASM for Digital PDP-7 minicomputer.
- 1970, UNIX was rewritten in ASM for Digital PDP-11.
- UNIX name and many idea (`tree structure fs`, `shell`, files as unstructured streams of bytes) was from MULTICS.
- MULTICS (Multiplexed Information and Computing Service) was an earlier OS by AT&T, MIT and GE.
- Dennis Ritchie (early collaborator on UNIX) designed and implemented `C` programming language.
	- `C` followed by `B` (interpreted language).
	- `B` was developed by Thompson that drew ideas from `BCPL`.
- 1973, UNIX kernel was written in `C` (matured) entirely.
	- This made `C` popular as system programming language as it was build for it.
		- Other languages were developed primarily for different purposes and were backed by large committees:
			- FORTRAN for mathematical computation.
			- COBOL for commercial system processing streams of record-oriented data.
- 1977-78, UNIX was first ported to HW other that PDP-11.
	- Dennis Ritchie and Steve Johnson ported to Interdata 8/32
	- Richard Miller (University of Wollongong, Australia) ported it to Interdata 7/32.
	- Berkeley Digital VAX port was based on (earlier, 1978) port by John Reiser and Tom London. 
		- Known as 32V, it was same as PDP-11 UNIX 7e with larger address space and wider data type.

###### UNIX Editions (1969-79)
- 1e, Nov 1971:
	- Running on PDP-11.
	- Had FORTRAN compiler.
	- Tools such as: `ar`, `cat`, `chmod`, `chown`, `cp`, `dc`, `ed`, `find`, `ln`, `ls`, `mail`, `mkdir`, `mv`, `rm`, `sb`, `su`, `who`
- 2e, Jun 1972:
	- Running on 10 machines at AT&T.
- 3e, Feb 1973:
	- Includes `C` compiler
	- `pipe` were implemented
- 4e, Nov 1973:
	- Fully implemented in `C`.
- 5e, Jun 1974:
	- Widely used outside AT&T.

- Dennis Ritchie’s home page (http://www.cs.bell-labs.com/who/dmr/index.html) provides a pointer to an online version of this paper, as well as [Ritchie & Thompson, 1974], and has many other pieces of UNIX history.

###### AT&T
- Sanctioned by US govt for monopoly on US Telephone system.
- Settled terms prevent it from selling software.
- From UNIX 6e, it license UNIX (documentation, kernel source 10k lines of code) to universities for nominal distribution fee. This further popularise UNIX and use of OS.
- 1977, UNIX was running on 500 sites (125 universities in US and other countries).

###### Birth of BSD and System V
- 1979 Jan, UNIX 7e provided enhanced fs and system reliability.
	- Tools contained:
		- `awk`
		- `make`
		- `sed`
		- `tar`
		- `uucp`
		- Bourne shell
		- FORTRAN 77 compiler.
	- UNIX diverged into variant: BSD and System V.

###### BSD (Berkeley Software Distribution)
- Thompson spent 1975-76 as visiting professor at University of California, Berkeley (UoC-B).
- With graduate students added new features to UNIX. Bill Joy one of students confounded Sun Microsystems (early entry in UNIX workstation market).
	- `C` shell
	- `vi` editor
	- Berkeley Fast File System
	- `sendmail`
	- PASCAL compiler
	- Virtual Memory management on new Digital VAX architecture.
- Under BSD, the version of UNIX includes source was widely distributed.
	- Early release BSD and 2BSD were distributed new tools not complete UNIX.
	- 1979 Dec, 3BSD was full UNIX distro.
	- 1983, 4.2BSD by Computer System Research Group at UoC-B.
		- Complete implementation of TCP/IP
		- Socket API
		- Variety of networking tools.
		- It formed basis for SunOS (1983, 1st release) UNIX variant sold by Sun.
	- 1986, 4.3BSD
	- 1993, 4.4BSD

###### System V
- US antitrust legislation forced breakup of AT&T effective in 1982, after which it was no longer held monopoly on telephone system, permitted to market UNIX resulted release of System-III.
- AT&T UNIX Support Group (USG) employed 100s developer to enhance UNIX:
	- 1983, System V Release 1.
	- series of other releases
	- 1989, System V Release 4, incorporated many features from BSD (including networking)
- System V was licensed to commercial vendors who used it as basis of their UNIX implementation. 

###### Explosion of Variants
- By 1980, UNIX was available in range of commercial implementation on various HW and academia.
	- SunOS by Sun, later Solaris
	- Ultrix and OSF/1 by Digital, after series of renaming and acquisitions HP Tru64 UNIX
	- AIX by IMB
	- HP-UX by HP.
	- NeXTStep by NeXT
	- A/AU for Apple Macintosh and Microsoft
	- XENIX by SCO for Intel x86-32
- Vendor locking was big issue and switching was expensive.


### 1.2 A Brief History of Linux

- Linux refer to UNIX like OS. Linux kernel is a part of it.
- Many of component in Linux distro dated before Linux Kernel.

#### 1.2.1 The GNU Project
- 1984, Richard Stallman (MIT) started work for *free* UNIX implementation.
	- Free was legally rather than financially. http://www.gnu.org/philosophy/free-sw.html
	- Started GNU (recursively defined acronym for “GNU is not UNIX”.
	- Goal was to develop freely available UNIX like system (kernel/associated programs/packages).
	- Encouraged others to join him.
- 1985, Stallman founded Free Software Foundation (FSF) non-profit org to support GNU project.
	- GNU project defined GNU GPL (GNU General Public License).
		- Software are made available in source code form.
		- Redistribution of modified software should be under GPL.
	- Most of software in Linux distro follows GNU GPL or variant.
- GPL versions:
	- 1989, v1.
	- 1991, v2.
	- 2007, v3.
- Initial popular programs under GNU projects:
	- EMACS text editor
	- GCC (GNU `C` Compiler, now GNU compiler collection)
	- Bash shell
	- Glibc
- 1990, GNU project had all major component other than working UNIX kernel.
	- GNU/HUND (based on Mach micro-kernel) was started by was not complete to be released.
	- ~2007, GNU/HUND work was continued and works on x86-32 arch.
- Stallman prefer term GNU/Linux for entire Linux system.

#### 1.2.2 The Linux Kernel
- 1991, Linus Trovalds (Finnish student at University of Helsinki, Finland).
- Minix (small UNIX like OS kernel developed in mid 1980 by Andrew Tanenbaum, professor in Holland)
	- open source tool for teaching OS.
	- as teaching tool, it as independent of HW and does not utilizes 386 to fullest.
- Linus inspired by Minix developed efficient, full featured UNIX kernel for his Intel 80386 PC.
	- Basic kernel that could compile/run GNU programs.
	- 1991, Oct 5, announced of version 0.02 in `comp.os.minix` Usenet newsgroup. [LINUX’s History by Linus Torvalds](https://www.cs.cmu.edu/~awb/linux.history.html)
	- Initially Linux was released with restrictive license but soon to GPL.
	- Other programmers joined and added features:
		- improved fs
		- networking support
		- device drives
		- multiprocessor support
- Linux releases: [Linux kernel version history - Wikipedia](https://en.wikipedia.org/wiki/Linux_kernel_version_history)
	- 1994, Mar, v 1.0.
	- 1995, Mar. v 1.2.
	- 1996, Jun. v 2.0.
	- 1999, Jan. v 2.2.
	- 2001, Jan. v 2.4.
	- 2003, Dec. v 2.6.
- Linux kernel version numbers:
	- release-early, release-often model.
	- adopted kernel version numbering as `major-version.minor-version.improvements-or-bug-fixes`.
	- There was always two branch but does not always follows the theory due to long intervals between stable kernel releases.
		- Stable branch for production had even-minor-version.
		- Volatile development branch had next higher odd-minor-version.
		- Eg. 2.3.x development kernel branch resulted into 2.4 stable kernel.
	- By 2.6, development model was changed.
		- 2.6.x can contains new features and goes through a life cycle. The features stabilize in subsequent candidate releases.
		- Release cycles are ~3 months long.
		- For stable version, 2.6.z. Minor patches for bug fix and security problem (high priority), new release is created of form 2.6.z.r (r = sequential number).
		- Manual pages note the precise development kernel in which features was introduced/modified.
- Ported to other arch:
	- Initially the goal was to make efficient implementation on Intel 80386 later ported to different arch.
	- https://lwn.net/Articles/654783/
- Linux distribution:
	- Precisely Linux mean Linux kernel.
	- Practically Linux means Linux kernel along with common softwares/tools that make OS complete.
	- Initially, uses assembles all of software/fs/configuration by themselves which requires time and expertise.
	- Linux distributors created packages(distributions) to automate installation process (creating of fs, installing kernel/tools).
		- 1992, easiest distro includes MCC Interim Linux (Manchester Computing Center, UK), TAMU (Texas A&M University) and SLS(SfotLanding Linux System).
		- 1993, Slackware, one of oldest surviving commercial distro.
		- Debian (same time) non commercial.
		- SUS and Red Hat.
		- 2004, Ubuntu.
	- Linux distro also make contribution to projects and free software.


### 1.3 Standardization
- 1980, Wide variety of UNIX.
	- Some were based on BSD and some on System V while other drew features from both.
	- Each commercial vendor added features of their own.
	- Leads to requirement of standardization.


#### 1.3.1 The `C` Programming Language
- 1980, `C` was (10 year old) was available on most UNIX and other OS.
- There were no standard of C, leads to variations in different implementation.
	- Some language aspect were not details in de facto standard for `C` by Kernighan and Ritchie (1978), The `C` programming Language.
		- Older syntax called as tradition or K&R C.
	- 1985, Appearance of `C++`, improvement were introduces in `C` with backward compatibility.
		- functions prototypes
		- structure assignment
		- type qualifies (const/volatile)
		- enumeration types
		- void keyword.
- 1989, `C` was standardized as ANSI `C` (American National Standards Institute) X3.159-1989.
	- 1990, ANSI `C` was adopted as ISO (International Organization for Standardization) (ISO/IEC 9899:1990)
		- defined the syntax and semantics of C
		- described operation of standard `C` lib
			- stdio functions, string handling functions, math functions, introduces some headers files, etc.
		- ISO C90 or C89.
		- fully described in Kernighan and Ritchie’s The `C` Programming Language 2e, 1988.
	- 1999, revised `C` standard. ISO/IEC 9899:1999, [ISO/IEC JTC1/SC22/WG14 - C: Approved standards](http://www.open-std.org/jtc1/sc22/wg14/www/standards), known as C99.
		- addition of `long long`
		- boolean data type.
		- `//` comments
		- destructed pointers
		- variable length arrays.
- `C` programs written with standard libraries are portable. 

#### 1.3.2 The First POSIX Standards
- POSIX (Portable OS Interface) refers to standards developed under IEEE-PASC (Institute of Electrical and Electronic Engineers) (Portable Application Standards Committee).
	- PASC promote application portability at source code level.
	- POSIX name suggested by Richard Stallman.
	- 1988, POSIX.1 ( POSIX 1003.1) became IEEE standard
		- 1990, adopted by ISO with minor revision as ISO/IEC 9945-1:1990
		- It documents API sets of services which should be provided by conforming OS.
		- It is based on UNIX system calls and `C` lib. However, the POSIX API can be implemented by any OS.
	- 1993, IEEE POSIX 1003.1b, formally POSIX 1003.4; contains realtime extensions.
		- file synchronization
		- asynchronous IO
		- process scheduling
		- high precision clocks and timers
		- inter-process communication using semaphores, shared memory and message queues.
			- To distinguish from other similar System V IPC (semaphores/shared memory/message queues), POSIX prefix is applied.
	- 1995, IEEE POSIX 1003.1c; defined POSIX threads.
	- 1996, revision of POSIX.1 (ISO/EIC 9945-1:1996) incorporated realtime and threads extension.
	- IEEE POSIX 1003,1g; defined networking API and socket API.
	- 1999, IEEE POSIX 1003.1d and 2000, POSIX 1j; defined additional realtime extensions.
	- 1992, POSIX.2 (ISO/IEC 9945-2:1993)
		- standardized shell
		- various UNIX utilities including `C` cli.

#### 1.3.3 X/Open Company and The Open Group
- X/Open Company, consortium formed by international groups of vendors to adopt/adapt existing standards to produce comprehensive/consistent set of open system standards.
	- It produces X/Open Portability Guide, a series of guides based on POSIX.
	- Releases:
		- 1989, Issue 3 (XPG3)
		- 1992, XPG4
		- 1994, XPG4 v2, this also incorporated important parts of AT&T System V interface definition Issue 3. This revision also know as `Spec 1170` (referring to number of interfaces-functions, header files and commands).
- 1993, Novell acquired UNIX systems business from AT&T.
	- Novel divested itself of the business and transferred UNIX trademark to X/Open (early 1994).
- XPG4 v2 repackages as single UNIX Specification (SUS/SUS v1), UNIX 95.
	- It includes XPG4 v2.
	- X/Open Curse Issue 4 v2 spec.
	- X/Open Networking Services (XNS) Issue 4 spec.
	- 1997, SUSv2 (XPG5), implementation certified agains SUSv2 called as UNIX 98. 
- 1996, X/Open merged with OSF (Open Software Foundation) to form The Open Group (TOG).
	- Most of orgs associated with UNIX systems are member of TOG, continues to develop API standards.

#### 1.3.4 SUSv3 and POSIX.1-2001
- 1999, IEEE, TOG, ISO/IEC-JTC (Joint Technical Committee) 1 collaborated in Austin Common Standards Revision Group (CSRG).
	- aim of consolidation of POSIX and SUS.
	- resulted in POSIX 1003.1-2001/POSIX.1-2001, approved as ISO/IEC 9945:2002.
- POSIX 1003.1-2001 (SUSv3) replaces SUSv2, POSIX.1, POSIX.2 and earlier POSIX standards.
	- SUSv3 also includes X/Open CURSES Issue 4 v2 (XCURSES) spec; 372 functions and 3 headers file for curses-screen-handling API.
- SUSv3 have 4 parts:
	- Base Definitions (XBD):
		- contents of header files (84) specification provided.
	- System Interfaces (XSH):
		- functions (system calls/lib functions) (1123).
	- Shell and Utilities (XCU):
		- operations of shell/commands (160 utils).
	- Rationale (XRAT):
		- informative text and justifications for above parts.


#### 1.3.5 SUSv4 and POSIX.1-2008
- 2008, Austin group revised POSIX.1 and SUS as SUSv4.

#### 1.3.6 UNIX Standards Timeline
- https://oudalab.github.io/cs3113fa18/lecture/unix-to-linux.pdf

#### 1.3.7 Implementation Standards
- BSD (4.4BSD) and AT&T System V release 4 (SVR4) are two prominent implement standards.
	- Later standards was formalized by AT&T publication of System V Interface Definition (SVID).
	- 1989, SVID Issue 3, issue conformant for SVR4.
- Conditional compilation were used for non-portable code of SVR4 and BSD.

#### 1.3.8 Linux, Standards, and the Linux Standard Base
- Linux (kernel/glibc/tools) developments aims to conform UNIX/POSIX/SUS standards.
- No Linux distro are branded as “UNIX” by TOG as each distro would need to undergo conformance testing to obtain the branding and require to retest with each release. So the process is expensive and time consuming.
- Most Commercial UNIX implementation, same company develops and distribute the OS.
	- For linux, development and distribution are separate.
- Linus, works as fellow at Linux Foundation [The Linux Foundation – Supporting Open Source Ecosystems](https://www.linuxfoundation.org/) (earlier Open Source Development Laboratory, OSDL), non profit consortium of commercial/non-commercial orgs.
- Many features/patches first appears in distro, later accepted in mainline Kernel. 
- Linux Standard Base (LSB) ensure compatibility among distro.
	- aim to ensure that binary application can run on any LSB-conformant system. It more difficult to run same binary on different arch.
	- in contrast POSIX promoted source code portability. Eg. `C` program can compile on conformant system.
- Binary portability is required for commercial viable of Independent Software Vendor (ISV) applications for Linux.


[↑](https://arunsah.github.io/linuxprog#table-of-content)


## Chapter 2: Fundamental Concepts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.1 The Core Operating System: The Kernel



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.2 The Shell



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.3 Users and Groups



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.4 Single Directory Hierarchy, Directories, Links, and Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.5 File I/O Model



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.6 Programs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.7 Processes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.8 Memory Mappings



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.9 Static and Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.10 Interprocess Communication and Synchronization



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.11 Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.12 Threads



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.13 Process Groups and Shell Job Control



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.14 Sessions, Controlling Terminals, and Controlling Processes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.15 Pseudoterminals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.16 Date and Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.17 Client-Server Architecture



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.18 Realtime



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.19 The /proc File System



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 2.20 Summary




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 3: System Programming Concepts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.1 System Calls



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.2 Library Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.3 The Standard C Library; The GNU C Library (glibc)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.4 Handling Errors from System Calls and Library Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.5 Notes on the Example Programs in This Book



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.5.1 Command-Line Options and Arguments



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.5.2 Common Functions and Header Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.6 Portability Issues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.6.1 Feature Test Macros



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.6.2 System Data Types



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.6.3 Miscellaneous Portability Issues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.7 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 3.8 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 4: File I/O: The Universal I/O Model



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.2 Universality of I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.3 Opening a File: open()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.3.1 The open() flags Argument



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.3.2 Errors from open()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.3.3 The creat() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.4 Reading from a File: read()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.5 Writing to a File: write()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.6 Closing a File: close()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.7 Changing the File Offset: lseek()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.8 Operations Outside the Universal I/O Model: ioctl()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.9 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 4.10 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 5: File I/O: Further Details



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.1 Atomicity and Race Conditions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.2 File Control Operations: fcntl()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.3 Open File Status Flags



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.4 Relationship Between File Descriptors and Open Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.5 Duplicating File Descriptors



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.6 File I/O at a Specified Offset: pread() and pwrite()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.7 Scatter-Gather I/O: readv() and writev()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.8 Truncating a File: truncate() and ftruncate()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.9 Nonblocking I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.10 I/O on Large Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.11 The /dev/fd Directory



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.12 Creating Temporary Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.13 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 5.14 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 6: Processes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.1 Processes and Programs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.2 Process ID and Parent Process ID



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.3 Memory Layout of a Process



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.4 Virtual Memory Management



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.5 The Stack and Stack Frames



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.6 Command-Line Arguments (argc, argv)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.7 Environment List



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.8 Performing a Nonlocal Goto: setjmp() and longjmp()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.9 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 6.10 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 7: Memory Allocation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.1 Allocating Memory on the Heap



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.1.1 Adjusting the Program Break: brk() and sbrk()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.1.2 Allocating Memory on the Heap: malloc() and free()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.1.3 Implementation of malloc() and free()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.1.4 Other Methods of Allocating Memory on the Heap



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.2 Allocating Memory on the Stack: alloca()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.3 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 7.4 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 8: Users and Groups



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 8.1 The Password File: /etc/passwd



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 8.2 The Shadow Password File: /etc/shadow



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 8.3 The Group File: /etc/group



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 8.4 Retrieving User and Group Information



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 8.5 Password Encryption and User Authentication



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 8.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 8.7 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 9: Process Credentials



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.1 Real User ID and Real Group ID



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.2 Effective User ID and Effective Group ID



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.3 Set-User-ID and Set-Group-ID Programs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.4 Saved Set-User-ID and Saved Set-Group-ID



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.5 File-System User ID and File-System Group ID



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.6 Supplementary Group IDs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.7 Retrieving and Modifying Process Credentials



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.7.1 Retrieving and Modifying Real, Effective, and Saved Set IDs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.7.2 Retrieving and Modifying File-System IDs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.7.3 Retrieving and Modifying Supplementary Group IDs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.7.4 Summary of Calls for Modifying Process Credentials



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.7.5 Example: Displaying Process Credentials



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 9.9 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 10: Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.1 Calendar Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.2 Time-Conversion Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.2.1 Converting time_t to Printable Form



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.2.2 Converting Between time_t and Broken-Down Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.2.3 Converting Between Broken-Down Time and Printable Form



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.3 Timezones



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.4 Locales



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.5 Updating the System Clock



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.6 The Software Clock (Jiffies)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.7 Process Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 10.9 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 11: System Limits and Options



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 11.1 System Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 11.2 Retrieving System Limits (and Options) at Run Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 11.3 Retrieving File-Related Limits (and Options) at Run Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 11.4 Indeterminate Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 11.5 System Options



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 11.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 11.7 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 12: System and Process Information



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 12.1 The /proc File System



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 12.1.1 Obtaining Information About a Process: /proc/PID



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 12.1.2 System Information Under /proc



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 12.1.3 Accessing /proc Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 12.2 System Identification: uname()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 12.3 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 12.4 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 13: File I/O Buffering



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.1 Kernel Buffering of File I/O: The Buffer Cache



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.2 Buffering in the stdio Library



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.3 Controlling Kernel Buffering of File I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.4 Summary of I/O Buffering



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.5 Advising the Kernel About I/O Patterns



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.6 Bypassing the Buffer Cache: Direct I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.7 Mixing Library Functions and System Calls for File I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 13.9 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 14: File Systems



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.1 Device Special Files (Devices)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.2 Disks and Partitions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.3 File Systems



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.4 I-nodes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.5 The Virtual File System (VFS)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.6 Journaling File Systems



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.7 Single Directory Hierarchy and Mount Points



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.8 Mounting and Unmounting File Systems



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.8.1 Mounting a File System: mount()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.8.2 Unmounting a File System: umount() and umount2()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.9 Advanced Mount Features



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.9.1 Mounting a File System at Multiple Mount Points



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.9.2 Stacking Multiple Mounts on the Same Mount Point



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.9.3 Mount Flags That Are Per-Mount Options



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.9.4 Bind Mounts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.9.5 Recursive Bind Mounts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.10 A Virtual Memory File System: tmpfs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.11 Obtaining Information About a File System: statvfs()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.12 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 14.13 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 15: File Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.1 Retrieving File Information: stat()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.2 File Timestamps



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.2.1 Changing File Timestamps with utime() and utimes()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.2.2 Changing File Timestamps with utimensat() and futimens()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.3 File Ownership



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.3.1 Ownership of New Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.3.2 Changing File Ownership: chown(), fchown(), and lchown()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4 File Permissions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4.1 Permissions on Regular Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4.2 Permissions on Directories



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4.3 Permission-Checking Algorithm



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4.4 Checking File Accessibility: access()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4.5 Set-User-ID, Set-Group-ID, and Sticky Bits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4.6 The Process File Mode Creation Mask: umask()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.4.7 Changing File Permissions: chmod() and fchmod()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.5 I-node Flags (ext2 Extended File Attributes)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 15.7 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 16: Extended Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 16.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 16.2 Extended Attribute Implementation Details



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 16.3 System Calls for Manipulating Extended Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 16.4 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 16.5 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 17: Access Control Lists



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.2 ACL Permission-Checking Algorithm



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.3 Long and Short Text Forms for ACLs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.4 The ACL_MASK Entry and the ACL Group Class



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.5 The getfacl and setfacl Commands



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.6 Default ACLs and File Creation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.7 ACL Implementation Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.8 The ACL API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.9 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 17.10 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 18: Directories and Links



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.1 Directories and (Hard) Links



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.2 Symbolic (Soft) Links



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.3 Creating and Removing (Hard) Links: link() and unlink()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.4 Changing the Name of a File: rename()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.5 Working with Symbolic Links: symlink() and readlink()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.6 Creating and Removing Directories: mkdir() and rmdir()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.7 Removing a File or Directory: remove()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.8 Reading Directories: opendir() and readdir()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.9 File Tree Walking: nftw()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.10 The Current Working Directory of a Process



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.11 Operating Relative to a Directory File Descriptor



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.12 Changing the Root Directory of a Process: chroot()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.13 Resolving a Pathname: realpath()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.14 Parsing Pathname Strings: dirname() and basename()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.15 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 18.16 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 19: Monitoring File Events



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.2 The inotify API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.3 inotify Events



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.4 Reading inotify Events



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.5 Queue Limits and /proc Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.6 An Older System for Monitoring File Events: dnotify



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.7 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 19.8 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 20: Signals: Fundamental Concepts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.1 Concepts and Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.2 Signal Types and Default Actions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.3 Changing Signal Dispositions: signal()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.4 Introduction to Signal Handlers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.5 Sending Signals: kill()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.6 Checking for the Existence of a Process



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.7 Other Ways of Sending Signals: raise() and killpg()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.8 Displaying Signal Descriptions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.9 Signal Sets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.10 The Signal Mask (Blocking Signal Delivery)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.11 Pending Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.12 Signals Are Not Queued



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.13 Changing Signal Dispositions: sigaction()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.14 Waiting for a Signal: pause()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.15 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 20.16 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 21: Signals: Signal Handlers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.1 Designing Signal Handlers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.1.1 Signals Are Not Queued (Revisited)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.1.2 Reentrant and Async-Signal-Safe Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.1.3 Global Variables and the sig_atomic_t Data Type



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.2 Other Methods of Terminating a Signal Handler



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.2.1 Performing a Nonlocal Goto from a Signal Handler



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.2.2 Terminating a Process Abnormally: abort()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.3 Handling a Signal on an Alternate Stack: sigaltstack()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.4 The SA_SIGINFO Flag



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.5 Interruption and Restarting of System Calls



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 21.7 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 22: Signals: Advanced Features



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.1 Core Dump Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.2 Special Cases for Delivery, Disposition, and Handling



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.3 Interruptible and Uninterruptible Process Sleep States



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.4 Hardware-Generated Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.5 Synchronous and Asynchronous Signal Generation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.6 Timing and Order of Signal Delivery



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.7 Implementation and Portability of signal()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.8 Realtime Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.8.1 Sending Realtime Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.8.2 Handling Realtime Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.9 Waiting for a Signal Using a Mask: sigsuspend()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.10 Synchronously Waiting for a Signal



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.11 Fetching Signals via a File Descriptor



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.12 Interprocess Communication with Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.13 Earlier Signal APIs (System V and BSD)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.14 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 22.15 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 23: Timers and Sleeping



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.1 Interval Timers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.2 Scheduling and Accuracy of Timers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.3 Setting Timeouts on Blocking Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.4 Suspending Execution for a Fixed Interval (Sleeping)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.4.1 Low-Resolution Sleeping: sleep()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.4.2 High-Resolution Sleeping: nanosleep()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.5 POSIX Clocks



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.5.1 Retrieving the Value of a Clock: clock_gettime()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.5.2 Setting the Value of a Clock: clock_settime()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.5.3 Obtaining the Clock ID of a Specific Process or Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.5.4 Improved High-Resolution Sleeping: clock_nanosleep()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6 POSIX Interval Timers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6.1 Creating a Timer: timer_create()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6.2 Arming and Disarming a Timer: timer_settime()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6.3 Retrieving the Current Value of a Timer: timer_gettime()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6.4 Deleting a Timer: timer_delete()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6.5 Notification via a Signal



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6.6 Timer Overruns



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.6.7 Notification via a Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.7 Timers That Notify via File Descriptors: The timerfd API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 23.9 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 24: Process Creation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.1 Overview of fork(), exit(), wait(), and execve()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.2 Creating a New Process: fork()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.2.1 File Sharing Between Parent and Child



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.2.2 Memory Semantics of fork()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.3 The vfork() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.4 Race Conditions After fork()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.5 Avoiding Race Conditions by Synchronizing with Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 24.7 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 25: Process Termination



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 25.1 Terminating a Process: _exit() and exit()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 25.2 Details of Process Termination



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 25.3 Exit Handlers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 25.4 Interactions Between fork(), stdio Buffers, and _exit()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 25.5 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 25.6 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 26: Monitoring Child Processes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.1 Waiting on a Child Process



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.1.1 The wait() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.1.2 The waitpid() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.1.3 The Wait Status Value



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.1.4 Process Termination from a Signal Handler



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.1.5 The waitid() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.1.6 The wait3() and wait4() System Calls



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.2 Orphans and Zombies



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.3 The SIGCHLD Signal



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.3.1 Establishing a Handler for SIGCHLD



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.3.2 Delivery of SIGCHLD for Stopped Children



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.3.3 Ignoring Dead Child Processes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.4 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 26.5 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 27: Program Execution



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.1 Executing a New Program: execve()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.2 The exec() Library Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.2.1 The PATH Environment Variable



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.2.2 Specifying Program Arguments as a List



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.2.3 Passing the Caller’s Environment to the New Program



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.2.4 Executing a File Referred to by a Descriptor: fexecve()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.3 Interpreter Scripts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.4 File Descriptors and exec()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.5 Signals and exec()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.6 Executing a Shell Command: system()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.7 Implementing system()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 27.9 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 28: Process Creation and Program Execution in More Detail



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.1 Process Accounting



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.2 The clone() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.2.1 The clone() flags Argument



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.2.2 Extensions to waitpid() for Cloned Children



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.3 Speed of Process Creation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.4 Effect of exec() and fork() on Process Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.5 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 28.6 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 29: Threads: Introduction



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.2 Background Details of the Pthreads API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.3 Thread Creation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.4 Thread Termination



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.5 Thread IDs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.6 Joining with a Terminated Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.7 Detaching a Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.8 Thread Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.9 Threads Versus Processes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.10 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 29.11 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 30: Threads: Thread Synchronization



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1 Protecting Accesses to Shared Variables: Mutexes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1.1 Statically Allocated Mutexes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1.2 Locking and Unlocking a Mutex



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1.3 Performance of Mutexes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1.4 Mutex Deadlocks



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1.5 Dynamically Initializing a Mutex



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1.6 Mutex Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.1.7 Mutex Types



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.2 Signaling Changes of State: Condition Variables



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.2.1 Statically Allocated Condition Variables



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.2.2 Signaling and Waiting on Condition Variables



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.2.3 Testing a Condition Variable’s Predicate



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.2.4 Example Program: Joining Any Terminated Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.2.5 Dynamically Allocated Condition Variables



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.3 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 30.4 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 31: Threads: Thread Safety and Per-Thread Storage



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.1 Thread Safety (and Reentrancy Revisited)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.2 One-Time Initialization



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.3 Thread-Specific Data



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.3.1 Thread-Specific Data from the Library Function’s Perspective



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.3.2 Overview of the Thread-Specific Data API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.3.3 Details of the Thread-Specific Data API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.3.4 Employing the Thread-Specific Data API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.3.5 Thread-Specific Data Implementation Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.4 Thread-Local Storage



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.5 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 31.6 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 32: Threads: Thread Cancellation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 32.1 Canceling a Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 32.2 Cancellation State and Type



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 32.3 Cancellation Points



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 32.4 Testing for Thread Cancellation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 32.5 Cleanup Handlers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 32.6 Asynchronous Cancelability



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 32.7 Summary




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 33: Threads: Further Details



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.1 Thread Stacks



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.2 Threads and Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.2.1 How the UNIX Signal Model Maps to Threads



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.2.2 Manipulating the Thread Signal Mask



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.2.3 Sending a Signal to a Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.2.4 Dealing with Asynchronous Signals Sanely



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.3 Threads and Process Control



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.4 Thread Implementation Models



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.5 Linux Implementations of POSIX Threads



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.5.1 LinuxThreads



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.5.2 NPTL



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.5.3 Which Threading Implementation?



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.6 Advanced Features of the Pthreads API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.7 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 33.8 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 34: Process Groups, Sessions, and Job Control



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.2 Process Groups



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.3 Sessions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.4 Controlling Terminals and Controlling Processes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.5 Foreground and Background Process Groups



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.6 The SIGHUP Signal



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.6.1 Handling of SIGHUP by the Shell



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.6.2 SIGHUP and Termination of the Controlling Process



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.7 Job Control



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.7.1 Using Job Control Within the Shell



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.7.2 Implementing Job Control



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.7.3 Handling Job-Control Signals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.7.4 Orphaned Process Groups (and SIGHUP Revisited)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 34.9 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 35: Process Priorities and Scheduling



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.1 Process Priorities (Nice Values)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.2 Overview of Realtime Process Scheduling



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.2.1 The SCHED_RR Policy



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.2.2 The SCHED_FIFO Policy



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.2.3 The SCHED_BATCH and SCHED_IDLE Policies



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.3 Realtime Process Scheduling API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.3.1 Realtime Priority Ranges



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.3.2 Modifying and Retrieving Policies and Priorities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.3.3 Relinquishing the CPU



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.3.4 The SCHED_RR Time Slice



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.4 CPU Affinity



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.5 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 35.6 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 36: Process Resources



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 36.1 Process Resource Usage



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 36.2 Process Resource Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 36.3 Details of Specific Resource Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 36.4 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 36.5 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 37: Daemons



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.2 Creating a Daemon



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.3 Guidelines for Writing Daemons



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.4 Using SIGHUP to Reinitialize a Daemon



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.5 Logging Messages and Errors Using syslog



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.5.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.5.2 The syslog API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.5.3 The /etc/syslog.conf File



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 37.7 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 38: Writing Secure Privileged Programs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.1 Is a Set-User-ID or Set-Group-ID Program Required?



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.2 Operate with Least Privilege



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.3 Be Careful When Executing a Program



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.4 Avoid Exposing Sensitive Information



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.5 Confine the Process



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.6 Beware of Signals and Race Conditions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.7 Pitfalls When Performing File Operations and File I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.8 Don’t Trust Inputs or the Environment



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.9 Beware of Buffer Overruns



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.10 Beware of Denial-of-Service Attacks



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.11 Check Return Statuses and Fail Safely



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.12 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 38.13 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 39: Capabilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.1 Rationale for Capabilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.2 The Linux Capabilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.3 Process and File Capabilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.3.1 Process Capabilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.3.2 File Capabilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.3.3 Purpose of the Process Permitted and Effective Capability Sets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.3.4 Purpose of the File Permitted and Effective Capability Sets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.3.5 Purpose of the Process and File Inheritable Sets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.3.6 Assigning and Viewing File Capabilities from the Shell



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.4 The Modern Capabilities Implementation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.5 Transformation of Process Capabilities During exec()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.5.1 Capability Bounding Set



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.5.2 Preserving root Semantics



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.6 Effect on Process Capabilities of Changing User IDs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.7 Changing Process Capabilities Programmatically



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.8 Creating Capabilities-Only Environments



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.9 Discovering the Capabilities Required by a Program



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.10 Older Kernels and Systems Without File Capabilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.11 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 39.12 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 40: Login Accounting



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.1 Overview of the utmp and wtmp Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.2 The utmpx API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.3 The utmpx Structure



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.4 Retrieving Information from the utmp and wtmp Files



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.5 Retrieving the Login Name: getlogin()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.6 Updating the utmp and wtmp Files for a Login Session



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.7 The lastlog File



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 40.9 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 41: Fundamentals of Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.1 Object Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.2 Static Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.3 Overview of Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.4 Creating and Using Shared Libraries—A First Pass



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.4.1 Creating a Shared Library



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.4.2 Position-Independent Code



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.4.3 Using a Shared Library



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.4.4 The Shared Library Soname



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.5 Useful Tools for Working with Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.6 Shared Library Versions and Naming Conventions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.7 Installing Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.8 Compatible Versus Incompatible Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.9 Upgrading Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.10 Specifying Library Search Directories in an Object File



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.11 Finding Shared Libraries at Run Time



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.12 Run-Time Symbol Resolution



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.13 Using a Static Library Instead of a Shared Library



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.14 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 41.15 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 42: Advanced Features of Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.1 Dynamically Loaded Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.1.1 Opening a Shared Library: dlopen()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.1.2 Diagnosing Errors: dlerror()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.1.3 Obtaining the Address of a Symbol: dlsym()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.1.4 Closing a Shared Library: dlclose()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.1.5 Obtaining Information About Loaded Symbols: dladdr()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.1.6 Accessing Symbols in the Main Program



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.2 Controlling Symbol Visibility



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.3 Linker Version Scripts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.3.1 Controlling Symbol Visibility with Version Scripts



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.3.2 Symbol Versioning



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.4 Initialization and Finalization Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.5 Preloading Shared Libraries



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.6 Monitoring the Dynamic Linker: LD_DEBUG



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.7 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 42.8 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 43: Interprocess Communication Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 43.1 A Taxonomy of IPC Facilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 43.2 Communication Facilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 43.3 Synchronization Facilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 43.4 Comparing IPC Facilities



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 43.5 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 43.6 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 44: Pipes and FIFOs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.2 Creating and Using Pipes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.3 Pipes as a Method of Process Synchronization



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.4 Using Pipes to Connect Filters



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.5 Talking to a Shell Command via a Pipe: popen()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.6 Pipes and stdio Buffering



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.7 FIFOs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.8 A Client-Server Application Using FIFOs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.9 Nonblocking I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.10 Semantics of read() and write() on Pipes and FIFOs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.11 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 44.12 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 45: Introduction to System V IPC



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.1 API Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.2 IPC Keys



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.3 Associated Data Structure and Object Permissions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.4 IPC Identifiers and Client-Server Applications



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.5 Algorithm Employed by System V IPC get Calls



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.6 The ipcs and ipcrm Commands



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.7 Obtaining a List of All IPC Objects



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.8 IPC Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.9 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 45.10 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 46: System V Message Queues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.1 Creating or Opening a Message Queue



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.2 Exchanging Messages



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.2.1 Sending Messages



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.2.2 Receiving Messages



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.3 Message Queue Control Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.4 Message Queue Associated Data Structure



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.5 Message Queue Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.6 Displaying All Message Queues on the System



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.7 Client-Server Programming with Message Queues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.8 A File-Server Application Using Message Queues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.9 Disadvantages of System V Message Queues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.10 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 46.11 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 47: System V Semaphores



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.2 Creating or Opening a Semaphore Set



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.3 Semaphore Control Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.4 Semaphore Associated Data Structure



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.5 Semaphore Initialization



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.6 Semaphore Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.7 Handling of Multiple Blocked Semaphore Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.8 Semaphore Undo Values



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.9 Implementing a Binary Semaphores Protocol



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.10 Semaphore Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.11 Disadvantages of System V Semaphores



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.12 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 47.13 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 48: System V Shared Memory



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.2 Creating or Opening a Shared Memory Segment



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.3 Using Shared Memory



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.4 Example: Transferring Data via Shared Memory



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.5 Location of Shared Memory in Virtual Memory



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.6 Storing Pointers in Shared Memory



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.7 Shared Memory Control Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.8 Shared Memory Associated Data Structure



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.9 Shared Memory Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.10 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 48.11 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 49: Memory Mappings



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.2 Creating a Mapping: mmap()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.3 Unmapping a Mapped Region: munmap()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.4 File Mappings



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.4.1 Private File Mappings



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.4.2 Shared File Mappings



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.4.3 Boundary Cases



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.4.4 Memory Protection and File Access Mode Interactions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.5 Synchronizing a Mapped Region: msync()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.6 Additional mmap() Flags



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.7 Anonymous Mappings



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.8 Remapping a Mapped Region: mremap()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.9 MAP_NORESERVE and Swap Space Overcommitting



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.10 The MAP_FIXED Flag



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.11 Nonlinear Mappings: remap_file_pages()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.12 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 49.13 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 50: Virtual Memory Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 50.1 Changing Memory Protection: mprotect()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 50.2 Memory Locking: mlock() and mlockall()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 50.3 Determining Memory Residence: mincore()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 50.4 Advising Future Memory Usage Patterns: madvise()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 50.5 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 50.6 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 51: Introduction to POSIX IPC



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 51.1 API Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 51.2 Comparison of System V IPC and POSIX IPC



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 51.3 Summary




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 52: POSIX Message Queues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.2 Opening, Closing, and Unlinking a Message Queue



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.3 Relationship Between Descriptors and Message Queues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.4 Message Queue Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.5 Exchanging Messages



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.5.1 Sending Messages



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.5.2 Receiving Messages



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.5.3 Sending and Receiving Messages with a Timeout



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.6 Message Notification



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.6.1 Receiving Notification via a Signal



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.6.2 Receiving Notification via a Thread



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.7 Linux-Specific Features



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.8 Message Queue Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.9 Comparison of POSIX and System V Message Queues



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.10 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 52.11 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 53: POSIX Semaphores



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.2 Named Semaphores



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.2.1 Opening a Named Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.2.2 Closing a Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.2.3 Removing a Named Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.3 Semaphore Operations



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.3.1 Waiting on a Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.3.2 Posting a Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.3.3 Retrieving the Current Value of a Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.4 Unnamed Semaphores



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.4.1 Initializing an Unnamed Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.4.2 Destroying an Unnamed Semaphore



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.5 Comparisons with Other Synchronization Techniques



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.6 Semaphore Limits



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.7 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 53.8 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 54: POSIX Shared Memory



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 54.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 54.2 Creating Shared Memory Objects



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 54.3 Using Shared Memory Objects



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 54.4 Removing Shared Memory Objects



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 54.5 Comparisons Between Shared Memory APIs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 54.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 54.7 Exercise




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 55: File Locking



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.2 File Locking with flock()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.2.1 Semantics of Lock Inheritance and Release



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.2.2 Limitations of flock()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.3 Record Locking with fcntl()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.3.1 Deadlock



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.3.2 Example: An Interactive Locking Program



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.3.3 Example: A Library of Locking Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.3.4 Lock Limits and Performance



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.3.5 Semantics of Lock Inheritance and Release



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.3.6 Lock Starvation and Priority of Queued Lock Requests



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.4 Mandatory Locking



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.5 The /proc/locks File



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.6 Running Just One Instance of a Program



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.7 Older Locking Techniques



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.8 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 55.9 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 56: Sockets: Introduction



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.2 Creating a Socket: socket()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.3 Binding a Socket to an Address: bind()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.4 Generic Socket Address Structures: struct sockaddr



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.5 Stream Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.5.1 Listening for Incoming Connections: listen()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.5.2 Accepting a Connection: accept()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.5.3 Connecting to a Peer Socket: connect()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.5.4 I/O on Stream Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.5.5 Connection Termination: close()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.6 Datagram Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.6.1 Exchanging Datagrams: recvfrom() and sendto()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.6.2 Using connect() with Datagram Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 56.7 Summary




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 57: Sockets: UNIX Domain



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.1 UNIX Domain Socket Addresses: struct sockaddr_un



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.2 Stream Sockets in the UNIX Domain



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.3 Datagram Sockets in the UNIX Domain



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.4 UNIX Domain Socket Permissions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.5 Creating a Connected Socket Pair: socketpair()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.6 The Linux Abstract Socket Namespace



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.7 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 57.8 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 58: Sockets: Fundamentals of TCP/IP Networks



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.1 Internets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.2 Networking Protocols and Layers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.3 The Data-Link Layer



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.4 The Network Layer: IP



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.5 IP Addresses



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.6 The Transport Layer



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.6.1 Port Numbers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.6.2 User Datagram Protocol (UDP)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.6.3 Transmission Control Protocol (TCP)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.7 Requests for Comments (RFCs)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 58.8 Summary




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 59: Sockets: Internet Domains



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.1 Internet Domain Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.2 Network Byte Order



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.3 Data Representation



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.4 Internet Socket Addresses



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.5 Overview of Host and Service Conversion Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.6 The inet_pton() and inet_ntop() Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.7 Client-Server Example (Datagram Sockets)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.8 Domain Name System (DNS)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.9 The /etc/services File



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.10 Protocol-Independent Host and Service Conversion



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.10.1 The getaddrinfo() Function



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.10.2 Freeing addrinfo Lists: freeaddrinfo()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.10.3 Diagnosing Errors: gai_strerror()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.10.4 The getnameinfo() Function



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.11 Client-Server Example (Stream Sockets)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.12 An Internet Domain Sockets Library



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.13 Obsolete APIs for Host and Service Conversions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.13.1 The inet_aton() and inet_ntoa() Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.13.2 The gethostbyname() and gethostbyaddr() Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.13.3 The getservbyname() and getservbyport() Functions



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.14 UNIX Versus Internet Domain Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.15 Further Information



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.16 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 59.17 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 60: Sockets: Server Design



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 60.1 Iterative and Concurrent Servers



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 60.2 An Iterative UDP echo Server



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 60.3 A Concurrent TCP echo Server



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 60.4 Other Concurrent Server Designs



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 60.5 The inetd (Internet Superserver) Daemon



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 60.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 60.7 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 61: Sockets: Advanced Topics



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.1 Partial Reads and Writes on Stream Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.2 The shutdown() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.3 Socket-Specific I/O System Calls: recv() and send()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.4 The sendfile() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.5 Retrieving Socket Addresses



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6 A Closer Look at TCP



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6.1 Format of a TCP Segment



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6.2 TCP Sequence Numbers and Acknowledgements



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6.3 TCP State Machine and State Transition Diagram



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6.4 TCP Connection Establishment



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6.5 TCP Connection Termination



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6.6 Calling shutdown() on a TCP Socket



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.6.7 The TIME_WAIT State



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.7 Monitoring Sockets: netstat



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.8 Using tcpdump to Monitor TCP Traffic



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.9 Socket Options



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.10 The SO_REUSEADDR Socket Option



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.11 Inheritance of Flags and Options Across accept()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.12 TCP Versus UDP



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.13 Advanced Features



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.13.1 Out-of-Band Data



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.13.2 The sendmsg() and recvmsg() System Calls



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.13.3 Passing File Descriptors



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.13.4 Receiving Sender Credentials



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.13.5 Sequenced-Packet Sockets



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.13.6 SCTP and DCCP Transport-Layer Protocols



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.14 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 61.15 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 62: Terminals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.2 Retrieving and Modifying Terminal Attributes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.3 The stty Command



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.4 Terminal Special Characters



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.5 Terminal Flags



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.6 Terminal I/O Modes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.6.1 Canonical Mode



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.6.2 Noncanonical Mode



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.6.3 Cooked, Cbreak, and Raw Modes



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.7 Terminal Line Speed (Bit Rate)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.8 Terminal Line Control



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.9 Terminal Window Size



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.10 Terminal Identification



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.11 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 62.12 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 63: Alternative I/O Models



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.1.1 Level-Triggered and Edge-Triggered Notification



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.1.2 Employing Nonblocking I/O with Alternative I/O Models



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.2 I/O Multiplexing



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.2.1 The select() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.2.2 The poll() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.2.3 When Is a File Descriptor Ready?



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.2.4 Comparison of select() and poll()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.2.5 Problems with select() and poll()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.3 Signal-Driven I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.3.1 When Is “I/O Possible” Signaled?



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.3.2 Refining the Use of Signal-Driven I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.4 The epoll API



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.4.1 Creating an epoll Instance: epoll_create()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.4.2 Modifying the epoll Interest List: epoll_ctl()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.4.3 Waiting for Events: epoll_wait()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.4.4 A Closer Look at epoll Semantics



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.4.5 Performance of epoll Versus I/O Multiplexing



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.4.6 Edge-Triggered Notification



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.5 Waiting on Signals and File Descriptors



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.5.1 The pselect() System Call



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.5.2 The Self-Pipe Trick



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.6 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 63.7 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Chapter 64: Pseudoterminals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.1 Overview



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.2 UNIX 98 Pseudoterminals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.2.1 Opening an Unused Master: posix_openpt()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.2.2 Changing Slave Ownership and Permissions: grantpt()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.2.3 Unlocking the Slave: unlockpt()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.2.4 Obtaining the Name of the Slave: ptsname()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.3 Opening a Master: ptyMasterOpen()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.4 Connecting Processes with a Pseudoterminal: ptyFork()



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.5 Pseudoterminal I/O



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.6 Implementing script(1)



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.7 Terminal Attributes and Window Size



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.8 BSD Pseudoterminals



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.9 Summary



[↑](https://arunsah.github.io/linuxprog#table-of-content)



## 64.10 Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Appendix A: Tracing System Calls




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Appendix B: Parsing Command-Line Options




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Appendix C: Casting the NULL Pointer




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Appendix D: Kernel Configuration




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Appendix E: Further Sources of Information




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## Appendix F: Solutions to Selected Exercises




[↑](https://arunsah.github.io/linuxprog#table-of-content)



## References
- https://learning.oreilly.com/library/view/the-linux-programming/9781593272203/




[↑](https://arunsah.github.io/linuxprog#table-of-content)

[arunsah.github.io](https://arunsah.github.io)
