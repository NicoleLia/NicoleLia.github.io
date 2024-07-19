---
permalink: /human-preferences
title: ''
excerpt: ''
author_profile: true
redirect_from:
---

[Training Language Models to Follow Instructions with Human Feedback (2022/OPENAI)](https://proceedings.neurips.cc/paper_files/paper/2022/file/b1efde53be364a73914f58805a001731-Paper-Conference.pdf)

- Purpose: Many LLMs are biased towards predicting the next token rather than creating an alignment between the user's intention and the language model, resulting in LLMs that do not match the human intention. This article aims to optimize this problem.
- Contributions:
  - Labelers significantly prefer InstructGPT outputs over outputs from GPT-3. (Outputs from our 175B InstructGPT are preferred to 175B GPT-3 outputs 85 ± 3% of the time, and preferred 71 ± 4% of the time to few-shot 175B GPT-3.).
  - InstructGPT models show improvements in truthfulness over GPT-3 (a 21% vs. 41% hallucination rate, respectively).
  - InstructGPT models generate about 25% fewer toxic outputs than GPT-3 when prompted to be respectful.
- Tech:
  - Step 1: Fine-tune the model using cues written by the annotator and submitted via the language model API and SFT (supervised fine tuning).
  - Step 2: Train the reward model - the same SFT but with the last layer replaced. The input is prompt, but the output is a scalar reward - using only 6b parameters.
  - Step 3: Train the reinforcement learning PPO-ptx model with the reward model, then iterate with Step 2.
- Weaknesses
  - Human-based feedback is influenced by the context of different people, but they are not representative of all users.
  - They are not fully aligned and secure and still produce some toxic and biased outputs, etc.
  - InstructGPT produces more toxic output than a GPT-3 model of the same size when the cued model has maximum bias.
