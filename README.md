# Sintesi di un algoritmo basato su ResNet per Windows PE malware detection

**[Visualizza il PDF completo della tesi](tesi.pdf)**

Questo repository contiene i sorgenti LaTeX e il materiale utilizzato per la
mia tesi di laurea in Informatica presso l'Università degli Studi di Bari Aldo
Moro.

## Di cosa parla la tesi

La sicurezza informatica è diventata sempre più importante a causa della
diffusione di sistemi e servizi digitali. Tra le minacce principali ci sono i
malware, cioè software progettati per svolgere azioni dannose o non
autorizzate.

In questa tesi ho studiato un approccio per classificare i file Windows
Portable Executable (PE) come benigni o malevoli. L'idea di base è trasformare
il contenuto binario dei file PE in immagini e utilizzare poi tecniche di
Computer Vision e Deep Learning per effettuare la classificazione.

In particolare, ho confrontato:

- le strategie di mapping `LINEAR`, `ZIGZAG` e `SERPENTINE`;
- immagini RGB e immagini in scala di grigi;
- immagini a dimensione fissa e immagini con altezza variabile;
- le prestazioni di una rete neurale ResNet-50 nelle diverse configurazioni.

L'obiettivo del confronto è capire quale rappresentazione permetta di
distinguere nel modo più accurato possibile i file benigni da quelli malevoli.

## Dataset e risultati principali

Per la validazione è stato utilizzato il *PE Malware Machine Learning Dataset*
di Practical Security Analytics. Ho caricato su Kaggle una versione del dataset
già suddivisa in modo stratificato nei set di training e test:
[PE Malware Dataset su Kaggle](https://www.kaggle.com/datasets/domenicobianchini/pe-malware-dataset).

Il dataset comprende **201.549 file PE**, di cui:

- 86.812 file benigni;
- 114.737 file malevoli.

La suddivisione mantiene la proporzione tra file benigni e malevoli, con un
training set pari all'80% dei campioni e un test set pari al restante 20%. In
totale sono state valutate 12 configurazioni, ottenute
combinando le strategie di mapping, il tipo di immagine e la modalità di
calcolo delle dimensioni.

La configurazione che ha ottenuto il risultato migliore è stata:

```text
SERPENTINE + RGB + altezza variabile
```

con una *overall accuracy* pari al **97,61%** sul test set.

In generale, le configurazioni ad altezza variabile hanno ottenuto risultati
migliori rispetto alle configurazioni con immagini di dimensione fissa
`224 x 224`.

## Struttura del repository

I file principali sono organizzati nel seguente modo:

```text
.
├── README.md                 # Descrizione del progetto
├── tesi.tex                  # File principale LaTeX
├── introduzione.tex          # Contesto, motivazioni e obiettivi
├── capitolo1.tex             # File Windows PE e malware
├── capitolo2.tex             # Conversione dei file PE in immagini e ResNet
├── capitolo3.tex             # Dataset, esperimenti e risultati
├── conclusioni.tex           # Conclusioni e possibili sviluppi futuri
├── appendice.tex             # Progettazione UML e descrizione dei componenti
├── bibliografia.bib          # Riferimenti bibliografici
├── dedica.tex                # Dedica
├── note.tex                  # Note introduttive
├── ringraziamenti.tex        # Ringraziamenti
├── images/                   # Immagini, diagrammi e loghi usati nella tesi
├── topfront.sty              # Stile del frontespizio
├── tesi.pdf                  # PDF della tesi già compilato
├── LICENSE.txt               # Licenza del template
└── .gitignore                # File esclusi dal repository
```

## Nota sul codice e sul dataset

Il codice utilizzato per la conversione dei file PE in immagini, la
preparazione dei dati, il training e la valutazione del modello è disponibile
nel repository [pe-image-conversion](https://github.com/DomenicoBianchini/pe-image-conversion).

Il dataset utilizzato negli esperimenti è disponibile su
[Kaggle](https://www.kaggle.com/datasets/domenicobianchini/pe-malware-dataset) ed
è già organizzato nei set di training e test.

Nell'appendice della tesi è riportato il diagramma UML delle classi del
progetto, insieme alla descrizione dei principali componenti della pipeline.

## Sviluppi futuri

Alcuni possibili sviluppi individuati nel lavoro sono:

- verificare i risultati su dataset differenti;
- confrontare ResNet-50 con altre architetture della famiglia ResNet;
- calcolare le dimensioni delle immagini in funzione della lunghezza del
  singolo file PE;
- valutare l'utilizzo di `AutoImageProcessor` di Hugging Face per la
  preparazione delle immagini.

## Licenza

Per le condizioni di utilizzo del template e dei materiali presenti nel
repository, fare riferimento a [LICENSE.txt](LICENSE.txt).
