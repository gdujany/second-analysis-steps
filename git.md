For starting make a development area:

```
lb-dev AlignmentOnline v11r0
cd AlignmentOnlineDev_v11r0/```

`git log --oneline`

a git repository has been set up for you :) and the initial commit has already been made

Now if you want to getpack some packages you first have to instruct git where to find them,
for the moment nothing is set as you can check with

`git remote -v`

for each project you want to get packages from you have to do

`git lb-use AlignmentOnline`

this set as a remote repository the official LHCb svn mirror and calls it with the name of the project

`git remote -v`

it also makes some magic to set up correctly your environment so you can ...

To not spam the official LHCb mirrored git repository we can fork them
(this is not needed for real developing but just for today's example)
Go to https://gitlab.cern.ch/LHCb-SVN-mirrors/AlignmentOnline/forks and press fork
When asked indicate your local area

now we can change the remote to point to your local fork instead of the official LHCb one so you can mess up without problems

For extra safety go to settings and remove the fork relationship (this also is not needed!)

```
git remote set-url AlignmentOnline ssh://git@gitlab.cern.ch:7999/gdujany/AlignmentOnline.git
git remote update```

```
git remote -v```

to see that indeed now you point to your fork

```
git lb-checkout AlignmentOnline/master AlignmentOnline/AlignOnline```


git log --oneline`

you can see that it downloaded the package wanted from the remote repository, added all the files to your local repository and made a commit

Now modify something

git status

git add

git commit -m "test"

git lb-push AlignmentOnline test

And now if you go in your forked version you will see that a new branch appeared

Now if you want to add it to the master you can make a merge request



Now what if someone has changed the master in the meantime?

N.B. this is still preliminary and hopefully at some point it  will be automated
git lb-checkout AlignmentOnline/master AlignmentOnline/AlignOnline
First let's change the master:

...


Now if we try to make the merge request we will fail

There are two ways to go: if we are generally happy with the status of the branch and just need to
fix the conflict we can use the standard git ways to modify the branch i.e.

clone the repository locally, fix the conflicts and push the changes back

```
imported=$(git config -f .git-lb-checkout lb-checkout.AlignmentOnline.AlignmentOnline/AlignOnline.imported)
git checkout $(git config -f .git-lb-checkout lb-checkout.AlignmentOnline.AlignmentOnline/AlignOnline.base)
git lb-checkout $imported AlignmentOnline/AlignOnline```

```
git lb-checkout AlignmentOnline/master AlignmentOnline/AlignOnline
git rebase HEAD master```

an alternative to test it is to checkout an old version eg
```
git lb-checkout AlignmentOnline/v11r0 AlignmentOnline/AlignOnline```
