# Il Linguaggio di Programmazione Rust

![Build Status](https://github.com/rust-lang/book/workflows/CI/badge.svg)

Questa repository contiene il codice sorgente del libro "The Rust Programming Language"
in italiano.

[Il libro è disponibile cartaceo da No Starch Press.][nostarch].

[nostarch]: https://nostarch.com/rust-programming-language-2nd-edition

Puoi anche leggere il libro gratuitamente online. Per favore consulta il
libro fornito con le ultime versioni [stabili][stable], [beta] o [nightly]
di Rust. Tieni presente che eventuali problemi in quelle versioni potrebbero
essere già stati risolti in questa repository, poiché tali rilasci vengono
aggiornati con meno frequenza.

[stable]: https://doc.rust-lang.org/stable/book/
[beta]: https://doc.rust-lang.org/beta/book/
[nightly]: https://doc.rust-lang.org/nightly/book/

Leggi [releases] per scaricare solo il codice di tutti gli esempi che
sono presenti nel libro.

[releases]: https://github.com/rust-lang/book/releases

## Requisiti

"Costruire" (cioè renderlo in formato HTML) il libro richiede
[mdBook], idealmente della stessa
versione utilizzata da rust-lang/rust in [questo file][rust-mdbook].
Per ottenerlo:

[mdBook]: https://github.com/rust-lang-nursery/mdBook
[rust-mdbook]: https://github.com/rust-lang/rust/blob/master/src/tools/rustbook/Cargo.toml

```bash
$ cargo install mdbook --version <version_num>
```

## Costruire

Per costruire il libro, scrivi:

```bash
$ mdbook build
```

L'output verrà messo nella sottocartella `book`. Per vederlo, aprilo
nel browser.

_Firefox:_
```bash
$ firefox book/index.html                       # Linux
$ open -a "Firefox" book/index.html             # OS X
$ Start-Process "firefox.exe" .\book\index.html # Windows (PowerShell)
$ start firefox.exe .\book\index.html           # Windows (Cmd)
```

_Chrome:_
```bash
$ google-chrome book/index.html                 # Linux
$ open -a "Google Chrome" book/index.html       # OS X
$ Start-Process "chrome.exe" .\book\index.html  # Windows (PowerShell)
$ start chrome.exe .\book\index.html            # Windows (Cmd)
```

Per eseguire i test:

```bash
$ mdbook test
```

## Contribuire

Se vuoi contribuire ci piacerebbe molto ricevere il tuo aiuto! Consulta
[CONTRIBUTING.md][contrib] per conoscere i tipi di contributi che stiamo
cercando.

[contrib]: https://github.com/rust-lang/book/blob/main/CONTRIBUTING.md

Poiché il libro esiste anche in formato [cartaceo][nostarch] e desideriamo
mantenere la versione online del libro il più possibile vicina alla
versione caratcea, potrebbe volerci più tempo del solito per risolvere
il tuo problema o accettare la tua pull request.

Finora, abbiamo fatto un'ampia revisione per coincidere con le [Edizioni di Rust](https://doc.rust-lang.org/edition-guide/). Tra queste ampie revisioni, correggeremo solo gli errori. Se il tuo problema o la tua pull request non riguardano strettamente la correzione di un errore, potrebbe essere affrontato solo alla prossima grande revisione: con tempi nell'ordine di mesi o anni. Grazie per la tua pazienza!

### Traduzioni

Questa è la traduzione non ufficiale italiana del libro, ovviamente ci sono molte
altre [Traduzioni][Translations] in corso. Per maggiori informazioni su come fare ad aggiungere
una nuova lingua consulta la versione originale del libro. Al momento si sta
aspettando di avere il [supporto mdbook][mdbook support] prima di poter unirne qualcuna, ma
sentiti libero di iniziare!.

[Translations]: https://github.com/rust-lang/book/issues?q=is%3Aopen+is%3Aissue+label%3ATranslations
[mdbook support]: https://github.com/rust-lang-nursery/mdBook/issues/5