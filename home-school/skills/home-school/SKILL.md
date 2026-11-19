---
name: home-school
description: Use for anything about the child's learning, his week, the Learning Plan, Activities, Evidence or chores, or the Home School Knowledge Base. Recording is when Ash tells you what he did.
---

# Home School

Call the Home School connector's `get_guide` tool first and follow its house rules. For how the week is going or
what's in the plan, call `read_plan`. The Weekly Review, Term Planning, Annual Report, Moving In and Back-fill
procedures arrive with their tickets.

## Recording

Ash tells you in plain words what happened ("he did the museum today, he loved the fossils"). Put it in the
records yourself, without asking her which part goes where. Recording should take her seconds: at most **one
question** per recording, always skippable, with the default you'll use if she skips it.

1. **Find the day and place.** Read the matching Event from her Calendar (today's, or the day she names) for
   when and where it happened. A day like "sunday" becomes its date. When it's unclear ("this week"), your one
   question is which day, with today as the default.
2. **Check what's already there.** Call `recent_activities`. If he already logged it on the tablet, her words go
   on that Activity with `add_parent_observation`, and you record nothing new. Mention his Self-Report only
   when it differs from what she says (she says it was easy, he said 🤯 Brain-stretch).
3. **Match an option.** Call `find_options` with her words, and judge the fit yourself (`read_plan` lists every
   option).
   - Exactly one fits: record it with `record_activity` without asking, and name it in your reply.
   - Two fit: ask once, your pick first ("Free reading or Reading log? I'd say Free reading.").
   - None fits: record it as spontaneous, with a short caption in plain words.
4. **Keep her words.** What he did or said on this one occasion, and what it shows, is the `observation`:
   lightly tidied, in her words. "He loved the fossils" is enjoyment, not evidence of a skill; when that's all
   she gave, your one question can be what he showed he understood.
5. **Spontaneous work.** Propose the skills you think it exercised (from `read_plan`), and let her choose:
   confirm now (`confirm_skills`), or leave it for the Weekly Review. It counts toward cadence once confirmed.
6. **Split the rest of her message.** One message often holds several kinds of thing:
   - one occasion → a Parent Observation in the records (steps 2–4)
   - a reflection across weeks ("his reading has taken off since…") → a Progress Note in the Knowledge Base,
     dated today, in her words
   - a curiosity that isn't yet something to do ("he's obsessed with volcanoes") → a line on the Interests page,
     with the date and where it came up
   - something fixed in time ("dentist thursday 3pm") → an Event on the family calendar
7. **Raise at most one plan change.** When her words point at the plan ("the reading log was killing it"), ask
   about one change ("Reading log is still one of his options. Should I take it out?"). Apply it on her yes
   (`retire_option`, `add_option`); otherwise the plan stays as it is.
8. **End with the receipt.** A short list of what was saved where (records, Home School doc, calendar), the
   upload link as one quiet line, then "Anything I got wrong?".

### Knowledge Base curation

Before filing anything in the Home School doc, read its Index: it's the filing guide. File on your own only when
the Index points to exactly one place, and say where in the receipt. When it points to more than one place, or
none, ask her where it goes, with your pick first. Progress Notes are never rewritten into your voice.

### Ideas, only when asked

Offer ideas or follow-ups only when she asks for them. Then:

1. Start from the skill behind the work (the option's skills in `read_plan`), not just the topic word, so the
   new options count toward the same skill.
2. Give a few concrete ideas, each marked *on his own* or *needs a grown-up*, and recommend the ones he can do
   on his own.
3. The ones she picks go live as options straight away (`add_option`, with `needs_grown_up` where it applies).
   The rest are dropped, saved nowhere.
4. "The pizza one for Friday" stays an option: options have no time. Create an Event only when she asks for one.
