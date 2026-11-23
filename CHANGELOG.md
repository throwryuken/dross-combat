# DROSS: Combat Report — changelog

## v15.9.0 — 2026-11-23 (America/Denver)

Fixes the v15.8 move shake and cloak, and lets held bullets survive the Pure ultra. Progression, XP, upgrades, Oath systems, art style, and music files are unchanged. Saves from v15.7.2 / v15.8.0 still load (`SAVE_VERSION` 18). Movement physics (accel 2400 / decel 3200 / reverse 4200, top speed 194) is unchanged.

- **Bob:** the step phase is driven by distance traveled, one footfall per 48 px, so the bounce is ~2 Hz at top speed 194 (not a 6–9 Hz vibration). Amplitude ramps from 0 with speed (max 1.2 px) with no 0.25 speed floor. On a stop, amplitude eases to 0 and the phase resets to a footfall. Idle breathing is a separate ~0.3 Hz, ≤0.4 px motion and does not advance the step phase. The bob is applied in screen-up space, outside the facing/lean rotate, so it is no longer a diagonal wobble.
- **Lean and squash:** lean is capped at 6° and driven by lateral acceleration, so the body tips on turns and starts, then settles. Squash is only a short ≤3% impulse on start or stop, not a constant 5% stretch.
- **Cloak:** the Take 2 split-tail mantle now trails the player. Each tail follows a preallocated ring buffer of the shoulder's past world positions (a ribbon/wake), so the hem lags along the path and swings out on turns. Weaker springs, velocity drag, and looser bend/cone (55° / 110°) let it wake behind the player. The clocked moving flutter is gone; only a tiny speed-scaled hem flutter and a gentle idle settle remain. Colors and art direction are unchanged. No per-frame allocations in the cloth step. DPR cap unchanged (1.75, or 1.4 with Reduced FX).
- **Pure ultra:** held bullets are no longer un-held or erased when Hollow Domain starts (`eraseNearbyShots` and the in-ultra `updateShots` wipe skip `s.held`). Free enemy shots are still erased. About 0.4 s in, when the cluster pull/stun lands, all held bullets launch as a radial volley aimed at the stunned cluster, using the existing consume/held-volley path and damage (Kindling credit as usual). If no enemies are in range, the bullets stay in orbit.

## v15.8.0 — 2026-11-23 (America/Denver)

Movement feel, character animation, and a cloth-like cloak. Progression, XP, upgrades, Oath systems, art style, and music files are unchanged. Saves from v15.7.2 still load (`SAVE_VERSION` 18).

- **Movement style:** fast acceleration, short deceleration, with a higher rate when reversing (`move_toward` toward input × top speed, or toward zero). Top speed stays 194. Chosen because this is a bullet-dodging survivor: the character should feel weighty and alive without ice-physics lag.
- **Video lessons used** (Coding Quests, [Why Most Top-Down Movement Feels Bad](https://www.youtube.com/watch?v=cZvuas7wSDw)): replace instant start/stop with `move_toward`; keep aim/attacks independent of the visual turn; diagonals were already normalized; derive values from the existing room-crossing time (same top speed) instead of retuning random pixel speeds. Empty Palm remains the dash; no second dash was added.
- **Numbers:** accel 2400 px/s² (~0.08s to max), decel 3200 (~0.06s to stop), reverse 4200 (~0.09s). Enemy walk, shot, and charge speeds × 0.97 so dodge windows stay about the same.
- **Animation:** the body eases toward movement direction over 200ms, leans into the move, and uses a step bob plus a light squash/stretch so it is not a sliding sprite.
- **Cloak:** the Take 2 split-tail mantle is now a looser 5-segment Verlet/spring cloth per tail (inertia, flutter at speed, idle sway). Art direction unchanged: gold-trimmed shoulders, black/orange-red in Blackflame, white in Pure, flames dimmer than the pink bullets. No per-frame allocations in the cloth step. DPR cap unchanged (1.75, or 1.4 with Reduced FX).

## v15.7.2

VFX polish on top of the Take 2 Mantle. See `polish/v15_7_2/VERIFY-v15.7.2.md`.
