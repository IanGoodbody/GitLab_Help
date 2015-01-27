# GitLab_Help
GitLab Setup for 383, and some command line

This is intnded to be a help document for setting up GitLab for ECFE 383. I have set up the sections in an order that makes sense to me, or at least in the order I am using to fix up my machine for this class. I will be doing most of what I can through the console so that you can get familair with that too. Feel free to skip to what you need, but overall I think most of it will be helpful.

---

### Rooting Out the Octodex

Every time you run the `git init` command the Git Bash shell the Octodex (the github mascot cat-thing) will install a `.git` directory in your current working directory. For example, say I accidently messed up and ran `git init` in my downloads directory.

![alt text]('Example 1')

The first command is `cd` which changes the working directory, which git shows in yellow. Notice how after I ran `git init` the (master) tag was created after the working directory. What git does is create a "master" branch in this directory for a given project. This is part of the version control aspect of Git Bash which you can learn about [here]("http://git-scm.com/documentation"). 

The next command, `$ ls -A`, lists all the files in the working directory with the `-A` tag showing all hidden files. (More bash commadns can be found on [SS64]("http://ss64.com/bash/"), it will run you through almost anything that involves a shell). Any directory name prefaced with a `.` (ie `.git`) will be hidden and only show up unless a special tag is used. This can also be accomplished by going into your preferances in windows explorer and choosing to show hidden files.

Git Bash has no command to remove a repository, therefor you have to go in and do it the hard way. That either means displaying hidden folders and files then doing a nice Shift+Delete to perminately delete it without a second thought. Or you can run the bash command
```bash
rm -rf .git
```
which will get the job done too. When you are done the (master tag should go away.

![alt text](Example 2)

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

![alt text](Example 3)

Note: for some of us, this is a point where we will create our `README.md` document for the write up. Don't. Unlike Git Hub in 382, all of the write ups for this class have to be done on a GitLab Wiki written in Markdown. I Will cover this in a later section, and it is fairly intuitive once you get into GitLab, but for now just know that things are slightly different on the GitLab side.

### Client Side Git Bash

#### .gitignore

Once we have our directory set up and our repository initialized in a directory that contains (or will contain) all the lab project folders we can start setting up and using Git to track and commit files.

The first thing we will want to do is create our `.gitignore` file. This is a fairly simple text document that lists all the files that we want Git to not track, or, in our case, create a list of files we do want git to track.

Because `.gitignore` is invisible to the Git shell, I could not directly upload a file for simple download. Here are your options:

  1. Right click in your repository folder and create a text new text document, paste in the following code block, then rename the file as `.gitignore`, windows doesn't like it when you change the file extention but just click the the warning, your computer can deal with it

```
*
!*.vhd
!*.bit
!*.jpg
!*.ucf
!*.wcfg
```

  2. I uploaded a shell file that will create the `.gitignore` for you. Put the file in your repository, then with the Git Bash shell set to that directory type the command `build_gitignore.sh`. You can then us the command `cat .gitignore` to check that the file was created properly. See the example below.

![alt text](Example 4 "Fight the Sarcasm")

The code for the `.gitignore` follows the Unix shell wildcard conventions where the `*` is a symbol for *everything*. This tells our git shell to ignore everything except for any files with the extentions listed. The `*` lets the files have any name you want them  to have; the `!` act as a simple negation.

#### Adding and Committing

