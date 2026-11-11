# Long Hop: Red Centre Run

Test report for the offline build.

| | |
|---|---|
| File | `artifacts/LongHop.html` (same bytes as `index.html`) |
| Bytes | 156696 |
| SHA-256 | `fe3ff255e85efa531e8a20416f68080063a87535630315113734a4e1789b07ac` |

A case-insensitive scan of the HTML found none of the personal names, path prefixes, or the decoded token named in the brief.

## What shipped

- One self-contained HTML file. CSS, game code, drawings, and audio are inline. No CDN, no runtime network, no account.
- Cartoon outback lane-crossing. Mara the red kangaroo hops and charges leaps across utes, road trains, cattle, tumbleweed fire, log rivers, croc billabongs, gorge pads, empty gaps, flash floods, salt crust, and dust-storm highways.
- Scenery: ghost gums, boabs, spinifex, koalas, emus, wombats, cockatoos, wallabies, an echidna, and two sloths who are not from here. Crocs are avoided, not fought.
- Three lives. A red fruit restores one. Powers: speed, super jump, shield, slow time.
- Score in A$, with leap-length, risk, near-miss, and flow multipliers. Easy / Normal / Hard.
- Eight handcrafted crossings plus an endless muster. A par of eight minutes is shown. A full human timing of each crossing was not done.
- Four bonus rounds: boomerang shed, log surf, dust dash, rodeo hop. The story pays full rate. The shed pays three quarters.
- Title menu: Play, Crossings, Bonus shed, Unlockables, Scores, Settings, Rivals and co-op, Credits.
- Settings: volume, mute, graphics low/med/high, difficulty, reduced flash, touch auto/on/off.
- Saves in localStorage: settings, progress, unlocks, local scores.
- Unlockable coats, hoppers (wallaby, emu, sloth), and arenas.
- Frozen-mirage emperor penguins, reached by hopping off the left edge of a marked bank.
- Keyboard, touch, and standard gamepad. Rumble uses dual-rumble and ignores a missing or throwing actuator.
- Original procedural Web Audio: wind, insects, a made-up bird phrase, distant thunder, and an original string-and-brass loop. Not a tune from a film.
- Two-player and an on-field AI rival are not playable. Shared-pad and second-keyboard maps are implemented and documented. Four named rival personalities and an adaptive rule were checked as pure decisions. They do not spawn a second hopper.

## How the checks were run

Headless Chromium via Playwright, driving the real page. Keyboard, mouse, simulated touch pointer events, and a fake standard-mapping gamepad injected through `navigator.getGamepads`. A query flag on the test URL exposes placement and bonus helpers used only to reach late states; hop, collision, scoring, pickups, and the egg trigger still run the game's own code. The file was also opened from a `file:` URL in that same headless browser.

## Checks

| Check | Result |
|---|---|
| Boot to title, Play control present | PASS |
| No console or page errors on boot | PASS |
| No network request besides the document | PASS |
| Start a run (keyboard confirm) | PASS |
| First crossing has 82 lanes | PASS |
| Mirage cell is on the level | PASS |
| Starter fruit and four powers are on the first bank | PASS |
| Keyboard hop left | PASS |
| Keyboard hop forward, score increases | PASS |
| Standing in traffic drops a life | PASS |
| Fruit restores a life from 2 to 3 | PASS |
| Super jump pickup and activate | PASS |
| Speed boost pickup and activate | PASS |
| Shield pickup and activate | PASS |
| Slow time pickup and activate | PASS |
| Short hop score versus charged leap score (leap paid more) | PASS |
| Hop into the frozen mirage | PASS |
| Ice coat unlocks | PASS |
| Sloth hopper unlocks | PASS |
| Bonus boomerang starts, scores, and ends | PASS |
| Bonus log surf starts, scores, and ends | PASS |
| Bonus dust dash starts, scores, and ends | PASS |
| Bonus rodeo hop starts, scores, and ends | PASS |
| Difficulty cycles off Normal | PASS |
| Difficulty survives reload | PASS |
| Penguin unlocks survive reload | PASS |
| Reaching the last bank opens the tally | PASS |
| Gamepad stick hop after a button wakes the pad | PASS |
| Analog right trigger charges, and the release leaps (this run died on the landing) | PASS |
| Gamepad X uses a queued power | PASS |
| Menu button pauses | PASS |
| `playEffect('dual-rumble')` is called, and the in-game rumble log records it | PASS |
| A throwing actuator does not crash the page | PASS |
| A missing actuator does not crash the page | PASS |
| `readPad` full scheme: A, LT 0.4, RT 0.73, X, Menu | PASS |
| `readPad` shared right-stick scheme | PASS |
| Fixed rivals: Cautious Cal sidesteps, Reckless Riff hops the same board | PASS |
| Adaptive rival waits after recorded highway deaths; fixed mode ignores that memory | PASS |
| Touch controls can be forced on | PASS |
| Touch hop button moves the kangaroo | PASS |
| Offline render of the score and wind is non-silent (RMS about 0.037) | PASS |
| Audio context unlocks after a click | PASS |
| No console errors at the end of the run | PASS |
| Still no third-party network | PASS |
| Resize to a narrow portrait and a phone landscape, no page error | PASS |
| Hiding the document pauses a live run | PASS |
| `file:` URL boots and starts a run in headless Chromium | PASS |
| Real Mac Safari | NOT TESTED |
| Real Mac Chrome, outside this headless Chromium | NOT TESTED |
| Real iPad Safari | NOT TESTED |
| Real phone | NOT TESTED |
| Real Xbox or 360 pad over Bluetooth | NOT TESTED |
| Physical rumble motor | NOT TESTED |
| Human listening to the score | NOT TESTED |
| A timed human play of a full eight-minute crossing | NOT TESTED |
| Playable two-player match | NOT TESTED (not shipped) |
| On-field AI rival race | NOT TESTED (not shipped) |

48 scripted checks passed, plus resize, hide-to-pause, and the file URL boot.

## Known limits

- The look is a saturated cartoon, with readable animals, cast shadows, and squash on the hop. It is not a photoreal scene.
- Level 1 is 82 lanes. Later crossings are in the same range. Par is eight minutes. A careful player is who that par is for. It was not timed with a person.
- A full-trigger leap from the first bank can land in traffic and cost a life. That is the risk on the multiplier.
- Utes, trains, cattle, and crocs are original side-view drawings, simple at lane size.
- Two-player and the rival race are the next muster. The input split and the rival decisions are in the build and covered above.
- Safari, iPad, a physical pad, the rumble hardware, and a person's ears were not available here.
