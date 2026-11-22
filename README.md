# ce-agree
CE-Agree tests whether language models choose the verb form that agrees with its grammatical subject when nearby nouns give conflicting number cues. It includes 2,000 families of minimal pairs from doubly center-embedded English sentences, plus the lexicons used to generate them.

## Dataset

The benchmark contains 6,000 minimal pairs in 2,000 sentence families, with one
pair per family at each of three agreement checkpoints: the innermost verb
(V3), the intermediate verb (V2), and the final copula (COPULA).

| File | Contents |
| --- | --- |
| [Benchmark JSONL](data/stimuli/minpairs.ce2fam.generated.v0.7_nf2000.jsonl) | One minimal pair per line, with continuations and metadata |
| [Noun lexicon](data/lexicons/lexicon_nouns.csv) | 20 nouns and their singular and plural forms |
| [Transitive verb lexicon](data/lexicons/lexicon_verbs_transitive.csv) | 15 verbs and their present-tense agreement forms |

## Using the benchmark

For each JSONL record, concatenate the common `prefix` with `good` to recover
the grammatical sentence or with `bad` to recover its agreement-error
counterpart. Keep the leading space in each continuation. `pair_id` identifies
a single pair and `meta.family_id` groups its three checkpoints. The metadata
also records the checkpoint, noun numbers, and lexical IDs.

Report accuracy by checkpoint. To test attraction at V2, compare the pairs
where the nearer noun NP3 matches the grammatical subject NP2 in number with
those where it mismatches. Both noun numbers are recorded in `meta.nums`.

## License

Copyright (c) 2026 CE-Agree Authors. The benchmark stimuli and lexicons are
licensed under [Creative Commons Attribution 4.0 International](LICENSE).
When citing the data, include the name CE-Agree, the dataset version
`v0.7_nf2000`, and a link to this repository.
