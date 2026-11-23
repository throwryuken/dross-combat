# DROSS: Combat Report — changelog

## v15.8.0 — 2026-11-23 (America/Denver)

Movement feel, character animation, and a cloth-like cloak. Progression, XP, upgrades, Oath systems, art style, and music files are unchanged. Saves from v15.7.2 still load (`SAVE_VERSION` 18).

- **Movement style:** fast acceleration, short deceleration, with a higher rate when reversing (`move_toward` toward input × top speed, or toward zero). Top speed stays 194. Chosen because this is a bullet-dodging survivor: the character should feel weighty and alive without ice-physics lag.
- **Video lessons used** (Coding Quests, [Why Most Top-Down Movement Feels Bad](https://www.youtube.com/watch?v=cZvuas7wSDw)): replace instant start/stop with `move_toward`; keep aim/attacks independent of the visual turn; diagonals were already normalized; derive values from the existing room-crossing time (same top speed) instead of retuning random pixel speeds. Empty Palm remains the dash; no second dash was added.
- **Numbers:** accel 2400 px/s² (~0.08s to max), decel 3200 (~0.06s to stop), reverse 4200 (~0.09s). Enemy walk, shot, and charge speeds × 0.97 so dodge windows stay about the same.
- **Animation:** the body eases toward movement direction over 200ms, leans into the move, and uses a step bob plus a light squash/stretch so it is not a sliding sprite.
- **Cloak:** the Take 2 split-tail mantle is now a looser 5-segment Verlet/spring cloth per tail (inertia, flutter at speed, idle sway). Art direction unchanged: gold-trimmed shoulders, black/orange-red in Blackflame, white in Pure, flames dimmer than the pink bullets. No per-frame allocations in the cloth step. DPR cap unchanged (1.75, or 1.4 with Reduced FX).

## v15.7.2

VFX polish on top of the Take 2 Mantle. See `polish/v15_7_2/VERIFY-v15.7.2.md`.
