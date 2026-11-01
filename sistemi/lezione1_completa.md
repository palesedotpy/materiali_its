# Sistemi — Lezione 1 (30/10/2026)

> **Legenda**
> - ⚠️ **Correzione**: punto degli appunti originali che conteneva un errore o un'imprecisione.
> - 💡 **Approfondimento**: materiale aggiunto, utile da sapere anche se forse non era nelle slide.

---

## 1. Cos'è l'informatica?

- **Definizione**: l'informatica è la scienza che studia l'**elaborazione automatica delle informazioni** e le sue applicazioni.
- Il termine deriva dal francese *informatique* = **INFOR**mazione + auto**MATICA** (Philippe Dreyfus, 1962). In inglese si usa *Computer Science*.
- "Tutto ciò che esiste nell'universo" → l'idea è che **qualsiasi cosa può essere vista come informazione**: numeri, testi, immagini, suoni, DNA, il comportamento di un sistema fisico. Se qualcosa può essere **codificato** (tipicamente in bit), può essere elaborato da un calcolatore.

> 💡 **Approfondimento — Informazione e bit**
> L'unità minima di informazione è il **bit** (*binary digit*), che può valere 0 oppure 1. Claude Shannon (1948) ha fondato la *teoria dell'informazione*: un bit è la quantità di informazione necessaria per scegliere tra due alternative equiprobabili.

---

## 2. Cos'è un calcolatore?

- Un **calcolatore** è un sistema che riceve dei **dati in ingresso (input)**, li elabora seguendo un **algoritmo** e restituisce dei **risultati (output)**.

```
  INPUT  ──►  [ ELABORAZIONE (algoritmo) ]  ──►  OUTPUT
```

- **Computer**: unità in grado di eseguire **semplici operazioni aritmetiche e logiche** a una velocità molto superiore a quella di un essere umano. Il computer non è "intelligente": è velocissimo ed estremamente preciso nell'eseguire istruzioni elementari.

### Algoritmo

Un **algoritmo** è una sequenza **finita** di istruzioni **non ambigue** che, eseguite in ordine, risolvono un problema in un **numero finito di passi**.

Proprietà di un algoritmo:

| Proprietà         | Significato                                        |
| ----------------- | -------------------------------------------------- |
| **Finitezza**     | termina dopo un numero finito di passi             |
| **Non ambiguità** | ogni istruzione ha un solo significato possibile   |
| **Determinismo**  | a parità di input, produce sempre lo stesso output |
| **Eseguibilità**  | ogni passo è realmente eseguibile dall'esecutore   |
| **Generalità**    | risolve una *classe* di problemi, non un solo caso |

### Programma

- Un **programma** è un **algoritmo scritto in un linguaggio di programmazione**, cioè in una forma comprensibile (direttamente o dopo una traduzione) dal calcolatore.
- Celebre definizione di Niklaus Wirth: **Algoritmi + Strutture dati = Programmi**.

### Grammatiche di Chomsky

Un linguaggio di programmazione è un **linguaggio formale**: ha un alfabeto e delle regole precise (una **grammatica**) che stabiliscono quali frasi sono corrette. Noam Chomsky (1956) ha classificato le grammatiche in una gerarchia di 4 tipi:

| Tipo | Grammatica | Riconosciuta da | Esempio d'uso in informatica |
|---|---|---|---|
| **0** | Illimitata (ricorsivamente enumerabile) | Macchina di Turing | qualsiasi problema calcolabile |
| **1** | Dipendente dal contesto | Automa lineare limitato | — |
| **2** | Libera dal contesto (*context-free*) | Automa a pila | **sintassi** dei linguaggi di programmazione (parentesi bilanciate, blocchi annidati) |
| **3** | Regolare | Automa a stati finiti | **espressioni regolari**, analisi lessicale (riconoscere numeri, identificatori, parole chiave) |

Ogni tipo contiene il successivo: Tipo 3 ⊂ Tipo 2 ⊂ Tipo 1 ⊂ Tipo 0.

---

## 3. Programma e dati di ingresso

L'esecuzione di un programma coinvolge sempre tre elementi:

```
   PROGRAMMA (istruzioni)  ─┐
                            ├──►  ESECUTORE (calcolatore)  ──►  RISULTATI
   DATI DI INGRESSO       ──┘
```

- Il **programma** descrive *come* elaborare i dati; è lo stesso ogni volta.
- I **dati di ingresso** cambiano a ogni esecuzione.
- Lo stesso programma, con dati diversi, produce risultati diversi (es. un programma che somma due numeri).

> 💡 **Approfondimento — Architettura di Von Neumann**
> Nei calcolatori moderni **programma e dati risiedono nella stessa memoria** (concetto di *programma memorizzato*, John von Neumann, 1945). Componenti:
> - **CPU**: **ALU** (unità aritmetico-logica, fa i calcoli) + **CU** (unità di controllo, decide cosa fare) + **registri** (memorie velocissime interne);
> - **Memoria centrale (RAM)**: contiene istruzioni e dati;
> - **Dispositivi di I/O**: tastiera, schermo, disco, rete…;
> - **Bus**: collegano i componenti.
>
> La CPU esegue in loop il **ciclo fetch → decode → execute**: preleva un'istruzione dalla memoria, la decodifica, la esegue, passa alla successiva.

---

## 4. Tipologie di linguaggi (paradigmi di programmazione)

### Imperativo
Il programma è una **sequenza di comandi** che modificano lo stato (le variabili) della macchina. Si dice *come* fare le cose, passo per passo.
- Esempi: **C, Rust, Python, Java, Go, Pascal**.
- Sottocategoria importante: **orientato agli oggetti** (C++, Java, C#, Python).

### Dichiarativo (o descrittivo)
Si descrive **cosa** si vuole ottenere, non come ottenerlo.
- **Linguaggi di markup / descrizione**: HTML (struttura di una pagina), CSS (stile), XML (dati strutturati). ⚠️ Non sono linguaggi di programmazione in senso stretto: non hanno istruzioni di controllo (cicli, condizioni).
- **Linguaggi di interrogazione**: **SQL** (`SELECT nome FROM studenti WHERE voto > 27` → dici *cosa* vuoi, il database decide *come* trovarlo).

### Funzionale
Il programma è una **composizione di funzioni matematiche**; si evitano variabili modificabili ed effetti collaterali. Le funzioni sono "cittadini di prima classe" (si possono passare come argomenti e restituire).
- Esempi: **Haskell**, Lisp, Scheme, OCaml, F#, Erlang, Elixir.

> ⚠️ **Correzione**
> - **Lua** non è un linguaggio funzionale puro: è un linguaggio di scripting **multi-paradigma** (principalmente imperativo) che supporta alcune caratteristiche funzionali (funzioni come valori, closure). Probabilmente il professore lo citava per questo.

### Logico
Si **descrive il problema** tramite fatti e regole logiche; è la macchina a trovare la soluzione da sola, usando un **motore di inferenza** (risolutore logico).
- Esempio: **Prolog**.

```prolog
genitore(anna, marco).
genitore(marco, luca).
nonno(X, Z) :- genitore(X, Y), genitore(Y, Z).
% Domanda:  ?- nonno(anna, luca).   →  true
```

### Multi-paradigma: il caso Verse
- **Verse** è il linguaggio creato da **Epic Games** (l'azienda di Unreal Engine e Fortnite, fondata da Tim Sweeney), progettato con **Simon Peyton Jones** (uno dei principali creatori di Haskell) e **Lennart Augustsson**.
- È definito un linguaggio **funzionale-logico**, con una sintassi familiare a chi viene dai linguaggi imperativi.

> 💡 **Approfondimento**: molti linguaggi moderni sono **multi-paradigma** (Python, JavaScript, Rust, Scala, Kotlin): permettono di programmare in stile imperativo, a oggetti e funzionale.

---

## 5. Curiosità sull'hardware dette a lezione

### "L'istruzione più pesante per un processore è un jump"
- I processori moderni usano una **pipeline**: eseguono più istruzioni in parallelo, ognuna in una fase diversa (come una catena di montaggio).
- Un **salto (jump/branch)**, specialmente se **condizionato** (`if`, cicli), interrompe il flusso: il processore non sa quale sarà la prossima istruzione finché la condizione non è calcolata.
- Il processore cerca di **indovinare** (*branch prediction*). Se sbaglia, deve **svuotare la pipeline** e ricominciare: perde decine di cicli di clock.
- Per questo il codice con molti `if` imprevedibili può essere sensibilmente più lento.

### "Una GPU ha praticamente solo ALU"
- Una **CPU** ha pochi core (4–32) molto complessi: molta logica di controllo, grandi cache, branch prediction → ottima per compiti **sequenziali** e con molte decisioni.
- Una **GPU** ha **migliaia di core semplici**, quasi solo ALU, con poca logica di controllo → esegue **la stessa operazione su moltissimi dati contemporaneamente** (modello SIMD/SIMT).
- Ideale per grafica, calcolo matriciale, intelligenza artificiale. Meno adatta a codice pieno di salti (collegamento con il punto precedente!).

---

## 6. Linguaggi compilati, interpretati e pseudocompilati

I linguaggi ad **alto livello** (vicini al linguaggio umano) **non sono direttamente eseguibili** da un calcolatore, che capisce solo il **linguaggio macchina** (sequenze di bit specifiche per ogni processore). Serve quindi una **traduzione**, che può avvenire in tre modi.

> ⚠️ **Correzione**: negli appunti c'era "deve essere compilato": più precisamente deve essere **tradotto** in linguaggio macchina, tramite **compilazione** oppure **interpretazione**.

### Linguaggi compilati
- Un programma detto **compilatore** traduce **tutto il codice sorgente, una volta sola, prima dell'esecuzione**, producendo un **file eseguibile** in linguaggio macchina.
- Esempi: **C, C++, Rust, Go**, Fortran.
- ✅ Esecuzione molto veloce; errori di sintassi/tipo trovati prima dell'esecuzione.
- ❌ L'eseguibile dipende dall'architettura (un `.exe` per x86 non gira su ARM); bisogna ricompilare a ogni modifica.

Fasi della compilazione:
```
codice sorgente → analisi lessicale → analisi sintattica → analisi semantica
               → ottimizzazione → generazione codice oggetto → linking → eseguibile
```

### Linguaggi interpretati
- Un **interprete** legge il programma **istruzione per istruzione**, la traduce e la **esegue subito**, poi passa alla successiva. Non viene prodotto un eseguibile.
- Esempi: **Python** (in parte, vedi sotto), JavaScript (storicamente), PHP, Bash, Ruby.
- ✅ Portabile (basta avere l'interprete); modifiche immediate senza ricompilare.
- ❌ Più lento (la traduzione si ripete a ogni esecuzione); alcuni errori emergono solo durante l'esecuzione.

### Linguaggi pseudocompilati (ibridi)
- Il programma viene compilato in un **formato intermedio** (**bytecode**), indipendente dall'hardware.
- Il bytecode viene poi eseguito da una **macchina virtuale** (VM), che lo interpreta oppure lo compila "al volo" (**JIT – Just In Time**).
- Esempi: **Java** (`.java` → `.class` → **JVM**), **C#** (→ CIL → **.NET CLR**), **Python** (CPython compila in `.pyc` e poi lo interpreta).
- ✅ Compromesso tra portabilità ("*write once, run anywhere*") e velocità.

| | Compilato | Interpretato | Pseudocompilato |
|---|---|---|---|
| Traduzione | tutta, prima | riga per riga, durante | in bytecode, poi VM |
| Velocità | alta | bassa | media/alta (JIT) |
| Portabilità | bassa | alta | alta |
| Esempi | C, Rust | Bash, PHP | Java, C# |

---

## 7. Insiemi numerici, infinito e numeri non computabili

> ⚠️ **Correzione**: negli appunti gli esempi erano attribuiti agli insiemi sbagliati (es. √2 non è razionale, 1, 3, 6, −4 sono interi). Ecco la classificazione corretta.

| Insieme | Simbolo | Descrizione | Esempi |
|---|---|---|---|
| Naturali | ℕ | interi non negativi | 0, 1, 2, 3, 6 |
| Interi | ℤ | naturali + negativi | −4, 0, 3 |
| Razionali | ℚ | esprimibili come frazione p/q (q ≠ 0); decimali finiti o periodici | 1.1 = 11/10, 0.42, 1/3 = 0.333… |
| Irrazionali | — | **non** esprimibili come frazione; decimali infiniti non periodici | **√2**, π, e |
| Reali | ℝ | razionali + irrazionali | tutti i precedenti |
| Complessi | ℂ | estensione dei reali con l'unità immaginaria *i* (i² = −1) | 3 + 2i |

ℕ ⊂ ℤ ⊂ ℚ ⊂ ℝ ⊂ ℂ

- "Numeri non reali, sono un'estensione" → si riferisce ai **numeri complessi**, che estendono i reali per poter risolvere equazioni come x² = −1.
- **Numeri computabili**: un numero è *computabile* se esiste un algoritmo (un programma) capace di calcolarne le cifre con qualsiasi precisione. π, e, √2 sono irrazionali **ma computabili** (ci sono algoritmi che ne calcolano quante cifre vogliamo).
- **Numeri non computabili**: nessun programma può calcolarne le cifre. Esempio: la **costante Ω di Chaitin** (la probabilità che un programma scelto a caso termini).

> 💡 **Perché esistono numeri non computabili?** I programmi sono stringhe finite di simboli, quindi sono **numerabili** (si possono mettere in fila: 1°, 2°, 3°…). I numeri reali invece **non sono numerabili** (vedi diagonale di Cantor qui sotto). Quindi ci sono "più" numeri reali che programmi: **quasi tutti i numeri reali sono non computabili**.

### Hotel di Hilbert

Un paradosso di David Hilbert per capire l'infinito. Un hotel ha **infinite stanze** numerate 1, 2, 3, … ed è **completamente pieno**.

1. **Arriva 1 nuovo ospite** → ogni ospite si sposta dalla stanza *n* alla stanza *n + 1*. La stanza 1 si libera.
2. **Arrivano infiniti nuovi ospiti** → ogni ospite si sposta dalla stanza *n* alla stanza *2n*. Si liberano tutte le stanze dispari (infinite).
3. **Arrivano infiniti autobus, ognuno con infiniti ospiti** → si usa la **numerazione per diagonali** (sotto): a ogni coppia (autobus, posto) si assegna una stanza diversa.

Morale: un insieme infinito può essere messo in corrispondenza biunivoca con una sua parte propria (ℕ, i numeri pari e le coppie ℕ×ℕ hanno "la stessa quantità" di elementi).

### Numerazione per diagonali (funzione di accoppiamento di Cantor)

Mettiamo gli ospiti in una tabella: **riga = autobus**, **colonna = posto sull'autobus**. Numeriamo le caselle percorrendo le **diagonali**:

```
            posto 1  posto 2  posto 3  posto 4  ...
autobus 1      1        3        6       10
autobus 2      2        5        9       14
autobus 3      4        8       13
autobus 4      7       12
autobus 5     11
...
```

> ⚠️ **Correzione**: nella prima riga degli appunti c'era "1 3 4 10": il terzo valore è **6**.

- Ogni casella riceve un numero diverso e nessun numero viene saltato → ogni ospite ha una stanza.
- La **prima riga** contiene i **numeri triangolari**: 1, 3, 6, 10, 15, … con formula **Tₙ = n(n+1)/2** (1, 1+2, 1+2+3, 1+2+3+4, …).
- Formula generale della casella (riga *i*, colonna *j*):  **(i + j − 1)(i + j − 2) / 2 + j**
  - Verifica: (2, 2) → 3·2/2 + 2 = **5** ✓
- Lo stesso trucco dimostra che anche i **razionali ℚ sono numerabili** (ogni frazione p/q è una casella della tabella).

### Diagonalizzazione di Cantor (da non confondere con la precedente!)

Dimostra che i **numeri reali tra 0 e 1 NON sono numerabili**:
1. Supponiamo per assurdo di poterli elencare tutti: r₁, r₂, r₃, …
2. Costruiamo un nuovo numero *x* la cui **n-esima cifra è diversa dalla n-esima cifra di rₙ** (si "percorre la diagonale" e si cambia ogni cifra).
3. *x* è diverso da ogni numero della lista (differisce da rₙ almeno nella cifra n) → la lista non era completa → **contraddizione**.

```
r₁ = 0. [5] 1  2  8 ...
r₂ = 0.  4 [3] 9  0 ...
r₃ = 0.  7  7 [1] 4 ...
r₄ = 0.  0  2  6 [8]...
x  = 0.  6  4  2  9 ...   ← ogni cifra cambiata (+1)
```

> 💡 **Collegamento importante**: la stessa tecnica è usata da Turing per dimostrare l'**indecidibilità del problema della fermata** (*halting problem*): non esiste un programma che, dato un qualsiasi programma, decida se questo termina o no.

---

## 8. Sistemi di numerazione

Un **sistema di numerazione** è un modo di rappresentare i numeri tramite un insieme di simboli detti **cifre**, insieme a **regole** per combinarle e rappresentare qualsiasi numero. Nel corso della storia sono state adottate molte notazioni, spesso poco razionali, fino ad arrivare con fatica a quella oggi più diffusa: la **notazione posizionale decimale** (arrivata in Europa dall'India attraverso gli Arabi; diffusa da Fibonacci nel *Liber Abaci*, 1202).

> ⚠️ **Attenzione**: non confondere **numero** (il concetto astratto, la quantità) e **numerale** (la sua rappresentazione). "12", "XII", "1100₂" e "C₁₆" sono numerali diversi dello stesso numero.

### Tipologie

A seconda delle regole usate:
- **Additivi**: il valore del numero è la **somma** dei valori dei simboli; ogni simbolo ha un valore **fisso**, indipendente dalla posizione.
- **Posizionali**: il valore di ogni cifra **dipende dalla posizione** che occupa.

### Sistema attico (greco)
- Sistema **additivo** usato ad Atene (V sec. a.C.). Detto anche *acrofonico*: i simboli sono le iniziali dei nomi dei numeri.
- Simboli: **Ι** = 1, **Π** (*pente*) = 5, **Δ** (*deka*) = 10, **Η** (*hekaton*) = 100, **Χ** (*chilioi*) = 1000, **Μ** (*myrioi*) = 10000; più simboli composti per 50, 500, 5000 (Π con dentro Δ, Η, Χ).
- Grazie ai simboli intermedi "da 5", ogni simbolo si ripete **al massimo 4 volte**.
- Es.: ΗΗΔΔΔΙΙ = 100+100+10+10+10+1+1 = 232

### Sistema egizio
- Sistema **additivo** in base 10: un simbolo (geroglifico) specifico per ogni **potenza di dieci**.
- I multipli si ottengono **ripetendo il simbolo** tante volte quanto serve (**fino a 9 volte**).

| Valore | Geroglifico |
|---|---|
| 1 | bastoncino |
| 10 | archetto (giogo) |
| 100 | corda arrotolata |
| 1 000 | fiore di loto |
| 10 000 | dito |
| 100 000 | girino |
| 1 000 000 | uomo con le braccia alzate (dio Heh) |

- Es.: 2 fiori di loto + 3 corde + 5 bastoncini = 2305. L'ordine dei simboli non conta.

### Sistema romano
- Sistema **additivo-sottrattivo** con un numero limitato di simboli di valore costante:

| I | V | X | L | C | D | M |
|---|---|---|---|---|---|---|
| 1 | 5 | 10 | 50 | 100 | 500 | 1000 |

Regole:
1. Simboli uguali affiancati si **sommano**, ripetuti **al massimo 3 volte** (III = 3, XXX = 30).
2. Un simbolo minore **a destra** di uno maggiore si **somma**: VI = 6, LX = 60.
3. Un simbolo minore **a sinistra** di uno maggiore si **sottrae** (solo I, X, C e solo davanti ai due simboli immediatamente superiori): IV = 4, IX = 9, XL = 40, XC = 90, CD = 400, CM = 900.
4. V, L, D non si ripetono mai.

Es.: **MCMXCIV** = 1000 + 900 + 90 + 4 = **1994**; **MMXXVI** = **2026**.

> ⚠️ **Correzione**: negli appunti la frase "ripetuti per massimo nove volte" è valida per il sistema **egizio**, non per quello romano (max 3) né per quello attico (max 4).

> 💡 **Limiti dei sistemi additivi**: manca lo **zero**, servono sempre nuovi simboli per numeri grandi, e le operazioni (soprattutto moltiplicazione e divisione) sono molto scomode. Per questo hanno lasciato il posto ai sistemi posizionali.

---

## 9. Sistemi di numerazione posizionali

In un sistema posizionale i simboli assumono **valori diversi a seconda della posizione** che occupano. Es.: in 333 il primo 3 vale 300, il secondo 30, il terzo 3.

### Definizione generale
1. Si sceglie un numero naturale **b ≥ 2**, detto **base**.
2. Si scelgono **b simboli diversi**, detti **cifre**, che rappresentano i valori da **0 a b − 1**.
3. Un numero si scrive come sequenza di cifre cₙ₋₁ … c₁ c₀, e il suo valore è:

```
N = cₙ₋₁·bⁿ⁻¹ + … + c₂·b² + c₁·b¹ + c₀·b⁰
```

- La cifra più a destra è la **meno significativa** (LSD/LSB), quella più a sinistra la **più significativa** (MSD/MSB).
- Con *n* cifre in base *b* si rappresentano **bⁿ** valori diversi: da 0 a **bⁿ − 1**.
- Per la **parte frazionaria** si usano esponenti negativi: 0,101₂ = 1·2⁻¹ + 0·2⁻² + 1·2⁻³ = 0,625.
- Notazione: la base si indica in pedice, **1011₂**, **3F₁₆**, oppure con prefissi nei linguaggi di programmazione: `0b1011`, `0o17`, `0x3F`.

Esempio in base 10:  4703 = 4·10³ + 7·10² + 0·10¹ + 3·10⁰

> 💡 Lo **zero** è fondamentale nei sistemi posizionali: serve a indicare che una posizione è "vuota" (in 4703 lo 0 dice che non ci sono decine).

### L'evoluzione della base (perché proprio 10?)
- **Quinario (5)**: le dita di una mano. Problema: servono troppe cifre per rappresentare un numero.
- **Decimale (10)**: le dita di due mani. È quello che usiamo oggi.
- **Duodecimale / dozzinale (12)**: le **falangi** di quattro dita di una mano, contate con il pollice (3 × 4 = 12). Tracce oggi: la *dozzina*, 12 ore, 12 mesi. Vantaggio: 12 è divisibile per 2, 3, 4, 6.
- **Vigesimale (20)**: dita di mani **e** piedi. Usato dai Maya; tracce nel francese *quatre-vingts* (80 = 4 × 20).
- **Sessagesimale (60)**: usato dai **Babilonesi**. Svantaggio: troppi simboli da ricordare. Ma 60 ha moltissimi divisori (2, 3, 4, 5, 6, 10, 12, 15, 20, 30) e lo usiamo ancora per il **tempo** (60 secondi, 60 minuti) e gli **angoli** (360°).

### Sistemi posizionali usati in informatica
Con l'avvento dei calcolatori digitali si usano basi che sono **potenze di 2**:

| Sistema | Base | Cifre | Uso |
|---|---|---|---|
| **Binario** | 2 | 0, 1 | rappresentazione interna di tutti i dati |
| **Ottale** | 8 = 2³ | 0–7 | permessi dei file Unix (`chmod 755`) |
| **Esadecimale** | 16 = 2⁴ | 0–9, A–F | indirizzi di memoria, colori (`#FF8800`), dump di memoria |

### Sistema binario
- Usato per la rappresentazione interna dell'informazione dalla **quasi totalità degli elaboratori elettronici**.
- Perché? Perché è facile costruire dispositivi elettronici con **due stati stabili** e ben distinguibili (passa/non passa corrente, tensione alta/bassa, transistor acceso/spento). Due stati = poco rischio di errore.
- Terminologia: **bit** = una cifra binaria; **nibble** = 4 bit; **byte** = 8 bit; **word** = dipende dall'architettura (oggi 32 o 64 bit).

Potenze di 2 da sapere a memoria:

| 2⁰ | 2¹ | 2² | 2³ | 2⁴ | 2⁵ | 2⁶ | 2⁷ | 2⁸ | 2¹⁰ | 2¹⁶ |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 2 | 4 | 8 | 16 | 32 | 64 | 128 | 256 | 1024 | 65536 |

### Tabella di conversione (da sapere a memoria!)

| Dec | Bin | Ott | Hex | | Dec | Bin | Ott | Hex |
|---|---|---|---|---|---|---|---|---|
| 0 | 0000 | 0 | 0 | | 8 | 1000 | 10 | 8 |
| 1 | 0001 | 1 | 1 | | 9 | 1001 | 11 | 9 |
| 2 | 0010 | 2 | 2 | | 10 | 1010 | 12 | **A** |
| 3 | 0011 | 3 | 3 | | 11 | 1011 | 13 | **B** |
| 4 | 0100 | 4 | 4 | | 12 | 1100 | 14 | **C** |
| 5 | 0101 | 5 | 5 | | 13 | 1101 | 15 | **D** |
| 6 | 0110 | 6 | 6 | | 14 | 1110 | 16 | **E** |
| 7 | 0111 | 7 | 7 | | 15 | 1111 | 17 | **F** |

---

## 10. Conversioni tra basi

### Base qualsiasi → Decimale
Si applica la **definizione**: si moltiplica ogni cifra per la base elevata alla sua posizione e si somma.

```
101101₂ = 1·2⁵ + 0·2⁴ + 1·2³ + 1·2² + 0·2¹ + 1·2⁰
        =  32  +  0   +  8   +  4   +  0   +  1   = 45₁₀

5B₁₆    = 5·16¹ + 11·16⁰ = 80 + 11 = 91₁₀
```

### Decimale → Binario (divisioni successive)
Procedura iterativa in tre passi:
1. Si divide il numero per 2, calcolando **quoziente** e **resto**.
2. Se il quoziente è diverso da zero, si ripete il passo 1 usando il quoziente, finché non si ottiene 0.
3. Si scrivono i **resti in ordine inverso** rispetto a come sono stati calcolati (l'ultimo resto è la cifra più significativa).

Esempio: **156₁₀**

```
156 : 2 = 78   resto 0   ↑ (LSB)
 78 : 2 = 39   resto 0   │
 39 : 2 = 19   resto 1   │
 19 : 2 =  9   resto 1   │  leggere
  9 : 2 =  4   resto 1   │  dal basso
  4 : 2 =  2   resto 0   │  verso l'alto
  2 : 2 =  1   resto 0   │
  1 : 2 =  0   resto 1   │ (MSB)

156₁₀ = 10011100₂
```
Verifica: 128 + 16 + 8 + 4 = 156 ✓

> 💡 **Metodo alternativo (sottrazione di potenze)**: si sottrae la potenza di 2 più grande possibile e si mette 1 in quella posizione. 156 − 128 = 28 → 28 − 16 = 12 → 12 − 8 = 4 → 4 − 4 = 0. Posizioni 7, 4, 3, 2 → 10011100₂. Spesso è più veloce a mente.

### Decimale → Esadecimale (o qualsiasi base b)
**Stessa procedura**, ma dividendo per **16** (o per *b*). I resti da 10 a 15 si scrivono A–F.

```
156 : 16 = 9   resto 12 → C
  9 : 16 = 0   resto 9  → 9

156₁₀ = 9C₁₆
```

### Decimale → Binario: parte frazionaria (moltiplicazioni successive)
Si moltiplica la parte frazionaria per 2: la parte intera del risultato (0 o 1) è la cifra successiva; si continua con la nuova parte frazionaria finché diventa 0 (o si raggiunge la precisione voluta). Le cifre si leggono **dall'alto verso il basso**.

```
0,625 · 2 = 1,25  → 1
0,25  · 2 = 0,5   → 0
0,5   · 2 = 1,0   → 1      0,625₁₀ = 0,101₂
```

> 💡 **Attenzione**: alcuni numeri decimali "semplici" diventano **periodici** in binario: 0,1₁₀ = 0,0001100110011…₂. Per questo in quasi tutti i linguaggi `0.1 + 0.2 != 0.3`!

### Conversione tra basi potenze dello stesso numero
Se le due basi sono **potenze dello stesso numero** (es. 2, 8 = 2³, 16 = 2⁴) **non serve passare dal decimale**: ogni cifra della base maggiore corrisponde a un gruppo fisso di cifre della base minore.

Per Binario → Esadecimale ci sono quindi due possibili strategie:
- convertire da binario a decimale e poi da decimale a esadecimale (lento);
- **raggruppare i bit a 4 a 4** (veloce, sotto).

### Binario → Esadecimale
Dato che 16 = 2⁴, ogni cifra esadecimale corrisponde esattamente a **4 bit**:
1. Suddividere il numero binario in **gruppi di 4 cifre**, procedendo **da destra verso sinistra**.
2. Se l'ultimo gruppo a sinistra ha meno di 4 cifre, **aggiungere zeri a sinistra** (non cambiano il valore).
3. Sostituire ogni gruppo con la cifra esadecimale corrispondente (tabella).

```
1011011₂  →  101 1011  →  0101 1011  →  5 B  →  5B₁₆
```

### Esadecimale → Binario
1. Separare le cifre del numero in base 16.
2. Sostituire ogni cifra con il corrispondente gruppo di **4 bit** (tabella).
3. Concatenare i gruppi ed eventualmente eliminare gli zeri iniziali.

```
3F2₁₆  →  3    F    2   →  0011 1111 0010  →  1111110010₂
```

### Binario ↔ Ottale
Stessa idea con **gruppi di 3 bit** (8 = 2³):
```
1011011₂  →  1 011 011  →  001 011 011  →  1 3 3  →  133₈
```

---

## 11. Operazioni aritmetiche nei sistemi posizionali

Le operazioni si eseguono **esattamente come in base 10** (in colonna, con riporti e prestiti), ricordando che il **riporto scatta quando si raggiunge la base** (2 in binario, 16 in esadecimale) invece che 10.

### Somma binaria

Tabella:

| A | B | Somma | Riporto |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | **1** |
| 1 | 1 (+1 riporto) | 1 | **1** |

Esempio: 45 + 27 = 72
```
 riporti  1 1 1 1 1 1
            1 0 1 1 0 1     (45)
        +     1 1 0 1 1     (27)
        -----------------
          1 0 0 1 0 0 0     (72)
```

### Somma esadecimale
Se la somma di una colonna è **≥ 16**, si scrive (somma − 16) e si riporta 1.

Esempio: 3A7₁₆ + 1F9₁₆
```
 riporti   1 1
           3 A 7
         + 1 F 9
         -------
           5 A 0

colonna 0:  7 + 9       = 16 → scrivo 0, riporto 1
colonna 1:  A + F + 1   = 10 + 15 + 1 = 26 → 26 − 16 = 10 = A, riporto 1
colonna 2:  3 + 1 + 1   = 5
```
Verifica: 935 + 505 = 1440 = 5A0₁₆ ✓

> 💡 **Trucco**: converti le lettere in decimale, somma, e se superi 15 togli 16 e riporta 1.

### Overflow aritmetico
I calcolatori lavorano con un **numero fisso di bit** (8, 16, 32, 64). Con *n* bit senza segno si rappresentano i numeri da **0 a 2ⁿ − 1**.
Si ha **overflow** quando il risultato di un'operazione **non è rappresentabile** con i bit a disposizione: c'è un riporto oltre il bit più significativo, che viene perso.

```
Su 4 bit (max 15):
      1011   (11)
    + 0110   ( 6)
    ------
   1 0001    → il riporto "1" non entra nei 4 bit
             → risultato memorizzato: 0001 = 1  ✗ (doveva essere 17)
```

Esempio a 8 bit: FF₁₆ + 01₁₆ = 100₁₆ → su 8 bit resta **00**. È come il contachilometri di un'auto che torna a zero.

> 💡 Bug reali causati dall'overflow: il razzo **Ariane 5** (1996, conversione da 64 a 16 bit), il **"Gangnam Style"** che superò il contatore di visualizzazioni a 32 bit di YouTube, il **problema dell'anno 2038** (timestamp Unix a 32 bit).

### Sottrazione binaria
Tabella: 0−0 = 0; 1−0 = 1; 1−1 = 0; **0−1 = 1 con prestito** di 1 dalla colonna a sinistra.

```
     1100   (12)
   − 0101   ( 5)
   ------
     0111   ( 7)
```

In pratica, i calcolatori **non fanno sottrazioni**: calcolano A − B come **A + (−B)**, usando il complemento a 2 (sotto). Così basta un solo circuito sommatore.

### Complemento (rappresentazione dei numeri negativi)

**Complemento a 1**: si **invertono tutti i bit** (0 → 1, 1 → 0).
- Problema: esistono due zeri (+0 = 0000, −0 = 1111).

**Complemento a 2** (quello usato da tutti i computer moderni):
1. si invertono tutti i bit (complemento a 1);
2. si **somma 1**.

Esempio: −6 su 8 bit
```
 +6  = 0000 0110
 inv = 1111 1001
 +1  = 1111 1010   ← −6 in complemento a 2
```
Scorciatoia: partendo da destra, si copiano i bit fino al primo **1** compreso, poi si invertono tutti gli altri.

Proprietà:
- Il bit più significativo indica il **segno** (0 = positivo, 1 = negativo).
- Con *n* bit si rappresentano i numeri da **−2ⁿ⁻¹ a 2ⁿ⁻¹ − 1** (8 bit: da −128 a +127).
- **Un solo zero**.
- La sottrazione diventa una somma: 12 − 5 su 4 bit:

```
  12  =   1100
  −5  =   1011     (5 = 0101 → inv 1010 → +1 → 1011)
         ------
        1 0111     → si scarta il riporto finale → 0111 = 7 ✓
```

- **Overflow con segno**: si verifica quando si sommano due numeri **dello stesso segno** e il risultato ha **segno opposto**. Es. su 4 bit: 0111 (7) + 0001 (1) = 1000 = **−8** ✗.

> 💡 Il concetto vale in ogni base: il **complemento alla base** (in decimale, *complemento a 10*) e il **complemento alla base meno uno** (*complemento a 9*). Es. complemento a 9 di 347 su 3 cifre = 999 − 347 = 652.

### Moltiplicazione binaria
La tabellina binaria è banale: **0·0 = 0, 0·1 = 0, 1·0 = 0, 1·1 = 1**. Si procede come in decimale: ogni prodotto parziale è **o zero o una copia del moltiplicando spostata** a sinistra; poi si sommano.

Esempio: 11 × 5 = 55
```
          1 0 1 1    (11)
        ×   1 0 1    ( 5)
        ---------
          1 0 1 1
        0 0 0 0 ·
    + 1 0 1 1 · ·
    -------------
      1 1 0 1 1 1    (55)
```

> 💡 **Shift**: moltiplicare per 2 in binario = **spostare tutti i bit di una posizione a sinistra** (aggiungere uno 0 a destra), esattamente come moltiplicare per 10 in decimale. Dividere per 2 = spostare a destra. I processori usano questi *shift* perché sono velocissimi (in C: `x << 1`, `x >> 1`).

### Moltiplicazione esadecimale
Come in decimale: si moltiplica cifra per cifra, convertendo il risultato in base 16 (risultato = 16 · riporto + cifra).

Esempio semplice: 2A₁₆ × 3
```
A × 3     = 30 = 1·16 + 14 → scrivo E, riporto 1
2 × 3 + 1 = 7               → scrivo 7
2A₁₆ × 3  = 7E₁₆            (42 × 3 = 126 ✓)
```

Esempio a due cifre: 1B₁₆ × 2C₁₆
```
          1 B
        × 2 C
        -----
        1 4 4      ← 1B × C:  B·C = 11·12 = 132 = 8·16 + 4 → 4, rip. 8
                              1·C + 8 = 20 = 1·16 + 4  → 14
      + 3 6 ·      ← 1B × 2:  B·2 = 22 = 1·16 + 6 → 6, rip. 1
                              1·2 + 1 = 3
        -----
        4 A 4
```
Verifica: 27 × 44 = 1188 = 4A4₁₆ ✓

### Divisione binaria (cenno)
Si esegue come la divisione in colonna decimale, ma a ogni passo il quoziente può essere solo 0 o 1 (il divisore "ci sta" oppure no).
Es.: 110111₂ : 101₂ = 1011₂ (55 : 5 = 11).

---

## 12. 📝 Esercizi di riepilogo

1. Converti **200₁₀** in binario e in esadecimale.
2. Converti **2F₁₆** in decimale e in binario.
3. Converti **11101011₂** in esadecimale e in decimale.
4. Calcola **1101₂ + 0111₂**. C'è overflow su 4 bit?
5. Calcola **A5₁₆ + 6C₁₆**. Cosa succede su 8 bit?
6. Calcola **110₂ × 101₂**.
7. Rappresenta **−6** in complemento a 2 su 8 bit.
8. Converti **MCMLXXXIV** in numeri arabi.
9. Nella tabella di Cantor, che numero ha la casella (riga 3, colonna 3)?

<details>
<summary><b>Soluzioni</b></summary>

1. 200₁₀ = **11001000₂** = **C8₁₆**
2. 2F₁₆ = 2·16 + 15 = **47₁₀** = **101111₂**
3. 1110 1011 → **EB₁₆** = 14·16 + 11 = **235₁₀**
4. 1101 + 0111 = **10100₂** (13 + 7 = 20). Sì, overflow su 4 bit: resta 0100 = 4.
5. A5 + 6C = **111₁₆** (165 + 108 = 273). Su 8 bit overflow: resta **11₁₆** = 17.
6. 110 × 101 = **11110₂** (6 × 5 = 30)
7. 6 = 00000110 → 11111001 → **11111010**
8. M + CM + LXXX + IV = 1000 + 900 + 80 + 4 = **1984**
9. (3+3−1)(3+3−2)/2 + 3 = 5·4/2 + 3 = **13**

</details>

---

## 13. 💡 Argomenti correlati da approfondire

Argomenti che probabilmente verranno ripresi a breve, o che è utile conoscere per collegare i concetti di questa lezione:

1. **Multipli del byte**: attenzione a **kB = 1000 byte** (SI) vs **KiB = 1024 byte** (binario). Allo stesso modo MB/MiB, GB/GiB, TB/TiB. È il motivo per cui un disco "da 1 TB" appare come ~931 GiB.
2. **Rappresentazione in virgola mobile (IEEE 754)**: come vengono memorizzati i numeri reali (segno, esponente, mantissa); perché `0.1 + 0.2 ≠ 0.3`.
3. **Rappresentazione in modulo e segno** e **eccesso-k (bias)**: altre codifiche dei numeri negativi, da confrontare con il complemento a 2.
4. **Codifica BCD** (*Binary Coded Decimal*): ogni cifra decimale codificata con 4 bit.
5. **Codifica dei caratteri**: **ASCII** (7 bit, 128 caratteri), ASCII esteso, **Unicode** e **UTF-8**.
6. **Algebra di Boole e porte logiche** (AND, OR, NOT, XOR, NAND): il **sommatore binario** (half adder / full adder) si costruisce proprio con XOR e AND, e realizza la tabella della somma vista sopra.
7. **Operatori bit a bit** nei linguaggi (`&`, `|`, `^`, `~`, `<<`, `>>`) e uso delle **maschere di bit**.
8. **Endianness** (*big-endian* vs *little-endian*): in che ordine vengono memorizzati i byte di un numero in memoria.
9. **Macchina di Turing**, **tesi di Church-Turing** e **problema della fermata**: le basi teoriche di "cosa è calcolabile" (collegamento con Chomsky, diagonalizzazione e numeri non computabili).
10. **Architettura di Von Neumann vs Harvard** e **ciclo fetch-decode-execute**.
11. **Gerarchia di memoria** (registri → cache → RAM → disco): collegata al discorso CPU vs GPU.
12. **Pipeline e branch prediction**: per capire a fondo perché i salti sono costosi.

---

> **Consiglio di studio**: le conversioni e le operazioni in base 2 e 16 si imparano solo **facendo esercizi**. Verifica i tuoi risultati con la calcolatrice del sistema (modalità "Programmatore") oppure in Python: `bin(156)`, `hex(156)`, `int('10011100', 2)`, `int('9C', 16)`.
