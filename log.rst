Logování
========

Práce se pracovním záznamem (logem) z gitu je trochu magie. Na štěstí existuje
několik základních parametrů a pomůcek pro jednodušší orientaci, na zbytek je
Google.

Záznam práce ukáže `git log`::

    $ git log
    commit 1a9908487f5eebbeaad253e835cabb33ca18a8cd
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Mon Sep 19 16:37:50 2016 +0200
    
        Doplnění sekce práce s gitem
    
    commit bc12c5de2f90ae8832743f5ee8584640b3a59b65
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Thu Sep 15 14:17:38 2016 +0200
    
        last note
    
    commit 6574bcfd6f1e5b12c57760ed78b545154d666c54
    Merge: 7c75607 83221c8
    Author: Jachym Cepicky <jachym@users.noreply.github.com>
    Date:   Fri Sep 16 14:35:05 2016 +0200
    
        Merge pull request #1 from madlenkk/master
        
        Opravy překlepů
    
    commit 83221c8504b9c406057bffcd793d36c7eed5ad93
    Author: Magdalena Kabatova <magdalena.kabatova@gmail.com>
    Date:   Fri Sep 16 14:29:54 2016 +0200
    
        Opravy překlepů
    
    commit 7c75607f8faef75ceef6e8349359d66c425e0f02
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Wed Sep 7 16:25:24 2016 +0200
    
        neco o gitu
    
    commit c9aa4cf1ca1f626ae0566e7eaaa59c714a5e17e6
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Tue Sep 6 09:56:01 2016 +0200
    
        pridavam README
    
    commit a7440f4c16ce5473adcecf3c3595b876d997a039
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Tue Sep 6 09:51:22 2016 +0200
    
        initial commit

Ukáže všechny commity v dané větvi, jak šel čas "nekonečně" hluboko do historie.
Tento výpis není nejpřehlednější a lze ho různě podifikovat. Lze mimo jiné
speficikovat určité časové obdoví - to může být definováno časem nebo rozsahem
identifikátorů, např.  poslední 2 revize::

    $ git log -2
    commit 1a9908487f5eebbeaad253e835cabb33ca18a8cd
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Mon Sep 19 16:37:50 2016 +0200
    
        Doplnění sekce práce s gitem
    
    commit bc12c5de2f90ae8832743f5ee8584640b3a59b65
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Thu Sep 15 14:17:38 2016 +0200
    
        last note

ohraničení 2mi revizemi::

    $ git log c9aa4cf1ca1f626ae05..83221c8504b9c40
    commit 83221c8504b9c406057bffcd793d36c7eed5ad93
    Author: Magdalena Kabatova <magdalena.kabatova@gmail.com>
    Date:   Fri Sep 16 14:29:54 2016 +0200

        Opravy překlepů

    commit 7c75607f8faef75ceef6e8349359d66c425e0f02
    Author: Jachym Cepicky <jachym.......@mail.com>
    Date:   Wed Sep 7 16:25:24 2016 +0200
    
        neco o gitu

Copak zatím dělala `Magdalena`::
    
        $ git log --author Magdalena
        commit 83221c8504b9c406057bffcd793d36c7eed5ad93
        Author: Magdalena Kabatova <magdalena.......@mail.com>
        Date:   Fri Sep 16 14:29:54 2016 +0200

            Opravy překlepů

Lze trochu zpřehlednit výstup::

    $ git log --oneline --decorate --all --graph
    
    * 1a99084 (HEAD -> master) Doplnění sekce práce s gitem
    * bc12c5d last note
    *   6574bcf (origin/master) Merge pull request #1 from madlenkk/master
    |\  
    | * 83221c8 Opravy překlepů
    |/  
    * 7c75607 neco o gitu
    * c9aa4cf pridavam README
    * a7440f4 initial commit

Poslední příkaz používám jako tzv. `alias` - zkratku - kterou spouštím pomocí
`git tree`. Ukazuje mi postup prací, kde jsem já (`HEAD`), kde je server
(většinou `origin`), jak spolu souvisí různé větve a podobně. Alias můžete
přidat do konfiguračního souboru gitu uloženého někde jako `$HOME/.gitconfig`
nebo prostě příkazem `git config`::

    $ git config --global alias.tree 'log --oneline --decorate --all --graph'

    $ git tree

TIG
===

Pro příkazovou řádku existuje i příkaz `tig`, který dává také celekem přehledný
výstup::

        2016-09-19 20:19 Jachym Cepicky     o [master] {origin/master} dalsi tipy
        2016-09-19 20:16 Jachym Cepicky     o doplneni cheatsheetu
        2016-09-19 20:00 Jachym Cepicky     o remote
        2016-09-19 18:28 Jachym Cepicky     M─┐ Merge branch 'pokusna_vetev'
        2016-09-19 17:51 Jachym Cepicky     │ o [pokusna_vetev] commit do jine vetve
        2016-09-19 17:54 Jachym Cepicky     o │ vyroba konfliktniho řádečku
        2016-09-19 17:43 Jachym Cepicky     o─┘ pokracovani dokumentace
        2016-09-19 16:37 Jachym Cepicky     o Doplnění sekce práce s gitem
        2016-09-15 14:17 Jachym Cepicky     o last note
        2016-09-16 14:35 Jachym Cepicky     M─┐ Merge pull request #1 from madlenkk/master
        2016-09-16 14:29 Magdalena Kabatova │ o {madlenkk/master} Opravy překlepů
        2016-09-07 16:25 Jachym Cepicky     o─┘ neco o gitu
        2016-09-06 09:56 Jachym Cepicky     o pridavam README
        2016-09-06 09:51 Jachym Cepicky     I initial commit
