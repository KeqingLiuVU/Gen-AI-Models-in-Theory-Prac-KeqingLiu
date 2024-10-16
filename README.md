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


Input: X ∈ ℝ<sup>N×d</sup>, Θ = {θ<sub>i</sub> | θ<sub>i</sub> = 10000<sup>-2(i-1)/d</sup>, i ∈ [1, d/2]}
1. Generate queries, keys, and values:
       Q = W<sub>q</sub> · X
       K = W<sub>k</sub> · X
       V = W<sub>v</sub> · X
2. Apply rotary position embedding:
For m = 1 to N:
For i = 1 to d/2:
Q[m, 2i-1:2i] = Rotate2D(Q[m, 2i-1:2i], m·θ<sub>i</sub>)
K[m, 2i-1:2i] = Rotate2D(K[m, 2i-1:2i], m·θ<sub>i</sub>)
    
3. Compute attention scores:
Attention_Scores = (Q · K<sup>T</sup>) / sqrt(d)
    
4. Apply softmax and compute weighted sum:
Attention_Weights = Softmax(Attention_Scores)
Output = Attention_Weights · V
    
Return Output

Function Rotate2D(x, θ):
    Return [cos(θ)·x<sub>1</sub> - sin(θ)·x<sub>2</sub>, sin(θ)·x<sub>1</sub> + cos(θ)·x<sub>2</sub>]
## Critical Analysis

## Impacts

## Resource Links
@article{su2021roformer,
  title={RoFormer: Enhanced Transformer with Rotary Position Embedding},
  author={Su, Jianlin and Lu, Yu and Pan, Shengfeng and Murtadha, Ahmed and Wen, Bo and Liu, Yunfeng},
  journal={arXiv preprint arXiv:2104.09864},
  year={2021}
}


