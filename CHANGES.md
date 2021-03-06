CoqHammer v. 1.2
================

Coq versions compatibility: 8.10, 8.11.

Overview of changes
-------------------
* New reconstruction backend. The reconstruction tactics are now based
  on a reasonably general proof search procedure for the Calculus of
  Inductive Constructions and are more useful independently.
* Bugfixes in the `predict` program: now compiles with recent versions
  of GCC and works correctly on macOS.

CoqHammer v. 1.1.1
==================

Coq versions compatibility: 8.9, 8.10.

Overview of changes
-------------------
* Separate packaging of the plugin and the reconstruction tactics.
* Quick plugin and tactics tests which do not require ATP provers
  installed (`make quicktest`, `make test-plugin`, `make test-tactics`).
* Machine-learning features now take into account the polarity
  (positive/negative) of symbol occurrences (`opt_feature_polarity`).
* Opaqueness information now taken into account with constant
  unfolding.

CoqHammer v. 1.1
================

Coq versions compatibility: 8.8, 8.9.

Overview of changes
-------------------
* CVC4 integration.
* Minimization of dependencies.
* Parallel invocation of proof tactics.
* More reliable timeout mechanism based on `fork` and `wait`.
* Improvements in the reconstruction tactics, more rewrite hints for `sauto`.
* Change in reconstruction tactics interface. Tactics no longer need a
list of hypotheses, and a different set of tactics is used.
* Improvements in the translation.
* Messages now more user-friendly.
* `predict` tactic.
* Added `opam` support.
* More consistent removal of temporary files.
* Debugging commands.
* Tests (`make tests`).

Technical details of improvements to the translation
----------------------------------------------------
* Hashing of lifted-out terms.
* Type lifting (`opt_type_lifting`): hashing of types and lifting them out, e.g.,

```coq
forall f : nat -> nat, g : (nat -> nat) -> nat -> nat, ...
```

is translated to

```coq
forall f, T1(f) -> forall g, T2(g) -> ...
```

with axioms

```coq
forall f, T1(f) <-> forall x, nat(x) -> nat(f x)
forall g, T2(g) <-> forall h, T1(h) -> forall x, nat(x) -> nat(g h x)
```

instead of translating this to

```coq
forall f, (forall x, nat(x) -> nat(f x)) -> forall g, (forall h,
(forall x, nat(x) -> nat(h x))) -> forall x, nat(x) -> nat(g h x)) ->
...
```

* `Set` now collapsed to `Type`

CoqHammer v. 1.0
================

Coq versions compatibility: 8.6.

First full CoqHammer version.
