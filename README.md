# Kingdom_rush_xp_bytecode
the hero xp gain was modified in the compiled LuaJIT bytecode in game_gui.lua

The relevant hero xp handling is around the lines 9370-9428 and The code uses and references hero_level, hero_xp_base, hero_xp_thresholds, hero_xp_next, and hero_xp_ephemeral

The xp calculation is run inside a loop that processes the relevant hero progression data. i traced the loop through the bytecode rather than treating the surrounding instructions as the xp calc itself: there are unrelated code and calculations ignore those.

MORE SPECIFICALLY
to bypass the level reset code this was roughly the change i made:
game loads and i set
> hero.hero.xp = status.xp
> hero.hero.level = 10
then i ran an xp threshold loop (this existed before the mod and is how the game calculates hero xp) that overwrote certain steps
> for i, th in ipairs(GS.hero_xp_thresholds) do
    if th > hero.hero.xp then
        hero.hero.level = i
        break
    end
> end
the important part is that the mod does not change xp gain or spoof it; it merely skips the xp to level calculation leaving the level 10 status intact 
