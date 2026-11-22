# ce-agree
CE-Agree tests whether language models choose the verb form that agrees with its grammatical subject when nearby nouns give conflicting number cues. It includes 2,000 families of minimal pairs from doubly center-embedded English sentences, plus the lexicons used to generate them.

# Tagged Release
CE-Agree v1.0.0 contains the original CE2 dataset v0.7_nf2000, with 2,000 sentence families and 6,000 minimal pairs. 11_22_2026.

## Dataset

The benchmark contains 6,000 minimal pairs in 2,000 sentence families, with one
pair per family at each of three agreement checkpoints: the innermost verb
(V3), the intermediate verb (V2), and the final copula (COPULA).

| File | Contents |
| --- | --- |
| [Benchmark JSONL](data/stimuli/minpairs.ce2fam.generated.v0.7_nf2000.jsonl) | One minimal pair per line, with continuations and metadata |
| [Noun lexicon](data/lexicons/lexicon_nouns.csv) | 20 nouns and their singular and plural forms |
| [Transitive verb lexicon](data/lexicons/lexicon_verbs_transitive.csv) | 15 verbs and their present-tense agreement forms |

## Center embedding and agreement

A clause is **center-embedded** when it interrupts another clause. In this
grammatical sentence from family `ce2fam_01239`, the relative clause modifying
*the judges* contains a second relative clause modifying *the manager*. Both
embedded clauses come before the main predicate *are late*.

> The judges₁ [the manager₂ [the journalists₃ follow₃] blames₂] are₁ late.

Brackets mark the two embedded clauses. Subscripts link each subject noun
phrase to its verb. For example, *the journalists* (NP₃) is the subject of
*follow* (V₃).

Each row below is one minimal pair. Within a row, only the verb form at the
tested checkpoint changes. The prefix is shared, and all other verb forms stay
fixed.

| Checkpoint | Grammatical subject | Shared prefix | Grammatical continuation | Agreement-error continuation |
| --- | --- | --- | --- | --- |
| V₃ (innermost verb) | NP₃ (*the journalists*, plural) | `The judges the manager the journalists` | `follow blames are late.` | `follows blames are late.` |
| V₂ (intermediate verb) | NP₂ (*the manager*, singular) | `The judges the manager the journalists follow` | `blames are late.` | `blame are late.` |
| COPULA (main-clause *is/are*) | NP₁ (*the judges*, plural) | `The judges the manager the journalists follow blames` | `are late.` | `is late.` |

### Terms

- **Controller** — the grammatical subject whose singular or plural number
  determines the verb form.
- **Attractor** — a noun phrase other than the controller whose number can
  influence the model’s verb choice. At V₂, the nearest noun phrase is NP₃.
- **Congruent** — the specified attractor and controller match in number.
- **Incongruent** — the specified attractor and controller differ in number.
  At V₂ in this family, plural NP₃ (*the journalists*) is incongruent with
  singular NP₂ (*the manager*). The correct form is *blames*.

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
