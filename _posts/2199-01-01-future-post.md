---
title: 'Future Blog Post'
date: 2199-01-01
permalink: /posts/2012/08/blog-post-4/
tags:
  - RL
  - Thoughts
---

# How confident are you, ChatGPT?

**TL;DR:** I present reason to doubt that the key to OpenAI’s IMO Gold was a universal verifier. Instead, I argue that uncertainty estimation and calibration are central to this research direction and likely to shape future OpenAI products.

Recently, both OpenAI and DeepMind entered their models in the IMO 2025 and achieved gold medals by correctly solving problems 1 through 5. Problem 6 remained unsolved by both models. Interestingly, the solutions were written in informal natural language, not in formal systems like Lean. The latter approach was adopted by Harmonic [Gold](https://harmonic.fun/news) and Bytedance [Silver](https://seed.bytedance.com/en/blog/bytedance-seed-prover-achieves-silver-medal-score-in-imo-2025) and has an important advantage: while formal languages offer verifiability via compilers, informal reasoning risks hallucination. Yet, the fact that OpenAI and DeepMind produced correct solutions— later verified by human experts—highlights something very important: progress in supervising tasks that are hard to verify.

Noam Brown (one of the three OpenAI employees who worked on the IMO project) said in an [interview with Sequoia’s Sonya Huang](https://www.youtube.com/watch?v=EEIPtofVe2Q&list=PLOhHNjZItNnMm5tdW61JpnyxeYH5NDDx8):

“We observed progress on hard-to-verify tasks, which was a departure from our previous focus on verifiable rewards, and this improvement is what excited us.[...]
Initially, when language models came out, the challenge was getting them to reason. **Once they could reason, the next challenge was getting them to reason on hard-to-verify tasks.** Now that they can reason on hard-to-verify tasks, I think the next hurdle will be getting them to come up with novel questions.”

Some speculated that OpenAI built a [universal verifier](https://www.theinformation.com/articles/universal-verifiers-openais-secret-weapon) — an LLM capable of judging outputs across domains. But such verifiers are imperfect, just like the proving model itself. This opens the door to reward hacking: the model learns to fool the verifier rather than solve the problem.

Lean on the other hand is the example of a limited but perfect verifier: it works for mathematics and requires the model to use a formal language, but the resulting reward signal is always correct.

In the following article I will present arguments which instead of a universal verifier, but will put a technique called **calibration** into the focus.

Calibration refers to how well a model’s predicted confidence score match the actual likelihood of being correct. A well-calibrated model that says it's 80% confident should be right about 80% of the time. Overconfidence on the other hand means outputting an answer with high confidence that is actually wrong. **Hallucination** is a result of overconfident models. Researchers from FAIR at Meta found that [reasoning models trained with RL particularly tend to become overconfident after RL training](https://openreview.net/pdf?id=kYbojsAOBj).

The idea for the calibration hypothesis first came from this [X post](https://x.com/alexwei_/status/1947461238512095718?s=46) by Alexander Wei:

![Alexander Wei's post on X](images\Alexander_Wei_X_Post.png)

And actually after listening through the podcast again, it seems that **uncertainty is all over the conversation** (and also in the GPT5 launch, more later)!

“We allocated significant computational resources to problem six, but it was encouraging to see that **the model didn't attempt to fabricate a solution and instead acknowledged its inability to solve it**... **This level of self-awareness in the model is remarkable**, especially considering that earlier models would often try to be helpful by generating incorrect answers.”

“[...] Although it still can't solve the problem, **it now recognizes its inability to do so**, which I consider a significant improvement.”

“[...] **One of the intriguing aspects of these models is their ability to express uncertainty or confidence in natural language throughout the problem-solving process** [...] You often encounter the dreaded 'seems hard' response. That occurred on problem six. **The model frequently expressed difficulty.** It would respond with phrases like 'No progress,' 'Hard,' 'Seems hard,' and 'Keep going.'”

Here we can see strong evidence against the universal verifier theory, because it does not seem that the model has access to a verifier, but instead **the verification was absorbed into the model itself.**

## RL for Uncertainty Training

My hypothesis is that the team saw that the model initially showed a promising ability to estimate its own confidence in its reasoning, which led the team to explore ways to bring out this behavior in postraining with RL. This involved developing a novel RL setup: rewarding the model for correct answers with high confidence, and penalizing it when it confidently produces incorrect responses.  [A recent paper by MIT researchers] (https://www.arxiv.org/pdf/2507.16806) explores such an RL calibration approach in more detail. This training then likely encouraged the model to engage in deeper reasoning, developing an implicit internal verifier to assess uncertainty which explains why before finalizing an answer.

# Parallel Thinking and Multi-Agent Systems

Another crucial factor in solving the IMO for both OpenAI and DeepMind was scaling up reasoning through parallel computation. This was particularly important as both teams aimed to solve problems under the same 4.5-hour time constraint as human contestants. However, since models can run multiple processes simultaneously, comparing against human time is somewhat misleading—what truly matters is the total compute used, a detail neither team disclosed.
On the matter of parallel thinking DeepMind highlighted this in their [statement](https://deepmind.google/discover/blog/advanced-version-of-gemini-with-deep-think-officially-achieves-gold-medal-standard-at-the-international-mathematical-olympiad/):

“We achieved this year’s result using an advanced version of Gemini Deep Think [..] that incorporates some of our latest research techniques, including parallel thinking. This setup enables the model to simultaneously explore and combine multiple possible solutions before giving a final answer, rather than pursuing a single, linear chain of thought.”

OpenAI, on the other hand, emphasized the role of multi-agent systems:
“I believe both of you are on the multi-agent team. Please help me understand the role that multi-agent systems play in this process.”
“In addition to having the model think for extended periods and make progress on difficult-to-verify tasks, this also involved scaling up parallel compute, which has a multi-agent component.
 While we cannot go into too much detail about the exact techniques, this was certainly one way we were able to scale up test-time compute for the IMO.
 Regarding the multi-agent and parallel compute scaling, we prioritized generality in our techniques.”

The challenge with parallelization is to avoid overconfident hallucinations from multiple agents. Without proper calibration, this makes it difficult to select the correct answer. But with the method of confidence training we mentioned it, the model would instead either withhold an answer until it's sure, or output a confidence score that helps rank candidate solutions—enabling better use of parallel compute by choosing the highest-confidence result.

### Speculations:
More advanced setups may use a Manager–Worker architecture: one agent proposes diverse proof strategies which are then distributed to workers for development. This encourages exploration and reduces duplication between workers. In a video by DeepMind the mathematician Michel van Garrel with access to the model states:
“When I was thinking about solving that question, I was thinking about three different things, three different ideas, but it seems that that DeepThink was thinking about 20 or 100.”

In OpenAI's case, model behavior suggests a modular strategy: problems are broken into lemmas, which are solved independently. Agents could then share proven subparts, allowing others to compose a full proof (see DeepMind’s comment on “combining multiple possible solutions.”)
![Excerpt from OpenAIs problem 1 proof](images\lemma_openai_problem_1.png)

## GPT 5 Release 

Finally, I believe that this is a major direction that OpenAI will push for. In the GPT5 release they made hallucinations and reliability in domains such as healthcare very important. Customers want a model which they can rely on does not claim to have solved a problem if it hasn’t.

