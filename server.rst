Vzdálené repozitáře
===================

Vzdálený repozitář si opatříme příkazem `clone`::

    $ git clone https://github.com/geosense/git.git

Nebo v existujícím repozitáři si ho můžeme přidat příkazem `remote`::

    $ git remote add madlenkk https://github.com/madlenkk/git.git

Protože kolegové nikdy nespí, je potřeba často a pravidelně stahovat změny z
repozitáře. Jako nejlepší praktika se nám osvědčil systém `git fetch - git
rebase`.

.. note:: Často se v návodech objevuje postup `git pull --rebase`, ten má ale tu
    nevýhodu, že v jednom kroku musíte řešit případné konflikty mezi verzí na
    server a verzí ve vašem lokálním repozitáři. `git fetch` vám pouze stáhne
    změny ze serveru, ale nechá vas pracovat tam "kde zrovna jste". `git rebase`
    vám pak pomůže při "posunu nad" aktuální konec větve ze serveru.

Stánutí všech revizí ze všech serverů::

    $ git fetch --all
    Fetching origin
    Fetching madlenkk
    From https://github.com/madlenkk/git
     * [new branch]      master     -> madlenkk/master

`git tree` ukáže, kde jsem::

    $ git tree

    *   6ebd5ea (HEAD -> master) Merge branch 'pokusna_vetev'
    |\  
    | * 2e03719 (pokusna_vetev) commit do jine vetve
    * | 096304c vyroba konfliktniho řádečku
    |/  
    * b89a5c0 pokracovani dokumentace
    * 1a99084 Doplnění sekce práce s gitem
    * bc12c5d last note
    *   6574bcf (origin/master) Merge pull request #1 from madlenkk/master
    |\  
    | * 83221c8 (madlenkk/master) Opravy překlepů
    |/  
    * 7c75607 neco o gitu
    * c9aa4cf pridavam README
    * a7440f4 initial commit

Vidíte, že magdalenina větev `master` je o revizi za serverem `origin` a ten je
zase o nutný kus historie za mou lokální větví.

push a pull (vlastně fetch)
---------------------------
Pro práci se vzdálenými serveri slouží dva základní příkazy `git push` a `git
pull`. Nám se ale osvědčilo používat místo `pull` kombinaci `fetch` a `rebase`.

Rozdíl mezi `fetch` a `pull` je, že *`git pull` udělá v jednom kroce `git fetch`
následovaný `git merge`*. `pull` vás dounutí okamžitě řešit konflikty mezi
lokální a vzdálenou větví. 

`git fetch` vám dovolí pouze stáhnout nové revize ze vzdáleného serveru. `git
rebase` vám umožní se se svými lokálními commity *posunout nad* revize stažené
ze serveru.

Pokud chci poslat změny na vzdálený server, je to už jednoduché, použiji `git
push`.

Takže nejpre stáhneme změny ze vech vzdálených repozitářů::

    $ git fetch --all

Podíváme se, kde je kdo, kde je jaká větev::

    $ git tree

    *   6ebd5ea (HEAD -> master) Merge branch 'pokusna_vetev'
    |\  
    | * 2e03719 (pokusna_vetev) commit do jine vetve
    * | 096304c vyroba konfliktniho řádečku
    |/  
    * b89a5c0 pokracovani dokumentace
    * 1a99084 Doplnění sekce práce s gitem
    * bc12c5d last note
    *   6574bcf (origin/master) Merge pull request #1 from madlenkk/master
    |\  
    | * 83221c8 (madlenkk/master) Opravy překlepů
    |/  
    * 7c75607 neco o gitu

Vidíme, že jsme daleko před verzí v repozitáři `origin` in `madlankk`. Konflikty
nevidět, mohu vesele poslat svoje lokální revize na server `origin`::

    $ git push origin
    Username for 'https://github.com': jachym
    Password for 'https://jachym@github.com': 
    Counting objects: 25, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (25/25), done.
    Writing objects: 100% (25/25), 120.36 KiB | 0 bytes/s, done.
    Total 25 (delta 14), reused 0 (delta 0)
    remote: Resolving deltas: 100% (14/14), completed with 3 local objects.
    To https://github.com/geosense/git.git
       6574bcf..6ebd5ea  master -> master
    jachym@krovak:~/.../cleerio/skoleni/git (master)$

A zkontrolovat, jak se věci mají pomocí `git tree`::

    $ git tree
    *   6ebd5ea (HEAD -> master, origin/master) Merge branch 'pokusna_vetev'
    ...

Vidíte, že větve `master` a `origin/master` jsou již v souladu.

Nyní přijde ale do práce `madlenkka` a co nevidí - origin jí "ujel" o pěkných
pár commitů. Co jí zbývá, než stáhnout změny ze serveru::

    $ git fetch --all

Posunout svoji aktuální práci *nad* verzi na serveru::

    $ git rebase origin/master

  

