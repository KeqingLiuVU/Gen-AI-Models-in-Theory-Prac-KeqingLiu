# ReFormer: Enhanced Transformer with Rotary Position Embedding

## Overview

### Context: 
Transformer-based models rely on self-attention mechanisms, which allow them to model dependencies between tokens.
### Problem:

Traditional transformers lack inherent understanding of word order. Thus absolute and relative positional encodings are introduced to incorporate positional information about tokens. Previous solutions had drowbacks in:

1) Handling long sequences
2) Capturing relative positions effectively
3) Compatibility with efficient attention mechanisms

### Approach: 

RoFormer introduces a novel method called Rotary Position Embedding (RoPE): Encodes positions using rotation matrices, and incorporates relative position information directly into self-attention.

### Solution: 
1) Mathematical Formulation
2) Integration into Transformer Architecture: 
3) Experimental Validation

## Critical Analysis

## Impacts

## Resource Links

