# ![O3D302 (1)](https://user-images.githubusercontent.com/120630734/207893369-c059ca9f-2aec-485a-b9b4-2f1d04dbd1e4.jpg) 


# Guida pratica all'installazione e configurazione di un ambiente virtuale per il controllo del sensore 3D - ifm O3D302
https://www.ifm.com/it/it/product/O3D302


## Uso Conforme dispositivo
>Il sensore 3D O3D3xx è un sensore ottico che misura, punto per punto, la distanza tra il sensore e la superficie più vicina utilizzando la tecnologia a tempo di volo. Il sensore 3D O3D3xx illumina la scena con una fonte luminosa interna a infrarossi e calcola la distanza in base alla luce riflessa dalla superficie. Con l'elaborazione immagine interna vengono generati valori di processo dai dati e vengono confrontati con i valori di soglia. I valori di confronto e di processo vengono collegati alle uscite digitali. In questo modo è possibile risolvere le seguenti applicazioni: 
* Monitoraggio della completezza 
* Misurazione del livello 
* Monitoraggio della distanza 
* Misurazione di oggetti parallelepipedi 
* Classificazione di oggetti parallelepipedi 
>
>I dati letti e i valori di processo possono essere trasmessi tramite Ethernet e analizzati dall'utente. Anche il sensore 3D O3D3xx viene parametrizzato tramite Ethernet. Il sensore 3D O3D3xx può essere utilizzato solo nelle condizioni ambientali indicate nella scheda tecnica. La sicurezza del dispositivo è concepita se utilizzato nelle condizioni ambientali seguenti: 
* utilizzo in ambiente interno 
* altitudine fino a 2000 m 
* umidità relativa dell'aria fino al 90% massimo, non condensante 
* grado d'inquinamento 3 
>
>Considerando i requisiti per le emissioni di interferenze elettromagnetiche, il dispositivo è destinato ad applicazioni in ambienti industriali. Il dispositivo non è adatto per l’impiego in abitazioni


## Documenti necessari per la configurazione

| Libreria | LINK |
| ------ | ------ |
| OpenCV | <https://opencv.org/> |
| Open3D | <http://www.open3d.org/> |
| ifm3dpy | <https://ifm3d.com/sphinx-doc/build/html/index.html> |
| Python (v3.8) | <https://www.python.org/> |
| git | <https://git-scm.com/> |
| Microsoft C++ Build Tools | <https://visualstudio.microsoft.com/visual-cpp-build-tools/> |

## N.B.#1:
### Affinchè sia garantito un corretto funzionameto di Python bisogna verificare che le versioni differenti alla v3.8 vengano disinstallate e che durante l'installazione della v3.8 sia spuntata la voce "*Add Python 3.8 to PATH*"
![Python Install](https://user-images.githubusercontent.com/120630734/207897346-f84aa3c4-6031-49da-8d99-378e6035fe47.JPG)

## N.B.#2:
### Affinchè il comando *pip install -r requirements.txt* non dia errore durante il lancio (esecuzione), si devono scaricare i build Tools di Microsoft C++

## Configurazione Ambiente Virtuale (Prompt comandi)

> Note: Uno dei tuoi progetti potrebbe richiedere una versione diversa di una libreria esterna rispetto a un'altra. Se hai solo un posto dove installare i pacchetti, non puoi lavorare con due versioni diverse della stessa libreria. Questo è uno dei motivi più comuni per la raccomandazione di utilizzare un ambiente virtuale Python. Se installi due versioni diverse dello stesso pacchetto nel tuo ambiente Python globale, la seconda installazione sovrascrive la prima. Gli ambienti virtuali Python mirano a fornire un ambiente Python isolato.

```sh
# Creazione directory (cartella)
## mkdir – Crea una directory (cartella)
mkdir nome_directory
## cd – Cambia la cartella di lavoro attuale in quella specificata
cd nome_directory 
```

```sh
# Creazione SUB directory all'interno della directory superiore (sottocartella)
mkdir nome_SUBdirectory
cd nome_SUBdirectory 
```

```sh
# Creazione ambiente venv (Ambiente virtuale di Python)
## python3 -m venv /path/to/new/virtual/environment crea la cartella venv contenente tutti i file dell'ambiente virtuale sul percorso selezionato
python3 -m venv /path/to/new/virtual/environment

## python -m venv venv crea la cartella venv contenente tutti i file dell'ambiente virtuale nella directory selezionata
python -m venv venv
```


## Attivazione ambiente virtuale
> Note: In base al sistema operativo che si sta utilizzando, inserire il corrispettivo comando per attivare l'ambiente virtuale

| Platform | Shell           | Command to activate virtual environment |
| -------- | --------------- | --------------------------------------- |
| POSIX    | bash/zsh        | $ source venv/bin/activate            |
|          | fish            | $ source venv/bin/activate.fish       |
|          | csh/tcsh        | $ source venv/bin/activate.csh        |
|          | PowerShell Core | $ venv/bin/Activate.ps1               |
| Windows  | cmd.exe         | C:\> venv\Scripts\activate.bat        |
|          | PowerShell      | PS C:\> venv\Scripts\Activate.ps1     |


## Disattivazione ambiente virtuale
| Platform | Shell           | Command to activate virtual environment |
| -------- | --------------- | --------------------------------------- |
| Windows  | cmd.exe         | C:\> deactivate          |


## Installazione librerie
> Note: *Pip* è un sistema di gestione dei pacchetti scritto in Python, utilizzato per installare e gestire i pacchetti software.
```sh
## L'interfaccia della riga di comando di Pip consente l'installazione di pacchetti software Python emettendo un comando:
pip install nome_pacchetto

## Gli utenti possono anche rimuovere il pacchetto emettendo un comando:
pip uninstall nome_pacchetto
```

### Installazione libreria ifm3dpy
> Note: Installa nell'ambiente virtuale attivo la libreria ifm3dpy
```sh
# Python v3.8 should be installed
pip install ifm3dpy

WARNING: You are using pip version 19.2.3, however version 22.3.1 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.
```

### Installazione Build tools (git for Windows)
> Note: 
```sh
#Copiare dentro la SUBdirectory del sensore 3D gli esempi della visione 
mkdir ifm3d
# Copia della repository
cd ifm3d
git clone https://github.com/ifm/ifm3d.git --branch v1.0.0
```

### Requirements files
> Note: Il modo più semplice per rendere il nostro lavoro riproducibile da altri è includere un file dei requisiti nella directory principale del nostro progetto (directory superiore). Per fare ciò, eseguiremo il comando *pip freeze*, che elenca i pacchetti di terze parti installati, insieme ai loro numeri di versione, potendo così generare un file *requirements.txt*
```sh
# pip freeze does not output pip itself or packages for package management such as setuptools andwheel
pip freeze

## per salvare su un file librerie installate, anciare il segyuente programma:
pip freeze > requirements.txt
```

> Note: *Pip* ha una funzione per gestire elenchi completi di pacchetti e numeri di versione corrispondenti, tramite un file "*requirements*". Ciò consente la ricreazione efficiente di un intero gruppo di pacchetti in un ambiente separato (ad esempio un altro computer) o in un ambiente virtuale. Ciò può essere ottenuto con un file correttamente formattato e il seguente comando, dove *requirements.txt* è il nome del file:
```sh
# Nella directory superiore (di ifm3d)
pip install -r requirements.txt
### Installazione di requisiti seguendo un percorso specifico
pip install -r examples/python/viewer/requirements.txt
pip install .
```

```sh
# *pip list* emette tutti i pacchetti installati, inclusi quelli modificabili.
python -m pip list
py -m pip list --outdated --format columns
```

### Esecuzione programma Python
> Note: Scrittura per lanciare un programma con estensione .py
```sh
python nome_programma
```


## Risoluzione dei problemi
<https://docs.conda.io/en/latest/miniconda.html>

windows environment variables

