---
name: check-against-sources
description: >
  Check a draft against the person's own source documents with PortMem, and answer from those documents with the
  passage behind each statement. Use when the person asks to check, verify, fact-check or review a memo, summary or
  report against their documents ("check this draft against my documents", "is this memo right", "what does it
  leave out"); asks what their documents say ("what does the credit agreement say about default", "the key dates
  in the bond terms"); wants to choose or add the documents for a check; or asks about an earlier review ("show my
  last review", "which findings are still open", "who signed this off").
---

# Check work against the source documents

PortMem checks a draft against the documents it relies on, and keeps a record of what it found and what a person
decided. This skill is the method for using PortMem's tools well. PortMem does the checking: report what it
returns, and keep any view of your own apart from it.

An explicit instruction from the person comes before this skill. If they ask for another format, another level of
detail or another order of steps, do as they ask.

## Beside a PortMem card, two sentences

Some apps draw PortMem's review, its record of who decided what, its list of documents or its upload form as a card
in the conversation. The note that comes with the result says when one is on the person's screen. Then the card is
the answer, and this rule comes before everything below:

- Write at most two sentences beside a card. When one answer has two cards, at most two sentences for each.
- Say what PortMem found, as counts, or what the person does next in the card, and that the card shows the rest.
- Write no heading, list or table, and quote or restate no finding.
- Add no link: the card carries the links to the console and to the audit trail.
- Offer no next step and no revision unless the person asked for one. Ask a question only when the next step
  cannot start without the answer, as when the draft is not in the conversation yet.

Where no card is drawn, the rest of this skill says what to report. A terminal or command-line session draws no
card, whatever a note says: there, never tell the person to look at a card, and list what PortMem returned.

## Before starting

- If PortMem's tools are not available in this conversation, say so and ask the person to connect PortMem and sign
  in. Never check a draft from memory and present the answer as PortMem's.
- Work from the person's documents in PortMem and nothing else. To find a document's exact name, call
  `list_sources`: it is a lookup for you, not a list to write out.
- The person connected PortMem to have its tools used. Call the tool each step names, and let the app ask the
  person for approval when it wants to. Never skip a step, and never write a step's result yourself, because a
  tool might need approval.

## Check a draft

1. Get the whole draft. PortMem checks exactly the text it is sent, so pass the draft complete and word for word as
   `document`: never a summary, and never only the part that seems to matter. If the draft is not in the
   conversation, ask for it.
2. Settle which documents it is checked against.
   - The person named them: pass those names, `source` for one document, `sources` for several with the
     controlling one first.
   - The person wants to see, choose or rank their documents: call `choose_documents` and wait. Their choice comes
     back as a message naming the documents. Use exactly those names. Pass `source_levels` only when the person
     gave the ranking.
   - Neither: start the review without naming documents and PortMem picks the ones the draft is about. The result
     names them in `documents_picked`: tell the person which documents were used.
3. Call `start_review`, then call `review_status` with the `job_id` until the review has finished. A review takes
   up to a few minutes. Say nothing about findings before it has finished.
4. Call `show_review` with the review's `request_id`, every time a review finishes and without being asked
   again: it is how the person sees the result. Writing the findings out yourself does not replace this step.
5. Say what PortMem found in one or two sentences, as counts, from the result's `summary`. Then follow the note
   that comes with the result, which says whether PortMem's review view is on the person's screen:
   - The view is on screen: the person reads every finding there with its source passage. Point to the view and
     stop, as "Beside a PortMem card, two sentences" says.
   - No view is drawn, as in a terminal: list the findings as PortMem gives them, each with the source passage that
     decides it.

## Read the result honestly

- A material provision the draft leaves out is a finding like a wrong statement. Report it with the same weight.
- Use PortMem's own word for each verdict. "Supported" means the passage PortMem cites supports that statement. It
  is not an approval of the document.
- Never call a draft verified, approved or signed off because a review came back clean. Say what PortMem checked,
  against which documents, and what it found.
- Keep PortMem's findings apart from your own suggestions, and say which is which. Add no finding of your own to
  PortMem's list, and do not drop or soften one.
- Do not count again. When the result carries counts (`summary`, `trail`), give those numbers as they are.
- Give names, dates and times from PortMem's records as written.

## Fix the draft and check again

- Revise the draft only when the person asks.
- Mark each change that comes from a finding where it is made in the revised document, with a comment or a
  highlight naming the finding, not only in a list at the end. When you can edit the person's file, mark it in the
  file.
- When you have revised the draft, offer to review the revision: `start_review` with `prior_request_id` set to
  the earlier review's `request_id`, so the result shows which findings are resolved. Call a finding resolved only
  when that result says so.

## Answer from the documents

- For a question about what the documents say, call `search`. Narrow it with `source` or `sources` when the person
  named documents.
- For one whole document (its parties, key dates and amounts, and its material provisions), call `survey_source`.
  The first survey of a long document can take a few minutes: when the result says "preparing", ask again.
- Give each answer with the passage it rests on and the name of the document. When the documents do not say it,
  say that plainly. Mark anything from general knowledge as not from the documents.

## Add documents

- When the person wants to add or upload documents, call `add_documents`: whole files go straight to PortMem.
- When the person attached the file and this app passes files to tools, call `upload_file` with the file itself.
  When commands can be run on the person's computer, call `request_upload` and run the command it returns with the
  file's real path.
- A source document goes in complete, word for word: never a summary, an excerpt or one section. PortMem checks a
  draft only against the text it has.
- Never add the draft being checked as a source document.

## Earlier reviews and the record

- To open an earlier review, call `past_reviews`, then `show_review` with its `request_id` or its PM reference
  (PM-XXXX-XXXX-XXXX).
- For which findings were accepted and which are still open, or who ran, signed off, approved, returned or
  published a document, and when, call `record_history`. Tell it as PortMem recorded it. A person can only sign a
  finding off (accept it as it stands) or take that back: never say a finding was rejected, denied or fixed unless
  its outcome says so.
- For a summary, a log or an audit trail of what PortMem caught on a report, give PortMem's own audit trail: the
  `trail_url` in the review's result. Do not build such a page from the report or from memory.

## What stays with the person

Accepting a flagged claim, publishing a record and changing who can see a document are decisions the person makes
in the PortMem console. When the person asks for one of them, say it is theirs to do there and give the
`console_url` from the result. Never present one of these as done from the conversation.
