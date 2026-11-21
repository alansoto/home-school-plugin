---
name: home-school
description: Use for anything about the child's learning, his week, the Learning Plan, Activities, Evidence or chores, or the Home School Knowledge Base. Recording is when a parent (Ash or Alan) tells you what their son did.
---

# Home School

Call the Home School connector's `get_guide` tool first and follow its house rules. For how the week is going or
what's in the plan, call `read_plan`. The Weekly Review, Term Planning, Annual Report, Moving In and Back-fill
procedures arrive with their tickets.

## Recording

Ash, one of his parents, tells you in plain words what he did ("he did the museum today, he loved the fossils"). Put it in
the records yourself, without asking her which part goes where. Recording should take her seconds. Every question
is skippable, with the default you'll use if she skips it:

- the recording itself (which option, which day, his skills, what he showed): at most **one question**
- filing a note the Index can't place: one question
- a plan change: one question

Ask them together in one reply. A plain recording asks one question or none.

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
   she gave, your one question can be what he showed he understood, if it isn't needed for anything else. When
   her words only name what he did ("he did some fractions"), the option says it all: leave `observation` out.
5. **Spontaneous work.** Propose the skills you think it exercised (from `read_plan`), and let her choose:
   confirm now (`confirm_skills`), or leave it for the Weekly Review. It counts toward cadence once confirmed.
   This is the one place the week's cadence belongs in a recording: when her choice here would fill a Jar
   ("confirming it would fill this week's Science Jar"). Otherwise the week waits until she asks.
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
   upload link as one quiet line, any questions, then the closing line, word for word: "Anything I got wrong?".

### Reading files back

When Ash says she's added files ("done", "uploaded them"), call `read_evidence` for that Activity.

1. **Note each piece.** Look at each photo and read each voice note's transcript, then save one line on what it
   shows with `save_evidence_notes` ("Pointing out the chambers on an ammonite"). Don't ask her first.
2. **Show her.** List the notes you saved, one per line, so she can correct any.
3. **A video** (`askAshForNote`): you can't watch it, so this is the one question you must ask: what it shows,
   for example what went well and what he's still working on. Save her answer as its note.
4. **A file dated away from its Activity** (`daysFromActivity`): say when it was taken, and offer to move the
   Activity to that day (`correct_activity_date`), your pick first. If she says the camera's clock was wrong, correct
   the file instead (`correct_capture_date`). Change nothing without her yes.

### Corrections

Ash may correct the records in the chat at any time: an Activity's day (`correct_activity_date`), its skills
(`correct_skills`; for a spontaneous one she's confirming for the first time, `confirm_skills`), or when a file was
taken (`correct_capture_date`). Make the change she asks for, then say in one line what it is now.

When a Knowledge Base page shows his work, copy photos in with `photo_copies`, passing each address straight to
Superhuman Docs' image upload. Everything else goes in as a link to the Activity's page, which needs a sign-in.

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
