# Timezone Scheduler

> A meeting planner API for scheduling across timezones. Covers 80+ curated business hubs and 450+ IANA timezones. All times are DST-aware. Available at <https://timezones.centminmod.com>

The Timezone Scheduler helps coordinate meetings across global timezones. It classifies each participant's local time into business hours (9 AM-5 PM), extended hours (7-9 AM or 5-9 PM), or off hours (9 PM-7 AM), and can suggest optimal meeting times.

Let your AI LLM model learn how to use and setup the Timezone Scheduler as an API tool, AI Skill.md or MCP server by feeding the AI <https://timezones.centminmod.com/llms.txt>.

## Examples

**Table of Contents**

- [Timezone Scheduler API Example](#timezone-scheduler-api-example)
  - [Prompt](#prompt)
  - [Thinking](#thinking)
  - [Response](#response)
- [Comparison LLM Timezone Responses](#comparison-llm-timezone-responses)
  - [Claude AI Opus 4.6 Web](#claude-ai-opus-46-web)
  - [ChatGPT Plus - GPT-5.4 Thinking](#chatgpt-plus---gpt-54-thinking)
  - [Google Gemini AI Pro - Gemini 3.1 Pro Thinking](#google-gemini-ai-pro---gemini-31-pro-thinking)
  - [Google Gemini AI Pro - Gemini 3.1 Flash Lite](#google-gemini-ai-pro---gemini-31-flash-lite)
  - [ZAI Coding Pro - GLM-5](#zai-coding-pro---glm-5)
  - [MiniMax M2.7](#minimax-m27)
  - [Moonshot Kimini K2.5 Thinking](#moonshot-kimini-k25-thinking)
  - [Xiaomi Mimo V2 Pro](#xiaomi-mimo-v2-pro)
  - [Xiaomi Mimo V2 Flash](#xiaomi-mimo-v2-flash)
  - [Grok 4.20 Beta Thinking](#grok-420-beta-thinking)
  - [Grok 4.1 Fast Thinking](#grok-41-fast-thinking)

### Timezone Scheduler API Example

#### Prompt

> Find the most optimal meeting time that works across Brisbane (Australia), New York (USA), and London (UK), ideally falling within business hours for all three cities, or as close to business hours as possible.

#### Thinking

The suggest API returned the top 5 suggestions, all with score 6/9 (67%). The best it can do is have 2 out of 3 in business hours, with Brisbane always in "off" hours. Let me also try with a different source timezone to see if there's a better option, or let me try scheduling from different perspectives.
Actually, the API already optimized across all three. The fundamental challenge is that Brisbane (AEST, UTC+10) is far ahead of both New York (EDT, UTC-4) and London (GMT, UTC+0). That's a 14-hour gap between Brisbane and New York, which makes full business-hours overlap impossible.
Let me explore if pushing to early morning Brisbane times—around 7 AM—might qualify as extended hours instead of off-hours, though the math shows this still lands outside business windows for the other locations.

#### Response

Now I'll use the `suggest` API to find optimal meeting times across all three cities.The `suggest` API's best results put Brisbane at midnight. Let me also check early-morning Brisbane slots that might land in "extended" hours, which the suggest endpoint may have ranked lower but could be more practical.Now let me check one more option to confirm the tradeoffs: scheduling from London's morning.Here's the full analysis based on the API results.

**The core constraint:** Brisbane (UTC+10) and New York (UTC-4) are 14 hours apart. It is impossible to get all three cities into business hours (9 AM to 5 PM) simultaneously. One city will always be outside business hours.

**Viable options explored:**

| Option | Brisbane | New York | London | Tradeoff |
|---|---|---|---|---|
| **A. API's top pick** | 12:00 AM (off) | 10:00 AM (business) | 2:00 PM (business) | Brisbane sacrificed entirely |
| **B. Brisbane early AM** | 7:00 AM (extended) | 5:00 PM (extended) | 9:00 PM (off) | London sacrificed |
| **C. Brisbane evening** | 6:00 PM (extended) | 4:00 AM (off) | 8:00 AM (extended) | New York sacrificed |

**The API's recommendation (Option A)** scored highest at 67% (6/9) because it puts two out of three participants in core business hours. The other two options only achieve "extended" hours for two participants with one still in off hours.

**My recommendation: Option A** is the best overall pick, specifically **12:00 AM Brisbane / 10:00 AM New York / 2:00 PM London** on Monday March 23, 2026. It gives New York and London comfortable mid-day slots. The downside is that Brisbane is at midnight, but the alternative options only manage to push everyone into suboptimal extended/off slots rather than keeping two cities in their sweet spot.

If Brisbane absolutely cannot do midnight, **Option B (7:00 AM Brisbane)** is the best fallback: Brisbane gets an early but workable start, New York catches the end of day, and London takes the hit at 9 PM.

Shareable scheduling link for Option A: [View in Timezone Scheduler](https://timezones.centminmod.com/?m=eyJ2IjoyLCJmIjoiQXVzdHJhbGlhL0JyaXNiYW5lIiwiZCI6IjIwMjYtMDMtMjMiLCJoIjo3LCJtIjowLCJ0cyI6W3sidCI6IkFtZXJpY2EvTmV3X1lvcmsiLCJuIjoiTmV3IFlvcmsifSx7InQiOiJFdXJvcGUvTG9uZG9uIiwibiI6IkxvbmRvbiJ9XX0)


### Comparison LLM Timezone Responses

Comparison native AI LLM model responses

- [Claude AI Opus 4.6 Web](#claude-ai-opus-46-web)
- [ChatGPT Plus - GPT-5.4 Thinking](#chatgpt-plus---gpt-54-thinking)
- [Google Gemini AI Pro - Gemini 3.1 Pro Thinking](#google-gemini-ai-pro---gemini-31-pro-thinking)
- [Google Gemini AI Pro - Gemini 3.1 Flash Lite](#google-gemini-ai-pro---gemini-31-flash-lite)
- [ZAI Coding Pro - GLM-5](#zai-coding-pro---glm-5)
- [MiniMax M2.7](#minimax-m27)
- [Moonshot Kimini K2.5 Thinking](#moonshot-kimini-k25-thinking)
- [Xiaomi Mimo V2 Pro](#xiaomi-mimo-v2-pro)
- [Xiaomi Mimo V2 Flash](#xiaomi-mimo-v2-flash)
- [Grok 4.20 Beta Thinking](#grok-420-beta-thinking)
- [Grok 4.1 Fast Thinking](#grok-41-fast-thinking)

#### Claude AI Opus 4.6 Web

There's no perfect overlap for all three cities, but let me map it out and find the best compromise.

**Current offsets** (as of today, March 23, 2026):

- Brisbane: UTC+10 (no daylight saving)
- London: UTC+0 (GMT; clocks spring forward March 29)
- New York: UTC-4 (EDT; started March 8)

Brisbane is 10 hours ahead of London and 14 hours ahead of New York. That's a brutal spread, so someone will always be outside standard business hours.**The recommended slot is 7:00 AM Brisbane**, which lands at 5:00 PM New York and 9:00 PM London (both on the previous calendar day). Two of three cities are in or at the edge of business hours, and London at 9 PM is a reasonable ask for an important recurring meeting.

If Brisbane is willing to sacrifice instead, **9:00 PM Brisbane** flips the equation: London gets 11 AM, New York gets 7 AM, and Brisbane takes the late evening.

There is no time where all three fall within 9-to-5. The 14-hour gap between Brisbane and New York makes that mathematically impossible. One city always compromises.

**Note:** London's clocks spring forward on March 29, shifting to BST (UTC+1). After that date, the London times above shift one hour later (e.g., 7 AM Brisbane becomes 10 PM London instead of 9 PM).

#### ChatGPT Plus - GPT-5.4 Thinking

Viable options, with trade-offs:

- **Brisbane 8:00 pm / London 10:00 am / New York 6:00 am**
  Best overall balance. London stays comfortably in business hours, Brisbane is late but manageable, New York is early.

- **Brisbane 9:00 pm / London 11:00 am / New York 7:00 am**
  Easier for New York than 6:00 am, but Brisbane gets later.

- **Brisbane 10:00 pm / London 12:00 pm / New York 8:00 am**
  Good for London and acceptable for New York, but quite late for Brisbane.

- **Brisbane 11:00 pm / London 1:00 pm / New York 9:00 am**
  Fully inside business hours for London and New York, but very late for Brisbane.

- **Brisbane 7:00 pm / London 9:00 am / New York 5:00 am**
  Great for London, but too punishing for New York.

I’d choose **Brisbane 8:00 pm, London 10:00 am, New York 6:00 am** as the most optimal compromise.

Why this one:

- There is **no true overlap** where all three cities are simultaneously within normal business hours.
- Right now, Brisbane is on **UTC+10**, New York is on **UTC-4** because US daylight saving already started on **March 8, 2026**, and London is still on **UTC+0** until UK clocks go forward on **March 29, 2026**. ([Time and Date][1])
- Given those offsets, **8:00 pm Brisbane** lands at **10:00 am London** and **6:00 am New York**, which minimizes the worst inconvenience across the three locations better than the later Brisbane-heavy or earlier New York-heavy alternatives. This is an optimization judgment based on the current offsets.

Recommended meeting time:

- **8:00 pm Brisbane**
- **10:00 am London**
- **6:00 am New York**

One useful note: once the UK moves to daylight saving on **March 29, 2026**, that same Brisbane time becomes **11:00 am London** instead of 10:00 am, while New York stays at 6:00 am until later in the year. ([GOV.UK][2])

For a more human-friendly fallback set:

- best balance: **8:00 pm Brisbane / 10:00 am London / 6:00 am New York**
- New York-friendlier: **9:00 pm Brisbane / 11:00 am London / 7:00 am New York**
- London and New York business-hours priority: **11:00 pm Brisbane / 1:00 pm London / 9:00 am New York**

I can also give you a small recurring-meeting cheat sheet for these three cities across DST changes.

[1]: https://www.timeanddate.com/time/change/usa?utm_source=chatgpt.com "Daylight Saving Time 2026 in the United States"
[2]: https://www.gov.uk/when-do-the-clocks-change?utm_source=chatgpt.com "When do the clocks change?"

#### Google Gemini AI Pro - Gemini 3.1 Pro Thinking

Finding a single meeting time that falls within standard 9:00 AM to 5:00 PM business hours for Brisbane, New York, and London is mathematically impossible, as the time difference spans 14 hours. To accommodate all three, at least one city must meet outside of traditional office hours.

Based on the current date of March 23, 2026, here are the time zone offsets:
- **Brisbane (AEST):** UTC +10
- **London (GMT):** UTC +0
- **New York (EDT):** UTC -4

Here are the three most optimal windows for a meeting, ranked by how close they get to standard business hours:

##### 1. The Best Compromise (Focus on NY and London)

This is the most common choice for global teams because it captures two regions during their workday, while the third joins in the late evening.
- **New York:** 9:00 AM
- **London:** 1:00 PM
- **Brisbane:** 11:00 PM
- **Pros:** New York and London are both in the middle of their business day.
- **Cons:** Brisbane is very late at night.

##### 2. The Early/Late Shift (Focus on Brisbane and New York)

This option works well if the London participant is a "night owl" and the New York participant is finishing their day.
- **Brisbane:** 8:00 AM (Next Day)
- **New York:** 6:00 PM
- **London:** 10:00 PM
- **Pros:** Brisbane is just starting their workday; New York is only one hour past traditional business hours.
- **Cons:** London is late at night.

##### 3. The Morning/Evening Shift (Focus on London and Brisbane)

This slot is ideal for those in London and Brisbane, but it is very difficult for New York.
- **London:** 8:00 AM
- **Brisbane:** 6:00 PM
- **New York:** 4:00 AM
- **Pros:** London is starting their day; Brisbane is just finishing theirs.
- **Cons:** New York is in the middle of the night.

##### Summary Recommendation

The most "equitable" time is usually **12:00 PM London / 8:00 AM New York / 10:00 PM Brisbane**. In this scenario, London is in their mid-day, New York is just starting or slightly before their formal start, and Brisbane is at the end of their evening rather than the middle of the night.

#### Google Gemini AI Pro - Gemini 3.1 Flash Lite

To determine an optimal meeting time, let's analyze the time zone differences relative to UTC:

- **Brisbane (AEST):** UTC+10
- **London (GMT/BST):** UTC+0 or UTC+1 (Depending on Daylight Saving)
- **New York (EST/EDT):** UTC-5 or UTC-4 (Depending on Daylight Saving)

Current date is March 23, 2026. At this time, all three locations are observing their respective standard or daylight savings times (Note: March 23 is typically the transition period).

##### The Challenge

There is a significant geographic spread. When it is morning in Brisbane, it is overnight in New York and London. When it is business hours in New York, it is late evening/night in Brisbane.

**Viable Options:**

- **Option 1: Brisbane Morning / London Evening / New York Afternoon (Previous Day)**
  - *Trade-off:* Requires someone to meet outside traditional 9-5 hours.
- **Option 2: Brisbane Late Evening / London Morning / New York Early Morning**
  - *Trade-off:* Brisbane stays up very late, New York starts very early.
- **Option 3: Rotating shifts**
  - *Trade-off:* No one suffers all the time, but it lacks consistency.

##### Analysis and Recommendation

Mathematically, a 9-5 overlap for all three cities is impossible. The total spread is 15 hours (Brisbane is 15 hours ahead of New York).

**Recommendation: The "Bridge" Slot**

The most viable compromise is usually early morning for one party and late evening for the other.

- **Proposed Time:** 07:00 AM (New York) / 11:00 AM (London) / 09:00 PM (Brisbane)
- **Why this works:**
  - **New York (EST):** 7:00 AM (Early start, but professional).
  - **London (GMT):** 11:00 AM (Mid-morning, prime business time).
  - **Brisbane (AEST):** 9:00 PM (Late evening, but manageable for a single meeting).

This aligns London and New York perfectly within their respective business days while asking the Brisbane participant to take the meeting at the end of their day.

**Alternative (The "Other Way"):**

- **Proposed Time:** 10:00 PM (New York) / 2:00 AM (London) / 12:00 PM (Brisbane)
- **Why this is usually worse:** This forces London into the middle of the night, which is significantly more disruptive than a late evening in Brisbane.

**Conclusion:**
Aim for **07:00 AM (New York) / 11:00 AM (London) / 09:00 PM (Brisbane)**. It is the most sustainable slot that allows at least two parties to be in standard business hours and requires the third to work outside of them without being in the middle of the night.

#### ZAI Coding Pro - GLM-5

To find the most optimal meeting time across Brisbane, New York, and London, we must look at the intersection of standard business hours (typically 9:00 AM to 5:00 PM).

Due to the vast distance, there is **no "perfect" time** that falls strictly within 9–5 business hours for all three cities simultaneously. The geography makes this impossible because when it is afternoon in Brisbane, it is the middle of the night in New York.

However, there is a highly optimal "sweet spot" that falls within business hours for two cities and requires only a slight adjustment for the third.

##### The Optimal Meeting Time

**Time:** **8:00 AM – 9:00 AM (New York Time)**

Here is how this time translates across the three cities:

- 🇦🇺 **Brisbane:** **10:00 PM – 11:00 PM** (Same day)
  - *Verdict:* This is outside standard business hours, but it is a reasonable "late evening" slot that does not require waking up in the middle of the night.
- 🇬🇧 **London:** **1:00 PM – 2:00 PM**
  - *Verdict:* **Perfect.** This is right in the middle of the standard workday.
- 🇺🇸 **New York:** **8:00 AM – 9:00 AM**
  - *Verdict:* **Good.** This is just before standard office hours, but it is a very common time for early meetings or breakfast briefings.

---

##### Alternative: The "Early Bird" Option

If the New York team prefers to start at standard time (9:00 AM), and the Brisbane team is willing to stay up slightly later:

**Time:** **9:00 AM – 10:00 AM (New York Time)**

- 🇦🇺 **Brisbane:** **11:00 PM – 12:00 AM (Midnight)**
  - *Verdict:* A bit late for Brisbane, but manageable for a one-off important meeting.
- 🇬🇧 **London:** **2:00 PM – 3:00 PM**
  - *Verdict:* **Perfect.** Still mid-afternoon.
- 🇺🇸 **New York:** **9:00 AM – 10:00 AM**
  - *Verdict:* **Perfect.** Standard morning start.

##### Summary Recommendation

The best compromise is **8:00 AM New York / 1:00 PM London / 10:00 PM Brisbane**.

This is the only slot where two parties are operating completely within standard hours, and the third (Brisbane) is operating during reasonable waking hours (evening), rather than the New York team having to wake up at 4:00 AM or the London team having to stay until 9:00 PM.

***Note on Seasons:** This calculation assumes standard time zones (Brisbane is UTC+10, London is UTC+1/BST, New York is UTC-4/EDT). If London is in Winter (GMT) and New York is in Winter (EST), the optimal window shifts to 3:00 PM London / 10:00 AM New York / 1:00 AM Brisbane. However, the "8 AM NY / 1 PM London" window is generally the standard convention for global teams during Northern Hemisphere summer.*

#### MiniMax M2.7

##### Time Zone Analysis

**Current Date:** March 23, 2026

**DST Status:**

- US: EDT (UTC−4) — DST began March 8, 2026
- UK: GMT (UTC+0) — BST begins March 29, 2026
- Brisbane: AEST (UTC+10) — no DST

**Business Hours (local):**

| City | Local | UTC |
|------|-------|-----|
| London | 9:00–17:00 | 09:00–17:00 |
| New York | 9:00–17:00 | 13:00–21:00 |
| Brisbane | 9:00–17:00 | 23:00–07:00 |

##### The Problem

Brisbane's business hours (23:00–07:00 UTC) are **completely inverted** relative to London/New York (09:00–17:00 UTC). There is **no three-way overlap** during business hours.

##### Optimal Compromise

**Best meeting time: 09:00 UTC**

| City | Time | Business Hours? |
|------|------|-----------------|
| London | 9:00 AM | ✅ Perfect |
| New York | 5:00 AM | ❌ Too early |
| Brisbane | 7:00 PM | ❌ After hours |

**Alternative: 13:00–17:00 UTC** (5:00–9:00 AM NYC, 11 PM–3 AM Brisbane)

The reality is these three cities have minimal viable overlap. For a truly functional meeting, **two of the three participants must meet outside typical business hours**. I'd recommend either an early London morning (7:00–9:00 UTC) or a late New York evening slot.

#### Moonshot Kimini K2.5 Thinking

Given the current date (March 23, 2026) and time zone offsets:

- **Brisbane**: UTC+10 (AEST, no daylight saving)
- **New York**: UTC-4 (EDT, daylight saving active)
- **London**: UTC+0 (GMT, switches to BST on March 29)

There is no period where standard business hours (9 AM–5 PM) overlap for all three cities. The **optimal compromise** minimizes pain for all parties:

##### Primary Recommendation

**Brisbane: 10:00 PM – 11:00 PM**  
**New York: 8:00 AM – 9:00 AM**  
**London: 12:00 PM – 1:00 PM (midday)**

- **Brisbane**: Late evening (post-dinner, manageable for critical meetings)
- **New York**: Start of business day (standard working time)
- **London**: Midday lunch hour (core business period)

##### Alternative Option

If Brisbane prefers an early start over a late night:

**Brisbane: 7:00 AM – 8:00 AM**  
**New York: 5:00 PM – 6:00 PM**  
**London: 9:00 PM – 10:00 PM**

- **Brisbane**: Very early morning (start of day)
- **New York**: End of business day (acceptable for many)
- **London**: Late evening (outside standard hours)

##### Seasonal Variations

- **After March 29, 2026** (London BST/UTC+1): The 10 PM Brisbane slot becomes 1:00 PM in London (still ideal).
- **Winter (Nov–Mar)**: When New York is EST (UTC-5), the 10 PM Brisbane slot becomes 7:00 AM in New York (one hour earlier, still viable) and 12:00 PM in London.

**Verdict:** Schedule for **10:00 PM Brisbane time** (8:00 AM New York / 12:00 PM London). This hits active business hours in New York and London while keeping Brisbane at a manageable, if late, evening hour.

#### Xiaomi Mimo V2 Pro

##### Optimal Meeting Time Across Brisbane, New York & London

##### Time Zone Snapshot (March 23, 2026)

| City | Time Zone | UTC Offset |
|------|-----------|------------|
| Brisbane | AEST | UTC+10 |
| New York | EDT (DST active since Mar 8) | UTC−4 |
| London | GMT (DST starts Mar 29) | UTC+0 |

##### The Hard Truth

The three cities span **14 hours** of time zones. A 9–5 business window for any one city lands squarely in the sleeping hours of the others:

| Business Hours (local) | UTC Equivalent | In Brisbane | In New York | In London |
|---|---|---|---|---|
| Brisbane 9–17 | 23:00–07:00 | ✅ | 🌙 Sleeping | 🌙 Sleeping |
| London 8–17 | 08:00–17:00 | 🌙 Sleeping | 🌙 Sleeping→4AM | ✅ |
| New York 9–17 | 13:00–21:00 | 🌙 Sleeping | ✅ | 1PM–9PM ✅ |

**No UTC window falls within all three business hours simultaneously.**

##### Recommended Compromise

###### Option A — Best for New York & London, early morning for Brisbane

> **7:00–8:00 AM Brisbane / 5:00–6:00 PM New York / 9:00–10:00 PM London**

| City | Local Time | Status |
|------|-----------|--------|
| Brisbane | 7:00 AM | ⚠️ Early but workable (start of day) |
| New York | 5:00 PM | ✅ End of business day |
| London | 9:00 PM | ⚠️ Evening (after hours) |

###### Option B — Best for Brisbane & New York, late night for London

> **4:00 PM Brisbane / 12:00 AM (midnight) New York / 4:00 AM London**

This doesn't work — pushes NY and London into sleeping hours.

###### Option C — Best for Brisbane & London, very early for New York

> **4:00 PM Brisbane / 2:00 AM New York / 6:00 AM London**

Also poor — NY is asleep.

##### Winner: Option A

**7:00 AM Brisbane / 5:00 PM New York / 9:00 PM London (UTC 21:00)**

This is the optimal sweet spot because:

- **New York** gets a fully within-hours meeting (5 PM).
- **London** only stretches 2 hours past business hours (9 PM — reasonable for one-off calls).
- **Brisbane** is early (7 AM) but at the start of the workday, which is more tolerable than a late night.

###### Rotation Suggestion

If this is a recurring meeting, rotate the inconvenience:

| Week | Brisbane | New York | London |
|------|----------|----------|--------|
| Week 1 | 7:00 AM | 5:00 PM ⬅️ | 9:00 PM |
| Week 2 | 10:00 PM | 8:00 AM ⬅️ | 12:00 PM |

This keeps it fair — nobody always takes the off-hours slot.

#### Xiaomi Mimo V2 Flash

After considering the time zones and business hours for Brisbane (AEST, UTC+10), New York (EDT, UTC-4), and London (GMT, UTC+0), I evaluated several approaches to find an optimal meeting time. Here's a summary of the viable options with trade-offs:

- **Option 1: 10:00 UTC**  
  - London: 10:00 AM (within business hours)  
  - New York: 6:00 AM EDT (3 hours before business hours)  
  - Brisbane: 8:00 PM AEST (3 hours after business hours)  
  - Trade-off: New York participants would need to start very early, and Brisbane participants would meet late in the evening.

- **Option 2: 20:00 UTC**  
  - London: 8:00 PM GMT (3 hours after business hours)  
  - New York: 4:00 PM EDT (within business hours)  
  - Brisbane: 6:00 AM AEST (3 hours before business hours)  
  - Trade-off: London participants would meet late in the evening, and Brisbane participants would need to start early.

- **Option 3: 15:00 UTC**  
  - London: 3:00 PM (within hours)  
  - New York: 11:00 AM (within hours)  
  - Brisbane: 1:00 AM (next day, 8 hours before business hours)  
  - Trade-off: Brisbane participants would have to meet in the middle of the night.

- **Option 4: 01:00 UTC**  
  - London: 1:00 AM (8 hours before business hours)  
  - New York: 9:00 PM (4 hours after business hours)  
  - Brisbane: 11:00 AM (within hours)  
  - Trade-off: London and New York participants would meet outside typical evening hours.

**Chosen Option:**  
I recommend **20:00 UTC** as the most optimal time. This minimizes the maximum deviation from business hours (3 hours for London and Brisbane) while keeping New York within standard hours. It balances practicality, as 4:00 PM in New York is a common meeting time, and 6:00 AM in Brisbane or 8:00 PM in London might be acceptable for important meetings. Note that this assumes standard business hours (9 AM–5 PM local time) and does not account for daylight saving changes; always verify for the specific meeting date.

**Local Times at 20:00 UTC:**  

- London: 8:00 PM GMT  
- New York: 4:00 PM EDT  
- Brisbane: 6:00 AM AEST (next day)

#### Grok 4.20 Beta Thinking

**Viable options:**

- **13:00 UTC (9am NY, 1pm London, 11pm Brisbane)**: Strong core business hours for New York and London; Brisbane is very late. Trade-off: two cities optimal, one significantly disrupted.
- **22:00 UTC (8am Brisbane, 6pm NY, 10pm London)**: Good start for Brisbane, acceptable end-of-day for NY, late for London. Trade-off: favors the Australian user but pushes London past normal hours.
- **21:00 UTC (7am Brisbane, 5pm NY, 9pm London)**: Brisbane in early business hours, NY at end of business, London slightly after hours. Trade-off: all times fall within extended reasonable working window (7am–9pm local).
- **Alternating times across the three slots above**: Shares inconvenience fairly over multiple meetings. Trade-off: requires more scheduling coordination.

**Chosen approach:** 21:00 UTC (7am Brisbane, 5pm New York, 9pm London).  
This is the most optimal single time because it keeps every participant within an extended but workable window (7am–9pm local), avoids anyone being awake at midnight or later, and balances the load rather than heavily favoring two cities at the expense of the third.

**Recommended meeting time:**

- **Brisbane**: 7:00 AM AEST
- **New York**: 5:00 PM EDT
- **London**: 9:00 PM GMT

This works on the current date (23 March 2026) and most days in this season. For recurring meetings, consider rotating between the top two options every other meeting to maintain fairness.

#### Grok 4.1 Fast Thinking

##### Viable Options (UTC times, assuming Mar 2026: Brisbane AEST UTC+10, New York EDT UTC-4, London GMT UTC+0)

- **13:00 UTC** (NY 09:00, London 13:00, Brisbane 23:00): NY & London in business hours; Brisbane 6h after close (evening). Good balance, favors awake evening over sleep.
- **14:00 UTC** (NY 10:00, London 14:00, Brisbane 00:00): NY & London in business; Brisbane 7h after close (midnight). Slightly worse offset for Brisbane.
- **17:00 UTC** (NY 13:00, London 17:00, Brisbane 03:00): NY & London in business; Brisbane 6h before open (early morning). Sleep disruption risk.
- **09:00 UTC** (NY 05:00, London 09:00, Brisbane 19:00): London in business; NY early, Brisbane after hours. Only one in business.
- **21:00 UTC** (NY 17:00, London 21:00, Brisbane 07:00): NY in business; others after/before. Only one in business.

**Chosen: 13:00 UTC** (NY 09:00 EDT, London 13:00 GMT, Brisbane 23:00 AEST). Maximizes participants in business hours (2/3), with Brisbane's offset being evening (post-work) rather than predawn sleep interruption. No triple overlap possible due to 14h NY-Brisbane span. For a 1-2h meeting, extend to 13:00-15:00 UTC (Brisbane 23:00-01:00). Adjust for DST changes (e.g., London BST from Mar 29).
