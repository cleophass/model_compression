# **Model Compression**

Model compression refers to techniques used to reduce the size and computational requirements of machine learning models—particularly large language models (LLMs) - without significantly sacrificing performance.

## 🔧 5 Main Techniques to Compress or Optimize LLMs

1. **Quantization**  
2. **Pruning**  
3. **Knowledge Distillation**  
4. **Compilation**  
5. **Caching**

---

## #1. Quantization

Quantization involves reducing the precision of the numerical values (parameters) used in a model, such as weights and biases.

### 🤔 What does it mean?

Most models are trained using 32-bit floating-point numbers (FP32). Quantization replaces these high-precision values with lower-precision formats like 8-bit integers (INT8), significantly reducing the model's memory footprint and computational cost.

### 🔄 Two Main Approaches:

- **Post-Training Quantization (PTQ):**
  - Quantize a pre-trained model without re-training it.
  - Useful when using open-source models (e.g., on Hugging Face).
  - Simple and quick, but may slightly reduce accuracy.

- **Quantization-Aware Training (QAT):**
  - Simulate quantization during training so the model learns to compensate for reduced precision.
  - Often results in better accuracy compared to PTQ.
  - Requires access to the training pipeline and data.

> 📝 **Note:** INT8 models can be up to 4x smaller than FP32 ones and can also run faster on compatible hardware.

---

## #2. Pruning

Pruning removes unnecessary parameters from a model, directly reducing its size and potentially improving inference speed.

### 🧠 Two Types of Pruning:

- **Unstructured Pruning:**
  - Removes individual weights (usually those close to zero).
  - Results in sparse matrices (many zeroes).
  - Requires specialized hardware to efficiently skip zero computations.

- **Structured Pruning:**
  - Removes entire components (e.g., attention heads, neurons, layers).
  - Leads to a smaller and faster model compatible with standard hardware.
  - Easier to deploy in production, though with less aggressive compression.

---

## #3. Knowledge Distillation

Knowledge Distillation is a technique where a smaller model (the student) learns to mimic a larger, well-trained model (the teacher).

### 🧪 Key Concepts:

- **Soft Targets:**
  - Instead of training the student with hard labels (e.g., 0 or 1), we use the teacher’s output probabilities (soft labels).
  - This provides richer information and improves generalization.
  - Especially useful in tasks like classification or language modeling.

- **Synthetic Data Generation:**
  - Use the teacher model to generate data (e.g., synthetic text prompts and responses).
  - Helps train the student model even in low-data scenarios.

> 🧠 **Result:** The student model can approach the teacher’s performance while being significantly smaller and faster.

---

## #4. Compilation

Model compilation involves optimizing the model's computation graph for a specific target hardware or inference engine.

### ⚙️ How it helps:

- Converts the model into a more efficient format (e.g., using **TorchScript**, **ONNX**, or **XLA**).
- Enables hardware-specific optimizations, such as kernel fusion or graph simplification.
- Can reduce inference latency and improve throughput.

> 🔥 Especially effective when combined with quantization and deployed on edge devices or specialized accelerators (e.g., GPUs, TPUs).

---

## #5. Caching

Caching stores intermediate computations or full outputs to avoid redundant processing in repeated or similar queries.

### 💾 Use Cases:

- **Prompt Caching:** In LLMs, caching key/value pairs in transformers avoids recomputation for the same context window.
- **Output Caching:** Store model responses for repeated prompts in applications like chatbots or retrieval-augmented generation (RAG).

> ⚡️ Caching doesn't reduce the model size but significantly improves efficiency and responsiveness at runtime.
