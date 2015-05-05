#Vim Cheat Sheet
Vim commands cheat sheet.

### Exit

Command | Explaining
------ | -----
:q[uit]  | Quit Vim. This fails when changes have been made.
:q[uit]!|	Quit without writing.
:cq[uit]|	Quit always, without writing.
:wq|	Write the current file and exit.
:wq!|	Write the current file and exit always.
:wq {file}|	Write to {file}. Exit if not editing the last.
:wq! {file}|	Write to {file} and exit always.
:[range]wq[!]	[file]| Same as above, but only write the lines in [range].
ZZ|	Write current file, if modified, and exit.
ZQ|	Quit current file and exit (same as ":q!").

### Editing

Command | Explaining
------ | -----
:e[dit]|	Edit the current file. This is useful to re-edit the current file, when it has been changed outside of Vim.
:e[dit]!|	Edit the current file always. Discard any changes to the current buffer. This is useful if you want to start all over again.
:e[dit]| {file}	Edit {file}.
:e[dit]!| {file}	Edit {file} always. Discard any changes to the current buffer.
gf|	Edit the file whose name is under or after the cursor. Mnemonic: "goto file".

### Inserting Text

Command | Explaining
------ | -----
a|	Append text after the cursor [count] times.
A|	Append text at the end of the line [count] times.
i|	Insert text before the cursor [count] times.
I|	Insert text before the first non-blank in the line [count] times.
gI|	Insert text in column 1 [count] times.
o|	Begin a new line below the cursor and insert text, repeat [count] times.
O|	Begin a new line above the cursor and insert text, repeat [count] times.

###Inserting a file

Command | Explaining
------ | -----
:r[ead] [name]|	Insert the file [name] below the cursor.
:r[ead] !{cmd}|	Execute {cmd} and insert its standard output below the cursor.

[Source](http://fprintf.net/vimCheatSheet.html)
