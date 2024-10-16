# ReFormer: Enhanced Transformer with Rotary Position Embedding

## Overview

### Introduction: 
Sequential order of words is of great value to natural language understanding. But traditional transformers are inherently position-agnostic. They rely on self-attention mechanisms, which allow them to incorporate positional information about tokens.
### Problem:

Traditional transformers ldo not inherently understand word order, so absolute and relative positional encodings are introduced to address the issue. While these approaches are effective, they have drowbacks in the following areas:

* Handling long sequences
* Capturing relative positions effectively
* Compatibility with efficient attention mechanisms like linear self-attention

### Approach: 

RoFormer introduces a novel method called Rotary Position Embedding (RoPE). It encodes positions using rotation matrices, and incorporates relative position information directly into self-attention.

Rotary Position Embedding is prioritized over existing methods for its advantage in: 
* Sequence length flexibility
* Decaying inter-token dependency with increasing relative distances
* Capability of equipping the linear self-attention with relative position encding


### Solution: 
1) Mathematical Formulation
   
3) Integration into Transformer Architecture

5) Experimental Validation

## Critical Analysis

## Impacts

## Resource Links

