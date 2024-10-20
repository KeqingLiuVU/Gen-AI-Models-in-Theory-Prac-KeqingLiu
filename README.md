# ReFormer: Enhanced Transformer with Rotary Position Embedding

## Overview

### Background: 
Sequential order of words is of great value to natural language understanding. Transformer models require positional encoding because the Attention mechanism alone cannot capture the order of input tokens or distinguish their positions. There are two main approaches to address this:
* Absolute positional encoding: Integrate positional information directly into the input.
<img width="626" alt="Screenshot 2024-10-18 at 7 23 48 PM" src="https://github.com/user-attachments/assets/e70501c0-4b23-478f-bb56-4623e4124f10">

* Relative positional encoding: Modify the attention mechanism to enable it to distinguish tokens based on their positions.
<img width="754" alt="Screenshot 2024-10-18 at 7 24 33 PM" src="https://github.com/user-attachments/assets/51adfbbe-4287-496b-9a0c-78042b350460">

A: attention score matrix

B: position bias matrix based on the relative position j-i

Q, K: query and key vectors for tokens i and j

d_k: dimensionality of the key vectors


### Problem:

The 2 methods drawbacks in the following areas:

* Handling long sequences: Absolute positional encoding struggles with long sequences since it uses fixed position values that don't work well for longer contexts.
* Capturing relative positions effectively: Relative positional encoding is more complex and adds extra computation to handle the distances between tokens.
* Compatibility with efficient attention mechanisms like linear self-attention

### Approach: 

Rotary positional embedding, or RoPE, is an effective technique that combines the strengths of both absolute and relative embeddings. It encodes positional information by rotating word vectors in a high-dimensional space, with the rotation amount determined by each word's position in the sequence. This allows the model to easily compute the relative position between any two words by comparing their rotation differences. As a result, each word receives a unique rotation based on its absolute position, while the model can still capture relative positional information.

* Encodes positions using rotation matrices
* Incorporates relative position information directly into self-attention

![Screenshot 2024-10-18 at 7 52 14 PM](https://github.com/user-attachments/assets/feda4254-a81c-47f3-83e0-3e0bae264fb3)

![Screenshot 2024-10-19 at 9 49 43 AM](https://github.com/user-attachments/assets/b5a496d8-0845-4b6c-b853-13f93b28b2cd)

### Experiments: 

* Experimental Validation
  - Machine translation: sequence-to-sequence language translation tasks

     ![Screenshot 2024-10-18 at 10 45 58 AM](https://github.com/user-attachments/assets/ded9b5ba-3614-4e89-9044-6c6cdc5cee77)

  - Pre-training Language Modeling: learning contextual representations

    ![Screenshot 2024-10-18 at 10 50 07 AM](https://github.com/user-attachments/assets/327f61d0-95b4-421b-8dc6-ddba08e94184)
    
  - Fine-tuning on GLUE tasks: generalization ability on the downstream NLP tasks

    ![Screenshot 2024-10-18 at 10 49 31 AM](https://github.com/user-attachments/assets/2663e346-eea4-474b-9474-6041968296cb)

  - Long documents: text whose length exceeds 512 characters
    
    ![Screenshot 2024-10-18 at 6 25 04 PM](https://github.com/user-attachments/assets/abec11ba-4167-478a-b45a-c782391f864e)


Key finding: Rotary Position Embedding is prioritized over existing methods for its advantage in: 
1. Sequence length flexibility, with particularly strong results on long sequence tasks
2. Decaying inter-token dependency with increasing relative distances
3. Capability of equipping the linear self-attention with relative position encoding (e.g., Performers)
4. Faster convergence and lower loss in pre-training

## Architecture Overview

<img width="888" alt="Screenshot 2024-10-19 at 5 59 34 PM" src="https://github.com/user-attachments/assets/e7ea1961-cfb7-4840-a223-9c568433c00e">

![Screenshot 2024-10-18 at 10 08 10 AM](https://github.com/user-attachments/assets/91ee2438-cf28-458b-9c6c-befd06ed886e)

Given a token embedding and its position, absolute positional embedding adds a separate positional embedding to the token embedding. In contrast, rotary positional embedding integrates the positional information directly into the token embedding, producing a new embedding that naturally includes the position.

### A 2D case

![Screenshot 2024-10-18 at 6 09 43 PM](https://github.com/user-attachments/assets/450583f4-144f-4331-9ce0-bcc66a83d8fc)

![Screenshot 2024-10-19 at 5 54 27 PM](https://github.com/user-attachments/assets/d62271cf-fd70-4388-ba62-c4aa77d613fe)


The function appleis RoPE to either query (q) or key(k) at position m.  The formula: 

1. First applies a learned linear transformation to the input vector (multiplication by the W matrix)
2. Then rotates the result based on the position m (multiplication by the rotation matrix)

Pseudocode:

<img width="1129" alt="Screenshot 2024-10-19 at 6 38 33 PM" src="https://github.com/user-attachments/assets/d10e6c7d-e5a8-4a5c-ab6c-e2b2259b6391">

### General form

![Screenshot 2024-10-19 at 6 44 57 PM](https://github.com/user-attachments/assets/b03d56df-a505-4ee6-b169-1a9b52e04d88)

Pseudocode: 

<img width="703" alt="Screenshot 2024-10-19 at 7 53 56 PM" src="https://github.com/user-attachments/assets/eda46acd-2822-42df-9cab-3c1c44d3c64f">

When the vector has more than two dimensions, it is divided into two-dimensional chunks, and each chunk is rotated. The first chunk undergoes rotation in the first two dimensions, while different rotation angles are applied to each pair of dimensions in the vector. And RoPE assumes the dimension of vector is an even number.

![Screenshot 2024-10-19 at 8 03 46 PM](https://github.com/user-attachments/assets/d8ab011a-f7b8-474b-a08c-c8431890db61)

## Critical Analysis

* Limited theoretical explanation: While the authors provide mathematical formulations of RoPE, there lacks of thorough explanations on why it converges faster than baseline models with other position encoding strategies. This theoretical gap could have been developed further.
  
* Unexplained performance on long texts: Although the model has superior performance on long texts compared to peer models, the authors have not come up with a faithful explanation for this. This is a significant limitation that warrants further investigation.

* Limited comparison to recent alternatives: While the authors compare RoFormer to BERT and some other models, they don't extensively compare it to more recent position encoding methods or transformer variants. This limits the paper's ability to definitively claim superiority over state-of-the-art alternatives.

## Impact

### Impacts & Importance:

The paper proposed a novel method named Rotary Positional Embedding (RoPE). RoPE improves transformers by enabling better handling of relative positions and long dependencies in tasks like text generation. By improving both efficiency and accuracy, RoPE strengthens transformer models across domains, including NLP and computer vision.

### Intersection with other work:

Rotary Positional Embedding (RoPE) builds on the original positional encoding introduced by Vaswani et al. (2017), addressing its limitations in handling long sequences.

Since its introduction in 2022, RoPE has been incorporated into models like PaLM (Google), GPT-Neo and GPT-J (EleutherAI), and LLaMA (Meta), improving their ability to handle long sequences in real-world applications such as chatbots and document summarization.

RoPE enables scalable transformers with longer contexts, multimodal AI, and more efficient handling of large-scale data. Future work may explore adaptive or hierarchical positional encodings, further enhancing AI's ability to process complex inputs.

### Changing the AI landscape:

RoPE has enhanced transformers' capacity to process longer sequences, benefiting models like GPT-3 and PaLM. This improvement allows for more complex tasks, including document summarization, code generation, and advanced conversation modeling. Its adoption signals a shift toward more scalable transformers, laying the groundwork for advancements in sequence modeling and multimodal AI.

## Citation:
@misc{su2023roformerenhancedtransformerrotary,
      title={RoFormer: Enhanced Transformer with Rotary Position Embedding}, 
      author={Jianlin Su and Yu Lu and Shengfeng Pan and Ahmed Murtadha and Bo Wen and Yunfeng Liu},
      year={2023},
      eprint={2104.09864},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2104.09864}, 
}



@misc{phuong2022formalalgorithmstransformers,
      title={Formal Algorithms for Transformers}, 
      author={Mary Phuong and Marcus Hutter},
      year={2022},
      eprint={2207.09238},
      archivePrefix={arXiv},
      primaryClass={cs.LG},
      url={https://arxiv.org/abs/2207.09238}, 
}

Ashish Vaswani, Noam Shazeer, Niki Parmar, Jakob Uszkoreit, Llion Jones, Aidan N Gomez, L ukasz Kaiser,
and Illia Polosukhin. Attention is all you need. In I. Guyon, U. V. Luxburg, S. Bengio, H. Wallach,
R. Fergus, S. Vishwanathan, and R. Garnett, editors, Advances in Neural Information Processing Systems, volume 30. Curran Associates, Inc., 2017. URL https://proceedings.neurips.cc/paper/2017/file/
3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf.

## Resource Links
https://medium.com/p/31c082e16b26

https://kexue.fm/archives/8265

https://arxiv.org/abs/2207.09238

https://huggingface.co/docs/transformers/model_doc/roformer

https://www.youtube.com/watch?v=o29P0Kpobz0




