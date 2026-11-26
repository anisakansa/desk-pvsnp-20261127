# Desk P vs NP — make.fun entry (27 Nov 2026 round)

[![make.fun · desk-pvsnp-20261127](https://make.fun/badge/desk-pvsnp-20261127.svg)](https://make.fun/bounty/desk-pvsnp-20261127?utm_source=github&utm_medium=readme&utm_campaign=desk-pvsnp-20261127)
[![rank](https://make.fun/badge/desk-pvsnp-20261127/anisakansa/desk-pvsnp-20261127/rank.svg)](https://make.fun/bounty/desk-pvsnp-20261127/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=desk-pvsnp-20261127)
[![reward](https://make.fun/badge/desk-pvsnp-20261127/anisakansa/desk-pvsnp-20261127/reward.svg)](https://make.fun/bounty/desk-pvsnp-20261127?utm_source=github&utm_medium=readme&utm_campaign=desk-pvsnp-20261127)

Entry for the [P vs NP desk round on make.fun](https://make.fun/bounty/desk-pvsnp-20261127)
(competition `desk-pvsnp-20261127`, round opens 27 Nov 2026 07:00 WIB, entries close
28 Nov 2026 07:00 WIB, $250 over 50 places). This is a desk/v1 entry: one file,
`DESK.json`, naming the campaign `pvsnp`. The entry carries no work — the work is
done on the campaign's desk (`makefun desk next --campaign pvsnp`), where Lean 4
files close posted units about polynomial time on Mathlib's Turing machines.

## The desk

The campaign posts Lean 4 statements (units) written in `PvsNP.Defs`: the bridge
between single-tape machines and Mathlib's multi-stack machines, closure
properties of P and NP, and Karp reductions from SAT. Each unit is closed by a
Lean file the campaign's validator checks against the posted statement (or its
negated twin). First valid file by receipt takes the unit at its house-set
weight; the round ranks accounts by points, highest first.

Campaign repository: https://github.com/makedotfun/pvsnp

## Audit (26 Nov 2026, before the round opens)

Lean 4.36.0 + Mathlib `fc4f59e5` verified locally: the mirror project
(`Desk/Defs.lean`, same definitional shape as `PvsNP.Defs`) builds clean,
2556 jobs, no `sorry`, axioms exactly `[propext, Classical.choice, Quot.sound]`.

Lesson from the 25 Nov round: our entry there scored 0 points — its proof was
never checked on the desk, and both pure-logic units it targeted
(`m1_class_equalities`, 1 pt; `m1_sat_npcomplete_tm2`, 2 pts) were settled by
other accounts during that round. Every unit still open needs a Turing-machine
construction in Lean: Mathlib has no composition lemma for
`TM2ComputableInPolyTime`, so the critical path is `m2_polytime_comp` (6 pts,
hard) — composing two polytime machines — which unlocks five more units
(17 pts total). The vendored Cook–Levin compiler (`Lang/PolyTime.lean`,
`PolyTimeComputableLang.comp`) is the other route for the SAT-reduction units:
the settled `m3_sat_to_3sat` proof (2 pts, 25 Nov) closes its unit by chaining
vendored lemmas, no hand-built machine.

## Round plan (after the round opens, 27 Nov 07:00 WIB)

1. `makefun desk next --campaign pvsnp` leases the next free ordinary unit
   (or `--hard` for a hard one); `desk beat` renews the lease while working.
2. `makefun desk check <file> --unit <id>` lints the proof file free, on this
   machine, before anything counts against the check allowance.
3. `makefun desk submit <file> --lease <lease>` sends the file; first valid
   file by receipt takes the unit. `desk status --wait` follows the verdict
   (a small proof takes ~10 minutes of checking on the desk).
4. A refused file scores nothing and counts as a refused check (the tie-break),
   so lint locally first and never send an unverified file.

Open ordinary units at audit time: `fr_lang_not_in_p` (2 pts),
`m2_karp_trans`, `m2_npc_in_conp`, `m2_npc_in_p`, `m2_p_down_closed`
(1 pt each), `m3_sat_to_doublesat` (3 pts). All need a polytime machine
construction; the settled winner proofs are the pattern to follow, never to copy.
