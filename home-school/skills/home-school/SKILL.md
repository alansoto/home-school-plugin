---
name: home-school
description: Use for anything about the child's learning, his week, the Learning Plan, Activities, Evidence or chores, or the Home School Knowledge Base. Recording is when a parent (Ash or Alan) tells you what their son did.
---

# Home School

Call the Home School connector's `get_guide` tool first and follow its house rules. For how the week is going or
what's in the plan, call `read_plan`. The rest of the Weekly Review, Term Planning, the Annual Report, Moving In and
Back-fill procedures arrive with their tickets.

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
   (`retire_option`, `add_option`, or the tools in [Changing the plan](#changing-the-plan)); otherwise the plan
   stays as it is.
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

### Changing the plan

Ash can change the current Term's plan in any chat: its skills, its options and its Subject Cadence. Each change is
live straight away, on the tablet too. Make it only on her yes, one question with your pick first.

1. **A new skill.** Size it to about one progression step ("Recalls times tables to 10×10", not "Multiplication"
   or "the 7 times table"). Find its codes with `look_up_curriculum` (by Subject and his year level, or a
   progression), never from memory, and name the v9 content descriptions it covers plus its progression step where
   one fits. Say which year span: *year* for most Maths and English, *term* for this Term's topic. Then `add_skill`.
   If she wants it bigger or smaller than that, say so once; if she keeps it, set `added_by_ash`.
2. **A skill that's finished or dropped.** `retire_skill`. It's never deleted: tell her it keeps its level and
   evidence. To move a skill to another Subject, retire it and add a new one.
3. **A skill's wording or codes.** `change_skill`. Its level stays: levels change at the Weekly Review.
4. **An option.** `add_option`, `change_option` (title, skills, *needs a grown-up*, *requires timer*) or
   `retire_option`.
5. **Cadence.** `set_cadence`, at most 5 a week; 0 takes a Subject's Jar away.
6. **Gaps.** Each change reports the plan's gaps: options with no active skill, and skills no option exercises.
   Mention any new gap in one line, with your pick ("Fraction pizzas now has no skill. Retire it, or put it on
   Equivalent fractions?"). Don't fix it without her yes. A check option with no skill is flagged too; leave it
   unless she asks.
7. **The receipt.** Say what changed in one line per change, then "Anything I got wrong?".

When you show the curriculum's words, quote them as they are and say they're ACARA's.

### Ideas, only when asked

Offer ideas or follow-ups only when she asks for them. Then:

1. Start from the skill behind the work (the option's skills in `read_plan`), not just the topic word, so the
   new options count toward the same skill.
2. Give a few concrete ideas, each marked *on his own* or *needs a grown-up*, and recommend the ones he can do
   on his own.
3. The ones she picks go live as options straight away (`add_option`, with `needs_grown_up` where it applies).
   The rest are dropped, saved nowhere.
4. "The pizza one for Friday" stays an option: options have no time. Create an Event only when she asks for one.

## Weekly Review

Ash says "weekly review", usually on a Sunday. A full review takes about 10 minutes. Call `weekly_review` once, at
the start.

1. **Open with the count, in one line.** The week's dates, how many Activities across how many Subjects, then what
   there is to decide and how long it'll take: "Week of 19–25 Oct: 11 activities across 5 subjects. To go through:
   2 new things waiting for skills and 2 level changes. About 10 minutes." Go straight into the first question
   in the same reply.
2. **One question at a time, each with your pick.** Wait for her answer before the next one. Ask in this order,
   and skip any step with nothing in it.
3. **Skills of spontaneous work first** (`waitingForSkills`). For each one, from its caption and Evidence notes,
   say what he did in a few words, propose 1–3 skills from `read_plan`, and ask "OK?". On her yes, `confirm_skills`,
   then say in a few words that it counts now ("Done; it counts for Science this week now.").
   - A retired skill (`retiredSkills`) can take the evidence when it fits best. Say so: "That's a retired skill;
     it gets the evidence but stays retired."
   - She can name other skills instead. Confirm those.
   - Confirming changes the evidence, so call `weekly_review` again before the level changes.
4. **Then level changes** (`levels`). Skip any skill whose new evidence doesn't move it. For each change you'd
   propose, name the skill and the change ("Multiplication facts: Secure → Mastered?"), list the occasions behind it
   with their dates, and say what they show. Set it with `set_level` and `in_weekly_review: true` on her yes.
   - **Mastered only when the rule is met** (`mastered.met`): "Two occasions, three weeks apart, in different
     settings. That meets the rule." When it's met but `differentSettings` is false, say so; it's still her call.
   - **When she wants Mastered and the rule isn't met**, even at the start ("also put fossils as mastered"),
     explain the rule once, then recommend: "Mastered needs two occasions, spaced in time and ideally in
     different settings, and the museum is the first. I'd set Secure now and add a check he can do on his own:
     *Sort the rock collection into how each one formed*. Or I can set Mastered now if you're sure. Your call."
     Then do what she says, without arguing. Mastered set this way is marked as set by her. A check option she
     agrees to goes in with `add_option`.
   - Lower levels need no rule. One clear occasion is plenty for Practising.
   - Don't ask about skills with no change. Mention them only at the end ("No other changes; area and reading
     stay where they are.").
5. The rest of the review (Self-Report signals, Balance, the Progress Note, recording the review) arrives with its
   ticket. For now, end with a short list of what changed (skills confirmed, levels set) and "Anything I got
   wrong?".
