## Commenti

Tutti i programmatori si sforzano di rendere il proprio codice facilmente
comprensibile, ma delle volte è necessaria una spiegazione aggiuntiva.
In questi casi, i programmatori lasciano *commenti* nel loro codice
sorgente che il compilatore ignorerà ma che le persone che leggeranno il
codice sorgente potrebbero trovare utili.
Ecco un semplice commento:

```rust
// hello, world
```

In Rust, lo stile idiomatico è quello di iniziare commento con due slash
e il commento continua fino alla fine della riga. Per i commenti che si
estendono oltre una singola riga, potrai utilizzare `//` su ogni riga
oppure `/* */`, come ad esempio:

```rust
/*
So we’re doing something complicated here, long enough that we need
multiple lines of comments to do it! Whew! Hopefully, this comment will
explain what’s going on.
*/
```

I commenti possono anche essere messi dopo le linee di codice:

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-24-comments-end-of-line/src/main.rs}}
```

Ma li vedrai più spesso utilizzati in questo formato, cioè su una linea
separata prima del codice che vogliamo descrivere.

<span class="filename">Nome file: src/main.rs</span>

```rust
{{#rustdoc_include ../listings/ch03-common-programming-concepts/no-listing-25-comments-above-line/src/main.rs}}
```

Rust ha inoltre un'altro tipo di commento, i commenti di
documentazione (*documentation comments*), di cui discuteremo
nella sezione [“Pubblicare una *Crate* su Crates.io”][publishing]
del Capitolo 14.

[publishing]: ch14-02-publishing-to-crates-io.html
