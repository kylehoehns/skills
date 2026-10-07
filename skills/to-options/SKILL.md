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

1. **Sort the design tree.** Work from the grilling in this conversation. If there wasn't one, call the Skill tool with "grilling" first.

   Keep grilling's design tree, frontier and fact-finding, and ask one question per turn in place of its rounds: through your multiple-choice question tool (or that question's options as a numbered list when you have none), with your recommended option first and **Defer** last. Defer means someone other than the user makes this call.

   Put every question in exactly one pile:
   - **Decided**: the user settled it. It goes on the page as context, never as a question.
   - **Fact**: something the environment can answer. Look it up yourself, and call it a fact only when you can point at its source: the ticket line, the file, the vendor doc. A fact the ticket only implies is an open question.
   - **Open**: a trade-off the business cares about, owned by someone other than the user. Every deferred question lands here, and the questions that hang off it become its downstream questions, left unasked. For each of its options, note what that option leaves open: any number or name it needs, and the downstream questions it unlocks.

   An open question the user could settle alone isn't for the page: ask it now, the same way. Done when every question from the grilling sits in one pile, every fact cites its source, every open question names its decider by role, and every option's open points come from the grilling.

2. **Ask about the send.** In one exchange, confirm the deciders, and for each question that changes a screen, which application and screen it lives in. Lead with your recommended answer so the user can accept it in a word. Done when every open question has a decider, and every screen question has a home screen or the user said it has none.

3. **Pick the smallest view.** For each open question, choose the **smallest view** that makes its options look different, then give every option the same kind of view so they compare at a glance:
   - **It changes a screen**: read [UI.md](UI.md).
   - **It isn't UI** (an API, a data flow, a job, a report, a message): read [VIEWS.md](VIEWS.md).

   Every view gets one plain sentence above it saying what it shows, and keeps only the calls, fields and states that tell the options apart. Done when every option of every open question has its view, no question mixes kinds of view, and in the question's scenario no two options' views look the same.

4. **Build the page.** Write one self-contained HTML file from the template below. Open it at phone and laptop width (with a browser tool when you have one) and fix anything that overflows or clips. Publish it and give the user the link. Done when every open question from step 1 has a tab, you have seen every tab fit at both widths, and after one pick per tab the reply lists every question with its pick.

5. **Reshape.** The user will merge, split, cut and re-route questions. Rerun whichever steps the change touches and republish to the same path.

<page-template>

**Start here** tab guides the decider into the questions. Above the fold sits only:

- The effort's name.
- The **problem statement**: what's wrong today and who it hurts, in two sentences. Then one sentence on what this effort changes.
- One card per open question: the question, one line on why it needs deciding, and a link to its tab.

Below the fold, the decided list, so nobody reopens it.

Then one tab per open question:

- **The question**, in the decider's words.
- **The scenario**: one concrete moment with real-looking data, the same for every option, picked so each option gives a different result.
- **The options**, side by side. Each one gets a name, one line saying what it means, its view, and two or three bullets on what it costs. Where the user has a lean, tag that option "the team's lean". Each card ends on a **Pick** button that highlights the card. A picked card opens a note box labelled with what that option leaves open: any number or name it needs ("how often should it refresh?") and the downstream questions it unlocks. A card with nothing open labels it "Anything to add?".
- **Not sure yet**: one button under the options, for a decider who wants to talk it through.
- **What we checked**: the facts this question rests on, each with its source. A question with no facts goes without it.

Last, the **Your reply** tab, its label counting questions answered, **Not sure yet** included ("2/3"). It holds the decider's **reply**: an editable box drafted from every pick and note, redrawn whenever one changes, and a **Copy reply** button. The reply takes this shape:

```
<effort name>: my picks

1. <question tab name>: A (<option name>)
   <note>
2. <question tab name>: not sure yet, want to talk it through
3. <question tab name>: no pick yet
```

Picks and notes persist in the decider's browser. When the browser blocks copying, select the box's text and tell the decider to copy it by hand.

</page-template>

## Rules

- Name every person by role: "the owner", "the second in line", "the practice manager". Real names stay out, even when the ticket or the data has them.
- The page speaks to every decider alike. Who decides what is the user's send list, so no card, tab or header names a question's decider.
- Let labels carry the how-to: "Pick B", "Copy reply" and "Not sure yet" are the instructions, so the page spends its words on the options.
- Write in the decider's words. Labels inside a view stay real; the sentence above the view translates.
- Offer only options the user would build.
- Picks stay in the decider's browser, so the page works for anyone with the link.
