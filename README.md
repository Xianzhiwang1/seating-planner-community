# Seating Planner — Community

Public home for **issue reports, bug fixes, and feature requests** for
**Seating Planner** (the Classroom Seating Planner) — a React + TypeScript +
Firebase web app that turns a roster, a classroom layout, and a set of seating
rules into a fair, rule-aware seating chart in seconds.

## Try it live

**[Open the Seating Planner app →](https://seating-planner-1a06e.firebaseapp.com/login)**

Sign in, then build a seating chart in three steps: add your **students** (CSV
upload or manual entry), define your **tables** (the classroom layout), and set
**rules** such as who must sit together, who must stay apart, and who needs to be
near the front. The app shuffles students into a chart that respects every rule,
and you can save each plan privately to revisit later.

---

> **Note on the source code.** The main application source lives in a **private**
> repository. This community repo is a public tracker and showcase: it hosts
> issues, selected documentation, and illustrative code snippets. It is **not** a
> complete, runnable copy of the app.

---

## What this repo is for

- **Report bugs** you hit while using the app.
- **Request features** or suggest improvements.
- **Ask questions** about how the app behaves.
- **Read showcase docs** and code snippets that explain how key features work.

Found a problem or have an idea? Open an issue from the [Issues](../../issues)
tab and pick the matching template.

---

## What the app does

- Define **students** (CSV upload or manual entry), **tables**, and **rules**,
  then generate a seating arrangement that honours every constraint.
- Support **must-sit-together**, **cannot-sit-together**, and **near-instruction**
  rules during a Fisher–Yates shuffle with a 3-second time budget.
- Persist each chart to Firestore as a saved plan, private to the signed-in
  teacher.
- Gate all access behind Firebase Auth, with strict Firestore rules, Firebase
  App Check, Zod-validated payloads, and security headers.

| Layer | Choice |
| --- | --- |
| UI | React 19, plain CSS (scoped per component) |
| Language | TypeScript 5.9 |
| Bundler / dev server | Vite 7 |
| Backend | Firebase Auth, Firestore, App Check (reCAPTCHA v3) |
| Validation | Zod |

---

## Privacy and student data — please read before filing an issue

Seating Planner is built for educators, who may enter student-related
information. We take a data-minimization approach, and we ask you to do the same
when interacting with this public repository.

- **Minimize what you enter into the app.** We strongly recommend using student
  initials (for example, "J.S.") or your own numbering system (for example,
  "Student 1", "Student 2") rather than full student names. If you label
  students this way before entering them, actual names are never written to the
  database — this is the safest option.
- **Never enter sensitive personal information** into the app: dates of birth,
  home addresses, official student ID numbers, or medical or disability
  information.
- **Never post real student data or personal information in this public repo.**
  Issues, comments, screenshots, and logs are publicly visible. Redact names,
  emails, tokens, and credentials before sharing anything.
- **You are responsible for your data.** As the user (educator or
  administrator), you are solely responsible for ensuring your handling of
  student data complies with FERPA and any other applicable laws, and for
  keeping that data safe.
- **How the app uses your data.** The app stores your saved plans only so you can
  retrieve them when you sign in. It does not sell, rent, share, analyze, or use
  your data for advertising, marketing, or profiling. The full terms are in the
  in-app Terms of Use and Privacy Policy.

The application is provided "as is" and "as available," without warranty of any
kind. No system is completely secure, and you use the app and store data at your
own risk.

---

## Showcase

These are illustrative excerpts cherry-picked from the app's documentation to
demonstrate functionality. They are simplified for clarity and may differ from
the current private source.

- [Seating generation algorithm](docs/seating-algorithm.md) — how the rule-aware
  shuffle places students under a time budget.

---

## Useful links

- **Open an issue:** [Issues tab](../../issues)
- **Report a security concern:** see [`SECURITY.md`](SECURITY.md) — please report
  privately rather than opening a public issue.
- **Contributing and ground rules:** see [`CONTRIBUTING.md`](CONTRIBUTING.md).

---

## License

The documentation and code snippets in **this** repository are released under the
[MIT License](LICENSE). This license applies only to the contents of this public
repository, **not** to the private Seating Planner application as a whole.

When reusing a snippet that references third-party code, keep its original
attribution and license intact.
