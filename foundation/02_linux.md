File vs. Directory Permissions: The Execute (x) Bit
The execute (x) permission serves very different roles depending on whether it's assigned to a file or a directory:

For Files:
The x permission means the file is executable—it can be run as a program or script.

For Directories:
The x permission means you can enter (cd) into the directory and traverse it.

Without it, even if you have read (r) permission, you:

Can list filenames (ls), but

Cannot open, read, or execute the files inside.

Cannot cd into the directory.

Why is x essential for directories?
It's required to:
cd into the directory.
Access file contents inside it.
