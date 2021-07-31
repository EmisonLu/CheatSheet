# Git

## Update a forked repo with git rebase

**Step 1:** Add the remote (original repo that you forked) and call it “upstream”.

```
git remote add upstream https://github.com/original-repo/goes-here.git
```

**Step 2:** Fetch all branches of remote upstream.

```
git fetch upstream
```

**Step 3:** Rewrite the master with upstream’s master using git rebase.

```
git rebase upstream/master
```

**Step 4:** Resolve all conflicts manually, mark them as resolved with command below.

```
git add/rm <conflicted_files>
```

**Step 5:** Skip this commit.

```
git rebase --skip
```

**Step 6:** Push the updates to master.

```
git push origin master --force
```

