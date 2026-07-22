# Release Notes 4.0 (English)

> Major release · changes since version **3.0.2**
> **Note:** These release notes cover the current preview state and have so far been generated up to and including **4.0.0-preview.4**. They will be extended with the upcoming preview/RC builds through the final 4.0.0.

4.0 is a **major release**. At its core is a **completely rebuilt scheduling engine** modeled on Microsoft Project, together with a thoroughly modernized interface, new web modules (reports, capacity, collaboration), a new **administration portal** and a new installation/rollout mechanism.

---

## ⭐ Highlights at a glance

| | Highlight |
|---|---|
| 1 | **New scheduling** with real predecessor/successor calculation and MS-Project-style constraints |
| 2 | **Project calendars with working hours** (working days, time windows, holidays, ERP sync) |
| 3 | **Modernized interface** incl. dark mode and consistent language (DE/EN) |
| 4 | **ERP integration** right in the Gantt (references, bills of materials, sync status) |
| 5 | **New web reports** with dashboards, a filter wizard and PDF export |
| 6 | **Insert sales offers and offer line items** into a schedule as references |
| 7 | **New installation mechanism via ReadyStackGo** (guided, centralized rollout) |
| 8 | **New administration portal** (web) for configuration, user permissions, maintenance mode, error queue and client rollout |

---

## New scheduling (MS-Project-aligned)

The schedule calculation was rebuilt from the ground up (Critical Path Method, forward/backward pass):

- **Predecessor/successor links** in all four types: **Finish–Start (FS)**, **Start–Start (SS)**, **Finish–Finish (FF)**, **Start–Finish (SF)**, each with **lag/lead**. Move one task and dependent tasks follow automatically and correctly.
- **MS-Project-style constraints**: As Soon As Possible (ASAP), As Late As Possible (ALAP), Start/Finish No Earlier Than (SNET/FNET), Start/Finish No Later Than (SNLT/FNLT), Must Start/Finish On (MSO/MFO).
- **Conflicts are surfaced honestly** instead of silently "smoothed": when a date cannot be met, MS-Project-style **negative slack** with a warning indicator is shown (indicator column in the Gantt) rather than quietly bending the inputs.
- **Summary tasks** correctly roll up their subtasks (start/finish/duration); a directed constraint on a summary acts as a boundary for its children.
- **Automatic or manual** scheduling per task: manually pinned tasks keep their dates but still participate in conflict detection.
- **Milestones** with correct time-of-day handling and clean behavior on non-working days.
- **New warnings and messages column (indicators)** in the Gantt: a dedicated column shows every note per task at a glance – scheduling warnings (unmet constraints, negative slack, predecessor/successor conflicts, dates snapped to working days) as well as ERP sync notices (date drift or overrun). Each icon has an explanatory tooltip, so problems can be spotted and fixed immediately.
- **Warnings update live**: changes to constraints, dates or dependencies immediately refresh the indicator column and the warning counter in the status bar – no need to reload the plan. Warnings are attributed to the actual cause (the same conflict is no longer reported on several tasks).

> 📝 **Note**: Because 4.0 introduces a new scheduling engine, existing projects are migrated to the new engine on upgrade.

## Project calendars with working hours

- Real **working days and working-time windows** (e.g. Mon–Fri 08:00–17:00, multiple windows per day for lunch breaks) instead of plain calendar days.
- **Exceptions/holidays** on a dedicated sub-page per calendar; treated as non-working during scheduling.
- **ERP-synchronized calendars** are read-only in the UI (the ERP is the source) and clearly marked.
- **Default/required calendar**: every project gets a calendar; without an explicit assignment a default calendar applies.
- Per-project assignment under **Settings → Calendar**.
- Detailed step-by-step guide: see the calendar guide.

## Project list & archiving

- **New schedule selection page**: a central landing page for picking and opening schedules – either as a **card view** or a **sortable table view** (toggleable, the choice is persisted).
- **Search and filters** by project name, manager, clerk, business unit and revision, plus **status tabs** (All / Active / Archived) with counts.
- **Archive a project**: schedules can be archived right from the project list. Archived projects appear under the "Archived" tab and are kept read-only. Archiving runs asynchronously with real-time progress.
- **Creator and creation date** of a schedule are captured and shown in the project list.

## Create a project from a sales order/offer

- **Create a new project directly from a sales order or offer**: the create dialog is now web-based and prefills ERP data (e.g. order/offer number, due date, business unit); the new project stays linked to the ERP document.

## Insert offers & orders into a schedule

- **Sales offers and offer line items** can be inserted into an existing schedule via the **"Schedule references"** dialog (**"Assign offers"**) – either the whole offer or specific line items.
- Inserted references appear as **ERP tasks in the Gantt** (document number, type icon, description) and stay **live-synced with ams.erp**.
- **Sales orders and order line items** can be assigned the same way; existing references can be removed individually or all at once.

## ERP integration

- **ERP references and dates** shown directly in the Gantt: labels, type icons and tooltips, including live-created ERP tasks.
- **Bill-of-materials sync** with correct duration (from the working-day span, no longer a fixed "1 day") and without incorrect milestone behavior.
- **Per-task sync status** ("in sync / out of sync") and a **"Re-sync ERP"** button.
- More robust ERP date distribution (a central per-project date hub).

## Task detail view (modernized)

- A task's detail area is new and web-based, embedded in the desktop client (WebView2).
- Tabs for **predecessors**, **discussion**, **notes (memo)** and **bill of materials (BOM)**.
- **Extended predecessor tab**: a **conflict-count badge** on the tab, **conflict-kind icons** with explanatory tooltips, the **lag unit** shown on the fields, **double-click** a predecessor to jump to it, and **removing a predecessor can be undone**.
- **Rename a task title by clicking** it directly in the detail view.
- A task's constraints/dates are maintained here, consistent with the new scheduling.
- The detail view can be **detached into its own window** that reliably stays in the foreground.
- A stuck or hidden detail area can be recovered at any time via **"Reset detail area"**; the conflicts pane is now scrollable.

## Reporting & capacity

- New **web reports** with **dashboards** and a **filter wizard** (configuration without SQL knowledge).
- **Interactive charts**: hot-edit, drill-down, hyperlinks, print and **PDF export** directly from the analysis page.
- **Enhanced PDF export** of reports: configurable margins, page numbers, "fit to width" and optional splitting of large charts across multiple pages (N × M).
- **Capacity report** with clearer charts: configurable chart size and column count, drop-downs for report type/grouping, available-capacity and capacity-factor lines, and clearly highlighted overload notices.
- **Capacity planning** with new web booking dialogs (actual hours, percent complete, production marker); the resource grid additionally shows **order and line item**, and the personnel number can be prefilled via a link (URL parameter).

## Collaboration

- **Discussions** per task, in real time.
- **Notes (memos)** per task; optionally copied along when copying tasks.
- The discussion and notes panes now use the **consistent design system (ConsistentUI)** and blend in seamlessly in look-and-feel and dark mode.

## Copy & paste

- Copy tasks including **subtasks** – or **subtasks only**, without the head task.
- Optionally **include notes** when copying.
- **Visual feedback** in the Gantt: copied and pasted tasks are briefly highlighted, so it is immediately clear what was copied and where it was pasted.

## Interface, language & usability

- **Consistent language (German/English)**: all modules follow the chosen language; **language switcher** in the desktop client (persisted, changeable any time). No more mixed-language UI.
- Modernized **shell**: new title bar, Fluent color palette, **dark mode**.
- **Dark mode expanded**: switching now also applies to the embedded web modules and the WPF menu, and updates live. Dark mode is **not yet complete** – the Gantt chart and some WPF dialogs, among others, will follow in upcoming preview builds.
- Web modules are hosted seamlessly inside the desktop client.
- **Multi-project timeline**: an **edit mode (F2)** prevents accidental date moves. In addition, a **drag-and-drop bug was fixed** – dates now jump to the exact target position (and snap cleanly) instead of drifting due to accumulated mouse movements.
- Consistent **weekend/holiday shading** in the Gantt.
- New built-in **customer documentation portal** (help).

## Administration portal (new) *(for administrators)*

Alongside the application itself there is now a dedicated, web-based **administration portal** with a modern interface (sidebar, dark mode, German/English, sign-in/out showing the signed-in user):

- **Central configuration**: system-wide settings are maintained centrally and activated via a **release switch**; clients load their settings from the server on startup – no more manual distribution of configuration files.
- **User/administrator permissions**: administrators are managed in the portal; the first person to sign in can be promoted to administrator automatically (including a recovery path after a reinstall or handover).
- **Feature flags** and an **audit log** directly in the portal.
- **Maintenance mode**: the system can be put into maintenance – with an announcement and a countdown grace period; signed-in clients are warned in time.
- **Error/queue management**: failed background operations are shown clearly and can be **retried or discarded** individually.
- **mandant.ini import**: existing tenant settings can be read in and applied via a dialog.
- **Client rollout from the portal**: the desktop client can be deployed directly from the portal to a network path – with **live progress**.
- **Bulk revision**: all active projects can be revised in a single run from the portal (the "Revisions" menu item).

## Installation & operations *(for administrators)*

- **New installation mechanism via ReadyStackGo (RSGO)**: the entire application is rolled out centrally and in a guided way – individual services/containers are installed and updated from a manifest, without setting up each component manually.
- **One RSGO for multiple target servers**: the same ReadyStackGo instance can serve several environments/target servers (remote environments).
- **Guided client installer**: sets up the desktop client at the customer site (version selection, tenant number, target directory). The matching version is **fetched from the server on demand**, the tenant number can be prefilled centrally from the configuration, and a permanent background service is no longer required.

## Stability, improvements & fixes in detail

Beyond the headline features, 4.0 includes numerous refinements and bug fixes:

**Opening & session**
- Projects open reliably even after longer periods of inactivity – the session is refreshed automatically instead of failing with a sudden sign-out error.
- Schedules open reliably in distributed installations, too (an internally missing connection detail is now fully resolved).
- The session now survives a **server restart**: security keys and the session store are held centrally, so a restart no longer signs everyone out. The session also stays active beyond the plain access-token lifetime.
- When the sign-in has expired, the desktop client first attempts a **silent re-login** before prompting; transient connection errors to the server are caught and shown as a **friendly message** instead of aborting with an error dialog.

**Scheduling**
- Date-bound milestones (start/finish no earlier/later than) keep their day on non-working days, or move correctly to the next working day.
- "As late as possible" (ALAP) now respects the earliest feasible start date and preserves predecessor/successor order.
- Summary tasks no longer produce spurious "snapped to working day" notices.
- Predecessor/successor links are shown reliably in the overview.
- Dates that cannot be met are consistently shown as negative slack with a warning (MS-Project-conformant).
- Negative slack is attributed to its **actual cause**: predecessors or successors of an unmeetable "no later than" constraint no longer get their own misleading slack warning.
- The **warning counter in the status bar matches the warning icons in the Gantt** – the same conflict is no longer counted twice.
- Warnings appear **live**, without reloading the plan.
- A **start-to-start successor** of an end-of-day milestone keeps the shared start date; a **duration change on a manually scheduled task** re-schedules its finish correctly.

**ERP integration**
- Correct labels and type icons, including for live-created ERP tasks.
- No more date offset (−1 day) on ERP plan dates.
- Bill-of-materials sync with correct duration and without incorrect milestone behavior.
- Inherited order references no longer carry an incorrect ERP due date.
- Fixed a display crash for certain live-created ERP tasks.

**Reports & capacity**
- More robust PDF export: the export dialog no longer closes accidentally, works in kiosk mode and exports all charts.
- Correct German date format in the export columns.
- Overload notices are shown correctly even at 0 hours; stable, consistent label colors across all capacity charts.
- Fixed an infinite loop in the capacity calculation of large work plans; the capacity overview is sorted chronologically and falls back per work center on overload.

**Administration portal**
- Language switching (DE/EN) works reliably; sign-out button and display of the actually signed-in user.
- Icons and forms render correctly; navigation is legible in dark mode.
- Fixed saving of the configuration.

**Interface & desktop**
- The WPF menu follows dark mode (neutral grey instead of AMS blue).
- The detail window reliably stays in the foreground; a stuck detail area can be recovered via "Reset detail area".
- Form fields no longer lose their values when they are only shown behind a condition.
- Leaving a plan cleanly closes the active plan and its menus.
- Copy/paste of notes: fixed a crash on paste.
- Notes: clearing a note removes the note icon from the table.
- The bill-of-materials list now sorts the task ID numerically instead of alphanumerically; the bill-of-materials view no longer opens empty (stale persisted page size), and the assignment grids are capped at 500 rows.
- Fixed a **desktop client startup crash** (clipboard status bar).
- Projects **without tasks** now show their menus and an empty detail area instead of a stuck state; flicker of the detail view on identical live updates is fixed.
- The **conflicts/warnings pane** and the **WPF menu** follow dark mode; various layout fixes in the project list (headroom for the scrollbar, context menu in the merged Status column, grid stays within the window width).

**Collaboration**
- The notes and discussion panes were reworked with the consistent design system: readable message bubbles, an always-active Send button, no flash-of-unstyled-content on open, and no more spurious scrollbar.

**Administration portal**
- Bulk revision of all active projects from the portal; the mandant.ini import ships production defaults and derives the ERP root directory.

**Installation**
- Numerous robustness improvements to the client installer (on-demand download, prefilling of target directory and tenant number, correct handling of UNC paths and placeholders).

## Changed / Removed

- The **"Type curve"** field in the **"Assign resource"** and **"Change target value"** dialogs has been removed. It is no longer needed in the new web workflow; a task's stored type-curve value is preserved and continues to be processed.
