# Configuration contracts

## R8 Schema and live effects

Each setting has one case-sensitive URL key and a cookie named `tetris_` plus that key. Exact decoded strings below are valid; whitespace, alternate case, booleans such as `true` and empty values are invalid. The schema is shared by controls, parser, defaults and serializer.

| Control / key | Valid values | Default | Effect |
| --- | --- | --- | --- |
| Ghost visibility / `ghost` | `hide`, `dynamic`, `show` | `show` | Immediate, all-or-nothing R6 projection visibility. |
| Hard drop / `hardDrop` | `0`, `1` | `1` | Immediate command eligibility. |
| Next preview / `next` | `0`, `1` | `1` | Immediate visibility, same queue. |
| Hard-drop locking / `dropLock` | `follow`, `immediate` | `follow` | Captured by next incoming active piece. |
| General locking / `lock` | `failed`, `interval` | `interval` | Captured by next incoming active piece. |
| Hold / `hold` | `0`, `1` | `1` | Immediate eligibility; held kind preserved. |

Use labelled native controls and display current selections. If lock settings differ from the active piece’s captured pair, show “Applies to next piece.” A Hold exchange counts as an incoming piece. Disabled hard drop or penetrator Hold remains inert regardless of focus or synthetic duplicate commands. Settings can be changed in ready/running/paused/game-over states. Session values are authoritative immediately even when persistence fails. No settings change restarts the game or resets active timers.

## R9 Resolution and persistence

Resolve independently per key on page initialization:

1. Read the first occurrence of the URL key using standard query decoding. A valid decoded value wins. Invalid or empty first occurrence is treated as absent; subsequent duplicate occurrences do not override it.
2. Otherwise read the exact cookie name. A valid decoded cookie value wins. Malformed percent encoding, duplicate exact-name cookies, unknown values or unavailable cookie access count as absent for that key.
3. Otherwise use its default. An invalid value for one key cannot invalidate or default another setting.

Every valid explicit URL value must be written to its corresponding cookie, including a default-equivalent value. Invalid/omitted parameters must not overwrite a saved cookie; invalid cookies need not be repaired until a valid explicit value or interactive change supplies a replacement. Initial cookie/default resolution must not automatically add missing URL parameters. Configuration does not persist game board, score, source or bonuses.

On an interactive valid setting change, update the session value and corresponding control, then independently attempt its cookie save and URL update. Replace all occurrences of that setting’s URL key with one canonical value using history replacement, with no navigation or game reload. Preserve unrelated parameters, pathname and fragment; byte-identical query encoding/order is not required. Other setting keys remain semantically unchanged. Invalid programmatic selections leave state and both persistence ports untouched.

Cookies contain URI-encoded canonical values with Path=/, SameSite=Lax and Max-Age=31536000; add Secure on HTTPS and omit it on HTTP development origins. Read cookies by exact name, not substring. Attempt an immediate readback after saving; if the value is not observable, report cookie persistence unavailable. Browser expiration, user deletion or blocking can remove cookies; URL/session behavior remains independent. A valid default URL value must still be saved/read back, not optimized away.

If cookie access/save fails, history replacement throws, or URL access is unavailable, retain the validated session selection. Attempt the other port independently and show a concise status identifying which persistence mechanism is unavailable. Do not expose raw exception details. No failure may crash or freeze gameplay. There is no promise of persistence when the user/browser blocks it; a successful save must survive a same-origin reload while the cookie remains available.

## Acceptance matrix

| Fixture | Expected result |
| --- | --- |
| No URL/cookie | All defaults; no invented URL keys. |
| Valid URL default and conflicting cookie | URL wins and default value replaces that cookie. |
| Omitted URL with nondefault cookie | Cookie wins and stays saved. |
| Invalid URL, valid cookie | Cookie wins; invalid URL does not poison other fields or overwrite cookie. |
| Invalid/blocked cookie without valid URL | Default for that key only. |
| Six keys from mixed sources | Each independently matches its winning source and origin. |
| Duplicate URL key | First decoded occurrence alone determines validity/value; interactive update leaves one canonical occurrence. |
| Malformed/duplicate cookie | Treat that cookie as absent without throwing. |
| Change each control, reload | Its valid selection and URL survive; other selections/unknown query/fragment remain. |
| Cookie failure / history failure / both | Current session remains playable; unaffected port still attempted; status explains limitation. |
| Hold disabled then enabled | Existing held kind retained; active penetrator still cannot Hold. |
| Lock change during grounding | Active deadline/policy unchanged; next normal spawn or Hold incoming captures selections. |
