# Wan 2.2 Google Colab Template

A ready to use Google Colab notebook template for running [Wan 2.2](https://github.com/Wan-Video/Wan2.2), an advanced image to video AI model. This template simplifies the setup process and provides an optimized workflow for generating videos from images on Colab's free GPU resources.


[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/theelderemo/wan2.2-google-colab/blob/main/wan2_2.ipynb)

## Features

- **One Click Setup**: Automated installation of all dependencies and model downloads
- **Optimized for Colab**: Pre-configured settings for Google Colab (also works on other notebook platforms)
- **Memory Efficient**: Includes flags for model offloading and CPU-based text encoding to manage VRAM
- **User Friendly Interface**: Simple upload → configure → generate workflow
- **Multiple Resolutions**: Support for 1280×720, 832×480, and 1024×1024 outputs

## Quick Start

### Option 1: Using the Notebook (Recommended)

1. **Open in Google Colab**:
   - Upload `wan2_2.ipynb` to Google Colab, or
   - Use the "Open in Colab" button if you've set one up

2. **Select GPU Runtime**:
   - Go to `Runtime` → `Change runtime type`
   - Select `GPU` (preferably A100 if available)
   - Click `Save`

3. **Run the Cells**:
   - Execute each cell in order (or use `Runtime` → `Run all`)
   - The notebook will:
     - Clone the Wan 2.2 repository
     - Install all required dependencies
     - Download the model (≈60GB, takes 5ish minutes)
     - Set up the generation pipeline

4. **Generate Your Video**:
   - Upload an input image when prompted
   - Configure your prompt and settings
   - Run the generation cell and wait for your video!

### Option 2: Using the Python Script

If you prefer working with Python scripts directly:

```python
# The wan2_2.py file contains the same workflow
# You can run it in any Python notebook environment
```

## Requirements

### Recommended Hardware (Google Colab)
- **GPU**: NVIDIA A100 (40GB) or T4 (16GB)
- **RAM**: 12GB+ system RAM
- **Storage**: 70GB+ free space for model and temporary files

### Software Dependencies
All dependencies are automatically installed by the notebook:
- Python 3.8+
- PyTorch 2.4.0+
- Transformers, Diffusers, Accelerate
- Flash Attention
- Various CV and ML libraries

## Usage Guide

### Step 1: Upload Your Image
The notebook will prompt you to upload an input image. Supported formats:
- JPEG/JPG
- PNG
- BMP

### Step 2: Configure Settings

#### Prompting
Write a detailed text description of the motion/action you want to see in your video:

```
Example: "A woman smiling and waving at the camera, 
her hair gently moving in the breeze"
```

#### Model Configuration
- **Task**: Choose between `i2v-A14B` (14B parameters, higher quality) or `i2v-1.3B` (faster)
- **Resolution**: Select from `1280*720`, `832*480`, or `1024*1024`
- **Checkpoint Directory**: Default is `./Wan2.2-I2V-A14B`

#### Optimization Flags
Enable these to manage memory usage:
- **Offload Model**: Offloads parts of the model to CPU to save VRAM
- **Use T5 CPU**: Runs text encoder on CPU (recommended for free tier)
- **Convert Model Dtype**: Converts model to lower precision for memory efficiency

### Step 3: Generate Video
Run the generation cell and wait. Processing typically takes:
- **A100 GPU**: 5-10 minutes per video
- **T4 GPU**: 15-25 minutes per video

### Step 4: View Your Video
The notebook automatically displays the generated video inline when complete.

## Repository Structure

```
wan2.2-google-colab/
├── wan2_2.ipynb          # Main Colab notebook
├── wan2_2.py             # Python script version
└── README.md             # This file
```

## Customization

### Changing the Model
To use a different Wan 2.2 checkpoint:

1. Update the `checkpoint_dir` variable in Step 2
2. Use the appropriate task identifier (`i2v-A14B` or `i2v-1.3B`)

### Advanced Parameters
You can modify the generation command in Step 3 to add more flags. Refer to the [official Wan 2.2 repository](https://github.com/Wan-Video/Wan2.2) for all available options.

## Troubleshooting

### Out of Memory Errors
If you encounter CUDA out of memory errors:
1. Enable all optimization flags (offload, T5 CPU, convert dtype)
2. Try a lower resolution (832×480 instead of 1280×720)
3. Use the smaller 1.3B model instead of 14B
4. Restart runtime and clear cache before running

### Model Download Fails
- Check your internet connection
- The model is ≈60GB, ensure enough storage
- Try rerunning the download cell

### Video Quality Issues
- Use more detailed prompts
- Ensure input image is high quality
- Try the larger A14B model if using 1.3B
- Experiment with different resolutions

## Credits

- **Wan 2.2 Model**: [Wan-Video/Wan2.2](https://github.com/Wan-Video/Wan2.2)

## License

This template follows the same license as the Wan 2.2 project. Please refer to the [original repository](https://github.com/Wan-Video/Wan2.2) for licensing information.

## Contributing

Contributions are welcome! If you have improvements or fixes:
1. Fork this repository
2. Make your changes
3. Submit a pull request

## Additional Resources

- [Wan 2.2 Official Repository](https://github.com/Wan-Video/Wan2.2)
- [Hugging Face Model](https://huggingface.co/Wan-AI/Wan2.2-I2V-A14B)
- [Google Colab Documentation](https://colab.research.google.com/)

## Support

For issues specific to this template, please open an issue in this repository.

For questions about the Wan 2.2 model itself, refer to the [official repository](https://github.com/Wan-Video/Wan2.2).

---

**Note**: This is an unofficial template designed to make Wan 2.2 more accessible on Google Colab and other notebook platforms. Always ensure you have appropriate compute resources and comply with the platform's usage policies.
