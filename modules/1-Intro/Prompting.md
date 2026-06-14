
# Introduction

Everybody is used to 'googleing' something, whether it's "What is the weather today?" or "Why is Brazil no longer a powerhouse in football ahem.. soccer?". 

The search engine checks it's index of the web and provides ranked results based on the question.

At a 30k level, prompting is the same thing, except instead of a search engine, you are asking a large language model (LLM) to provide an answer. The LLM has been trained on a massive amount of data, and it predicts and formulates an answer based on the input prompt.

The key difference is that the LLM is not just providing a list of links to web pages, but is generating relevant response (mainly) based on its training data. The input can be supplemented with context from more current data for the LLM to be able to generate a more accurate response, but that's another story.

# Prompting


The quality of the output of a prompt depends on a lot of factors, some of which can be easily controlled by the user. *We will focus on some of these options.

### INPUT PROMPT TIPS

* Be precise: The more specific your prompt, the better is the response.

* Provide context: If your prompt is ambiguous, the LLM may not understand what you are asking for. Providing context can help the LLM generate a more accurate response.

* Use examples: If you want the LLM to generate a specific type of response, providing examples can help it understand what you are looking for.

* Assign a role: If you want the LLM to generate a response from a specific perspective, assigning a role can help it understand the context and generate a more relevant response.

* Use structure: If you want the LLM to generate a response in a specific format, using structure can help it understand how to organize the information.

* Define constraints: If you want the LLM to generate a response within certain constraints, defining those constraints can help it understand what is acceptable and what is not.

### Techniques to improve the input prompt

#### RACE FRAMEWORK
1. *Role*: Defines the AI’s persona, expertise, or perspective (e.g., “Act as a senior financial analyst”).
2. *Action*: Specifies exactly what the AI needs to do (e.g., “Draft an executive summary of this quarterly report”).
3. *Context*: Provides the necessary background, audience, constraints, or unique situation.
4. *Execute* (or Expectation/Format): Dictates the final output structure, tone, and delivery style (e.g., “Format the output as a table with bullet points, keep it under 500 words”).

#### Zero-Shot Prompting
Zero-shot prompting is a technique where you provide the LLM with a prompt that does not include any examples or context. This can be useful when you want to test the LLM's ability to generate a response based solely on its training data. For example, if you want the LLM to generate a creative story, you can provide a simple prompt like "Write a story about a dragon and a knight" and see how the LLM responds without any additional guidance.

#### Few-Shot Prompting
Few-shot prompting is a technique where you provide the LLM with a few examples of the desired output along with the input prompt. This helps the LLM understand the format and style of the response you are looking for. For example, if you want the LLM to generate a summary of a news article, you can provide a few examples of summaries along with the article to help the LLM

#### Chain-of-Thought Prompting
Chain-of-thought prompting is a technique where you encourage the LLM to generate a step-by-step explanation of its reasoning process. This can help the LLM arrive at a more accurate and coherent response, especially for complex tasks. For example, if you want the LLM to solve a math problem, you can prompt it to explain its reasoning process step by step, which can lead to a more accurate solution.

#### Prompt Chaining
Prompt chaining is a technique where you break down a complex task into smaller, more manageable prompts. This can help the LLM generate a more accurate and coherent response by allowing it to focus on one aspect of the task at a time. For example, if you want the LLM to generate a detailed report on a specific topic, you can break it down into smaller prompts such as "Provide an overview of the topic", "List the key points", and "Summarize the findings". This can help the LLM generate a more comprehensive and well-structured report. 

#### Iterative Prompting
Iterative prompting is a technique where you provide feedback on the LLM's response and ask it to refine its answer based on that feedback. This can help the LLM improve the quality of its response over multiple iterations. For example, if you ask the LLM to generate a summary of a news article and it provides a response that is too long, you can provide feedback such as "Please make the summary more concise and focus on the main points" and ask it to generate a revised summary. This iterative process can help the LLM generate a more accurate and relevant response over time.