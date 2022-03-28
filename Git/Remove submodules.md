* Delete the relevant section from the `.gitmodules` file.
* Stage the `.gitmodules` changes:`git add .gitmodules`
* Delete the relevant section from `.git/config`.
* Remove the submodule files from the working tree and index:`git rm --cached path_to_submodule` (no trailing slash).
* Remove the submodule's `.git` directory:`rm -rf .git/modules/path_to_submodule`
* Commit the changes:`git commit -m "Removed submodule <name>"`
* Delete the now untracked submodule files:`rm -rf path_to_submodule`

[](https://git.wiki.kernel.org/index.php/GitSubmoduleTutorial#Removal)[https://git.wiki.kernel.org/index.php/GitSubmoduleTutorial#Removal](https://git.wiki.kernel.org/index.php/GitSubmoduleTutorial#Removal)