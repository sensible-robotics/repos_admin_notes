Goal:
=====
Given a public repository PUBLIC_REPO, and a fork from it, FORK_REPO which is also public and has a new branch (BRANCH_X); we wish to
create a private copy of the code that points to PUBLIC_REPO (for future PRs), and keep the changes from BRANCH_X,
so if FORK_REPO is deleted, the BRANCH_X changes survive and can potentially be pushed to PUBLIC_REPO one day.

Let's call our private copy PRIVATE_REPO.

Note: This [site](https://medium.com/@bilalbayasut/github-how-to-make-a-fork-of-public-repository-private-6ee8cacaf9d3) was inspiration for this solution.

Steps:
======
1. Mirror the repository, name it PRIVATE_REPO. Details are [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/duplicating-a-repository) . Set it to be private.
2. Get into it:
   ```
   cd PRIVATE_REPO
   ```
3. Add a remote to your PRIVATE_REPO, this remote will point to the fork:
   ``` 
   git remote add forked_starters git@github.com:MY_USER/FORK_REPO.git
   ```
4. Fetch the forked code:
   ```
   git fetch forked_starters
   ```
   You'll see the forked branches (e.g. BRANCH_X) been listed, in addition to other branches. E.g.:
   
   ```From github.com:MY_USER/FORK_REPO
   * [new branch]      BRANCH_1                  -> forked_starters/BRANCH_1
   * [new branch]      BRANCH_2                  -> forked_starters/BRANCH_2
   * [new branch]      master                    -> forked_starters/master
   * [new branch]      BRANCH_X                  -> forked_starters/BRANCH_X
   ```
5. Checkout forked_starters/BRANCH_X in a local branch:
   ``` git checkout -b local_BRANCH_X forked_starters/BRANCH_X
   ```
6. Push your local branch (which has the original BRANCH_X from the FORKED_REPO in it) back to your mirror under the name of BRANCH_X.
   ```git push origin -u local_BRANCH_X:BRANCH_X
   ```
 
 Done!
