# Beta Results

5-day beta: 289 users, 359 sessions, ~5,200 messages, and up to 317 messages in a single session.

If you're familiar with AI companion products, you've seen this problem before: getting users in is easy; keeping them is not. This report is for anyone dealing with short sessions, conversations that fall apart, and low second-month renewal.

## Traffic

Traffic came from two small Telegram channels with a general male audience and one roleplay-focused channel. Most users churned quickly, as expected: this was cold, unoptimized traffic, a single character, and a first-pass test.

## Session Depth

20% of sessions passed 30 messages, 11% passed 50, and 3% passed 100. The longest sessions ran well past 150 user messages. In a market where most bots lose momentum after the first few exchanges, that is a strong signal of dialogue quality.

<img width="1417" height="713" alt="Session depth chart" src="https://github.com/user-attachments/assets/d24a5493-30bb-4178-aac7-bc4b944139f1" />

<br><br>

The table below shows a cross-section of session depth: how many messages a typical session generated and how far the most engaged users went.

The average session yielded 21.56 messages, but the tail matters more in this test: the top 10% reached 55 messages, and the top 5% reached 85+.

<br><br>

| Sessions | Users | Avg. turns / session | p75 turns | p90 turns | p95 turns |
| -------: | ----: | -------------------: | --------: | --------: | --------: |
|      359 |   289 |                21.56 |      26.5 |        55 |      85.6 |

## User-Level Engagement

The chart above shows depth per visit. This one shows cumulative attention per user, including conversation restarts.

A quarter of users went beyond their first session: they returned, restarted the conversation, and spent more time with the same character. If users are willing to replay the same scenario, the product is generating repeat engagement rather than relying only on first-session interest.

<img width="1427" height="712" alt="User-level engagement chart" src="https://github.com/user-attachments/assets/237f938c-9883-4ea5-84eb-ab6033381ede" />

## Time to Monetization Point

Most users expected faster progression, while the prompt prioritized realism and gradual scene development. The monetization point was reached only around turn 38 on average — too late for cold traffic. Many users dropped off before getting there, which explains a significant share of short sessions.

| Metric                               | Value |
| ------------------------------------ | ----: |
| Users reaching monetization point    |    50 |
| Sessions reaching monetization point |    55 |
| Avg. turns to monetization point     |    38 |

## Post-Beta Modes: Casual vs. Roleplay

After the main beta, a mode switch was added for the remaining ad traffic: one path optimized for faster progression, and another for users who wanted a full roleplay experience.

| Mode     | Users |
| -------- | ----: |
| Casual      |    41 |
| Roleplay |     7 |

In Casual mode, 39% of users reached the monetization point — 16 out of 41 — while the median path dropped fourfold, from 38 turns to 9.5.

| Metric                                         |   Value |
| ---------------------------------------------- | ------: |
| Users reaching monetization point in сasual mode  | 16 / 41 |
| Median turns to monetization point in сasual mode |     9.5 |

The engine can be tuned for different monetization models. Immersive roleplay supports longer narrative progression, while less patient traffic needs faster engagement and a shorter path to conversion. The result depends not just on the model, but on how the conversation logic, runtime modes, and prompt are tuned around it. The same engine can support both longer-form roleplay and faster, higher-frequency interactions.

## Why a Static Prompt Doesn't Survive Real Users

Pack all of a character's behavior into one large prompt, and the model starts degrading quickly: instructions drift, the bot gets pulled into meta-conversation, starts repeating itself, and eventually loses track of what the user is actually asking.

Instead, the engine assigns each turn a runtime mode:

| Mode              | Triggers when...                                                                                                                     |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| `repair`          | The user tries to break the scene through meta questions, derailment, or attempts to force the interaction outside its intended flow |
| `reground`        | The user drifts out of the moment through disengaged, low-effort replies or fading interest                                          |
| `follow_user`     | The user sets the pace and direction, and the bot follows the lead while staying in character                                        |
| `take_initiative` | The user remains in the scene but stops driving it, so the bot adds action, shifts the pace, or advances the next beat               |

## Dynamic Steering in Numbers

Most responses were state-aware and action-driven: 48% took initiative, and 44% followed the user. Separately, 16% of turns included repair or reground behavior when the conversation started to break down.

| Turn type         | Count |  Share |
| ----------------- | ----: | -----: |
| `take_initiative` | 2,531 | 48.69% |
| `follow_user`     | 2,307 | 44.38% |
| `repair`          |   466 |  8.96% |
| `reground`        |   356 |  6.85% |

These modes can overlap within the same turn, so their shares are not intended to sum to 100%.

Modes are not decorative logic on paper. Only 12.3% of replies went out without dynamic steering. In 87.7% of turns, the bot received a concrete instruction for the current situation.

| Metric                    | Value |
| ------------------------- | ----: |
| Total turns               | 5,198 |
| Dynamically steered turns | 4,559 |
| Dynamically steered share | 87.7% |

Long dialogues hold because the character does not respond to every situation the same way. It continuously adapts to the user's state.

## Recovery

The most important test is what happens after something goes wrong — when a user tries to break the bot or loses interest.

| Metric                     | Value |
| -------------------------- | ----: |
| Recovery events            |   580 |
| Median turns post-recovery |    12 |
| p75 turns post-recovery    | 34.25 |
| p90 turns post-recovery    |  72.1 |

Recovery did real work. In most cases, the bot brought users back into the conversation and kept them there. This matters especially in roleplay-heavy products, where users frequently test boundaries, derail the interaction, and probe for failure points. The character held up under that pressure.

## Photo Flow

Photo flow is not the focus of this report, so this is not a deep dive — only the headline: visual delivery is built directly into the engine. The timing of visual content comes from the dialogue engine; post-processing reads the current scene state and decides whether to surface a visual.

| Session length (turns) | Sessions | Avg. photo triggers |
| ---------------------- | -------: | ------------------: |
| 1–5                    |      155 |                0.48 |
| 6–15                   |       75 |                3.13 |
| 16–30                  |       57 |                6.37 |
| 31–50                  |       32 |               10.72 |
| 51–100                 |       29 |               17.24 |
| 101+                   |       11 |               36.55 |

A user does not remain in one static moment. They move through a sequence of scene states, and each state can trigger relevant visual content. Contextual delivery makes each image part of the interaction, not a separate gallery item. The user gets new context to engage with, while the product gets natural points for premium content and conversion.

## Conclusion

This beta shows that a dialogue engine does not just affect how natural a conversation feels — it affects the economics of the product. When the bot holds the scene, remembers what happened, and behaves appropriately to the moment, the product has a better chance of bringing users back and converting them into renewals.

If you already have traffic, the weak point usually is not getting more people in. It is avoiding the loss of users who have already shown up.

---

Interested in a pilot, a product audit, or a scoping call? → [site](https://thaelr.github.io/personal-site/) · [email](mailto:shenko.nik@gmail.com) · [telegram](https://t.me/taabler)
