# Modern Sleep Test Checklist

Use this checklist for manual emulator testing after `Modernize sleep duration`.
Mark each item pass/fail and record the ROM, save, party, opponent, and move used.

## Build And Data Checks

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Clean build | `make clean && make` completes successfully. | |
| Manifest | `ENGINE_MANIFEST.md` documents inflicted sleep as 1-3 turns and Rest as fixed. | |
| No critical-hit changes | Critical-hit behavior is unchanged in this commit. | |

## Inflicted Sleep Duration

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Sing sleep | Use `SING` repeatedly in wild or trainer battles. | Successful inflicted sleep uses a short 1-3 turn range. | |
| Hypnosis sleep | Use `HYPNOSIS` repeatedly. | Successful inflicted sleep uses a short 1-3 turn range. | |
| Sleep Powder sleep | Use `SLEEP_POWDER` repeatedly. | Successful inflicted sleep uses a short 1-3 turn range. | |
| Spore sleep | Use `SPORE` repeatedly. | Successful inflicted sleep uses a short 1-3 turn range. | |
| Battle Tower sleep | Test a Battle Tower-style battle if available. | Inflicted sleep still uses the same Crystal Modern 1-3 turn range. | |

## Rest Regression

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Rest healing | Use `REST` below full HP. | User heals to full, clears status, and becomes asleep. | |
| Rest duration | Track turns after `REST`. | Rest remains fixed self-inflicted sleep behavior and was not changed to the random 1-3 inflicted range. | |
| Rest at full HP | Use `REST` at full HP. | Existing failed/full-HP behavior is unchanged. | |

## Move And Status Regression

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Snore | A sleeping Pokemon can still use `SNORE` according to existing rules. | |
| Sleep Talk | A sleeping Pokemon can still use `SLEEP_TALK` according to existing rules. | |
| Nightmare | Nightmare still requires the target to be asleep and clears when the target wakes. | |
| Held sleep cure | Mint Berry or equivalent held sleep cure still wakes the Pokemon. | |
| Sleep prevention item | Existing held sleep-prevention behavior still blocks sleep. | |
| Substitute | Substitute still blocks sleep where it did before. | |
| Already asleep text | Sleep moves still fail with the already-asleep message against sleeping targets. | |
