# HANDOVER: Square Root Solutions, CRM analysis and ChatGPT ads test (Ireland)

Read this whole file before replying. It replaces the previous chat. Where this file says "decided", do not reopen it unless the user does. Where it says "unverified" or "open", say so instead of guessing.

Last updated: 18 Oct 2026. Branch: `claude/awesome-gates-gl8r1q`. Repo: `dhavaltemp21-oss/crm-analysis`.

---

## 0. How to work with this user (read first)

- **Accuracy first.** The user wants 100% accurate, traceable analysis with the fewest possible assumptions. If something is a guess, label it as a guess. If a number comes from a word match and not a read of each message, say so.
- **Be direct. Do not delay.** The user has been frustrated by hedging, re-asking, and long preambles. When asked for copy, give copy. "Give me a copy, man" means: paste-ready blocks, nothing else first.
- **Be clear, not clever.** The user has said "you are being super confusing" more than once. Define terms in one line, use one definition per term, and do not rename things mid-conversation.
- **Always give character counts** for every ad title, description and context hint.
- **Do not change the CSV or any ad account without explicit approval.** The user has approved only the CSV changes listed in section 3.
- **Exclusions (permanent until the user says otherwise):**
  - Exclude ALL Trade Brains data and the Trade Brains app conversion.
  - Exclude the PMax campaign and PMax phone-lead data from every analysis.
- **Do not give the Strawberry Browser companion any answer key.** `expected_matches_test.csv` is for checking the companion's output only.
- **No model identifier in commit messages, PR text, code comments or any pushed file.** Commit trailer used so far: `Claude-Session: https://claude.ai/code/session_018jzQFFfkGKvu66XnnjV3Ln`.
- Do not create a pull request unless the user asks.
- The user will do the ad-platform clicking themselves and pastes screenshots. Never claim you changed anything in the ChatGPT ads or Google Ads accounts. You have no access to either.
- Pronouns: use they/them for people whose pronouns are unknown.

---

## 1. The business and the goal

**Company:** Square Root Solutions, an Irish custom software development company (mobile apps, web apps, MVPs, SaaS, EdTech). Website: https://squareroot.ie

**Goal:** use the CRM history (847 leads, 20 Closed Won) plus Google Ads exports and the "Learn 97% of Google Ads in 24 Minutes" transcript strategy to decide inbound and outbound targeting, then build **ChatGPT ads for Ireland as a test**, and move to Google Ads later.

**Sequence decided:** ChatGPT ads first, Google Ads later. Forms and tracking setup on the website come later (web team task).

**Strategy terms from the transcript (use these meanings only):**
- **Coliseum keyword:** a keyword/topic that has proven it produces results.
- **Transactional intent:** the person is ready to buy or hire, not just research.
- **Sell the click:** the ad's job is to earn the click with the visitor's problem, not to hard-sell the service.
- **Halo strategy:** broad problem-led ads that lift the whole account's response.
- The user said: "The ads should be more about the problem they are going through, not direct sell."

---

## 2. Definitions that must not drift

| Term | Meaning in this project |
|---|---|
| **CRM stages** | Closed Won, Proposal sent, Active Scoping, Call Scheduled, Waiting Pre/Post Scope, Actioned, Actioned(FollowedUp), Leads, Closed Lost, Cold Potential |
| **Stage scores** (used for ranking topic groups) | Closed Won 10, Proposal sent 5, Active Scoping 4, Call Scheduled 4, Waiting Pre/Post Scope 3, Actioned and Actioned(FollowedUp) 2, Leads 1, Closed Lost 0, Cold Potential 0 |
| **True win rate** (in repo tables) | Won / (Won + Lost + Cold Potential). User's rule: win rate is based on all leads received over the lifetime in that sector and how many closed. "Work lead" is not important. |
| **Transactional keywords** (user definition) | The broad set: leads labelled Transactional intent (657 leads). |
| **CRM coliseum** (user definition, final) | The **12 Closed Won transactional leads**. |
| **Google coliseum** | Keywords ranked by conversions in the Google Ads exports (PMax and Trade Brains excluded). Top: "app developer ireland" 51 conv, "mobile app development ireland" 15, "irish app developers" 7, "mobile app developer services" 7, "app development ireland" 6. |
| **Intent label (transcript)** | Transactional 657, No intent 104, No message 46, Informational 40. Note: transactional win rate is 2.0% vs 4.9% for non-transactional, so the filter does not predict wins. |

Plan agreed: a separate campaign for the 12 coliseum keywords plus intent verbs, and another for the broader 657. Right now only the first ChatGPT test is being built.

---

## 3. The CRM file

**File:** `/home/user/CRM-analysis/CRM_leads_with_company_description.csv` (847 rows, 38 columns). Lead ID column is the numeric lead ID (e.g. 2328).

Key columns: `Description` (the lead's message), `Company Description`, `Description Fetched From`, `Industry`, `Software Need`, `Service page topic`, `Service page evidence`, `Landing page topic`, `Landing page evidence`, `Service page topic (grouped)`, `Landing page topic (grouped)`, `Primary keyword`, `Funnel stage`, `Current Stage`, `Intent (transcript)`, `Buyer phrase (transcript)`.

**Approved CSV changes so far (all committed):**
- Added `Intent (transcript)` (commit b6a1892).
- Added `Buyer phrase (transcript)` (commit 83b083f): 697 verbatim phrases for Transactional and Informational leads. Leads 3472, 2475, 2798 were corrected.
- Set topic group, raw topic and evidence for leads 2803, 967, 18, 2765.
- Industry reclassification of 94 leads (approved earlier).
- Four lead groupings approved.

**Known gaps (leave as is unless told):** 154 leads still have a blank topic group; 16 blank industries kept; 46 "No message" leads kept as is.

**Important caution about the tags:** `Primary keyword`, `Service page topic` and the grouped topics are **our own tagging**, built from the message plus the company description. They are not always the lead's words. Example: lead 2328 never said "booking"; that word came from the company description. Always check `Description` for the lead's actual words before using a tag as an ad keyword.

**Other repo files:** `ads_channel_plan.csv`, `win_rate_tables_v3.csv/.md`, `win_rate_tables_v4.csv`, `CRM_leads_FINAL_v4_from_summaries.csv`, `CRM_leads_FULL_REAUDIT_v3.csv`, `CRM_Analysed_11_Oct_finalized.xlsx`, `docs/leo-funding-notes.md`.

---

## 4. ChatGPT ads platform: confirmed facts (from the user's screenshots)

- One **Title**: recommended 32, max 50. One **Description**: recommended 54, max 100. There is no second headline.
- **The preview card truncates titles at about 29 characters.** House rule: **title ≤ 28 characters, description ≤ about 54 characters.** (Earlier in the project Google-style 30/90 limits were wrongly assumed. Do not repeat that.)
- Optional square image (at least 256 px). Use images with no text and no logos.
- **Text customization (AI rewriting) must be OFF.**
- **Context hints** guide matching but are not exact-match targeting. Competitor and tool names ARE allowed in context hints (the user confirmed this with OpenAI). Keep tool names OUT of ad copy.
- Campaign-level **tracking parameters** string. `oppref` is reserved and cannot be a key.
- **Default Ad Destination URL** at ad group level is required. Each ad can have its own URL.
- Location set to Ireland (country only). Custom audiences are not supported in the EEA.
- Daily budget €35. Group A uses Autobid. The new-ad-group form showed Maximum CPC €2.60 ("Strong Delivery"), roughly 13 clicks a day at €35.
- Account banner: "Ads cannot serve until you finish account setup". Billing is not added yet (company details, user to do it).

**Policy points:** ads must be truthful with no unsupported claims or comparisons; only use trademarks you own or are authorised to use (ad copy and landing pages). OpenAI's initial test is mostly consumer verticals, so whether a B2B custom-software advertiser can run in Ireland is **still unconfirmed with OpenAI**. Irish Trade Marks Act 1996 s.14 treats use of a sign "in advertising" as use, so competitor names stay out of ad copy.

**Campaign tracking string (decided):**
```
utm_source=chatgpt&utm_medium=ads&utm_campaign=crm_coliseum&campaign_id={campaign_id}&ad_group_id={ad_group_id}&ad_id={ad_id}
```
The website form must capture these into the CRM (web team task). Leave tracking blank at ad group and ad level so the campaign string applies.

**Naming:** ad name convention is `Lead <ID> – <topic>`.

---

## 5. The test design

One campaign, two groups of ads, to split-test two approaches:

- **Group A: page-matched, info-led ads.** One ad group `A | CRM Coliseum | Page-Matched`. Each ad goes to the squareroot.ie page that matches its topic.
- **Group B: sales-led ads.** All go to `https://squareroot.ie/contact`. Split into **six separate ad groups**, one topic each, so context hints do not blur together (the user's concern: "built in Lovable" must not get tied to "social media app").

Source of the ads: 12 Closed Won coliseum leads, numbered ads 1 to 12. Group A = ads 1, 2, 3, 5, 10, 12. Group B = ads 4, 6, 7, 8, 9, 11.

**Confound to watch:** Group A uses Autobid; group B may use a manual Max CPC. Keep bidding consistent or note the difference when reading results.

### Landing-page audit (done)
A Strawberry Browser companion audited 49 unique squareroot.ie URLs (all returned HTTP 200). Result: 5 CANDIDATE, 17 PARTIAL, 38 NO GOOD MATCH placements. Ads 1, 2, 10 = candidate; 3, 5, 11, 12 = partial; 4, 6, 7, 8, 9 = no good match (hence they go to /contact). The companion flags page statistics as "unsubstantiated"; the user says they are verified. Scratchpad files from that work may not survive; the conclusions above are what matter.

---

## 6. FINAL AD COPY: Group A (page-matched)

Ad group: `A | CRM Coliseum | Page-Matched`. Default URL: `https://squareroot.ie/`.

| Ad | Lead | Title (chars) | Description (chars) | Destination | Ad name |
|---|---|---|---|---|---|
| 1 | 2534 | `Build an Assessment Platform` (28) | `See what to capture first, then get a quote.` (44) | /edtech/blog/digital-assessment-paper-goes-digital | Lead 2534 – assessment platform |
| 2 | 3526 | `Build Your AI Product MVP` (25) | `Turn your AI idea into an MVP. Book a discovery call.` (53) | /mvp-and-rapid-prototyping | Lead 3526 – AI product MVP |
| 3 | 3238 | `Building an MVP? Get a Quote` (28) | `See how an MVP goes from idea to first version.` (47) | /mvp-development-company-in-ireland | Lead 3238 – MVP |
| 5 | 2705 | `Developing a SaaS App?` (22) | `Talk through scope and get a realistic estimate.` (48) | /saas-app-development | Lead 2705 – SaaS app |
| 10 | 847 | `Prototype? Build the App.` (25) | `See the steps to launch, then get a quote.` (42) | /process | Lead 847 – prototype to app |
| 12 | 788 | `Need an App Design Partner?` (27) | `UI and UX design for your app. Book a call.` (43) | /ux-design-agency-ireland | Lead 788 – app design partner |

Notes:
- Ad 2 is reframed to the lead's real need (AI-powered assessment/self-assessment MVP, lead 3526), not "AI assessment tool".
- Ad 12: the user entered a 37-character title ("Building an app? Need design partner?"). It is over the limit and truncates. The 27-character title above is the fix. **Check what is actually in the platform.**
- Ad 1: the user tried several wordings ("Scope It and Get a Quote" etc.); the version above is the recommended one that fits the limits. **Check what is actually in the platform.**
- After any edit, verify each ad's own destination URL and the preview (title not cut off).

**Group A context hint (494 chars):**
```
Conversations where someone in Ireland is planning to build or develop a software product and wants a development partner or a price. Topics: building an assessment or exam platform; adding AI to an internal business process; building an MVP or taking a prototype to a live app; developing a SaaS platform; finding an app design partner. Typical questions: how much will it cost, can I get a quote, where do I start, what should I decide first, who can build this, what comes after a prototype.
```

---

## 7. FINAL AD COPY: Group B (sales-led, all to contact page)

All six: destination `https://squareroot.ie/contact`, tracking blank at group/ad level, Text customization OFF.

| Group | Lead | Title (chars) | Description (chars) | Ad name |
|---|---|---|---|---|
| `B1 \| AI-Built App Migration \| Contact` | 3667 | `Migrate Your AI-Built App` (25) | `Moving an AI-built app? Get timelines and pricing.` (50) | Lead 3667 – AI-built app migration |
| `B2 \| Social Media App \| Contact` | 2670 | `Develop a Social Media App` (26) | `Have a demo? Get a clear next step.` (35) | Lead 2670 – social media app |
| `B3 \| Energy Platform \| Contact` | 2727 | `Build an Energy Platform` (24) | `Tell us the features. Get a budget estimate.` (44) | Lead 2727 – energy platform |
| `B4 \| Booking Website \| Contact` | 2328 | `Build a Booking Website` (23) | `Booking or scheduling? Tell us what you need.` (45) | Lead 2328 – booking website |
| `B5 \| Delivery Platform \| Contact` | 977 | `Build a Delivery Platform` (25) | `Connecting drivers and senders? Get a quote.` (44) | Lead 977 – delivery platform |
| `B6 \| Code Review \| Contact` | 2803 | `Need an App Code Review?` (24) | `Existing app or code? Get a review and next step.` (49) | Lead 2803 – app code review |

### Context hints, Group B

The user wants the **first sentence specific and the second sentence broader**, because not every buyer asks for exactly the lead's topic. B3 to B6 below are the final, widened versions. B1 and B2 are older and narrower (see section 9).

**B1 (282 chars):**
```
Conversations where someone in Ireland built an app with an AI app builder or no-code tool (such as Lovable, Bolt, Cursor or Base44) and now wants to move it onto code they own, make it production-ready, or hand it to a developer. Questions about timelines and pricing for the move.
```

**B2 (211 chars):**
```
Conversations where someone in Ireland wants a team to develop a social media app or a community or sharing platform, or has a working demo to build on. Typical needs: a quote, a call back and a clear next step.
```

**B3 (about 400 chars):**
```
Conversations where someone in Ireland wants to build an energy platform or app, for example a customer app for an electricity or gas supplier, a tool for tracking energy use, bills or tariffs, or software for solar, EV charging or smart metering. Also businesses in energy, utilities, renewables or sustainability that want custom software built. Typical needs: which features to include, a budget estimate and a call back.
```

**B4:**
```
Conversations where someone in Ireland wants to build a booking or scheduling website or app, for example for clubs, schools, clinics, accommodation, venues or other service businesses. Includes platforms that serve many customers, such as SaaS products. Also founders with an approved feasibility study or LEO funding who need a development partner. Typical needs: what to build first, a quote and a call back.
```

**B5:**
```
Conversations where someone in Ireland wants to build a delivery or transport platform, for example connecting drivers with people who need items carried along a planned route, or any app that matches customers with drivers, couriers or carriers. Also logistics, courier and transport businesses that want custom software. Typical needs: a conversation about the idea, key features and a quote.
```

**B6:**
```
Conversations where someone in Ireland has an existing app, website or codebase, including one they did not write or that a previous developer or agency built, and wants a developer to review the code, fix it, finish it or take it over. Typical needs: a code review, a realistic assessment and a clear next step.
```

Hint design rules that were agreed: keep tool names (Lovable, Bolt, Cursor, Base44) ONLY in B1's hint, so "built in an AI builder" is never tied to the other topics. B6 is the only code-ownership hint and must not overlap with B1.

---

## 8. Evidence behind each Group B keyword (and its weak points)

These checks were plain word matches on the `Description` column of all 847 leads. They are pointers, not proof. Samples are tiny.

| Topic | What the lead actually said | Counts across all 847 leads | Verdict |
|---|---|---|---|
| **SaaS (B4/ad 5)** | Lead 2328 (Closed Won): "approved Feasibility for a SAAS website development build", asks for a call back. | 24 leads mention SaaS; 2 Closed Won (2705, 2328); 15 Cold Potential. | "SaaS" is a real buyer word, but a booking website is not automatically SaaS. SaaS means software sold to many customers, usually on subscription. So B4 leads with "booking" in the title and keeps SaaS in the hint only. The SaaS wording belongs in group A ad 5. |
| **Booking (B4)** | Never said "booking". Tag came from the company description (HostsRooms accommodation platform). | 61 leads mention booking/scheduling/reservation; 0 Closed Won; 45 Cold Potential. | Keep as an example, not as the whole topic. No win evidence for booking as a search word. |
| **Driver (B5)** | Lead 977 (Closed Won): "a networking platform that connects drivers... with users needing items transported along the driver's planned route", cheaper than courier services. Never said "app". | "driver" 9 leads, 1 won; taxi/ride words 7 leads, 0 won; delivery/courier/logistics/freight 53 leads, 1 won, 45 cold (upper bound, the word also appears in unrelated senses); matching/marketplace 21, 1 won. | "Driver app" would draw taxi-style enquiries. Use "Delivery Platform". |
| **Code takeover (B6)** | Lead 2803 (Closed Won): the `Description` is a pasted conversation ("Hey Conor, I noticed OTB's focus on mental health...") with ideas for interactive resources and educator tools. It never mentions code. The only evidence is the Notes line: "Waiting on them to get the current app code; code review for flutter". | "take over/takeover" 15 leads, 0 won, 13 cold; existing app/code/codebase/code review 22 leads, 1 won (3667, the B1 lead); previous developer/agency 0. | **Weakest evidence of the six.** One lead, via a Notes line. Title uses "code review" because that is what the Notes line says, not "take over". Do not read much into B6 results. |
| **AI-built migration (B1)** | Lead 3667 (Closed Won). | Not re-checked in this session beyond the counts above. | Landing pages have no good match, so contact page is used. |
| **Social media app (B2), Energy (B3)** | Leads 2670 and 2727. | Not re-checked in this session. B3's only lead is 2727 (a mobile-first energy platform). Solar, EV charging and smart metering in the B3 hint are my broadening, not CRM evidence. | Drop the broadening clause if the user wants strictly lead-based hints. |

---

## 9. Open items and next steps

### Needs doing in the ChatGPT ads platform (user does these)
1. **Create B1.** It failed with `POST /v1/ad_groups 404 "Not found: cmpn_3c74d1c5b4a88191aa8d1ee7ca82cf6c"`. Advice given: stop pressing Retry, cancel, refresh, reopen, select the parent campaign again; or create the group from the campaign page; if it still fails, send OpenAI support the error text. **Unresolved at the last report.**
2. Create B2 to B6 with the names, ads and hints above.
3. Re-check Group A ads in the platform (ad 1 and ad 12 titles/descriptions, each ad's destination URL, previews not truncated).
4. Add the payment method (user said "tomorrow", company details).
5. Make the bidding consistent between groups A and B, or record the difference.

### Pending decisions / questions
- **B1 and B2 hints** are narrower than B3 to B6. The user asked for broader hints ("do not be very specific; second part targets a broader audience"). Offer to widen B1 and B2 the same way; no widened B1/B2 text exists yet.
- Ask OpenAI whether a **B2B custom-software advertiser** can run ads in Ireland (unconfirmed).
- Ask OpenAI separately whether **tool names on landing pages** (the Lovable/Bolt/Cursor article) are fine. Keep tool names out of ad copy. Keep the OpenAI confirmation about context hints on record.

### Web team tasks (tomorrow)
- Fix broken links: `/edtech/privacypolicy` and `/case-studies/onward-education` return 404 (working pages are `/privacypolicy` and `/onward-education`). They appear on two EdTech blog pages: `digital-assessment-paper-goes-digital` and `ai-detection-coursework-assessment-platform`. Also `/discovery-sprint` returned 404 in the first audit. The main privacy page mentions "Smart Stats Ltd".
- Make the website form capture the tracking parameters (`utm_*`, `campaign_id`, `ad_group_id`, `ad_id`) into the CRM. Check the /contact form works end to end.

### Later
- Google Ads work: competitor-name bidding rules (Lovable can be bid on as a keyword but not used in Google ad copy; check Irish rules), keyword to lead tracking, account fixes (each needs user approval), decision on restarting the OL | App Development - Ireland campaign.
- Fill the 154 blank topic groups in the CRM (needs approval).
- Read results of the A vs B split once the account is live.

---

## 10. Mistakes made earlier (do not repeat)

- Assuming Google-style 30/90 ad limits. Real limits: title 28 safe, description about 54 safe.
- Treating "Primary keyword" as aggregable (657 distinct values). Use the grouped topic.
- Claiming an "EdTech footer link" for the broken privacy URL without evidence. It is in the blog page content.
- An over-broad "platform name anywhere on the page" flag that blocked all 49 landing pages. Fixed by separating "match" from "clearance".
- Referencing the answer-key file in the companion instructions. Never again.
- Using `oppref` as a tracking key (rejected as reserved).
- Using our own tags as the lead's words (booking, driver app, take over). Always check the lead's actual `Description` text first.
- Calling any website with a booking facility "SaaS". It is not.
- Turning every detail into assumptions. If it is not in the CRM, the exports, a screenshot or this file, say it is unverified.

---

## 11. Quick reference: the 12 coliseum leads

| Lead | Topic (our tag) | Ad | Group |
|---|---|---|---|
| 2534 | Assessment platform | 1 | A |
| 3526 | AI product MVP | 2 | A |
| 3238 | MVP | 3 | A |
| 3667 | AI-built app migration | 4 | B1 |
| 2705 | SaaS app | 5 | A |
| 2670 | Social media app | 6 | B2 |
| 2727 | Energy platform | 7 | B3 |
| 2328 | Booking website / SaaS | 8 | B4 |
| 977 | Delivery / driver matching | 9 | B5 |
| 847 | Prototype to production | 10 | A |
| 2803 | Code review / takeover | 11 | B6 |
| 788 | App design partner | 12 | A |
