

## Transformer‑Augmented U‑Net for Segmentation

This project implements a custom U‑Net architecture enhanced with **attention** and **transformer blocks** to improve segmentation performance, especially around object boundaries.

### Model Overview
- **Encoder**: Four convolutional blocks (`DoubleConv`) with max pooling to gradually compress the image and extract features.
- **Skip Transformer**: At the deepest encoder level, a transformer block captures long‑range dependencies between pixels, giving the network global context.
- **Bottleneck Transformer**: Another transformer block operates on the compressed representation to refine features before decoding.
- **Dual Decoders**:
  - **Main decoder**: Reconstructs the segmentation mask with CBAM (Channel + Spatial Attention) to focus on important regions.
  - **Auxiliary decoder**: Provides a second prediction path with added noise during training, encouraging robustness.
- **Boundary Refinement**: A small CNN takes the difference (uncertainty) between the two decoders and sharpens edges for cleaner masks.

### Key Features
- **CBAM Attention**: Combines channel and spatial attention to highlight relevant features.
- **Transformers**: Capture global relationships that standard CNNs miss.
- **Dual Outputs**: Main + auxiliary predictions help estimate uncertainty.
- **Refinement Module**: Cleans up boundaries where the model is unsure.
- **Gradient Checkpointing**: Reduces GPU memory usage by ~40%, making training feasible on limited hardware.

### Outputs
The model produces:
1. **Main logits** – primary segmentation prediction.  
2. **Auxiliary logits** – secondary prediction with noise.  
3. **Refined mask** – final polished segmentation.  
4. **Uncertainty map** – highlights regions where predictions disagree.

---

This way, anyone reading your repo will immediately understand the **big picture**: it’s a U‑Net with transformers, attention, dual decoders, and boundary refinement.  

