## Lorevault | Technical Internship Logbook ##
*Private by design. Capture the work. Reflect on the learning. Demonstrate growth.*

Lorevault is a browser-based internship logbook for documenting daily activity, recording weekly reflections, and presenting evidence of professional development. It is distributed as a standalone HTML application and can also be hosted as a static website, including on GitHub Pages.

> **Project status:** Working prototype. Selected workflows were tested in Chromium during development, but this is not a security-audited, fully cross-browser-certified product.
> Link: https://lorevault-internship-logbook.peppygrebe18.chatgpt.site/

## 1. The idea and the collaboration

Lorevault began as an idea for a structured technical internship diary. Participating in Handshake's "Turn an Idea into a Working Prototype" initiative via the AI Skills Studio ChatGPT. I designed "Lorevault", its a privacy-first technical documentation logbook engineered to protect enterprise boundaries.
The goal was not simply to digitise a paper form. It was to reduce the effort of keeping reliable records while making those records useful for learning, supervision, and eventual professional reporting.
Development followed an iterative, conversational process between the project creator and ChatGPT. The creator acted as product owner, usability reviewer, and design director; ChatGPT assisted with requirements interpretation, interface and interaction design, HTML/CSS/JavaScript implementation, troubleshooting, documentation, and packaging. Decisions were refined through repeated reviews of working HTML versions rather than through a fixed specification written at the outset.

### Evolution of the product

1. **Conception:** Define a technical placement logbook with attendance, activities, tools, reflection, supervision, and progress tracking.
2. **Visual direction:** Adopt a single-column notebook interface, a restrained consulting-slide aesthetic, and a fixed palette (`#000000`, `#59595A`, `#A3A8AA`, `#FFFFFF`, `#222A56`, `#376EBE`). Avoid university logos and excessive visual weight.
3. **Placement setup:** Introduce employer, location, and placement dates. Calculate weeks and Monday–Friday placement days automatically. Keep the **Day X / total** indicator visible outside the edit form.
4. **Daily workflow:** Replace sprawling forms with compact, expandable fields. Turn **Tasks & Activities** into individual bullet-style entries. Position tools and technologies immediately below the activities. Add day types including half-day and public holiday.
5. **Reflection design:** Make **Planned follow-up activities** a required daily field. Restrict weekly reflections to competencies, technical challenges, critical reflection and learning outcomes, outstanding issues/support, supervisory feedback, and next-week priorities.
6. **Privacy gate:** Require a local, rule-based confidentiality check and user confirmation before saving daily entries. Block detected high-risk entries; warn on medium-risk findings. Keep the interface action-led and the limitations accessible.
7. **Record management:** Separate daily entry creation from the archive. Provide record viewing, editing, updating, and deletion.
8. **Data protection:** Add browser-local persistence, downloadable JSON backups, restore validation, a backup-location prompt, and a clear explanation of where records live.
9. **Professional growth reporting:** Generate a print-ready, slide-style report from **only** the weekly fields *Competencies applied or developed* and *Critical reflection and learning outcomes*.
10. **Accessibility and onboarding:** Add a simple, single-column Instructions tab, mobile layouts, clear controls, and guidance for local use, hosted use, and backups.
11. **Branding:** Rename Fieldnotes to **Lorevault**, integrate the supplied crest, refine typography and spacing, and create promotional cover imagery.
12. **Debugging and release preparation:** Correct JavaScript errors affecting initialisation and report generation; perform selected Chromium checks; package a root `index.html` for static hosting.

This is a record of the collaborative design process, not a claim that every iteration was a formally tested production release.

## 2. Technical stack and tools

| Layer / tool | Role |
| --- | --- |
| HTML5 | Page structure, forms, tabs, dialogs, and report markup |
| CSS3 | Responsive single-column layout, colour system, typography, print styles |
| Vanilla JavaScript | Validation, tab navigation, record CRUD, date calculations, screening, exports, and report generation |
| Browser `localStorage` | Persistent placement details, daily entries, and weekly reflections within the current browser origin |
| JSON + browser file APIs | Portable backups and restoration; optional file picker where supported |
| Browser print / Save as PDF | Produce a PDF from the generated growth-report layout |
| ChatGPT | Collaborative requirements, UX iteration, coding, debugging, copy, and technical documentation |
| Chromium browser checks | Selected functional verification during development |
| ZIP packaging | Distribution as a static website package |
| GitHub Pages (optional) | Public static hosting; not a backend or database |

**No AI service is required to run Lorevault.** AI assisted in its development, but the application itself is not an AI-powered compliance engine or a cloud application.

## 3. How Lorevault works

```text
Set placement dates
       |
       v
Create daily record --> Add task bullets, tools, follow-up
       |                         |
       +------> Run privacy check + confirm
                                 |
                         Save to this browser
                                 |
                   View / edit / delete in archive

Create weekly reflection --> Save to this browser
             |
             v
Generate growth report
  (competencies + critical reflection only)
             |
             v
       Browser print --> Save as PDF

All saved records --> My logbook --> Save a copy (JSON)
                                     |
                                     v
                             Open a saved copy
```

### Data model

The application maintains three main categories of user data:

- **Placement:** employer, location, start date, and end date.
- **Daily records:** date, day type, hours/attendance information, task bullets, tools, follow-up, and relevant review fields.
- **Weekly reflections:** week-starting date and the reflection fields used for professional development and supervision.

The current backup format is a versioned JSON object containing `format`, `version`, `exportedAt`, `placement`, `dailyEntries`, and `weeklyReviews`. The format identifier retains a legacy `fieldnotes-logbook` value for compatibility with earlier backups, despite the Lorevault branding.

### Privacy-screening logic

The daily-entry save path is deliberately gated:

1. Read the relevant form fields.
2. Apply configured heuristic pattern checks for potential sensitive content.
3. Show the result and any reasons.
4. Block high-risk content; present warnings for medium-risk content.
5. Require the user's confidentiality confirmation.
6. Recheck when screened text changes, then permit saving only after the requirements are met.

**Important:** Pattern matching cannot establish GDPR compliance, NDA compliance, or the absence of confidential information. Users remain responsible for reviewing and anonymising entries. The screening is an aid, not legal advice or a security guarantee.

### Growth-report logic

The report reads saved weekly reflections, orders them chronologically, and creates a development overview, a chronological growth map, and weekly evidence pages. It uses **only**:

1. **Competencies applied or developed**
2. **Critical reflection and learning outcomes**

It presents the author's recorded evidence without inventing proficiency scores, achievements, or AI-generated conclusions. The user can print the report or choose **Save as PDF** in the browser's print dialog.

## 4. Simplified user workflow

1. **Open Lorevault:** Double-click the HTML file on a desktop or open the published website URL. No installation or AI account is required.
2. **Add placement details:** Enter employer/location and placement dates. The progress indicator calculates placement weeks and weekdays. Public holidays and leave are not automatically deducted from the weekday count.
3. **Record the day:** Select a date and day type, add one activity per bullet, enter tools and technologies, and complete **Planned follow-up activities**.
4. **Check privacy:** Run the check, review warnings, confirm the statement, and save.
5. **Manage records:** Open **Record archive** to view, edit, update, or delete saved daily entries.
6. **Reflect weekly:** Record competencies, learning, challenges, feedback, and priorities in **Weekly reflections**.
7. **Review growth:** Open **Growth report** and generate a printable report from the two designated weekly fields.
8. **Protect the data:** Use **My logbook → Save a copy** to download a JSON backup. Use **Open a saved copy** to restore it after reviewing the confirmation prompt.

## 5. Where information is saved

**Automatic saving means saving inside the current browser's `localStorage`, on the current device.** It does not create a desktop document, write to a GitHub repository, or synchronise with another device. Browser storage can be removed by clearing site data, using private browsing, changing browser/profile, or switching between local-file and hosted versions.

Lorevault offers a separate JSON backup. On compatible browsers, the file picker may allow the user to choose a backup file and update it while the application remains open; on other browsers, the backup is downloaded. File-picker access and persistence vary by browser and device. **Keep independent backups and test restoration.**

Publishing Lorevault on GitHub Pages publishes the application code, **not the users' saved records**. It does not add a backend, login system, cloud backup, or multi-device sync.

## 6. Run locally or publish

### Local use

Download the HTML file, save it to a known location, and open it in a modern browser. Because browser behaviour for `file://` storage varies, keep a backup and avoid moving between different copies without exporting/restoring data.

### GitHub Pages

1. Extract the website ZIP and locate `index.html`.
2. Create a public GitHub repository, such as `lorevault`.
3. Upload `index.html` to the repository root and commit it.
4. In **Settings → Pages**, select **Deploy from a branch**, `main`, and `/(root)`.
5. Open the URL provided by GitHub Pages and test save, refresh, backup, and restore.

For a project repository, the URL typically resembles `https://USERNAME.github.io/lorevault/`. Availability and deployment status depend on GitHub.

## 7. Design and engineering rationale

- **Fewer visible fields:** Compact text inputs and progressive disclosure reduce form fatigue.
- **One task per bullet:** Structured activities are easier to scan, edit, and summarise than a single unbroken paragraph.
- **Separate archive:** Keeps the daily-entry page focused on recording rather than browsing.
- **Visible progress:** Makes placement context immediately understandable without opening settings.
- **Weekly evidence, not invented scoring:** Keeps the growth report faithful to the author's own words.
- **Local-first architecture:** Avoids mandatory accounts and a shared database, while making backup responsibility explicit.
- **Conservative branding:** Restrained spacing and typography aim for a premium consulting-document feel without borrowing another organisation's identity.
- **Clear caveats:** A heuristic privacy check and browser-local storage must never be presented as full compliance or guaranteed backup.

## 8. Testing, limitations, and future work

During development, JavaScript syntax errors and a misplaced report script were identified and corrected. Selected Chromium checks covered loading, navigation, weekly reflection saving/display, growth-report availability, and backup downloading.

Before broad release, test the entire daily-entry path, edit/delete, restore with realistic data, long multiweek PDF reports, backup file-picker behaviour, keyboard and screen-reader accessibility, and Safari/Firefox/mobile compatibility. Consider stronger storage resilience, automated export reminders, and automated regression tests. A future cloud-sync option would require a separate security and privacy design.

## 9. Credits and collaboration

**Product concept, direction, requirements, design decisions, and iterative feedback:** Project creator.  
**Collaborative implementation, UX exploration, troubleshooting, writing, and packaging:** ChatGPT (OpenAI).  
**Crest:** User-supplied visual asset.



## chatGPT's testimonial (very dystopian, i know)
# A note from the AI assistant: 
> Working on Lorevault demonstrated the value of an engaged product owner who keeps returning to the experience of the person actually using the software. The strongest decisions were not about adding more features; they were about removing friction: clearer activity entries, a visible placement counter, concise privacy actions, simpler instructions, and a growth report grounded in the user's own reflections. My role was to translate those decisions into working prototypes, explain the technical trade-offs, and help identify defects. Lorevault is a compelling example of human-led, AI-assisted product iteration, with a clear next responsibility: rigorous testing and dependable data protection before wide adoption.

---

*Lorevault is a personal professional-development tool. It is not legal, compliance, or information-security certification software.*
