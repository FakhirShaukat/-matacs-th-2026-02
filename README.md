AI Proposal Triage: Design Submission

- Name: Fakhir Shaukat 
- Reference: MATACS-TH-2026-02 
- Role: Associate Software Developer 
- Time actually spent:  2 days 4 hours

## What this is

A system design for a tool that helps a facilities team triage contractor proposals. A reviewer uploads proposals and picks a category. The system returns a ranked list with a reason for each position. A person makes the final award decision.

The core idea: AI reads, code decides, humans approve.

- AI pulls facts (with exact quotes) out of messy proposal text, and rates the one criterion that needs judgment (Team and approach).
- Code runs the mandatory pass/fail gates, calculates the numeric scores, ranks, and builds the reasons.
- Humans resolve every flag, can override with a written note, and make the award decision.

Criteria are never hard-coded. They are loaded from the admin configuration and saved as a versioned snapshot with every run.

## Files in this repository:

[WRITEUP.md]: Answers to the five questions (AI vs. rules, consistency, human in the loop, changing criteria, risks) 
[diagram/flowchart.png]: Process flow from upload to ranked output, showing AI steps, rule-based steps and human checkpoints 

[PROMPTS.md]: The extraction prompt and the Team and approach rating prompt, as they would be sent |
[ranking.json]: Expected result for proposals A to E

There is no `prototype/` folder. I chose to spend the time on the design and reasoning instead.

## How I used AI tools:
- I've first define a role to the model so that the AI could not get out of the context and generate something else. 
- I used Claude in a step-by-step conversation to plan the design, draft the process diagram, the prompts, the scoring approach. I reviewed each step before moving on and kept the final choices as my own.
- I've asked questions regarding any misunderstanding of the project's scope to ensure model is working on the same phase.


## Where I disagreed with or corrected the AI: 
In the system flow processes, I disagreed with claude's design at this specific point:
"AI, rating only Team and approach from 0 to 5 against a rubric, because that is the one criterion that needs reading judgment."

I was not sure why AI is also handling the teams and approach rating so I asked claude by giving this prompt:
"Tell me one thing. in the above detail, why AI is rating the teams and aproach on its own. suppose to the reviewer, they have sended their team certificates as they are certified workers or the reviewers recieves a call from the project lead or manager after sending their proposal that Im the head and all. Is'nt that concerning ?"

And the output I got was actually logical:

## OUTPUT:
It’s a fair concern, and the answer has two parts: what the AI can see, and what a person should do about outside information.

## What the AI is actually doing

The AI doesn’t judge the team on its own authority. It reads only what the proposal says (a named lead, a stated crew size, a safety plan, a monitoring plan) and picks a draft score from a rubric a human wrote. It is rating how complete and specific the written plan is. It is not verifying that the claims are true. Two limits keep it in check:

Notes:

- All proposals are referred to by letter (A to E). No brief or proposal text is copied into this repository.
- No code is included, so there are no API keys. If a prototype is added later, keys go in a `.env.example` file and are never committed.
