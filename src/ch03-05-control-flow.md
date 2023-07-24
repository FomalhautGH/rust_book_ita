## Control Flow

La capacità di eseguire del codice in base ad una condizione e di eseguire del
codice ripetutamente finché una condizione è vera sono elementi fondamentali
nella maggior parte dei linguaggi di programmazione. I costrutti più comuni
che consentono di controllare il flusso di esecuzione del codice in Rust sono
le espressioni `if` e i `loop`.

### Espressioni `if`

Un espressione `if` consente di eseguire un blocco di codice in base a delle
condizioni. Dopo aver specificato una condizione si può dire: “Se questa
condizione è vera, esegui questo blocco di codice. Se la condizione è falsa,
non eseguire questo blocco di codice.”

Crea un nuovo progetto chiamato *branches* nella tua directory di progetti per
esplorare l'espressione if. Nel file *src/main.rs*, inserisci quanto segue:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-26-if-true/src/main.rs}}
```

Tutte le espressioni `if` iniziano con la keyword `if`, seguita da una condizione.
In questo esempio, la condizione controlla se la variabile `number` ha un valore
inferiore a 5. Subito dopo la condizione, inseriamo il blocco di codice da
eseguire se la condizione è vera (cioè se da come risultato `true`), racchiuso
tra parentesi graffe. I blocchi di codice associati alle espressioni `if` vengono
talvolta chiamati in inglese *arms* cioè bracci, proprio come i bracci nelle
espressioni match che abbiamo discusso nella sezione [“Confrontare il numero dato
come risposta al numero segreto”][comparing-the-guess-to-the-secret-number] del
Capitolo 2.

Opzionalmente, possiamo anche aggiungere un espressione `else`, come abbiamo
fatto nell'esempio, per fornire al programma un blocco alternativo di codice
da eseguire se la condizione da come risultato `false`. Se non aggiungi un
espressione `else` e la condizione è falsa, il programma semplicemente salta
il blocco di codice associato all'`if` e passa al prossimo pezzo di codice da
eseguire.

Prova as eseguire questo codice, il risultato sarà questo:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-26-if-true/output.txt}}
```

Proviamo a cambiare il valore di `number` per fare in modo che la condizione
risulti in `false` per vedere cosa succede:

```rust,ignore
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-27-if-false/src/main.rs:here}}
```

Esegui il programma ancora e guarda l'output:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-27-if-false/output.txt}}
```

È anche importante notare che la condizione in questo codice *deve* essere di tipo
`bool`. Se la condizione non è di tipo `bool`, otterremo un errore. Prova infatti
ad eseguire il seguente codice:

<span class="filename">Nome file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/src/main.rs}}
```

La condizione dell'`if` questa volta varrà `3`, quindi Rust ci darà errore:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-28-if-condition-must-be-bool/output.txt}}
```

L'errore indica che Rust si aspettava un `bool` ma ha trovato un intero. A differenza
di linguaggi come Ruby e JavaScript, Rust non proverà implicitamente a convertire tipi
non booleani in un booleano. Devi essere esplicito e fornire sempre all'espressione
`if` un valore booleano come condizione. Se vogliamo che il blocco di codice associato
all'`if` venga eseguito solo quando il numero non è uguale a `0`, possiamo modificare
l'espressione `if` in questo modo:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-29-if-not-equal-0/src/main.rs}}
```

Eseguire questo codice stamperà `number was something other than zero`.

#### Gestire più Condizioni con l'`else if`

Puoi usare multiple condizioni combinando gli `if` con gli `else` in una espressione
`else if`. Per esempio: 

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-30-else-if/src/main.rs}}
```

Questo programma ha quattro possibili percorsi. Dopo averlo eseguito, dovresti vedere
questo output:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-30-else-if/output.txt}}
```

Quando questo programma viene eseguito, viene controllata ogni espressione `if`
in sequenza e viene eseguito solo il primo blocco di codice che soddisfa la
condizione ed il resto non viene neanche controllato. Nota infatti come
anche se 6 è divisibile per 2, non vediamo l'output `number is divisible by 2`,
e neanche `number is not divisible by 4, 3, or 2` del blocco `else`.

Utilizzare troppe espressioni `else if` può rendere il codice disordinato,
quindi se ne hai più di una, potresti voler ristrutturare il codice. Il
Capitolo 6 spiega un potente costrutto fatto apposta per ciò, chiamato
`match`.

#### Utilizzare l'`if` in uno Statement `let`

Visto che l'`if` è un espressione, la possiamo utilizzare all'interno di uno
statement `let` nella parte destra per assegnare il valore risultante
ad una variabile, come nell'esempio 3-2.

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-02/src/main.rs}}
```

<span class="caption">Voce 3-2: Assegnare il risultato di una espressione `if` ad una
variabile </span>

Alla variabile `number` verrà assegnato un valore che dipende dell'esito dell'
espressione `if`. Esegui questo codice per vedere cosa succede:

```console
{{#include ../listings/ch03-common-programming-concepts/listing-03-02/output.txt}}
```

Ricorda che i blocchi di codice ritorneranno l'ultima espressione al loro interno
e i numeri stessi sono espressioni. In questo caso, il valore dell'intera
espressione `if` dipende da quale blocco di codice viene eseguito. Ciò significa
che i valori che possono essere ritornati da ciascun *braccio* dell'`if` devono
essere dello stesso tipo; nella Voce 3-2 ad esempio, i valori ritornati dal braccio
dell'`if` e dal braccio dell'`else` sono entrambi `i32`. Se i tipi non corrispondono,
come nell'esempio seguente, otterremo un errore:

<span class="filename">Nome file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/src/main.rs}}
```

Quando proviamo a compilare questo codice, otterremo un errore. Di fatti, i bracci
dell'`if` e dell'`else` ritornano valori non compatibili. Rust indicherà esattamente
dove trovare il problema nel programma:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-31-arms-must-return-same-type/output.txt}}
```

L'espressione ritornata dal blocco `if` è un intero, mentre l'espressione ritornata
dal blocco `else` è una stringa. Ciò non potrà funzionare perché le variabili devono
essere di un solo tipo e Rust ha bisogno di conoscere a compile time qual'è il tipo
esatto per la variabile `number`. Conoscendo il tipo di `number`, il compilatore
sarà in grado di verificare che il tipo sia valido in tutti i posti in cui
utilizziamo la variabile `number`. Rust non sarebbe in grado di fare tutto ciò
se il tipo della variabile `number` fosse determinato solo a runtime; il compilatore
in quel caso sarebbe soltanto più complesso, lento e farebbe meno garanzie sul
codice se dovesse tenere traccia di possibili tipi multipli per una variabile.

### Ripetizione con i Loop

È spesso utile poter eseguire un blocco di codice più di una volta. Per questa cosa,
Rust fornisce diversi *loop* ("cicli"), che eseguiranno il codice al loro interno
fino alla fine e dopo ripartiranno immediatamente dall'inizio dello stesso. Per
sperimentare con i loop, creiamo un nuovo progetto chiamato *loops*.

Rust ha ben tre tipi di loop: `loop`, `while` e `for`. Proviamoli uno per uno.

#### Ripetere il codice con `loop`

La keyword `loop` dice a Rust di eseguire un blocco di codice più e più volte all'infinito
fino a quando non gli dici esplicitamente di fermarsi.

Come esempio, modifica il file *src/main.rs* nella tua cartella *loops* in questo modo:

<span class="filename">Nome file: src/main.rs</span>

```rust,ignore
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-32-loop/src/main.rs}}
```

Quando eseguiamo questo programma, vedremo stampare continuamente `again!` fino a quando
non chiudiamo il processo manualmente. La maggior parte dei terminali supporta la shortcut
<span class="keystroke">ctrl-c</span> per interrompere un programma che è bloccato in un
loop costante. Provaci:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-32-loop
cargo run
CTRL-C
-->

```console
$ cargo run
   Compiling loops v0.1.0 (file:///projects/loops)
    Finished dev [unoptimized + debuginfo] target(s) in 0.29s
     Running `target/debug/loops`
again!
again!
again!
again!
^Cagain!
```

Il simbolo `^C` rappresenta dove hai premuto <span class="keystroke">ctrl-c</span>.
Potresti o meno vedere la parola `again!` stampata anche dopo il `^C`, ciò dipende
su dov'era il codice che stava venendo eseguito nel loop quando ha ricevuto il
segnale di interrompersi.

Ovviamente, Rust ti permette di uscire da un ciclo utilizzando del codice. Puoi
piazzare la keyword `break` all'interno del loop per dire al programma quando
fermare l'esecuzione del loop. Ricorda che lo abbiamo fatto anche nel guessing
game nella sezione [“Quittare dopo la Risposta Corretta”][quitting-after-a-correct-guess]
del Capitolo 2 per uscire dal programma quando l'utente vince indovinando il
numero corretto.

Abbiamo anche utilizzato la keyword `continue` nel guessing game, che all'interno
di un loop dice di skippare tutto il codice rimanente e passare subito alla
prossima iterazione.

#### Ritornare valori da un loop

Uno degli utilizzi di un `loop` è quello di ripetere un'operazione che potrebbe fallire,
come ad esempio controllare se un thread ha completato il suo lavoro o meno.
Potresti anche avere la necessità di passare il risultato di quell'operazione
al di fuori del loop per il resto del tuo codice. Per fare ciò, puoi aggiungere
il valore che desideri ritornare dopo l'espressione `break` che interrompe il loop
ritornando quel valore in modo che tu possa utilizzarlo, come
mostrato qui:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-33-return-value-from-loop/src/main.rs}}
```

Prima del loop, dichiariamo una variabile chiamata `counter` e la inizializziamo
a `0`. Successivamente dichiariamo una variabile chiamata `result` per contenere il
valore restituito dal loop. Ad ogni iterazione del loop, incrementiamo di `1` la
variabile `counter` e poi controlliamo se `counter` è uguale a `10`. Quando lo è,
utilizziamo la parola chiave `break` seguita dal valore `counter * 2`. Dopo il loop,
utilizziamo un punto e virgola per terminare lo statement che assegna il valore
a `result`. Infine, stampiamo il valore di `result`, che in questo caso sarà `20`.

#### "Etichette" dei Loop per disambiguare tra più Loop

Se hai dei loop annidati in altri loop, `break` e `continue` vengono applicati al loop
più interno. Puoi opzionalmente specificare una *etichetta* (in inglese "label") su
un loop in modo che potrai utilizzare le keyword `break` e `continue` specificatamente
su quel loop invece che sul loop più interno. I nomi delle etichette devono iniziare
con un apostrofo. Ecco un esempio con due loop annidati:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/src/main.rs}}
```

Il loop esterno ha l'etichetta `'counting loop`, e contera da 0 fino a 2. Il loop più
interno senza etichetta conta alla rovescia da 10 a 9. Il primo `break` che non specifica
alcuna etichetta fermerà soltanto il loop più interno. Invece lo statement `break 'counting loop;`
fermerà il loop esterno. Questo codice stampa:

```console
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-32-5-loop-labels/output.txt}}
```

#### Cicli Condizionali con il `while`

Spesso un programma ha bisogno di verificare una condizione all'interno di
un loop. Finché la condizione è vera, il loop continua. Quando la condizione
diventa falsa, il programma usa `break`, interrompendo il loop. È possibile
implementare questo comportamento utilizzando una combinazione di `loop`,
`if`, `else` e `break`; se vuoi, puoi provare a farlo ora in un programma.
Tuttavia, questo pattern è così comune che Rust ha un costrutto integrato
per questo scopo, chiamato ciclo `while`. Nella Voce 3-3, utilizziamo il
`while` per eseguire un pezzo di codice tre volte, contando alla rovescia
ogni volta, e poi, dopo il loop, stampiamo un messaggio ed usciamo.

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-03/src/main.rs}}
```

<span class="caption">Voce 3-3: Utilizzare un ciclo `while` per eseguire
del codice finchè una condizione è vera</span>

Questo cotrutto elimina molto annidamento che risulterebbe necessario se si
utilizzassero `loop`, `if`, `else` e `break`. In poche parole se la condizione è vera
il loop continua; altrimenti smette.

#### Iterare attraverso una Collezione con il `for`

Volendo puoi utilizzare il `while` per iterare attraverso degli elementi di una
collezione di dati, come ad esempio un array. Ad esempio, il loop nella Voce 3-4
stampa ogni elemento dell'array `a`.

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-04/src/main.rs}}
```

<span class="caption">Voce 3-4: Iterare attraverso gli elementi di una collezione
di dati usando un ciclo `while`</span>

Qui, il codice "conta" attraverso gli elementi dell'array. Inizia dall'indice `0`
e continua a iterare fino a quando non raggiunge l'ultimo indice dell'array (ovvero
fino a quando la condizione `index < 5` non è più vera). Eseguendo questo codice
verranno stampati tutti gli elementi dell'array:

```console
{{#include ../listings/ch03-common-programming-concepts/listing-03-04/output.txt}}
```

Tutti e cinque i valori dell'array vengono stampati nel terminale, come previsto.
Anche se la variabile `index` raggiungerà eventualmente il valore `5`, il ciclo
infatti si interromperà prima di cercare stampare un sesto valore dall'array.

Tuttavia, questo approccio è error prone; potremmo far panicare il programma se
il valore dell'indice o la condizione non sono corretti. Ad esempio, se si
cambiasse la definizione dell'array `a` in modo che abbia quattro elementi ma
ci si dimentica di aggiornare anche la condizione a `while index < 4`, il codice
panicherà. Inoltre, questo approccio è meno performante perché il compilatore
aggiunge del codice a runtime per verificare se l'indice si trova all'interno
dei limiti dell'array ad ogni iterazione del loop.

Come alternativa più concisa, è possibile utilizzare un ciclo `for` per eseguire
del codice per ogni elemento di una collezione di dati. Un ciclo `for` è mostrato
ad esempio nella Voce 3-5.

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-05/src/main.rs}}
```

<span class="caption">Voce 3-5: Iterare attraverso ogni elemento di una collezione
di dati con il ciclo `for`</span>

Quando eseguiamo questo codice, vedremo lo stesso output della Voce 3-4. Ma
più importante, abbiamo anche aumentato la sicurezza del codice ed eliminato
la possibilità di errori che potrebbero derivare dal superare la fine dell'array
o dal fermarsi prima e perdere alcuni elementi.

Utilizzando il ciclo `for`, non dovremmo ricordarci sempre di modificare del
codice se cambiamo il numero di valori presenti nell'array, come invece
sarebbe necessario nel metodo utilizzato nella Voce 3-4.

La sicurezza e la concisione dei cicli `for` li rendono il costrutto ciclico
più comunemente utilizzato in Rust. Anche in situazioni in cui si desidera
eseguire del codice un certo numero di volte, come nell'esempio del conto
alla rovescia che utilizzava un ciclo `while` nella Voce 3-3, la maggior parte
dei Rustaceans utilizzerebbe un ciclo `for`. Il modo per farlo sarebbe quello
di utilizzare un `Range`, fornito dalla libreria standard, che genera tutti
i numeri in sequenza a partire da un numero e termina prima di un altro numero.

Ecco come sarebbe diventato il conto alla rovescia utilizzando un ciclo
`for` e un altro metodo di cui non abbiamo ancora discusso, `rev`, per
invertire il range.

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-34-for-range/src/main.rs}}
```

Questo codice è un più carino, non è vero?

## Riepilogo

Ci sei riuscito! Questo era un capitolo bello grosso. Hai imparato le variabili,
dati singoli, dati composti, tipi, funzioni, commenti, espressioni `if` e cicli!
Per allenarti con i concetti discussi in questo capitolo, prova a scrivere dei
programmi che fanno ciò:

* Un convertitore tra Fahrenheit e Celsius
* Un generatore del numero *n* nella serie di Fibonacci.
* Un programma che stampa le lyrics del canto natalizio “The Twelve Days of Christmas”,
  avvantaggiandosi del fatto che c'è molta ripetizione nella canzone.

Quando sei pronto ad andare avanti, parleremo di un concetto in Rust che *non* esiste
normalmente in altri linguaggi: l'ownership.

[comparing-the-guess-to-the-secret-number]:
ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[quitting-after-a-correct-guess]:
ch02-00-guessing-game-tutorial.html#quitting-after-a-correct-guess
