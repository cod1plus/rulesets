# cod1plus rulesets

The fair-play cvar rules (PunkBuster `pb_sv_cvar` syntax) that COD1.6X clients enforce on
1.6X servers. One file per ruleset id; a server names the id it wants in `ruleset.txt`
next to `competitive.cfg` (cod1plus.so publishes it as `sv_competitive_ruleset`).

## Editing a rule

1. Edit `<id>.pb` here. Grammar (one rule per line):
   ```
   pb_sv_cvar <cvar> IN a          value must equal a          -> forced + locked
   pb_sv_cvar <cvar> IN a b        a <= value <= b             -> clamped
   pb_sv_cvar <cvar> OUT a b       value must NOT be in [a, b] -> engine default
   pb_sv_cvar <cvar> INCLUDE s...  value must contain one of s -> engine default
   pb_sv_cvar <cvar> EXCLUDE s...  value must contain none of s
   ```
   A cvar the client does not register is ignored. A cvar named in the server's
   `competitive.cfg` follows that file instead (it overrides this list).
2. Bump the `; version N` header.
3. Commit to `main`. Every client picks the new file up at its next launch.
4. To push it to players **in game**, write `<id>@N` in the servers' `ruleset.txt`
   (re-read live): a client behind version N re-downloads within a few seconds.

Clients keep a cached copy (`rulesets\` next to the game) and a built-in copy of
`codbase-2023-05`, so an unreachable repo never disables the rules.

## Files

- `codbase-2023-05.pb` - the CoDBase / CyberGamer list for CoD 1.5 (May 2023, Anglhz),
  `cl_maxpackets IN 60 125` for the 40-tick client.
