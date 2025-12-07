## Analysis Questions

1. **Security Risk**: Why is a world-writable directory (like `uploads/`) more dangerous than a world-writable file?
What could an attacker do?

This is definitely a huge security risk, as an attacker would have more access in general, since a directory can have multiple files compared to just a single file. In addition, with a world-writable directory, an attacker can create, delete, or replace multiple files (replace them with malicious scripts) since anyone on the system can modify the contents of that file.

2. **Permission Bits**: Explain what `-perm -002` means versus `-perm /111`. Why do we use different options for
different searches?

`-perm -002` means that an item is world-writable, regardless of other permission bits, anyone on the system can write to it. On the other hand, `-perm /111` matches files that have an execute bit, which can be used for finding anything executable. So `-perm -002` is used for finding world-writable items where other people have write access, while `-perm /111` is used to find files that are executable by someone that isn't just world-accessible.


3. **Real-World Impact**: If you ran this scanner on a production web server and found 50 world-writable files, what immediate actions should you take?

If I ran this scanner and found 50 world-writable files, I would immediately get rid of the world-write permissions from those files, setting them so that only I have access or a specific group of people. I would then attempt to determine what, if anything, malicious or not, has been altered in the files. Finally, I would identify the cause and restore any affected files from a clean backup if necessary, and then set up regular scans.


4. **Process Substitution**: Explain why using `find ... | while read` doesn't work for counting, but `while read ... done < <(find ...)` does. What is the difference?
Using `find ... | while read` doesn't work for counting because the while loop uses a shell created by the pipeline, so if a change occurs to a variable like counter, it is lost when the subshell exits. On the other hand, `while read ... done < <(find ...)` works because the loop runs in the current shell, and variable updates carry over after the loop ends.


5. **Automation**: How would you schedule this script to run automatically every day at 2 AM and email the results to a security team?
To do this, I would add something along the lines of: 0 2 * * * /usr/bin/CUS1163-LAB10/security_scanner.sh | mail -s "Security Results" team@gmail.com
