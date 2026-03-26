# Wan2.2 Google Colab — Complete Video Generation Suite

A comprehensive Google Colab notebook covering **every generation mode** in [Wan2.2](https://github.com/Wan-Video/Wan2.2) — the open-source MoE video generation model from Alibaba. Includes text-to-video, image-to-video, speech-to-video, pose-driven animation, character replacement, and more.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/theelderemo/wan2.2-google-colab/blob/main/wan2_2.ipynb)

---

## Supported Generation Modes

| Section | Mode | Model | Resolution | Notes |
|---------|------|-------|------------|-------|
| 2 | **Text-to-Video** | T2V-A14B | 480P / 720P | MoE 27B total / 14B active |
| 3 | **Image-to-Video** | I2V-A14B | 480P / 720P | Aspect ratio follows input image |
| 4 | **Text+Image-to-Video** | TI2V-5B | 720P @ 24fps | Runs on RTX 4090 (24 GB) |
| 5a | **Speech-to-Video** | S2V-14B | 480P / 720P | Image + audio file → talking video |
| 5b | **Pose-Driven Speech-to-Video** | S2V-14B | 480P / 720P | Image + audio + pose MP4 |
| 5c | **TTS Speech-to-Video** | S2V-14B + CosyVoice | 480P / 720P | Synthesize voice, then animate |
| 6a | **Character Animation** | Animate-14B | 720P | Character mimics motion from video |
| 6b | **Character Replacement** | Animate-14B | 720P | Swap character into existing video |

---

## Quick Start

### 1. Open in Google Colab

Click the badge above or upload `wan2_2.ipynb` directly to [colab.research.google.com](https://colab.research.google.com).

### 2. Select a GPU Runtime

Go to `Runtime` → `Change runtime type` → select **A100** (recommended for A14B models) or **T4/L4** (for TI2V-5B).

### 3. Run Section 0 — Setup

Run the setup cells once per session. They:
- Check your GPU
- Clone the Wan2.2 repo (skips if already present)
- Install all Python dependencies
- Optionally install flash-attn and CosyVoice (S2V TTS) extras

### 4. Run Section 1 — Download Your Model(s)

Each model has its own download cell. Only download what you need:

| Cell | Model | Approx Size |
|------|-------|-------------|
| 1.1 | Wan2.2-T2V-A14B | ~28 GB |
| 1.2 | Wan2.2-I2V-A14B | ~28 GB |
| 1.3 | Wan2.2-TI2V-5B | ~10 GB |
| 1.4 | Wan2.2-S2V-14B | ~28 GB |
| 1.5 | Wan2.2-Animate-14B | ~28 GB |

### 5. Jump to Any Generation Section

Each section is self-contained. Configure settings via the `@param` widgets, upload your inputs, and run the generation cell.

---

## Notebook Structure

```
wan2_2.ipynb
├── Section 0 — Setup & Installation
│   ├── 0.1  GPU check
│   ├── 0.2  Clone Wan2.2 repo
│   ├── 0.3  Install core dependencies
│   ├── 0.4  Install flash-attn (optional)
│   ├── 0.5  Install S2V / CosyVoice deps (optional)
│   └── 0.6  Install huggingface-hub CLI
│
├── Section 1 — Model Download
│   ├── 1.1  T2V-A14B
│   ├── 1.2  I2V-A14B
│   ├── 1.3  TI2V-5B
│   ├── 1.4  S2V-14B
│   └── 1.5  Animate-14B
│
├── Section 2 — Text-to-Video (T2V-A14B)
│   ├── 2.1  Configuration (resolution, steps, seed, prompt extension)
│   └── 2.2  Run generation
│
├── Section 3 — Image-to-Video (I2V-A14B)
│   ├── 3.1  Upload image
│   ├── 3.2  Configuration
│   └── 3.3  Run generation
│
├── Section 4 — Text+Image-to-Video (TI2V-5B)
│   ├── 4.1  Upload image (optional — omit for pure T2V)
│   ├── 4.2  Configuration
│   └── 4.3  Run generation
│
├── Section 5 — Speech-to-Video (S2V-14B)
│   ├── 5.1  Upload image & audio
│   ├── 5.2a Basic S2V config + run
│   ├── 5.3b Pose-driven S2V (upload pose video) + run
│   └── 5.4c TTS S2V — CosyVoice voice cloning + run
│
├── Section 6 — Character Animation & Replacement (Animate-14B)
│   ├── 6.1  Upload character image & motion video
│   ├── 6.2  Choose mode (animate / replace) & resolution
│   ├── 6.3  Preprocess input video (extracts pose/face signals)
│   ├── 6.4a Run — Animation mode
│   └── 6.4b Run — Replacement mode
│
└── Section 7 — Display & Download
    ├── 7.1  List all generated videos
    ├── 7.2  Preview video inline
    └── 7.3  Download to local machine
```

---

## GPU Requirements

| Model | Minimum VRAM | Recommended |
|-------|-------------|-------------|
| TI2V-5B | 24 GB | RTX 4090 / L4 |
| T2V-A14B | 24 GB (with offload flags) | A100 80 GB |
| I2V-A14B | 24 GB (with offload flags) | A100 80 GB |
| S2V-14B | 80 GB | A100 80 GB |
| Animate-14B | 80 GB | A100 80 GB |

> All A14B sections include `--offload_model`, `--convert_model_dtype`, and `--t5_cpu` toggle flags to reduce VRAM usage on smaller GPUs.

---

## Prompt Extension

For richer, more detailed outputs, the T2V and I2V sections support **prompt extension** via:

- **Local Qwen** — runs a Qwen2.5 LLM (T2V) or Qwen2.5-VL (I2V) locally to expand your prompt. No API key needed.
- **Dashscope API** — uses Alibaba Cloud's hosted `qwen-plus` / `qwen-vl-max` models. Requires a free [Dashscope API key](https://www.alibabacloud.com/help/en/model-studio/getting-started/first-api-call-to-qwen).

---

## Troubleshooting

### Out of Memory (OOM)
- Enable all three memory flags: `offload_model`, `convert_model_dtype`, `t5_cpu`
- Drop resolution to 832×480
- Use TI2V-5B (Section 4) instead of the A14B models — it runs on 24 GB

### Model Download Fails
- Re-run the download cell — `huggingface-cli` resumes partial downloads
- Log in to Hugging Face to avoid rate limits: uncomment the `login()` line in cell 0.6

### flash-attn Build Fails
- Skip cell 0.4 — the model falls back to standard attention automatically
- Or try: `pip install flash-attn --no-build-isolation` after installing all other deps first

### S2V / CosyVoice Import Errors
- Make sure you ran cell 0.5 before Section 5c
- CosyVoice requires the `requirements_s2v.txt` extras

### Animate Preprocessing Fails
- Ensure `Wan2.2-Animate-14B/process_checkpoint` exists (downloaded in cell 1.5)
- Input video should be a standard MP4 with a clearly visible human subject

---

## Repository Structure

```
wan2.2-google-colab/
├── wan2_2.ipynb    # Main notebook (all generation modes)
├── README.md       # This file
└── SECURITY.md
```

---

## Credits & Links

- **Wan2.2 Model**: [Wan-Video/Wan2.2](https://github.com/Wan-Video/Wan2.2)
- **Hugging Face**: [Wan-AI](https://huggingface.co/Wan-AI/)
- **Paper**: [arXiv:2503.20314](https://arxiv.org/abs/2503.20314)
- **CosyVoice (TTS)**: [FunAudioLLM/CosyVoice](https://github.com/FunAudioLLM/CosyVoice)

## License

This template is released under the same [Apache 2.0 License](https://github.com/Wan-Video/Wan2.2/blob/main/LICENSE.txt) as the upstream Wan2.2 project.

---

> This is an unofficial Colab template. For questions about the Wan2.2 model itself, refer to the [official repository](https://github.com/Wan-Video/Wan2.2) or join their [Discord](https://discord.gg/AKNgpMK4Yj).
