Cheatsheet
==========

git init
    inicializace repozitáře

git clone
    vytvoření lokální kopie ze vzdáleného repozitáře

git commit
    Uložení lokálních změn do lokálního repozitáře

    **Asi nejdůležitější a nejčastěji používaný příkaz**

git branch
    Vytváření nové větve (správa větví)

git merge
    sloučení změn *z druhé větve do aktuální*

git checkout 
    Přepnutí se do jiné branche, na jiný commit, na jiný tag

git fetch
    Stažení změn ze serveru

git rebase
    Přeskládání aktuální práce nad nový základ (např. nad změny stažené před tím
    ze serveru pomocí `git fetch`)

git push
    poslání lokálních změn na vzdálený server

git pull
    alternativní stažení změn ze serveru spolu s `mergováním` konfliktů mezi
    lokální a vzdálenou větví

git remote
    správa vzdálených repozitářů

Typické workflow
================

Bez větví
---------

Klonování existujícího repozitáře::

    git clone https://github.com/geosense/git

Na začátku práce stáhnout aktuální verze ze vzdálených repozitářů a přeskládat
svoji případnou práci nad ně::

    git fetch --all
    git rebase

Následuje práce v textovém editoru, a mnoho a mnoho commitů::

    git commit -a -m"důležitá změna"
    git commit -m"jiná změna - ale jenom v jednom souboru" gui.rst

Po skončení směny - nebo v případě požáru::

    git push

A opusťte budovu

Když se chci podívat, co se změnilo, kde jsem::

    git status

    git tree

když pracuji s větvemi
----------------------

vyrobím a přepnu se do větve::

    git branch jmeno_vetve
    git checkout jmeno_vetve

Dál pracuji normálně::

    git commit
    git commit
    ... 

    git push
    git fetch --all
    git rebase

    git commit
    git commit
    git commit
    ...

Sem tam použiji `git tree` a `git status` (nebo holt `gitk`, no...)

Když chci sloučit změny *do cílové větve `master`*::

    git checkout master
    git merge jmeno_vetve
    git push
