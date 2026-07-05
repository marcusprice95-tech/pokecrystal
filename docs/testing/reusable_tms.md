# Reusable TMs Test Checklist

Use this checklist for manual emulator testing after `Make TMs reusable`.
Mark each item pass/fail and record the ROM, save, map, party, and TM/HM used.

## Build And Data Checks

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Clean build | `make clean && make` completes successfully. | |
| TM move list | `data/moves/tmhm_moves.asm` is unchanged by reusable TMs. | |
| TM/HM capacity | `NUM_TMS`, `NUM_HMS`, and `NUM_TM_HM_TUTOR` are unchanged. | |
| Save structures | `wTMsHMs` remains the same byte-per-TM/HM storage; no SRAM layout changes are introduced. | |

## Teaching Behavior

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Successful TM teach | Own one TM, teach it to a compatible Pokemon, then reopen the TM/HM pocket. | The Pokemon learns the move and the TM remains available. | |
| Cancel before teaching | Select a TM, choose a Pokemon, then cancel before learning. | The TM remains available. | |
| Incompatible Pokemon | Use a TM on an incompatible Pokemon. | The TM remains available and the incompatible message appears. | |
| Pokemon already knows move | Use a TM on a Pokemon that already knows that move. | The TM remains available and no duplicate move is learned. | |
| Existing stacked TM save | Load or create a save state where a TM quantity is greater than 1. | The TM behaves as owned and reusable; quantity is not shown in the TM/HM pocket. | |

## HM Regression

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Successful HM teach | Teach any HM to a compatible Pokemon. | HM behavior matches vanilla Crystal and the HM remains available. | |
| HM field use | Teach a field HM such as CUT or SURF and use it in the overworld with normal badge requirements. | Field move behavior is unchanged. | |
| HM cannot be tossed | Try to toss an HM from the TM/HM pocket. | HM still cannot be tossed. | |

## Bag And Pocket Behavior

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| TM quantities hidden | The TM/HM pocket shows TM numbers and move names but no `xNN` TM quantity. | |
| TM cannot be tossed | Selecting a TM does not offer or allow a successful toss. | |
| TM menu usability | Selecting a TM still opens the normal teaching flow. | |
| Pocket scrolling | TM/HM pocket scrolling and CANCEL behavior remain stable with several TMs and HMs owned. | |

## Mart Behavior

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Buy new TM | Buy a TM not currently owned from a mart that sells TMs. | The purchase succeeds and adds one owned TM. No stacking is visible. | |
| Buy owned TM | Try to buy the same TM again. | Purchase is blocked with an owned-TM message before money is taken. | |
| Buy normal item | Buy a regular stackable item such as POTION. | Quantity selection and item stacking still work normally. | |
| Sell TM | Try to sell a TM. | The mart refuses to buy it. | |
| Sell normal item | Sell a normal tossable item. | Selling behavior is unchanged. | |

## PC And Held Item Behavior

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Deposit TM in PC | Open the player's PC item storage and try to deposit a TM. | The TM is not deposited. | |
| Deposit normal item in PC | Deposit a normal item such as POTION. | PC item deposit behavior is unchanged. | |
| Pokemon hold TM from pack | Try to give a TM to a Pokemon from the pack. | The Pokemon cannot hold the TM. | |
| Pokemon hold normal item | Give a normal held item to a Pokemon. | Held-item behavior is unchanged. | |

## Reward And Duplicate Behavior

| Test | Suggested setup | Expected result | Pass/Fail notes |
| --- | --- | --- | --- |
| Item ball TM | Pick up a TM item ball. | The TM becomes owned. Existing map event behavior is otherwise unchanged. | |
| Gift TM | Receive a scripted gift TM. | The TM becomes owned. Gift/map scripts are not redesigned in this milestone. | |
| Duplicate TM reward | Receive a TM already owned, if a test setup allows it. | Ownership remains stable and does not create meaningful quantity stacking. | |

## Link And Compatibility Notes

| Test | Expected result | Pass/Fail notes |
| --- | --- | --- |
| Time Capsule policy | Crystal Modern does not attempt Time Capsule compatibility for modern engine features. | |
| Link held item safety | Since Pokemon cannot hold TMs, TMs should not be introduced into link trades as held items through normal menus. | |
