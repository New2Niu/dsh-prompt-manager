# Changelog

## Unreleased

- With the **Prompts** control hidden, the prompts a session has attached no longer vanish from view: they render as chips in the dock directly above the composer. Each chip shows the prompt title and a remove button, and removing a chip cancels that prompt — so a `/提示词` pick still has a visible result and a way back when the tool-row control is off. The row mirrors the control's request states too: a dimmed pending chip while a pick is being activated, and an error chip with a retry action when the host rejects it. The settings hint for the switch now mentions the chips.
- Tightened the prompt cards in settings: the excerpt now sits in the left content column and is limited to a single line with an ellipsis, so it stops before the visibility switch instead of running underneath the action buttons, and the switch / actions are vertically centered in the card. Cards no longer shrink when the list hits its max height, which previously clipped the second line. The paragraph explaining where hidden prompts go has been removed. The row still stacks on narrow screens without horizontal overflow.
- Restyled the **Prompts** control in the composer tool row to match the host's other toolbar entries (and `dsh-ide-git`'s pills): a transparent 8px-radius target with an 8px inset, 13px label in the secondary text color, a 14px icon and a 10px chevron. The label now **is** the state — it reads `提示词` when nothing is attached and the prompt's own title once one is picked, with extra picks folded into a `+N` badge — instead of a brand-colored `提示词 · 标题` pill with a check mark. Hover and expanded use the host's hover fill.
- Restyled the composer prompt picker so it reads as a DSH menu instead of a small form: a 16px surface with 6px padding, an inset filled search field instead of a bordered input flush against the edge, a plain “已加入 / 全部移除” status row instead of a filled banner, tighter 36px rows, and a single check mark replacing the square checkbox. The settings search field keeps its own bordered style.
- Added a display switch at the top of the Prompt Manager settings page that hides or restores the **Prompts** control in the composer tool row. The slash commands (`/prompt`, `/提示词`, `/keyword`) keep working either way, and the choice is remembered per browser.
- Added a visibility switch to every prompt card. Hidden prompts stay in the library, keep their injections, and still appear in settings, but are left out of the composer picker and the `/keyword` candidate list. The flag travels with exports, imports, and the local mirror file.
- The `/prompt` and `/提示词` slash commands now accept abbreviations: any two-or-more-character prefix (`/pr`, `/pro`, `/prom`, `/提示`) opens the full prompt list just like the full alias. Single letters and lookalikes such as `/promptly` still search normally, and a leading space (`/ pro`) searches the alias text itself.

## 1.6.0 - 2026-10-27

- Aligned with DSH 0.2.1-rc.3: declared `engines.dsh` and `dsh.manifestVersion` so the plugin manager can evaluate compatibility, and verified the Host routes, settings page, composer picker, and per-session injection against the new release.
- Used DSH 0.2.1's literal prompt sections (`interpolate: false`) so `{{placeholders}}` reach the model exactly as written. Older DSH releases still receive the brace-escaping fallback.
- Resolved the plugin's API paths against the document directory so they keep working when DSH is published under a reverse-proxy path prefix (`--public-url https://host/dsh/`).
- Kept prompt reads and mutations local-only on DSH 0.2.x public deployments by also requiring a loopback `Host` authority; `DSH_PROMPT_MANAGER_ALLOW_REMOTE=1` remains the explicit opt-out.

## 1.5.2 - 2026-09-27

- Improved contrast in DSH 0.1.7-rc.2: search and form placeholders no longer use the barely visible dimmed label color.
- Matched the built-in plugin inventory search field and settings card tokens, adopted the official isolated frosted menu material, and kept the composer picker inside narrow viewports without horizontal scrolling.

## 1.5.1 - 2026-09-27

- Fixed a multi-tab sync loop: pages now observe another tab's library changes without posting them back to the host. Concurrent edits still merge, and identical content no longer causes repeated revision conflicts or a flashing conflict notice.

## 1.5.0 - 2026-08-23

- Fixed user-added prompts being reset to the four seed prompts after a DSH restart. The desktop app serves the Web UI on a fresh port each launch, which isolates browser `localStorage` by origin; the prompt library is now mirrored to a durable local file (`$DSH_HOME/dsh-prompt-manager/prompts.json`) and restored from it when the browser copy is missing.
- Fixed the primary "新建"/"New" button blending text into its background in both light and dark themes. It now uses the DSH button fill and foreground tokens instead of the non-inverting `brand-primary-invert` token, and the picker check mark follows the same fix.
- Preserved intentionally empty libraries, kept hydration read-only until the host copy is known, and added revision-based conflict handling with serialized client writes.
- Made host persistence private and crash-safe with owner-only permissions, a serialized mutation queue, and same-directory atomic replacement. Corrupt files are retained as `prompts.json.corrupt-*` before an explicit repair write.
- Restricted prompt-library and active-session reads to the local machine by default, matching the existing mutation policy.

## 1.4.1 - 2026-08-15

- Kept mouse-wheel and touchpad scrolling inside the prompt picker instead of scrolling the conversation behind it.
- Contained overscroll at both ends of the prompt list so the background remains still while the picker is open.

## 1.4.0 - 2026-08-15

- Rebuilt the composer picker as a compact menu anchored directly above the Prompts control, matching DSH's model menu behavior.
- Added multi-select injection so a session can use several ordered prompts at once and remove them independently.
- Migrated existing single-prompt browser records automatically and preserved prompt-set inheritance across conversation branches.
- Replaced fixed success-green injection styling with DSH theme tokens so active states follow the selected theme color.
- Removed the redundant Done button from the always-visible Settings library.

## 1.3.0 - 2026-08-15

- Moved prompt activation into a compact control inside the composer tool row, beside the access-mode control.
- Added a searchable composer popup for selecting, switching, and removing the current session prompt.
- Removed Inject actions and active badges from Settings so the prompt library is clearly management-only.
- Made forked sessions inherit the nearest ancestor prompt and show that inherited state in the composer.
- Added persistent per-session disable overrides so removing an inherited prompt remains effective after restart.

## 1.2.0 - 2026-08-15

- Changed prompt selection from inserting text into the composer to injecting it as a session-level system prompt.
- Added an active-prompt status bar above the composer with one-click removal and retry states.
- Added Inject actions and active-state badges to Prompt Manager settings.
- Kept injections isolated by session and restored them after a DSH restart from browser-local state.
- Added loopback-only mutation protection, same-origin checks, input limits, and Host regression tests.
- Escaped `{{placeholder}}` pairs so user templates cannot accidentally trigger DSH system-prompt variable errors.

## 1.1.0 - 2026-08-15

- Added Chinese and English interfaces that follow the DSH language setting.
- Added JSON backup import and export with merge and replace modes.
- Added favorites, usage-aware ordering, and both `/提示词` and `/prompt` aliases.
- Added schema validation, legacy-data migration, storage failure warnings, and reliable cross-tab clearing.
- Improved keyboard, mobile, focus, and touch accessibility.
- Fixed whitespace handling in slash-menu descriptions.
- Added core regression tests and official DSH bundle metadata.

## 1.0.0

- Initial prompt library, search, editing, clipboard copy, and `/提示词` insertion.
