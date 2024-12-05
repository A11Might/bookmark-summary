Title: A Made-up Name is Better Than No Name

URL Source: https://mbuffett.com/posts/a-made-up-name/

Markdown Content:
In working on Chessbook recently, I often found myself referring to (position, move) pairs. Specifically positions that are stored as EPDs, and moves that are stored in San notation.

```
let difficulty_by_epd_san = //...;
let existing_epd_sans = //...;
let unique_moves_by_epd_san = //...;
fn epd_san_plus_to_condition((epd, san_plus): &(String, String)) -> _ //...;
```

I got so used to thinking of these things together as pairs, and wished I had a name for it. I couldn’t think of an existing name that worked well and wasn’t a mouthful like `MoveFromPosition`. So I made up a name. Anything that’s an EPD and a San, is now a Kep. Because that’s the first thing that popped in my head. It’s a short, made-up name to nicely refer to a position string and a move notation.

```
let difficulty_by_kep = //...;
let existing_keps = //...;
let unique_moves_by_kep = //...;
fn kep_to_condition((epd, san_plus): &Kep) -> _ //...;
```

Just sharing this because I never thought to do this before, and I’ve really liked it. It’s not about saving a few characters – it feels easier to think about these things when I have a name for it. An `(epd, san_plus)` pair took up two slots in working memory, a `Kep` takes up one. Obviously don’t go crazy with it, but it’s a tool I’m happy to have added to the toolbox.

If you have any questions, comments, or just want to say hi, please email me at [me@mbuffett.com](mailto:me@mbuffett.com). Online, I'm most active [on twitter](https://twitter.com/MarcusBuffett).

If you play games, my PSN is mbuffett, always looking for fun people to play with.

If you're into chess, I've made a [repertoire builder](https://chessbook.com/). It uses statistics from hundreds of millions of games at your level to find the gaps in your repertoire, and uses spaced repetition to quiz you on them.

Samar Haroon, my girlfriend, has started a podcast where she talks about the South Asian community, from the perspective of a psychotherapist. [Go check it out!](https://open.spotify.com/show/7teSzaHt5I3r9s5PPLZFrF?si=J1-h-uFCTLyXGPbZnYSIGQ).

If you want to support me, you can [buy me a coffee](https://github.com/sponsors/marcusbuffett).
