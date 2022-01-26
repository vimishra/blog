---
title: "Remove Submodule From Git"
date: 2021-07-22T16:19:48+05:30
draft: false
tags: ["git"]
---

In order to remove a submodule from git, you need to follow the below 4 steps. 

1. Delete the relevant line from the `.gitmodules` file.
2. Delete the relevant section from `.git/config`.
3. Run `git rm --cached path_to_submodule` (no trailing slash).
4. Commit and delete the now untracked submodule files.

## Example

In my blog repo, I was trying multiple different themes and so had added a ton of submodules. Here is `.gitmodules` file.

```shell
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ cat .gitmodules
[submodule "public"]
	path = public
	url = https://github.com/vimishra/vimishra.github.io.git
	branch = main
[submodule "themes/PaperMod"]
	path = themes/PaperMod
	url = https://github.com/adityatelange/hugo-PaperMod.git
[submodule "themes/strange-case"]
	path = themes/strange-case
	url = https://github.com/ExchangeRate-API/strange-case.git
[submodule "themes/hugo-bootstrap-5"]
	path = themes/hugo-bootstrap-5
	url = https://github.com/NotWoods/hugo-bootstrap-5.git
[submodule "themes/hugo-coder"]
	path = themes/hugo-coder
	url = https://github.com/luizdepra/hugo-coder.git
[submodule "themes/hello-friend-ng"]
	path = themes/hello-friend-ng
	url = https://github.com/rhazdon/hugo-theme-hello-friend-ng.git
[submodule "themes/hyde"]
	path = themes/hyde
	url = https://github.com/spf13/hyde.git
[submodule "themes/hyde-hyde"]
	path = themes/hyde-hyde
	url = https://github.com/htr3n/hyde-hyde.git
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
```
I intend to keep papermod theme and will show how to delete `strange-case` theme. After cleaning up the `.gitmodules` and `.git/config` files, this is how they look.

```shell
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ cat .gitmodules 
[submodule "public"]
	path = public
	url = https://github.com/vimishra/vimishra.github.io.git
	branch = main
[submodule "themes/PaperMod"]
	path = themes/PaperMod
	url = https://github.com/adityatelange/hugo-PaperMod.git
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ cat .git/config     
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
	ignorecase = true
	precomposeunicode = true
[submodule "public"]
	url = https://github.com/vimishra/vimishra.github.io.git
	active = true
[remote "origin"]
	url = https://github.com/vimishra/blog.dev.repo.git
	fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
	remote = origin
	merge = refs/heads/main
[submodule "themes/PaperMod"]
	url = https://github.com/adityatelange/hugo-PaperMod.git
	active = true
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
```
Then I ran a bunch of `git rm --cached commands`. Here is the summary.
```shell
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ git rm --cached themes/hello-friend-ng
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ git rm --cached themes/hyde-hyde
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ git rm --cached themes/hyde
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ git rm --cached themes/hugo-coder/
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ git rm --cached themes/hugo-bootstrap-5/
~/devel/blog.dev.repo (main) [*] via  v16.5.0 
➜ git rm --cached themes/strange-case/
```

This was followed by a `git add` and a `git commit -a` command to turn in all these commits.