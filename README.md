# Pellet dictionaries

Offline dictionary language packs for [Pellet](https://getpellet.app), the
local-first notes app. Pellet downloads a pack from the
[Releases](https://github.com/getpelletapp/pellet-dictionaries/releases) page
the first time you enable a language under Settings › Dictionary; after that,
every lookup happens on your device and nothing is fetched again.

## What a pack is

One `.pdict` file per language: a small header, a compressed index, and
compressed chunks of dictionary entries sorted by headword, plus a
part-of-speech table that Pellet's *Show syntax* uses to colour words in the
editor. The file is read a few kilobytes at a time by byte range, so a 45 MB
pack costs nothing until a word is looked up.

Each entry carries the word's parts of speech, its senses, and a pronunciation
in IPA where Wiktionary has one. Inflected forms ("escarpments") point at their
lemma ("escarpment").

| Pack | Language | Source | Notes |
|---|---|---|---|
| `en-v1.pdict` | English | English Wiktionary via kaikki.org | 1,340,037 headwords |

Every release also carries a `SHA256SUMS` file. Pellet verifies a downloaded
pack against the hash pinned in the app before it is ever opened, so a
modified or corrupted file is refused.

## Where the words come from

The packs are derived from [Wiktionary](https://www.wiktionary.org/),
extracted as machine-readable data by
[Wiktextract](https://github.com/tatuylonen/wiktextract) and published at
<https://kaikki.org/dictionary/>. That data, and therefore these packs, is
available under the same licences as Wiktionary: the
[Creative Commons Attribution-ShareAlike 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
licence and the [GNU Free Documentation License](https://www.gnu.org/licenses/fdl-1.3.html).
See [LICENSE-DATA](LICENSE-DATA).

If you use Wiktextract's data in your own work, its author asks for this
citation: Tatu Ylonen, *"Wiktextract: Wiktionary as Machine-Readable
Structured Data"*, Proceedings of the 13th Conference on Language Resources
and Evaluation (LREC 2022), pp. 1317–1325.

## Building a pack

The build script lives with the app. It streams a kaikki.org JSONL dump,
keeps the records of one language, and writes the pack and a statistics file;
its README describes the exact commands, what is kept and dropped, and the
release steps. A new language is one more pack here and one more row in the
app's catalogue.
