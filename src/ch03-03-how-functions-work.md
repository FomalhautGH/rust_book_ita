## Funzioni

Le funzioni vengono utilizzate molto. Precedentemente avrai già potuto notare
una delle funzioni più importanti di Rust: la funzione `main`, che è il punto
dove la maggior parte dei programmi inizia. Hai già anche visto la keyword
`fn`, che ti permette di dichiarare nuove funzioni.

In Rust si usa lo standard *snake case* per i nomi delle funzioni e variabili,
in cui tutte le lettere sono in minuscolo e gli underscore separano le parole
(like_this). Ecco un esempio di programma che contiene una funzione:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-16-functions/src/main.rs}}
```

Possiamo quindi definire una funzione in Rust scrivendo `fn`, seguito dal nome
della funzione e da una coppia di parentesi tonde. Le parentesi graffe indicano
al compilatore dove inizia e termina lo *scope* della funzione.

Possiamo chiamare qualsiasi funzione che abbiamo definito inserendo il suo nome
seguito da una coppia di parentesi. Poiché `another_function` è definita nel
programma, può essere chiamata all'interno della funzione `main`. Nota che
abbiamo definito `another_function` *dopo* la funzione `main` nel codice sorgente;
avremmo potuto anche definirla prima. A Rust non interessa dove definisci le tue
funzioni, ma solo che siano definite in uno scope visibile per la funzione chiamante.

Iniziamo un nuovo progetto binario chiamato *functions* per esplorare
ulteriormente le funzioni. Copia l'esempio di `another_function` in *src/main.rs*
ed eseguilo. Dovresti vedere l'output seguente:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-16-functions/output.txt}}
```

Le righe vengono eseguite nell'ordine in cui sono scritte nella funzione
`main`. Prima viene stampato il messaggio “Hello, world!” e dopo viene
chiamata la funzione `another_function` e viene stampato il suo messaggio.

### Parametri

Possiamo ovviamente definire anche funzioni che prendono *parametri*. Quando
una funzione prende parametri, è possibile fornire valori concreti per quei
parametri. In linguaggio tecnico i valori concreti sono chiamati *argomenti*,
ma in conversazioni informali, le persone tendono a usare indifferentemente i
termini *parametro* e *argomento* sia per le variabili nella definizione di
una funzione che per i valori concreti passati durante la chiamata di una
funzione.

In questa versione di `another_function` aggiungiamo un parametro:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/src/main.rs}}
```

Se provi ad eseguire questo programma dovresti ottenere l'output seguente:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-17-functions-with-parameters/output.txt}}
```

Nella dichiarazione di `another_function` ora si può specificare un parametro
chiamato `x`. Il tipo di `x` è segnato come `i32`. Quando passiamo il valore
`5` a `another_function`, la macro `println!` inserisce il valore `5` al posto
delle parentesi graffe che contengono `x` nella stringa format.

Nella dichiarazione delle funzioni, è *obbligatorio* specificare il tipo di
ciascun parametro. Questa è una scelta di Rust: richiedere il tipo nelle
dichiarazione delle funzioni significa che il compilatore quasi mai ha bisogno
che tu li debba utilizzare altrove nel codice per capire di quale tipo si
tratta. Il compilatore è inoltre in grado di fornire messaggi di errore
migliori se conosce i tipi che la funzione si aspetta.

In caso di parametri multipli, separa i parametri con le virgole,
come mostrato qui:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/src/main.rs}}
```

Questo esempio crea una funzione chiamata `print_labeled_measurement` con
due parametri. Il primo parametro si chiama `value` ed è di tipo `i32`. Il
secondo si chiama `unit_label` ed è di tipo `char`. La funzione quindi
stamperà una stringa contenente sia il valore che l'unità di misura.

Proviamo quindi ad eseguire questo codice. Sostituisci il programma attualmente
presente nel file *src/main.rs* del tuo progetto *functions* con l'esempio
appena mostrato ed eseguilo utilizzando cargo run:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-18-functions-with-multiple-parameters/output.txt}}
```

Dato che abbiamo richiamato la nostra funzione con `5` come valore per `value`
e `'h'` come valore per `unit_label`, l'output del programma conterrà questi
valori.

### Statements e Espressioni

I corpi delle funzioni sono composti da una serie di *statements* che opzionalmente
terminano con un espressione. Finora, le funzioni di cui abbiamo parlato non
includevano un espressione alla fine, ma hai già visto un'espressione come parte
di uno statement. Poiché Rust è un linguaggio basato sulle espressioni, questa è
una distinzione importante da imparare. Altri linguaggi non hanno le stesse
distinzioni, quindi vediamo cosa sono gli statements, le espressioni e come le loro
differenze influenzano come vengono scritte le funzioni.

* Gli **statements** sono istruzioni che svolgono un azione e non ritornano nessun valore.
* Le **espressioni** invece risulteranno in un valore. Guardiamo qualche esempio.

Abbiamo già utilizzato entrambe le cose. Ad esempio creare e assegnare un valore
ad una variabile con la keyword `let` è uno statement. Nel codice 3-1, `let y = 6`;
è uno statement.

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/listing-03-01/src/main.rs}}
```

<span class="caption">Listing 3-1: A `main` function declaration containing one statement</span>

Le dichiarazioni delle funzioni sono anche degli statement; l'intero esempio precedente è uno statement.

Gli statement non restituiscono valori. Pertanto, non è possibile assegnare uno statement
`let` a un'altra variabile, come cerca di fare il seguente codice; otterrai infatti un errore:

<span class="filename">Nome file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/src/main.rs}}
```

Quando eseguirai questo programma. l'errore che otterrai sarà questo:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-19-statements-vs-expressions/output.txt}}
```

Lo statement `let y = 6` non restituisce un valore, quindi non c'è nessun valore
a cui `x` possa essere associato. Questo è diverso da quello che accade in altri
linguaggi, come C e Ruby, in cui l'assegnazione restituisce il valore stesso
dell'assegnazione. In quei linguaggi, è possibile scrivere `x = y = 6` e sia `x`
che `y` avranno il valore `6`; questo non si può fare in Rust.

Le espressioni invece restituiscono un valore e costituiscono la maggior parte del
codice che scriverai in Rust. Considera un'operazione matematica, come `5 + 6`, che
è un espressione equivalente al valore `11`. Le espressioni possono anche far parte
degli statement: nell'esempio 3-1, il `6` nell'istruzione `let y = 6`; è
un'espressione equivalente al valore `6`. Richiamare una funzione è un'espressione.
Richiamare una macro è un'espressione. In generale uno scope creato con le parentesi graffe è
un'espressione, ad esempio:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-20-blocks-are-expressions/src/main.rs}}
```

Questa espressione:

```rust,ignore
{
    let x = 3;
    x + 1
}
```

è uno scope che, in questo caso, vale `4`. Quel valore viene associato a `y`
come parte dell'istruzione `let`. Nota come la riga di codice `x + 1` non ha
un punto e virgola alla fine, a differenza della maggior parte delle righe di
codice che hai visto finora. Le espressioni infatti non includono punti e
virgola finali. Se aggiungi un punto e virgola alla fine di un espressione,
la trasformi in uno statement e non restituirà alcun valore. Tieni presente
questo mentre impari i valori di ritorno delle funzioni e le espressioni
spiegate in seguito.

### Funzioni con Valori di Ritorno

Le funzioni possono restituire dei valori al codice che le richiama. Non dobbiamo
specificare nomi per i valori ritornati, ma dobbiamo specificare il loro tipo dopo
la freccia (`->`). In Rust, il valore di ritorno di una funzione è il valore
dell'espressione stessa composta dall'intera funzione. È possibile ritornare in
anticipo da una funzione utilizzando la keyword `return` e specificando un valore,
ma la maggior parte delle funzioni restituisce in modo implicito l'ultima espressione.
Ecco un esempio di una funzione che restituisce un valore:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/src/main.rs}}
```

Non vengono richiamate funzioni, macro e non ci sono neanche `let` statements
nella funzione `five`, c'è soltanto il numero `5` da solo. Questa è una funzione
perfettamente valida in Rust. Nota che il tipo del valore ritornato della
funzione è specificato anche come `-> i32`. Prova ad eseguire questo codice;
l'output sarà questo:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-21-function-return-values/output.txt}}
```

Il `5` nella funzione `five` è il valore ritornato, motivo per cui il tipo dopo
la freccia è `i32`. Esaminiamo questo più nel dettaglio. Ci sono due parti
importanti: la prima è la linea di codice `let x = five();` che mostra che
stiamo utilizzando il valore di ritorno di una funzione per inizializzare
una variabile. Poiché la funzione five restituisce un `5`, quella linea
di codice è equivalente alla seguente:

```rust
let x = 5;
```

La seconda è che la funzione `five` non ha parametri e specifica il tipo
del valore ritornato, infatti il corpo della funzione è un solitario `5`
senza punto e virgola perché è un'espressione di cui vogliamo ritornare
il valore.

Guardiamo un'altro esempio:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-22-function-parameter-and-return/src/main.rs}}
```

L'esecuzione di questo codice stamperà `The value of x is: 6`. Ma se inseriamo
un punto e virgola alla fine della riga contenente `x + 1`, la trasformeremo
da un'espressione ad uno statement, e di consequenza otterremo un errore.

<span class="filename">Nome file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/src/main.rs}}
```

Compilare questo codice risulta in un errore:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-23-statements-dont-return-values/output.txt}}
```

Il messaggio di errore, `mismatched types`, ci dice qual'è il problema di questo
codice. Per come è stata scritta la funzione `plus_one` ci si aspetta che restituirà
un `i32`, ma gli statements non restituiscono alcun valore, come indicato da `()`,
il tipo *unit*. Pertanto, non viene restituito nulla, il che va in conflitto con
la definizione stessa della funzione e provoca un errore. In questo errore, Rust
fornisce un aiuto per aiutare a risolvere questo problema: suggerisce infatti di
rimuovere il punto e virgola, il che risolverebbe l'errore.
