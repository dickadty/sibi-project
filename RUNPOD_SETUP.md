# Setup Guide - RunPod + VS Code Remote SSH

## Quick Start

### 1. Connect via SSH (di Mac terminal)

```bash
ssh runpod-direct
# atau
ssh runpod-runpod-io
```

### 2. Setup di RunPod

```bash
cd /workspace
mkdir sibi-project
cd sibi-project

# Clone atau copy project
# Jika via GitHub:
git clone <repo-url> .

# Atau upload via scp dari Mac:
# scp -r -i ~/.ssh/id_ed25519 -P 58343 /Users/dickyaditya04/Downloads/AI/* root@213.181.111.2:/workspace/sibi-project/
```

### 3. Setup Python Environment

```bash
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Verify GPU

```bash
nvidia-smi

# Test TensorFlow GPU
python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```

### 5. Run Jupyter in VS Code

Option A - Direct in VS Code:

1. Open VS Code
2. Command Palette: "Remote-SSH: Connect to Host"
3. Select `runpod-direct` or `runpod-runpod-io`
4. Open folder: `/workspace/sibi-project`
5. Open notebook file
6. Select Python kernel (should show venv)
7. Run cells!

Option B - Via Jupyter Server:

```bash
# In RunPod terminal
jupyter notebook --ip=0.0.0.0 --no-browser --port=8888

# Copy token URL and open in browser
```

## File Structure in RunPod

```
/workspace/sibi-project/
├── data/
│   ├── raw/
│   │   └── sibi/
│   │       ├── A/
│   │       ├── B/
│   │       ... dst
│   └── processed/
├── models/
├── reports/
├── features/
├── venv/
├── requirements.txt
└── training_sibi_efficientnetb0_.ipynb
```

## Tips

- **GPU Monitoring during training:**

  ```bash
  # In another terminal
  watch -n 1 nvidia-smi
  ```

- **Check GPU Memory:**

  ```bash
  nvidia-smi --query-gpu=memory.used,memory.total --format=csv
  ```

- **Stop RunPod pod when done** to save costs

- **Keep venv activated** when running Jupyter

## Troubleshooting

### GPU not detected

```bash
# Check if CUDA is available
python -c "import tensorflow as tf; print(tf.test.is_built_with_cuda())"

# Check GPU drivers
nvidia-smi
```

### Permission denied for SSH key

```bash
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub
```

### Port already in use

```bash
# Use different port for Jupyter
jupyter notebook --port=8889
```

## Contact Info

SSH Host: `ssh.runpod.io` atau `213.181.111.2:58343`
User: `4xf6ry9ljtim8f-64411af4` atau `root`
Key: `~/.ssh/id_ed25519`
