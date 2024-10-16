# ReFormer: Enhanced Transformer with Rotary Position Embedding

## Overview

### Introduction: 
Sequential order of words is of great value to natural language understanding. But traditional transformers are inherently position-agnostic. They rely on self-attention mechanisms, which allow them to incorporate positional information about tokens.
### Problem:

Traditional transformers do not inherently understand word order, so absolute and relative positional encodings are introduced to address the issue. While these approaches are effective, they have drawbacks in the following areas:

* Handling long sequences
* Capturing relative positions effectively
* Compatibility with efficient attention mechanisms like linear self-attention

### Approach: 

ReFormer, a transformer enhanced with RoPE (Rotary Position Embedding), was developed. 

RoFormer introduces a novel method called Rotary Position Embedding (RoPE):
* Encodes positions using rotation matrices
* Incorporates relative position information directly into self-attention

### Solution: 
* Mathematical Formulation
  - Derives RoPE from first principles
  - Proves its properties mathematically
   
* Integration into Transformer Architecture
  - Replaces traditionally additive position encodings
  - Modifies self-attention mechanism to use RoPE

* Experimental Validation
  - Machine translation: WMT 2014 English-German dataset
  - Language model pre-training: BookCorpus and Wikipedia
  - Find-tuning: GLUE benchmark tasks
  - Long document classification: Chinese legal document matching

Key finding: Rotary Position Embedding is prioritized over existing methods for its advantage in: 
1. Sequence length flexibility, with particularly strong results on long sequence tasks
2. Decaying inter-token dependency with increasing relative distances
3. Capability of equipping the linear self-attention with relative position encoding (e.g., Performers)
4. Faster convergence and lower loss in pre-training

## Critical Analysis

## Impacts

## Resource Links

