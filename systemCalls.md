# System Calls

## fork()

* creates a new process which is called child.
* Parent and child process have the same content, but in different memorie spaces. If any method is called in one of those two, the other process is not effected.
* On success, the pid of the child process is returned

Condition where is fails:
* fork() fails to allocate the necessary kernel structures when memory is tight.

## stat()

* gives information about a file
* int stat(const char \*pathname, struct stat \*statbuf);
* pathname is the location of the file, statbuf is the buffer where the information will be stored
* 0 is returned on success, -1 on error

## kill()

* sends a signal to any process group or process
* if pid is positive, sig is sent to a specific process with the given pid
* if pid equals 0, sig is sent to every process in progress group
* if pid equals -1, sig is sent to every process for which the calling process has permissions to send signals
* if pid is less than -1, then sig is sent to every process in the
process group whose ID is -pid
* on success 0 is returned, on error -1
* fails if the process does not have permission to send the signal to any of the target processes.

## mmap()

* maps files or devices into memory
* void \*mmap(void \*addr, size_t length, int prot, int flags, int fd, off_t offset);
* on success, a pointer to the mapped area is returned. On error, MAP_ERROR is returned.

## chmod()

* changes permissions of a file
* int chmod(const char \*pathname, mod_t mode);
* pathname is the location of the file, mode is the new permission the file
* on success, 0 is returned, on error eather: EACCES, EFAULT, EIO, ELOOP, ENAMETOOLONG, ENOENT, ENOMEM, ENOTDIR, EPERM, EROFS, EBADF, EINVAL or ENOTSUP
* fails if the file does not exist.

## waitpid()

* waits for a process to change his state
* pid_t waitpid(pid_t pid, int \*status, int options);
* status is the pointer to the position, where the actual status is stored.
* on success, 0 is returned, on error, -1 is returned

## exec
* fails if the number of bytes in the new process's argument list is greater than the system-imposed limit of ARM_MAX bytes.

## unlink
* fails if the pathname points outside of accessible address space

## read
* fails if fd is not a valid file descriptor or is not open for reading

## mount
* fails if one of the pointer arguments points outside the user address space.

# Trap
A trap, also known as exception or fault, is a type of synchronous interrupt caused by an exceptional condition (e.g. a division by zero, invalid memory access). A trap usually results to switch into kernel mode. Before the process can continue, the OS performs some actions.
