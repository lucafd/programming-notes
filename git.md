---
title: "Git notes"
author: "ahzits"
---

[TOC]

# Beginner's notes

#### Git_tutorial 1->20

- From *lab08* I learn what is the difference between `reset` and `checkout` to delete the added files? the former unadd them singularly, the latter everyone at the same time. Moreover, `unstage` is a good alias for `reset HEAD`.

- The trick `add .` adds all the files because adds the current directory! In general if instead of `add` I had `checkout` there wouldn't be any problem

- *lab10* is good  to format the `log` and maybe to understand what I chose as `hist`:

```bash
git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"
```

- That's interesting, `checkout` selects also the head of the commit!

- other options for `hist` are `--max-count=1` and `--all`

- getting older versions: it's like doing things detaching the head,but with checkout I move onto the last version of the branch. Master or Main is the main branch.

- the parent of `v1` is `^v1` or `v1~1`. `tag` behaves like branches, only puts labels

- `checkout`resets everything that wasn't staged but only modified files, only those that existed before, instead `git clean` removes untracked.

- this is needed to do the revert without being verbose

```bash
 git revert HEAD --no-edit
```

- `revert` serve a creare un nuovo commit ma con il valore del commit precedente a quello che vogliamo togliere, HEAD  usato solo perché era proprio l'ultimissimo, per il resto non c'è nulla di male.

- `git reset --hard` resetta tutto a quello che c'è prima senza fare vedere nulla?

- as it seems `git reset` updates the indexes? however it sort of an opposite to `add` and with various options that modify the `reset` behaviour

- `amend` it is used to correct a little thing that you forgot without messing with the history: `git commit --amend -m`

- idem resetting the branch back one commit and then adding it again

- By using git to do the move (`git mv file dir`), we inform git of 2 things: that the file `hello.rb` has been deleted, and the file `lib/hello.rb` has been created. Both are staged and ready to be committed.

- show alias con git 

```
 git config --global alias.alias "! git config --get-regexp ^alias\. | sed -e s/^alias\.// -e s/\ /\ =\ /"
```

- I don't know why but `git checkout -- .` deletes untracked files

#### Git_tutorial 21->35

- vogliamo vedere come sono strutturati i file nella cartella git 

- beh object contiene gli oggetti ma compressi

- refs cosa contiene? sembra contenere tutti i riferimenti dei branch le loro teste e i tag che ho messo

- in the file with the name of the tag there is the hash code at which we applied the tag

- esiste anche un file HEAD che contiene il riferimento di dove sta la testa del nostro branch

- ok esiste il `cat-file -t` (stands for type) `-p` (dump) il primo dice il tipo di hash che ho invece il secondo dice la parentela mi sa e le caratteristiche del commit

- quindi l'hash che otetniamo dal tree è quello che poi ci dà i top file del commit che ho dumpato

- ci sono quei numeri che non mi convincono davvero
```bash
  $ git cat-file -p 6e4d252
  100644 blob 9ef219a9ab545099bacd762cf54bf33dbdd1a8a6    Rakefile
  040000 tree 48d6daf671a802c1ecb93e92068b8a650aad8332    lib
```

- ok sembra che i numeri 100644 e i loro hash siano codificati come file finali e invece l'altro codice sia per le directory, infatti se cerchiamo il parent otteniamo il file direttamente

- commit obj blob obj e tree obj sono i tre tipi di oggetti che ci sono qui, i commit obj sono nella cartella `.git`

- riesci a trovare il file originale seguendo direttamente il sha1 fino al file originale

- quando vuoi cambiare branch? quando le modifiche che fai potrebbero prendere un po'

- `git checkout -b <branchname>` is a shortcut for `git branch <branchname>` followed by a `git checkout <branchname>`.

- then `git merge b1 ` quando sono su b2 mergia b2 al b1 mantenendolo separato e aggiornando b2

- merging conflicts compare nel file come HEAD  e cose strane tipo la sha1 del commit da comparare o mergiare

- ricordati sempre dell'opzione di `git hist all` che torna spesso comoda

**differenza fra rebase e merge**

ora trattiamo questa differenza che direi che sembra importante:

- ok prima avevamo mergiato tutto senza fare troppe storie e vabbè ora però dobbiamo tornare indietro, per il rebase

- in pratica riscrive la storia in modo che i due fossero senza conflitti e con un albero di dipendenze molto lineare

- advice when never use rebase:

    -  If the branch is public and shared with others.  Rewriting publicly  shared branches will tend to screw up other members of the team.
    - When the *exact* history of the commit branch is important (since rebase rewrites the commit history)

    it is adviced for short lived local branches, merge for public repos

- ora rebase e merge fatti come abbiamo fatto servono a tenere aggiornato solo il secondo branch mentre master no. allora poi dobbiamo mergiare into master per chiudere tutto. ora vediamo dopo un rebase

- git fa i fastforward change perché la head of master è genitrice della testa di greet e quindi cambia solamente commit di riferimento

- ora greet e master puntano allo stesso commit

#### Git_tutorial 36->49

- error handling in multiple directories

- `git clone hello cloned_hello` clone things directly in the directory where you are 

- the name in branch is practically that one in origin

- `HEAD`  and `origin/HEAD` are different!!

- `git remote show origin` should show the origin directory

- The `git remote set-url` command takes two arguments:

    - An existing remote name. For example, `origin` or `upstream` are two common choices.

    - A new URL for the remote. For example:

        - If you're updating to use HTTPS, your URL might look like:

			```bash
          https://github.com/USERNAME/REPOSITORY.git
			```

        - If you're updating to use SSH, your URL might look like:
			```bash
            git@github.com:USERNAME/REPOSITORY.git
			```

- se mostro i branch solamente dovrei vedere solo master, gli altri come devo fare? `git branch -a` li dovrebbe mostrare tutti, in rosso quelli che sono solo nell'origine e non sono tracciati nell'altro

- `git fetch` updates with respect to the origin but only the origin branch, not the HEAD of the cloned branch

- The changes of the branch in the cloned should be  merged!

- when I have `++` and` --` is telling me how much lines are changed!

- posso farli assieme

- `git pull` is equivalent to `git fetch` followed by `git merge`

- to force a `pull` type

    ```bash
    git fetch origin branch_name
    git reset --hard origin/branch_name
    ```

- `git branch --track greet origin/greet` per creare un branch che traccia quello originale, quindi equivale a creare un branch e poi pullare su quel branch

- `bare` repositories are usually used for sharing. le `bare` sono quelle che er convenzione terminano con `.git` e non c'è nulla di lavoro ma solo le info per il branch e per copiare. sostanzialmente è la cartella `.git` di una non bare repo

- adding a remote repository>

	```bash
  cd working-origin  
  git remote add shared ../hello.git
	```

- cosa fa l'opzione `shared` perché io non l'ho capito. ok è il nome della repo verso cui spingiamo che abbiamo aggiunto a remote

- `git push shared master` sembra che io lo stia spingendo verso la cartella shared che serve per condividere e non verso l'origin

- quindi le cartelle shared vanno aggiunte a tutti quelli che vogliamo sincronizzare

#### git_tutorial 50&51

- `git daemon` che fa?

- ```bash
    git daemon --verbose --export-all --base-path=.
  ```


- per ricevere in risposta `--enable=receive-pack` ma fai attenzione che non c'è autenticazione del server e chiunque può pushare
- queste cose si possono fare anche con IP  generici per scambiare cose

## Other things to learn but later on

- Reverting Committed Changes
- Cross OS Line Endings -> `git-eol.md`
- Remote Servers
- Protocols
- SSH Setup
- Remote Branch Management
- Finding Buggy Commits (git bisect)
- Workflows
- Non-command line tools (gitx, gitk, magit)
- Working with GitHub
- `git diff` tells the difference between different elements or even commits, `git dff --staged` works differently: with `--staged` tells the difference between what it has been added to the *stage*, whilst without `--staged` tells the difference with what hasn't been added yet to the *stage*.

### **Quick setup** — if you’ve done this kind of thing before

```bash
https://github.com/lucafd/bootable-media.git
git@github.com:lucafd/bootable-media.git
```

Get started by  [creating a new file](https://github.com/lucafd/bootable-media/new/main) or [uploading an existing file](https://github.com/lucafd/bootable-media/upload). We recommend every repository include a [README](https://github.com/lucafd/bootable-media/new/main?readme=1), [LICENSE](https://github.com/lucafd/bootable-media/new/main?filename=LICENSE.md), and [.gitignore](https://github.com/lucafd/bootable-media/new/main?filename=.gitignore).

### …or create a new repository on the command line

```
echo "# bootable-media" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/lucafd/bootable-media.git
git push -u origin main
```

### …or push an existing repository from the command line

```
git remote add origin https://github.com/lucafd/bootable-media.git
git branch -M main
git push -u origin main
```

### …or import code from another repository

You can initialize this repository with code from a Subversion, Mercurial, or TFS project.

## GitKatas

The other tutorial that I have to take.

---

Sometimes, it marks as changed files only because `filemode` or `chmod` are changed, thus you can make it ignore it by configuring git through:

```bash
git config core.fileMode false
```



## Remote change of directory

Verify url:

```
 git remote -v        # View existing remote repository
# origin  https://github.com/demo/samplerepo.git (fetch)
# origin  https://github.com/demo/samplerepo.git (push)
```

 Now replace with the new URL

```
$ git remote set-url origin https://github.com/demo/samplerepo1.git
# Change the 'origin' remote's URL
```

Validate the new URL or Path

```
$ git remote -v
# Verify new remote URL
# origin https://github.com/demo/samplerepo1.git (fetch)
# origin https://github.com/demo/samplerepo1.git (push)
```

# Difference between `checkout -- .` and `reset HEAD --hard ` 

First, let's just address the double hyphen or double dash, to get it out of the way (especially since this question no longer has a marked duplicate).

Git mostly uses this in [the POSIX-approved fashion (see Guideline 10)](http://pubs.opengroup.org/onlinepubs/009696899/basedefs/xbd_chap12.html), to indicate a dividing line between option arguments and non-option arguments.  Since `git checkout` accepts branch names, as in `git checkout master`, and also file (path) names, as in `git checkout README.txt`, you can use the `--` to force Git to interpret whatever comes after the `--` as a file name, even if it would otherwise be a valid branch name.  That is, if you have both a *branch* and a *file* named `master`:

    git checkout master

will check out the *branch*, but:

    git checkout -- master

will check out the *file* (confusingly, from the current *index*).

### [Branches, index, and files, oh my](http://ask.metafilter.com/15238/Where-does-the-phrase-X-Y-Z-Oh-my-come-from)

Next, we need to address a quirk of `git checkout`.  As one can see from [the documentation](https://www.kernel.org/pub/software/scm/git/docs/git-checkout.html), there are many "modes" of `git checkout` (the documentation lists six separate invocations in the synposis!).  There are various rants (of varying quality: [Steve Bennet's](https://stevebennett.me/2012/02/24/10-things-i-hate-about-git/) is actually useful, in my opinion, though naturally I do not agree with it 100% :-) ) about Git's poor "user experience" model, including the fact that `git checkout` has too many modes of operation.

In particular, you can `git checkout` a *branch* (to switch branches), or `git checkout` one or more *files*.  The latter extracts the files from a particular commit, or from the index.  When Git extracts files from a commit, it first copies them *to* the index, and then copies them *from* the index, *to* the work-tree.

There is an underlying implementation reason for this sequence, but the fact that it shows through at all is a key element.  We need to know a lot about Git's index, because both `git checkout` and `git reset` use it, and sometimes in different ways.

It's a good idea, I think, to draw a three-way diagram or table illustrating the current—or `HEAD`—commit, the index, and the work-tree.  Suppose that:

 * there are two ordinary, committed files `README.md` and `file.txt`;
 * there is a new, `git add`-ed but uncommitted `new.txt`;
 * there is a file named `rmd.txt` that has been `git rm`-ed but not committed;
 * and there is an untracked file named `untr.txt`.

Each entity—the `HEAD` commit, the index, and the work-tree—holds three files right now, but each holds a *different set* of files.  The table of the entire state then looks like this:

      HEAD       index    work-tree
    -------------------------------
    README.md  README.md  README.md
    file.txt   file.txt   file.txt
               new.txt    new.txt
    rmd.txt
                          untr.txt

There are many more possible states than just these: in fact, for each file-name, there are *seven* possible combinations of "in/not-in" HEAD, index, and work-tree (the eighth combination is "not in all three", in which case, what file are we even talking about in the first place?!).

### The `checkout` and `reset` commands

The two commands you're asking about, `git checkout` and `git reset`, are both able to do many things.  The specific invocations of each, however, reduce the "things done" to one of two, to which I will add several more:

 * `git checkout -- .`: copies *from* index, *to* work-tree, only
 * `git checkout HEAD -- .`: copies *from* HEAD, *to* index, and then *to* work-tree
 * `git reset --mixed`: resets index from HEAD (and then leaves work-tree alone)
 * `git reset --hard`: resets index from HEAD, then resets work-tree from index

These overlap a lot, but there are several crucially-different parts.

Let's consider the file named `new.txt` above in particular.  It's in the index right now, so if we copy *from* the index, *to* the work-tree, we replace the work-tree copy with the index copy.  This is what `git checkout -- new.txt` does, for instance.

If, instead, we start by copying from `HEAD` to the index, nothing happens to `new.txt` in the index: `new.txt` doesn't *exist* in `HEAD`.  Hence an explicit `git checkout HEAD -- new.txt` just fails, while a `git checkout HEAD -- .` copies the files that are in `HEAD` and leaves the two existing `new.txt` versions undisturbed.

The file `rmd.txt` is *gone* from the index, so if we `git checkout -- .`, Git does not see it and does nothing about it.  But if we `git checkout HEAD -- .`, Git copies `rmd.txt` from `HEAD` into the index (now it's back) and then from the index to the work-tree (and now it's back there, too).

The `git reset` command has a key difference when used with no path name arguments.  Here, it literally re-sets the index to match the commit.  That means that for `new.txt`, it notices that the file is not in `HEAD`, so it *removes* the index entry.  If used with `--hard`, it therefore also *removes* the work-tree entry.  Meanwhile `rmd.txt` *is* in `HEAD`, so it copies that back to the index, and with `--hard`, to the work-tree as well.

If there are unstaged, i.e., work-tree only, changes to the other two files `README.md` and `file.txt`, both forms of `git checkout` and the `--hard` form of `git reset` wipe out those changes.

If there are *staged* changes to those files—changes that have been copied into the index—then `git reset` un-stages them.  So does the variant of `git checkout` where you give it the name `HEAD`.  However, the variant of `git checkout` where you copy the index files back to the work-tree keeps those staged changes staged!

### Top level vs current directory

Last, it's worth noting that `.`, meaning *the current directory*, may at any time be different from "top of Git repository":

    $ git rev-parse --show-toplevel
    /home/torek/src/kernel.org/git
    $ pwd
    /home/torek/src/kernel.org/git/Documentation
    $ git rev-parse --show-cdup
    ../

Here, I am in the `Documentation` sub-directory of the top level directory `git`, so `.` means *everything in `Documentation` and its subdirectories*.  Using `git checkout -- .` will check out (from the index) all the `Documentation` and `Documentation/RelNotes` files, but not any of the `../builtin` files, for instance.  But `git reset`, when used without path names, will reset *all* entries, including those for `..` and `../builtin`.

---

# [git-clean](https://git-scm.com/docs/git-clean)

Remove untracked files from the working tree. Synopsis:

```bash
 git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] <path>…
```

### Description

Cleans the working tree by recursively removing files that are not under version control, **starting from the current directory**.

Normally, only files unknown to Git are removed, but if the `-x` option is specified, ignored files are also removed. This can, for example, be useful to remove all build products.

If any optional `<path>...` arguments are given, only those paths are affected.

---

Step 1 is to show what will be deleted by using the `-n` option:
     

    # Print out the list of files and directories which will be removed (dry run)
    git clean -n -d

Clean Step - **beware: this will delete files**:
    

    # Delete the files from the repository
    git clean -f

 - To remove directories, run `git clean -f -d` or `git clean -fd`
 - To remove ignored files, run `git clean -f -X` or `git clean -fX`
 - To remove ignored and non-ignored files, run `git clean -f -x` or `git clean -fx`

**Note** the case difference on the `X` for the two latter commands.

If `clean.requireForce` is set to "true" (the default) in your configuration, one needs to specify `-f` otherwise nothing will actually happen.

Again see the [`git-clean`][1] docs for more information.

---

### Options

**`-f`, `--force`**  

If the Git configuration variable `clean.requireForce` is not set to
false, git clean will refuse to run unless given `-f`, `-n` or `-i`.

**`-x`**

Don’t use the standard ignore rules read from ``.gitignore` (per
directory) and `$GIT_DIR/info/exclude`, but do still use the ignore
rules given with `-e` options. This allows removing all untracked files,
including build products. This can be used (possibly in conjunction
with git reset) to create a pristine working directory to test a clean
build.

**`-X`**

Remove only files ignored by Git. This may be useful to rebuild
everything from scratch, but keep manually created files.

**`-n`, `--dry-run`**

Don’t actually remove anything, just show what would be done.

**`-d`**

Remove untracked directories in addition to untracked files. If an
untracked directory is managed by a different Git repository, it is
not removed by default. Use `-f` option twice if you really want to
remove such a directory.

[1]: http://git-scm.com/docs/git-clean	""git clean documentation""

---

# Line Endings (CR/LR/CRLR)

 Saturday. March 07, 2020 -  6 mins  

 [engineering](https://kuantingchen04.github.io/tags/#engineering) [git](https://kuantingchen04.github.io/tags/#git) 

If you are developing softwares on cross-platform projects (e.g.  Windows/Linux/MacOS), you will find that the line endings is sometimes  pretty annoying, especially when reading files.

## Outline

1. Line Endings Format
   - Control Characters: Carriage Return (CR), Line Feed (LR)
2. [Look-Up, Convert Text File’s Terminators](https://kuantingchen04.github.io/line-endings/#ii-look-up--change-texts-terminators)
3. For Cross-Platform Projects: Auto-Correct Line Ending Format (Git)
   - [Sol 1: Git Configuration](https://kuantingchen04.github.io/line-endings/#solution-1-git-configuration)
   - [Sol 2: Setup .gitattributes](https://kuantingchen04.github.io/line-endings/#solution-2-gitattribute)
4. [For Cross-Platform Projects: Ignore File Mode](https://kuantingchen04.github.io/line-endings/#iv-ignore-file-mode)

------

## I. Line Ending Formats

There are mainly two kinds of control characters for line endings, **Carriage Return** (CR, the code is \r) and **Line Feed** (LF, the code is \n).

On different OS, different line ending is used.

- OSX, Linux: **LF (\n)**

- Legacy MacOS (MacOS 9 and earlier): **CR (\r)**

- Windows: 

  CR LR pair (\r\n)

  - Carriage return points the cursor to the beginning of the line horizontly and  Line feed shifts the cursor to the next line vertically. Combination of  both gives you new line(\n) effect.

You can find more details on [Wiki](https://en.wikipedia.org/wiki/Newline#Representation).

------

## II. Look Up / Change Text’s Terminators

If you download a file to your system from a different OS. You might  notice that some weird behaviors occurs while processing the strings.  Probably it is a result of inconsistency between text and OS.

### Ubuntu Users

For Ubuntu users, you can simply use `file` command to see the files line ending format.

```
foo@bar:~$ file testfile1.txt
testfile.txt: ASCII text

foo@bar:~$ file testfile2.txt
testfile2.txt: ASCII text, with CRLF line terminators
```

To convert from DOS/Windows to Unix:

```
foo@bar:~$ dos2unix testfile2.txt
```

To convert from Unix to DOS/Windows:

```
foo@bar:~$ unix2dos testfile1.txt
```

### Editor Users (Take JetBrains for Example)

Lots of editors/IDE allow user to set up line separators (line endings) for  newly created files, and change line separator style for existing files.

![lineseperators_image](https://resources.jetbrains.com/help/img/idea/2019.3/cl_lineseparators_settings.png)

CLion Settings



------

## III. Auto-Correct Git’s Text Line Ending

If you are working on **cross-platform projects**, the subtle difference above could be incredibly annoying; many editors  on Windows silently replace existing LF-style line endings with CRLF, or insert both line-ending characters when the user hits the enter key.

In order to gaurantee that the code fits your OS system, there are two  common ways to set things up so git will git to auto-correct line ending formats.

### Solution 1: Git Configuration

Git can handle this by auto-converting CRLF line endings into LF when you  add a file to the index, and vice versa when it checks out code onto  your filesystem. That is, to change **core.autocrlf**. (You could add —-global to set all repos)

There are three values for this variable: **true**, **input**, **false**.

![test](https://kuantingchen04.github.io/assets/images/2020-02-21-autocrlf.png)

Commit-Checkout Cycle



```
git config core.autocrlf true
```

- Set **core.autocrlf=true**: Git will auto-convert CRLF line endings into LF when you add a file to  the index; Git will convert LF to CRLF when checking out code. (For  cross-platform projects, this is the recommended setting on Windows)

```
git config core.autocrlf input
```

- Set **core.autocrlf=input**: When committing text files, CRLF will be converted to LF. Git will not  perform any conversion when checking out text files. (For cross-platform projects this is the recommended setting on Unix, but don’t use input  under windows)

```
git config core.autocrlf false
```

- Set **core.autocrlf=false**: Git will not perform any conversions when checking out or committing  text files. (Choosing this option is not recommended for cross-platform  projects)

### Solution 2: .gitattribute

It is a good idea to keep a .gitattributes file as we don’t want to expect everyone in our team set their config. This file should keep in repo’s  root path and if exist one, git will respect it.

```
text=auto  #Convert to OS’s line ending
```

- This will treat all files as text files and convert to OS’s line ending on checkout and back to LF on commit automatically.

```
* text eol=crlf
* text eol=lf
```

- You can also tell it explicitly

## IV. Ignore File Mode

After you clone a repo, you may find that even if we set up `core.autocrlf` as we described above, it is still saying that files have been  modified. The reason is that the file permissions may not be supported.  (Linux has more complete access rights *-rwxrwxrwx* than Windows) You could try and set `core.fileMode` to **false**.

```bash
git config core.fileMode false
```

*If you set core.fileMode to false, make sure that executable’s and script’s permission is well handle.*

As https://stackoverflow.com/a/1580644 suggested, `core.fileMode` is not the best practice and should be used carefully. This setting  only covers the executable bit of mode and never the read/write bits. In many cases you think you need this setting because you did something  like `chmod -R 777`, making all your files executable. But in most projects **most files don’t need and should not be executable for security reasons**.

The proper way to solve this kind of situation is to handle folder and file permission separately, with something like:

```
find . -type d -exec chmod a+rwx {} \; # Make folders traversable and read/write
find . -type f -exec chmod a+rw {} \;  # Make files read/write
core.fileMode
```
Tells Git if the executable bit of files in the working tree is to be honored.
Some filesystems lose the executable bit when a file that is marked as executable is checked out, or checks out an non-executable file with executable bit on. [git-clone(1)](https://www.kernel.org/pub/software/scm/git/docs/git-clone.html) or [git-init(1)](https://www.kernel.org/pub/software/scm/git/docs/git-init.html) probe the filesystem to seee if it handles the executable bit correctly and this variabl is automatically set as necessary. A repository, however, may be on a filesystem that handles the filemode correctly, and this variable is set to *true* when created, but later may be made accessible from another environment that loses the filemode (e.g. exporting ext4 via CIFS mount, visiting a Cygwin created repository with Git for Windows or Eclipse). In such a case it may be necessary to set this variable to *false*. See [git-update-index(1)](https://www.kernel.org/pub/software/scm/git/docs/git-update-index.html). The default is true (when core.filemode is not specified in the config file).

## Reference

##### Line Endings

- https://en.wikipedia.org/wiki/Carriage_return#Computers
- https://stackoverflow.com/a/3570574
- https://www.jetbrains.com/help/clion/configuring-line-endings-and-line-separators.html
- https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration
- https://stackoverflow.com/a/20653073

##### File Mode

- https://www.jianshu.com/p/3b0a9904daca
- https://stackoverflow.com/a/1580644
- http://linuxcommand.org/lc3_lts0090.php

#### Related Posts

-  [Vim and Useful Plugins ](https://kuantingchen04.github.io/vim-plugins/) 