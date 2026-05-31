# AI Desktop File Organizer

Applicazione desktop Electron per importare, classificare e organizzare file di programmazione in cartelle per linguaggio o progetto.

## Funzionalita

- Importazione file multipla tramite selezione o drag & drop
- Classificazione automatica per estensione e contenuto
- Organizzazione locale in cartelle ordinate
- Salvataggio metadati progetto in un database JSON locale
- Ricerca per nome, linguaggio e percorso
- Analisi AI opzionale con OpenAI API
- Generazione README automatica anche senza chiave API, usando euristiche locali

## Requisiti

- Node.js 20 o superiore
- npm

## Avvio

```bash
npm install
npm start
```

Per abilitare l'analisi AI:

```bash
set OPENAI_API_KEY=la_tua_chiave
npm start
```

## Creare il programma per Windows

Su PowerShell usa `npm.cmd`, per evitare blocchi della execution policy:

```powershell
npm.cmd install
npm.cmd run dist
```

Il programma verra creato nella cartella `dist/`.

Output previsti:

- Installer Windows `.exe` con procedura guidata
- Eseguibile portable `.exe`

La build e non firmata digitalmente, cosi non richiede privilegi amministratore o Developer Mode per estrarre gli strumenti di code signing.

Per creare solo la versione portable:

```powershell
npm.cmd run dist:portable
```

Su PowerShell:

```powershell
$env:OPENAI_API_KEY="la_tua_chiave"
npm start
```

## Struttura

```text
src/
  main/
    main.js
    fileManager.js
    aiService.js
  renderer/
    index.html
    app.js
    style.css
  db/
    sqlite.js
  utils/
    classifier.js
  preload.js
```

## Note sicurezza

L'app usa IPC con `contextIsolation` e un preload dedicato. Il renderer non accede direttamente a Node.js o al file system; tutte le operazioni passano dal main process.
