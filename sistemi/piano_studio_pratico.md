# Piano di studio pratico — Sistemi (Lezioni 1–2)

**Scadenza: sabato 7 novembre 2026, entro le 19:00**
Basato su `lezione1_completa.md` e `lezione2_completa.md`.

Questo piano copre solo le **abilità pratiche/operative** (conversioni, aritmetica, codifiche, IEEE 754). La teoria pura (storia, paradigmi, Chomsky, Von Neumann, CPU/GPU) è volutamente esclusa — ripassala separatamente con flashcard se all'esame servono le definizioni.

---

## Ipotesi e calendario

| Quando | Tempo effettivo | Obiettivo principale |
|---|---|---|
| **Gio 5 nov, sera** | ~2 h 30 | Sistemi di numerazione + tutte le conversioni di base |
| **Ven 6 nov, sera** | ~3 h 15 | Aritmetica binaria/esadecimale + interi con segno |
| **Sab 7 nov, mattina** | ~3 h | Virgola fissa + IEEE 754 |
| **Sab 7 nov, pomeriggio** | ~3 h | Rifacimento esercizi + simulazione + punti deboli |
| **Totale** | **~11 h 45** | Finire entro sabato sera |

> Se una giornata slitta: proteggi i blocchi **[OBBLIGATORIO]** e sposta gli esercizi **[OPZIONALE]** al giorno successivo. Non saltare la simulazione di sabato.

---

## Come studiare ogni blocco (importante)

Per ogni blocco usa questo ciclo:

1. **5 min — richiamo a memoria:** scrivi formule/procedure senza appunti.
2. **10 min — verifica e correzione:** confronta con gli appunti, correggi solo ciò che è sbagliato.
3. **30–40 min — risolvi a mano:** solo carta, niente calcolatrice mentre risolvi.
4. **10 min — verifica e registra:** controlla con Python/calcolatrice programmatore, scrivi ogni errore nel registro.

**Regole**
- Mostra sempre riporti/prestiti e il numero di bit. La maggior parte degli errori d'esame è dovuta a larghezza/overflow.
- Per i numeri con segno, indica sempre la codifica (**MS / C1 / C2**) e il numero di bit.
- Non limitarti a leggere la soluzione: rifai da capo l'esercizio sbagliato il giorno dopo.
- Le tabelle di conversione e le potenze di 2 vanno richiamate a memoria, non consultate.

---

## Preparazione (giovedì, 15 min)

- [x] Crea un file per il registro degli errori `errori.md` con questa intestazione:

  ```markdown
  | Data | Argomento | Esercizio | Cosa ho fatto | Metodo corretto | Rifatto |
  |------|-----------|-----------|---------------|-----------------|---------|
  ```

- [x] Apri una calcolatrice in modalità programmatore (Linux: `gnome-calculator` → Modalità → Programmatore) e una REPL Python.
- [x] Scrivi una volta su carta: potenze di 2 (2⁰…2¹⁰, 2¹⁶), la tabella 0–15 dec/bin/esadec e i simboli romani.
- [x] Tieni quel foglio come unico riferimento per i tre giorni.

---

# Giorno 1 — giovedì 5 nov (2 h 30)
## Sistemi di numerazione e conversioni

### Blocco 1.1 — Sistemi di numerazione [OBBLIGATORIO] — 30 min

- [x] Spiega a voce la differenza tra **numero** e **numerale**; tra sistemi **additivi** e **posizionali**.
- [ ] Scrivi a memoria i simboli romani e le 4 regole; converti 5 numeri arabi → romani e 5 romani → arabi.
- [ ] Scrivi i simboli attici (Ι, Π, Δ, Η, Χ, Μ) e converti 3 numeri.
- [ ] Scrivi i simboli egizi per le potenze di 10 e converti 3 numeri.
- [ ] Fai gli esercizi **A1–A5** del blocco esercizi (in fondo al file).

**Obiettivo raggiunto quando:** sai convertire un numero romano di 4 cifre e un numero attico/egizio di 4 simboli senza appunti.

### Blocco 1.2 — Basi dei sistemi posizionali [OBBLIGATORIO] — 25 min

- [x] Scrivi la formula generale posizionale e sviluppa: `4703₁₀`, `101101₂`, `5B₁₆`, `A.E₁₆`, `0.101₂`.
- [x] Riproduci a memoria la **tabella 0–15 dec/bin/esadec** (16 righe).
- [x] Recita le potenze di 2: 2⁰…2¹⁰ e 2¹⁶.
- [x] Indica quanti valori sono rappresentabili con *n* bit in base *b* (0 … bⁿ−1).
- [x] Converti tra notazione `0b`, `0x` e notazione con pedice.

**Obiettivo raggiunto quando:** la tabella di 16 righe è scritta senza errori in meno di 4 minuti.

### Blocco 1.3 — Tutte le conversioni di base [OBBLIGATORIO] — 55 min

- [x] **Base b → decimale:** 8 conversioni, di cui 2 frazionarie (binario, esadecimale).
- [x] **Decimale → binario (interi):** 6 conversioni con il metodo delle divisioni; verificane 3 con il metodo della sottrazione delle potenze.
- [x] **Decimale → esadecimale:** 4 conversioni con divisione per 16 (resti 10–15 → A–F).
- [ ] **Decimale → binario (frazioni):** 4 conversioni con moltiplicazione ripetuta per 2 (fermati a 6 bit se periodico).
- [ ] **Binario ↔ esadecimale:** 8 conversioni usando gruppi di 4 bit (includi zeri iniziali e un caso frazionario).
- [ ] **Catene miste:** 4 conversioni che combinano i metodi (es. decimale → binario → esadecimale).
- [ ] Fai gli esercizi **B1–B10**.

**Obiettivo raggiunto quando:** ogni conversione è verificata e ogni errore è nel registro.

### Blocco 1.4 — Mini-quiz a tempo [OBBLIGATORIO] — 20 min

- [ ] 15 conversioni miste in 15 minuti, senza appunti.
- [ ] Correggile; registra ogni errore.
- [ ] Rifai subito le 3 più lente/sbagliate.

**Obiettivo di fine Giorno 1:** le conversioni sono meccaniche e quasi senza errori; la tabella 0–15 e le potenze di 2 sono memorizzate.

---

# Giorno 2 — venerdì 6 nov (3 h 15)
## Aritmetica e interi con segno

### Blocco 2.1 — Aritmetica senza segno in base 2 e 16 [OBBLIGATORIO] — 50 min

- [ ] Scrivi a memoria le tabelle di addizione, sottrazione e moltiplicazione binaria.
- [ ] **8 addizioni binarie** con riporti; per ciascuna indica il risultato su 4 o 8 bit e se c'è overflow unsigned.
- [ ] **6 addizioni esadecimali** (ricorda: riporto quando la colonna raggiunge 16).
- [ ] **6 sottrazioni binarie senza segno** con prestiti, mostrando ogni prestito.
- [ ] **4 moltiplicazioni binarie** e **2 divisioni binarie** (il bit del quoziente può essere solo 0 o 1).
- [ ] **3 moltiplicazioni esadecimali** (es. una cifra × una cifra e due cifre × una cifra).
- [ ] **Esercizi sugli shift:** moltiplica/divide per 2 e per 4 usando shift a sinistra/destra; scrivi il pattern di bit prima e dopo.
- [ ] Fai gli esercizi **C1–C8**.

**Obiettivo raggiunto quando:** riporti/prestiti sono corretti e sai prevedere l'overflow prima di fare la somma.

### Blocco 2.2 — Rappresentazione dei numeri con segno [OBBLIGATORIO] — 50 min

- [ ] Riproduci a memoria la tabella `+5 / −5 / +0 / −0` in **modulo e segno, C1, C2**.
- [ ] Codifica **10 valori decimali** (positivi e negativi) in tutte e tre le codifiche su 8 bit.
- [x] Nega **8 pattern di bit** in C1 e in C2 (inverti; inverti + 1).
- [ ] Decodifica **10 pattern** in decimale, mescolando le tre codifiche.
- [ ] Compila la tabella degli intervalli per **4, 8, 16 bit** (unsigned, MS, C1, C2).
- [ ] Usa la regola dell'intervallo C2 per scegliere il numero di bit per: temperature −50…+150; valori −200…+200; valori 0…1000.
- [ ] Fai gli esercizi **D1–D2** e **D7–D8**.

**Obiettivo raggiunto quando:** non confondi mai C1 e C2 e sai perché C2 ha un valore negativo in più.

### Blocco 2.3 — Aritmetica con segno e overflow [OBBLIGATORIO] — 70 min

- [ ] **Modulo e segno:** 6 addizioni/sottrazioni usando le regole dei casi (stesso segno → somma dei moduli; segni diversi → sottrai il minore dal maggiore).
- [ ] **C1:** 8 addizioni, di cui almeno 3 con **riporto circolare**; poi 4 sottrazioni usando A + C1(B).
- [ ] **C2:** 10 addizioni/sottrazioni, mescolando i segni; scarta il riporto finale.
- [ ] **Overflow:** 6 verifiche con entrambi i metodi:
  - riporto entrante nell'MSB ≠ riporto uscente dall'MSB;
  - due operandi con lo stesso segno danno un risultato di segno opposto.
- [ ] Fai la stessa operazione una volta in C1 e una in C2 e scrivi le differenze (seconda somma vs riporto scartato).
- [ ] Fai gli esercizi **D3–D6**.

**Obiettivo raggiunto quando:** sai fare la sottrazione in C2 senza convertire in decimale e rilevi correttamente l'overflow con segno.

### Blocco 2.4 — Consolidamento [OBBLIGATORIO] — 25 min

- [ ] Rivedi il registro degli errori; rifai **5 esercizi sbagliati** da capo.
- [ ] Quiz misto da 10 minuti: 2 conversioni, 2 addizioni, 2 sottrazioni, 2 negazioni, 2 verifiche di overflow.
- [ ] Segna le 3 abilità più deboli per il ripasso finale di sabato.

**Obiettivo di fine Giorno 2:** rappresentazione e aritmetica con segno sono solide; l'overflow non è confuso con il carry unsigned.

---

# Giorno 3 — sabato 7 nov (circa 6 h, finire entro le 19:00)
## Virgola mobile + consolidamento completo

### Blocco 3.1 — Virgola fissa e basi frazionarie [OBBLIGATORIO] — 45 min

- [ ] Spiega la differenza tra virgola fissa e mobile; indica un vantaggio e un limite di ciascuna.
- [ ] Per il **formato 4.4**, codifica/decodifica 6 valori (incluso un negativo in C2).
- [ ] 6 conversioni frazionarie: esadecimale ↔ decimale ↔ binario (es. `A.E`, `D3.C8`, `2B.4`).
- [ ] 3 frazioni decimali → binario; individua quali diventano periodiche.
- [ ] Fai gli esercizi **F4–F5** e **B8–B10**.

**Obiettivo raggiunto quando:** gestisci correttamente la virgola binaria e non converti mai le cifre esadecimali frazionarie una per una come decimali.

### Blocco 3.2 — IEEE 754 [OBBLIGATORIO] — 75 min

- [ ] Scrivi `N = (−1)^S × M × 2^E` e spiega segno, mantissa, esponente, bit nascosto, bias.
- [ ] Riproduci a memoria la tabella dei formati **32 bit / 64 bit** (campi, bias, precisione).
- [ ] **Normalizza 10 numeri binari** (sposta la virgola dopo il primo 1; scrivi l'esponente).
- [ ] **Codifica 6 numeri in esadecimale a 32 bit**: almeno un intero positivo, uno negativo, uno frazionario, uno < 1.
- [ ] **Decodifica 6 pattern esadecimali** in decimale.
- [ ] Scrivi la tabella dei valori speciali: ±0, denormalizzati, ±∞, NaN.
- [ ] Verifica tutte le codifiche/decodifiche con `struct` di Python.
- [ ] Fai gli esercizi **E1–E7**.

**Obiettivo raggiunto quando:** `6.625 → 40D40000` e `C1200000 → −10` vengono senza aiuto.

### Blocco 3.3 — Rifacimento completo degli esercizi [OBBLIGATORIO] — 60 min

- [ ] **Lezione 1, esercizi 1–9**, senza appunti (30 min).
- [ ] **Lezione 2, esercizi 1–8**, senza appunti (30 min).
- [ ] Correggi con le soluzioni; rifai subito ogni esercizio sbagliato.
- [ ] Aggiungi ogni errore al registro.

**Obiettivo raggiunto quando:** almeno 14 dei 17 esercizi sono corretti al primo tentativo.

### Blocco 3.4 — Simulazione d'esame [OBBLIGATORIO] — 75 min

- [ ] Scrivi una **simulazione di 20 domande** in 45 minuti (usa il blocco esercizi + gli esercizi delle note; niente appunti, niente calcolatrice).
- [ ] Correggi onestamente.
- [ ] Per ogni risposta sbagliata: rifai da capo e scrivi la procedura corretta nel registro.
- [ ] Riprova le 5 domande più soggette a errore dopo 20 minuti.

Mix suggerito: 4 conversioni, 2 sistemi di numerazione, 3 operazioni unsigned, 3 codifiche con segno, 3 operazioni con segno + overflow, 3 IEEE 754, 2 virgola fissa/Cantor.

### Blocco 3.5 — Richiamo finale [OBBLIGATORIO] — 30 min

- [ ] **Brain dump a foglio bianco:** scrivi a memoria ogni procedura (base b → dec, dec → b, raggruppamenti, addizione, sottrazione, C1, C2, overflow, IEEE 754).
- [ ] Confronta con gli appunti; correggi le lacune.
- [ ] Rifai le 10 domande che hai sbagliato più spesso nei tre giorni.
- [ ] Rivedi il registro degli errori un'ultima volta.
- [ ] Spunta la checklist di copertura qui sotto.

### Blocco 3.6 — Extra opzionali [OPZIONALE] — 30 min
Solo se il programma/esame include questi argomenti:

- [ ] Multipli del byte: kB vs KiB, MB vs MiB, perché un disco "da 1 TB" mostra ~931 GiB.
- [ ] Basi ASCII/Unicode: `'A' = 65`, `'a' = 97`, `'0' = 48`; cos'è UTF-8.
- [ ] Operatori bit a bit e maschere: `&`, `|`, `^`, `~`, `<<`, `>>`; imposta/azzera/verifica un bit.
- [ ] Endianness: scrivi i byte di `0x12345678` in big-endian e little-endian.
- [ ] BCD: codifica/decodifica un numero decimale di 4 cifre.
- [ ] Accoppiamento di Cantor: calcola la stanza per (riga, colonna) e viceversa.

---

## Checklist di copertura — tutti gli argomenti pratici

### Sistemi di numerazione e rappresentazione
- [ ] Numero vs numerale; additivo vs posizionale
- [ ] Numeri romani (4 regole, massimo 3 ripetizioni, casi sottrattivi)
- [ ] Numeri attici (simboli, massimo 4 ripetizioni)
- [ ] Numeri egizi (potenze di 10, fino a 9 ripetizioni)
- [ ] Formula del valore posizionale, LSD/MSD, intervallo bⁿ
- [ ] Potenze di 2 e unità binarie (bit, nibble, byte, word)
- [ ] Tabella 0–15 dec/bin/esadec
- [ ] Base b → decimale (incluse le frazioni)
- [ ] Decimale → binario / esadecimale con divisioni
- [ ] Frazione decimale → binario con moltiplicazioni
- [ ] Binario ↔ esadecimale (gruppi di 4)
- [ ] Esadecimale frazionario ↔ binario ↔ decimale

### Aritmetica
- [ ] Addizione binaria con riporti
- [ ] Addizione esadecimale con riporto a 16
- [ ] Overflow unsigned in addizione a larghezza fissa
- [ ] Sottrazione binaria con prestiti
- [ ] Moltiplicazione binaria
- [ ] Moltiplicazione esadecimale
- [ ] Divisione binaria
- [ ] Shift come moltiplicazione/divisione per 2

### Interi con segno
- [ ] Modulo e segno: codifica/decodifica
- [ ] C1: codifica/decodifica/negazione
- [ ] C2: codifica/decodifica/negazione
- [ ] Tabella intervalli per unsigned/MS/C1/C2 (n bit)
- [ ] Scelta del numero di bit per un intervallo
- [ ] Addizione/sottrazione in modulo e segno
- [ ] Addizione/sottrazione in C1 con riporto circolare
- [ ] Addizione/sottrazione in C2, scartando il riporto
- [ ] Rilevamento overflow con segno (riporto entrante vs uscente, regola dei segni)

### Virgola mobile
- [ ] Virgola fissa, formato 4.4
- [ ] Formula floating point e normalizzazione
- [ ] Bit nascosto e bias dell'esponente (127 / 1023)
- [ ] Codifica IEEE 754 singola precisione
- [ ] Decodifica IEEE 754 singola precisione
- [ ] Layout dei campi IEEE 754 doppia precisione
- [ ] Valori speciali: ±0, denormalizzati, ±∞, NaN
- [ ] Errore di arrotondamento: `0.1 + 0.2 ≠ 0.3`

### Altri argomenti pratici dalle note
- [ ] Formula di accoppiamento di Cantor e numeri triangolari
- [ ] Ragionamento sull'hotel di Hilbert (solo concetto)
- [ ] Argomento diagonale (solo concetto)

---

## Blocco esercizi (ripetizioni extra opzionali)

Usali dopo i blocchi principali se ti servono altre ripetizioni. Le risposte sono in fondo — non sbirciare.

### A. Sistemi di numerazione
- A1. Converti `MCMXCIV` in arabo.
- A2. Converti `3888` in romano.
- A3. Converti il numero attico `ΗΗΔΔΔΙΙ` in arabo.
- A4. Scrivi `2305` in simboli egizi.
- A5. Converti `2026` in romano.

### B. Conversioni di base
- B1. `200₁₀` → binario ed esadecimale.
- B2. `2F₁₆` → decimale e binario.
- B3. `11101011₂` → esadecimale e decimale.
- B4. `156₁₀` → binario ed esadecimale.
- B5. `0.625₁₀` → binario.
- B6. `1011011₂` → esadecimale e decimale.
- B7. `3F2₁₆` → binario.
- B8. `2B.4₁₆` → decimale e binario.
- B9. `A.E₁₆` → decimale e binario.
- B10. `D3.C8₁₆` → decimale e binario.

### C. Aritmetica senza segno
- C1. `1101₂ + 0111₂`; overflow su 4 bit?
- C2. `A5₁₆ + 6C₁₆`; cosa succede su 8 bit?
- C3. `110₂ × 101₂`.
- C4. `110111₂ ÷ 101₂`.
- C5. `1 1101 1101₂ − 0111 0101₂`.
- C6. `3A7₁₆ + 1F9₁₆`.
- C7. `2A₁₆ × 3`.
- C8. `1B₁₆ × 2C₁₆`.

### D. Interi con segno
- D1. Codifica `−45` su 8 bit in MS, C1, C2.
- D2. Codifica `−22` su 8 bit in C2.
- D3. Calcola `25 − 40` in C2 su 8 bit.
- D4. Calcola `(−12) − 5` in C1 su 8 bit.
- D5. Calcola `90 + 50` in C2 su 8 bit; c'è overflow?
- D6. Calcola `31 − (−42)` su 8 bit.
- D7. Intervalli con 6 bit: C2 e modulo e segno.
- D8. Decodifica `11101010₂` come numero C2 a 8 bit.

### E. Virgola mobile
- E1. Codifica `6.625` in IEEE 754 a 32 bit (binario + esadecimale).
- E2. Codifica `123.75` in IEEE 754 a 32 bit (esadecimale).
- E3. Decodifica il float a 32 bit `C1200000₁₆`.
- E4. Codifica `12.5` in IEEE 754 a 32 bit.
- E5. Codifica `−0.75` in IEEE 754 a 32 bit.
- E6. Codifica `100.0` in IEEE 754 a 32 bit.
- E7. Spiega perché `0.1 + 0.2 ≠ 0.3` usando le frazioni binarie.

### F. Cantor e virgola fissa
- F1. Quale stanza è (riga 3, colonna 3) nella tabella di Cantor?
- F2. Quale stanza è (riga 2, colonna 4)?
- F3. Qual è il 6° numero triangolare?
- F4. Decodifica il valore in virgola fissa 4.4 `0101.1000`.
- F5. Codifica `−3.25` in virgola fissa 4.4, C2.

---

<details>
<summary><b>Blocco esercizi — risposte</b></summary>

### A
- A1. 1000 + 900 + 90 + 4 = **1994**.
- A2. **MMMDCCCLXXXVIII**.
- A3. 100 + 100 + 10 + 10 + 10 + 1 + 1 = **232**.
- A4. 2 × 1 000 + 3 × 100 + 0 × 10 + 5 × 1 → **2 fiori di loto + 3 corde arrotolate + 5 bastoncini**.
- A5. **MMXXVI**.

### B
- B1. `11001000₂`, `C8₁₆`.
- B2. `47₁₀`, `101111₂`.
- B3. `EB₁₆`, `235₁₀`.
- B4. `10011100₂`, `9C₁₆`.
- B5. `0.101₂`.
- B6. `5B₁₆`, `91₁₀`.
- B7. `1111110010₂`.
- B8. `43.25₁₀`, `101011.01₂`.
- B9. `10.875₁₀`, `1010.111₂`.
- B10. `211.78125₁₀`, `11010011.11001₂`.

### C
- C1. `10100₂` (20). Su 4 bit: `0100` → **overflow**.
- C2. `111₁₆` (273). Su 8 bit: `11₁₆` → **overflow unsigned**.
- C3. `11110₂` (30).
- C4. `1011₂` (11).
- C5. `101101000₂` (360).
- C6. `5A0₁₆` (1440).
- C7. `7E₁₆` (126).
- C8. `4A4₁₆` (1188).

### D
- D1. MS `10101101`, C1 `11010010`, C2 `11010011`.
- D2. `11101010`.
- D3. `11110001₂` = **−15**.
- D4. `11101110₂` = **−17** (dopo il riporto circolare).
- D5. `10001100₂` = **−116**; **sì, overflow** (due positivi danno un negativo).
- D6. `01001001₂` = **+73**.
- D7. C2: **−32 … +31**; MS: **−31 … +31**.
- D8. **−22**.

### E
- E1. `0 10000001 10101000000000000000000` = **40D40000₁₆**.
- E2. **42F78000₁₆**.
- E3. Segno 1, esponente 130 → 3, mantissa 1.25 → **−10**.
- E4. **41480000₁₆**.
- E5. **BF400000₁₆**.
- E6. **42C80000₁₆**.
- E7. 0.1 in binario è **periodico** (`0.0001100110011…₂`), quindi non è memorizzabile esattamente; entrambi gli operandi vengono arrotondati e la somma non è esattamente 0.3.

### F
- F1. `(3+3−1)(3+3−2)/2 + 3 = 13`.
- F2. `(2+4−1)(2+4−2)/2 + 4 = 14`.
- F3. `6·7/2 = 21`.
- F4. `0101.1000₂ = 4 + 1 + 0.5 = 5.5`.
- F5. `0011.0100₂` (+3.25) → inverti + 1 → **`1100.1100₂`**.

</details>

---

## Se hai poco tempo

Ordine di priorità (dal più importante):

1. Conversioni di base (Giorno 1, blocchi 1.2–1.3).
2. Codifica/decodifica C2 + addizione/sottrazione C2 + overflow (Giorno 2, blocchi 2.2–2.3).
3. Codifica/decodifica IEEE 754 (Giorno 3, blocco 3.2).
4. Aritmetica binaria/esadecimale unsigned (Giorno 2, blocco 2.1).
5. C1 e modulo e segno (Giorno 2, blocchi 2.2–2.3).
6. Virgola fissa ed esadecimale frazionario (Giorno 3, blocco 3.1).
7. Sistemi di numerazione e Cantor (Giorno 1, blocco 1.1; Giorno 3, blocco 3.5).
8. Extra opzionali (Giorno 3, blocco 3.6).

---

## Controllo finale — sabato prima delle 19:00

- [ ] Tutti i blocchi **[OBBLIGATORIO]** sono spuntati.
- [ ] I 17 esercizi delle due note sono rifatti senza appunti.
- [ ] La simulazione è corretta e ogni errore è stato rifatto.
- [ ] Il registro degli errori non ha voci irrisolte.
- [ ] La checklist di copertura è tutta spuntata (tranne gli extra opzionali che hai deciso di saltare).
- [ ] Sai scrivere le procedure chiave su un foglio bianco senza appunti.
