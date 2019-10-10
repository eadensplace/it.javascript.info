# Modalità multilinea, flag "m"

La modalità multilinea viene abilitata dalla flag `pattern:/.../m`.

Essa influisce solo sul comportamento di `pattern:^` e `pattern:$`.

Nella modalità multilinea essi combaciano non solo all'inizio e alla fine della stringa, ma anche all'inizio/fine della riga.

## Inizio riga ^

Nell'esempio sottostante, il testo è composto da più righe. Il pattern `pattern:/^\d+/gm` prende un numero dall'inizio di ciascuna riga:

```js run
let str = `1st place: Winnie
2nd place: Piglet
33rd place: Eeyore`;

*!*
alert( str.match(/^\d+/gm) ); // 1, 2, 33
*/!*
```

Il motore delle regexp si sposta lungo il testo e cerca l'inizio di una riga `pattern:^`, quando la trova continua a cercare corrispondenze per il resto del pattern `pattern:\d+`.

Senza la flag  `pattern:/.../m` solo il primo numero viene trovato:

```js run
let str = `1st place: Winnie
2nd place: Piglet
33rd place: Eeyore`;

*!*
alert( str.match(/^\d+/g) ); // 1
*/!*
```

Questo avviene perchè, di base, l'accento circonflesso `pattern:^` cerca corrispondenze all'inizio del testo, e in modalità multilinea le cerca all'inizio di qualunque linea.

## Line end $

The dollar sign `pattern:$` behaves similarly.

The regular expression `pattern:\w+$` finds the last word in every line

```js run
let str = `1st place: Winnie
2nd place: Piglet
33rd place: Eeyore`;

alert( str.match(/\w+$/gim) ); // Winnie,Piglet,Eeyore
```

Without the `pattern:/.../m` flag the dollar `pattern:$` would only match the end of the whole string, so only the very last word would be found.

## Anchors ^$ versus \n

To find a newline, we can use not only `pattern:^` and `pattern:$`, but also the newline character `\n`.

The first difference is that unlike anchors, the character `\n` "consumes" the newline character and adds it to the result.

For instance, here we use it instead of `pattern:$`:

```js run
let str = `1st place: Winnie
2nd place: Piglet
33rd place: Eeyore`;

alert( str.match(/\w+\n/gim) ); // Winnie\n,Piglet\n
```

Here every match is a word plus a newline character.

And one more difference -- the newline `\n` does not match at the string end. That's why `Eeyore` is not found in the example above.

So, anchors are usually better, they are closer to what we want to get.
