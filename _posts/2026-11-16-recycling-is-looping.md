---
layout: article
title: "Recycling is Looping: From Protein Folding to LLMs"
description: "How AlphaFold's recycling reappears as recurrent depth in language models."
date: 2026-11-16
math: true
tags:
  - Language Models
  - Model Architecture
  - Protein Folding
---

Deep learning runs on a handful of simple ideas that scale with data and compute. And because these methods share a common language of networks, ideas that work for board games or proteins can often be carried over to text. Reasoning models are one example. They bring AlphaZero's recipe to LLMs: spend extra compute at inference and use reinforcement learning to expand states, backtrack, etc.

Looping is another of these ideas. Looped transformers reuse the same layers several times to buy depth without adding parameters. [AlphaFold 2](https://www.nature.com/articles/s41586-021-03819-2) used a version of this in 2021 under another name: recycling. Now that looping has reached frontier language models, recycling looks less like a protein-folding trick and more like a general principle that was already lying around: spend extra compute by running the same network again on its own output.

The two paradigms differ in where the thinking happens. Reasoning thinks out loud, in tokens, by writing a chain of thought. Looping thinks silently, in the latent space, by refining a representation. Combining the two seems to stack their benefits.

## Recycling: looping the whole network

AlphaFold 2 runs its full network, 48 Evoformer blocks plus the structure module, then feeds its own output back in and runs the same weights again. Four passes is the default, so 48 blocks of parameters give 192 blocks of effective depth.

<figure>
  <img src="{{ '/images/alphafold-recycling.svg' | relative_url }}" alt="AlphaFold 2 runs its network, then recycles its output into the input for another pass.">
  <figcaption>AlphaFold 2 reuses the same network on a refined input.</figcaption>
</figure>

The pair representation and first MSA row are layer-normalized; the predicted structure is turned into a binned distance map. All three are added to the input embeddings.

## Looping for LLMs

In September 2026, The Information reported that OpenAI's Astra uses recurrent depth: the same block runs several times on a token's hidden state before the next token is produced. OpenAI's chief scientist Jakub Pachocki [responded](https://x.com/merettm/status/2095023204993490967) that the depth of the computation graph of their frontier models, including Astra, is within a factor of two of GPT-4.

> "…including Astra, is within a factor of two of GPT-4."
>
> **Jakub Pachocki** (@merettm), OpenAI chief scientist · [view on X](https://x.com/merettm/status/2095023204993490967)

He did not deny the looping, he merely gave a bound. Weeks later, a [Microsoft Foundry page](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/introducing-gpt-6-1-sol-in-microsoft-foundry-advanced-intelligence-optimized-for/4560811) described GPT-6.1 Sol as using the same base weights as GPT-6 Sol with two inference passes instead of three, which many read as fewer loops.

None of this is confirmed architecture, and frontier labs publish few details. But the picture is consistent: a few loops per token, run inside the model rather than written out as text. That is exactly the shape of AlphaFold's recycling, which defaults to four passes.

[Geiping et al. (2025)](https://arxiv.org/abs/2502.05171) offer one public version of the idea. A prelude of 2 layers embeds the input, a core block of 4 layers is looped, and a coda of 2 layers reads out the next token.

<figure>
  <img src="{{ '/images/recurrent-depth-loop.svg' | relative_url }}" alt="A recurrent-depth model passes the hidden state through the same core block repeatedly, mixing in the original embedding at each loop.">
  <figcaption>A recurrent-depth language model loops the core block before producing a token.</figcaption>
</figure>

Each loop mixes the input embedding back in with the previous state. In AlphaFold:

$$
x = e + \mathrm{LayerNorm}(h_{\mathrm{prev}})
$$

In the recurrent-depth model:

$$
s_i = R\big(A\,[\,e\,;\,s_{i-1}\,]\big)
$$

AlphaFold adds the recycled state to the embedding. The recurrent-depth model concatenates the two and lets a learned matrix A mix them. Either way, every pass sees both the original input and its own latest draft.

The training recipes are strikingly close:

|  | AlphaFold 2 recycling | Recurrent depth |
| --- | --- | --- |
| Loops in training | Random, 1 to 4 | Random, mean 32 (log-normal Poisson) |
| Gradients | Only through the last pass | Only through the last 8 loops |
| Start state | Zeros | Random noise |
| At test time | More recycles for hard targets | More loops for harder tasks |

Crucially, the loop runs within one token. The model refines the same position before emitting it, just as AlphaFold refines the same protein before outputting a structure.

## Results

The authors write that recycling contributes markedly to accuracy with only minor extra training time. Their Figure 4 shows where that accuracy comes from.

[View the AlphaFold 2 ablations in Figure 4a](https://www.nature.com/articles/s41586-021-03819-2/figures/4).

*AlphaFold 2 ablations ([Jumper et al. 2021](https://www.nature.com/articles/s41586-021-03819-2), Fig. 4a).* Removing recycling costs roughly 3 to 5 GDT on CASP14 domains and about 2 lDDT-Cα on PDB chains.

Easy proteins barely use the loop and hard ones depend on it. Geiping et al. find the same in language: easy benchmarks converge in few loops, math keeps improving with more, and the model scales up to compute equivalent to a 50B-parameter model from 3.5B parameters.

[See Tables 1 and 4 in Geiping et al. (2025)](https://arxiv.org/abs/2502.05171) for the reported benchmark results.

## Conclusion

Recycling is one of deep learning's simple, reusable ideas: run the same network again on its own output, and let hard inputs take more passes than easy ones. AlphaFold showed it worked in 2021; language models picked it up years later, after adapting it to the new domain.
