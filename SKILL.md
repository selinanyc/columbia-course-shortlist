---
name: Columbia course shortlist
description: >-
  Use when someone wants to find, compare, or shortlist Columbia University
  courses for a term (to take or to audit), check professor reviews, spot time
  conflicts, or draft an audit request to an instructor.
---
# Columbia course shortlist

Goal: turn the user's interests into a shortlist of Columbia courses with reviews, links, and next steps. Never log in with the user's UNI, never register or enroll anyone, and never send emails yourself (draft only).

## 0. Clarify (only what's missing)
- Term (Spring/Fall + year), interest areas, departments to include, whether they will enroll or audit, and any days/times they're busy.

## 1. Term codes and sources
- Term code = year + season digit: 1 = Spring, 2 = Summer, 3 = Fall (e.g. 20271 = Spring 2027).
- **Directory of Classes (DoC)**: works with plain curl, no login.
  - Subject index: `https://doc.sis.columbia.edu/sel/subj-{Letter}.html` (shows which terms each subject has published).
  - Department index: `https://doc.sis.columbia.edu/sel/departments.html`.
  - Subject + term listing: `https://doc.sis.columbia.edu/subj/{SUBJ}/_{Season}{Year}.html` (e.g. `/subj/JOUR/_Fall2026.html`). Gives course number, section, title, call number, points, enrollment, instructor, Vergil link.
  - Section detail: `https://doc.sis.columbia.edu/subj/{SUBJ}/{Letter}{Number}-{term}-{section}/` (e.g. `/subj/JOUR/J4001-20263-001/`): approvals required, type, in-person/online, division.
  - DoC no longer shows days, times, or rooms, and has no descriptions. If a term returns 404 it isn't published yet; say so and offer to use the previous same-season term as a preview, clearly labeled.
- **Vergil** (`https://vergil.columbia.edu/vergil/class/{term}/{call_number}`) has days/times/rooms but is behind a Cloudflare challenge for scripts. Don't try to bypass it. Either give the user the deep links, or use a browser to read each class page for days/times/room if the user wants a schedule grid.
- The official Open Data Service JSON feed requires a Columbia login; don't use it.

## 2. Reviews (CULPA, public JSON, light request rate)
- Search: `https://culpa.info/api/search/search?queryString={name or course}` returns professor (`professor_id`) and course (`course_id`) hits.
- Professor card: `/api/professor_page/card/{professor_id}` (avg_rating, num_reviews, ai_overview, quotes). Reviews: `/api/review/professor/{professor_id}`.
- Course card/reviews: `/api/course_page/card/{course_id}`, `/api/review/course/{course_id}`.
- Department lists: `/api/departments/all`, `/api/departments/{id}/courses`, `/api/departments/{id}/professors`.
- If endpoints break, re-discover them from the current `main.*.js` bundle on culpa.info. Many professional-school courses have zero reviews; say so rather than implying quality.

## 3. Build the shortlist
- Filter by the user's interests (titles, instructors, department). Prefer lectures/seminars that allow auditing.
- For each pick: course code + title, instructor, points, call number, approvals required, CULPA rating and number of reviews (or "no reviews"), one-line why it fits, Vergil link. Add days/times only if actually read from Vergil.
- Flag time conflicts against the user's calendar if days/times are known.
- Deliver as a short list for a few courses, or a table for many.

## 4. Auditing (visiting scholars and others)
- Columbia Faculty Handbook: visiting scholars may audit lecture courses with the instructor's permission and cannot register/enroll (https://facultyhandbook.columbia.edu/content/visiting-scholarsscientists). Summer courses also need the Summer Session dean's permission.
- Policies vary by school (e.g. the Journalism School lets auditors attend free by contacting the professor, no transcript record). Check the hosting school's policy page before advising; some instructors may require formal registration instead.
- Offer to draft a short, polite audit-request email per instructor (who the user is, which course, why, that they'll audit without credit); the user reviews and sends it.

## 5. Timing
- Note the school's add/drop and first-day-of-class dates from its academic calendar, and remind the user to ask instructors before the first class. If the term isn't published yet, offer to re-check DoC periodically.
