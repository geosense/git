Dalších pár tipů
================

Tagy
----

`tag` je záložka posazená na určitou revizi. Trochu se tváří jako větev. Je to
místo, kam se můžete chtít v budoucnu vrátit (třeba verze)::

    git tag verze-1.2.3

Hooky
-----

Hook (háček) je, co se má stát, když se v repozitáři udělá nějaká změna.
Nejčastěji na `push` do repozitáře, ale může to být i nová větev, tag, smazání
větve, atd atd.. My na každý `push` pouštíme sadu testů a build aplikace

Rozdíl mezi GIT, GITHub, GitLab
-------------------------------

GIT
    je systém pro správu verzí, umožňující vedení několika paralelních větví
    projektu, umožňuje jejich slučování, vede historii projektu. GIT je open
    source.

GITHub
    je webová stránka/služba, která dává k dispozici zdarma git repozitáře na
    serveru (pro open source projekty), přidává sociální aspekt k vývoji, bug
    tracker, wiki, spoustu webových nastavovátek. GITHub sice hostuje hromadu
    open source projektů, ale sama o sobě je proprietární

GITLab
    Je trochu jako GITHub, ale open source, můžete si to nainstalovat k sobě na
    server a provozovat. U nás žije na http://gitlab.geo doméně
