# OpenStage - Access Data Standard for Live Entertainment
*Working name. Placeholder only: "open access" already means free scholarly publishing, so the name will change before any launch.*

**Version:** 0.1 (draft for discussion)
**Status:** A proposal, not a standard. Shared to find collaborators and a steward.
**Scope:** Theatre and live entertainment, UK.
**Licence (intended):** Specification under Apache 2.0. To confirm with a steward.

---

## 1. The problem

Access information for UK live entertainment is spread across many places, held in different formats, and often out of date or unverified. Very little of it is machine-readable.

To plan one trip, a disabled audience member or their companion usually has to pull together a venue page, an operator's access scheme, a PDF brochure, a third-party listing, a transport planner, and often a phone call to the box office, because access seats frequently can't be booked online. The same fact, such as whether an auditorium has a Changing Places toilet or that a show is captioned on 14 March, is recorded in different words, in different places, to different standards, and checked at unknown times.

The result is trips that are hard to plan and easy to get wrong. People are excluded less because the access isn't there, and more because the information about it can't be found, compared, or trusted.

Parts of a solution exist: operator access pages, listings sites, surveyed venue guides, and consumer sites such as Theatre Access NYC in the US. What is missing is a shared, open format that venues publish to once and that any service can read. That is what this addresses.

## 2. Why a standard, not another website

A website is one output. A standard is shared plumbing that many outputs can use.

If venues publish access data once, in an agreed structure, the same feed can drive their own websites, their ticketing, third-party listings, journey planners, and assistive tools, without each one re-typing or re-interpreting it. Public transport did this with GTFS. UK sport and physical activity did it with OpenActive, an ODI, Sport England-backed standard for what, where, and when sessions happen. Both kept a neutral steward and a small required core.

For a large operator, holding access information in one model is cheaper to maintain than keeping it consistent by hand across dozens of venue pages and channels.

## 3. Scope (v0.1)

In scope:
- Sector: live entertainment, meaning theatre, musicals, opera, dance, comedy, and live music in venues. Theatre is the first worked example.
- Geography: UK.
- Subject: venue access (physical access, facilities, getting there); production access and content (the sensory and content profile of a show); performance access (which access services run on which date, and how to book them).

Out of scope for v0.1, though the core is built to extend later:
- Cinema, sport, and broadcast (possibly later).
- Booking and payment (the standard points to how to book; it does not handle the transaction).
- Personal data.
- Accreditation rules.

## 4. Who it is for

- Audiences and companions with access requirements, involved as co-designers.
- Publishers: venues, operators, and producers.
- Consumers: listings sites, aggregators, ticketing platforms, journey planners, assistive apps, and publishers' own websites.
- A steward: a neutral body that manages change and versions.
- Disabled-led organisations and access-service providers, for vocabulary review and quality.

## 5. Type of standard

Using the ODI's three types, v0.1 is mainly two things:
1. A shared vocabulary and model: common entities, definitions, and controlled lists.
2. A light exchange format: a JSON-LD / JSON Schema serialisation so the data can be published and read consistently.

Validation comes later, once the model has settled.

## 6. Existing standards to build on

- schema.org accessibility terms (`accessibilityFeature`, `accessibilityHazard`, `accessMode`): reuse where they overlap, so the data also works for search engines and assistive tech. They were written mainly for digital content, so they cover only part of a physical venue and a live show.
- GTFS / GTFS-Pathways: for getting there (step-free routes, station access). Reference it rather than copy it.
- OpenActive: the closest UK model, and a likely neighbour.
- IATA special-assistance codes (WCHR, BLND, DEAF, and so on): a precedent for small, agreed vocabularies used across a whole industry.
- AccessAble: an established method for surveying venue access. A template, and a possible data partner, for the venue tier.
- Attitude is Everything: a live-events access charter and accreditation. A possible model for the separate certification.

## 7. Core model

Three entities, split by how often the data changes. This matches how the industry already thinks: a venue hosts productions, and a production has many performances.

**Venue** (changes rarely; re-check periodically): location; step-free status (entrance, route, any steps); lifts (size, floors served); wheelchair spaces (number, location, sightlines, transfer seats); toilets, including whether there is a Changing Places toilet; hearing systems and where they actually work; quiet space; ear-defender loans; assistance-dog policy; re-entry policy; trained staff; getting there (nearest step-free station and distance, accessible drop-off, Blue Badge parking); familiarisation photos or video.

**Production** (set once per show): running time; interval and rough timing; sensory profile (strobe, flashing, blackout, loud bangs, gunfire, haze, pyrotechnics, scent, sustained loud passages); audience interaction, graded none / optional / likely / unavoidable; content warnings; age guidance; link to a visual story or sensory guide.

**Performance** (per date and time): date and time; which access services run that occurrence; whether relaxed adjustments are on (house lights up, effects reduced, staffed chill space); how to book access seats (online / phone / email, with phone-only shown as a barrier); whether a companion scheme applies.

**Shared vocabularies:** AccessService, SensoryHazard, AccessFacility, BookingMethod, plus provenance and confidence.

Rules for every field:
- Three states, not a plain yes/no: yes, no, or unknown. "No data" must not read as "confirmed none".
- Measurements, not adjectives: "door to seat: 45 m, level", not "short walk".
- Provenance on every record: who verified it, and when.
- Use a controlled list wherever a value can be one.
- Plain-language and easy-read versions are proper fields, not extras.

## 8. Live-entertainment profile (v0.1)

The profile sets concrete values for this sector.

**AccessService:** relaxed_performance, sensory_adapted, captioned_open, captioned_app, bsl_interpreted, audio_described, touch_tour, dementia_friendly, assisted_other.

> relaxed_performance and sensory_adapted are kept separate on purpose. Provision framed for children does not fit adults with sensory needs, and the vocabulary should let an adult sensory-adapted offer be described without that implication.

**SensoryHazard:** strobe, flashing, blackout, loud_bang, gunfire, haze_smoke, pyrotechnics, scent, sustained_loud, low_frequency.

**AccessFacility:** step_free, lift, wheelchair_space, transfer_seat, accessible_toilet, changing_places, hearing_loop, infrared_system, quiet_space, ear_defenders, assistance_dog_welcome, accessible_parking.

Opera, dance, comedy, and live music use the same profile. Genre-specific values are added as the community finds them.

## 9. Minimum data, and the badge (kept separate)

The required core is small, around 15 to 20 fields, so publishing is realistic. Everything else is optional.

Two separate things:
- Data: a "Verified Access Data" mark rewards complete, recently checked data, whatever the building is like. A listed theatre that cannot be made step-free can still earn it by being clear about what it has. This removes the reason not to take part.
- Provision (later, optional): a tiered rating of the access actually offered, based on existing live-events accreditation. Kept apart from the data, so honesty is always worth it.

## 10. Governance, licensing, and change (outline)

- Work in the open: public repo, versioned drafts, decisions visible.
- Steward: a neutral body owns change and versioning. The standard should not be owned long-term by one person or one company.
- Versioning: semantic versioning, with a written change process.
- Licensing: specification under Apache 2.0.
- Co-design: disabled-led organisations help shape the vocabulary and quality from v0.1, not afterwards.

## 11. Proof of concept and next steps

1. Light discovery: test the problem and the field priorities with 5 to 10 people across audiences, venues, and consumers.
2. Reference feed: venue partners publish real sample data to the v0.1 model.
3. One JSON-LD example and a draft data dictionary (Appendix A is a start).
4. Find a steward and a funder.
5. Publish v0.1 in the open and ask for comment.

What early partners are asked for: publish one sample feed, and review the vocabulary. Not adopt a finished standard.

---

## Appendix A — Example (JSON-LD, illustrative only)

```json
{
  "@context": {
    "schema": "https://schema.org/",
    "os": "https://openstage.example/ns/v0.1#"
  },
  "@type": "schema:TheaterEvent",
  "os:production": {
    "name": "Example Production",
    "schema:duration": "PT2H40M",
    "os:interval": { "present": true, "approxAfter": "PT1H20M" },
    "os:audienceInteraction": "optional",
    "os:sensoryProfile": ["strobe", "loud_bang", "haze_smoke"],
    "os:contentWarnings": ["depiction_of_violence"],
    "os:visualStory": "https://example.org/visual-story.pdf"
  },
  "os:performance": {
    "schema:startDate": "2026-03-14T19:30:00+00:00",
    "os:accessServices": ["captioned_open"],
    "os:relaxedAdjustmentsActive": false,
    "os:booking": { "method": "phone", "contact": "+44 20 0000 0000" },
    "os:companionScheme": true
  },
  "os:venue": {
    "@type": "schema:PerformingArtsTheater",
    "name": "Example Theatre",
    "os:stepFree": { "status": "partial", "entrance": "side", "verifiedDate": "2026-01-20" },
    "os:facilities": ["wheelchair_space", "accessible_toilet", "infrared_system"],
    "os:changingPlaces": "no",
    "os:nearestStepFreeStation": { "name": "Example Station", "distanceMetres": 320 },
    "os:provenance": { "verifiedBy": "venue_access_team", "verifiedDate": "2026-01-20" }
  }
}
```

## Appendix B — Open questions

- Where is the line between referencing transport data (GTFS) and restating it?
- Should the provision/accreditation rating live with this standard, or with an existing accreditation body?
- What is the minimum re-check cadence for the "Verified Access Data" mark?
- Which body is the natural long-term steward? SOLT?
