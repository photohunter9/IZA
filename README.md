# Badmephisto's Speedcubing
## Dokumentácia k projektu do predmetu IZA

#### 1. Popis aplikácie
Aplikácia **Badmephisto's Speecubing** je určená pre fanúšikov skladania Rubikovej kocky na čas. Táto disciplína sa tiež nazýva *speedcubing* (rýchlostné skladanie kocky) a algoritmy ktoré sa v tejto aplikácií nachádzajú, ako aj popisy k nim sú prevzaté zo známej stránky Andreja Karpathyho známeho pod akronymom *badmephisto*. Aplikácia teda poskytuje zoznam algoritmov na skladanie Rubikovej kocky, ako aj popisy k nim s rôznymi radami na ľahšie zapamätanie. Okrem toho aplikácia poskytuje aj sekciu so znázornením notácie využívanej v algoritmoch, užitočnú hlavne pre nových speedcuberov alebo pre pripomenutie menej používaných značení. Poslednú sekciu aplikácie tvoria užitočné stopky prispôsobené pre speedcubing. Tie ukladajú každý čas ktorý užívateľ zmeria a poskytujú zaujímavé štatisky ako priemerný či najlepší čas ako aj zoznam všetkých časov.

#### 2. Popis implentácie
Implementácia aplikácie bola vďaka vývojovému prostrediu **Xcode** relatívne jednoduchá. A prebiehala v niekoľkých krokoch:
##### 2.1. Storyboard
Najprv bolo potrebné vytvoriť *Storyboard* určujúci rozloženie sekcií rovnako ako dizajn užívateľského rozhrania. Ako koreň navigácie som zvolil Tab Bar Controller keďže aplikácia bude mať len 4 hlavné sekcie a prepínanie medzi nimi by malo byť čo najrýchlejšie a čo najpraktickejšie. Každá zo sekcií Tab Bar Controlleru je ďalej zabalená do Navigation Controlleru, keďže tri z nich budú potrebovať zobraziť ďalšiu obrazovku, a vo štvrtej pridaný z dôvodu zachovania dizajnu s vrchnou lištou s názvom sekcie. Dve sekcie s algoritmami využívajú scénu zobrazujúcu detail algoritmu s popisom, zatiaľ čo sekcia s časovačom obsahuje scénu zobrazujúcu štatistiky nameraných časov.
##### 2.2. OLL a PLL Table View Controllery
Tieto jednoduché Controllery obsahujú pole stringov s algoritmami a komentármi k nim. Tieto potom využívajú pri plnení tabuľky spolu s obrázkami z *Assetov*. Takisto implementuje preparáciu na prechod na pohľad detailu kde nastaví typ a index algoritmu ktorého detail sa má zobraziť.
##### 2.3 Detail View Controller
Detail View Controller obsahuje premenné *algType* a *algIndex* jednoznačne idetifikujúce ktorý algoritmus sa má zobraziť. Tieto premenné sú nastavené OLL alebo PLL Table View Controllerom pri prechode na Detail View. Podľa týchto premenných potom Detail Viewe Controller nastaví obrázok, algoritmus aj komentár pri načítaní pohľadu.
##### 2.4 Timer View Controller
Tento View Controller obsluhuje časovač na meranie času potrebného na zloženie kocky. Tejto úlohe je prispôsobený aj samotný pohľad, ktorý obsahuje veľké tlačidlo na zapnutie, zastavenie a vynulovanie časovača. Na meranie času používa scheduledTimer systémového objektu Timer, ktorý spustí každú sekundu jednoduchú funkciu ktorá pričíta čas a aktualizuje zobrazený čas. Pri vynulovaní časovača dôjde k uloženiu času. iOS ponúka viaceré možnosti ako perzistentne ukladať dáta aplikácie. Pri implementácií ukladania časov som však zvažoval hlavne dve alternatívy. Prvou z nich je uloženie dát pomocou *UIDocument*, ktorý poskytuje uloženie dát formou dokumentu ktorý je možné asynchrónne čítať aj zapisovať. Existuje však aj druhá možnosť a tou je využitie *UserDefaults* ktoré je síce primárne určené na ukladanie preferencií, no je tiež ideálne na uloženie malého objemu dát, čo je aj prípad tejto aplikácie. Rozhodol som sa preto využiť UserDefaults a vytvoriť v ňom pole integerov reprezentujúcich namerané časy v stotinách sekúnd.
##### 2.5 Statistics View Controller
Namerané dáta sa využijú v Statistics View Controlleri ktorý načíta časy z UserDefaults a následne z nich vypočíta priemerný čas, nájde ten najlepší a podobne. Okrem toho tiež vyplní tabuľku zo všetkými časmi zoradenými chronologicky od najnovšeiho po najstarší. Je tu tiež možnosť vymazať namerané časy.

#### 3 Záver
Výslednú aplikáciu som dal na otestovanie dvom užívateľom z cieľovej skupiny ktorí boli s aplikáciou celkovo spokojný, uviedli však aj návrhy na zlepšenie vo forme pridania možnosti mazať namerané časy jednotlivo a tiež pridanie ďalších informácií napríklad o náročnosti alebo pravdepodobnosti výskytu algoritmov pri zobrazení detailu. Tieto vylepšenia by mohli byť súčasťou budúcej práce na aplikácií.