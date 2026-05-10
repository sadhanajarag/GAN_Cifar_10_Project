# 🎨 GAN on CIFAR-10: Training & Image Generation

A **Generative Adversarial Network (GAN)** that learns to generate realistic 32×32 colour images by training on the **CIFAR-10** dataset.

---

## 📖 Table of Contents

1. [What is a GAN?](#-what-is-a-gan)
2. [Project Structure](#-project-structure)
3. [Hardware Requirements](#-hardware-requirements)
4. [Software Prerequisites](#-software-prerequisites)
5. [Installation — Step by Step](#-installation--step-by-step)
6. [How to Run](#-how-to-run)
7. [Expected Outputs](#-expected-outputs)
8. [Troubleshooting](#-troubleshooting)
9. [Credits](#-credits)

---

## 🧠 What is a GAN?

A **Generative Adversarial Network** consists of two neural networks competing against each other:

| Network | Role | Goal |
|---|---|---|
| **Generator** | Creates fake images from random noise | Fool the Discriminator |
| **Discriminator** | Classifies images as real or fake | Detect the Generator's fakes |

They play an adversarial game:
- The Generator gets better at creating realistic fakes
- The Discriminator gets better at detecting them
- Training ends when the Generator produces images the Discriminator can't distinguish from real ones

```
Random Noise → [Generator] → Fake Image → [Discriminator] → Real or Fake?
```

---

## 📁 Project Structure

```
Folder Path : 
│
├── GAN_CIFAR10_Assignment.ipynb   # 📓 Main notebook (run this!)
├── requirements.txt               # 📦 Python dependencies
├── README.md                      # 📄 This file
│
│   --- Generated during training ---
│
├── first_epoch_images.png         # 📸 Screenshot: Epoch 1 output
├── last_epoch_images.png          # 📸 Screenshot: Final epoch output
├── 10_fake_images.png             # 🖼️  10 generated fake images
├── training_summary_plots.png     # 📊 Loss & accuracy charts
└── cifar_gan_generator.h5         # 🧠 Saved Generator model
```

---

## 💻 Hardware Requirements

| Component | Minimum | Your Setup (HP ZBook Fury 16 G11) |
|---|---|---|
| **GPU** | NVIDIA GPU with 4+ GB VRAM | ✅ NVIDIA RTX 3500 Ada (12 GB VRAM) |
| **RAM** | 8 GB | ✅ 32 GB |
| **Storage** | 2 GB free | ✅ 954 GB |
| **OS** | Windows 10/11 | ✅ Windows 11 Enterprise 24H2 |

> 💡 **No GPU?** The notebook will still work on CPU — it will just be slower (~10 min/epoch instead of ~1 min/epoch).

---

## 🛠️ Software Prerequisites

| Software | Version | Purpose |
|---|---|---|
| **Anaconda** | Latest | Python environment manager |
| **Python** | 3.10 | Programming language |
| **TensorFlow** | 2.10.1 | Deep learning framework (last Windows GPU-native version) |
| **NVIDIA Driver** | 591.66+ | GPU driver (already installed) |
| **CUDA** | 11.x | GPU computing libraries |

---

## 🚀 Installation — Step by Step

### Step 1: Open Anaconda Prompt

Search **"Anaconda Prompt"** in the Windows Start Menu and open it.

### Step 2: Create a New Conda Environment

```bash
conda create -n gan_env python=3.10 -y
```

This creates an isolated Python 3.10 environment named `gan_env`.

### Step 3: Activate the Environment

```bash
conda activate gan_env
```

You should see `(gan_env)` in your prompt.

### Step 4: Navigate to the Project Folder

```bash
Path of folder example : cd C:\Users\JARAGST\GAN
```

### Step 5: Install Dependencies

**Option A — Using requirements.txt (Recommended):**

```bash
pip install -r requirements.txt
```

**Option B — Manual install:**

```bash
pip install tensorflow==2.10.1 numpy==1.23.5 matplotlib jupyter notebook ipykernel Pillow h5py
```

### Step 6: Install CUDA Libraries (for GPU support)

```bash
conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1 -y
```

> If `cudatoolkit=11.2` is not available, try:
> ```bash
> conda install -c conda-forge cudatoolkit=11.8 cudnn=8.6 -y
> ```

### Step 7: Register the Kernel with Jupyter

```bash
python -m ipykernel install --user --name=gan_env --display-name="Python 3 (gan_env)"
```

### Step 8: Verify GPU Detection

```bash
python -c "import tensorflow as tf; print('TF:', tf.__version__); print('GPU:', tf.config.list_physical_devices('GPU'))"
```

**✅ Expected output:**
```
TF: 2.10.1
GPU: [PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]
```

If GPU shows as `[]`, see the [Troubleshooting](#-troubleshooting) section.

---

## ▶️ How to Run

### Step 1: Activate the Environment

```bash
conda activate gan_env
```

### Step 2: Navigate to the Project Folder

```bash
cd C:\Users\JARAGST\GAN
```

### Step 3: Launch Jupyter Notebook

```bash
jupyter notebook
```

This will open your browser. Click on **`GAN_CIFAR10_Assignment.ipynb`** to open it.

### Step 4: Select the Correct Kernel

In the notebook menu bar:
- Click **Kernel** → **Change Kernel** → Select **Python 3 (gan_env)**

### Step 5: Run All Cells

- Click **Cell** → **Run All**
- Or run cells one by one with **Shift + Enter**

### Step 6: Watch the Training!

- After each epoch, a **3×3 grid of generated images** will be displayed
- Watch how images evolve from random noise to recognizable objects
- Training will **automatically stop** when the Generator is good enough

---

## 📤 Expected Outputs

After training completes, you will have:

| File | Description |
|---|---|
| `first_epoch_images.png` | 📸 Generated images after **Epoch 1** — should look like random noise |
| `last_epoch_images.png` | 📸 Generated images after the **final epoch** — should show recognizable shapes |
| `10_fake_images.png` | 🖼️ 10 completely new fake images from the trained Generator |
| `training_summary_plots.png` | 📊 Loss curves and Discriminator accuracy over epochs |
| `cifar_gan_generator.h5` | 🧠 Saved Generator model (~3 MB) — can be loaded later to generate more images |

### ⏱️ Expected Training Time

| Hardware | Time per Epoch | Total (100 epochs) |
|---|---|---|
| RTX 3500 Ada (your GPU) | ~30–60 seconds | ~50–100 minutes |
| CPU only | ~8–12 minutes | ~13–20 hours |

> 💡 **Early stopping** may trigger before 100 epochs — typically around epoch 30–60.

---

## 🔧 Troubleshooting

### ❌ GPU shows as `[]` (not detected)

**Cause:** CUDA libraries not installed or PATH not set.

**Fix:**
```bash
conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1 -y
```

If still not working, install CUDA manually:
1. Download CUDA 11.2 from [NVIDIA CUDA Archive](https://developer.nvidia.com/cuda-11.2.0-download-archive)
2. Download cuDNN 8.1 from [NVIDIA cuDNN Archive](https://developer.nvidia.com/rdp/cudnn-archive)
3. Copy cuDNN files into the CUDA installation folder

---

### ❌ `ModuleNotFoundError: No module named 'tensorflow'`

**Cause:** Wrong environment or TF not installed.

**Fix:**
```bash
conda activate gan_env
pip install tensorflow==2.10.1
```

---

### ❌ `AttributeError: module 'tensorflow' has no attribute '__version__'`

**Cause:** Conflicting TensorFlow packages.

**Fix:**
```bash
pip uninstall tensorflow tensorflow-intel -y
pip install tensorflow==2.10.1
```

---

### ❌ `numpy` version errors

**Cause:** TF 2.10 requires numpy < 1.24.

**Fix:**
```bash
pip install numpy==1.23.5
```

---

### ❌ Kernel not showing in Jupyter

**Cause:** ipykernel not registered.

**Fix:**
```bash
conda activate gan_env
pip install ipykernel
python -m ipykernel install --user --name=gan_env --display-name="Python 3 (gan_env)"
```

---

### ❌ `ResourceExhaustedError` (Out of GPU Memory)

**Cause:** Batch size too large for GPU memory.

**Fix:** Reduce batch size in the training cell:
```python
BATCH_SIZE = 64   # Reduce from 128 to 64
```

---

### ❌ Images look the same (Mode Collapse)

**Cause:** Generator learned to produce only one type of image.

**Fix:** 
- Restart training (re-run all cells)
- Reduce learning rate: change `0.0002` to `0.0001`
- Train for fewer epochs

---

## 🙏 Credits

- **Dataset:** [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) by Alex Krizhevsky
- **Framework:** [TensorFlow](https://www.tensorflow.org/) / [Keras](https://keras.io/)

---

## 📝 Quick Reference Commands

```bash
# Activate environment
conda activate gan_env

# Deactivate environment
conda deactivate

# List all environments
conda env list

# Check GPU
python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"

# Launch notebook
cd C:\Users\JARAGST\GAN
jupyter notebook

# Delete environment (if needed)
conda remove -n gan_env --all -y
```