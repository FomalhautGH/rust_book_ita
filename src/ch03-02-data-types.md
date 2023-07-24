## Tipi di Dato

Ogni valore in Rust è di un certo *tipo*, ciò specifica a Rust che tipo di
dati si sta utilizzando in modo che sappia come lavorarci. Parleremo di
due sottocategorie di tipi: gli *scalar* e *compound*.

Tieni presente che Rust è un linguaggio di programmazione *scritto staticamente*,
il che significa che deve conoscere i tipi di tutte le variabili durante la
compilazione. Il compilatore di solito è in grado di dedurre il tipo che vogliamo
utilizzare in base al valore stesso e al modo in cui lo stiamo utilizziamo. Nei
casi in cui sono possibili diversi tipi, come quando abbiamo convertito una stringa
in un numero utilizzando il metodo `parse` nella sezione [“Comparing the Guess
to the Secret Number”][comparing-the-guess-to-the-secret-number] nel Capitolo 2,
dobbiamo specificare il tipo, come segue:

```rust
let guess: u32 = "42".parse().expect("Not a number!");
```

Se non aggiungiamo il `: u32` dopo la variabile come nel codice appena mostrato,
Rust ci accoglierà con il seguente errore. Ciò significa che il compilatore ha
bisogno di più informazioni da noi sul tipo che vogliamo utilizzare:

```console
{{#include ../listings/ch03-common-programming-concepts/output-only-01-no-type-annotations/output.txt}}
```

In seguito vedrai diversi modi con cui potrai specificare il tipo per altri tipi
di dato.

### Scalar

Uno *scalar* rappresenta un singolo valore. Rust ha quattro tipi *scalar* principali: interi, reali, booleani e caratteri. Potresti riconoscerli da altri linguaggi di programmazione. Vediamo come funzionano però in Rust.

#### Interi

Un *intero* è un numero senza la parte frazionaria. Abbiamo utilizzato un
intero nel Capitolo 2, lo `u32`. Questo tipo di intero indica che il
valore associato deve essere un intero senza segno (gli interi con segno
iniziano con `i` invece di `u`) che occupa 32 bit di spazio in memoria. La
Tabella 3-1 mostra vari interi utilizzabili integrati in Rust. Possiamo
utilizzare una qualsiasi di queste varianti per dichiarare un intero.

<span class="caption">Table 3-1: Varianti di intero in Rust</span>

| Lunghezza  | Signed  | Unsigned |
|------------|---------|----------|
| 8-bit      | `i8`    | `u8`     |
| 16-bit     | `i16`   | `u16`    |
| 32-bit     | `i32`   | `u32`    |
| 64-bit     | `i64`   | `u64`    |
| 128-bit    | `i128`  | `u128`   |
| arch       | `isize` | `usize`  |

Ogni variante può essere sia con segno (*signed*) che senza segno (*unsigned*)
e ha una dimensione esplicita. Con *signed* e *unsigned* si fa riferimento alla
possibilità che il numero sia negativo o meno, in altre parole, se il numero ha
bisogno di un segno (*signed*) o se sarà sempre positivo (*unsigned*).
È simile a scrivere numeri su carta:
quando il segno è importante, un numero viene mostrato con un segno **+** o un
segno **-**; tuttavia, quando è possibile presumere che il numero sia sempre
positivo, viene mostrato senza segno. I numeri con segno vengono memorizzati
utilizzando la rappresentazione [two’s complement][twos-complement].

Ogni variante con segno può memorizzare numeri da -(2<sup>n - 1</sup>) a 2<sup>n -
1</sup> - 1, dove *n* è il numero di bit utilizzati da quella variante di
intero. Quindi ad esempio un `i8` può memorizzare numeri da -(2<sup>7</sup>)
a 2<sup>7</sup> - 1, che corrisponde a -128 fino a 127. Le varianti senza
segno possono invece memorizzare numeri da 0 a 2<sup>n</sup> - 1, quindi
ad esempio un u8 può memorizzare numeri da 0 a 2<sup>8</sup> - 1, che corrisponde
a 0 fino a 255.

Inoltre, gli interi `isize` e `usize` dipendono dall'architettura del
computer su cui viene eseguito il tuo programma, indicato nella tabella
come "arch": 64 bit se si tratta di un'architettura a 64 bit e 32 bit
se si tratta di un'architettura a 32 bit.

Puoi scrivere i *literal* numerici in un modo qualsiasi tra quelli
mostrati nella Tabella 3-2. Ricorda che i *literal* numerici che
possono corrispondere a più tipi numerici consentono il suffisso per
specificare il tipo, come ad esempio `57u8`. I *literal* numerici
possono anche utilizzare il simbolo `_` come separatore visivo per
rendere più leggibile il numero, ad esempio `1_000`, che avrà lo
stesso valore di `1000`.

<span class="caption">Table 3-2: Literal Interi in Rust </span>

| Literal              | Esempio       |
|----------------------|---------------|
| Decimal              | `91_242`      |
| Hex                  | `0xfe`        |
| Octal                | `0o73`        |
| Binary               | `0b1011_0100` |
| Byte (solo per `u8`) | `b'A'`        |

Quindi come si fa a sapere quale intero utilizzare? Se non lo sai, il predefinito
di Rust è solitamente un buon punto di partenza: il prendefinito è `i32`. La
situazione principale in cui si utilizzerebbe `isize` o `usize` è quando si
indicizza qualche tipo di collezione di dati.

> ##### Overflow Intero
>
> Supponiamo di avere una variabile di tipo `u8` che può quindi contenere valori
> compresi tra 0 e 255. Se provi a modificare la variabile con un valore al di
> fuori di tale intervallo, ad esempio 256, si verificherà un overflow, che può
> comportare due diversi comportamenti. Quando si compila in debug Rust controllerà
> se ci sono overflow che possono far *panicare* il tuo programma a runtime. Rust
> utilizza il termine *panicare* quando un programma termina con un errore;
> discuteremo in modo più approfondito del *panico* nella sezione degli [“Errori
> Unrecoverable con `panic!`”][unrecoverable-errors-with-panic] nel Capitolo 9.
>
> Quando compili invece in modalità di "release" con `--release`, Rust non controllerà
> se ci sono overflow di interi che possono far *panicare* il programma. Invece, in
> caso overflow, Rust esegue il *wrapping del two's complement*. In breve, i valori
> superiori al valore massimo che il tipo può contenere vengono settati al valore
> minimo che il tipo può avere. Nel caso di un `u8`, il valore 256 diventa 0, il
> valore 257 diventa 1 e così via. Il programma non panicherà, ma la variabile avrà
> un valore che probabilmente non è quello che ti aspettavi. Fare affidamento su
> questo comportamento è considerato un errore.
>
> Per gestire in modo esplicito il rischio di overflow, puoi utilizzare queste
> famiglie di metodi forniti dalla libreria standard per i tipi primitivi numerici:
>
> * Fai le operazioni utilizzando i metodi `wrapping_*`, come `wrapping_add`.
> * Ritornare il valore `None` se c'è un overflow con i metodi `checked_*`.
> * Ritornare il valore e un booleano indicante la presenza o meno di
>   overflow con i metodi `overflowing_*`.
> * Evita che i valori vadano fuori range bloccandoli al loro valore massimo
>   o minimo con i metodi `saturating_*`.

#### Reali

Rust ha anche due tipi primitivi per i *numeri reali* (i float), che sono i
seguenti: `f32` e `f64`, che sono grandi rispettivamente 32 bit e 64 bit. Il
tipo predefinito è `f64` perché sui processori moderni performa approssimativamente
alla stessa velocità di un `f32` ma è in grado di offrire una maggiore precisione.
A tutti i float si può specificare il segno.

Ecco un esempio che mostra le variabili float:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-06-floating-point/src/main.rs}}
```

I float sono rappresentati secondo lo standard IEEE-754. Il tipo `f32` è un
float a precisione singola, mentre l'`f64` ha precisione doppia.

#### Operazioni numeriche

Rust supporta le operazioni matematiche di base che ci si aspetterebbe per tutti
i tipi di numeri: addizione, sottrazione, moltiplicazione, divisione e resto. La
divisione tra interi approssima all'intero più vicino. Il seguente codice mostra
come utilizzare ogni operazione numerica in una dichiarazione `let`:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-07-numeric-operations/src/main.rs}}
```

Ogni espressione in queste dichiarazioni utilizza un operatore matematico e risulterà
in un valore singolo, che verrà poi assegnato alla variabile. [Appendix B][appendix_b]
contiene una lista di tutti gli operatori che Rust supporta.

#### Il tipo bool

Come nella maggior parte degli altri linguaggi di programmazione, in Rust il tipo di
dato booleano ha due possibili valori: `true` o `false`. I valori booleani occupano
un byte di spazio. Il tipo booleano in Rust è specificato utilizzando la keyword `bool`.
Ad esempio:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-08-boolean/src/main.rs}}
```

Il modo in cui i booleani vengono utilizzati di più è attraverso i condizionali,
come un espressione `if`. Vedremo come le espressioni `if` funzionano in Rust
nella sezione [“Control Flow”][control-flow].

#### Il tipo carattere

Il tipo `char` in Rust è il suo più primitivo tipo alfabetico. Ecco qualche esempio
di come dichiarare variabili `char`:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-09-char/src/main.rs}}
```

Nota come specifichiamo i *literal* `char` con gli apici singoli (''), a
differenza dei *literal* stringa, che utilizzano le doppie virgolette ("").
Il tipo `char` in Rust ha una dimensione di quattro byte e rappresenta un
singolo valore Unicode, il che significa che può rappresentare molto più di
quanto faccia l'ASCII. Lettere accentate, caratteri cinesi, giapponesi e coreani,
emoji e spazi vuoti sono tutti valori validi per il tipo primitivo `char` in Rust.
I valori Unicode vanno da `U+0000` fino a `U+D7FF` e da `U+E000` fino a `U+10FFFF`
inclusi. Tuttavia, un "carattere" non è un concetto definito in un modo preciso
in Unicode, quindi l'intuizione umana su cosa sia un "carattere" potrebbe non
coincidere con ciò che è un char in Rust. Discuteremo in dettaglio di
questo argomento nella sezione [“Memorizzare testo UTF-8 con le Stringhe”][strings]
nel Capitolo 8.

### Tipi composti

I *tipi composti* possono raggruppare diversi valori in un solo tipo. Rust ha
due tipi primitivi composti: le tuple e gli array.

#### The Tuple Type

Una *tupla* è un modo generale di raggruppare insieme un certo numero di valori
con tipi diversi in un unico tipo composto. Le tuple hanno una lunghezza fissa:
una volta dichiarate, non possono crescere o rimpicciolire.

Le tuple si creano scrivendo una lista di valori separati da virgole all'interno
di parentesi. Ogni posizione nella tupla ha un tipo, e i tipi dei diversi valori
nella tupla non devono necessariamente essere gli stessi. In questo esempio è
stata aggiunta la specifica del tipo opzionale per questa tupla:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-10-tuples/src/main.rs}}
```

La variabile `tup` viene legata all'intera tupla perché una tupla è considerata un
singolo elemento composto. Per ottenere i singoli valori da una tupla, possiamo
utilizzare il *pattern matching* per destrutturare i valori di una tupla, come segue:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-11-destructuring-tuples/src/main.rs}}
```

Questo programma crea inizialmente una tupla e la lega alla variabile `tup`.
Successivamente, utilizza un pattern con il `let` per prendere `tup` e suddividerla
in tre variabili separate, `x`, `y` e `z`. Questo processo è chiamato *destrutturazione*
(in inglese "destructuring") perché divide la singola tupla in tre parti. Infine,
il programma stampa il valore di `y`, che è `6.4`.

Possiamo anche accedere direttamente a un elemento di una tupla utilizzando la
*dot notation* (`.`) seguita dall'indice del valore che intendiamo accedere. Ad esempio:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-12-tuple-indexing/src/main.rs}}
```

Questo programma crea la tupla `x` e accede a ciascun elemento della tupla
utilizzando i rispettivi indici. Come nella maggior parte dei linguaggi di
programmazione, il primo indice di una tupla è 0.

La tupla senza alcun valore ha un nome speciale, *unit*. Questo valore e il
relativo tipo sono entrambi scritti come `()` e rappresentano un valore o un
return vuoto. Le espressioni implicitamente restituiscono il valore unit se
non restituiscono nessun altro valore.

#### L'Array

Un altro modo per avere una collezione di valori è con un *array*.
A differenza di una tupla, gli elementi di un array devono essere
omogenei (stesso tipo). A differenza degli array in alcuni altri
linguaggi, gli array in Rust hanno una lunghezza fissa.

Gli array vanno scritti come una lista separata da virgole all'interno
di parentesi quadre:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-13-arrays/src/main.rs}}
```

Gli array sono utili quando si desidera allocare i dati nella stack anziché
nella heap (discuteremo della stack e della heap in modo più dettagliato nel
[Capitolo 4][stack-and-heap]) o quando si desidera garantire di avere sempre
un numero fisso di elementi. Tuttavia, un array non è flessibile come il
vector. Un *vector* è un tipo di collezione simile fornito dalla libreria
standard che *può* crescere o rimpicciolire in dimensione. Se non sei sicuro
se utilizzare un array o un vector, probabilmente dovresti utilizzare un
vector. Nel [Capitolo 8][vectors] verranno discusse in modo più dettagliato
le caratteristiche dei vector.

Tuttavia, gli array sono più utili quando si conosce il numero di elementi
il cui non avrà bisogno di cambiare. Ad esempio, se si vogliono memorizzare
i nomi dei mesi in un programma, probabilmente si utilizzerà un array anziché
un vector perché si sa che conterrà sempre 12 elementi:

```rust
let mesi = ["Gennaio", "Febbraio", "Marzo", "Aprile", "Maggio", "Giugno", "Luglio",
              "Agosto", "Settembre", "Ottobre", "Novembre", "Dicembre"];
```

Per specificare il tipo di un array si utilizzano le parentesi quadre con
il tipo di ciascun elemento, un punto e virgola e il numero di elementi
nell'array, in questo modo:

```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

Qui, `i32` è il tipo di ogni elemento. Dopo il punto e virgola, il numero
5 indica che l'array contiene cinque elementi.

È anche possibile inizializzare un array contenente lo stesso valore per
ogni elemento specificando il valore iniziale, seguito da un punto e
virgola la lunghezza dell'array tra parentesi quadre, come mostrato qui:

```rust
let a = [3; 5];
```

L'array chiamato `a` conterrà `5` elementi, tutti inizializzati a `3`.
Sarebbe come scrivere `let a = [3, 3, 3, 3, 3];`, ma in modo più conciso.

##### Accedere gli elementi dell'array

Un array è un singolo blocco di memoria di dimensione fissa, nota, che
può quindi essere allocato nello stack. Puoi accedere gli elementi di
un array utilizzando l'indice, come segue:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-14-array-indexing/src/main.rs}}
```

In questo esempio, la variabile chiamata `first` avrà il valore `1`
perché è il valore all'indice `[0]` dell'array. La variabile chiamata
`second` invece avrà il valore `2` dall'indice `[1]` dell'array.

##### Accesso invalido degli elementi di un array

Vediamo cosa succede se si prova ad accedere un elemento dell'array
che si trova oltre la fine dell'array. Immagina di eseguire questo
codice simile al "guessing game" nel Capitolo 2 per accedere ad un
elemento dell'array:

<span class="filename">Nome file: src/main.rs</span>

```rust,ignore,panics
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access/src/main.rs}}
```

Questo codice viene compilato senza problemi. Se infatti esegui questo
codice utilizzando `cargo run` e inserisci `0`, `1`, `2`, `3` o `4`, il
programma stamperà il valore corrispondente a quell'indice nell'array. Se
però inserisci un numero oltre la fine dell'array, ad esempio `10`, vedrai
questo output:

<!-- manual-regeneration
cd listings/ch03-common-programming-concepts/no-listing-15-invalid-array-access
cargo run
10
-->

```console
thread 'main' panicked at 'index out of bounds: the len is 5 but the index is 10', src/main.rs:19:19
note: run with `RUST_BACKTRACE=1` environment variable to display a backtrace
```

Il programma ha generato un errore a *runtime* nel momento in cui è stato
utilizzato un valore non valido per accedere al valore dell'array. Il
programma ha panicato mostrando un messaggio di errore e non ha eseguito
l'istruzione `println!` finale. Quando si tenta di accedere a un elemento
utilizzando l'indice, Rust verifica che l'indice specificato sia inferiore
alla lunghezza dell'array. Se l'indice è maggiore o uguale alla lunghezza,
Rust genererà un errore ("panica"). Questo controllo deve avvenire durante
l'esecuzione, specialmente in questo caso, poiché il compilatore non può
sapere in anticipo quale valore l'utente inserirà.

Questo è un esempio dei principi di sicurezza della memoria di Rust in azione.
In molti linguaggi di basso livello, questo tipo di controllo non viene
effettuato e, quando si fornisce un indice non corretto, si può accedere a
memoria non valida. Rust ti protegge da questo tipo di errore fermando
immediatamente il programma anziché permettere l'accesso a memoria non
valida e continuare l'esecuzione dello stesso. Nel Capitolo 9 si discuterà
ulteriormente della gestione degli errori in Rust e di come sia possibile
scrivere codice leggibile e sicuro che eviti sia il panico che l'accesso a
memoria non valida.

[comparing-the-guess-to-the-secret-number]:
ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[twos-complement]: https://it.wikipedia.org/wiki/Complemento_a_due
[control-flow]: ch03-05-control-flow.html#control-flow
[strings]: ch08-02-strings.html#storing-utf-8-encoded-text-with-strings
[stack-and-heap]: ch04-01-what-is-ownership.html#the-stack-and-the-heap
[vectors]: ch08-01-vectors.html
[unrecoverable-errors-with-panic]: ch09-01-unrecoverable-errors-with-panic.html
[appendix_b]: appendix-02-operators.md
