# Broadcastwell Audit Method

This is the method Broadcastwell uses to measure whether AI search engines name a company when a buyer asks for the best software in that company's category.

It is published so that anyone receiving a Broadcastwell measurement can check how the numbers were produced, and so that anyone else can reproduce the measurement independently.

The authoritative, versioned statement of this method is published at https://broadcastwell.com/methodology. This repository restates it. Where the two ever disagree, the methodology page is correct.

## This is not the study

Broadcastwell publishes two different things and they use different methods. Keeping them straight matters.

| | The 2026 State of GEO (study) | Client measurement (this document) |
|-|-|-|
| Purpose | Research across a market | Measurement for one company |
| Engines | One, held constant | Four |
| Engines used | One engine, held constant, stated in the study | ChatGPT, Claude, Perplexity, Google AI Overviews |
| Scale | 860 answers, 85 companies, 61 categories | 120 observed answers per Diagnostic |
| Why | Holding the engine constant keeps results comparable across categories. | Buyers use different engines. A single engine is not enough to advise one company. |
| Published at | [github.com/Broadcastwell/state-of-geo-2026](https://github.com/Broadcastwell/state-of-geo-2026) | this repository |

Research figures and client figures are reported separately and never combined.

The study's DOI covers the study only. It does not cover this method.

## What gets measured

Four outcomes are recorded for every observed answer. They are reported separately and are never combined into a single score.

1. Mention. The brand is named in the answer text. An answer counts once for a brand it names, however many times it names it.
2. Citation. The brand's own domain appears among the sources the answer cited. A citation and a mention are separate outcomes, and an answer can do either without the other.
3. Recommendation position. Where the brand falls when an answer returns an ordered or grouped shortlist. Recorded only when the answer has a discernible order. Otherwise the report says: no discernible order in this answer.
4. Competitor named. A rival from the list agreed before the run appears in the answer text, scored by the same rule as a mention.

No composite visibility score is produced. Mentions, citations and position move for different reasons and at different speeds, and adding them together hides which of the three actually moved.

Sentiment is not measured. The measurement records presence, not tone. The answer text is delivered in full so the description can be read directly.

## The method

### 1. The question set

A Diagnostic asks ten questions, written for the category and agreed with the client before the run, then frozen in wording.

No question names the client. Three of the ten ask for alternatives to a named incumbent and two compare named rivals, following Appendix A of the Absence Manual.

A question that already contains a name hands the answer that name, so an answer repeating it measures the question rather than the engine's choice. Questions that name a rival are reported as separate figures with the class stated, never blended into one headline number.

A reworded question is a different question. If a question set changes, that opens a new baseline rather than continuing the old one.

### 2. The four engines

The same ten questions, worded identically, are put to four engine products in the same run: ChatGPT, Claude, Perplexity and Google AI Overviews.

The automation that runs the queries, the endpoints, the model version strings and any third party involved in collection are implementation rather than method, and are not published. Reports name the engine, not the model string. Nothing in the implementation changes whether a figure is true.

### 3. Repetition

A single run is not evidence. Engines are not deterministic, and the same question asked an hour later can return a different list.

The current configuration is ten buyer questions, four engines, and three documented repeat runs of every question on every engine. Ten multiplied by four multiplied by three is 120 observed answers per Diagnostic.

Every observation is retained, including the ones that disagree with the others, and the run to run spread is reported alongside the rate rather than averaged away.

### 4. Scoring rules

The rules below decide what counts. They are applied the same way to a win and to a loss.

Brand matching is on word boundaries. A brand counts as named when the answer contains the brand as a whole word, matched case-sensitively for a single plain alphabetic word, so a company called Pitch does not score a hit on the ordinary word "pitch". Brands containing a dot, digit, hyphen or space are unambiguous and matched case-insensitively.

Domain matching compares hostnames. A citation counts when a cited source resolves to the brand's hostname. Subdomains of that hostname count. A different domain that merely contains the brand's domain as a substring does not.

Failed responses leave the denominator. When an engine returns nothing, errors, or refuses, that observation is excluded from the denominator and is never scored as a miss. Every exclusion is listed with its reason in the delivered data.

Floors are labelled as floors. Where a figure is a minimum rather than an exact count, it is labelled a minimum rather than presented as an exact number with a caveat elsewhere.

### 5. Uncertainty

Every rate is a sample, not a census. A rate published without a range is not evidence.

Every headline figure is published with its sample size and a 95 percent confidence interval, calculated with the Wilson score interval for a binomial proportion. Wilson is used rather than the normal approximation because it stays sensible at small samples and at rates near zero, which is where a first baseline usually sits.

A change between two runs that sits inside both intervals is not reported as movement. It is reported as a figure that did not separate from the previous one, with both intervals shown.

This is also why the controlled four-engine re-score is quarterly rather than monthly. A monthly re-score on a sample this size would spend most of its life reporting movement that cannot be distinguished from noise.

### 6. Aggregation

- A question counts as a miss only if the brand was absent from every engine on every repeat.
- Questions won on some engines and lost on others are reported separately as partial visibility.
- Per-engine counts are always reported alongside the total, because engines disagree.

## Limitations, stated plainly

- Run to run variance is real. The same question asked twice minutes apart can return a different leader. Broadcastwell has observed this directly, which is why every question and engine pair is run three times.
- 120 observed answers is a sample. Differences that sit inside both confidence intervals should not be read as movement.
- Google AI Overviews does not return an overview for every query, and those observations are excluded rather than scored as misses.
- Broadcastwell writes the questions. They follow a fixed structural mix, agreed before the run, but they are not drawn from observed buyer search data.
- The measurement records whether an engine names a brand. It does not establish why, and no engine outcome is guaranteed.

## What the client receives

Every observed answer as the engine returned it, with the engine, the date and time it ran, and every source it cited. Wins and losses alike, including every observation excluded from a denominator and the reason it was excluded. No reported figure is one a client cannot trace back to the answers underneath it.

Client baselines, findings, question sets and outcomes are never published without written permission.

## Reproducing this

Anyone with access to the four engine products can reproduce the measurement from the description above. There is nothing proprietary in it.

## Related

- The versioned method: https://broadcastwell.com/methodology
- What a Diagnostic measures, and what it cannot tell you: https://broadcastwell.com/ai-visibility-audit
- The free mini-audit, ten buyer questions and one named engine: https://audit.broadcastwell.com
- The Absence Manual: https://docs.broadcastwell.com

## Contact

Broadcastwell, Bloomington, Indiana

https://broadcastwell.com
