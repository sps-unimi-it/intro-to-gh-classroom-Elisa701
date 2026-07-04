# Esame Elisa — Replication study: sentiment dictionaries on BBC News

Repository per il progetto d'esame del corso **c4ss** (Computational Social Science).  
Lo studio replica l'approccio di Chan et al. (2021) e del notebook di riferimento `Sentiment_analysis.ipynb`, applicando tre lessici di sentiment off-the-shelf a un corpus diverso: **9 recenti articoli brevi della BBC News**, tre per categoria: *sport*, *technology*, *health*.

## Struttura del progetto

```text
Esame_Elisa/
├── Data/
│   └── BBC_news/              # Corpus di 9 articoli .txt
│       ├── health/
│       │   ├── health_001.txt
│       │   ├── health_002.txt
│       │   └── health_003.txt
│       ├── sport/
│       │   ├── sport_001.txt
│       │   ├── sport_002.txt
│       │   └── sport_003.txt
│       └── tech/
│           ├── tech_001.txt
│           ├── tech_002.txt
│           └── tech_003.txt
├── Esame_Elisa_BBC.ipynb      # Notebook principale con l'analisi
├── lexica/                    # Copia locale dei tre lessici (mirror/fallback)
│   ├── AFINN-111.txt
│   ├── bing-positive-words.txt
│   ├── bing-negative-words.txt
│   └── NRC-Emotion-Lexicon-Wordlevel-v0.92.txt
├── Results/                   # CSV e figure generati dall'analisi
│   ├── sentiment_by_article.csv
│   ├── sentiment_by_category.csv
│   ├── boxplot_sentiment_by_category.png
│   ├── dictionary_agreement.png
│   └── content_length_bias.png
└── README.md                  # Questo file (rinomina README_v2.md → README.md)
```

Ogni file `.txt` contiene una riga `Title:`, una riga `URL:` e il corpo dell'articolo, sul modello di `Data/Presidents_texts/`.  
I file sono organizzati in sottocartelle per categoria (`health/`, `sport/`, `tech/`).

## Lessici utilizzati

I tre dizionari off-the-shelf richiesti dall'esame sono:

1. **AFINN-111** — punteggi interi da -5 a +5 per parola.
2. **Bing Liu** — liste di parole *positive* e *negative*.
3. **NRC Emotion Lexicon** — associazioni di parole a 8 emozioni, inclusi `positive` e `negative`.

Il notebook cerca i lessici in `../downloaded_lexica/` (come da struttura originale del corso). Se quella cartella non è disponibile, usa automaticamente la copia locale in `Esame_Elisa/lexica/`.

## Requisiti

È sufficiente avere **Python 3** installato. Le librerie necessarie sono:

- `pandas`
- `numpy`
- `matplotlib`
- `scipy`
- `jupyter`

## Come eseguire l'analisi con un ambiente virtuale (venv)

1. Aprire il **Terminale** su Mac.
2. Spostarsi nella cartella del progetto:

   ```bash
   cd /Users/davides/Desktop/Esame/Esame_Elisa
   ```

3. Creare l'ambiente virtuale:

   ```bash
   python3 -m venv .venv
   ```

4. Attivare l'ambiente virtuale:

   ```bash
   source .venv/bin/activate
   ```

   Il terminale mostrerà `(.venv)` all'inizio della riga.

5. Installare le librerie necessarie:

   ```bash
   python3 -m pip install pandas numpy matplotlib scipy jupyter
   ```

6. Verificare l'installazione:

   ```bash
   python3 -c "import pandas, numpy, matplotlib, scipy, jupyter; print('Tutto OK')"
   ```

7. Avviare Jupyter:

   ```bash
   jupyter notebook Esame_Elisa_BBC.ipynb
   ```

8. Eseguire tutte le celle: nel menu del notebook selezionare `Cell → Run All`.
9. I file CSV e le figure vengono salvati automaticamente in `Esame_Elisa/Results/`.

### Disattivare l'ambiente

Quando hai finito, nel terminale scrivi:

```bash
deactivate
```

## Output prodotti

| File | Descrizione |
|------|-------------|
| `sentiment_by_article.csv` | Punteggi raw e normalizzati per ciascun articolo |
| `sentiment_by_category.csv` | Media dei punteggi normalizzati per categoria |
| `boxplot_sentiment_by_category.png` | Distribuzione dei punteggi normalizzati per lessico e categoria |
| `dictionary_agreement.png` | Correlazioni tra i tre dizionari |
| `content_length_bias.png` | Confronto tra punteggi raw (dipendenti dalla lunghezza) e normalizzati |

## Consegna tramite GitHub Classroom

1. **Accetta l'assignment** sul link GitHub Classroom fornito dal docente.
2. **Clona** il repository personale che GitHub Classroom crea automaticamente:

   ```bash
   git clone <URL-del-tuo-repo>
   cd <nome-repo>
   ```

3. **Organizza i file** come richiesto dalle istruzioni d'esame. In particolare, assicurati che siano presenti:

   - `Esame_Elisa/Data/BBC_news/*`
   - `Esame_Elisa/Esame_Elisa_BBC.ipynb`
   - `Esame_Elisa/Results/*`
   - I lessici in `downloaded_lexica/` (se usi la struttura originale del corso) oppure la copia locale in `Esame_Elisa/lexica/`

4. **Escludere l'ambiente virtuale** dal repository creando un file `.gitignore` con questo contenuto:

   ```gitignore
   .venv/
   venv/
   __pycache__/
   .ipynb_checkpoints/
   .DS_Store
   Results_new/
   ```

5. **Committa e pusha** tutto:

   ```bash
   git add .
   git commit -m "Consegna esame c4ss — BBC sentiment analysis"
   git push origin main
   ```

6. Verifica su GitHub che tutti i file siano stati caricati correttamente e che il notebook sia leggibile.

## Note

- Gli articoli sono stati scaricati da URL ufficiali BBC e salvati come `.txt` nelle sottocartelle di `Esame_Elisa/Data/BBC_news/`.
- L'analisi usa **punteggi normalizzati per lunghezza** (`score / word_count`) per replicare la correzione del content-length bias discussa nello studio di riferimento.
- Sport risulta il più positivo in media; health il più negativo; technology è neutro o leggermente positivo a seconda del lessico.
