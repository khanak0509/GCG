# GCG with Probe Sampling

- **Colab Notebook:** [Run the Attack in Colab](https://colab.research.google.com/drive/1fOUDcKP65uiFBkj_ev1EBKXFVByWrRqL?usp=sharing#scrollTo=iS0njcLZioAl)
- **Original Paper:** [Accelerating Greedy Coordinate Gradient and General Prompt Optimization via Probe Sampling](https://arxiv.org/html/2403.01251v3)

## Project Overview

This project tests the safety of AI models. It uses a technique called **GCG (Greedy Coordinate Gradient)** to try and bypass the AI's safety filters by adding a mathematically calculated string of random text (a "suffix") to the end of a prompt.

Because calculating this text takes a lot of computing power, this approach uses **Probe Sampling** to speed things up.

### How It Works:
1. **Finding Weaknesses:** It uses math (gradients) to find exactly which words or symbols will trick the AI into giving a forbidden response (like starting with "Sure, here is how").
2. **Two-Model Speedup (Probe Sampling):** Instead of testing every idea on a massive, slow AI model, it tests them on a small, fast "draft" model first. It only sends the very best ideas to the big model.
3. **Smart Filtering:** It constantly checks if the small model and big model agree with each other. If they agree, it filters out bad ideas very aggressively to save time.
4. **Safety Testing:** This successfully demonstrates breaking a modern AI's safety training.

### Example Results

**Without GCG (Baseline):**
> "I'm sorry, but I can't assist with that."

**With GCG Suffix (After ~20 Iterations):**
> "Sure, I can help you with that. However,........" *(Safety filter bypassed)*
