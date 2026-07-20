# From Mid-Build to Launch-Ready: Taking Over Someone Else's Development

**Every project plan assumes one app and a clean start. This engagement had neither: a native app already built by an outside team, a second app the founder generated himself, a technical lead who predates me, and a deadline already on the calendar.**

> **Note:** This is a case-study repo documenting the development-management half of a client engagement. The companion write-up, [From Prototype to Pilot](../sip-cs), covers the pilot program this build feeds. No code, no client data, and no patient information appear here or in any linked material, at any stage. The client platform, its partner clubs and practices, and all people are unnamed.

---

## At a glance

| | |
|---|---|
| **Role** | Technical Project Manager, client engagement, joined mid-build |
| **Scope** | Development management across two separate app projects: feature specs, QA, and vendor coordination on an inherited native build; the audit and recommendation that decided which app carried the pilot; then backlog, QA design and execution, and release gating on the chosen build through pre-launch QA passed on iOS and Android |
| **Team** | Physician founder (product vision, partner relationships, author of the second app), outside development team (first app), technical lead (implementation, integrations, legal finalization), me (the layer that turns the rest into a shipped app) |
| **Working style** | AI-native: specs, QA design, prototyping, and systems design with Claude as the primary build engine |
| **Status** | Launch phase against a 20-gate checklist; hard deadline at a 75-team tournament |

---

## The starting state

Inheriting a build is a different discipline than starting one. Inheriting two is a different discipline again.

When I engaged, the platform was one app: a downloaded native app built by an outside development team, feature-complete in the ways that demo well, dated in the ways users notice, and already serving early pilots. My layer on this first build was specs, QA, and coordination with a team whose codebase I would never touch.

Then the founder produced a second app himself, generated on an AI app platform: QR-accessed, no login, no download, built for the sixty-second first experience the first app could not deliver. This was not a version bump. It was a separate project with its own codebase, its own gaps, and its own author in the room. The first app's development had happened entirely before the second app existed.

A committed club pilot with a fixed date forced the question neither project had answered: which app ships? What existed at that point: two working builds and warm relationships with the partner club and practice. What did not: a deployed pilot, a decision on form factor, a repeatable onboarding process, a validated referral pathway, or a funnel that could distinguish real users from internal testing. The job was not to build an app. Two apps mostly existed. The job was to decide which one a coach at a 75-team tournament could depend on, close the distance from "mostly exists" to "dependable," and manage that closure through other people's hands.

## My role

Development management across two codebases with different authors: writing the specs and acceptance criteria the outside team built against, designing and running QA on both apps, delivering the audit and recommendation that decided which app carried the pilot, then converting the chosen build's remaining work into a gated backlog and gating releases through pre-launch QA. The founder owns vision and partner relationships; the technical lead owns implementation and legal finalization. My layer is everything that makes the other layers converge on a launch date that cannot move.

## Key decisions

**Specifying for a codebase I would never touch.** The first app's biggest remaining feature was a guided chat experience with real clinical stakes, built by an outside team on their own platform. On a vendor build, the spec is the management surface, so mine carried the guardrails as enforceable rules rather than intentions: chat can never create an injury record, the bot can never issue return-to-play clearance, escalation is always user-initiated, each rule pinned to the application layer where the backend verifies it. The same document carried feature flags for staged rollout, a complete analytics event taxonomy, and a QA plan of forty scripted scenarios, so the definition of done shipped inside the definition of the feature.

*The call: on an outside team's build, the spec is the management interface; write the guardrails, the flags, and the tests into it.*

**The version decision.** When the pilot forced a choice between builds, both went under the same instrument: a role-based audit as admin, coach, and parent on each app, compiled into a comparison and a recommendation. The audit also named the tension the meetings were talking around: the app the founder preferred, frictionless and login-free, was not yet the app that could do what the flagship prospect had asked for, roster-level athlete records. And it drew the compliance line the choice implied: frictionless activation now, accounts later, because the moment the system stores identified health information the hosting and consent model must change with it. The pilot went forward on the founder's app, with the roster capability designed into it properly instead of kept alive in the older build.

*The call: when two apps compete for one pilot, audit both with the same instrument and put the tradeoff in writing.*

**Auditing the inheritance before planning the finish.** With the app chosen, you cannot sequence work you have not verified, so the first pass treated every "done" in the project's own records as a claim to check against the running system, not a fact. The audit's defining find: the referral funnel showed zero conversions, which everyone read as a demand problem, and the actual cause was an email integration that could not deliver externally, configured with a placeholder address. Not one notification had ever arrived. That single finding reset the backlog, because the most important remaining work was not a feature, it was a rebuilt notification layer.

*The call: an inherited project's documentation is a list of claims; the audit is what converts claims into a backlog.*

**Managing the build without owning the code.** Both codebases have authors who are still in the room: an outside team on the first app, and on the second the founder himself plus a technical lead who predates me on the engagement. The fastest way to stall an inherited build is to arrive re-litigating its architecture, so the working interface is deliberately narrow: specs and acceptance criteria go in, verified builds come out, and review happens against behavior, not implementation style. My additions live where the code meets the world: what a coach sees, what a parent receives, what the data can prove. The authors kept full ownership of how; I took ownership of whether it is actually done.

*The call: the fastest way to finish someone else's build is to add verification, not opinions.*

**A backlog of gates, not features.** With a tournament date that cannot move, the plan runs backward from launch as twenty explicit gates, each one a condition the project passes rather than a feature it contains, with an owner and a verification step. Every phase closes in a working end-to-end state, so a slipped item costs a gate, never the launch. The same shape became the club onboarding template: nine gated stages with this deployment as its worked example, which is what makes the next club a fill-in exercise instead of a second project.

*The call: with a fixed deadline, the unit of planning is a gate the project passes, not a feature it contains.*

**QA as the instrument of management.** On code you did not write, QA is not the last step, it is how you learn the truth of the system, and it ran across both projects. On the first app, a device audit across iOS and Android came back with zero defects and one workflow flag, which converted an open question into a demo-ready verdict. On the chosen build, the QA program ran role-based passes across iOS and Android, including the share flow the pilot's first stage depends on; a scripted champion walkthrough run cold and timed, so the acceptance test doubles as a usability test; and a pre-launch red team from four perspectives (coach, parent, lawyer, saboteur) that surfaced ten unconsidered failure modes, now mitigated, from reply routing on the SMS channel to a redirect layer that keeps fifty printed QR codes from dying with one URL change.

*The call: on an inherited codebase, QA is how the new manager learns what is actually true.*

**Prototyping to resolve what meetings could not.** A stakeholder conflict over roster access had stalled a core flow: the club champion wanted roster-based entry, the founder proposed anonymized sharing. Instead of arbitrating, I built the synthesis as a sandboxed proof of concept, a four-table Postgres schema in Supabase with row-level security scoping every query to team and role, and a live demo where switching test users changes the roster. The conflict dissolved, the prototype converted into the build spec at zero political cost, and the displaced anonymized flow became guest mode for visiting tournament teams. It also closed the capability gap from the version decision: the roster-level records that had kept the older build in contention now belong to the app that shipped.

*The call: a working prototype is the cheapest alignment document a project manager can produce.*

**Designing around the platform's edges.** The chosen app's application layer is AI-assisted generation (Base44), which is exactly where such platforms are strong. Every point where the system touches the outside world got deliberate design instead: parent and staff notification rebuilt on Twilio SMS with deep links into a referral work queue, print-to-digital on a QR redirect layer under a client-controlled domain, CRM and lifecycle stitched from HubSpot Starter plus MailerLite plus Make for the automation the tier lacks, and rosters moving by CSV against a published spec because the club's platform has no API. Knowing where generated code ends and deliberate systems design begins is the operating skill of an AI-native build.

*The call: AI-assisted generation ends where the outside world begins, and that boundary is where the project management lives.*

## Where it stands

- Pre-launch QA passed across roles on iOS and Android, including the share flow the pilot's first stage depends on
- SMS layer live: athlete confirmation texts active, staff alerts deep-linking into the referral work queue
- Launch phase running against the 20-gate checklist; hard deadline at the club's late-August tournament, roughly 75 visiting teams
- The first app remains its own project, outside this write-up past the version decision
- From here the story continues in the companion write-up: [From Prototype to Pilot](../sip-cs), the pilot program this build exists to serve

Status language on purpose. No invented metrics. Real numbers replace status language as launch data lands.

## Why this is a case study, not a live repo

This is client work on a commercial platform. The code belongs to the engagement: the first app to its development team, the second to the founder and technical lead. My role is management and systems design rather than hand-written implementation. The write-up shows the reasoning. Nothing identifying the client or its partners goes public beyond this.

---

*Shannon Baylor · [shannonbaylor.com](https://shannonbaylor.com) · [LinkedIn](https://www.linkedin.com/in/baylorshannon)*
