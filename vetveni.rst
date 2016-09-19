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

    

