# Broadcastwell Audit Method

This is the method Broadcastwell uses to measure whether AI search engines name a company when a buyer asks for the best software in that company's category.

It is published so that anyone receiving a Broadcastwell audit can check how the numbers were produced, and so that anyone else can reproduce the measurement independently.

## This is not the study

Broadcastwell publishes two different things and they use different methods. Keeping them straight matters.

| | The 2026 State of GEO (study) | Client audit (this document) |
|---|---|---|
| Purpose | Research across a market | Measurement for one company |
| Engines | One, held constant | Four |
| Engine used | Anthropic Claude Sonnet with live web search | Claude, OpenAI, Perplexity, Google AI Overviews |
| Scale | 860 answers, 85 companies, 61 categories | 40 answers per company |
| Why | Holding the engine constant keeps results comparable across categories. A four-engine study at that scale would require 3,440 runs. | Buyers use different engines. A single engine is not enough to advise one company. |
| Published at | [github.com/Broadcastwell/state-of-geo-2026](https://github.com/Broadcastwell/state-of-geo-2026) | this repository |

The study's DOI covers the study only. It does not cover this method.

## What gets measured

For a single company, in a single named category, the audit produces three numbers:

1. Named — in how many answers the company's brand appears
2. Cited — in how many answers the company's own domain appears as a source
3. Named instead — which competitors appeared, and how often

## The method

### 1. Question generation

Ten buyer questions are generated for the category before the company's own site is reviewed, so the question set is not shaped to favour the company being measured.

The ten cover a fixed mix:

- 3 category questions ("best X for Y")
- 2 alternatives questions ("alternatives to X")
- 2 head-to-head comparisons ("X vs Y")
- 2 use-case questions
- 1 pricing or evaluation question

The company's own name is never included in a question.

### 2. The four engines

The same ten questions, worded identically, are put to four engines.

| Engine | Endpoint | Retrieval |
|---|---|---|
| Claude | api.anthropic.com/v1/messages | web_search tool, live |
| OpenAI | api.openai.com/v1/responses | web_search tool, live |
| Perplexity | api.perplexity.ai/chat/completions | sonar model family, live by default |
| Google AI Overviews | SerpApi google engine, plus a second google_ai_overview call when the first returns only a page token | Live Google results |

Ten questions across four engines is forty scored answers per company.

On naming. "OpenAI" here means the OpenAI API with web search enabled. That is not the same product as the consumer ChatGPT application and may return different answers. Google has no official AI Overviews API; SerpApi is a third-party scraper, and not every query returns an overview.

### 3. Scoring

Each of the forty answers is scored on two binary outcomes.

Named. The brand string is matched on word boundaries, not as a substring, so a company called Pitch does not score a hit on the ordinary word "pitch". Brands that are a single plain alphabetic word are matched case-sensitively for the same reason. Brands containing a dot, digit, hyphen or space are unambiguous and matched case-insensitively.

Cited. Every URL the engine returned as a source is parsed to a hostname and compared against the company's domain. Subdomains of the company's domain count. A different domain that merely contains the company's domain as a substring does not.

Competitor names supplied with the request are matched the same way.

### 4. Failures are excluded, not counted as misses

A call that fails after three retries, or a Google query that returns no AI Overview, is recorded with an error and removed from the denominator. A company is reported as 0 of 39 rather than a misleading 0 of 40.

### 5. Aggregation

- A question counts as a miss only if the brand was absent from every engine.
- Questions won on some engines and lost on others are reported separately as partial visibility.
- Per-engine counts are always reported alongside the total, because engines disagree.

## Limitations, stated plainly

- Run-to-run variance is real. The same question asked twice minutes apart can return a different leader. Broadcastwell has observed this directly. Any single audit is a point-in-time reading, not a fixed score.
- Forty answers is a small sample. Differences of one or two answers between months should not be read as movement.
- Google AI Overviews depends on a third-party scraper, and not every query returns an overview.
- The OpenAI API is not consumer ChatGPT.
- Broadcastwell wrote the questions. They are written to a fixed structural mix, before reviewing the company, but they are not drawn from observed buyer search data.

## Reproducing this

Anyone with API access to the four engines can reproduce the measurement from the description above. There is nothing proprietary in it.

## Contact

Broadcastwell, Bloomington, Indiana

https://broadcastwell.com
