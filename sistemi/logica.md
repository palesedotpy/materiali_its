# Rappresentazione dei caratteri

Il calcolatore lavora solo con numeri binari: ogni carattere viene quindi rappresentato come un **numero intero**, che il calcolatore poi interpreta e mostra come carattere grazie a una **tabella di codifica** (es. `65` → `A`).

- Inizialmente si usavano sistemi di codifica a 7 o 8 bit.
- Oggi si usano codifiche con **più di 8 bit**, per poter rappresentare gli alfabeti di tutto il mondo.

## Codifica ASCII

*American Standard Code for Information Interchange.*

- Ogni carattere è codificato come un numero a **7 bit** → 2⁷ = **128 caratteri** (da 0 a 127).
- Spesso memorizzato in 8 bit (1 byte): l'ottavo bit veniva usato come bit di parità o per estensioni ("ASCII esteso").
- Tra i 128 caratteri ci sono:
  - lettere maiuscole (`A`=65 … `Z`=90) e minuscole (`a`=97 … `z`=122)
  - cifre (`0`=48 … `9`=57)
  - simboli di punteggiatura (`!`, `?`, `@`, …)
  - **caratteri di controllo** non stampabili (0–31 e 127: es. a capo, tabulazione)

> Limite: contiene solo i caratteri dell'inglese, niente lettere accentate (`è`, `à`, …).

## Codifica ISO-8859-1 (Latin-1)

- Codifica a **8 bit** → 2⁸ = **256 caratteri**.
- I primi 128 caratteri sono **identici all'ASCII** (compatibilità).
- I restanti 128 aggiungono lettere accentate e simboli delle lingue dell'Europa occidentale (`à`, `é`, `ñ`, `ü`, `ç`, …).

### Problemi di ISO-8859-1

- 256 caratteri non bastano per tutte le lingue (greco, cirillico, arabo, cinese, …).
- Sono nate tante varianti (ISO-8859-2, -5, -7, -15, …), ognuna per un gruppo di lingue: **lo stesso numero indica caratteri diversi** a seconda della variante → testi illeggibili se si usa la codifica sbagliata.
- Mancano alcuni simboli, ad esempio l'euro `€` (aggiunto poi in ISO-8859-15).

## Codifica Unicode

- Sistema di codifica a **32 bit**, di cui solo **21 informativi**.
- Permette di codificare **oltre un milione di caratteri** (codici da `U+0000` a `U+10FFFF`): tutti gli alfabeti, simboli matematici, emoji, …
- I primi 128 codici coincidono con l'ASCII.
- Esistono diverse "sotto-codifiche" (formati di codifica) che usano **meno bit** per i caratteri più comuni:

| Codifica | Dimensione per carattere | Note |
|----------|--------------------------|------|
| UTF-8    | da 1 a 4 byte (variabile) | Compatibile con ASCII, la più usata sul web |
| UTF-16   | 2 o 4 byte               | Usata internamente da Windows, Java |
| UTF-32   | 4 byte fissi             | Semplice ma spreca spazio |

---

# Algebra booleana

## Valori

L'algebra booleana è un tipo di algebra **binaria**: possono esistere solo due valori, **{Falso, Vero}**, rappresentati anche come **{0, 1}**.

Per questo motivo:
- è utilizzata in tutti i **circuiti logici** di base del computer (corrente assente/presente);
- è implementata in tutti i **linguaggi di programmazione** per rappresentare condizioni e decisioni (`if`, `while`, …).

## Definizioni

**Proposizione logica**: un'affermazione alla quale può essere assegnato un valore booleano.
Es. *"sta piovendo"*, *"Marco è più alto di Francesca"*.
(Non sono proposizioni le domande o gli ordini: *"che ore sono?"*, *"chiudi la porta"*.)

**Interpretazione di una proposizione**: assegnare un valore booleano a una proposizione.
Es. la proposizione *"sta piovendo"* sarà **Vera** se sta effettivamente piovendo, **Falsa** altrimenti.

## Il problema di Monty Hall

Esempio classico di come l'intuito possa ingannare nel ragionamento logico/probabilistico.

- Ci sono **3 porte**: dietro una c'è un'auto, dietro le altre due una capra.
- Il concorrente sceglie una porta.
- Il conduttore, che **sa** dove si trova l'auto, apre una delle altre due porte mostrando una capra.
- Il concorrente può **tenere** la sua porta o **cambiare**.

**Conviene cambiare**:
- tenendo la porta si vince con probabilità **1/3** (la probabilità della scelta iniziale);
- cambiando si vince con probabilità **2/3**: se la prima scelta era sbagliata (2 casi su 3), cambiando si trova sicuramente l'auto.

## Variabili booleane

Una **variabile booleana** è una variabile che può assumere solo i valori **0 (Falso)** o **1 (Vero)**.
Si indica di solito con una lettera maiuscola (`A`, `B`, `C`, …) e rappresenta una proposizione.

Es. `A` = "sta piovendo", `B` = "ho l'ombrello".

## Operatori logici

L'algebra booleana permette di definire facilmente espressioni logiche anche molto complesse tramite formule contenenti **variabili booleane** e **operatori logici**.

Operatori logici fondamentali:

| Operatore | Simbolo algebra | Programmazione (C/Java/JS) | Python |
|-----------|-----------------|----------------------------|--------|
| AND       | `A · B` (o `AB`) | `A && B`                  | `A and B` |
| OR        | `A + B`          | `A \|\| B`                | `A or B` |
| NOT       | `¬A` (o `Ā`)     | `!A`                      | `not A` |

**Precedenza**: `NOT` → `AND` → `OR` (come in matematica: il prodotto prima della somma). Le parentesi cambiano l'ordine.

### AND

- Operatore **binario** (lavora su due operandi).
- Detto anche **prodotto logico**.
- Il risultato è vero **solo se entrambe** le variabili sono vere.

| A | B | A · B |
|---|---|-------|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | **1** |

**Esempio**: "esco **se** non piove **e** ho finito i compiti" → esco solo se entrambe le condizioni sono vere.

### OR

- Operatore **binario**.
- Detto anche **somma logica**.
- Il risultato è vero se **almeno una** variabile è vera.

| A | B | A + B |
|---|---|-------|
| 0 | 0 | 0 |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | **1** |

### NOT

- Operatore **unario** (lavora su un solo operando).
- Detto anche **invertitore** o **complemento**.
- Inverte il valore: vero diventa falso e viceversa.

| A | ¬A |
|---|----|
| 0 | 1 |
| 1 | 0 |

### XOR (OR esclusivo)

- Operatore **binario**, simbolo `A ⊕ B`.
- Detto anche **somma modulo 2**: il risultato è vero se il **numero di variabili vere è dispari** (con due variabili: se sono diverse).
- Si può esprimere con gli operatori fondamentali: `A ⊕ B = ¬A·B + A·¬B`.

| A | B | A ⊕ B |
|---|---|-------|
| 0 | 0 | 0 |
| 0 | 1 | **1** |
| 1 | 0 | **1** |
| 1 | 1 | 0 |

## Tabelle di verità

Una **tabella di verità** elenca il valore di una funzione booleana per **tutte le combinazioni** possibili delle variabili.
Con *n* variabili ci sono **2ⁿ righe** (2 variabili → 4 righe, 3 variabili → 8 righe).

**Esempio**: `F = ¬A + ¬C·B`
(in programmazione: `!A || !C && B` — l'AND viene valutato prima dell'OR)

| A | B | C | ¬A | ¬C·B | F |
|---|---|---|----|------|---|
| 0 | 0 | 0 | 1 | 0 | **1** |
| 0 | 0 | 1 | 1 | 0 | **1** |
| 0 | 1 | 0 | 1 | 1 | **1** |
| 0 | 1 | 1 | 1 | 0 | **1** |
| 1 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 | 0 | 0 |
| 1 | 1 | 0 | 0 | 1 | **1** |
| 1 | 1 | 1 | 0 | 0 | 0 |

Es. riga `A=1, B=0, C=0`: `0 or (1 and 0)` = `0 or 0` = **0**.

## Dalla tabella di verità alla formula booleana (sintesi)

Data la tabella di verità di una funzione è possibile ricavarne la formula booleana (**somma di prodotti**):

1. Si considerano solo le righe in cui la funzione vale **1**.
2. Per ogni riga si scrive un **prodotto (AND)** di tutte le variabili: la variabile va scritta **normale** se vale 1, **negata** se vale 0.
3. Si **sommano (OR)** tutti i prodotti ottenuti.

**Esempio**:

| A | B | F |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 1 → `¬A·B` |
| 1 | 0 | 1 → `A·¬B` |
| 1 | 1 | 0 |

`F = ¬A·B + A·¬B` (cioè lo XOR).

## Proprietà dell'algebra booleana

| Proprietà | Forma AND | Forma OR |
|-----------|-----------|----------|
| Identità | `A · 1 = A` | `A + 0 = A` |
| Elemento nullo | `A · 0 = 0` | `A + 1 = 1` |
| Idempotenza | `A · A = A` | `A + A = A` |
| Complemento | `A · ¬A = 0` | `A + ¬A = 1` |
| Doppia negazione | `¬¬A = A` | |
| Commutativa | `A · B = B · A` | `A + B = B + A` |
| Associativa | `(A·B)·C = A·(B·C)` | `(A+B)+C = A+(B+C)` |
| Distributiva | `A·(B + C) = A·B + A·C` | `A + B·C = (A+B)·(A+C)` |
| Assorbimento | `A · (A + B) = A` | `A + A·B = A` |
| De Morgan | `¬(A · B) = ¬A + ¬B` | `¬(A + B) = ¬A · ¬B` |

## Sintesi di una formula: semplificazione

Usando le proprietà dell'algebra booleana è possibile **semplificare** le formule delle funzioni (meno operatori = circuito più semplice ed economico).

Si prenda ad esempio la formula ottenuta nell'esercizio di sintesi precedente:

`f = A·B·¬C·D + A·B·C·¬D + A·B·C·D`

1. **Idempotenza** (`X = X + X`): il termine `ABCD` serve due volte, quindi lo duplico:
   `f = AB¬CD + ABC¬D + ABCD + ABCD`
2. **Distributiva**: metto in evidenza `ABD` tra il primo e un `ABCD`:
   `AB¬CD + ABCD = ABD(¬C + C)`
3. **Distributiva**: metto in evidenza `ABC` tra il secondo e l'altro `ABCD`:
   `ABC¬D + ABCD = ABC(¬D + D)`
4. **Complemento** (`¬X + X = 1`) e **identità** (`X · 1 = X`):
   `f = ABD · 1 + ABC · 1 = ABD + ABC`
5. **Distributiva**: metto in evidenza `AB`:

   **`f = A·B·(C + D)`**

Da 3 termini con 4 variabili ciascuno si arriva a una formula con 2 AND e 1 OR.
