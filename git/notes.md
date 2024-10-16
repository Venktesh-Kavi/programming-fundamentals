## Git Knowledge Base

### Dont use pull from remote

* Assume that there are two developers working on the same branch
```
Root: A
Dev1: A - A'
Dev2: A - A''
```
* When Dev2 pulls the commit from the branch. A new merge commit is created every time. 
```
  merge commit (A'-A'')
      |
   A' A''
   |  |
      A
```

* This affects the commit history with a lot of merge commits.

Solution
* Always perform git pull --rebase
* If there is merge conflict (eg.. between A' and A'') then use git merge to resolve the conflict.

### Maintaintaing a neat commit history

Squash and Merge
* Perform squash and merge. Each feature branch might have multiple merge commits because of merging base branch with feature branch
  throughtout the feature dev lifecycle.
* If merged without squashing, the commit history will have multiple merge commit in the git graph.
* Squash and merge to avoid this.

Rebase
* Use rebase when we want maintain a linear commit history.
* When many developers are working on a project, the commit history can go haywire with merges.
* Though the disadvantages of git rebases are:
    * Every conflicting commit has to be resolved while the rebase is in progress.
* Important Note: If your feature branch is already pushed to remote, never rebase it. [ref]([](https://www.youtube.com/watch?v=DkWDHzmMvyg&t=319s)https://www.youtube.com/watch?v=DkWDHzmMvyg&t=319s)

```
1/ git rebase main (the branch to rebase with)
2/ run through the commits
3/ git rebase --continue (enter the new commit message)
4/ git add
5/ git push
```
### Git Worktre

- Since git v2.5.0 (2015 release)

disadvantages of git stash

1/ Many rebuilds
2/ Only one active worktree is present with conventional git stash approach

Example:
If the codebase working has a longer build time. git stashing and swithcing to a new branch requires rebuild.
Similarly stash popping the changes in the current branch requires a rebuild

intro git worktree
* Always add worktree to the parent directory of the current working project. Nested worktree can cause confusions during file additions.

1/ git worktree add ../ex-hotfix-worktree
2/ git worktree list
3/ git worktree remove . (typically worktree stay longer to reduce rebuilds on branches like main)


