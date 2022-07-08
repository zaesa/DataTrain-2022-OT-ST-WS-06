# DataTrain | OT-ST-WS-06 | Git / GitHub

## 0. Preparation

Before attending the course, follow the steps in the [Setup guide](documentation/00-setup-your-environment.md).

## 1. Onboarding 

Before we start. Lets check your [check your configuration](excercises/01.md) first.

## 2. Why using a version control system

### 2.1 Iterations of working documents

When I worked on a document, I started with a file, let's call it `document.txt`.
As the work progressed, for example when updating the layout, I didn't want to lose anything and renamed the file to `document-v2.txt`.
Now the madness begins. I send this file to a friend to review it. They send me their feedback, and I work it into a file called `document-v2-final_draft.txt`. I send this to another friend and collect their feedback in `document-v2-final_draft2.txt`. 
Finally, I finish the document and name it `document-final.txt`. Before I print or publish it, I ask my dear mother to review it, and you may have guessed it, she sends me back the file `document-final-fixed.txt`. I look at the changes and find a few more problems, so I have this file `document-FINAL-FINAL.txt`.

At this point, my project folder will look something like this:

```bash
my-project
├── document.txt
├── document-v2.txt
├── document-v2-final_draft.txt
├── document-v2-final_draft2.txt
├── document-final.txt
├── document-final-fixed.txt
└── document-FINAL-FINAL.txt
```

Even worse, these files can be active at the same time, as I may be making changes to the `document-final.txt` file while someone else is correcting the same file I sent them.

```mermaid
gantt
    dateFormat YYYY-MM-DD
    
    section Document
    document.txt : done, doc1, 2022-06-10, 2022-06-14
    document-v2.txt : done, doc2, 2022-06-14, 2022-06-17
    document-v2-final-draft.txt : done, doc3, 2022-06-17, 2022-06-18
    document-v2-final-draft.txt : done, doc4, 2022-06-18, 2022-06-20
    document-final.txt : active, doc5, 2022-06-20, 2022-06-26
    document-final-fixed.txt : active, doc5, 2022-06-24, 2022-06-27
    document-FINAL-FINAL.txt : active, doc5, 2022-06-27, 2022-06-28
```

Now imagine what this might look like for projects with multiple files, such as source code or larger projects like books, papers, and so on.

In the early era of software development in the 1960s and 1970s, the need arose for a system to manage these changes in a logical way. The first [Source Code Control System](https://en.wikipedia.org/wiki/Source_Code_Control_System) was developed in 1972. Later, other version control systems were developed. The most commonly used system is the one we are talking about today.

### 2.2 A version control system?

With books, there are different editions. When the content is updated, the edition is increased. This has been done for hundreds of years. Most books are written by a single person, and when they are edited in collaboration, people tend to divide the chapters. Working on a book in the traditional way and in collaboration with other people is very labor intensive.
The work of software engineers in the 1960s was spread across mainframes and thousands of lines of code, which are not as easy to read as prose. Mistaking a lowercase L for a capital i isn't wild in novels, but in the software world it quickly leads to bugs.

That's why VCS were developed. But what should they be able to do anyway?

- Track changes across multiple files
- Compare different versions
- Restore a previous state
- Collaborate with other people

The first VCS was just the beginning, others were developed after to meet changing needs.

- [RCS](https://www.gnu.org/software/rcs/) (1982)
- [CVS](http://cvs.nongnu.org/) (1990)
- [SVN](https://subversion.apache.org/) (2000)
- [Mercurial](https://www.mercurial-scm.org/) (2005)
- [Git](https://git-scm.com/) (2005)

### 2.3 What is git?

> Git is a free and open source distributed version 
> control system designed to handle everything from 
> small to very large projects with speed and efficiency.
> 
> [git-scm.com](https://git-scm.com/)

After some controversy, Linus Torvalds was looking for a version control system to use for the development of the Linux kernel.
Unable to find a solution that met his requirements, he began developing git in 2005.
Due to the high status of the Linux kernel in the developer community, git became popular quite quickly.

Every year, [StackOverflow](https://stackoverflow.com/) collects answers from its users. One question they ask is about VCS. 

For years, the use of Git has been on the rise. Ten years after its initial release, Git was already used by 69.3% of StackOverflow survey respondents.
In the most recent 2022 survey, 93.87% of 71,379 people responded that they use Git as their preferred version control system.

![](images\so-s-vcs-use-2022.png)
[StackOverflow Survey 2022 - VCS](https://survey.stackoverflow.co/2022/#section-version-control-version-control-systems)

#### But what exactly is git?

Git is a command line tool with a large number of commands for controlling changes to your files. If you call the help information via `git --help` after installation, you will get an overview of the available commands.

```bash
$ git --help       
usage: git [--version] [--help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone     Clone a repository into a new directory
   init      Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add       Add file contents to the index
   mv        Move or rename a file, a directory, or a symlink
   restore   Restore working tree files
   rm        Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect    Use binary search to find the commit that introduced a bug
   diff      Show changes between commits, commit and working tree, etc
   grep      Print lines matching a pattern
   log       Show commit logs
   show      Show various types of objects
   status    Show the working tree status

grow, mark and tweak your common history
   branch    List, create, or delete branches
   commit    Record changes to the repository
   merge     Join two or more development histories together
   rebase    Reapply commits on top of another base tip
   reset     Reset current HEAD to the specified state
   switch    Switch branches
   tag       Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch     Download objects and refs from another repository
   pull      Fetch from and integrate with another repository or a local branch
   push      Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
See 'git help git' for an overview of the system.
```

Each of these commands has its own help section. Just append `--help` to a command and you will get a technical description of what that command does. Depending on your system, you will either get the information in your terminal or a browser window will open.
E.g. `git init --help` shows you a _DESCRIPTION_ of what this command does. You also have a list of _OPTIONS_ that you can append to `git init`.

Git is NOT GitHub or GitLab or any other service or software. Git can be used to work with those services, but it must not be confused with them.

### 2.4 Collaboration

Git, as it stands, can be used to collaborate with others. If you are working on a repository that you have obtained in some way, you can use commands like `git format-patch mybranch` to create a patch file that updates someone else's repository with your changes via the command `git am mychanges.patch`. But this is very cumbersome and some people thought this should be simplified. They developed software like GitHub, Gitlab, Bitbucket, Gitea. Some offer their software as open source and/or as a service.

These services and solutions offer features that go far beyond those of Git. From additional ticket systems, project management, wikis, reviews, communities to automation.

The most used platform, according to the StackOverflow survey, is GitHub, which we are talking about today.
More about using GitHub for collaboration is explained in later chapters.

![](images\so-s-vcs-platforms-2022.png)
[StackOverflow Survey 2022 - VCS Platforms](https://survey.stackoverflow.co/2022/#section-version-control-version-control-platforms)

