# checkDiet 🥑

App web a pagina singola per monitorare l'andamento di una dieta **keto + digiuno 23h** senza dover loggare i pasti ogni giorno. Inserisci solo il **peso** ogni 2-3 giorni: l'app calcola da sola trend, proiezione verso l'obiettivo e alert.

Tutto in un unico file `index.html`: nessun framework, nessuna dipendenza, nessun build. Grafici disegnati in SVG puro.

## Funzionalità

- **Input minimo:** peso (obbligatorio) + giro vita settimanale (opzionale) + livello di energia (opzionale).
- **A colpo d'occhio:** peso attuale, kg persi, kg mancanti, ritmo (kg/settimana), data di arrivo stimata, BMI, mantenimento calorico stimato.
- **Alert automatici:** ritmo troppo veloce (rischio muscolo/elettroliti), ritmo ideale, plateau, energia bassa, promemoria se non pesi da >4 giorni.
- **Grafici:** peso nel tempo (con linea obiettivo + proiezione), ritmo settimanale, progress bar, BMI, giro vita, energia.
- **Sezione Dieta:** riassunto del piano, ripartizione macro (P/C/F), kcal per pasto, e i **7 pasti completi** con ingredienti.
- **Stima metabolica:** da altezza + data di nascita calcola età, BMR (Mifflin-St Jeor) e mantenimento, mostrando il deficit reale rispetto all'intake.
- **Sync cloud** PC ↔ telefono via [jsonbin.io](https://jsonbin.io) + backup Esporta/Importa JSON.

## Come si usa

1. Apri la pagina (vedi *Pubblicazione* sotto per averla a un URL).
2. Inserisci il peso quando ti pesi. Reinserire una data già presente la sovrascrive; la ✕ nello storico elimina una riga.
3. **⚙︎ Obiettivo/altezza** per impostare peso e data di inizio, peso e data obiettivo, altezza e data di nascita.

### Far ripartire il conteggio da un nuovo peso iniziale
1. **⚙︎ Obiettivo/altezza** → imposta **Peso iniziale** e **Data di inizio** reali.
2. Nello **Storico** elimina con la ✕ l'eventuale punto-seme finto.
3. Aggiungi la prima misurazione vera col form.

## Sincronizzazione tra dispositivi

I dati vivono su un "bin" di jsonbin.io; la chiave di sync sta nel `localStorage` di ogni dispositivo (separata dai dati). Modificare il codice **non** richiede di riconfigurare la sync: basta ricaricare il file e fare refresh.

**Setup (una volta):**
1. Registrati su [jsonbin.io](https://jsonbin.io) → copia la **Master Key** (`X-Master-Key`).
2. Apri l'app → **☁︎ Configura sync** → incolla la Master Key, lascia **Bin ID vuoto** → l'app crea il bin e mostra il **Bin ID** da segnare.
3. Sul secondo dispositivo: **☁︎ Configura sync** con la **stessa Master Key + il Bin ID**.
4. **🔄 Sincronizza** per scaricare i dati aggiornati (oltre al pull automatico all'apertura).

> Conflitti gestiti con *last-write-wins* (uso a un dispositivo per volta). L'**Esporta backup** resta come rete di sicurezza.

## Pubblicazione (GitHub Pages)

1. Tieni il file come **`index.html`** nella root del repo.
2. **Settings → Pages** → Source: branch `main`, cartella `/ (root)` → Save.
3. URL: `https://<utente>.github.io/<repo>/`
4. Su iPhone (Safari): **Condividi → Aggiungi alla schermata Home** → diventa un'icona a tutto schermo.

Dopo ogni push, ricorda solo di fare **refresh** della pagina: sync e dati restano.

## Stack

HTML + CSS + JavaScript vanilla. Grafici SVG generati a runtime. Persistenza: `localStorage` (cache) + jsonbin.io (cloud). Nessuna build, nessun server.
