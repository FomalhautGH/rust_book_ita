## Hello, World!

Ora che hai installato Rust, è il momento di scrivere il tuo primo programma
in Rust. È tradizione quando si impara un nuovo linguaggio di programmazione
scrivere un piccolo programma che stampa la scritta `Hello, world!` sullo schermo,
quindi lo faremo anche qui.

> Nota: Questo libro presume una familiarità di base con la command line. Rust
> non ha richieste specifiche riguardo il tuo ambiente di sviluppo o agli
> strumenti che utilizzi, né al luogo in cui il tuo codice risiede. Pertanto,
> se preferisci utilizzare un ambiente di sviluppo integrato (IDE) invece della
> command line, sentiti libero di utilizzare il tuo IDE preferito. Molti IDE
> ora hanno un certo livello di supporto per Rust; consulta la documentazione
> dell'IDE che utilizzi per ulteriori dettagli. Il team di Rust si è impegneto
> nell'offrire un ottimo supporto IDE tramite `rust-analyzer`. Per ulteriori
> dettagli, consulta l'[Appendice D][devtools].

### Creare una Cartella Progetto

Inizierai creando una cartella per mettere il tuo codice Rust da qualche parte.
A Rust non importa dove il tuo codice è messo, ma per gli esercizi e progetti
in questo libro, consigliamo di creare una cartella *projects* nella tua cartella
principale e di tenere tutti i tuoi progetti lì.

Apri un terminale ed esegui i seguenti comandi per creare una cartella *projects*
e un'altra cartella per il progetto "Hello, world!" al suo interno.

Per Linux, macOS e PowerShell su Windows, usa questi:

```console
$ mkdir ~/projects
$ cd ~/projects
$ mkdir hello_world
$ cd hello_world
```

Per il CMD di Windows, usa questi:

```cmd
> mkdir "%USERPROFILE%\projects"
> cd /d "%USERPROFILE%\projects"
> mkdir hello_world
> cd hello_world
```

### Scrivere ed Eseguire un Programma Rust

In seguito, crea un nuovo file sorgente chiamato *main.rs*. I file Rust hanno
sempre l'estensione *.rs*. Se vuoi utilizzare più di una parola nel tuo file
Rust, lo standard è quello di usare un trattino basso per separarle.
As esempio, usa *hello_world.rs* invece che *helloworld.rs*

Ora apri il file *main.rs* che hai appena creato e scrivi il codice
presentato nella Voce 1-1.

<span class="filename">Nome file: main.rs</span>

```rust
fn main() {
    println!("Hello, world!");
}
```

<span class="caption">Voce 1-1: Programma che stampa `Hello, world!`</span>

Salva il file e torna nel terminale nella cartella *~/projects/hello_world*.
Su Linux o macOS, esegui i seguenti comandi per compilare ed eseguire
il file.

```console
$ rustc main.rs
$ ./main
Hello, world!
```

Su Windows, esegui il comando `./main.exe` invece che `./main`:

```powershell
> rustc main.rs
> .\main.exe
Hello, world!
```

Indipendentemente dal tuo sistema operativo, la stringa `Hello, world!` dovrebbe
essere stata stampata nel terminale. Se non vedi questo output, riferisciti alla
parte del [“Troubleshooting”][troubleshooting] nella sezione dell'installazione
per capire il problema.

Se invece la stringa `Hello, world!` è stata stampata, cogratulazioni! Hai
ufficialmente scritto un programma in Rust. Questo ti rende un programmatore
Rust—benvenuto!

### Anatomia di un Programma Rust

Let’s review this “Hello, world!” program in detail. Here’s the first piece of
the puzzle:

```rust
fn main() {

}
```

These lines define a function named `main`. The `main` function is special: it
is always the first code that runs in every executable Rust program. Here, the
first line declares a function named `main` that has no parameters and returns
nothing. If there were parameters, they would go inside the parentheses `()`.

The function body is wrapped in `{}`. Rust requires curly brackets around all
function bodies. It’s good style to place the opening curly bracket on the same
line as the function declaration, adding one space in between.

> Note: If you want to stick to a standard style across Rust projects, you can
> use an automatic formatter tool called `rustfmt` to format your code in a
> particular style (more on `rustfmt` in
> [Appendix D][devtools]<!-- ignore -->). The Rust team has included this tool
> with the standard Rust distribution, as `rustc` is, so it should already be
> installed on your computer!

The body of the `main` function holds the following code:

```rust
    println!("Hello, world!");
```

This line does all the work in this little program: it prints text to the
screen. There are four important details to notice here.

First, Rust style is to indent with four spaces, not a tab.

Second, `println!` calls a Rust macro. If it had called a function instead, it
would be entered as `println` (without the `!`). We’ll discuss Rust macros in
more detail in Chapter 19. For now, you just need to know that using a `!`
means that you’re calling a macro instead of a normal function and that macros
don’t always follow the same rules as functions.

Third, you see the `"Hello, world!"` string. We pass this string as an argument
to `println!`, and the string is printed to the screen.

Fourth, we end the line with a semicolon (`;`), which indicates that this
expression is over and the next one is ready to begin. Most lines of Rust code
end with a semicolon.

### Compiling and Running Are Separate Steps

You’ve just run a newly created program, so let’s examine each step in the
process.

Before running a Rust program, you must compile it using the Rust compiler by
entering the `rustc` command and passing it the name of your source file, like
this:

```console
$ rustc main.rs
```

If you have a C or C++ background, you’ll notice that this is similar to `gcc`
or `clang`. After compiling successfully, Rust outputs a binary executable.

On Linux, macOS, and PowerShell on Windows, you can see the executable by
entering the `ls` command in your shell:

```console
$ ls
main  main.rs
```

On Linux and macOS, you’ll see two files. With PowerShell on Windows, you’ll
see the same three files that you would see using CMD. With CMD on Windows, you
would enter the following:

```cmd
> dir /B %= the /B option says to only show the file names =%
main.exe
main.pdb
main.rs
```

This shows the source code file with the *.rs* extension, the executable file
(*main.exe* on Windows, but *main* on all other platforms), and, when using
Windows, a file containing debugging information with the *.pdb* extension.
From here, you run the *main* or *main.exe* file, like this:

```console
$ ./main # or .\main.exe on Windows
```

If your *main.rs* is your “Hello, world!” program, this line prints `Hello,
world!` to your terminal.

If you’re more familiar with a dynamic language, such as Ruby, Python, or
JavaScript, you might not be used to compiling and running a program as
separate steps. Rust is an *ahead-of-time compiled* language, meaning you can
compile a program and give the executable to someone else, and they can run it
even without having Rust installed. If you give someone a *.rb*, *.py*, or
*.js* file, they need to have a Ruby, Python, or JavaScript implementation
installed (respectively). But in those languages, you only need one command to
compile and run your program. Everything is a trade-off in language design.

Just compiling with `rustc` is fine for simple programs, but as your project
grows, you’ll want to manage all the options and make it easy to share your
code. Next, we’ll introduce you to the Cargo tool, which will help you write
real-world Rust programs.

[troubleshooting]: ch01-01-installation.html#troubleshooting
[devtools]: appendix-04-useful-development-tools.md
