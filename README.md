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

