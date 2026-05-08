# Outlaw Air Service Experimental QA Checklist

Purpose: verify that OAS behaves consistently as a lightweight operations sandbox and personal flight journal.

North star: Choose the flight -> Fly the operation -> Preserve the story.

Use this checklist for regression passes after UI, economy, timer, preset, save, or Flight Log changes.

## Test Setup

- [ ] Open the Experimental app fresh in a modern browser.
- [ ] Confirm the app loads without script errors or broken images.
- [ ] Confirm the banner/header renders correctly in Night Mode.
- [ ] Toggle Day Mode and Night Mode once before testing.
- [ ] Create a Backup Save before destructive tests.
- [ ] If testing from a dirty save, note starting cash, debt, rep, fleet location, and log count.

## v0.6.7 Paper EFB Visual Pass

- [ ] Day Ops uses the warm Aviation Cream canvas instead of pure white.
- [ ] Night Ops keeps the outer cockpit shell dark while data cards stay light and readable.
- [ ] Pilot's Choice inputs and dropdowns use white fields with dark text in Day and Night Ops.
- [ ] Estimate (if known) reads as a distinct solid action button.
- [ ] Top navigation labels read 1 - Pilot's Choice, 2 - Dispatch, 3 - Aircraft, 4 - Score.
- [ ] Top navigation buttons look clickable and scroll to the correct sections.
- [ ] Available Aircraft table keeps Paper EFB contrast in Day and Night Ops.
- [ ] Company Ledger stat cards keep Paper EFB contrast in Day and Night Ops.
- [ ] Flight Log entries look like readable archived dispatch records.
- [ ] Profit, loss, and ABORTED entries remain easy to scan.

Expected result: OAS feels like a cockpit shell around readable dispatch paperwork.

## First-Run Operational Flow

- [ ] On a fresh/default save, confirm Pilot's Choice appears as the primary first action.
- [ ] Confirm Quick Contract and Browse Jobs are present but visually secondary.
- [ ] Confirm the Dispatch Card starts in the ready/create-operation state.
- [ ] Confirm Pilot's Choice starts collapsed and the EFB Dispatch Hub is the startup focus.
- [ ] Confirm Create Operation (Pilot's Choice) opens Pilot's Choice and scrolls to it.
- [ ] Confirm inline guidance tells the user what to do next.
- [ ] Confirm the OPS FLOW / QUICK OPS strip describes the current flow clearly.
- [ ] Confirm no popups appear during normal first-run flow.

Expected result: a new user can understand where to start without reading external instructions.

## Pilot's Choice Flow

- [ ] Select each Operation Preset once and confirm the operation type/risk update.
- [ ] Confirm preset flavor text updates and remains advisory only.
- [ ] Enter valid 3 or 4 character airport identifiers.
- [ ] Enter a manual distance and create the operation.
- [ ] Use Estimate on known routes and confirm distance updates when available.
- [ ] Confirm route, aircraft, operation type, risk, and distance remain editable before creation.
- [ ] Confirm a created Pilot's Choice operation auto-selects the chosen aircraft.
- [ ] Confirm aircraft can be changed after creation.
- [ ] Confirm payout, timer target, and aircraft row highlight update after aircraft changes.

Expected result: Pilot's Choice feels flexible, user-controlled, and not restrictive.

## Quick Contract Flow

- [ ] Generate a Quick Contract from the Dispatch Card start state.
- [ ] Confirm the app scrolls/focuses to the Dispatch Card.
- [ ] Confirm guidance says to assign an aircraft.
- [ ] Confirm only compatible owned aircraft appear.
- [ ] Pick an aircraft and confirm Dispatch Card changes to ready/review state.
- [ ] Confirm Quick Contract does not replace Pilot's Choice as the primary flow.

Expected result: Quick Contract works as a fast "surprise me" mode.

## 5-Job Board Flow

- [ ] Generate Browse Jobs / 5-Job Board.
- [ ] Confirm five jobs appear with route, type, risk/tier, and base value.
- [ ] Pick a job and confirm it becomes the active dispatch.
- [ ] Confirm aircraft assignment guidance appears.
- [ ] Confirm job board clears or becomes secondary after selecting a job.
- [ ] Confirm no stale job remains active after completion, abort, cancel, or clear dispatch.

Expected result: job board is optional quick-start content, not the main app identity.

## Dispatch Card Sequencing

- [ ] No active operation: Dispatch Card shows EFB Dispatch Hub / Awaiting Dispatch Orders.
- [ ] Operation created with no aircraft: Dispatch Card says Pick aircraft.
- [ ] Aircraft assigned: Dispatch Card shows route, aircraft, distance, risk/cargo, payout, timer target, summary.
- [ ] Pilot's Choice creation guidance says Operation Created and points to Dispatch Card review.
- [ ] EFB Dispatch Card uses Paper EFB data cards instead of dark data panels.
- [ ] EFB Dispatch Card does not contain a Complete Operation button.
- [ ] EFB control row is Start Operation | Pause/Resume | Reset Timer | Cancel Dispatch.
- [ ] Timer running: guidance says complete only after arrival.
- [ ] Timer paused: guidance says resume or reset if restarting.
- [ ] Operation completed: guidance points to Flight Log or next operation.
- [ ] Dispatch canceled: guidance says no log entry or financial penalty was recorded.

Expected result: the card always answers "what happens next?"

## Aircraft Assignment Logic

- [ ] Pilot's Choice manual mode allows the full aircraft list.
- [ ] Quick Contract only shows compatible owned aircraft.
- [ ] 5-Job Board selected jobs only show compatible owned aircraft.
- [ ] Aircraft note text is pilot-facing and never says "Loaded from aircraft.html."
- [ ] Aircraft row highlight follows the selected aircraft.
- [ ] Timer target updates when aircraft changes.
- [ ] Payout updates when aircraft changes.
- [ ] Operation Penalties expands automatically after aircraft selection.
- [ ] Bonus Rules expands automatically after aircraft selection.
- [ ] Cost / Penalty expands automatically after aircraft selection.

Expected result: aircraft choice matters without exposing implementation details.

## Operation Timer

- [ ] Start Operation begins the live timer.
- [ ] Start Operation remains disabled until an aircraft is selected.
- [ ] Attempting to start the timer without aircraft selection is blocked.
- [ ] Pause / Resume appears as one dynamic button, not two separate buttons.
- [ ] Timer running state changes the dynamic button label to Pause.
- [ ] Timer paused state changes the dynamic button label to Resume.
- [ ] Pause freezes the timer.
- [ ] Pausing the timer smoothly guides the view to the Company Ledger closeout area.
- [ ] Resume continues from the paused value.
- [ ] Reset Timer returns to 00:00:00.
- [ ] Complete Operation captures actual elapsed time in the Flight Log.
- [ ] Completing with timer still running opens confirmation.
- [ ] Completing under 1 minute opens confirmation.
- [ ] Completing very soon after dispatch creation opens confirmation.
- [ ] Return to Dispatch closes confirmation and does not log anything.
- [ ] Confirm Complete Operation logs exactly one entry.

Expected result: timer behaves like an optional EFB companion, not enforcement.

## Cancel Dispatch vs Abort / Fail

- [ ] Cancel Dispatch opens a confirmation prompt.
- [ ] Canceling the prompt returns to the active dispatch unchanged.
- [ ] Cancel Dispatch clears the current dispatch.
- [ ] Cancel Dispatch does not charge operating cost.
- [ ] Cancel Dispatch does not charge insurance.
- [ ] Cancel Dispatch does not charge debt/relocation/failure cost.
- [ ] Cancel Dispatch does not write a Flight Log entry.
- [ ] Abort / Fail opens a confirmation warning.
- [ ] Abort / Fail can be canceled from the browser confirmation.
- [ ] Abort / Fail records a failed operation when confirmed.
- [ ] Abort / Fail charges the expected penalty/costs.
- [ ] Abort / Fail writes an ABORTED entry to the Flight Log.

Expected result: planning cleanup and true failed operations feel clearly different.

## Flight Log Validation

- [ ] Completed flights show operation title, route, aircraft, gross, costs, penalty, net, date.
- [ ] Pilot's Choice entries show preset when applicable.
- [ ] Timer entries show Operation Time when timer was used.
- [ ] Memo text appears under the correct log entry.
- [ ] Edit Memo / Add Memo changes only the memo text and leaves route, gross, costs, penalty, timer, and net locked.
- [ ] Completing or aborting an operation opens the Flight Log and highlights the newest entry.
- [ ] Empty memo does not create awkward blank blocks.
- [ ] Abort entries show ABORTED title, gross 0, costs, abort penalty, event, memo if provided.
- [ ] Copy Log Text includes route, aircraft, gross, costs, penalty, net, event, preset, time, and memo.
- [ ] Print / Save Log produces a readable output.
- [ ] Log remains readable after many entries.

Expected result: Flight Log works as both journal and QA/debugging surface.

## Notable Flights

- [ ] Best Net selects the highest positive net entry.
- [ ] Longest Timer selects the longest actual operation time.
- [ ] Latest Entry reflects the most recent log entry.
- [ ] Aborted negative entries do not become Best Net unless all entries are negative.
- [ ] Notable Flights hides or remains graceful with no log entries.

Expected result: notable summaries reinforce operational memory.

## Economy and Payout Sanity

- [ ] C152/C172 short operations produce sensible low-tier payouts.
- [ ] C208/utility operations produce medium payouts.
- [ ] C-47 or similar vintage cargo operations cover operating cost on appropriate presets.
- [ ] C-17 / heavy cargo operations produce positive net on Heavy Cargo after costs.
- [ ] Scenic/Ferry operations with higher-cost aircraft do not unexpectedly clamp to $0 when completed successfully.
- [ ] Gross, costs, and net shown in Dispatch Card match the Flight Log after completion.
- [ ] Bonuses increase estimated and logged net.
- [ ] Penalties reduce estimated and logged net.
- [ ] Net never becomes visually misleading when gross and costs exist.

Expected result: economy remains an incentive, not a grind or punishment trap.

## Preset Payout Validation

Run at least one test flight for each preset using a reasonable aircraft:

- [ ] Freeform / Pilot's Choice
- [ ] Alaska Bush Ops
- [ ] Pacific Northwest Cargo
- [ ] Caribbean Island Hopper
- [ ] European Charter
- [ ] Amazon Jungle Supply
- [ ] Arctic Survival
- [ ] Desert Cargo Corridor
- [ ] VIP Charter
- [ ] Heavy Cargo
- [ ] Medical Relief Flights
- [ ] Night Ops
- [ ] Scenic Touring

For each preset:

- [ ] Correct operation type is selected.
- [ ] Risk feels appropriate.
- [ ] Ops Desk advisory matches the operation flavor.
- [ ] Gross is nonzero.
- [ ] Estimated net is sensible for the selected aircraft.
- [ ] Completed Flight Log entry matches the expected preset.

Expected result: presets guide atmosphere and payout scale without enforcing gameplay rules.

## Heavy Aircraft Validation

- [ ] C-17 on Heavy Cargo produces a positive net after operating costs.
- [ ] C-17 on inappropriate light/scenic operations either remains low reward or clearly reflects high operating cost.
- [ ] Heavy Cargo timer target is reasonable for distance and cruise speed.
- [ ] Heavy aircraft costs display correctly in Cost / Penalty.
- [ ] Heavy aircraft Flight Log entries preserve gross/cost/net clearly.

Expected result: heavy aircraft feel expensive but viable when used for appropriate operations.

## Company Setup Persistence

- [ ] Change Company Name and confirm it persists after refresh.
- [ ] Change Home Base and confirm it persists after refresh.
- [ ] Set custom home base and confirm it displays correctly.
- [ ] Set Fleet Location to Home Base and confirm fleet location updates.
- [ ] Clear Dispatch confirms before clearing active dispatch planning state.
- [ ] Clear Dispatch does not reset company setup.
- [ ] Reset Career warning names the career data and Flight Log impact before confirming.
- [ ] Reset Career restores defaults only after confirmation.
- [ ] Take Loan confirms debt added before changing cash/debt.

Expected result: Company Setup supports identity and continuity without feeling like a management sim.

## Insurance Behavior

- [ ] None shows $0 and no maintenance-hit reduction.
- [ ] Basic shows estimated per-flight cost and reduced maintenance-hit probability.
- [ ] Premium shows higher estimated per-flight cost and stronger maintenance-hit reduction.
- [ ] Insurance cost appears in Cost / Penalty estimate.
- [ ] Insurance cost is included in completed flight costs.
- [ ] Cancel Dispatch does not charge insurance.
- [ ] Abort / Fail charges insurance only when a failed operation is confirmed.

Expected result: insurance is optional, readable, and not surprising.

## Save / Export / Import

- [ ] Backup Save generates save text.
- [ ] Copy Save copies the current save text when available.
- [ ] Restore Save accepts a valid backup and restores state.
- [ ] Invalid restore text shows a clear failure message.
- [ ] Restore preserves company setup, fleet, cash, debt, rep, log, and stats.
- [ ] Backup before Reset Career can restore the prior state.
- [ ] Save data survives browser refresh.

Expected result: save tools are trustworthy and understandable.

## Mobile / Tablet Readability

- [ ] Test phone portrait width.
- [ ] Test tablet portrait width.
- [ ] Test tablet landscape width.
- [ ] Buttons stack cleanly without text overlap.
- [ ] Pilot's Choice form fields remain usable.
- [ ] Dispatch Card remains readable.
- [ ] Timer controls remain tappable.
- [ ] Flight Log entries scan cleanly.
- [ ] No section requires hover-only behavior.

Expected result: OAS remains console-friendly as a phone/tablet EFB companion.

## Day vs Night Mode

- [ ] Day Mode uses the Paper EFB look for operational data cards.
- [ ] Night Mode keeps Paper EFB data containers light grey with dark text.
- [ ] Night Mode retains navy/gold/silver branding.
- [ ] Day Mode remains readable and does not wash out important guidance.
- [ ] Ops Desk advisory is readable in both modes.
- [ ] Next Step guidance is readable in both modes.
- [ ] Buttons maintain clear priority in both modes.
- [ ] Flight Log net values are readable in both modes.
- [ ] Section hierarchy remains clear in both modes.

Expected result: both modes preserve operational clarity.

## Ops Desk Advisory Behavior

- [ ] Advisory appears on active dispatches.
- [ ] Advisory has the Ops Desk label.
- [ ] Advisory changes appropriately by preset/type.
- [ ] Advisory does not pop up or interrupt workflow.
- [ ] Advisory does not change randomly during timer updates.
- [ ] Advisory remains short and operational.
- [ ] Advisory never implies hard enforcement or real-world dispatch validity.

Expected result: Ops Desk adds subtle life without becoming tutorial clutter.

## README vs App Flow Consistency

- [ ] README Launch App link points to Experimental app.
- [ ] README repo links point to Experimental repo where appropriate.
- [ ] README Pilot's Choice description matches current app.
- [ ] README Operation Timer description matches current timer controls.
- [ ] README Company Setup description matches current controls.
- [ ] README Save System warning matches actual backup/restore behavior.
- [ ] README future direction does not promise current unavailable features as current features.
- [ ] README Index links work on GitHub.

Expected result: a new user can understand the current app without stale instructions.

## Edge-Case and Regression Tests

- [ ] Create operation with invalid airport code and confirm validation works.
- [ ] Create same-origin/same-destination operation and confirm only scenic/training exceptions apply.
- [ ] Try Complete Operation with no active dispatch.
- [ ] Try Complete Operation with no aircraft selected.
- [ ] Start timer with no active dispatch.
- [ ] Resume timer with no active dispatch.
- [ ] Generate a new operation while one is active and confirm app blocks it.
- [ ] Change aircraft after timer started and confirm payout/timer remain coherent.
- [ ] Clear Dispatch from Company Setup and confirm no log entry is created.
- [ ] Reset Career and confirm operation state, timer, log, and company data reset.
- [ ] Test after browser refresh during active dispatch.
- [ ] Test after restoring a save made before recent QA fixes.

Expected result: edge cases fail gracefully and do not corrupt the operational story.

## Release Readiness Notes

- [ ] Paper EFB data cards remain readable in both Day Ops and Night Ops.
- [ ] Available Aircraft table remains readable in both Day Ops and Night Ops.
- [ ] Company Ledger stats remain readable in both Day Ops and Night Ops.
- [ ] No known payout path produces unexpected $0 net on successful, appropriately scaled operations.
- [ ] Cancel Dispatch and Abort / Fail semantics are clear in UI and Flight Log.
- [ ] Flight Log entries remain useful for QA and enjoyable as pilot history.
- [ ] No pilot-facing text exposes implementation details.
- [ ] No new feature adds heavy management, grind, or rigid enforcement.
- [ ] App still feels lightweight, browser-based, console-friendly, and honor-system driven.

Final release-readiness question: can a brand-new user understand what to do next at every major state?
