## Installazione

Il primo passo sarà quello di installare Rust. Scaricheremo Rust attraverso il
comando `rustup`, uno strumento della linea di comando per gestire le diverse
versioni di Rust e gli strumenti associati ad esso. Avrai bisogno di una
connessione ad internet per il download.

> Nota: Se preferisci non utilizzare `rustup` per qualche ragione, perfavore leggi
> [Altri Metodi di installazione di Rust][otherinstall] per più opzioni.

I passaggi seguenti installano l'ultima versione stabile del compilatore di Rust.
Le garanzie di stabilità di Rust assicurano che tutti gli esempi scritti nel libro
che vengono compilati si compileranno anche con versioni più recenti di Rust.
L'output potrebbe differire leggermente tra le versioni perché Rust migliora
spesso i messaggi di errore e gli avvisi. In altre parole, qualsiasi versione
più recente e stabile di Rust che installi
utilizzando questi passaggi dovrebbe funzionare come previsto con il contenuto di questo libro.

> ### Notazione sulla linea di comando
>
> In questo capitolo e in tutto il libro, mostreremo alcuni dei comandi utilizzati nel
> terminale. I comandi che eseguirai nel terminale iniziano tutti con `$`. Tu non avrai
> bisogno di scrivere il carattere `$`; serve solo ad indicare l'inizio di ogni
> comando. Comandi che non iniziano con  `$` di solito mostrano l'output
> del comando precedente. Inoltre, esempi specifici di PowerShell useranno
> `>` invece che `$`.

### Installazione `rustup` su Linux e macOS

Se utilizzi Linux o macOS, apri un terminale ed esegui il seguente comando:

```console
$ curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
```

Questo comando scaricherà uno script e darà inizio all'installazione dello strumento
di `rustup`, che installerà l'ultima versione stabile di Rust. Ti potrebbe venir
chiesta la password. Se l'installazione è andata correttamente ti verrà scritto:

```text
Rust is installed now. Great!
```

Avrai anche bisogno di un *linker*, essendo un programma che Rust utilizza per unire
i risultati della compilazione in un unico file.
È probabile che tu ne abbia già uno. Se incorrerai in errori di linking
dovresti installare un compilatore per C che di solito include anche un linker.
Un compilatore per C è anche utile per il fatto che molti pacchetti di Rust
dipendono da del C e avranno quindi bisogno di un compilatore per il C

Su macOS puoi installare un compilatore C eseguendo:

```console
$ xcode-select --install
```

Utenti Linux dovrebbero generalmente installare GCC o Clang, in accordo con la
documentazione della loro distribuzione di Linux. Ad esempio, se usi Ubuntu,
puoi installare il pacchetto `build-essential`.

### Installazione di `rustup` su Windows

Su Windows, vai su [https://www.rust-lang.org/tools/install][install] e segui le istruzioni
per installare Rust. Ad un certo punto dell'installazione riceverai un messaggio
che ti spiegherà che avrai anche bisogno degli strumenti di build MSVC per Visual
Studio 2013 o più recente.

Per ottenere gli strumenti di build dovrai installare [Visual Studio
2022][visualstudio]. Quando ti verrà chiesto quali componenti installare, seleziona:

* “Desktop Development with C++”
* L'SDK per Windows 10 o 11
* Il pacchetto della lingua Inglese, insieme a tutti gli altri pacchetti di lingue che vuoi installare

Tutto il resto del libro utilizza comandi che funzionano sia su *cmd.exe* e PowerShell.
Se ci sono difference specifiche, spiegheremo quali utilizzare.

### Troubleshooting

Per controllare se hai installato Rust correttamente o no, apri uno shell ed esegui questo comando:

```console
$ rustc --version
```

Dovresti vedere il numero di versione, l'hash del commit e la data del commit
per l'ultima versione stabile rilasciata, nel seguente formato:

```text
rustc x.y.z (abcabcabc yyyy-mm-dd)
```

Se vedi questa informazione, hai installato Rust correttamente!
Se invece non la vedi, controlla che Rust sia nella variabile `%PATH%` del sistema
come segue.


Nel CMD di Windows, usa:

```console
> echo %PATH%
```

Su PowerShell, usa:

```powershell
> echo $env:Path
```

Su Linux e macOS, usa:

```console
$ echo $PATH
```

Se tutto ciò è corretto ma Rust comunque non funziona, ci sono diversi posti
dove puoi trovare aiuto. Scopri come metterti in contatto con altri
Rustaceans (un nomignolo ironico con cui ci chiamiamo) sulla [pagina della community][community].

### Aggiornamento e Disinstallazione

Una volta che Rust è installato grazie a `rustup`, aggiornare ad una versione appena
rilasciata è molto facile. Dal tuo shell, esegui il seguente comando:

```console
$ rustup update
```

Per invece disinstallare Rust e `rustup`, esegui il seguente comando dallo shell:

```console
$ rustup self uninstall
```

### Documentazione Locale

L'installazione di Rust include anche una copia della sua documentazione
così che tu possa leggerla offline. Esegui `rustup doc` per aprire la
documentazione locale nel tuo browser.

Ogni volta che un tipo o una funzione è messa a diposizione dalla
libreria standard e tu non sei sicuro sul cosa faccia e sul come utilizzarlo/a,
usa la documentazione API per scoprirlo.

[otherinstall]: https://forge.rust-lang.org/infra/other-installation-methods.html
[install]: https://www.rust-lang.org/tools/install
[visualstudio]: https://visualstudio.microsoft.com/downloads/
[community]: https://www.rust-lang.org/community
