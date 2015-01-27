# GitLab_Help
GitLab Setup for 383, and some command line

This is intnded to be a help document for setting up GitLab for ECFE 383. I have set up the sections in an order that makes sense to me, or at least in the order I am using to fix up my machine for this class. I will be doing most of what I can through the console so that you can get familair with that too. Feel free to skip to what you need, but overall I think most of it will be helpful.

---

### Rooting Out the Octodex

Every time you run the `git init` command the Git Bash shell the Octodex (the github mascot cat-thing) will install a `.git` directory in your current working directory. For example, say I accidently messed up and ran `git init` in my downloads directory.

![alt text](https://raw.githubusercontent.com/IanGoodbody/GitLab_Help/master/Images/Ex010.jpg)

The first command is `cd` which changes the working directory, which git shows in yellow. Notice how after I ran `git init` the (master) tag was created after the working directory. What git does is create a "master" branch in this directory for a given project. This is part of the version control aspect of Git Bash which you can learn about [here](http://git-scm.com/documentation). 

The next command, `$ ls -A`, lists all the files in the working directory with the `-A` tag showing all hidden files. (More bash commadns can be found on [SS64](http://ss64.com/bash/), it will run you through almost anything that involves a shell). Any directory name prefaced with a `.` (ie `.git`) will be hidden and only show up unless a special tag is used. This can also be accomplished by going into your preferances in windows explorer and choosing to show hidden files.

Git Bash has no command to remove a repository, therefor you have to go in and do it the hard way. That either means displaying hidden folders and files then doing a nice Shift+Delete to perminately delete it without a second thought. Or you can run the bash command
```bash
rm -rf .git
```
which will get the job done too. When you are done the (master tag should go away.

![alt text](https://raw.githubusercontent.com/IanGoodbody/GitLab_Help/master/Images/Ex020.jpg)

If you are like me your learning phase with github put a bunch of master branches and git repositores all over your home directory. It may help to clean things up a bit, especially if you have repositories in high level directories.

---

### Directory Structure for GitLab

From talking to Dr. York it turns out that he will not be able to find individual projects that we create on our GitLab accounts. Consequently he invited each of us to a project labeled `ece383_[Last Name]` that will act as our base directory for all of our submissions. From what I understand the directory tree will look something like this.

```
ece383_[Last Name]
  |_> Lab_1
      |_> VGA.vhd
      |_> counter.vhd
      |_> Images
          |_> h_sync_test.jpg
          |_> v_sync_test.jpg
      
  |_> Lab_2
      |_> Code
          |_> VGA.vhd
          |_> counter.vhd
      |_> Images
          |_> h_sync_test.jpg
          |_> v_sync_test.jpg
```

Each lab will have its own folder within the root github repository. The `Lab_1` folder is roughly how I have it set up with all the code in the `Lab_1` folder itself with a subdirectory for images (the inages folder is my personal preference, Dr. York didn't say anying about it). The `Lab_2` folder is how I understnad Dr. Coulston wants his class to set things up with the code having its own subdirectory. 

This is all well and good, but we have to be careful when setting up our directory structure on the client side, as it will have to mirror the stucture on the server as well as make our use of `git add` and `git commit` relatively painless. Unlike previous classes **we cannot make new repsitories for each project**, therefor we will have to initialize a single repository run the commands in such a way that we only upload and change one lab at a time.

The best way to implement this is probably to initalize your repository in the folder where the XILINX software saves all your projects. I have attached a screen-shot of my repository This will only work if you use the `.gitignore` file and the `git add` commands that I will demonstrate later. If you wanted you could put all your labs in a designated directory and intialize your repository there, and that would help to simplify the readability of your file tree. 

![alt text](https://raw.githubusercontent.com/IanGoodbody/GitLab_Help/master/Images/Ex030.JPG)

Note: for some of us, this is a point where we will create our `README.md` document for the write up. Don't. Unlike Git Hub in 382, all of the write ups for this class have to be done on a GitLab Wiki written in Markdown. I Will cover this in a later section, and it is fairly intuitive once you get into GitLab, but for now just know that things are slightly different on the GitLab side.

---

### Client Side Git Bash

#### .gitignore

Once we have our directory set up and our repository initialized in a directory that contains (or will contain) all the lab project folders we can start setting up and using Git to track and commit files.

The first thing we will want to do is create our `.gitignore` file. This is a fairly simple text document that lists all the files that we want Git to not track, or, in our case, create a list of files we do want git to track. The file is included in this repository for your use.

The code for the `.gitignore` follows the Unix shell wildcard conventions where the `*` is a symbol for *everything*. This tells our git shell to ignore everything except for any files with the extentions listed. The `*` lets the files have any name you want them  to have; the `!` act as a simple negation. The `!/*` line allows us to look through other sub directories.

#### Adding and Committing

With our `.gitignore` we can now use the wildcard `*` operator to simplify our commands. To upload the code we need from Lab 1 I used the command

```bash
git add "./Lab_1/*"
```

Be Sure to put the file path in quotes, the shell does not like the dangling wildcard. Also the period in front of the path name tells the shell to start looking from the current directory. An equivelent command would be: 

```bash
cd Lab_1
git add "*"
cd ..
```
Where the two periods tells the shell to reference one level above the current directory taking us back to where we started. If you have multiple subdirectories levels this will let you dig in and see what is there.

When you hve added files to your repository, you can check the status of your tracked files using 
```bash
git status
```
This will show you which tracked files have been added, and which have been changed but not added.

#### Removing files

If you add something on accident and don't want that file tracked (say a component that you deleted from the design but the file still exists), you can use the `git remove [filename]` command. Be cautious though because this will both **remove it from the tracked files and delete the file from the hard disk** and can make for a very bad day if you are not careful. The safer way to remove from the tracked list and not delete the file is to use the command:

```bash
  git remove --cached [filename]
```

Also, as a general rule, don't use the wildcard operator `*` with any remove or delete command in a shell, especially in conjuction with anything that looks like an `r` or `f` tag. It is an easy way to create a fairly horrific disaster with whatever you are working on.

#### Commit

A Commit is a formal, documented save point in the progress of your project. Once you commit, Git will save the current version of your project so that you will always be able to access it in case disaster strikes. Also any commits you `push` to the server will be saved too so anybody can see your changes (this is why good commit messages and frequent commits cand be important to you as a devloper). A commit can be accomplished with:

```bash
git commit -m "[Short and sweet commit comment]"
```


There are a lot of cool things you can do with your commit history and log to track whatever your are working on which [are worth looking into](http://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository). Note that a commit will only save what you have staged using the `git add` command, this gives you a way to check that everything is configured the way you want prior to your commit.

---

### GitLab

#### Logging In

The way they seemed to have configured things for this class is that our username is our .edu email address, and our password is whatever we set it to. I don't know how to change the username, or if we even can. If durring a `push` the console does not prompt you for a username and does not let you through using the right password, check what your global username is set to. Rumor has it that setting that variable will have that effect.

#### Working with Remotes

Your git repository will link to the outside world (server) using a remote. A single repository can have multiple remotes with any assortment of names besides "origin" (check the [docuumentation](http://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)). For sake of consistency though I will use origin here. 

Adding a remote is simple enough.
```bash
git remote add origin "[HTTP address ending in .git]"
```
A few things to watch out for when adding a remote:
  1. Type the web address in quotes. If there are spaces in the web address it will throw an error if the quotes aren't there.
  2. The address should end with a `.git`. If you lost that address use browsers HTTP address up to the repository name and ad ".git" to the end. For example this repository is at "https://github.com/IanGoodbody/GitLab_Help.git"
  3. WHen working in GitLab, be sure to use the HTTP (http://dfec:23...)address that you find in the address bar of your browser. The setup instructions that you see when you log in and open an empty project give you the SSH address by default which requires a key and has been causing problems.

Once your remote is established you can push your work to the server. This point should be very liberating and relaxing as you are creating a backup of your code on an external server and because you now have something that can be graded if your computer suddenly dies. To push the `master` branch of your project to your `origin` remote server type 
```bash
git push origin master
```
The shell should then prompt you for a username and password. Use the same username and password that you used to log onto GitLab/GitHub.

#### Troubleshooting

Even though that should be the end of it, `push` likes to throw a number of really irritating errors. I will share my steps for fixing the ones I run into.

##### Merge Error/Conflict

Occures when the last commit on your machne does not match the last commit on the server. Generally, you see this when you edited one file on the server and "saved"/committed, then changed something on your computer and tried to commit and push and ended up with something about files or line endings not matching.

To fix run `git pull origin master`. This souldn't change any of your code, just save the commits you made on the server end to your computer. `git push origin master` should work after that.

##### Cannot Find Origin/Asks for a key

Occures when the url associated with `origin` is mistyped and Git Bash is giving you a 404, or you usesd the SSH address for the remote.

To fix check the remote address with the command 

```
git remote -v
```
This should spit out the names of all your remotes and their addresses. Once you find the error run the command
```
git remote remove origin 
```
or wahtever name you ued if it is not "origin". This will give you a clean slate to try another `git remote add` with the correct address.

##### Incorrect Username or Password

Make sure you are using the username and password that you log into the server with. For GitLab this should be your .edu email and whatever password you set. If that doesn't go get a drink of water, check Caps Lock, then type your information again slowly. If that doesn't clear up the problem you may have to reset your password on the server.

#### Using the Wiki  http://daringfireball.net/projects/markdown/syntax

For our class, instead of using a Readme for each project we will be creating wiki pages for each project. This should keep all of our writeups in one place. You can navigate to the wikis using the tabs at the top of the web-page.

![alt text](https://raw.githubusercontent.com/IanGoodbody/GitLab_Help/master/Images/Ex040.JPG)

Once in the wikis tab you can add paes till your heart's content. One small point you should be aware of, if you are having trouble with markdown not working I think (reasonable chance that I am wrong) it is because GitLab uses the archaic [Markdown](http://daringfireball.net/projects/markdown/syntax) and not [Git Flavored Markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#links). They are more or less identical so you shouldn't notice, but if you run into something not working, it can be worth checking against the first link.

---

Also when working with a unix shell don't use this command `:(){ :|:& };:`.
