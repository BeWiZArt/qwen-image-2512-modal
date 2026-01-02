# ComfyUI Qwen Image 2512 on Modal

A clean, minimal Modal script to run ComfyUI with Qwen Image 2512 model for high-quality image generation.

## Features

- **One-click deployment**: Simple `modal serve` command
- **All models included**: Text encoders, diffusion models, VAE, and Lightning LoRA
- **A100 GPU**: Optimized for Qwen Image 2512 performance
- **Web interface**: Full ComfyUI UI accessible via browser
- **Persistent storage**: Models cached for reuse

## Quick Start

### 1. Install Dependencies
```bash
# Clone the repository
git clone https://github.com/innovativebran/qwen-image-2512-modal.git
cd qwen-image-2512-modal

# Install Python dependencies
pip install -r requirements.txt

# Alternative: Install modal directly
pip install modal>=1.2.0
```

### 2. Authenticate with Modal
```bash
modal setup
```

### 3. Deploy the App
```bash
modal serve qwen.py
```

### 4. Access ComfyUI
The command will output a URL like:
```
https://your-app-id--your-workspace.modal.app
```

Open this URL in your browser to access the ComfyUI interface.

## Usage Tutorial

### Basic Image Generation

1. **Open the ComfyUI URL** provided after deployment
2. **Load the Qwen Image 2512 workflow** (models are pre-loaded)
3. **Enter your prompt** in the text box
4. **Click "Queue Prompt"** to generate

### Recommended Settings

- **Resolution**: 1328x1328 (default)
- **Steps**: 4 (Lightning mode - fast)
- **CFG Scale**: 7.0
- **Sampler**: Euler
- **Scheduler**: Simple

### Example Prompts

```
A beautiful landscape with mountains and lakes
A detailed portrait of a woman
A cyberpunk city at night
A fantasy castle in the clouds
```

## Models Included

### Text Encoders
- `qwen_2.5_vl_7b_fp8_scaled.safetensors` - Main text encoder

### Diffusion Models
- `qwen_image_2512_fp8_e4m3fn.safetensors` - Fast FP8 model (default)
- `qwen_image_2512_bf16.safetensors` - High-quality BF16 model (use if you have enough VRAM)

### VAE
- `qwen_image_vae.safetensors` - Image decoder

### LoRAs
- `Qwen-Image-Lightning-4steps-V1.0.safetensors` - Lightning LoRA for fast 4-step generation

## File Structure

```
📂 ComfyUI/
├── 📂 models/
│   ├── 📂 text_encoders/
│   │      └── qwen_2.5_vl_7b_fp8_scaled.safetensors
│   ├── 📂 loras/
│   │      └── Qwen-Image-Lightning-4steps-V1.0.safetensors
│   ├── 📂 diffusion_models/
│   │      ├─ qwen_image_2512_bf16.safetensors
│   │      └── qwen_image_2512_fp8_e4m3fn.safetensors
│   └── 📂 vae/
│          └── qwen_image_vae.safetensors
```

## Performance Tips

1. **Use the FP8 model** for faster generation (default)
2. **4 steps** is usually sufficient for good quality
3. **A100-40GB** GPU provides optimal performance
4. **Batch multiple generations** for efficiency

## Troubleshooting

### Installation Issues

**If you get "modal-client is no longer being updated" error:**
```bash
pip uninstall modal-client -y
pip install modal>=1.2.0
```

**If modal command doesn't work:**
```bash
# Try using python module
python -m modal serve qwen.py

# Or reinstall specific version
pip uninstall modal -y
pip install modal==1.2.0
```

### If the URL doesn't work:
1. Wait 2-3 minutes for full startup
2. Check the Modal dashboard for app status
3. Try refreshing the URL

### If generation fails:
1. Ensure all models downloaded successfully
2. Check the ComfyUI console for errors
3. Try a simpler prompt first

### Performance issues:
1. Use the FP8 model instead of BF16
2. Reduce image resolution
3. Use fewer steps (4 is usually enough)

## Requirements

- **Python 3.8+**
- **Modal account** (free tier available)
- **A100-40GB GPU access** (may require billing)
- **~20GB storage** for models

### Python Dependencies
See `requirements.txt` for the complete list:
```bash
modal>=1.2.0
```

## Configuration

You can modify these settings in `qwen.py`:

- **GPU**: Change `gpu="A100-40GB"` to other available GPUs
- **Timeout**: Adjust `timeout=3200` for longer/shorter sessions
- **Container lifetime**: Modify `scaledown_window=300`

## License

This script uses Qwen Image 2512 models. Please check the model licenses on Hugging Face for usage terms.
