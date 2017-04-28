---
layout: post
title: Howto Convert SVN to GIT
permalink: howto-convert-svn-git/
description: A small step-by-step example on how to move your source code from SVN to GIT.
category: coding
---

Today I'd like to share my solution for a common problem a lot of IT companies experience when finally moving from Subversion (SVN) to Git as their central version control system (VCS): Converting a SVN repository into a Git repo including its commit history and authors.

To achieve this, I decided to split this issue into smaller pieces:

1. Extracting all authors of the SVN repository,
2. Creating a proper authors file mapping SVN users to Git users,
3. Converting SVN repo to Git including its history and authors.

Here is what I did:

## Converting SVN to GIT w/ History & Authors

Checkout your SVN repository.

```
svn co SVN_REPO_URL
```

Go into the repo directory and extract authors from the SVN repo [using this statement](http://stackoverflow.com/questions/2159567/what-is-the-format-of-an-authors-file-for-git-svn-specifically-for-special-char).

```
svn log --xml | grep author | sort -u | perl -pe 's/.>(.?)<./$1 = /'
```

Using this information, create an authors.txt file like this:

```
# SVN_AUTHOR_HANDLE = GIT_AUTHOR_HANDLE <GIT_AUTHOR_EMAIL>
jbrennenstuhl = jbspeakr <jan@brennenstuhl.me>
...
```

Using this file you now can start converting your SVN repo into a Git repo.

```
git svn clone -A authors.txt SVN_REPO_URL
```

This will convert the old SVN repo into a new Git repo including the complete SVN history and mapping its authors following the mapping in authors.txt. Depending on the dimension of the SVN repo history, this can take several minutes or even hours!

If you don't want to have the entire SVN history you could choose to start from a specific revision like this:

```
git svn clone -rSVN_REVISION:HEAD -A authors.txt SVN_REPO_URL
```

Still using SVN? Start converting to Git now!
