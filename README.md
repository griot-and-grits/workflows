# 🎬 AI-Augmented Video Generation Workflow with Kubeflow Pipelines

This repository outlines a modular, scalable workflow for generating enriched videos from raw footage using machine learning and generative AI. The pipeline is orchestrated using **Kubeflow Pipelines**, with each step implemented as a Python script or Jupyter notebook.

---

## 📌 Workflow Overview

The pipeline performs the following steps:

1. **Transcribe audio from video**
2. **Identify speakers (diarization)**
3. **Extract key entities (events, people, locations)**
4. **Enrich entities with historical context**
5. **Generate AI-powered video snippets**
6. **Create AI voiceovers for narration**
7. **Animate uploaded photos**
8. **Assemble final video**

Each step is containerized and orchestrated via Kubeflow for reproducibility and scalability.

---

## 🧩 Pipeline Components

### 1. 🎧 Audio Transcription
- **Input**: Raw video file (MP4)
- **Tools**: `ffmpeg`, Whisper, Google Speech-to-Text
- **Output**: Timestamped transcript (JSON/SRT)

### 2. 🗣️ Speaker Diarization
- **Input**: Transcript + audio
- **Tools**: `pyannote-audio`, Resemblyzer
- **Output**: Annotated transcript with speaker labels

### 3. 🧠 Named Entity Recognition & Topic Extraction
- **Input**: Annotated transcript
- **Tools**: `spaCy`, Hugging Face Transformers, OpenAI API
- **Output**: Structured metadata (JSON)

### 4. 📚 Historical Context Enrichment
- **Input**: Extracted entities
- **Tools**: Wikipedia API, Wolfram Alpha, LLMs
- **Output**: Historical summaries (text)

### 5. 🎨 AI-Generated Video Snippets
- **Input**: Historical text
- **Tools**: RunwayML, Genmo, Deforum
- **Output**: Short video clips

### 6. 🗣️ AI Voiceover Generation
- **Input**: Historical text
- **Tools**: ElevenLabs, PlayHT, Azure Neural TTS
- **Output**: Voiceover audio (MP3/WAV)

### 7. 🖼️ Photo Animation
- **Input**: Uploaded images from S3
- **Tools**: D-ID, Deep Nostalgia, Stable Video Diffusion
- **Output**: Animated photo clips

### 8. 🧵 Final Video Assembly
- **Input**: All generated media assets
- **Tools**: `moviepy`, `ffmpeg`, Adobe Premiere API
- **Output**: Final video (MP4)

---

## ⚙️ Pipeline Architecture

| Component | Type | Parallelizable | Suggested Tools |
|-----------|------|----------------|------------------|
| Transcription | Script | ✅ | Whisper, ffmpeg |
| Diarization | Script | ✅ | pyannote-audio |
| NER & Topic Extraction | Notebook | ✅ | spaCy, transformers |
| Historical Enrichment | Notebook | ✅ | Wikipedia API, LLM |
| Video Generation | Notebook | ✅ | RunwayML, Genmo |
| Voiceover | Script | ✅ | ElevenLabs, Azure TTS |
| Photo Animation | Script | ✅ | D-ID, Stable Diffusion |
| Final Assembly | Script | ❌ | moviepy, ffmpeg |

---

## 📁 Folder Structure

```bash
.
├── notebooks/
│   ├── 01_transcription.ipynb
│   ├── 02_diarization.ipynb
│   ├── 03_entity_extraction.ipynb
│   ├── 04_historical_enrichment.ipynb
│   ├── 05_video_generation.ipynb
│   ├── 06_voiceover.ipynb
│   ├── 07_photo_animation.ipynb
│   └── 08_video_assembly.ipynb
├── pipeline/
│   └── pipeline_definition.py
├── Dockerfiles/
│   └── component-specific Dockerfiles
├── data/
│   └── input_videos/, transcripts/, outputs/
├── README.md
