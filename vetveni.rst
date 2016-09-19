Větvení
=======

Tohle si necháme na praktickou ukázku, protože se to s ní pochopí líp. Větvení
vám umožní "jakoby" vytvářet kopie adresáře současné práce do zálohy, něco
vyzkoušet, pak se vrátit k předchozí verzi, začít jinak, zkusit to na jiné větvy
zas jinak atp.

Další možný scénář je, že dva lidé pracují na různých věcech, každý ve své
větvi, navzájem si "nelezou do souborů", a nakonci se jejich práce sehraje
dohromady.

GIT by vás měl povzbuzovat v tom, abyste vytvářeli *co nejvíce větví*. V rámci
Cleerio vývojáři vytváří samostatnou větev na každý "ticket" v Redmine. Teprve
když je větev schválena, dává se do hlavní větve, která se jmenuje `master`.

Pro práci s větvemi slouží `git branch` a umí toho hodně.

Seznam dostupných větví - na serverech i lokálních::

    $ git branch -la

    * master
    remotes/origin/master

Tento výpis znamená:

* na serverech mohou být jiné větve, než u vás na lokále. 
* můžete mít různě pojmenované větve u sebe a na serveru - a přesto budou
  korespondovat

Jak to vypadá na frontendu naší aplikace::

    $ git branch -la
    ...
    remove
    setOptions_refactoring
    sprint-03
    templates
    tmp
    tmp2
    remotes/origin/1397_maxExtent
    remotes/origin/1612_neighbours
    remotes/origin/2422_faster_vectors
    remotes/origin/2478_rotateButton
    remotes/origin/3476_renameCallbackListen
    remotes/origin/3971_jsdoc
    remotes/origin/4433_iefixes
    remotes/origin/4537_partialLV
    ...

Jak to vypadá v PyWPS::

    ...
      help
    * master
      pygrass
      pywps-3.2
      pywps-3.2.3
      pywps-4
      web
      ...
      remotes/jachym/1.0
      remotes/jachym/1.0@1
      remotes/jachym/109_close_stream
      remotes/jachym/122_documentation
      ...
      remotes/jan-rudolf/1.0
      remotes/jan-rudolf/1.0@1
      remotes/jan-rudolf/flask
      remotes/jan-rudolf/gh-pages
      remotes/jan-rudolf/master
      ...
      remotes/origin/1.0
      remotes/origin/1.0@1
      remotes/origin/151_dblog2
      remotes/origin/HEAD -> origin/master
      remotes/origin/flask
      remotes/origin/master


Jsou vidět tři registrované vzdálené servery: `origin`, `jachym` a `jan-rudolf`,
každý s hromadou větví.

GIT umí udržet pořádek v tom, jaká větev na lokále odpovídá jaké větvi na
serveru. Větev můžete smazat z lokálu - ale na serveru zůstane. Můžete ji smazat
i ze serveru. Můžete ji na lokále přejmenovat - ale na serveru zůstane stejná.

Založení nové větve je celkem primocare::

    $ git branch pokusna_vetev

Ověříme jaké máme větve::

    $ git branch -la

    * master
    pokusna_vetev
    remotes/origin/master

Ověříme, *kde* v historii větev vlastně vznikla (buď v `gitk` nebo pomocí
logu)::

    $ git tree

    * 1a99084 (HEAD -> master, pokusna_vetev) Doplnění sekce práce s gitem
    * bc12c5d last note
    *   6574bcf (origin/master) Merge pull request #1 from madlenkk/master
    |\  
    | * 83221c8 Opravy překlepů
    |/  
    * 7c75607 neco o gitu
    * c9aa4cf pridavam README
    * a7440f4 initial commit

Vidíte, že `pokusna_vetev` vznikla na místě, kd se aktuálně nachází moje
rozdělaná práce (`HEAD`), což shodou okolností odpovídá stavu větve `master`.

Přepnu se do větve `pokusna_vetev` a zapíšu všechny změny::

    $ git checkout pokusna_vetev

    $ git commit -a -m"Commit do jine vetve"

    $ git tree

    * 2e03719 (HEAD, pokusna_vetev) commit do jine vetve
    * b89a5c0 (master) pokracovani dokumentace
    * 1a99084 Doplnění sekce práce s gitem
    * bc12c5d last note
    *   6574bcf (origin/master) Merge pull request #1 from madlenkk/master
    |\  
    | * 83221c8 Opravy překlepů
    |/  
    * 7c75607 neco o gitu
    * c9aa4cf pridavam README
    * a7440f4 initial commit

Přepnu se zpátky do větve `master` a provedu záměrně nějakou konfliktní změnu v
existujícím souboru::

    $ git checkout master

    # editace existujícího souboru

    $ git commit -m"vyroba konfliktniho řádečku" -a
    $ git show 

    commit 096304c55364e3e4b849fe567402b3444258a49e
    Author: Jachym Cepicky <jachym.cepicky@gmail.com>
    Date:   Mon Sep 19 17:54:14 2016 +0200
    
        vyroba konfliktniho řádečku
    
    diff --git a/vetveni.rst b/vetveni.rst
    index b754523..29faf4d 100644
    --- a/vetveni.rst
    +++ b/vetveni.rst
    @@ -72,4 +72,4 @@ Jak to vypadá v PyWPS::
           remotes/jan-rudolf/master
     
         
    -
    +Tady vyrobíme nějaký ten konfliktní řádeček


Jak to vypadá s historií revizí::

    $ git tree

    * 096304c (HEAD -> master) vyroba konfliktniho řádečku
    | * 2e03719 (pokusna_vetev) commit do jine vetve
    |/  
    * b89a5c0 pokracovani dokumentace
    * 1a99084 Doplnění sekce práce s gitem
    * bc12c5d last note
    *   6574bcf (origin/master) Merge pull request #1 from madlenkk/master
    |\  
    | * 83221c8 Opravy překlepů
    |/  
    * 7c75607 neco o gitu
    * c9aa4cf pridavam README
    * a7440f4 initial commit
    

A nyní můžeme vyzkoušet spojení větví. Chci změny **z větve** `pokusna_vetev`
spojit **do větve** `master`::

    # projistotu

    $ git checkout master
    $ git status
    On branch master
    Your branch is ahead of 'origin/master' by 3 commits.
      (use "git push" to publish your local commits)
     ...

    # vlastní merge

    $ git merge pokusna_vetev

    Auto-merging vetveni.rst
    CONFLICT (content): Merge conflict in vetveni.rst
    Automatic merge failed; fix conflicts and then commit the result.

Hurá, máme konflikt a musíme ho vyřešit. Protože máme perfektní nástroj na řešní
konfliktů nastavený, stačí použít `git mergetool`, který spustí textový editor
VIM, ve kterém mohu pohldně konflikty vyřešit.::

    $ git mergetool

Merge je v podstatě samostaný commit, po vyřešení konfliktů musím commit vyrobit
ručně::

    $ git commit

V textovém editoru se mi nabídne komentář "Merge branch 'pokusna_vetev'".
Uložte soubor a mergování bude samo automaticky pokračovat.

Výsledek::

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
    ...

Mám novou revizi 6ebd5ea, vzniklou sloučením větví `pokusna_branch` a `master`,
vyřešili jsme ručně konflikt. Vše se děje na lokálním repozitáři - serverová
verze pořád zůstala *zamrzlá* na revizi 6574bcf. Je čas poslat změny na server.
