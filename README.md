HPDM172 Git Tutorial - University of Exeter - 2024

This tutorial assumes you have Git installed,
For setup something you can do to start is setup your identity. This identifies you to
As a helpful step, if you're run Linux, you may want to set Git to use your favourite editor
First steps - starting with Git on command line
-----------------------------------------------
    $ git clone https://github.com/neilvaughan/git-workshop.git
Now try to run this command:
    $ git add

This will cause an error because we have not navigated into the git repository folder yet:

![image](https://github.com/user-attachments/assets/e040f572-f5ca-437d-a990-cdfed7005552)

Next, move into the git repository folder and list the contents, by using these commands:

    $ dir

![image](https://github.com/user-attachments/assets/09d9d9ce-97fb-4ded-b804-277595754665)

To explore further, you can also check to see if there are also hidden files.

    $ dir /a:h
![image](https://github.com/user-attachments/assets/8636fc9d-e724-4daa-b85e-4c280349dad1)
You should also see hidden the `.git` subdirectory. This is
    $ cd .git
    $ dir
Now you can navigate back to the parent folder. 

    $ cd ..

If you no longer wanted to have this cloned repository on your 
local machine, you can simply delete the whole folder. That won't
have any effect on the remote server's copy of the repository.
You could then clone the repository again later on if you wanted to
by using the same method we have just done.

Let’s create two files named `test.txt` and `file2.txt`.

    $ echo hello > text.txt
    $ echo file contents > file2.txt
To verify that the files have been created, type:

    $ file2.txt

This should open up one of the new text files and show some text inside it.
    $ git add test.txt file2.txt
    Author: NeilVaughan
    Date:   Sun Jul 16 13:13:42 2024 +0100
        diff --git a/file2.txt b/file2.txt
        new file mode 100644
        index 0000000..be1d686
        --- /dev/null
        +++ b/file2.txt
        @@ -0,0 +1 @@
        +file contents
        diff --git a/test.txt b/test.txt
        new file mode 100644
        index 0000000..f2aa86d
        --- /dev/null
        +++ b/test.txt
        @@ -0,0 +1 @@
        +hello

![image](https://github.com/user-attachments/assets/b6a832b9-35ab-487b-be9b-79a6f19512bd)


Another feature of git
some content to test.txt.
Open `test.txt` in notepad or using the command below, to add any new text into the file.
        $ echo This is a new line of text in the test file. > test.txt
If using notepad, remember to **save** the file.
Now we may want to see what has changed in the file. A very useful command is `git diff`.
This is very useful to see exactly what changes you have done.
    diff --git a/test.txt b/test.txt
    index f2aa86d..7ca0bdf 100644
    --- a/test.txt
    +++ b/test.txt
    @@ -1 +1 @@
    -hello
    +This is a new line of text in the test file.

![image](https://github.com/user-attachments/assets/591cf27b-0429-4de8-8c31-4c1e1c06f895)
Now let’s add our modified file, `test.txt` to the staging area. Do you
remember how? Use the git add command shown below.

    $ git add test.txt

Next, check the `status` of `test.txt`. Is it in the staging area now?
Status can be checked using the git status command.

    $ git status

You should see something like this:

C:\Users\nv266\git-workshop>git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test.txt

![image](https://github.com/user-attachments/assets/17c29467-1edd-4482-b778-d6639b36c7b8)
Let’s say we changed our mind about putting the new text into `test.txt`. One
    $ git reset HEAD test.txt
You should see this message:
    M   test.txt

![image](https://github.com/user-attachments/assets/3127466e-3797-4efb-bcfa-43c0208b24c1)
    $ git status

Now there should be no changes, so it shows this message:

"no changes added to commit (use "git add" and/or "git commit -a")"
Your staging area should now be empty. 

But what’s happened to the new text changes that we added? 
It’s still there. We are now back to the state just
Open the 'test.txt' file to check the contents:

    $ test.txt

You will see that the new text that was added to the file is still there:

This is a new line of text in the test file. 

just before we added the new text to `test.txt`.
    $ git checkout test.txt

You have now un-done your changes. 
    $ test.txt
You will see that the test.txt file now has reverted to the original text 'hello'.
`main`.

![image](https://github.com/user-attachments/assets/0e61002f-fcca-4349-86e2-080951a6004b)
    * exp1
      main
    $ echo 'experimental content' > exp.txt
    $ git add exp.txt
Now, let’s compare them to the main branch. Use `git diff`
    $ git diff main
![image](https://github.com/user-attachments/assets/0f7b48ea-8048-40b1-af0a-78dd7d16f301)
Basically what the above output says is that `exp.txt` is present on
the `exp1` branch, but is absent on the `master` branch.
Disappearing Files between branches
-----------------------------------
Try switching back to the main branch (Hint: It’s the same command we
    $ git checkout main

Now, where’s our `exp.txt` file ?
    $ dir
    README.md  text.txt   file2.txt
As you can see the new file 'exp.txt' you created in the other 'exp1' branch has
disappeared. 

Even if you open the folder in windows explorer, the file is still disappeared:

$ start C:\Users\nv266\git-workshop

Not to worry, the exp.txt file is safely tucked away, and will re-appear
    $ git checkout exp1
    $ dir

    README.md  text.txt   file2.txt   exp.txt

Note that if you create a new file in one branch but do not use 
git add and git commit, then the file will be visible from other branches.
Git merging works by first switching into the branch you want to
merge *into*, and then running the command to merge the other branch in.
We now want to merge our `exp1` branch into `main`. First, switch to
    git checkout main
Next, we merge the `exp1` branch into `main` :
Do you see something like the following output ?
If one of the other files in exp1 branch had also been modified
as well, the message may be showing 2 file changes instead of 1.

![image](https://github.com/user-attachments/assets/00e0bb89-2d94-4e48-88b7-c9ad1f83768d)

how the two branches have merged. This may be available on linux but 
may need to be installed seperately, so you can skip this 'gitk' step.

If you wanted to you could now remove the experimental 'exp1' branch,
but there’s no harm in keeping it. You may need to look back at it in future.

Git is pretty good at merging automatically, even when the same file is
We'll now practise fixing merge conflicts. Recall that conflicts are caused
Create a new branch called newbranch

    $ git checkout -b newbranch

Now you can modify the code.txt file by swapping the order of the numbers
in the add and multiply sections.

    $ code.txt

For example:
Swap "sum = num1 + num2;" for "sum = num2 + num1;"
Swap "product = num1 * num2" for "product = num2 * num1"
Close and save the code.txt file.

When you use git diff to compare the two versions of code.txt you will see this:

    $ git diff main
![image](https://github.com/user-attachments/assets/702a26d3-3bd9-4b40-b591-67d45523fd23)
Now we will try to merge the two versions together:

    $ git checkout main
    $ git merge newbranch

Now you will see this merge error. It was not able to automatically merge:

![image](https://github.com/user-attachments/assets/b6997208-d29b-461c-923b-02b2e6229ace)
The End
-------
The End
-------