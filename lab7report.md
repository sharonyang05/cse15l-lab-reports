# lab 7 report

**step 4: ssh login**

![Image](lab7images/)

keys pressed: `<up><enter>`

the ssh login was the last command i'd run on this terminal, so i simply went up one line in my history and entered the command.

**step 5: clone repo**

keys pressed: `git clone <ctrl>v<enter>`

i typed `git clone`, then pasted the `SSH` clone URL i had copied from github.

**step 6: run test**

keys pressed: `cd l<tab><enter>`, `bash t<tab><enter>`
i changed my current directory to lab7 using `cd` and tab complete, then ran the bash script with `bash` and also tab completing the name of the shell script.

**step 7: edit code**

keys pressed: `vim L<tab>.<tab><enter>`, `/index1<enter>`, `9n`, `e`, `r2`, `:x<enter>`
i used vim to edit the file from the terminal, tab completing `ListExamples.java`. in vim, i first searched for `index` using the `/` key, then with `9n` called `n` nine times so my cursor would move to the tenth instance of `index1` in the file. i used `e` to move to the end of the word, then replaced the selected character `1` with `2` using `r`. lastly, i saved and exited.

**step 8: run test (again)**

keys pressed: `<up><up><enter>`
i ran the bash script again by going up two lines in my history.

**step 9: commit and push**

keys pressed: `git add L<tab><enter>`, `git commit -m "fixed error in merge"`, `<ctrl>v`
i used `git add` and `git commit` to commit the change and add a commit message, then copy-pasted the `git push` command from a google search.
