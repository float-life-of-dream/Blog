---
date: 2026-04-24
authors:
  - liyao
title: Code Review Best Practices I've Learned
slug: code-review-best-practices
description: >
  Practical tips for giving and receiving code reviews that are constructive, efficient, and drama-free.
categories:
  - Software Engineering
---

# Code Review Best Practices I've Learned

After years of reviewing code (and having my code reviewed), here are the practices that make reviews productive instead of painful.

## As a Reviewer

### 1. Review the Diff, Not the Developer

Focus on the code, not the person who wrote it. Use neutral language:

| Bad | Good |
|-----|------|
| "You forgot to handle the error" | "What happens when `response` is `null`?" |
| "This is wrong" | "I think this might miss the edge case where..." |

### 2. Start with What You Like

Pointing out good patterns reinforces them. A quick "Nice use of `defaultdict` here" builds rapport.

### 3. Distinguish Nitpicks from Blockers

Use labels to set expectations:

- **[blocker]** — must fix before merge
- **[nit]** — stylistic preference, merge at author's discretion
- **[question]** — I don't understand, please explain

### 4. Don't Review for More Than 60 Minutes

After an hour, your attention drifts. Take a break and come back.

## As an Author

### 1. Small PRs Win

A 200-line PR gets reviewed fast. A 2000-line PR sits for a week. Break big changes into reviewable chunks.

### 2. Self-Review First

Before requesting review, go through your own diff. You'll catch half the issues yourself.

### 3. Write a Good Description

```
## What
Add retry logic to the payment API client.

## Why
Intermittent network errors were causing ~2% of payment requests to fail.
This adds exponential backoff retry (3 attempts, max 10s).

## Test Plan
- [x] Unit tests for retry count
- [x] Integration test with mock server returning 500s
- [x] Manual test in staging
```

### 4. Don't Take Feedback Personally

Reviews are about making the product better, not about you. If you feel defensive, step away for 10 minutes before responding.

## TL;DR

Keep PRs small, reviews respectful, and communication clear. Code review is a conversation, not a gate.

---

*What are your code review pet peeves?*
