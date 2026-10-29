# Project Plan: GPT From Scratch

**Author:** Wangchuk Gyeltshen
**Started:** October 2026
**Type:** Solo learning and portfolio project

## 1. Overview

This project builds a small GPT-style language model from scratch in Python and PyTorch, without using any pretrained weights or high-level model libraries. The model is trained locally to generate text in the style of a chosen corpus. The goal is to understand, by implementing it, how the transformer architecture behind modern large language models actually works.

## 2. Goals

- Implement every core component myself: tokenizer, embeddings, self-attention, multi-head attention, transformer blocks and the training loop.
- Train the model on a GPU and generate readable text in the style of the training data.
- Track and document every training run so progress and decisions are visible.
- Produce a clean, well-documented GitHub repository suitable for a portfolio.

## 3. Scope

### In scope
- Character-level tokenizer, then a Byte Pair Encoding (BPE) tokenizer written from scratch
- Bigram baseline model
- Decoder-only transformer (GPT architecture)
- Training on a public domain corpus first, then on a corpus of my own choosing
- Text generation with sampling controls (temperature, top-k)
- A simple demo (command line first, optional web demo later)

### Out of scope
- Competing with real LLMs in quality or size
- Using pretrained weights or libraries like Hugging Face Transformers for the model itself
- Instruction tuning or chat behaviour (possible future work)
- Paid cloud compute

## 4. Milestones

| # | Milestone | Outcome |
|---|-----------|---------|
| M0 | Environment setup | Virtual environment, PyTorch with CUDA working on the GPU, repo structure in place |
| M1 | Data and character tokenizer | Load a public domain corpus (Tiny Shakespeare), encode and decode text, train/validation split |
| M2 | Bigram baseline | Simplest possible language model trained and generating (mostly nonsense) text; baseline loss recorded |
| M3 | Self-attention | Single-head attention, then multi-head attention with positional embeddings |
| M4 | Full transformer | Feed-forward layers, residual connections, layer norm and dropout; scaled-up training on the GPU |
| M5 | BPE tokenizer | Byte Pair Encoding tokenizer implemented from scratch and compared with the character tokenizer |
| M6 | Custom corpus | Model trained on my own chosen corpus (to be decided) |
| M7 | Demo and write-up | Generation script or web demo, README results, loss curves and sample outputs |

### Stretch goals
- Model checkpointing and resuming training
- Mixed precision training to fit larger models
- Hosting a demo on a free platform such as Hugging Face Spaces

## 5. Tools and Resources

| Category | Choice |
|----------|--------|
| Language | Python 3.13 |
| Framework | PyTorch (with CUDA) |
| Editor | VS Code |
| Version control | Git and GitHub (`WangchukGyeltshen/gpt-from-scratch`) |
| Hardware | Local laptop with NVIDIA RTX 4060 (8 GB VRAM) |
| Plotting | Matplotlib |

### Learning references
- Vaswani et al., *Attention Is All You Need* (2017): https://arxiv.org/abs/1706.03762
- Andrej Karpathy, *Let's build GPT: from scratch, in code, spelled out*: https://www.youtube.com/watch?v=kCc8FmEb1nY
- Andrej Karpathy, nanoGPT repository: https://github.com/karpathy/nanoGPT
- Tiny Shakespeare dataset (from char-rnn): https://github.com/karpathy/char-rnn

## 6. Constraints and Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| 8 GB of GPU memory limits model size | Cannot train large models | Keep models around 10 to 30 million parameters; use smaller batches or mixed precision if needed |
| Small custom corpus leads to overfitting | Model memorises instead of generalising | Monitor validation loss, use dropout, stop training early |
| Some PyTorch features have limited Windows support | Slower training or errors | Avoid optional features like `torch.compile` unless they work |
| Bugs in hand-written components are hard to spot | Model trains poorly | Build incrementally, test each component, compare loss against the expected baseline |

## 7. Success Criteria

- Validation loss clearly improves from the bigram baseline to the full transformer.
- Generated text is recognisably in the style of the training corpus.
- Every training run is logged in `docs/EXPERIMENTS.md`.
- Someone else can clone the repository and run training by following the README.

## 8. Documentation

| Document | Purpose | When written |
|----------|---------|--------------|
| `README.md` | Project summary, setup, usage and results | Updated throughout |
| `docs/PROJECT_PLAN.md` | This plan | Now |
| `docs/DESIGN.md` | Architecture, tokenizer, dataset and training setup | As each part is built |
| `docs/EXPERIMENTS.md` | Log of training runs and findings | From M2 onwards |