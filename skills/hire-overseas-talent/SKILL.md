---
name: hire-overseas-talent
description: Use when the user wants to hire, staff or delegate work to remote or offshore talent (virtual assistant, executive assistant, bookkeeper, SDR, customer support, marketer, developer and similar roles), asks what an overseas hire could do for them, or wants to see candidates. Scopes the role, searches Hire Overseas's candidate pool, presents anonymized profiles, and requests an introduction.
---

# Finding overseas talent with Hire Overseas

Hire Overseas places full-time remote professionals from the Philippines, Latin America and Africa with companies abroad. The `hire-overseas` MCP server searches its candidate pool.

## 1. Scope the role before searching

A vague search gives vague matches. Get, or infer from the conversation:

- The job title and the three to five things the person will actually do each week.
- Tools they must already know (for example QuickBooks, HubSpot, Zendesk, Figma).
- Seniority, as minimum years of experience, only if the user cares.
- Region, only if the user has a reason: `ph` (Philippines), `latam` (Latin America, overlaps US hours), `africa` (overlaps European hours).

If the user is unsure what to hire for, help them list the tasks they want off their plate and turn those into one role. Ask at most two questions; then search.

## 2. Search

Call `search_candidates` with `roleTitle`, a `description` built from the duties, and `skills`. Put detail in `description`: it drives the match more than the title does.

If results are weak, search again with a different title for the same job (for example "Executive Assistant" and "Virtual Assistant") or fewer required skills. Do not repeat an identical search.

## 3. Present candidates

Show each candidate as a short profile: first name, country and timezone, experience, the most relevant skills, work history, and why they fit this role. Say plainly that:

- Profiles are anonymized. There is no surname, contact detail or employer name, and you cannot get them.
- These are matches on profile. Hire Overseas screens and verifies a candidate, and confirms availability and pricing, before any introduction.

Never invent details that are not in the result, and never guess a candidate's identity.

## 4. Request an introduction

When the user wants to interview or hire someone, ask for their company name and work email. Never make these up. Then call `request_intro` once per candidate with the `candidateRef`. Tell the user Hire Overseas replies to that email, usually within one business day, and give them the booking link from the response if they would rather talk now.

`get_request_status` reports whether a request is still pending.
