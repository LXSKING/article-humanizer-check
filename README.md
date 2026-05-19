# Article Humanizer Check

[中文](#中文) | [English](#english)

## 中文

### 简介

`article-humanizer-check` 是一个用于检查学术文章、SCI 论文 proof 或正文中 AI 生成痕迹的 Codex Skill。它会识别过度模板化、宣传化、空泛化或 chatbot 式的表达，并给出局部、低干预的修改建议。

该 Skill 的目标不是生成整篇改写稿，而是在不改变科学结论、不重构段落、不扩展论证的前提下，让文本更自然、更克制、更像人类学术写作。

### 适用场景

- 检查 AI 辅助写作后的论文段落是否有明显 AI 痕迹。
- 检查 Abstract、Introduction、Discussion、Conclusion 中的套路化表达。
- 对 SCI proof 或终稿进行低风险语言自然度检查。
- 去除 chatbot 残留、夸大语气、含糊归因、过度 hedging 和模板化转折。
- 在 proof 阶段判断哪些语言问题可以直接建议修改，哪些需要作者确认。

### 核心原则

- 最小必要修改。
- 不做大幅重写。
- 不改变科学结论。
- 不扩展论证。
- 不重构文章结构。
- 不新增证据、引用、结果或解释。
- 可能影响科学含义、claim strength、数据解释、引用支持或术语准确性的建议，必须标记为作者确认项。

### 支持输入

- 上传的 `.docx` proof 文件
- 上传的 `.pdf` proof 文件
- 上传的 `.md` 或 `.txt` 文本
- 直接粘贴到对话中的段落、章节或全文

### 审校维度

1. **Content patterns**：检查意义夸大、名人/媒体堆砌、空泛分析、宣传式语言、含糊归因和模板化挑战叙述。
2. **Language patterns**：检查 AI 高频词、copula avoidance、negative parallelism、rule of three、synonym cycling、false ranges 和不必要的无主句。
3. **Style patterns**：检查破折号滥用、粗体滥用、inline-header lists、Title Case headings、emoji、连字符堆叠和提示词式开场。
4. **Communication patterns**：检查 chatbot artifact、cutoff disclaimer、sycophantic tone 等对话式痕迹。
5. **Filler and hedging**：检查填充短语、过度缓和和空泛结论。

### 优先级与风险标签

优先级：

- `Must correct`：明显 AI artifact、chatbot 残留、无依据的含糊归因、夸大表达或影响学术可信度的问题。
- `Author confirmation needed`：可能影响科学含义、claim strength、数据解释、术语、引用或证据支持的问题。
- `Optional/minor`：低风险自然度、简洁性或局部语气改进。
- `Do not change at proof stage`：proof 阶段不适合进行的大幅风格改写、结构调整或扩展论证。

修改风险：

- `Low`：局部词语替换、标点、删除填充词、删除明显 chatbot 残留。
- `Medium`：术语一致性、归因具体化、句意歧义、句子级改写或语气细微变化。
- `High`：科学解释、结论强度、Methods/Results 含义、引用支持、伦理基金、作者信息或新增/删除科学内容。

### 输出文件

正式交付始终只生成一个 Markdown 报告：

```text
article-humanizer-check-report.md
```

报告默认使用中文。英文 manuscript excerpts、suggested replacement wording、page/section/paragraph locations、figure/table/citation labels、proper names、statistical notation 和 journal-specific terms 保留原文。

报告应包含审校范围、问题总览、维度检查结果、逐条反馈、修改清单、作者确认清单和二次核查。不要额外生成 clean copy、rewritten manuscript、tracked-change document 或单独的 action list。

### 使用示例

```text
Use $article-humanizer-check to review this Introduction section for AI-like wording. Please follow the minimal-change principle and output only article-humanizer-check-report.md.
```

```text
请使用 $article-humanizer-check 检查这篇 SCI proof 中的 AI 写作痕迹。请不要整段重写，只给出局部修改建议，并将可能影响科学含义的问题列为作者确认项。
```

```text
Use $article-humanizer-check to check whether this Discussion section contains inflated claims, vague attributions, formulaic transitions, or excessive hedging.
```

### 文件结构

```text
article-humanizer-check/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    └── report-template.md
```

- `SKILL.md`：Skill 的正式触发说明和执行规则。
- `references/report-template.md`：正式 Markdown 报告模板。
- `agents/openai.yaml`：Codex UI 元数据和默认调用提示。

## English

### Overview

`article-humanizer-check` is a Codex Skill for reviewing academic or scientific article text for traces of AI-generated writing. It identifies formulaic, promotional, vague, over-polished, or chatbot-like wording and provides localized, low-intervention suggestions.

The Skill is not intended to produce a fully rewritten manuscript. Its purpose is to make the text sound more natural and publication-appropriate while preserving scientific conclusions, paragraph structure, argument scope, citations, figure/table labels, and proof-stage limits.

### Use Cases

- Check AI-assisted academic writing for visible AI traces.
- Review Abstract, Introduction, Discussion, and Conclusion sections for formulaic phrasing.
- Perform conservative language-naturalness checks on SCI proofs or near-final manuscripts.
- Remove chatbot artifacts, inflated language, vague attribution, excessive hedging, and template-like transitions.
- Decide which wording issues can be suggested directly and which require author confirmation.

### Core Principles

- Make only the smallest necessary change.
- Do not broadly rewrite paragraphs.
- Do not change scientific conclusions.
- Do not expand the argument.
- Do not restructure the manuscript.
- Do not add evidence, citations, results, or interpretations.
- Mark any suggestion that may affect scientific meaning, claim strength, data interpretation, citation support, or terminology accuracy as requiring author confirmation.

### Supported Inputs

- Uploaded `.docx` proof files
- Uploaded `.pdf` proof files
- Uploaded `.md` or `.txt` text
- Pasted paragraphs, sections, or full article text

### Review Dimensions

1. **Content patterns**: significance inflation, name-dropping, superficial analysis, promotional language, vague attribution, and formulaic challenge framing.
2. **Language patterns**: AI vocabulary, copula avoidance, negative parallelisms, rule of three, synonym cycling, false ranges, and unnecessary subjectless fragments.
3. **Style patterns**: em dash overuse, boldface overuse, inline-header lists, Title Case headings, emojis, hyphenated word-pair stacking, and prompt-like signposting.
4. **Communication patterns**: chatbot artifacts, cutoff disclaimers, and sycophantic tone.
5. **Filler and hedging**: filler phrases, excessive hedging, and generic conclusions.

### Priority and Risk Labels

Priority labels:

- `Must correct`: clear AI artifacts, chatbot remnants, unsupported vague attribution, inflated claims, or wording that undermines scholarly credibility.
- `Author confirmation needed`: issues that may affect scientific meaning, claim strength, data interpretation, terminology, citations, or evidence support.
- `Optional/minor`: low-risk naturalness, concision, or local tone improvements.
- `Do not change at proof stage`: broad stylistic rewriting, structural changes, or expanded argumentation that is inappropriate at proof stage.

Modification risk labels:

- `Low`: local wording, punctuation, filler removal, or obvious chatbot artifact removal.
- `Medium`: terminology consistency, attribution specificity, ambiguity, sentence-level rewriting, or subtle tone changes.
- `High`: scientific interpretation, conclusion strength, Methods/Results meaning, citation support, ethics/funding, author metadata, or added/deleted scientific content.

### Output File

Formal delivery always creates one Markdown report:

```text
article-humanizer-check-report.md
```

The report is Chinese by default. English manuscript excerpts, suggested replacement wording, page/section/paragraph locations, figure/table/citation labels, proper names, statistical notation, and journal-specific terms should remain in the source language.

The report should include review scope, issue overview, dimension results, detailed feedback, modification list, author confirmation checklist, and second-pass audit. Do not create a separate clean copy, rewritten manuscript, tracked-change document, or action list.

### Example Prompts

```text
Use $article-humanizer-check to review this Introduction section for AI-like wording. Please follow the minimal-change principle and output only article-humanizer-check-report.md.
```

```text
Use $article-humanizer-check to check this SCI proof for AI-generated writing traces. Do not rewrite whole paragraphs; provide localized suggestions only and list meaning-sensitive issues as author confirmation items.
```

```text
Use $article-humanizer-check to check whether this Discussion section contains inflated claims, vague attributions, formulaic transitions, or excessive hedging.
```

### File Layout

```text
article-humanizer-check/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    └── report-template.md
```

- `SKILL.md`: official Skill trigger description and execution rules.
- `references/report-template.md`: formal Markdown report template.
- `agents/openai.yaml`: Codex UI metadata and default prompt.
