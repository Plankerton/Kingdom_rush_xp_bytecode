Primary patch: Xp multiplier

Multiplier: 1000 (i set to 1000 but any value is fine; be careful of overflow if it is set too high)

Applied in all 3 difficulty modes as game had 3 separate multipliers in the decompiled code

EASY, NORMAL, VETERAN => 1000

multiplier was modified at xp progression threshold and constant rather than changing the hero level directly to level 10 as that causes issues with skill progression.

actual hero Xp continues increasing normally, just at 1000 times the original rate.

Hero level calculation remains intact.

Hero skill progression remains intact.



Relevant bytecode includes:

ISEQN / ISNEN level comparisons

TSETS ... "hero_level"

TGETS ... "hero" → "level"

TGETS ... "hero_xp_thresholds"

TGETV threshold lookup


code uses the actual hero.level to determine progression and Xp thresholds.

Therefore forcing the working level to 10 can bypass the normal level transition state that hero skills relies on
