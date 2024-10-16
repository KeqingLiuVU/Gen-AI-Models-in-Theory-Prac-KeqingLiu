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
![Screenshot 2024-10-16 at 2 10 37 PM](https://github.com/user-attachments/assets/54942433-b592-45a0-9cae-3354d08b1971)
## Critical Analysis

## Impacts

## Resource Links
@article{su2021roformer,
  title={RoFormer: Enhanced Transformer with Rotary Position Embedding},
  author={Su, Jianlin and Lu, Yu and Pan, Shengfeng and Murtadha, Ahmed and Wen, Bo and Liu, Yunfeng},
  journal={arXiv preprint arXiv:2104.09864},
  year={2021}
}


