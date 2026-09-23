# Inštrukcie pre anotátora — referenčné Učebné výstupy lekcie

Tento dokument popisuje, ako vytvoriť **referenčnú množinu Učebných výstupov** (Learning Outcomes) pre jednu video lekciu. Inštrukcie sú písané tak, aby boli použiteľné rovnako pre **človeka** ako aj pre **jazykový model**; oboch budeme ďalej označovať jednotne ako *anotátor*.

Výstupom tejto úlohy je súbor riadkov v CSV formáte (viď §Výstup), ktorý sa následne použije ako referenčný (gold) štandard pri vyhodnotení automatickej extrakcie.

## Vstupy

K dispozícii je dvojica zdrojov pre danú lekciu:

- **Video lekcia** — autoritatívny zdroj.
- **Transkript videa** — vygenerovaný automaticky, slúži ako podporný zdroj a referenčný text.

Voľba zdroja závisí od typu anotátora:

- **Človek** by mal pri tvorbe LO uprednostňovať **video** (s transkriptom ako podpornou pomôckou), pretože video obsahuje aj neverbálnu informáciu (ukazované obrázky, kód, zapojenia) a transkript môže obsahovať chyby rozpoznávania reči. V prípade nezhody má vždy prednosť video.
- **Jazykový model (LLM)** v štandardnom režime pracuje **iba s transkriptom**, pokiaľ nie je v konkrétnom experimente uvedené inak.

## Nezávislosť anotácie

Anotácia je vždy **slepá** — pri tvorbe Učebných výstupov sa nikdy nepozeraj na anotácie iných ľudí ani strojov a neber ich do úvahy. Riaď sa výlučne týmito inštrukciami, zoznamom slovies v `bloom_verbs.csv` a vlastným úsudkom nad danou lekciou. Tým sa zachováva nezávislosť anotátorov, ktorá je nevyhnutná pre korektné meranie medzianotátorskej zhody a pre férové porovnanie automatickej extrakcie voči referenčným anotáciám.

## Čo je Učebný výstup

**Učebný výstup** (ďalej *LO*) je jediná slovenská veta v tvare:

> *Študent vie [aktívne sloveso v infinitíve] [predmet] [doplnenie].*

ktorá vyjadruje, čo má študent po danej časti lekcie vedieť alebo dokázať. Tento tvar (modálne *vie* + infinitív) zodpovedá štandardnej formulácii Učebných výstupov v slovenských kurikulárnych dokumentoch a zároveň anglickému *„the student will be able to …"* (SWBAT).

LO je **na strane obsahu** — opisuje, čo lekcia učí. Je nezávislý od konkrétneho študenta.

## Tvar slovesa

Sloveso v LO musí byť vybrané zo **zatvoreného zoznamu kanonických slovenských Bloomových slovesných kotiev**, definovaných v súbore `../bloom_verbs.csv` (jediný zdroj pravdy pre povolené slovesá). Zoznam má 6 úrovní (1 = Zapamätať si, 6 = Tvoriť) a 6–8 slovies na úroveň.

V `bloom_verbs.csv` sú slovesá uvedené v **infinitívnom tvare** (napr. *vymenovať*, *interpretovať*, *skonštruovať*) — tom istom, ktorý sa v LO vete vyskytuje za modálnym *vie* (napr. *„Študent vie vymenovať …"*, *„Študent vie interpretovať …"*, *„Študent vie skonštruovať …"*). V stĺpci `verb` výstupného CSV sa zaznamenáva presne tento infinitív — slúži ako kotva pre kontrolu konzistencie voči `bloom_verbs.csv`.

Ak by danému LO sémanticky sedelo sloveso, ktoré v zozname nie je, vyberie sa najbližšie ekvivalentné z toho istého zoznamu.

### Programovanie a zapojenia

Pri Učebných výstupoch zameraných na tvorbu kódu alebo fyzické zapojenia sa odporúča explicitný objektový tvar:

- *„Študent vie skonštruovať program, ktorý …"* — pre LO o písaní kódu (napr. v MakeCode),
- *„Študent vie skonštruovať zapojenie, ktoré …"* alebo *„Študent vie použiť krokosvorkové káble na zapojenie …"* — pre LO o fyzickom zapájaní hardvéru.

Vyhýbaj sa neurčitému tvaru *„Študent vie skonštruovať …"* bez objektu — vždy uveď, *čo* sa konštruuje.

## Úroveň kognitívneho procesu

Každý LO sa označí jednou zo šiestich úrovní Revidovanej Bloomovej taxonómie:

| Úroveň | Názov | Čo študent po lekcii vie |
|---|---|---|
| 1 | Zapamätať si | vybaviť si fakty z dlhodobej pamäte |
| 2 | Porozumieť | konštruovať význam na základe získaných informácií |
| 3 | Aplikovať | použiť postup alebo štruktúru v konkrétnej situácii |
| 4 | Analyzovať | rozložiť celok na časti a určiť ich vzájomné vzťahy |
| 5 | Hodnotiť | posúdiť podľa daných kritérií a štandardov |
| 6 | Tvoriť | vytvoriť nový vnútorne súdržný celok z jednotlivých prvkov |

Ak by LO obsahovalo slovesá z viacerých úrovní, anotátor zvolí **najvyššiu** prítomnú úroveň. Sloveso a úroveň musia byť vzájomne konzistentné — pre zvolenú úroveň sa použije sloveso z `bloom_verbs.csv` patriace tej istej úrovni.

## Postup anotácie

1. **Oboznámenie sa s lekciou.** Pozri si video a/alebo prečítaj transkript v plnom rozsahu, aby si získal predstavu o štruktúre a hlavných témach lekcie.
2. **Identifikácia učebných obsahov.** Po každom logickom celku (typicky 30–90 sekúnd vo videu, prípadne jeden tematický odsek v transkripte) si polož otázku: *Čo by mal študent vedieť alebo dokázať po tejto časti?* Odpoveď zaznamenaj ako kandidát na LO.
3. **Formulácia LO.** Každého kandidáta zapíš ako jednu vetu v tvare *„Študent vie [infinitív] [predmet] …"*. Sloveso vyber z `bloom_verbs.csv` tak, aby čo najpresnejšie odrážalo požadovanú kognitívnu aktivitu.
4. **Priradenie úrovne.** Doplň úroveň kognitívneho procesu (1–6) zodpovedajúcu zvolenému slovesu.
5. **Kontrola.** Pre každý LO over:
   - je veta v tvare *„Študent vie [infinitív] [predmet] …"*,
   - je sloveso v zozname `bloom_verbs.csv` pre priradenú úroveň,
   - je obsah LO viditeľný v lekcii (nie domyslený mimo zdroja),
   - je LO **atomický** (presne jedno aktívne sloveso, jeden konkrétny výstup — žiadne *„a"* spájajúce dva ciele).

## Pravidlá pre hraničné prípady

- **Atomicita.** LO obsahuje práve **jedno** aktívne sloveso a **jeden** súdržný cieľ. Veta typu *„Študent vie porovnať X a Y a spracovať zistenia do tabuľky"* obsahuje dva ciele (porovnať, spracovať) — rozdeľ ju na dva samostatné LO.
- **Trivialita.** Nezahŕňaj LO, ktoré je čistá výplň reči (napr. *„Študent vie opísať, že lekcia začína"*).
- **Halucinácia.** Nezahŕňaj LO, ktorého obsah nie je viditeľný v zdroji. Ak si nie si istý, či je daný obsah v lekcii, radšej ho vynechaj.
- **Duplicity.** Ak ten istý výstup zaznie v lekcii viackrát, zaznamenaj ho len raz.
- **Granularita.** Cieľová granularita je *jeden LO na 30–90 sekúnd lekcie*. Príliš jemné delenie produkuje triviálne LO; príliš hrubé delenie spája viacero výstupov do jedného.

## Rozhranie medzi úrovňami CP1 a CP2

Najčastejšie nejasné rozhranie je medzi úrovňami **1 (Zapamätať si)** a **2 (Porozumieť)**. Rozdiel je v tom, *čo má študent so získanou informáciou robiť*:

- **CP1 — Zapamätať si.** Študent má fakt iba **vybaviť** alebo **uviesť** z pamäte; nevyžaduje sa od neho, aby informáciu vysvetlil, parafrázoval alebo dal do súvislosti. Príklady: *„Študent vie uviesť, že micro:bit má kolíky 0, 1 a 2"*, *„Študent vie vymenovať tri farby LED pásika"*, *„Študent vie pomenovať komponenty potrebné na zostrojenie obvodu"*.
- **CP2 — Porozumieť.** Študent má z faktu **konštruovať význam** — vysvetliť, prečo niečo funguje, ako sa veci vzájomne vzťahujú, alebo preformulovať myšlienku vlastnými slovami. Príklady: *„Študent vie vysvetliť, prečo dlhšie LED pásiky potrebujú 5V napájanie"*, *„Študent vie opísať vzťah medzi frekvenciou tónu a notou"*, *„Študent vie interpretovať priebeh signálu na grafe"*.

**Rozhodovacie pravidlo.** Ak LO vyžaduje len **vymenovanie**, **uvedenie** alebo **identifikáciu** faktu, zvoľ **CP1** aj v prípade, že by veta gramaticky znela aj so slovesom *opísať*. Sloveso *opísať* a CP2 sa použijú iba vtedy, keď študent musí z informácie vyvodiť význam alebo súvislosť — nie iba zopakovať, čo bolo v lekcii povedané.

## Výstup

Anotátor odovzdá CSV súbor s nasledovnými stĺpcami:

| stĺpec | typ | popis |
|---|---|---|
| `course_id` | int | identifikátor kurzu |
| `lecture_slug` | str | identifikátor lekcie (slug, napr. `bananovy-klavir`) |
| `lecture_title` | str | názov lekcie |
| `annotator` | str | identifikátor anotátora (napr. `annotator_a`, `llm_v1`) |
| `lo_id` | str | unikátny identifikátor LO v rámci anotátora a lekcie |
| `text` | str | celá veta LO (*„Študent …"*) |
| `verb` | str | sloveso z `bloom_verbs.csv` |
| `cognitive_process` | int (1–6) | úroveň kognitívneho procesu |

Príklad jedného riadka:

```csv
course_id,lecture_slug,lecture_title,annotator,lo_id,text,verb,cognitive_process
1,bananovy-klavir,Banánový klavír,annotator_a,a_bananovy_klavir_001,"Študent vie vymenovať programovateľné kolíky micro:bita: 0, 1 a 2.",vymenovať,1
```

## Self-check po dokončení

Pred odovzdaním súboru anotátor potvrdí:

- každý riadok prešiel kontrolou v §Postup anotácie, krok 5,
- v rámci jednej lekcie sa žiadne dva LO nepokrývajú obsahovo (nie sú duplicitné ani parafrázy toho istého),
- žiadny LO neobsahuje dva ciele spojené *„a"* alebo *„aj"* (atomicita),
- pomer LO naprieč úrovňami zhruba odráža charakter lekcie (faktografická lekcia môže mať väčšinu na úrovniach 1–2; projektová lekcia bude mať viac na úrovniach 3–6),
- zoznam LO predstavuje *úplnú* referenciu pre danú lekciu — všetko, čo by mal študent vedieť po lekcii, je v ňom zachytené.
