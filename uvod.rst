.. _uvod:

****
Úvod
****

Systém správy verzí (`Version control`_) je důležitou částí správy programů,
dokumentů webových stránek a dalších informací. Změny jsou ukládávny do bloků,
tzv. *revizí* - jedna revize odpovídá stavu celého projektu v určitý čas. Systém
správy verzí jde k počátkům knihtisku, kdy se jednotlivá vydání knihy označují
datem nebo číslem vydání. Dalším úkolem systémů správy verzí je nějak umožnit
spolupracovat více lidem na jednom souboru a "sehrávat" dohromady změny na
různých ale i stejných místech (pomáhají tak řešit vzniklé *konflikty*). 

Ke správě verzí se nejčastěji používají speciální programy. Často je správa
verzí zapracována do softwarových produktů (MS Word) nebo služeb (Wikipedia).

Spravovat verze softwaru můžeme i "ručně" prostřednictvím vytváření kopií
existujícícho software. V praxi to ale vede ke spoustě chyb, málo kdo je tak
disciplinovaný, aby pro každý pokus v konfiguračním souboru vytvořil nejprve
stabilní kopii nebo naopak vytvořil kopii na hraní.

Občas je potřeba pracovat na několika verzích najednou, mít možnost mezi nimi
rychle přepínat, vrátit se v historii, "odskočit si" do "verze z verze" a
vyzkoušet jiný postup a tak dále. 

Struktura použitá ve verzovacích systémech
==========================================

Změny vs. celé soubory
----------------------

Verzovací systémy pracují s daty v čase a ty lze uložit do různých struktur.
Některé systémy ukládají pouze změny mezi soubory, což je výhodné při menších
změnách ale komplikuje práci při komplexních změnách, jiné naopak ukládají celé
souboury a zpětně dopočítávají změny mezi nimi, což je právě výhodnější při
práci s komplexními změnami.

Aby mohla být změna v nějakém souboru zaznamenána v sytému, musí být nejprve
*commitnuta*. *Necommitnutá* změna zatím nezaznamenaná v systému správy verzí je
*pracovní kopie*. Je to podobné, jako když otevřete soubor, provádíte změny a
*dokud změny nezapíšete zpátky na disk, změny se v souboru neprojeví*.

Centrální vs. distribuovaný
---------------------------

Způsob uspořádání pracovních kopií a různých verzí a větví může být buď
*centrální*, kdy se všichni pracovníci vztahují k jednomu centrálnímu
repozitáři nebo naopak *distribuovaný*, kdy každý uživatel je pánem své
vlastní verze celého programu - žádná kopie není striktvně autoritativní.

Struktura revizí
----------------

I když je praxe často komplikovaná, nejbližší aproximací ukládání změn v systému
verzí je představa stromu s centrálním hlavní kmenem, z něhož jsou odvozeny
větve (které by se měly ideálně vracet zpět dohlaního kmene).

Každá změna zaznamenaná v kódu je označena jako *revize*. *Revize* je jedinečná
sada změn v čase, označená unikátním identifikátorem.

Hlavní "větev", na které se účastníci projektu dohodli jako na větvi, kde se
budou shromažďovat finální změny se označuje jako *trunk* nebo *master*.

Nová revize může vzniknout i sloučením předchozích větví - *mergováním*. Nová
revize tak má za "rodiče" více než jednu větev.

Klíčová slova
=============

:Branch - Větev:
    Sada souborů, jejichž kopie byla v určitém čase uložena do
    zvláštní větve a jsou na nich prováděny separátní změny. Takže obě kopie
    těchto souborů povedou k různému výsledku.

:Diff - Výpis změn:
    Většinou textový výpis znázorňující změnu mezi dvěma revizemi

:Checkout - čekautovat:
    Vytvořit lokální kopii revizí ze vzdáleného repozitáře. 

:Clone - klonovat:
    Vytvořit nový repozitář obsahující revize z jiného repozitáře. 

:Commit - komit:
    Zapsat nebo *mergovat* změny z neuložené *lokální kopie* zpět do repozitáře.

:Conflict - konflikt:
    Konflikt vznikne, pokud dvě strany provedly změny v souborech a systém je
    není schopen sám automaticky spojit. Uživatel obvykle musí konflikty vyřešit
    - *resolve* - ručně vybráním preferované verze nebo jejich ručním sloučením.

:HEAD:
    Revize, na kterou ukazuje aktuální verze - většinou poslední revize v dané
    větvi.

:Merge - merdžovat:
    Operace, během které jsou na jeden soubor aplikovány dvě sady změn.

:Pull, push - pulovat, pušovat:
    Kopírování revizí z jednoho repozitáře do druhého. Buď z cílového repozitáře
    "do mého" nebo kopírovat změny z mého lokálního repozitáře do cílového.

:Repository - repozitář:
    Místo, nejčastěji na serveru, ve kterém jsou kopie souborů spolu s jejich
    kompletní historií

:Revize:
    Změna v jakékoliv formě - je to stav celého vývojového stromu v nějakém
    čase. Jako synonymum se často používá *commit*.

:Tag:
    *Záložka*, speciálně pojmenovaný commit (revize) většinou odkazuje k
    nějaké významné události v čase projektu.

:Trunk, master:
    Unikátní vývojová linie která není větev (nebo naopak je "hlavní vývojová
    větev" záleží na pojmenování).

:Working copy - pracovní kopie:
    Změny sice uložené do souborů a zapsané na disk, ale zatím neuložené do
    repozitáře (pomocí *commitu*). 

Na co je vhodné používat verzovací systémy
==========================================

Nejvíce se hodí na textové soubory nebo malé binární soubory. Změny se totiž
nejčastěji ukládají (a zobrazují) po řádcích. Binární soubory (jako jsou
zazipované archivy, word dokumenty, velké obrázky a pod.) nemají více řádků -
udělat mezi nimi pro člověka nebo počítač čitelný rozdíl je nemožné.

V určitých projektech to může znamenat změnu workflow, přizpůsobení nástrojů
verzovatelnosti. Je snazší verzovat několik textových souborů (ve formátu LaTeX)
než wordovské dokumenty (na to se musí použít interní nástroj Wordu ... se vším
dobrým i zlým).


**Odkazy**

.. _Version control:  https://en.wikipedia.org/wiki/Version_control
