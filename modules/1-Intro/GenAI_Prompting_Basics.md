# GenAI Prompting Guide: Basics and Best Practices

## Table of Contents
1. [Introduction](#introduction)
2. [Core Concepts](#core-concepts)
3. [Prompt Fundamentals](#prompt-fundamentals)
4. [Improving Your Inputs](#improving-your-inputs)
5. [Controlling Your Outputs](#controlling-your-outputs)
6. [Practical Examples](#practical-examples)
7. [Common Pitfalls and Solutions](#common-pitfalls-and-solutions)
8. [Advanced Techniques](#advanced-techniques)
9. [Quick Reference](#quick-reference)

---

## Introduction

GenAI (Generative Artificial Intelligence) models like GPT, Claude, and others have revolutionized how we work with AI. However, the quality of output you receive is **directly proportional to the quality of your input** — your prompt.

This guide covers:
- **Why prompting matters** — How it affects output quality
- **What makes prompts effective** — Clarity, context, and structure
- **How to improve inputs** — Techniques and strategies
- **How to control outputs** — Formatting, constraints, and parameters

---

## Core Concepts

### What is a Prompt?

A prompt is an instruction or question you give to a GenAI model. It's the input that guides the model to generate relevant, useful responses.

**Key characteristics:**
- Can be a single sentence or multiple paragraphs
- Can be a question, command, or scenario
- Sets expectations for tone, format, and content

### The Prompt-Response Cycle

```
Your Prompt → Model Processing → Response
     ↑                              ↓
     └──────── Feedback/Refinement ←┘
```

The model:
1. **Reads and understands** your prompt
2. **Processes** the context and task
3. **Generates** a response based on patterns in training data
4. **Returns** the output in the specified (or inferred) format

### Why Precision Matters

**Vague prompt:**
> Write about marketing

**Result:** Generic, unfocused response that might not match your needs.

**Precise prompt:**
> Write a 300-word LinkedIn post about AI automation for HR departments, targeting HR managers, in a professional but conversational tone. Include 2 specific benefits and 1 implementation tip.

**Result:** Focused, relevant, actionable content.

---

## Prompt Fundamentals

### 1. Clarity and Specificity

**Rule:** Be explicit about what you want. Don't assume the model will infer your needs.

**❌ Unclear:**
```
Tell me about Python
```

**✅ Clear:**
```
Explain the differences between Python lists and tuples, with 2 examples of when to use each.
```

### 2. Context Provision

**Rule:** Provide sufficient background information for the model to understand your domain.

**❌ Missing context:**
```
Generate a deployment strategy
```

**✅ With context:**
```
We're a SaaS company with 500 daily active users on our web platform. We currently deploy to AWS using Docker containers. Generate a zero-downtime deployment strategy for a feature release.
```

### 3. Role Definition

**Rule:** Assign a persona or expertise level to frame the response appropriately.

**Examples:**
- "You are a senior software architect with 15 years of experience..."
- "Act as a beginner-friendly Python tutor..."
- "Respond as a cybersecurity expert evaluating cloud infrastructure..."

### 4. Structure and Formatting

**Rule:** Use clear formatting to organize your thoughts.

**❌ Unstructured:**
```
I need help with a Python function that takes a list and returns the average but I also need it to handle empty lists and maybe filter out outliers
```

**✅ Structured:**
```
I need a Python function with these requirements:

**Input:**
- A list of numbers

**Functionality:**
- Calculate the average (mean)
- Handle empty lists (return None)
- Filter out values > 3 standard deviations from mean

**Output:**
- Return the filtered average as a float

**Format the code with docstring and type hints.**
```

### 5. Constraint Definition

**Rule:** Specify constraints to control scope and format.

**Examples of constraints:**
- Length: "Limit to 200 words"
- Format: "Return as JSON with keys: name, email, department"
- Tone: "Use simple, non-technical language"
- Avoid: "Do not include Python 2 syntax"

---

## Improving Your Inputs

### Technique 1: The RACE Framework

A structured approach to writing effective prompts:

**R — Role:** Who should the model act as?
**A — Action:** What should the model do?
**C — Context:** What background is needed?
**E — Examples/End-state:** What should the output look like?

**Example:**

```
**Role:** You are a data analyst with expertise in SQL and business intelligence.

**Action:** Write a SQL query to find our top 10 customers by revenue in the last 6 months.

**Context:** 
- Database: PostgreSQL
- We have tables: orders, customers, order_items
- We need to filter for enterprise customers only
- Revenue is calculated as order_items.quantity * order_items.unit_price

**End-state:** 
Return SQL code with:
- Comments explaining each part
- Proper JOIN syntax
- ORDER BY clause showing revenue descending
```

### Technique 2: Few-Shot Prompting

Provide examples of the desired output pattern to help the model understand your expectations.

**Example — Extracting sentiment:**

```
Analyze the sentiment of customer reviews. Respond ONLY with: 
{"review": "[text]", "sentiment": "[positive|neutral|negative]"}

Examples:
{"review": "Great product, works as advertised!", "sentiment": "positive"}
{"review": "It's okay, nothing special.", "sentiment": "neutral"}
{"review": "Stopped working after a week.", "sentiment": "negative"}

Now analyze this review:
"Amazing quality and fast shipping. Highly recommend!"
```

### Technique 3: Chain-of-Thought (CoT) Prompting

Ask the model to show its reasoning step-by-step. This often improves accuracy, especially for complex tasks.

**Without CoT:**
```
If a store has 50 apples and sells 30% of them, then receives 20 more, how many does it have now?
```

**With CoT:**
```
If a store has 50 apples and sells 30% of them, then receives 20 more, how many does it have now?

Think step by step:
1. Calculate how many were sold
2. Calculate remaining after sale
3. Add the new shipment
4. Give final answer
```

### Technique 4: Constrained Output Format

Specify exactly how you want the output structured.

**Examples:**

**Bullet points:**
```
List 5 best practices for cloud security:
- Practice 1
- Practice 2
... 
```

**JSON:**
```
Return as JSON:
{
  "name": "...",
  "email": "...",
  "role": "..."
}
```

**Markdown table:**
```
Create a comparison table with columns: Feature, Tool A, Tool B, Tool C
```

**Code block:**
```
Write a Python function (include function signature, docstring, and comments)
```

### Technique 5: Iterative Refinement

Your first prompt rarely produces perfect results. Refine based on responses.

**Iteration cycle:**
1. Ask initial question
2. Evaluate response
3. Provide feedback or new constraints
4. Ask refined follow-up
5. Repeat until satisfied

**Example progression:**

**Prompt 1:**
> Write marketing copy for our SaaS product

**Prompt 2 (after seeing generic response):**
> Rewrite that copy to focus on cost savings. Use data showing we save customers 40% on operations costs. Add a CTA button.

**Prompt 3 (after seeing too salesy):**
> Make it less sales-focused and more educational. Show how it works before asking for action.

---

## Controlling Your Outputs

### Output Control Mechanism 1: Format Specification

Tell the model exactly what format you want.

**Example:**

```
Summarize this article in JSON format:
{
  "title": "...",
  "main_points": ["...", "..."],
  "key_takeaway": "...",
  "word_count": ...
}
```

### Output Control Mechanism 2: Length Constraints

Be specific about length expectations.

**Examples:**
- "In 1-2 sentences..."
- "Approximately 250 words"
- "No more than 5 bullet points"
- "Limit to 100 tokens"

### Output Control Mechanism 3: Tone and Style

Define the voice and approach.

**Examples:**
```
Write this in a:
- Professional but approachable tone
- Beginner-friendly (avoid jargon)
- Conversational style (like you're talking to a friend)
- Academic tone with citations
- Creative and engaging tone
```

### Output Control Mechanism 4: Required Elements

Explicitly state what must be included.

**Example:**

```
Write a product review that includes:
- At least 2 specific features discussed
- Personal anecdote or use case
- Rating on 1-5 scale
- Recommendation for who should buy it
```

### Output Control Mechanism 5: Prohibited Elements

Tell the model what to avoid.

**Example:**

```
Explain blockchain technology:
- Do NOT use the word "crypto"
- Do NOT reference specific cryptocurrencies
- Do NOT include technical equations
- Avoid acronyms
```

### Output Control Mechanism 6: Temperature and Creativity Settings

*(When using APIs or specialized interfaces)*

- **Low temperature (0.1-0.3):** More consistent, factual, deterministic
  - Use for: Data extraction, code generation, calculations
- **Medium temperature (0.5-0.7):** Balanced
  - Use for: General questions, content creation
- **High temperature (0.8-1.0):** More creative, varied
  - Use for: Brainstorming, creative writing, idea generation

---

## Practical Examples

### Example 1: Product Description

**Scenario:** You need product descriptions for an e-commerce site.

**❌ Basic prompt:**
```
Write a product description for a wireless headphone
```

**✅ Optimized prompt:**
```
Write a 100-150 word product description for wireless headphones targeting remote workers.

Include:
- 3 specific technical features (battery life, connectivity, comfort)
- One benefit for remote workers (clear calls, focus)
- Call-to-action

Tone: Professional but approachable
Format: HTML-ready (use <p> tags)
Avoid: Generic marketing phrases like "game-changer" or "best in class"
```

**Expected output:** Well-targeted, specific, formatted description.

---

### Example 2: Code Generation

**Scenario:** You need a Python function.

**❌ Basic prompt:**
```
Write a Python function to process data
```

**✅ Optimized prompt:**
```
Write a Python function called `process_user_data` that:

**Input:** 
- users: list of dicts with keys "name" (str), "email" (str), "age" (int)

**Processing:**
- Filter out users under age 18
- Convert email to lowercase
- Remove duplicate entries (by email)

**Output:**
- Returns: list of processed user dicts

**Requirements:**
- Include type hints
- Include docstring with examples
- Handle edge cases (empty list, None values)
- Use list comprehension where appropriate
- No external libraries
```

**Expected output:** Production-ready function with documentation.

---

### Example 3: Analysis and Summary

**Scenario:** Summarize a complex research paper.

**❌ Basic prompt:**
```
Summarize this research paper [text]
```

**✅ Optimized prompt:**
```
Summarize this research paper for a business audience (non-technical).

Structure your response as:
1. **Problem Statement** (1-2 sentences): What problem does this solve?
2. **Key Findings** (3-4 bullet points): Main discoveries
3. **Business Impact** (2-3 sentences): How could a company use this?
4. **Limitations** (1-2 bullet points): Any constraints or caveats?

Avoid:
- Technical jargon (explain any you must use)
- Academic language
- Citations

Tone: Clear and actionable

[Paste research paper here]
```

**Expected output:** Business-focused, accessible summary.

---

## Common Pitfalls and Solutions

| Pitfall | Problem | Solution |
|---------|---------|----------|
| **Too vague** | Model guesses at your intent | Add specific details and examples |
| **Insufficient context** | Response is generic or off-target | Explain the "why" and background |
| **No format specified** | Output format is unusable | Request specific format (JSON, markdown, code, etc.) |
| **Contradictory constraints** | Model can't satisfy both requirements | Prioritize constraints or rethink them |
| **Too many requirements** | Model loses track of all needs | Break into multiple prompts if needed |
| **Unclear success criteria** | Hard to evaluate if response is good | Define what "good" looks like upfront |
| **No examples given** | Model interpretation differs from yours | Provide 1-3 examples of desired output |
| **Assuming common knowledge** | Model includes irrelevant details | Specify exactly what background is needed |

---

## Advanced Techniques

### Technique 1: Prompt Chaining

Break complex tasks into multiple prompts, using output from one as input to the next.

**Example:** Blog post creation
1. **Prompt 1:** Generate 5 blog post title ideas
2. **Prompt 2:** Choose best title, generate outline
3. **Prompt 3:** Write first draft from outline
4. **Prompt 4:** Revise for SEO and engagement
5. **Prompt 5:** Generate social media snippets

### Technique 2: System Prompts vs. User Prompts

**System prompt:** Sets overall behavior and guardrails (if using APIs)
```
You are a helpful customer service representative. Be friendly, professional, 
and solve problems efficiently. If you can't answer, escalate politely.
```

**User prompt:** The actual request
```
A customer is upset that their order hasn't arrived. Address their concern.
```

### Technique 3: Zero-Shot vs. Few-Shot Learning

**Zero-shot:** No examples provided
```
Translate "Hello" to Spanish
```

**Few-shot:** Examples provided
```
Translate these words to Spanish:
- Cat → Gato
- Dog → Perro
- House → Casa

Now translate: Bird →
```

Few-shot typically produces better results for complex tasks.

### Technique 4: Temperature-Based Creativity Control

Adjust randomness in model response (where available):
- **Facts/Data:** Use low temperature
- **Creative writing:** Use high temperature
- **Balanced tasks:** Use medium temperature

### Technique 5: Using "Persona" Effectively

Don't just assign a title—give context:

**Weak:**
```
Act as a JavaScript expert.
```

**Strong:**
```
You are a senior JavaScript engineer with 10 years of experience, specializing in 
React and Node.js. You prioritize clean, maintainable code with excellent performance.
```

---

## Quick Reference

### Essential Prompt Components Checklist

- [ ] **Clear task/question:** What exactly do you want?
- [ ] **Role/context:** What background does the model need?
- [ ] **Format specification:** How should output be structured?
- [ ] **Length/constraints:** Any limits or requirements?
- [ ] **Tone/style:** What voice or approach?
- [ ] **Examples:** Any sample outputs to guide the model?
- [ ] **Success criteria:** How will you know if it's good?

### Prompt Template

```
**Role:** [Who should the model act as?]

**Task:** [What exactly should be done?]

**Context:** [Background information needed]

**Format:** [How should output be structured?]

**Constraints:**
- Length: [word count or similar]
- Tone: [professional, casual, etc.]
- Must include: [required elements]
- Avoid: [prohibited elements]

**Examples:**
[Provide 1-3 examples of good output]

**Input/Content:**
[Provide the actual content to process]
```

### Refinement Template

When first attempt isn't perfect:

```
[Previous response]

That's close, but please adjust:
1. [Specific feedback point 1]
2. [Specific feedback point 2]
3. [What to add/remove/change]

Try again focusing on [key aspect].
```

---

## Key Takeaways

1. **Clarity is everything** — Vague prompts get vague results
2. **Context matters** — The more relevant background, the better
3. **Format guides output** — Specify structure to get usable results
4. **Iterate and refine** — Rarely perfect on first try
5. **Examples help** — Few-shot prompting improves consistency
6. **Test and verify** — Always validate output quality
7. **Different tasks need different approaches** — Adjust technique to the problem

---

## Practice Exercises

1. **Write a basic prompt** for summarizing a news article
2. **Improve it** by adding constraints, format, and tone
3. **Add examples** showing what good output looks like
4. **Refine further** with specific required elements
5. **Create a persona** that would produce better results

---

## Resources and Further Reading

- OpenAI Prompt Engineering Guide
- Anthropic Claude Documentation
- Hugging Face Prompting Guide
- DeepLearning.AI Short Courses

---

*Last updated: 2026-06-14*
*For questions or improvements, contribute to the documentation.*
