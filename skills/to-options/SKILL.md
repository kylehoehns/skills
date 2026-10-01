---
name: to-options
description: Turn the questions a grilling couldn't settle into one page that shows each answer side by side, for the people who decide.
disable-model-invocation: true
metadata:
  credits:
    skill: show-me
    author: Dex Horthy
    organisation: Humanlayer
    url: "https://github.com/humanlayer/skills/blob/main/plugins/show-me/skills/show-me/SKILL.md"
---

Turn the questions a grilling couldn't settle into an **options page**: one HTML page the user hands to each **decider**, the person who owns a call the user can't make. A decider struggles to answer a question in the abstract. Shown what each answer would give them, they can make the call more easily.

**Show the answer, not the question.** Every open question becomes what someone would actually get under each option: the screen, the API response, the text message, the rows. The decider reacts to that, never to the transcript.

1. **Sort the design tree.** Work from the grilling in this conversation. If there wasn't one, call the Skill tool with "grilling" first. Put every question in exactly one pile:
   - **Decided**: the user settled it. It goes on the page as context, never as a question.
   - **Fact**: something the environment can answer. Look it up yourself, and call it a fact only when you can point at its source: the ticket line, the file, the vendor doc. A fact the ticket only implies is an open question.
   - **Open**: a trade-off the business cares about, owned by someone other than the user.

   An open question the user could settle alone isn't for the page: ask the user now. Done when every question from the grilling sits in one pile, every fact cites its source, and every open question names its decider by role.

2. **Ask about the send.** In one exchange, confirm the deciders, and for each question that changes a screen, which application and screen it lives in. Lead with your recommended answer so the user can accept it in a word. Done when every open question has a decider, and every screen question has a home screen or the user said it has none.

3. **Pick the smallest view.** For each open question, choose the **smallest view** that makes its options look different, then give every option the same kind of view so they compare at a glance:
   - **It changes a screen**: read [UI.md](UI.md).
   - **It isn't UI** (an API, a data flow, a job, a report): read [VIEWS.md](VIEWS.md).

   Every view gets one plain sentence above it saying what it shows, and keeps only the calls, fields and states that tell the options apart. Done when every option of every open question has its view, and no question mixes kinds of view.

4. **Build the page.** Write one self-contained HTML file from the template below, publish it, and give the user the link. Done when every open question from step 1 has a tab, and the page reads cleanly at phone and laptop widths.

5. **Reshape.** The user will merge, split, cut and re-route questions. Rerun whichever steps the change touches and republish to the same path.

<page-template>

**Start here** tab: what the effort is, in two sentences. How to read the page. A table of open questions and who decides each. The facts, each with its source. The decided list, so nobody reopens it.

Then one tab per open question:

- **The question**, in the decider's words, and the decider's role.
- **The scenario**: one concrete moment with real-looking data, the same for every option.
- **The options**, side by side. Each one gets a name, one line saying what it means, its view, and two or three bullets on what it costs. Tag the user's lean only where they have one.
- **The pick**: one line saying exactly what to choose, plus any number or name the choice needs ("pick A or B; if A, how often it refreshes").
- **Downstream questions** sit under the question they depend on, labelled with the answer that unlocks them ("only if B").

</page-template>

## Rules

- Name every person by role: "the owner", "the second in line", "the practice manager". Real names stay out, even when the ticket or the data has them.
- Write in the decider's words. Labels inside a view stay real; the sentence above the view translates.
- Offer only options the user would build.
- The page starts a conversation. Answers come back in the meeting, so the page collects nothing.
