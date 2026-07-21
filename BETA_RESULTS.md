# Beta Results

5-day beta: 289 users, 359 sessions, ~5,200 messages, up to 317 messages in a single session.

If you're already familiar with AI companion products, you've seen this problem before: getting a user in is easy, keeping them is not. This report is for anyone who has already run into short sessions, conversations that fall apart, and low month-two renewal.

## Traffic

Traffic came from two small Telegram channels with male audience, plus one roleplay-focused channel. Most users churned quickly, as expected — this was cold, unoptimized traffic, a single character, and a first-pass test.

## Session Depth

20% of sessions passed 30 messages, 11% passed 50, 3% passed 100. The longest sessions ran well past 150 user messages. In a market where most bots deflate after a short warm-up, that's a strong signal on dialogue quality.

<img width="1417" height="713" alt="график на сайт" src="https://github.com/user-attachments/assets/d24a5493-30bb-4178-aac7-bc4b944139f1" />
<br><br>
The table below shows a cross-section by session depth: how many messages did a regular session give and how far did the most involved users go.
The average session yielded 21.56 messages. But in this test, the tail is more important: the top 10% of sessions went for 55 messages, the top 5% for 85+
<br><br>

  | Sessions | Users | Avg. turns / session | p75 turns | p90 turns | p95 turns | 
  | -------: | ----: | -------------------: | --------: | --------: | --------: | 
  |      359 |   289 |                21.56 |      26.5 |        55 |      85.6 |  




## User-Level Engagement

The chart above shows depth per visit. This one shows cumulative attention per user, including scene restarts.

A quarter of users didn't stop at the first pass — they came back into the scene, restarted, and spent more attention on the same character. If a user is willing to replay the same scenario, the product isn't just monetizing first-time interest, it's monetizing repeat engagement.

<img width="1427" height="712" alt="user depth" src="https://github.com/user-attachments/assets/237f938c-9883-4ea5-84eb-ab6033381ede" />


## Time to Target Action

Most users came in looking for a get fun, but the prompt was tuned for realism: the character was too strict with the user and brought the scene back to harsh realism. Target action reached the target action only around turn 38 — too hard quest for cold traffic. A share of users simply didn't stick around long enough to get there. That gap explains a good part of the short-session problem.

| Metric | Value |
|---|---|
| Users reaching target action | 50 |
| Sessions reaching target action | 55 |
| Avg. turns to target action | 38 |

## Post-Beta Modes: Fast vs. Roleplay

After the main beta, on the tail of ad traffic, a mode switch was added: one path for users who wanted things to move fast, one for those who wanted a full roleplay scene.

| Mode | Users |
|---|---|
| Fun | 41 |
| Roleplay | 7 |

In fun mode, 39% of users reached the target action (16 of 41), and the median path to it dropped 4x — from 38 turns to 9.5.

| Metric | Value |
|---|---|
| Users reaching target action (fast mode) | 16 / 41 |
| Median turns to target action (fast mode) | 9.5 |

The takeaway: the engine can be tuned to different monetization models. Slow-burn roleplay keeps a long warm-up and extended scene; fast-lane traffic needs a shorter path to the target action and payment. The result depends not just on the model, but on how the conversation logic, modes, and prompt are tuned around it — the same engine can run as a slow roleplay or a fast, high-frequency scenario.

## Why a Static Prompt Doesn't Survive Real Users

Pack all of a character's behavior into one large prompt and the model starts degrading fast: instructions drift, the bot picks up on meta-conversation, starts repeating itself, and eventually loses track of what's actually being asked of it.

Instead, the engine assigns each turn a runtime mode:

| Mode | Triggers when... |
|---|---|
| `repair` | the user tries to break the scene — meta questions, attempts to derail, inappropriate escalation |
| `reground` | the user drifts out of the moment — disengaged, low-effort replies, fading interest |
| `follow_user` | the user is setting pace and direction — the bot picks up the lead and stays in character |
| `take_initiative` | the user is in the scene but not driving it — the bot adds action, shifts pace, pushes the next beat |

## Dynamic Steering in Numbers

Most responses were state-aware and action-driven: 48% took initiative, 44% followed the user. Another 16% repaired or regrounded the conversation when it started to break down.
| Turn type | Count | Share |
|---|---|---|
| take_initiative | 2,531 | 48.69% |
| follow_user | 2,307 | 44.38% |
| repair | 466 | 8.96% |
| reground | 356 | 6.85% |

Modes aren't decorative logic on paper — only 12.3% of replies went out without dynamic steering. In 87.7% of turns, the bot received a concrete instruction for the current situation. 


| Metric | Value |
|---|---|
| Total turns | 5,198 |
| Dynamically steered turns | 4,559 |
| Dynamically steered share | 87.7% |

That's what sustains a long dialogue: the avatar doesn't answer the same way to everything, it continuously adapts to the user's state.

## Recovery

The most important test is what happens after things go wrong — when a user tries to break the bot, or loses interest.

| Metric | Value |
|---|---|
| Recovery events | 580 |
| Median turns post-recovery | 12 |
| p75 turns post-recovery | 34.25 |
| p90 turns post-recovery | 72.1 |

Recovery wasn't a formality. In most cases, the bot actually brought the user back into the conversation and held them there. This matters specifically for mature-themed traffic — users test boundaries, go off-script, push, and probe for where the bot breaks. After this test round, the character held up under that pressure.

## Photo Flow

Photo flow isn't the focus of this report, so this isn't a deep-dive — just the headline: it's natively built into the engine. The moment a photo is offered comes directly out of the dialogue engine's output; post-processing reads scene state and decides whether to surface a visual.

| Session length (turns) | Sessions | Avg. photo triggers |
|---|---|---|
| 1–5 | 155 | 0.48 |
| 6–15 | 75 | 3.13 |
| 16–30 | 57 | 6.37 |
| 31–50 | 32 | 10.72 |
| 51–100 | 29 | 17.24 |
| 101+ | 11 | 36.55 |

A user doesn't sit in one static moment — they move through a sequence of scene states, and each one is a potential photo trigger. That's the point of contextual delivery: an image isn't a separate gallery, it's a continuation of the current beat. The user gets new material to react to, and the product gets sensible checkpoints for unlocking media and payment.

## Conclusion

This beta shows that a dialogue engine doesn't just affect "how nice the conversation reads" — it affects the economics of the product. When the bot holds the scene, remembers what happened, and behaves appropriately to the moment, the product has a better shot at bringing users back and converting renewals.

If you already have traffic, the weak point usually isn't getting more people in — it's not burning the ones who already showed up.

---

Interested in a pilot, an audit of your product, or a scoping call? → [site] · [email] · [telegram]
