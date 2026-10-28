# Changelog 2026-10-28: Lab 1 refresh (Lab Builder v2)

Branch: `Lab-Builder`. Scope: `Instructions/Labs/LAB-01.md` and its screenshots only. ARM templates, automation scripts and the other labs are unchanged.

## How it was tested

A full live walkthrough of Lab 1 on a CloudLabs instance (ODL lab user, Temporary Access Pass sign-in) in Chrome, at a 1272 x 621 CSS viewport and 1.5x device scale. Every step was done in the real product. Every screenshot was captured live, then annotated in the house style with `Annotate-Screenshot.ps1 -Strict` (red boxes, numbered badges, 2 px border, tenant names and user domains blurred).

## Content changes in LAB-01.md

| Area | Old guide | Current product (fixed) |
|---|---|---|
| Sign-in | "Sign into Microsoft Azure", Password | Microsoft **Sign in** page, then **Enter Temporary Access Pass**; the step now labels the value Temporary Access Pass |
| New environment pane | Region "United States - Default", Dataverse toggle visible at once | **Macro Region Geography** = North America; Dataverse toggle is under **Change default settings**, and Save turns into **Next** |
| Add Dataverse | Security group select and Save | Same flow, re-captured; added a Note for the "A self-service signup plan is required" error |
| Environment settings | Step had no screenshot | Added the More actions menu and the Settings page screenshots |
| Power Apps first run | Not mentioned | Added the **Welcome to Power Apps** dialog step (Get started) |
| Environment switch | Only a Note: "make sure you are in Copilot" | Explicit step: Environment picker, then select Copilot (Power Apps opens in the default environment) |
| Table generation | Said "three tables" and listed four | Four tables (Showing, Client, Agent, Property); Table options, One table, Apply |
| Copilot prompts | "add a column to track client full name" and similar | Copilot now rejects prompts without a table name ("Please reenter the query and ensure the relevant table names are also specified."), so every prompt now names the RealEstateShowing table |
| Status column | "add an option for Completed to the Status column" | The generated table has no Status column; the prompt now creates a Status choice column with Scheduled, Completed and Canceled |
| Sample rows | "add 5 more rows of data in all the three tables" | "add 5 more rows of data to the RealEstateShowing table" (one table) |
| ID column | "track ID of the RealEstateShowing table" | Prompt reworded; Note that Copilot names it (for example Showing Reference ID) |
| Save and open app | "Select Save and open app twice" | Two explicit steps: toolbar button, then the **Done working?** dialog |
| Gallery edits | Flat tree (RecordsGallery1 > Title1) | Tree is now nested in containers (ScreenContainer1 > BodyContainer1 > SidebarContainer1 > RecordsGallery1); path documented |
| Body1 formula | `ThisItem.'Status'` | Fails: the name clashes with the Dataverse system Status column. Now `Text(ThisItem.'Status (crxxx_status)')` picked from IntelliSense, with an explanation Note |
| Form edits | "ID tracking" field | Field is the ID column Copilot created; Form1 location, the Properties pane and Edit fields steps updated |
| Test record | "Agent Email: < Your name >", "Excel file in Module 1 / Real Estate Properties table" (neither exists) | Fictional sample values for every field; removed the wrong reference |
| Save and exit | Save, "exit the app" | Save as dialog (name), Back, then **Leave the app?** Leave, Cancel on Start with data, verify on the Apps page |
| Style | En dashes, mixed task heading styles, legacy inject tags, "screenshot of the prompt" alt text | No en or em dashes, consistent `### Task N:` headings, self-closing inject tags with enableCopy, descriptive alt text, `**(N)**` markers matched to badges |

## Screenshots

- 46 new screenshots named `L1T{task}S{step}.png` (the repo's existing `L3T1S3` scheme) in `Instructions/Media/`. Source: live capture for all of them.
- 35 old Lab 1 images removed: none was referenced by any other page (checked with grep across all `.md` files). The removed names include the three files with parentheses that broke the image links (`copilot-(1).png`, `table-options(1).png`, `power-apps(3).png`).

## Lint (lint-lab.ps1, profile copilot-saas), LAB-01.md only

| | Before | After |
|---|---|---|
| Blockers | 4 (3 broken image links, plus one in Getting-Started-01) | 0 |
| Warnings | 7 | 1 (ValidationCoverage) |
| Hygiene | 9 | 0 |

## Found but not fixed (out of scope or needs a decision)

1. **Lab tenant licenses**: the first instance had 0 licenses, so environment creation failed with "A self-service signup plan is required". It was fixed during testing by adding licenses. Make sure the CloudLabs template assigns a Power Apps license (or equivalent) to every lab user.
2. **masterdoc.json** loads the guides from `CloudlabsAI-Git/Power-platform-Copilot/main`. These changes reach learners only after this branch is merged into that repository.
3. **ValidationCoverage**: Lab 1 has no validation steps. Adding them needs validation scripts, which were out of scope.
4. **Getting-Started-01.md** has a broken image (not in masterdoc.json, so not shown to learners). `Instructions/Media/response-summary.png` is an orphan from before this change.
5. LAB-02 to LAB-05 were not tested in this pass.
6. The skill's "fresh-agent freshness spot-check" was replaced by the end-to-end live walkthrough, which exercised every step in the current product.
