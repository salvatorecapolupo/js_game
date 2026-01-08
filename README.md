# The Kernel Breach 🛡️💻

### Descrizione

**The Kernel Breach** è un mini-gioco di ruolo (RPG) testuale ambientato in un sistema operativo ostile. Vestirai i panni di un hacker il cui obiettivo è penetrare nel "Core" del sistema e causare un crash controllato prima che il *Garbage Collector* ti elimini.

### Struttura del Progetto

Il gioco è diviso in due file principali per seguire le best practice di sviluppo:

* `index.html`: Il "guscio" del gioco. Contiene l'interfaccia grafica (stile terminale) e il pulsante di avvio.
* `game.js`: Il "cervello". Contiene tutta la logica, i dati delle stanze e le regole di gioco.

### Come Iniziare

1. Salva entrambi i file nella stessa cartella.
2. Apri `index.html` con qualsiasi browser (Chrome, Firefox, Edge).
3. Clicca su **"AVVIA EXPLOIT"**.
4. Interagisci tramite i messaggi che compaiono sullo schermo inserendo il numero corrispondente alla tua scelta.

### Obiettivo

Raggiungere il nodo `ending_win` senza far scendere la `cpuPower` a zero. Attenzione alle scelte: alcune consumano risorse, altre ti regalano Bitcoin (inutili, ma fanno curriculum!).

---

## 📚 Concetti JS coinvolti (Spiegati semplicemente)

Ecco cosa c'è "sotto il cofano". Questi sono i punti che un prof di informatica amerebbe sentire:

### 1. Oggetti come Macchine a Stati

Invece di usare mille variabili sparse, il gioco usa un grande oggetto chiamato `nodes`. Ogni proprietà di questo oggetto (`gate`, `core`, ecc.) rappresenta uno "stato" del gioco.

* **Perché è utile?** Rende il codice scalabile. Se vuoi aggiungere 100 nuove stanze, non devi cambiare la logica del gioco, ma solo aggiungere dati all'oggetto.

### 2. La Ricorsione

La funzione `loop()` è il cuore del gioco. Noterai che alla fine della sua esecuzione, se il gioco non è finito, chiama di nuovo se stessa: `this.loop(prossimaStanza)`.

* **Concetto:** Una funzione che chiama se stessa si dice **ricorsiva**. In questo caso serve a creare il "ciclo del gioco" senza usare un loop infinito `while(true)` che bloccherebbe il browser.

### 3. Gestione dello Stato (State Management)

L'oggetto `player` tiene traccia di tutto ciò che cambia: punti vita (CPU), soldi e inventario.

* **Dinamicità:** Quando scegli un'opzione che ha un `effect()`, modifichiamo direttamente le proprietà di `player`. Questo è il concetto base di come funzionano i personaggi nei videogiochi più complessi.

### 4. Array e Metodi di Iterazione (`forEach`)

Per mostrare le scelte all'utente, usiamo `node.options.forEach()`.

* **Spiegazione:** Il `forEach` prende ogni opzione nell'array e le "cicla" una per una per costruire il messaggio testuale. È molto più moderno e leggibile del classico `for (let i=0; ...)`.

### 5. Il contesto `this`

Nel gioco c'è una battuta sul fare il log di `this`.

* **Il problema:** In JavaScript, `this` cambia valore a seconda di *come* e *dove* viene chiamata una funzione. Nelle funzioni normali punta all'oggetto che possiede la funzione (il nostro `game`), ma nelle *arrow function* (`=>`) il `this` viene ereditato dallo scope esterno. È uno dei motivi principali di bug per i programmatori JS!

### 6. Funzioni Callback (negli `effect`)

Alcuni nodi hanno una proprietà `effect: () => { ... }`. Questa è una funzione passata come proprietà.

* **Utilità:** Ci permette di "iniettare" logica specifica solo in certe stanze (es. togliere vita o aggiungere oggetti) solo quando servono.

---

### Prossimo passo consigliato

Il gioco ora usa i `prompt()`, che sono un po' invasivi. **Ti piacerebbe che modificassimo il codice per far apparire il testo direttamente dentro la pagina HTML, magari con un effetto "macchina da scrivere"?** Sarebbe un ottimo modo per imparare la manipolazione del DOM!
