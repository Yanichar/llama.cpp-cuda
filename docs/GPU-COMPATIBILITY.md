# GPU Compatibility Reference

## Finding Your GPU's Compute Capability

### Method 1: Using nvidia-smi

```bash
nvidia-smi --query-gpu=name,compute_cap --format=csv
```

### Method 2: Check NVIDIA Documentation

Visit: https://developer.nvidia.com/cuda-gpus

### Method 3: Using PyTorch (if installed)

```python
import torch
if torch.cuda.is_available():
    print(f"GPU: {torch.cuda.get_device_name(0)}")
    print(f"Compute Capability: {torch.cuda.get_device_capability(0)}")
```

## Compute Capability Breakdown

### 6.1 (Pascal)
- NVIDIA Titan XP
- Tesla P40
- GeForce GTX 1080, GTX 1070, GTX 1060, GTX 1050

**CUDA Support:** 12.8 (via this build only)

## Minimum CUDA Driver Versions

| CUDA Toolkit | Minimum Driver (Linux) | Minimum Driver (Windows) |
|--------------|------------------------|--------------------------|
| 12.8         | 570.15                | 571.00                   |

## Checking Your Driver Version

### Linux
```bash
nvidia-smi
# or
cat /proc/driver/nvidia/version
```

### Windows
```cmd
nvidia-smi
```

## CUDA Compatibility Matrix

| GPU Architecture | Compute Cap. | CUDA 12.8 |
|-----------------|--------------|-----------|
| Pascal          | 6.1          | ✅        |

## Recommendations by Use Case

### Pascal GPUs (GTX 10xx, Titan XP, Tesla P40)
**Only available option:** CUDA 12.8
- This build targets only compute capability 6.1 (Pascal)
- Use the original upstream repository for builds targeting other architectures

## Troubleshooting

### "CUDA driver version is insufficient"
- Update your NVIDIA driver to meet the minimum requirements for CUDA 12.8 (Driver >= 570.15 Linux / 571.00 Windows)

### "No CUDA-capable device detected"
- Check if your Pascal GPU is properly installed: `nvidia-smi`
- Verify NVIDIA driver is loaded: `lsmod | grep nvidia`

### "Binary not found"
- Verify you extracted the entire tarball
- Check permissions: `chmod +x llama-*`
- Ensure you're in the correct directory

## Additional Resources

- [NVIDIA CUDA Compatibility Guide](https://docs.nvidia.com/cuda/cuda-toolkit-release-notes/)
- [GPU Compute Capability Table](https://developer.nvidia.com/cuda-gpus)
- [NVIDIA Driver Downloads](https://www.nvidia.com/download/index.aspx)
