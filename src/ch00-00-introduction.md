# Introduzione

> Nota: Questa edizione del libro è la stessa di [The Rust Programming
> Language][nsprust] disponibile in cartaceo e ebook da [No Starch
> Press][nsp].

[nsprust]: https://nostarch.com/rust-programming-language-2nd-edition
[nsp]: https://nostarch.com/

Benvenuti sul libro riguardante *The Rust Programming Language*.
Rust ti aiuta a scrivere software più veloci e più affidabili.
L'ergonomia di linguaggi a livello elevato e il controllo a basso livello sono
spesso in conflitto nella progettazione dei linguaggi di programmazione; Rust
affronta questo conflitto. Bilanciando potenza tecnica e un'ottima esperienza
per lo sviluppatore, Rust ti offre la possibilità di controllare aspetti a
basso livello (come l'utilizzo della memoria) senza tutte le complicazioni
tradizionalmente associate a tale controllo.

## Per chi è Rust?

Rust è l'ideale per diverse persone per ragioni differenti. Consideriamo qualche gruppo
di persone tra i più importanti.

### Team di sviluppatori

Rust si sta dimostrando uno strumento molto produttivo per la collaborazione tra
grandi team di sviluppatori con diversi livelli di conoscenza della programmazione
di sistemi. Il codice di basso livello è soggetto a vari bug, che nella maggior
parte degli altri linguaggi possono essere individuati solo attraverso test
approfonditi e una revisione scrupolosa del codice da parte di sviluppatori esperti.
In Rust, il compilatore svolge un ruolo di controllore rifiutando di compilare del codice
contenententi questi bug difficili da individuare, inclusi i bug nel parallelismo.
Lavorando fianco a fianco del compilatore, il team può dedicare il proprio tempo
alla logica del programma anziché risolvere bug.

Rust inoltre include strumenti di sviluppo contemporanei nella programmazione di sistemi:

* Cargo, il gestore di librerie e strumento di build, rende aggiungere, compilare
  e gestire librerie semplice e consistente nell'ecosistema di Rust.
* Rustfmt, lo strumento di formattazione che rende consistente lo stile del codice tra sviluppatori.
* Il Server di Rust, che potenzia l'integrazione all'interno degli IDE per la completazione del codice
  e messaggi di errore.

Utilizzando questi ed altri strumenti nell'ecosistema di Rust, gli sviluppatori
potranno essere molto più produttivi nella programmazione di sistemi a basso livello.

### Studenti

Rust è adatto agli studenti e a coloro che sono interessati a imparare i concetti dei sistemi.
Utilizzando Rust, molte persone hanno imparato argomenti come lo sviluppo di sistemi operativi.
La community è molto accogliente e felice di rispondere alle domande degli studenti.
Attraverso sforzi come questo libro, il team di Rust vuole rendere i concetti dei sistemi
accessibili a più persone possibili, specialmente a coloro che sono nuovi nell'ambito della programmazione.

### Compagnie

Centinaia di compagnie, piccole e grandi, usano Rust per svariati compiti, compresi strumenti
per CLI, servizi web, DevOps tooling, dispositivi embedded, analisi audio e video, transcoding,
crypto monete, bioinformatics, motori di ricerca, applicazioni IoT, machine learning e
addirittura per molte parti di Firefox.

### Sviluppatori Open Source

Rust è per le persone che vogliono sviluppare Rust, community, strumenti di sviluppo
e librerie. Apprezzeremo molto il tuo contributo nello sviluppo di Rust.

### Persone che danno importanza alla velocità e stabilità

Rust è per le persone che desiderano velocità e stabilità in un linguaggio di programmazione.
Per velocità, intendiamo sia la velocità con cui un programma scritto in Rust può essere eseguito,
sia la velocità con cui Rust consente di scrivere programmi. I controlli del compilatore di Rust
garantiscono la stabilità attraverso l'aggiunta di funzionalità e il refactoring.
Questo va in contrasto con il legacy code molto fragile presente spesso con linguaggi privi di questi controlli
che porta gli sviluppatori ad aver paura nel fare modifiche. Mirando alle astrazioni a costo zero,
cioè caratteristiche di alto livello che vengono compilate in codice a basso livello
altrettanto veloce del codice scritto manualmente, Rust si impegna a rendere il codice sicuro anche veloce.

Il linguaggio Rust spera di supportare pure molti altri utenti;
quelli menzionati qui sono solo alcuni dei principali interessati.
Nel complesso, l'ambizione più grande di Rust è eliminare i compromessi che i programmatori
hanno accettato per decenni, fornendo sicurezza *e* produttività, velocità *ed* ergonomia.
Dai una possibilità a Rust e vedi se le sue modalità fanno al caso tuo.

## Per chi è questo libro?

Questo libro presuppone che tu abbia già esperienza in qualche altro linguaggio di programmazione,
indipendentemente da quale sia. Abbiamo cercato di rendere il materiale per imparare ampiamente
accessibile a persone provenienti da diverse ambiti di programmazione. Non dedichiamo molto
tempo a parlare di cosa sia la programmazione o come pensarla. Se sei completamente nuovo alla
programmazione, sarebbe meglio leggere un libro che fornisca specificamente un'introduzione alla
programmazione.

## Come utilizzare questo libro?

In generale, questo libro presume che tu lo stia leggendo in modo sequenziale, dalla prima
all'ultima pagina. I capitoli successivi si basano sui concetti illustrati nei
capitoli precedenti e i capitoli precedenti potrebbero non approfondire dettagli
su un argomento specifico, ma torneranno sull'argomento in un capitolo successivo.

Troverai due tipi di capitoli in questo libro: capitoli sui concetti e capitoli di
progetto. Nei capitoli sui concetti, imparerai un concetto nuovo di Rust. Nei capitoli di
progetto, costruiremo piccoli programmi insieme, applicando ciò che hai imparato
fino a quel momento. I capitoli 2, 12 e 20 sono capitoli di progetto; tutti gli altri
sono capitoli sui concetti.

Il Capitolo 1 spiega come installare Rust, come scrivere un programma "Hello, world!"
e come utilizzare Cargo, il gestore dei pacchetti e strumento di compilazione di Rust.
Il Capitolo 2 è un'introduzione pratica alla scrittura di un programma in Rust, in cui
costruirai un gioco "indovina numero". Qui copriremo i concetti a un livello
elevato e nei capitoli successivi verranno forniti ulteriori dettagli. Se vuoi provarci
subito, puoi andare direttamente al Capitolo 2.
Il Capitolo 3 copre le caratteristiche di Rust simili a quelle di altri linguaggi di
programmazione e nel Capitolo 4 imparerai il sistema di "ownership" di Rust. Se sei
una persona particolarmente meticolosa che preferisce imparare ogni dettaglio
prima di passare al successivo, hai la possibilità di saltare il Capitolo 2 e passare
direttamente al Capitolo 3, tornando al Capitolo 2 quando desidererai lavorare su
un progetto applicando i dettagli appresi.

Il Capitolo 5 discute di classi (struct) e metodi, mentre il Capitolo 6 copre le
enum, le espressioni di `match` e il costrutto di flow control `if let`.
Utilizzerai classi (struct) ed enumerazioni per creare tipi personalizzati in Rust.

Nel Capitolo 7, imparerai il sistema dei moduli di Rust e le regole di privatezza
da seguire per organizzare il tuo codice e la sua API pubblica. Il Capitolo 8 discute
di alcune comuni strutture di dati fornite dalla libreria standard di Rust, come vettori,
stringhe e Hash Maps. Nel Capitolo 9 scopriremo come Rust gestisce gli errori e quindi la
sua filosofia.

Il capitolo 10 approfondisce i concetti dei tipi generici, traits e lifetimes,
che ti danno il potere di scrivere codice che può essere applicato su diversi
tipi. Il capitolo 11 è tutto sul testing, che seppur conoscendo le garanzie che offre
Rust è necessario per assicurare che la logica stessa del programma sia corretta.
Nel capitolo 12, creeremo una nostra implementazione per una sottoparte di
funzionalità dallo strumento CLI `grep` che cerca per del testo all'interno dei files.
Per questo, utilizzeremo molti dei concetti discussi nei capitoli precedenti.

Il capitolo 13 esplorerà le closures e gli iteratori: funzionalità di Rust
derivate da lingiuaggi di programmazione funzionali. Nel capitolo 14, esamineremo
Cargo più nel dettaglio e parleremo sulle pratiche migliori per condividere
le tue librerie con altri. Il capitolo 15 discuterà dei puntatori intelligenti
(smart pointers) che la libreria standard fornisce e dei traits che abiliteranno
le loro funzionalità.

Nel capitolo 16, parleremo di diversi modelli per la programmazione parallela
e di come Rust ti aiuta a programmare in multipli thread senza paura.
Il capitolo 17 mostra come gli idiomi di Rust si confrontano con gli
altri principi dell'OOP con cui potresti essere familiare.

Il capitolo 18 è un riferimento sui pattern e sul *pattern matching*, che sono
potenti metodi per esprimere idee attraverso i programmi Rust. Il capitolo 19
contiene svariati concetti avanzati di interesse, come l'unsafe Rust, le macro,
di più sui lifetimes, i trait, i tipi, le funzioni e le closures.

Nel capitolo 20, completeremo un progetto in cui implementeremo un web server
a basso livello con tanto di threads.

Alcuni appendici contengono informazioni utili sul linguaggio in un formato più
referenziale. L'appendice A lista le parole chiave di Rust, l'appendice B lista
gli operatori e i simboli, l'appendice C lista i trait derivabili forniti dalla
libreria standard, l'appendice D lista alcuni strumenti di sviluppo utili e
l'appendice E spiega le edizioni di Rust.
Nell'appendice F puoi trovare le traduzioni del libro e in quello G spiega come
Rust è creato e cos'è nighly Rust.

Non c'è un modo sbagliato di leggere questo libro: se vuoi saltare avanti, fai pure!
Potresti aver bisogno però di tornare su capitoli vecchi se hai confusione. Ma
fai ciò che ti è più comodo.

<span id="ferris"></span>

Un'importante parte del processo di studio di Rust è imparare come leggere i messaggi
di errore che il compilatore mostra: questi ti guideranno verso del codice funzionante.
Per questo, mostremo molti esempi di codice che non vengono compilati con il messaggio
di errore in ogni situazione. Sappi che che se copi ed esegui un esempio a caso,
potrebbe non compilarsi! Assicurati di leggere cosa c'è scritto vicino per capire
cosa sta cercando di fare l'esempio di codice che hai copiato e se deve dare errore.
Ferris ti aiuterà a distinguere il codice che non funziona come dovrebbe:

| Ferris                                                                                                           | Significato                                      |
|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|
| <img src="img/ferris/does_not_compile.svg" class="ferris-explain" alt="Ferris with a question mark"/>            | Questo codice non verrà compilato!               |
| <img src="img/ferris/panics.svg" class="ferris-explain" alt="Ferris throwing up their hands"/>                   | Questo codice panicherà!                         |
| <img src="img/ferris/not_desired_behavior.svg" class="ferris-explain" alt="Ferris with one claw up, shrugging"/> | Questo codice non darà il risulato aspettato.    |

La maggior parte delle volte, ti guideremo noi verso la versione corretta di ogni
codice che non viene compilato.

## Codice Sorgente

I file sorgente da cui questo libro è stato generato si possono trovare su
[GitHub][book].

[book]: https://github.com/rust-lang/book/tree/main/src
