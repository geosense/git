***
GIT
***

GIT napsal původně Linus Torvalds pro správu zdrojových kódů linuxového jádra. Z
licenčních důvodů museli opustit projekt BitKeeper a ruční řešení revizí už
nepřicházelo vzhledem k množství změn v úvahu.

GIT je *decentralizovaný* což znamená, že není jeden hlavní repozitář, ke
kterému se ostatní "kopie" pouze odvolávají, ale každý *klon* je považován za
plnohodnotný repozitář. Všichni mají vždy k dispozici plnou kopii projektu
včetně historie - ale mohou mít i několik různých "plných kopií". Správce
projektu obvykle sehrává z různých repozitářů změny do hlavního repozitáře a
rozhoduje o jejich pořadí a prioritách.

.. note:: **Jak to je v Cleerio:** Přes uvedené výše, u většiny projektů
        používáme *jeden centrální repozitář*, do kterého nahráváme postupně
        naše změny. Nepoužíváme vlastní kopie celého projektu a navzájem si
        neklonujeme různé veřejné klony projektu. Příklad: `jachym` vždycky bude
        stahovat změny z a posílat změny do repozitáře označeného jako *origin*
        na serveru `gitlab.geo/gp2-lib/`. Nikdy si neudělá kopii od `pavel` nebo
        `chrudos`. Ale: jachym bude vždycky pracovat minimálně se dvěma klony
        projektu: s *origin* (tedy tím, co je na serveru) a s *lokální kopií*.

        Intenzivně používáme možnost větvení a zpětné sehrávání - každý vývojář
        je odpovědný za kód, který posílá do hlavní větve. Kód je ale vyvíjen
        separátně ve větvích a do hlavní větve *masteru* jde až po odladění a
        když je jisté, že nevzniknou konflikty.


Vytvoření prázdného lokálního repozitáře
========================================

.. note:: Předpokládáme, že máte nainstalován systém GIT do vašeho počítače.

Pro takové to domácí verzování stačí, když si v adresáři s vaším projektem
založíte repozitář.

.. code-block:: bash

    $ mkdir muj_projekt
    $ cd muj_projekt
    $ git init

Příkaz `git init` budete potřebovat po celou dobu životnosti projektu jenom
jednou - na jeho začátku. A pak ho zapomenete.

Když si nevíte rady, zkuste nápovědu

.. code-block:: bash

    $ git --help


A dostane se vám vyčerpávající odpovědi::

    usage: git [--version] [--help] [-C <path>] [-c name=value]
               [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
               [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
               [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
               <command> [<args>]
    
    These are common Git commands used in various situations:
    
    start a working area (see also: git help tutorial)
       clone      Clone a repository into a new directory
       init       Create an empty Git repository or reinitialize an existing one
    
    work on the current change (see also: git help everyday)
       add        Add file contents to the index
       mv         Move or rename a file, a directory, or a symlink
       reset      Reset current HEAD to the specified state
       rm         Remove files from the working tree and from the index
    
    examine the history and state (see also: git help revisions)
       bisect     Use binary search to find the commit that introduced a bug
       grep       Print lines matching a pattern
       log        Show commit logs
       show       Show various types of objects
       status     Show the working tree status
    
    grow, mark and tweak your common history
       branch     List, create, or delete branches
       checkout   Switch branches or restore working tree files
       commit     Record changes to the repository
       diff       Show changes between commits, commit and working tree, etc
       merge      Join two or more development histories together
       rebase     Forward-port local commits to the updated upstream head
       tag        Create, list, delete or verify a tag object signed with GPG
    
    collaborate (see also: git help workflows)
       fetch      Download objects and refs from another repository
       pull       Fetch from and integrate with another repository or a local branch
       push       Update remote refs along with associated objects
    
    'git help -a' and 'git help -g' list available subcommands and some
    concept guides. See 'git help <command>' or 'git help <concept>'
    to read about a specific subcommand or concept.

Co vlastně udělal příkaz `git init` ? Vytvořil lokální adresář `.git` s
kompletní historií projektu a nějakou tou konfigurací.

Stav vašeho aktuálního lokálního repozitáře získáte příkazem `git status` status
může vypadat různě, např. ::

        $ git status
        On branch master
        Your branch is ahead of 'origin/master' by 1 commit.
          (use "git push" to publish your local commits)
        nothing to commit, working directory clean

nebo (tyto soubory nejsou v repozitáři a můžu je přidat)::

    $ git status
        On branch prep
        Your branch is up-to-date with 'origin/prep'.
        Untracked files:
    (use "git add <file>..." to include in what will be committed)

	node_modules_ol3/
	package.json.orig
	src/gs/app/gp2.js.orig
	src/gs/layout/layout.js.orig
	src/gs/module/datagrid.js.orig
	src/gs/module/datagrid.js.rej
        ...
    
Status je dobré číst. Pokud změníme nějaký soubor, ukáže nám to status::

    $ git status
    On branch master
    Your branch is ahead of 'origin/master' by 1 commit.
      (use "git push" to publish your local commits)
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
      (use "git checkout -- <file>..." to discard changes in working directory)

            modified:   git.rst

    no changes added to commit (use "git add" and/or "git commit -a")
    
Změny mohu uložit do revize pomocí `git commit`. Mohu buď vyjmenovat soubor
který chci uložit nebo použít přepínač `-a`, který uloží změny ve všech
registrovaných souborech. Další užitečná volba je `-m`, která přidá komentář ke
commitu. Pokud nepoužiji volbu `-m`, spustí se textový editor podle nastavení
systému, do kterého je potřeba komentář zadat::

    $ git commit -a -m"Doplnění sekce práce s gitem"
    [master 1a99084] Doplnění sekce práce s gitem
    1 file changed, 48 insertions(+), 2 deletions(-) 

`git status` prozradí, že změny byly uloženy, ale že lokální kopie mého
repozitáře je od 2 commity napřed před verzí na serveru `origin`::

    $ git status
    On branch master
    Your branch is ahead of 'origin/master' by 2 commits.
      (use "git push" to publish your local commits)
    nothing to commit, working directory clean

Příkaz `git show` může ukázat, co bylo konkrétní změnou v poslední (nebo
libovolné) revizi (commitu)::

    $ git show
    commit 1a9908487f5eebbeaad253e835cabb33ca18a8cd
    Author: Jachym Cepicky <jachym.cepicky@gmail.com>
    Date:   Mon Sep 19 16:37:50 2016 +0200

        Doplnění sekce práce s gitem

    diff --git a/git.rst b/git.rst
    index 93cab2e..557bd32 100644
    --- a/git.rst
    +++ b/git.rst
    @@ -97,7 +97,53 @@ A dostane se vám vyčerpávající odpovědi::
         concept guides. See 'git help <command>' or 'git help <concept>'
         to read about a specific subcommand or concept.
     
    -Vytvoření prázdného lokálního repozitáře
    -========================================
     Co vlastně udělal příkaz `git init` ? Vytvořil lokální adresář `.git` s
     kompletní historií projektu a nějakou tou konfigurací.
    +
    +Stav vašeho aktuálního lokálního repozitáře získáte příkazem `git status` status
    +může vypadat různě, např. ::
    +

Každá revize má unikátní identifikátor, který mohu kdykoliv v budoucnu použít a
vrátit se k němu, často stačí pouze pár unikátních prvních znaků::

    $ git show 1a9908487f
    commit 1a9908487f5eebbeaad253e835cabb33ca18a8cd
    Author: Jachym Cepicky <jachym.cepicky@gmail.com>
    Date:   Mon Sep 19 16:37:50 2016 +0200
    
        Doplnění sekce práce s gitem
    
    diff --git a/git.rst b/git.rst
    index 93cab2e..557bd32 100644

Nový soubor a adresář můžeme přidat (registrovat) v repozitáři příkazem `git
add`::

    $ git add cheatsheet.rst
    $ git status

    On branch master
    Your branch is ahead of 'origin/master' by 2 commits.
      (use "git push" to publish your local commits)
    Changes to be committed:
      (use "git reset HEAD <file>..." to unstage)
    
    	    new file:   cheatsheet.rst

A to je vlastně celé workflow: Pracujete, děláte změny v souborech, ucelené
bloky změn ukládáte do repozitáře do samostatných revizí (`git commit`), nové
soubory registrujete v repozitáři jak přicházejí (pomocí `git add`). 


