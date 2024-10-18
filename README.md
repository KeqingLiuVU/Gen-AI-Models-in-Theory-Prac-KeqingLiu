# ReFormer: Enhanced Transformer with Rotary Position Embedding

## Overview

### Introduction: 
Sequential order of words is of great value to natural language understanding. Transformer models require positional encoding because the Attention mechanism alone cannot capture the order of input tokens or distinguish their positions. There are two main approaches to address this:
* Absolute positional encoding: Integrate positional information directly into the input.
* Relative positional encoding: Modify the attention mechanism to enable it to distinguish tokens based on their positions.
  
### Problem:

The 2 methods drawbacks in the following areas:

* Handling long sequences
* Capturing relative positions effectively
* Compatibility with efficient attention mechanisms like linear self-attention

### Approach: 

ReFormer, a transformer enhanced with RoPE (Rotary Position Embedding), was developed. 

The novel method called Rotary Position Embedding (RoPE):
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

## Architecture Overview
### A 2D case

![Screenshot 2024-10-18 at 6 09 43 PM](https://github.com/user-attachments/assets/450583f4-144f-4331-9ce0-bcc66a83d8fc)

## Critical Analysis

## Impacts

## Resource Links
https://medium.com/p/31c082e16b26

https://kexue.fm/archives/8265

