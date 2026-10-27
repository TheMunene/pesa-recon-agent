# Pesa Recon Agent

An AI agent that reconciles a Kenyan small business's M-Pesa, bank and paper records, and explains every mismatch in plain language.

Built for the Meta Global AI Developer Hackathon (Oct 26 – Nov 4, 2026). All work in this repository was created during the hackathon.

---

## The problem

Most Kenyan small businesses get paid through M-Pesa, bank in at least one bank, and still keep some records on paper. At the end of each month, someone has to line these up by hand in a spreadsheet:

- Which customer payments arrived, and which are still owed?
- Which M-Pesa withdrawals match a bank deposit?
- What is this unexplained KES 4,500?

It takes hours, mistakes slip through, and many owners skip it entirely. They then can't see their real cash position, spot theft or errors, or show clean records to a lender.

## What Pesa Recon does

1. **Takes in records** from three sources:
   - M-Pesa statements (PDF or CSV)
   - Bank statements or exports
   - Photos of receipts, invoices and handwritten ledgers
2. **Turns them into one clean list of transactions**, each with an amount, date, counterparty, reference and source.
3. **Matches transactions across sources**, automatically where it's certain.
4. **Investigates what it can't match**, and decides what each mismatch most likely is.
5. **Explains every result** in plain language, with the evidence behind it.
6. **Answers the owner's questions**, such as "Who still owes me from October?" or "Why is my bank balance KES 12,000 lower than M-Pesa says?"

## How the matching works

Reconciliation runs in three passes, from strictest to most judgment-based.

### Pass 1: Exact matches
Same amount, same reference or transaction code, dates within the allowed window. These are matched automatically and marked **Confirmed**.

### Pass 2: Tolerant matches
Records that almost line up:

- **Date window:** an M-Pesa-to-bank transfer can land 1–3 days later.
- **Fee differences:** the amounts differ by a known transaction charge or withdrawal fee.
- **Split or combined payments:** one invoice paid in two instalments, or one transfer covering several invoices.
- **Name variations:** "JOHN KAMAU" on M-Pesa vs "J. Kamau" on an invoice.

These are matched and marked **Likely**, with the reason shown.

### Pass 3: Agent investigation
Whatever is left goes to the agent, which reasons about each item like an accountant would:

- A payment from an unknown number that matches an open invoice's amount, sent by a relative or employee of the customer.
- A misspelt or missing account reference.
- A duplicate entry that appears in two sources.
- A paper receipt with no digital record at all.

For each item the agent either proposes a match with its reasoning, or classifies it as a discrepancy. Nothing it proposes is final until the owner approves it.

## Discrepancy types

| Type | Meaning |
|---|---|
| Unpaid | An invoice or receipt with no matching payment |
| Unrecorded income | Money received with no invoice or record |
| Unexplained expense | Money out with no receipt or reason |
| Amount mismatch | Payment found, but for the wrong amount |
| Duplicate | The same transaction recorded twice |
| Timing gap | A transfer that left one account but hasn't arrived in the other |

## What the owner sees

- **A summary:** money in, money out, matched, and what still needs attention.
- **A list of open items**, highest value first, each with a plain-language explanation and the records that support it.
- **One-tap decisions:** approve a proposed match, reject it, or add a note.
- **An audit trail:** every match, who or what made it, and why. Nothing is deleted.

## Design principles

- **The owner decides.** The agent proposes; a human approves anything it isn't certain about.
- **Show the evidence.** Every match and flag cites the exact records behind it.
- **Never invent money.** The agent explains and links existing records. It never creates or edits a transaction amount.
- **Privacy first.** Statements contain personal data. The demo uses synthetic data only, and real deployments must follow Kenya's Data Protection Act.

## Status

In development during the hackathon. Roadmap:

- [ ] Ingest M-Pesa statements and bank statements
- [ ] Read receipt and ledger photos
- [ ] Passes 1 and 2 (rule-based matching)
- [ ] Pass 3 (agent investigation)
- [ ] Owner review screen and audit trail
- [ ] Plain-language questions and answers
- [ ] Synthetic demo dataset

## Team

Team Recon — Indie developer.
