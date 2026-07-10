# Agastya School ERP

A full school ERP system with an AI-powered chatbot, built as a single static HTML file. No backend, no framework, no build step -- drag and drop to deploy.

## Live Demo

**[agastyaassignment.netlify.app](https://agastyaassignment.netlify.app)**

## Features

- **Dashboard** -- live fee collection stats, collection rate, attendance overview, per-student term status
- **Student directory** -- search by name or roll number, filter by class, section, and gender
- **Student detail view** -- full profile, fee history, marks by exam, recent attendance
- **Fees** -- all payment records, filter by status and term, running totals
- **Marks** -- performance grid across 4 exams, grade badges, click through to student detail
- **Attendance** -- summary with 75% threshold flagging, filter by class and status
- **Ask Agastya (chatbot)** -- SQL-first query engine, LLM layer for reasoning and policy questions
- **Pipeline Inspector** -- live animated RAG architecture demo with real Groq API call at stage 4

## Chatbot Architecture

Every message goes through a 4-layer routing pipeline before any response is generated:

```
User message
   -> Greeting check         (instant pre-written response)
   -> Policy/reasoning check (LLM layer: criteria, explain, suggest, why, compare)
   -> SQL engine             (structured queries: fees, marks, attendance, filters)
   -> LLM fallback           (anything the parser cannot resolve)
```

The SQL engine handles all structured queries directly from in-memory data -- zero API calls for fees, marks, attendance lookups, count queries, multi-filter combinations, and named student lookups. LLM is reserved for reasoning, policy, and advice questions only.

## Dataset

185 students across 6 classes (Class 8A, 8B, 9A, 9B, 10A, 10B) with realistic distributions:

- 555 fee records across 3 terms at Rs.6,500 per term
- 3,700 mark records across 5 subjects and 4 exams
- 11,840 attendance records across 90 school days
- Payment rates vary by class (realistic unpaid distribution)
- Attendance drawn from a normal distribution per student

Source: adapted from Kaggle Student Performance Dataset (CC0). Financial data modelled since no public school fee dataset exists for obvious privacy reasons.

## Tech Stack

- Pure HTML, CSS, and JavaScript -- no framework, no build tool
- In-memory data engine (SQL-equivalent filter/aggregate logic)
- Lucide icons (MIT)
- Groq Llama 3 70B via Groq API (pipeline inspector stage 4 only)
- Deployed on Netlify (static, single file)

## Run Locally

```bash
# No setup needed
open index.html
```

Or just drag `index.html` into any browser tab.

## Query Examples

```
What are Ishan Gupta fees?
How many students in class 10 have unpaid fees?
How many female students in class 9 and 10?
Students with attendance between 60% and 70% in class 9
Average attendance of class 8?
Top performers in mid term in class 9?
What is the attendance criteria students have to fulfill?
Suggest a fee reminder strategy
Compare class 8 and 9 attendance
```

## Author

Rajrishi Kashyap
[linkedin.com/in/rajrishikashyap](https://linkedin.com/in/rajrishikashyap) | [github.com/rajrishikashyap](https://github.com/rajrishikashyap)
