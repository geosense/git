***
GIT
***

GIT napsal původně Linus Torvalds pro správu zdrojových kódů linuxového jádra. Z
licenčních důvodů museli opustit projekt BitKeeper a ruční řešení revizí už
nepřicházelo vzhledem k množství změn v úvahu.

GIT je *decentralizovaný* což znamená, že není jeden hlavní repozitář, ke
kterému se ostatní "kopie" pouze odvolávají, ale každý *klon* je považován za
plnohodnotný repozitář. Všichni mají vždy k dispozici plnou kopii projektu
včetně historie - ale mohou mít i několik různých "plných kopií". Spráce
projektu obvykle sehrává z různých repozitářů změny do hlavního repozitáře a
rozhoduje o jejich pořadí a prioritách.

.. note:: **Jak to je v Cleerio:** Přes uvedené výše, u většiny projektů
        používáme *jeden centrální repozitář*, do kterého nahráváme postupně
        naše změny. Nepoužíváme vlastní kopie celého projektu a navzájem si
        neklonujeme různé veřejné klony projektu. Příklad: `jachym` vždycky bude
        stahovat změny z a posílat změny do repozitáře označeného jako *origin*
        na serveru `gitlab.geo/gp2-lib/`. Nidky si neudělá kopii od `pavel` nebo
        `chrudos`. Ale: jachym bude vždycky pracovat minimálně se dvěma klony
        projektu: s *origin* (tedy tím, co je na serveru) a *lokální kopií*.

        Intenzivně používáme možnost větvení a zpětné sehrávání - každý vývojář
        je odpovědný za kód, který posílá do hlavní větve. Kód je ale vyvíjen
        separátně ve větvích a do hlavní větve *masteru* jde až pod odlazení a
        když je jisté, ne nevzniknout konflikty.


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

