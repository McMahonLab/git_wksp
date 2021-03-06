[Up To Schedule](../../../README.md) - Back To [Make Incremental Changes II](../local/Revert_and_branch.md) - Forward To [Collaborate](../collaborate/Readme.md)

# Working with Github
----

**Based on material by Katy Huff, Anthony Scopatz, Sri Hari Krishna
Narayanan, and Matt Gidden**


### ![Exercise](../../../common/pics/exercise.jpg) Exercise : A little Review...

- Make a directory called 'git_rev'
- Initialize that directory as a git repo
- Make a README file, add and commit it
- Update the README file, and look a the differences since you last committed
- Add and commit the new changes.


## GitHub.com

GitHub is a site where many people store their open (and closed) source
code repositories. It provides tools for browsing, collaborating on and
documenting code. GitHub,
much like other forge hosting services ([launchpad](https://launchpad.net),
[bitbucket](https://bitbucket.org), [sourceforge](http://sourceforge.net),
etc.) provides :

-   landing page support
-   wiki support
-   network graphs and time histories of commits
-   code browser with syntax highlighting
-   issue (ticket) tracking
-   user downloads
-   varying permissions for various groups of users
-   commit triggered mailing lists
-   other service hooks (twitter, etc.)

**NOTE**: Repos are public **by default**. If you don't want
to share your stuff with the world, you can make a
private repo.  While that often costs money on Github, they now
have [education discounts](https://github.com/blog/1775-github-goes-to-school).

## GitHub Accounts

Setting up GitHub requires a GitHub user name and password.  Please take a
moment to [create a free GitHub account](https://github.com/signup/free). Some of the McMahonLab repos are private. You will need to keep your forks of those repos private too, so request an [educational discount](https://education.github.com/discount_requests/new) to get some free private repos. (We'll explain about forks later on in this tutorial.)

## git remote : Steps for Forking a Repository

From [Github](https://github.com/octocat/Spoon-Knife):

> Creating a fork is producing a personal copy of someone else's project. A fork
> acts as a bridge between the original repository and your personal copy. You can
> submit Pull Requests to help make other people's projects better by offering
> your changes to the original project. Forking is at the core of social coding at
> GitHub.

So, **forking** a repository on Github gives you a copy of that repository in
your Github account. **cloning** a repository gives you a copy of that
repository on your **local** machine. In order to connect your local copy and
the versions on Github, we tell your local copy that they exist, via **git
remote**.

The **git remote** command allows you to add, name, rename, list, and delete
repositories such as the original one **upstream** from your fork, others that
may be **parallel** to your fork, and so on.

In the McMahon lab, all __upstream__ repositories are stored on the [McMahonLab GitHub page](https://github.com/McMahonLab). We'll be continuing our testing exercises using the McMahonLab [simplestats](https://github.com/McMahonLab/simplestats) as the upstream repository,
so you'll need to start off by getting a copy of that repository to work on.

### Exercise : Fork Our GitHub Repository

Step 0 : Clean Up Your Local Space

We'll be interacting with remote repositories now, so let's clean up the
simplestats folder on your machine.

    $ cd
    $ rm -rf simplestats

**BE CAREFUL with rm -rf.** We are __only__ using it because git repos are write
protected and can't be deleted easily with out it.

Or if you'd like to keep it around

    $ cd
    $ mv simplestats old-simplestats

Step 1 : Go to our
[repository](https://github.com/McMahonLab/simplestats)
from your browser, and click on the Fork button. Choose to fork it to your
user name rather than any organizations.

Step 2 : Clone it. From your terminal :

    $ git clone https://github.com/YOU/simplestats
    $ cd simplestats
    $ git remote -v
    origin  https://github.com/YOU/simplestats (fetch)
    origin  https://github.com/YOU/simplestats (push)

Your local repository is now connected to the remote repository using the
alias `origin`.

Step 3 : Add a connection to the common repository :

    $ git remote add upstream https://github.com/McMahonLab/simplestats
    $ git remote -v
    origin  https://github.com/YOU/simplestats (fetch)
    origin  https://github.com/YOU/simplestats (push)
    upstream        https://github.com/McMahonLab/simplestats (fetch)
    upstream        https://github.com/McMahonLab/simplestats (push)

### Remote Naming Conventions

All repositories that are clones begin with a remote called `origin`, by
default.  The most common convention is clone from your own fork (`origin`). If
your fork is based on someone else's project (e.g., your research group's), you
should then add that repository as a remote named `upstream`.

## git fetch : Fetching the contents of a remote

Now that you have connected your repository to the "upstream" original, it
is able to pull in updates from that repository. In this case, if you
want your master branch to track updates in the original simplestats
repository, you simply **git fetch** that repository into the master
branch of your current repository.

    $ git fetch upstream

The fetch command alone merely pulls down information recent changes
from the original master (`upstream`) repository. By itself, the fetch
command does not change your local working copy. To update your local
working copy to include recent changes in the original (`upstream`)
repository, it is necessary to also merge.

## git diff : Examine the differences

Now that you have fetched the `upstream` repo, you can look at the differences
between that and your local copy.  To see a summary of which files have
changed and by how much:

    $ git diff --stat upstream/master

To explore the actual changes:

    $ git diff upstream/master

## git merge:

If you are satisfied with the changes, the final step is to merge the `upstream` repo into your local copy of the `master` branch:

```
$ git checkout master
$ git merge upstream/master
```

## git pull : Pull = Fetch + Merge

The command **git pull** is the same as executing **git fetch** followed
by **git merge**. Though it is not recommend for cases in which there
are many branches to consider, the pull command is shorter and simpler
than fetching and merging as it automates the branch matching.
Specifically, to perform the same task as we did in the previous
exercise, the pull command would be :

    $ git pull upstream master
    Already up-to-date.

When there have been remote changes, the pull will apply those changes
to your local branch, unless there are conflicts with your local
changes.

## git push : Sending Your Commits to Remote Repositories

The **git push** command pushes commits in a local working copy to a
remote repository. The syntax is git push [remote] [local branch].
Before pushing, a developer should always pull (or fetch + merge), so
that there is an opportunity to resolve conflicts before pushing to the
remote.

__Note__: The preferred way to push your commits to a remote repository is through a __pull request__. This will be discussed in the next section.

## Exercise: Update your remote to an upstream change

Assume that your lab group collectively works on a project (like `simplestats`),
and someone has updated the `master` branch (we can simulate that by a helper
doing an update -- helpers?).

It is now your job to:

* get the upstream changes
* check what files have changed and how
* apply them to your local repository
* apply them to your fork

hint: **don't** use `git pull`

----

[Up To Schedule](../../../README.md) - Back To [Make Incremental Changes II](../local/Revert_and_branch.md) - Forward To [Collaborate](../collaborate/Readme.md)
