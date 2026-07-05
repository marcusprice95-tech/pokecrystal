# Modern Confusion Test Checklist

Use this checklist for manual emulator testing after `Modernize confusion self-hit chance`.
Mark each item pass/fail and record the ROM, save, party, opponent, and move used.

## Build And Data Checks

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Clean build | `make clean && make` completes successfully. | |
| Manifest | `ENGINE_MANIFEST.md` documents approximately 1/3 confusion self-hit chance. | |
| Duration preserved | Standard confusion duration remains 2-5 turns. | |
| No critical-hit changes | Critical-hit behavior is unchanged in this commit. | |

## Self-Hit Chance

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Player confusion | Have the player Pokemon become confused with `CONFUSE_RAY`, `SUPERSONIC`, `SWEET_KISS`, or a confusion secondary effect. Record at least 60 confused action attempts. | Self-hit rate should be roughly one third, allowing for random variance. | |
| Enemy confusion | Confuse an enemy Pokemon and record at least 60 confused action attempts. | Enemy self-hit rate should be roughly one third. | |
| Confusion can still act | While confused, the Pokemon should often act successfully. | Confusion no longer feels like a 50/50 lockout. | |

## Duration And Cure Regression

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Confusion duration | Confusion still lasts 2-5 turns before printing the confused-no-more message. | |
| Bitter Berry / confusion cure | Held confusion-curing items still remove confusion normally. | |
| Safeguard | Safeguard still blocks confusion where it did before. | |
| Substitute | Substitute still blocks confusion where it did before. | |
| Existing moves | `CONFUSE_RAY`, `SUPERSONIC`, `SWEET_KISS`, `DIZZY_PUNCH`, `PSYBEAM`, and `DYNAMICPUNCH` still apply confusion according to their move data. | |

## Berserk Gene

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Berserk Gene activation | Give a Pokemon Berserk Gene and enter battle. | Attack rises and confusion starts. | |
| Berserk Gene duration | Track the confusion counter after Berserk Gene activates. | Confusion lasts a normal 2-5 turns, not 256 turns or a stale previous count. | |
| Berserk Gene self-hit chance | Record confused action attempts after Berserk Gene activation. | Self-hit rate follows the same roughly one-third rule. | |
