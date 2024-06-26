# git diff
- shows the diff between working with staging 
- you can use commit hash or branch too

The `git diff` command is used to display the differences between two states of the repository. Here's a breakdown of how it works and some common use cases:

1. **Show changes in the working directory**: If you've made changes to your files but haven't staged them yet, you can see the differences between the current state of your working directory and the last commit using:
`git diff`
  
2. **Show changes in the staging area (index)**: If you've staged changes using `git add` but haven't committed them yet, you can see the differences between the staging area and the last commit using:
`git diff --cached`
This command compares the changes you've staged with what's currently committed.

3. **Compare between two commits**: You can compare any two commits by providing their commit hashes:

`git diff <commit1> <commit2>`
This command shows the difference between the two specified commits.

4. **Compare a file between two commits**: To compare changes in a specific file between two commits, you can use:
`git diff <commit1> <commit2> -- <file>`
This command shows the differences in the specified file between the two commits.
   
5. **View changes in a specific branch**: You can also use `git diff` to compare the changes between your current branch and another branch:
 `git diff <branch_name>`
 This command shows the differences between the current branch and the specified branch.

## how to read diff
```sh
$ git diff
diff --git a/index.html b/index.html
index 4f75fde..41ca6e8 100644
--- a/index.html
+++ b/index.html
@@ -3,7 +3,7 @@
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
-    <title>Document</title>
+    <title> Index file </title>
 </head>
 <body>
     footer was added successfully
```

Here + and - are not addition or deletion. This is just to show the two files.
```sh
--- a/index.html
+++ b/index.html
```

line numbers
```sh
@@ -3,7 +3,7 @@
```

actual changes
```sh
-    <title>Document</title>
+    <title> Index file </title>
```

what you can do after git diff?
```sh
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

$ git add index.html

$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   index.html
```

to view the git diff of a staged file
```sh
$ git diff --staged
diff --git a/index.html b/index.html
index 4f75fde..41ca6e8 100644
--- a/index.html
+++ b/index.html
@@ -3,7 +3,7 @@
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
-    <title>Document</title>
+    <title> Index file </title>
 </head>
 <body>
     footer was added successfully
```


### difference between two commits

```sh
$ git log --oneline
3e505b4 (HEAD -> master) update index file
553d125 Merge branch 'footer'
5149ec0 (footer) update index file
2020251 add footer in index file
56ff0b5 add footer section to the code base
4fc3120 Merge branch 'nav-bar'
8076f8a add hero section to the code base
30217fe added navbar.html
c5ac897 added index.html
a9916ae initial commit
```


```sh
$ git diff 3e505b4 4fc3120
The most similar command is
	status
diff --git a/footer.html b/footer.html
deleted file mode 100644
index 61d4aaf..0000000
--- a/footer.html
+++ /dev/null
@@ -1,3 +0,0 @@
-<footer>
-    nice footer
-</footer>
\ No newline at end of file
diff --git a/index.html b/index.html
index 41ca6e8..d01f779 100644
--- a/index.html
+++ b/index.html
@@ -3,9 +3,9 @@
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
-    <title> Index file </title>
+    <title>Document</title>
 </head>
 <body>
-    footer was added successfully
+
 </body>
 </html>
\ No newline at end of file
(END)
```

or you can use 
```sh
$ git diff 3e505b4..4fc3120
diff --git a/footer.html b/footer.html
deleted file mode 100644
index 61d4aaf..0000000
--- a/footer.html
+++ /dev/null
@@ -1,3 +0,0 @@
-<footer>
-    nice footer
-</footer>
\ No newline at end of file
diff --git a/index.html b/index.html
index 41ca6e8..d01f779 100644
--- a/index.html
+++ b/index.html
@@ -3,9 +3,9 @@
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
-    <title> Index file </title>
+    <title>Document</title>
 </head>
 <body>
-    footer was added successfully
+
 </body>
 </html>
\ No newline at end of file
(END)
```


### difference between two branches
```sh
$ git diff master footer
diff --git a/index.html b/index.html
index 41ca6e8..4f75fde 100644
--- a/index.html
+++ b/index.html
@@ -3,7 +3,7 @@
 <head>
     <meta charset="UTF-8">
     <meta name="viewport" content="width=device-width, initial-scale=1.0">
-    <title> Index file </title>
+    <title>Document</title>
 </head>
 <body>
     footer was added successfully
(END)
```

or you can use git diff master..footer

# git stash

The `git stash` command is used in Git to temporarily store changes that are not ready to be committed yet, allowing you to work on another task or switch branches without committing your changes. It's useful when you need to quickly switch to a different branch or pull in changes from another branch without committing your current changes.
conflicting changes do not allow to switch the branches, without commit.
it is like a temporary shelf.

```sh
$ git stash
Saved working directory and index state WIP on master: 3e505b4 update index file

$ git stash list
stash@{0}: WIP on master: 3e505b4 update index file

$ git stash pop
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   footer.html

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (a058137ffc829f33517757a6e9dcff8ffa9ec973)
```

you can pop the changes from one branch to another.

if you have multiple stash, you can apply stash by 
```sh
git stash pop stash@{2}
```
