
```bash

# check which commits you want to merge
git log ^{commit-before-first} {last-commit} --reverse -- {directory}

# cherry-pick the hashes of the commits you want to merge
git cherry-pick $(git log ^{commit-before-first} {last-commit} --pretty=format:"%h" --reverse -- {directory})

# if there are any conflicts, solve them and then
git commit --allow-empty
git cherry-pick --continue

```