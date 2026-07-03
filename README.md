# 🧠 Attention-Based BCI

A Brain–Computer Interface (BCI) that reads EEG-captured brain-wave samples and predicts
whether the user **intended to press the spacebar**. Built around **ATCNet**, an attention-based
convolutional network for EEG motor-imagery classification.

## Team
- **Aran**
- **Raz**

## Project Description
The system ingests EEG samples of recorded brain waves and outputs a binary decision —
*spacebar-click intended* vs. *not intended*. It preprocesses the raw signal, trains and
evaluates the model per subject, and saves the trained model for downstream application.

## Repository Structure
| Path | Purpose |
|------|---------|
| `ATC_NET/` | Main, actively-maintained model, preprocessing, training & evaluation |
| `sanity_labs/` | Sanity checks on simpler models — *no longer maintained* |
| `neural_net_demo/` | First model attempt — *no longer maintained* |
| `information_and_documentation/` | Notes, issues, and cluster/run instructions |

## Model
- **ATCNet** — attention-based temporal convolutional network for EEG classification,
  adapted from [Altaheri/EEG-ATCNet](https://github.com/Altaheri/EEG-ATCNet).
- Dataset: Nathanel Zur's EEG experiment. <!-- TODO: add dataset download link -->
- Pipeline: preprocess → train → test → evaluate (accuracy, loss, confusion matrix, ROC).

## Installation
```bash
git clone https://github.com/RazMagal/Attention-Based-BCI.git
cd Attention-Based-BCI
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt
```

## Usage
1. Add your own EEG recordings, or download the subject data matrices from the dataset link
   into `ATC_NET/Zurs_Dataset/subjects/<subject_id>/`.
2. Run the aggregation step to assemble the per-subject data matrices.
3. Run the training / evaluation entry point in `ATC_NET/` (see
   `information_and_documentation/` for cluster run instructions).

## License
GNU GPL
