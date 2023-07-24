## Variabili e Mutabilità

Come menzionato nella sezione [“Memorizzare valori con le variabili”
][storing-values-with-variables], di default alle variabili
non si può modificare il valore. Questa è una delle tante "spintarelle"
che Rust ti dà per farti scrivere il codice in un modo che trae vantaggio
della sicurezza e facile "concurrency" che Rust offre. Tuttavia, hai comunque
l'opzione per renderle modificabili. Scopriamo come e perchè Rust
ti incoraggia a favore dell'immutabilità e perchè alcune volte
potresti volerne fare a meno.

Quando una variabile è immutabile, quindi quando un valore è legato ad una
variabile, non puoi modificare quel valore. Per vederlo, crea un nuovo progetto
chiamato *variabili* nella tua cartella *progetti* utilizzando il comando
`cargo new variabili`.

In seguito, nella tua cartella *variabili*, apri *src/main.rs* e rimpiazza il
codice con il seguente che non compilerà:

<span class="filename">Nome file: src/main.rs</span>

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/src/main.rs}}
```

Salva ed esegui il programma usando `cargo run`. Dovresti ricevere un
messaggio di errore riguardante l'immutabilità, come è mostrato
nell'output:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-01-variables-are-immutable/output.txt}}
```

Questo esempio mostra come il compilatore ti aiuta a trovare errori nel tuo
programma. Gli errori di compilazione possono essere frustranti, ma in realtà
significano solo che il tuo programma non sta facendo ciò che vuoi in
sicurezza, non significano che non sei un bravo programmatore! Pure i Rusteceans
più esperti si trovano davanti a molti errori.

Hai ricevuto il messaggio `` cannot assign twice to immutable variable `x`
`` perchè hai provato ad assegnare un'altro valore alla variabile immutabile `x`.

È importante ricevere errori in fase di compilazione quando cerchiamo di
modificare un valore che è designato come immutabile, perché questa stessa situazione
può portare a dei bug. Se una parte del nostro codice opera pensando che un valore
non cambierà mai e un'altra parte del nostro codice cambia quel valore, è possibile che
la prima parte del codice non faccia ciò per cui è stata progettata. La causa di questo
tipo di bug può risultare difficile da individuare in seguito, specialmente quando il
secondo codice cambia il valore soltanto *alcune* volte. Il compilatore di Rust garantisce
che quando dichiari che un valore non cambierà, effettivamente non cambierà, quindi non
è necessario tenerne traccia personalmente.

Ma la mutabilità può essere molto utile e rendere il codice più comodo da scrivere.
Sebbene le variabili siano immutabili di default, è possibile
renderle mutabili aggiungendo `mut` davanti al nome della variabile, esattamente come hai
fatto nel [Capitolo 2][storing-values-with-variables]. L'aggiunta di `mut` inoltre,
fa capire ad altri possibili lettori del codice che la variabile
può essere modificata da altri pezzi di codice.

Ad esempio, modifichiamo *src/main.rs* in questo modo:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/src/main.rs}}
```

Quando eseguiamo il programma ora otterremo questo:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-02-adding-mut/output.txt}}
```

Possiamo cambiare il valore legato alla variabile `x` da `5` a `6` da quando `mut`
è stato utilizzato. In conclusione, decidere se utilizzare o no la mutabilità
dipende da cosa pensi sia l'opzione più chiara e sensata.

### Costanti

Come le variabili immutabili, le *costanti* sono valori legati ad un nome che non
possono essere cambiati, ma ci sono alcune differenze tra costanti e variabili.

Prima di tutto, non è consentito utilizzare `mut` con le costanti. Le costanti
sono immutabili di default e rimarranno sempre immutabili.
Le costanti si dichiarano utilizzando la keyword `const` anziché `let`, e il
tipo del valore deve essere specificato. Parleremo dei tipi e delle annotazioni di tipo
nella sezione successiva, [“Tipi di dato”][data-types], quindi non preoccuparti
dei dettagli al momento. Sappi solo che devi sempre specificare il tipo.

Le costanti possono essere dichiarate in qualsiasi *scope* ed anche
globalmente, il che le rende utili per i valori
che molte parti del codice devono conoscere.

L'ultima differenza è che le costanti possono solo essere legate ad un valore
che è calcolato da un espressione costante, non sul risultato di un valore
che può essere calcolato soltanto durante l'esecuzione del programma.

Ecco un esempio di dichiarazione di una costante:

```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

Il nome della costante è `THREE_HOURS_IN_SECONDS` e il suo valore è impostato sul
risultato della moltiplicazione di 60 (il numero di secondi in un minuto) per 60
(il numero di minuti in un'ora) per 3 (il numero di ore di cui vogliamo tenere
conto). Lo standard di denominazione delle costanti in Rust prevede
l'utilizzo di tutte le lettere maiuscole con il trattino basso tra le parole.
Il compilatore è in grado di eseguire un insieme limitato di operazioni durante la compilazione,
il che ci consente di scrivere questo valore in modo più comprensibile e verificabile,
anziché impostare questa costante direttamente al valore 10.800. Consulta la [sezione nella Rust Reference
sulla evaluation delle costanti][const-eval] per ulteriori informazioni su quali
operazioni possono essere utilizzate nella dichiarazione delle costanti.

Le costanti rimangono valide per l'intera esecuzione del programma,
all'interno dello *scope* in cui sono state dichiarate. Questa proprietà rende
le costanti utili per la tua applicazione in cui più parti del
programma potrebbero aver bisogno di conoscere il valore della costante,
come ad esempio il numero massimo di punti che un giocatore di un gioco può
guadagnare o la velocità della luce.

Dare nomi alle costanti che rappresentano valori all'interno del
tuo programma è utile nel trasmettere il significato di quel valore a possibili futuri
lettori/manutentori del codice. Inoltre, avrai solo un posto nel codice in cui
apportarai modifiche se il valore della costante dovesse essere aggiornato in futuro.

### Shadowing

Come hai visto nel tutorial del guessing game nel [Capitolo
2][comparing-the-guess-to-the-secret-number], è possibile dichiarare
una nuova variabile con lo stesso nome di una variabile precedente. I Rustaceans
dicono che la prima variabile viene *oscurata* (da qui "shodowing") dalla seconda,
il che significa che il compilatore considererà la seconda variabile quando
si utilizza il nome della variabile. In pratica, la seconda variabile sovrascrive la prima
fino a quando essa stessa non viene oscurata o lo *scope* finisce. Possiamo quindi
oscurare una variabile utilizzando lo stesso nome
della variabile e ripetendo l'uso della keyword `let` come segue:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-03-shadowing/src/main.rs}}
```

Questo programma inizia associando a `x` il valore `5`. Successivamente, crea
una nuova variabile `x` ripetendo `let x =`, prendendo il valore originale e
aggiungendovi `1`, quindi il valore di `x` diventerà `6`. Poi, all'interno di uno
*scope* interno creato con le parentesi graffe, la terza dichiarazione `let`
oscura nuovamente `x` e crea una nuova variabile, moltiplicando il valore
precedente per `2` rendendo `x` equivalente a `12`. Quando lo *scope* interno
finisce, l'oscuramento finisce anche e `x` tornerà ad essere `6`. Quando eseguiamo
questo programma, l'output sarà il seguente:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-03-shadowing/output.txt}}
```

L'oscuramento è diverso dal settare una variabile `mut` perché otterremo un
errore di compilazione se accidentalmente cerchiamo di riassegnare un valore
a questa variabile senza utilizzare la keyword `let`. Utilizzando `let`,
possiamo eseguire alcune modifiche su un valore, ma la variabile resterà immutabile
dopo che tali modifiche sono state eseguite.

L'altra differenza tra `mut` e l'oscuramento è che, poiché stiamo effettivamente
creando una nuova variabile, quando utilizziamo nuovamente la keyword `let`,
possiamo cambiare il tipo del valore ma riutilizzare lo stesso nome. Ad esempio,
supponiamo che il nostro programma chieda all'utente di specificare quanta
spaziatura voglia in un testo inserendo dei caratteri vuoti, e successivamente
vogliamo memorizzare quell'input come un numero:

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-04-shadowing-can-change-types/src/main.rs:here}}
```

La prima variabile `spaces` è una stringa mentre la seconda variabile `spaces`
è un numero. L'oscuramento ci evita quindi di dover pensare a nomi diversi, come
ad esempio `spaces_str` e `spaces_num`; al contrario, possiamo riutilizzare il nome
`spaces`. Tuttavia, se provassimo a utilizzare `mut`, come mostrato qui, otterremmo
un errore di compilazione:

```rust,ignore,does_not_compile
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/src/main.rs:here}}
```

L'errore ci dice che non possiamo modificare il tipo di una variabile:

```console
{{#include ../listings/ch03-common-programming-concepts/no-listing-05-mut-cant-change-types/output.txt}}
```

Ora che appiamo scoperto come funzionano le variabili, scopriamo i vari tipi
che posso avere.

[comparing-the-guess-to-the-secret-number]:
ch02-00-guessing-game-tutorial.html#comparing-the-guess-to-the-secret-number
[data-types]: ch03-02-data-types.html#data-types
[storing-values-with-variables]: ch02-00-guessing-game-tutorial.html#storing-values-with-variables
[const-eval]: ../reference/const_eval.html
