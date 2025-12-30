# Complete AI Skin Lesion Analysis System

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Python 3.8+](https://img.shields.io/badge/Python-3.8+-blue.svg)
![Colab](https://img.shields.io/badge/Google-Colab-orange.svg)

A comprehensive AI-powered skin lesion analysis system that combines **OpenCV feature extraction**, **Vision Language Models (VLM)**, and **Retrieval-Augmented Generation (RAG)** to provide evidence-based dermatological diagnoses with medical literature citations.

---

## System Overview

### Key Features

#### Triple-Modality Analysis
- **OpenCV Computer Vision**: Automated quantitative feature extraction with calibration
- **Vision Language Model**: Llama-3.2-11B-Vision-Instruct with DermatoLLama LoRA adapter
- **RAG System**: Medical literature retrieval and citation from dermatology abstracts and clinical guidelines

#### Comprehensive Analysis Output
- **5+ Ranked Differential Diagnoses** with likelihood levels
- **Quantitative Measurements**: Size, asymmetry, color distribution, border irregularity
- **Dermoscopic Structure Detection**: Blue-white veil, pigment network, globules, dots, vascular patterns
- **ABCDE Melanoma Risk Assessment**: Automated detection of risk factors
- **Evidence-Based Recommendations**: With medical literature citations
- **Confidence Scoring**: Uncertainty quantification for analysis reliability

#### Advanced Image Processing
- Automated hair artifact removal (black-hat morphological transform)
- K-means clustering for lesion segmentation with Otsu fallback
- Calibration system with ruler/coin reference detection
- Multi-color zone detection with spatial distribution analysis
- Border irregularity and texture pattern analysis
- Circularity and asymmetry scoring

---

## Quick Start

### Prerequisites
- Google Colab account (recommended) or local Jupyter environment
- HuggingFace account with access to `Llama-3.2-11B-Vision-Instruct`
- GPU runtime (T4 or better recommended)

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Akram-Toumi/Skin-Cancer-Analysis.git
cd Skin-Cancer-Analysis
```

2. **Open in Google Colab**
   - Upload `skin-cancer.ipynb` to Google Colab
   - Select GPU runtime: `Runtime → Change runtime type → GPU (T4)`

3. **Run Setup Cells** - Execute cells sequentially:
   - Cell 1: Install all dependencies
   - Cell 2: HuggingFace authentication
   - Cell 3: Build RAG system with medical literature
   - Cell 4: Load VLM model with quantization
   - Cell 5: Setup OpenCV pipeline
   - Cell 6: Launch Gradio interface

### Usage

1. **Upload Image**: PNG/JPG dermoscopic or clinical image
2. **Select Analysis Mode**:
   - ✅ OpenCV Enabled (Recommended): Automated feature extraction
   - ❌ OpenCV Disabled: Direct VLM analysis or manual measurements
3. **Adjust Parameters** (Optional):
   - Analysis tokens (512-2048)
   - Temperature (0.1-1.0)
   - Number of sources (1-10)
4. **Click "Analyze Lesion"**
5. **Review Results** across five tabs:
   - OpenCV Features
   - Dermoscopic Structures
   - Literature Sources
   - Evidence-Based Diagnosis
   - Confidence Report

---

## System Architecture

```
Input Image
    ↓
┌─────────────────────────────────┐
│   OpenCV Feature Extraction     │
│  • Hair removal                 │
│  • Lesion segmentation          │
│  • Calibrated measurements      │
│  • Dermoscopic structure detect │
└─────────────────────────────────┘
    ↓
┌─────────────────────────────────┐
│      RAG Medical Retrieval      │
│  • FAISS vector search          │
│  • PubMed abstracts             │
│  • Clinical guidelines          │
│  • Weighted relevance ranking   │
└─────────────────────────────────┘
    ↓
┌─────────────────────────────────┐
│   Vision Language Model (VLM)   │
│  • Llama-3.2-11B-Vision         │
│  • DermatoLLama LoRA adapter    │
│  • 4-bit quantization           │
│  • Multi-modal fusion           │
└─────────────────────────────────┘
    ↓
Evidence-Based Diagnosis Report
```

---

## Technical Details

### Models & Libraries

| Component | Model/Library |
|-----------|---------------|
| VLM | `meta-llama/Llama-3.2-11B-Vision-Instruct` (4-bit quantized) |
| LoRA Adapter | `DermaVLM/DermatoLLama-50k` |
| Embeddings | `sentence-transformers/all-MiniLM-L6-v2` |
| Vector Store | FAISS |
| Computer Vision | OpenCV, scikit-image |
| Framework | Transformers, LangChain, Gradio |

### Knowledge Base Sources
- **Medical Abstracts**: `TimSchopf/medical_abstracts` dataset (filtered for dermatology)
- **Clinical Guidelines**: ABCDE criteria, Breslow thickness staging, dermoscopic pattern analysis
- **Reference Documents**: Pigment network analysis, vascular patterns, blue-white veil significance

### OpenCV Feature Extraction

| Category | Features |
|----------|----------|
| **Morphology** | Area, perimeter, diameter, circularity, asymmetry score |
| **Color Analysis** | K-means clustering (4+ color zones), clinical color classification |
| **Spatial Distribution** | Central vs peripheral color patterns |
| **Border Assessment** | Irregularity score, definition quality |
| **Texture** | Variance analysis, edge density, pigmentation patterns |
| **Dermoscopy** | Blue-white veil, pigment network, globules, dots, vascular structures |
| **ABCDE Risk** | Automated melanoma risk factor detection |

### Computational Requirements

| Resource | Requirement |
|----------|-------------|
| RAM | 16GB minimum (Colab free tier sufficient) |
| GPU | T4 or better (provided by Colab) |
| Storage | ~30GB for model weights + datasets |
| Runtime | ~10 minutes setup, ~30-60 seconds per analysis |

---

## Output Structure

### 1. OpenCV Features Tab
```
DERMATOLOGICAL LESION ANALYSIS:

MORPHOLOGY:
- Size: Approximately X.X mm diameter, X.X mm² area
- Shape: [asymmetric/symmetric] with [regular/irregular] borders
- Border definition: [well-defined/poorly-defined]
- Overall circularity: X.XXX

COLOR ANALYSIS:
- Number of distinct color zones: X
- Color composition: [detailed breakdown with percentages]
- Spatial distribution: [central/peripheral/mixed]

SURFACE & TEXTURE:
- Pigmentation pattern: [reticular/irregular/homogeneous]
- Surface appearance: [smooth/textured/varied]

ABCDE RISK FACTORS:
⚠️ [Detected risk factors or "No major risk factors"]
```

### 2. Dermoscopic Structures Tab
```
DERMOSCOPIC STRUCTURE ANALYSIS:

BLUE-WHITE VEIL:
  ✅ PRESENT - Coverage: X.X%
  Distribution: [focal/diffuse]

PIGMENT NETWORK:
  Type: [Typical/Atypical/Broadened]
  Density: X.XXX

GLOBULES AND DOTS:
  Dots detected: X
  Globules detected: X

VASCULAR STRUCTURES:
  Pattern: [dotted/linear/polymorphous]
```

### 3. Evidence-Based Diagnosis Tab
```
1. DIFFERENTIAL DIAGNOSIS (Ranked by Likelihood)
   - [5+ diagnoses with likelihood levels]
   - Citations: [Source X], [Source Y]

2. CONCERNING FEATURES WITH EVIDENCE
   - [Specific quantitative features]
   - Clinical significance with citations

3. CLINICAL RECOMMENDATIONS
   - Urgency level: [Immediate/Urgent/Routine]
   - Next steps: [Specific actions]
   - Citations: [Source X]

4. PATIENT COMMUNICATION GUIDANCE
   - [Clear, compassionate explanation]
```

---

## Medical Disclaimer

> ⚠️ **This system is for research and educational purposes only.**
>
> - **NOT** a substitute for professional medical advice, diagnosis, or treatment
> - **NOT** FDA approved or clinically validated
> - Always consult a qualified dermatologist for medical decisions
> - Do not use for self-diagnosis or treatment planning
> - Intended for research, education, and tool development

---

## Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## Acknowledgments

- **Meta AI** for Llama-3.2-11B-Vision-Instruct
- **DermaVLM Team** for the DermatoLLama-50k adapter
- **Timothy Schopf** for the medical_abstracts dataset
- **Hugging Face** for model hosting and transformers library
- **Gradio** for the interactive interface framework

---

## Contact

For questions, issues, or collaboration:
- Open an issue on GitHub
- Email: [akram.toumi007@gmail.com]
---

⭐ If you find this project useful, please consider giving it a star!
