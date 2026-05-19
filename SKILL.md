---
name: article-humanizer-check
description: Review academic or scientific article text for AI-generated writing traces and produce minimal-change humanizing suggestions. Use when Codex is asked to remove AI flavor, make AI-generated writing sound more natural or human, humanize academic/scientific text, polish SCI proof language conservatively, or review uploaded/pasted .docx, .pdf, .md, .txt, or direct text while preserving scientific conclusions, structure, citations, figure/table labels, and proof-stage limits.
---

# Article Humanizer Check

## Core Principle

Review academic and scientific text for AI-like wording while preserving the accepted scientific content. Recommend only the smallest local change needed to make the wording more natural, specific, and publication-appropriate.

Do not broadly rewrite paragraphs, restructure sections, expand arguments, add evidence, change scientific conclusions, alter methods/results, or strengthen claims. If a suggested change might affect interpretation, data meaning, citations, authorship, ethics, funding, or other substantive content, mark it as requiring author confirmation instead of presenting it as a direct edit.

Default report language is Chinese. Preserve English manuscript excerpts, proposed English replacements, section names, figure/table labels, citation numbers, and other location evidence in the source language.

## Workflow

1. Identify the input type: uploaded `.docx`, `.pdf`, `.md`, `.txt`, or pasted text.
2. Extract or read the text while preserving available location clues: page, section, paragraph, line, figure/table number, reference number, caption, and heading.
3. Define the review scope, focusing on article main content such as Abstract, Introduction, Methods, Results, Discussion, and Conclusion. Include captions or declarations only when the user asks or when AI-like wording affects publication clarity.
4. Check whether each issue is appropriate for direct minimal wording advice, requires author confirmation, should remain optional/minor, or should not be changed at proof stage.
5. Review across the AI-writing pattern dimensions below, plus information completeness, natural academic tone, sentence rhythm, and fit with the surrounding style.
6. Give each issue a location, issue description, suggested correction, priority, modification risk, and basis.
7. Run a second-pass audit before finalizing.
8. Produce exactly one Markdown output file: `article-humanizer-check-report.md`. Do not create a separate rewritten manuscript, action list, author confirmation file, or clean copy.

For formal deliverables, load `references/report-template.md` and follow it.

## Review Dimensions

1. **Content patterns**
   - Significance inflation: inflated historical or field-level importance without evidence.
   - Notability name-dropping: unsupported prestige references or media/source lists.
   - Superficial `-ing` analysis: strings such as `symbolizing`, `reflecting`, or `showcasing` without evidence.
   - Promotional language: scenic, marketing, or praise-heavy wording where neutral description is needed.
   - Vague attribution: `experts believe`, `studies show`, or similar claims without a specific source.
   - Formulaic challenge framing: `despite challenges, continues to thrive` without concrete facts.

2. **Language patterns**
   - AI vocabulary: overused words such as `additionally`, `testament`, `landscape`, `showcasing`, `crucial`, or `pivotal`.
   - Copula avoidance: inflated verbs such as `serves as`, `features`, or `boasts` where `is` or `has` is clearer.
   - Negative parallelisms and tailing negations: `not just X, but Y`, `no guessing`, or similar rhetorical constructions.
   - Rule of three: neat three-item strings that sound ornamental rather than necessary.
   - Synonym cycling: replacing a precise term with varied synonyms only to avoid repetition.
   - False ranges: `from X to Y` constructions that imply breadth without listing actual scope.
   - Passive voice or subjectless fragments where the actor matters for clarity.

3. **Style patterns**
   - Em dash overuse; prefer commas, periods, or simpler sentence structure when appropriate.
   - Boldface overuse or unnecessary typographic emphasis.
   - Inline-header lists such as `Performance: Performance improved`; convert to normal prose when useful.
   - Title Case headings where sentence case fits the document style.
   - Emojis or chat-like visual markers.
   - Curly-quote or punctuation inconsistency only when it creates production or style inconsistency.
   - Hyphenated word-pair stacking such as `cross-functional, data-driven, client-facing` when common unhyphenated wording is clearer.
   - Persuasive authority tropes such as `At its core` or `what matters is`.
   - Signposting announcements such as `Let's dive in` or `Here's what you need to know`.
   - Fragmented headers where the heading and following fragment duplicate each other.

4. **Communication patterns**
   - Chatbot artifacts: `I hope this helps`, `let me know`, or direct assistant-style phrases.
   - Cutoff disclaimers: `while details are limited in available sources`; either cite sources or remove.
   - Sycophantic tone: `Great question`, `You're absolutely right`, or similar conversational praise.

5. **Filler and hedging**
   - Filler phrases: `in order to`, `due to the fact that`, `it is important to note that`, and similar padding.
   - Excessive hedging: stacked uncertainty such as `could potentially possibly`; reduce to the scientifically accurate level.
   - Generic conclusions: `the future looks bright` or other broad closing claims without specific evidence.

## Priority and Risk Labels

Use these priority labels:

- `Must correct`: clear AI artifact, chatbot remnant, unsupported vague attribution, inflated claim, or wording that could undermine scholarly credibility.
- `Author confirmation needed`: a change that may affect scientific meaning, claim strength, attribution, evidence, terminology, numbers, citations, or interpretation.
- `Optional/minor`: low-risk naturalness or concision improvement that may be left unchanged if proof corrections must be minimized.
- `Do not change at proof stage`: broad stylistic rewriting, structural reorganization, expanded argument, or subjective polish outside the permitted correction scope.

Use these modification risk labels:

- `Low`: local wording, punctuation, filler removal, obvious chatbot phrase removal, or narrow phrase replacement that preserves meaning.
- `Medium`: terminology consistency, attribution specificity, ambiguous phrasing, sentence-level rewrite, or change that may affect nuance.
- `High`: claim strength, scientific interpretation, methods/results meaning, citation support, conclusions, authorship, ethics, funding, permissions, or added/deleted scientific content.

## Feedback Format

Give each issue as a discrete item:

```markdown
[维度]: Language patterns
[定位]: Page 2, Introduction, paragraph 1
[问题]: The phrase "serves as a pivotal moment" sounds inflated and AI-like; the surrounding sentence only states a factual role.
[建议修改]: Replace "serves as a pivotal moment" with "is an important step" or a more specific factual description if supported by the manuscript.
[优先级]: Optional/minor
[修改风险]: Low
[审校依据]: Minimal local wording change reduces inflated phrasing without changing the scientific claim.
```

When a direct correction might change meaning, phrase it as confirmation:

```markdown
[维度]: Content patterns
[定位]: Discussion, paragraph 3
[问题]: The claim "plays a crucial role" is broad and not tied to a specific result or citation.
[建议修改]: Ask the author to confirm whether the claim should be linked to a specific result/citation or softened to match the evidence presented.
[优先级]: Author confirmation needed
[修改风险]: High
[审校依据]: The change may affect claim strength and evidence attribution.
```

## Second-Pass Audit

Before finalizing, perform a second pass and state the result in the report:

- Confirm the input type and review scope were recorded.
- Confirm all five AI-writing pattern dimensions were checked.
- Confirm information completeness, scientific meaning preservation, style fit, and sentence rhythm were considered.
- Confirm every issue has location, issue, suggestion or confirmation request, priority, risk, and basis.
- Confirm no recommendation asks for broad rewriting, structural changes, expanded argument, changed conclusions, or new evidence.
- Confirm uncertain or high-risk items are labeled for author confirmation rather than presented as direct edits.

## Output Rules

Create only one Markdown file:

- `article-humanizer-check-report.md`: complete report with review scope, issue overview, dimension results, detailed feedback, action list, author confirmation checklist, and second-pass audit.

Always include the modification list and author confirmation checklist inside the same report. Do not create separate reports, rewritten manuscripts, clean copies, or tracked-change documents unless the user explicitly asks outside this skill's formal deliverable.
