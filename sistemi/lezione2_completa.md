# Sistemi — Lezione 2 (02/11/2026)

> **Legenda**
> - ⚠️ **Correzione**: punto degli appunti originali che conteneva un errore o un'imprecisione.
> - 💡 **Approfondimento**: materiale aggiunto, utile da sapere anche se forse non era nelle slide.
>
> Tutti gli esempi sono su **8 bit**, salvo dove indicato diversamente.

---

## 1. Numeri binari con segno

Nella lezione 1 abbiamo visto i numeri binari **senza segno** (*unsigned*): con *n* bit si rappresentano i valori da 0 a 2ⁿ − 1.
Per rappresentare anche i **numeri negativi** (numeri *relativi*, ℤ) bisogna "spendere" parte dei bit per il segno. Esistono tre codifiche principali:

1. **Modulo e segno**
2. **Complemento a 1**
3. **Complemento a 2** (quella usata da tutti i calcolatori moderni)

In tutte e tre il **bit più significativo (MSB)** indica il segno: **0 = positivo**, **1 = negativo**. I numeri **positivi si scrivono allo stesso modo** in tutte e tre le codifiche; cambia solo il modo di scrivere i negativi.

| Decimale | Modulo e segno | Complemento a 1 | Complemento a 2 |
|---|---|---|---|
| +5 | 0000 0101 | 0000 0101 | 0000 0101 |
| −5 | **1**000 0101 | 1111 1010 | 1111 1011 |
| +0 | 0000 0000 | 0000 0000 | 0000 0000 |
| −0 | 1000 0000 | 1111 1111 | — (non esiste) |

---

## 2. Modulo e segno

- Il primo bit è il **segno**, gli altri *n − 1* bit sono il **modulo** (il valore assoluto), scritto normalmente in binario.
- Es.: −22 → segno 1, modulo 22 = 001 0110 → **1001 0110**.
- ✅ Molto intuitiva: è come scriviamo i numeri a mano (+22, −22).
- ❌ **Due rappresentazioni dello zero**: +0 = 0000 0000 e −0 = 1000 0000.
- ❌ Le operazioni sono **complicate**: il circuito deve guardare i segni e confrontare i moduli prima di decidere cosa fare.

### Regole per la somma in modulo e segno

| Segni | Cosa si fa | Segno del risultato |
|---|---|---|
| **Uguali** (+ + oppure − −) | si **sommano i moduli** | lo stesso segno degli addendi |
| **Diversi** (+ − oppure − +) | si **sottrae il modulo minore dal maggiore** | il segno dell'addendo con **modulo maggiore** |

Esempio: (+9) + (−21)
```
segni diversi → |21| − |9| = 12, segno di 21 (−)
21 = 001 0101
 9 = 000 1001  −
     --------
     000 1100  (12)    →  risultato: 1000 1100 = −12
```

---

## 3. Complemento a 1

- I positivi si scrivono normalmente.
- Un negativo −X si ottiene **invertendo tutti i bit** di +X (0 → 1, 1 → 0).
- Es.: +22 = 0001 0110 → −22 = **1110 1001**.
- ✅ La sottrazione si fa con una somma (vedi sotto).
- ❌ Ancora **due zeri**: +0 = 0000 0000 e −0 = 1111 1111.
- ❌ Nella somma serve il **riporto circolare** (*end-around carry*), vedi sotto.

### Negazione in complemento a 1
Per cambiare segno a un numero (da +X a −X **o viceversa**) basta **invertire tutti i bit**.
```
 +35 = 0010 0011
 −35 = 1101 1100
```

### Leggere un numero negativo in complemento a 1
Se l'MSB è 1, il numero è negativo: si **invertono i bit** per trovare il modulo.
```
1101 1100  →  inverto  →  0010 0011 = 35   →  il numero è −35
```

### Somma di numeri relativi in complemento a 1

Regola:
1. Si sommano i due numeri **normalmente**, bit per bit, **compreso il bit di segno**.
2. Se c'è un **riporto oltre l'MSB** (il 9° bit), **non si butta**: si **somma al risultato** (*riporto circolare*, *end-around carry*).

#### Esempio 1 — (−35) + 17 (nessun riporto finale)
```
   1101 1100   (−35)
 + 0001 0001   (+17)
 -----------
   1110 1101   → MSB = 1, negativo → inverto: 0001 0010 = 18  →  −18 ✓
```

> ⚠️ **Correzione**: negli appunti questa operazione era scritta con il segno "**−**", ma il calcolo fatto (e il risultato 1110 1101) corrisponde a una **somma**: −35 + 17 = −18.

#### Esempio 2 — 28 − 94 = 28 + (−94)
```
 +28 = 0001 1100
 +94 = 0101 1110  →  −94 = 1010 0001   (inverto i bit)

   0001 1100   (+28)
 + 1010 0001   (−94)
 -----------
   1011 1101   → negativo → inverto: 0100 0010 = 66  →  −66 ✓
```

#### Esempio 3 — (−9) − 21 = (−9) + (−21) (con riporto circolare)
```
 +9  = 0000 1001  →  −9  = 1111 0110
 +21 = 0001 0101  →  −21 = 1110 1010

     1111 0110   (−9)
   + 1110 1010   (−21)
   -----------
   1 1110 0000   ← c'è un riporto oltre l'8° bit
   +         1   ← lo risommo (riporto circolare)
   -----------
     1110 0001   → negativo → inverto: 0001 1110 = 30  →  −30 ✓
```

> ⚠️ **Correzione**: negli appunti c'era la scorciatoia "sommo i moduli 9 + 21 e poi complemento". Va bene come verifica, ma la somma 1001 + 10101 fa **11110** (= 30), non 11100 (= 28). Il risultato finale 1110 0001 = −30 negli appunti è comunque corretto.

#### Esempio 4 — (−7) + 10 (con riporto circolare)
```
 +7 = 0000 0111  →  −7 = 1111 1000

     1111 1000   (−7)
   + 0000 1010   (+10)
   -----------
   1 0000 0010   ← riporto oltre l'8° bit
   +         1   ← riporto circolare
   -----------
     0000 0011   = +3 ✓
```

#### Esempio 5 — 5 − 9 = 5 + (−9)
```
 +9 = 0000 1001  →  −9 = 1111 0110

   0000 0101   (+5)
 + 1111 0110   (−9)
 -----------
   1111 1011   → negativo → inverto: 0000 0100 = 4  →  −4 ✓
```

### Il problema del complemento a 1
Il complemento a 1 ha due difetti:
1. **Doppio zero** (0000 0000 e 1111 1111): spreca una combinazione e complica i confronti (il circuito deve sapere che sono "uguali").
2. **Riporto circolare**: a volte bisogna fare **una seconda somma** per aggiungere il riporto → circuito più lento.

La soluzione è il **complemento a 2**.

---

## 4. Complemento a 2

- I positivi si scrivono normalmente.
- Un negativo −X si ottiene così: **complemento a 1 di +X, poi si somma 1**.
- ✅ **Un solo zero**.
- ✅ Nella somma il riporto oltre l'MSB **si scarta e basta** (niente riporto circolare).
- ✅ Somma e sottrazione usano **lo stesso circuito sommatore** degli unsigned.

### Negazione in complemento a 2
Vale in entrambe le direzioni (+X → −X e −X → +X): **inverto tutti i bit e sommo 1**.

Esempio: −22
```
 +22 = 0001 0110
 inv = 1110 1001   (complemento a 1)
  +1 = 1110 1010   ← −22 in complemento a 2
```

> ⚠️ **Nota sugli appunti**: negli appunti c'era "−22: 0001 0101 → 1110 1010". Il risultato **1110 1010 è corretto per −22 in complemento a 2**. Il passaggio intermedio 0001 0101 (= 21) si spiega con un metodo alternativo equivalente: **−X = inverti(X − 1)** → 22 − 1 = 21 = 0001 0101 → inverto → 1110 1010. Attenzione però: 1110 1010 **in complemento a 1** varrebbe −21, non −22!

💡 **Scorciatoia**: partendo da destra si copiano i bit **fino al primo 1 compreso**, poi si invertono tutti gli altri.
```
+22 = 0001 0|110      → copio "110", inverto il resto
−22 = 1110 1|010
```

### Leggere un numero negativo in complemento a 2
- Metodo 1: si rifà la negazione (inverto + 1): 1110 1010 → 0001 0101 + 1 = 0001 0110 = 22 → **−22**.
- 💡 Metodo 2: l'MSB vale **−2ⁿ⁻¹** invece di +2ⁿ⁻¹:
  1110 1010 = **−128** + 64 + 32 + 8 + 2 = **−22** ✓

---

## 5. Intervalli di rappresentazione dei numeri relativi binari

Con **n bit**:

| Codifica | Minimo | Massimo | Zeri | Con 8 bit | Con 16 bit |
|---|---|---|---|---|---|
| Senza segno | 0 | 2ⁿ − 1 | 1 | 0 … 255 | 0 … 65 535 |
| Modulo e segno | −(2ⁿ⁻¹ − 1) | 2ⁿ⁻¹ − 1 | **2** | −127 … +127 | −32 767 … +32 767 |
| Complemento a 1 | −(2ⁿ⁻¹ − 1) | 2ⁿ⁻¹ − 1 | **2** | −127 … +127 | −32 767 … +32 767 |
| Complemento a 2 | **−2ⁿ⁻¹** | 2ⁿ⁻¹ − 1 | **1** | **−128** … +127 | −32 768 … +32 767 |

- In tutti i casi le combinazioni sono **2ⁿ** (256 con 8 bit).
- In modulo e segno e complemento a 1 una combinazione è "sprecata" per il secondo zero → l'intervallo è **simmetrico**.
- In complemento a 2 quella combinazione viene usata per un negativo in più (1000 0000 = −128) → l'intervallo è **asimmetrico**: c'è un negativo in più dei positivi.

> 💡 Curiosità: in complemento a 2 il negato di −128 su 8 bit è… di nuovo −128 (1000 0000 → 0111 1111 + 1 = 1000 0000), perché +128 non è rappresentabile. È un caso classico di overflow (in C, `-INT_MIN` è *undefined behavior*).

---

## 6. Il problema della scelta del numero di bit

Un calcolatore lavora sempre con un **numero fisso di bit** (8, 16, 32, 64). Prima di rappresentare un dato bisogna quindi scegliere quanti bit usare:

- **Troppo pochi bit** → i valori non entrano nell'intervallo → **overflow** (risultati sbagliati).
- **Troppi bit** → spreco di memoria e operazioni più lente.

Per i numeri interi la regola è: con *n* bit in complemento a 2 servono **−2ⁿ⁻¹ ≤ valore ≤ 2ⁿ⁻¹ − 1**.
Es.: per rappresentare temperature da −50 a +150 basta **1 byte**? No: 150 > 127 → servono almeno **9 bit** (in pratica si usa un intero a 16 bit).

Il problema diventa ancora più evidente con i **numeri con la virgola** (sezione 11): bisogna decidere quanti bit dare alla parte intera e quanti alla parte frazionaria.

---

## 7. Sottrazione binaria

### Caso generale (numeri senza segno)

Tabella della sottrazione bit a bit:

| A | B | A − B | Prestito |
|---|---|---|---|
| 0 | 0 | 0 | 0 |
| 1 | 0 | 1 | 0 |
| 1 | 1 | 0 | 0 |
| 0 | 1 | **1** | **1** (si prende in prestito 1 dalla colonna a sinistra) |

> ⚠️ **Correzione**: negli appunti il caso 3 (0 − 1) era rimasto in sospeso e mancava il caso 1 − 1. Il prestito vale **2** nella colonna corrente (come in decimale "prendere in prestito" vale 10): 0 − 1 → (2 + 0) − 1 = **1**, con prestito.

### Sottrazione in modulo e segno

Si vuole calcolare **A − B**. Si guarda il segno dei due operandi:

| Caso | Riscrittura | Cosa si fa |
|---|---|---|
| **A > 0 e B > 0** | \|A\| − \|B\| | se \|A\| ≥ \|B\|: \|A\| − \|B\|, segno **+**; altrimenti \|B\| − \|A\|, segno **−** |
| **A < 0 e B < 0** | −\|A\| + \|B\| = \|B\| − \|A\| | se \|B\| ≥ \|A\|: \|B\| − \|A\|, segno **+**; altrimenti \|A\| − \|B\|, segno **−** |
| **A > 0 e B < 0** | \|A\| + \|B\| | si **sommano i moduli**, segno **+** |
| **A < 0 e B > 0** | −(\|A\| + \|B\|) | si **sommano i moduli**, segno **−** |

> ⚠️ **Correzione**: negli appunti il primo caso era scritto "B > 010": è un refuso per **B > 0**.

Si vede bene perché il modulo e segno è scomodo: servono **confronti** e **circuiti diversi** (sommatore e sottrattore) a seconda dei casi.

### Sottrazione in complemento a 1

Per calcolare **A − B**:
1. Si calcola il **complemento a 1 di B** (cioè −B).
2. Si **somma A + (complemento a 1 di B)**.
3. Se c'è un riporto oltre l'MSB, lo si **risomma al risultato** (riporto circolare).

> ⚠️ **Correzione**: negli appunti il punto 2 diceva "sommo il primo termine con il **compl 2**": in complemento a 1 si somma il **complemento a 1** calcolato al punto 1. Il complemento a 2 è il metodo successivo.

Esempio: **10 − 3**
```
 +10 = 0000 1010
 +3  = 0000 0011  →  C1 = 1111 1100

     0000 1010   (+10)
   + 1111 1100   (−3 in C1)
   -----------
   1 0000 0110   ← riporto oltre l'8° bit
   +         1   ← riporto circolare
   -----------
     0000 0111   = +7 ✓
```

### Sottrazione in complemento a 2

Per calcolare **A − B**:
1. Si calcola il **complemento a 2 di B** (inverto + 1).
2. Si **somma A + (complemento a 2 di B)**.
3. L'eventuale riporto oltre l'MSB **si scarta**.

Esempio: **10 − 3**
```
 +10 = 0000 1010
 +3  = 0000 0011  →  C1 = 1111 1100  →  C2 = 1111 1101

     0000 1010   (+10)
   + 1111 1101   (−3 in C2)
   -----------
   1 0000 0111   ← il riporto si scarta
     0000 0111   = +7 ✓
```

Confronto: stesso risultato, ma in complemento a 2 **non serve la seconda somma**.

---

## 8. Verifica dell'overflow (numeri con segno)

> In complemento a 2 si ha **overflow** quando **gli ultimi due riporti sono diversi fra loro**, cioè:
> **riporto entrante nell'MSB ≠ riporto uscente dall'MSB**.

Regola equivalente, più facile da controllare a occhio:
- **si sommano due numeri dello stesso segno** e il risultato ha **segno opposto** → overflow;
- sommando due numeri di **segno diverso** l'overflow **non può mai verificarsi**.

> ⚠️ Attenzione: con i numeri con segno **il riporto finale da solo non indica overflow!** (Nel 10 − 3 qui sopra c'era un riporto finale, ma il risultato è corretto.)

#### Esempio con overflow — 100 + 50 (risultato 150 > 127)
```
 riporti      0 1 1 0 0 0 0 0 0
              ↑ ↑
              │ └ riporto entrante nell'MSB = 1
              └── riporto uscente dall'MSB  = 0      → diversi → OVERFLOW ✗

                0 1 1 0 0 1 0 0   (+100)
              + 0 0 1 1 0 0 1 0   (+50)
              -----------------
                1 0 0 1 0 1 1 0   → letto in C2 = −106 ✗  (due positivi danno un negativo)
```

#### Esempio senza overflow — (−7) + 10
```
 riporto uscente dall'MSB = 1, riporto entrante nell'MSB = 1  → uguali → OK

        1111 1001   (−7)
      + 0000 1010   (+10)
      -----------
      1 0000 0011   → scarto il riporto → +3 ✓
```

💡 Nei processori questo controllo è un semplice **XOR tra gli ultimi due riporti**, e il risultato finisce nel **flag di overflow (V/OF)** del registro di stato. Il riporto finale invece finisce nel **flag di carry (C/CF)**, che indica l'overflow per i numeri **senza segno**.

---

## 9. Operazioni binarie: riepilogo

| | Modulo e segno | Complemento a 1 | Complemento a 2 |
|---|---|---|---|
| Rappresentazione | ✅ **facile** e intuitiva | più complessa (inverto i bit) | più complessa (inverto + 1) |
| Zero | ❌ **doppio** (+0, −0) | ❌ **doppio** (+0, −0) | ✅ **univoco** |
| Intervallo (8 bit) | −127 … +127 | −127 … +127 | −128 … +127 |
| Somma/sottrazione | ❌ complicate (confronti, casi) | ✅ più semplici (solo somme) ma serve il **riporto circolare** | ✅ **le più semplici**: solo somme, il riporto si scarta |
| Uso reale | esponente/segno nei float | quasi in disuso | **tutti i computer moderni** (`int` in C, Java, …) |

#### Esempio — 31 − (−42)
Sottrarre un negativo equivale a sommare il suo opposto: 31 − (−42) = 31 + 42 = **73**.
```
   0001 1111   (+31)
 + 0010 1010   (+42)
 -----------
   0100 1001   = 64 + 8 + 1 = +73 ✓
```
Negli appunti c'era anche **1011 0110**: è il complemento a 1 di 73, cioè **−73 in C1** (sarebbe per esempio il risultato di −31 − 42). In C2, −73 = 1011 0111.

---

## 10. Esercizio: sottrazione binaria senza segno

**1 1101 1101₂ − 0111 0101₂** (codifica senza segno, 9 bit)

Si allinea a destra (aggiungendo uno zero a sinistra al secondo numero) e si procede colonna per colonna da destra, con i prestiti:

```
 prestiti    1 1
           1 1 1 0 1 1 1 0 1    (477)
         − 0 0 1 1 1 0 1 0 1    (117)
         -------------------
           1 0 1 1 0 1 0 0 0    (360)
```

Colonna per colonna (da destra, bit 0 → bit 8):
```
bit 0:  1 − 1           = 0
bit 1:  0 − 0           = 0
bit 2:  1 − 1           = 0
bit 3:  1 − 0           = 1
bit 4:  1 − 1           = 0
bit 5:  0 − 1           = 1   prestito dal bit 6
bit 6:  1 − 1 − 1 (pr.) = 1   prestito dal bit 7
bit 7:  1 − 0 − 1 (pr.) = 0
bit 8:  1 − 0           = 1
```
Verifica: 477 − 117 = **360** = 256 + 64 + 32 + 8 ✓

> ⚠️ **Correzione**: negli appunti il risultato parziale era "0101000"; le ultime 7 cifre corrette sono **1101000** (il bit 6 vale 1, per via del prestito dal bit 5). Il risultato completo è **101101000₂**.

---

## 11. Virgola fissa e virgola mobile

Per rappresentare i **numeri con la virgola** (razionali/reali) con un numero finito di bit ci sono due approcci.

### Virgola fissa (*fixed point*)
- Si decide **una volta per tutte** quanti bit sono per la **parte intera** e quanti per la **parte frazionaria**: la virgola è in una posizione **fissa** (non viene memorizzata).
- Es. su 8 bit, formato 4.4 (4 bit interi + 4 frazionari):
  ```
  0101.1000 = 4 + 1 + 0,5 = 5,5
  ```
- ✅ Semplice: le operazioni sono quelle degli interi.
- ❌ **Problema della scelta dei bit**: con pochi bit interi non si rappresentano numeri grandi, con pochi bit frazionari si perde precisione. Non si possono avere insieme numeri molto grandi e molto piccoli.
- Usata in DSP, microcontrollori senza unità floating point, valori monetari.

### Virgola mobile (*floating point*)
- È la versione binaria della **notazione scientifica**: 123,75 = 1,2375 × 10².
- Un numero è rappresentato da tre campi:

```
N = (−1)^S × M × 2^E

S = segno       (1 bit: 0 = positivo, 1 = negativo)
M = mantissa    (le cifre significative)
E = esponente   (dove "galleggia" la virgola)
```

- La virgola si **sposta** (galleggia) a seconda dell'esponente → con lo stesso numero di bit si rappresentano sia numeri **enormi** sia numeri **piccolissimi**.
- **Forma normalizzata**: la mantissa si scrive sempre come **1,xxxx** (una sola cifra 1 prima della virgola). Dato che quella cifra è *sempre* 1, non serve memorizzarla (**bit nascosto**, *hidden bit*) → si guadagna un bit di precisione.
- ❌ Non tutti i numeri sono rappresentabili esattamente: si fanno **arrotondamenti** (es. 0,1 in binario è periodico → `0.1 + 0.2 != 0.3`).

---

## 12. Numeri frazionari in esadecimale

Il valore di un numero frazionario in base *b* si calcola con le **potenze negative** della base:

```
cₙ … c₁ c₀ , c₋₁ c₋₂ …  =  … + c₁·b¹ + c₀·b⁰ + c₋₁·b⁻¹ + c₋₂·b⁻² + …
```

In esadecimale: 16⁻¹ = 1/16 = 0,0625; 16⁻² = 1/256 = 0,00390625.

#### Esempio 1 — A.E₁₆
```
A.E₁₆ = 10·16⁰ + 14·16⁻¹ = 10 + 14/16 = 10 + 0,875 = 10,875₁₀
```
In binario (ogni cifra hex → 4 bit, **anche dopo la virgola**):
```
A    .  E
1010 . 1110   →   1010,111₂
```
Verifica: 8 + 2 + 0,5 + 0,25 + 0,125 = 10,875 ✓

> ⚠️ **Correzione**: negli appunti c'era "A.E = 10.14". **Non si possono convertire le cifre una per una** dopo la virgola: E = 14 è il numero di *sedicesimi*, non di centesimi. Il valore corretto è **10,875**. (Lo zero finale di 1010.1110 si può togliere: dopo la virgola gli zeri a destra non contano.)

#### Esempio 2 — D3.C8₁₆
```
D3₁₆ = 13·16 + 3          = 211
.C8₁₆ = 12/16 + 8/256     = 0,75 + 0,03125 = 0,78125

D3.C8₁₆ = 211,78125₁₀
```
In binario:
```
D    3    .  C    8
1101 0011 . 1100 1000   →   11010011,11001₂
```

💡 **Da decimale a esadecimale (parte frazionaria)**: come per il binario, ma moltiplicando per **16**. Es. 0,875 · 16 = **14**,0 → E → 0,875₁₀ = 0,E₁₆.

---

## 13. Conversione in virgola mobile binaria — esempio: 123,75

### Passo 1 — Converto il numero in binario
```
Parte intera:  123 = 64 + 32 + 16 + 8 + 2 + 1 = 111 1011₂
Parte fraz.:   0,75 · 2 = 1,5 → 1
               0,5  · 2 = 1,0 → 1        →  0,11₂

123,75₁₀ = 1111011,11₂
```

### Passo 2 — Normalizzo (sposto la virgola dopo il primo 1)
```
1111011,11  =  1,11101111 × 2⁶       (virgola spostata di 6 posti a sinistra)
```
- Segno: **+** → S = 0
- Esponente: **6**
- Mantissa: **1,11101111** → si memorizza solo **11101111** (il primo 1 è nascosto)

### Passo 3 — Rappresento rispettando i bit di mantissa ed esponente (IEEE 754, 32 bit)
L'esponente si memorizza **in eccesso 127** (*bias*): E memorizzato = 6 + 127 = **133** = 1000 0101₂.

```
 S |    E     |               M (23 bit)
 0 | 10000101 | 11101111000000000000000
```

### Risultato finale
```
0100 0010 1111 0111 1000 0000 0000 0000  =  42F78000₁₆
```

💡 Puoi verificarlo in Python:
```python
import struct
struct.pack('>f', 123.75).hex()   # '42f78000'
```

> 💡 **Perché l'esponente in eccesso (bias)?** Così l'esponente è sempre un numero **positivo** e due float positivi si possono confrontare come se fossero interi (bit per bit). Per decodificare: E reale = E memorizzato − 127.

---

## 14. Dimensioni standard in virgola mobile binaria (IEEE 754)

Nei moderni calcolatori le dimensioni di mantissa ed esponente sono fissate dallo standard **IEEE 754** (1985, revisionato nel 2008 e 2019):

| | **Singola precisione** (32 bit) | **Doppia precisione** (64 bit) |
|---|---|---|
| Segno | 1 bit | 1 bit |
| Esponente | 8 bit | 11 bit |
| Mantissa | 23 bit (+1 nascosto) | 52 bit (+1 nascosto) |
| Bias esponente | 127 | 1023 |
| Cifre decimali significative | ~7 | ~15–16 |
| Valore massimo | ≈ 3,4 × 10³⁸ | ≈ 1,8 × 10³⁰⁸ |
| Nome nei linguaggi | `float` (C, Java) | `double` (C, Java), `float` in Python |

```
32 bit:  [S][EEEEEEEE][MMMMMMMMMMMMMMMMMMMMMMM]
          1     8              23

64 bit:  [S][EEEEEEEEEEE][MMMMMMMMMMMMMMMMMMMMM…MMMM]
          1      11                  52
```

💡 **Valori speciali** (esponente tutto 0 o tutto 1):

| Esponente | Mantissa | Significato |
|---|---|---|
| tutti 0 | 0 | **±0** (sì, anche qui esistono due zeri!) |
| tutti 0 | ≠ 0 | numeri **denormalizzati** (piccolissimi, senza bit nascosto) |
| tutti 1 | 0 | **±∞** (es. 1/0) |
| tutti 1 | ≠ 0 | **NaN** (*Not a Number*, es. 0/0, √−1) |

---

## 15. 📝 Esercizi di riepilogo

1. Rappresenta **−45** su 8 bit in modulo e segno, complemento a 1 e complemento a 2.
2. Calcola **25 − 40** in complemento a 2 su 8 bit.
3. Calcola **(−12) − 5** in complemento a 1 su 8 bit.
4. Calcola **90 + 50** in complemento a 2 su 8 bit. C'è overflow? Verificalo con la regola dei riporti.
5. Qual è l'intervallo rappresentabile con **6 bit** in complemento a 2? E in modulo e segno?
6. Converti **2B.4₁₆** in decimale e in binario.
7. Rappresenta **6,625** in IEEE 754 a 32 bit (scrivi anche il risultato in esadecimale).
8. Che numero rappresenta il float a 32 bit **C1200000₁₆**?

<details>
<summary><b>Soluzioni</b></summary>

1. 45 = 0010 1101 → MS: **1010 1101**; C1: **1101 0010**; C2: **1101 0011**
2. −40: 0010 1000 → 1101 0111 → +1 → 1101 1000. 0001 1001 + 1101 1000 = **1111 0001** → negativo → inverto +1 = 0000 1111 = 15 → **−15** ✓
3. −12 = 1111 0011, −5 = 1111 1010. Somma = 1 1110 1101 → riporto circolare → **1110 1110** → inverto = 0001 0001 = 17 → **−17** ✓
4. 0101 1010 + 0011 0010 = **1000 1100** (= −116 in C2). **Sì, overflow**: due positivi danno un negativo; riporto entrante nell'MSB = 1, uscente = 0 → diversi. (140 > 127.)
5. C2: **−32 … +31**. Modulo e segno: **−31 … +31**.
6. 2B.4₁₆ = 2·16 + 11 + 4/16 = **43,25₁₀** = 0010 1011 . 0100 = **101011,01₂**
7. 6,625 = 110,101₂ = 1,10101 × 2². S = 0, E = 2 + 127 = 129 = 1000 0001, M = 1010 1000 … → **0 10000001 10101000000000000000000** = **40D40000₁₆**
8. 1100 0001 0010 0000 … → S = 1, E = 1000 0010 = 130 → 130 − 127 = 3, M = 1,01₂ = 1,25 → −1,25 × 2³ = **−10**

</details>

---

## 16. 💡 Argomenti correlati da approfondire

1. **Estensione del segno** (*sign extension*): per passare da 8 a 16 bit un numero in C2 si copia l'MSB a sinistra (−3 = 1111 1101 → 1111 1111 1111 1101), non si aggiungono zeri.
2. **Rappresentazione in eccesso-k (bias)**: la stessa usata per l'esponente IEEE 754; utile da confrontare con C1 e C2.
3. **Flag del processore**: *carry* (overflow unsigned), *overflow* (overflow signed), *zero*, *sign/negative*.
4. **Tipi interi nei linguaggi**: `signed`/`unsigned` in C, `int8`…`int64`/`uint8`… in Rust e Go; cosa succede in overflow (*wrap-around*, panic, eccezione).
5. **Errori di arrotondamento nei float**: epsilon di macchina, perché non confrontare mai due float con `==`, e perché per i soldi si usano decimali o interi (centesimi).
6. **Half precision (16 bit)** e **bfloat16**: formati ridotti usati nelle GPU e nell'intelligenza artificiale (collegamento con CPU vs GPU della lezione 1).
7. **Codifica BCD** (*Binary Coded Decimal*): alternativa per rappresentare numeri decimali esatti.
8. **Sommatore/sottrattore in complemento a 2**: come un unico circuito (full adder + XOR sugli ingressi) fa sia somme sia sottrazioni.

---

> **Consiglio di studio**: per controllare i risultati in Python:
> - complemento a 2 su 8 bit: `format(-22 & 0xFF, '08b')` → `'11101010'`
> - da C2 a decimale: `int('11101010', 2) - 256` → `-22`
> - float IEEE 754: `struct.pack('>f', 6.625).hex()` → `'40d40000'`
> - frazionari hex: `float.fromhex('0xA.E')` → `10.875`
