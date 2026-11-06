# Chest X-ray Report Generation

A deep-learning project exploring automatic radiology report generation from paired frontal and lateral chest X-ray images. The repository contains two model implementations and their Gradio interface notebooks.

> **Research/educational use only.** This project is not a medical device and must not be used for diagnosis, treatment, or clinical decision-making. Generated text can be inaccurate, incomplete, or misleading and requires review by qualified clinicians.

## Project overview

### 1. CNN + Transformer

Located in [`model-cnn-transformer/`](model-cnn-transformer/).

- Uses separate CNN feature extractors for frontal and lateral X-ray views.
- Combines image features with a Transformer encoder.
- Uses a Transformer decoder to generate the report text.
- Includes BLEU and ROUGE evaluation code in the training notebook.
- Includes a Gradio interface notebook for inference.

Main files:

- `train.ipynb` — data preparation, training, and evaluation workflow.
- `gradio_app.ipynb` — inference interface.
- `tokenizer.json` and `text_preprocessing_config.json` — text preprocessing assets.

### 2. ResNet + GPT-2

Located in [`model-resnet-gpt2/`](model-resnet-gpt2/).

- Extracts visual features from frontal and lateral images using an ImageNet-pretrained ResNet backbone.
- Projects the visual features into a prefix consumed by GPT-2.
- Fine-tunes GPT-2 to generate radiology report text.
- Evaluates generated reports with BLEU and ROUGE metrics and includes an image-use sanity check.
- Includes a Gradio interface notebook.

Main files:

- `train.ipynb` — Kaggle-oriented training and evaluation workflow.
- `gradio_app.ipynb` — inference interface notebook.

## Repository contents and large files

To keep this Git repository lightweight, trained checkpoints, full datasets, generated prediction files, and intermediate arrays are **not included**.

Examples of excluded artifacts include:

- `best.pt` and model checkpoint/weight files (`.pt`, `.pth`, `.h5`, `.keras`).
- Dataset archives, image files, and CSV exports containing dataset records.
- Intermediate arrays such as `.npy` files.

Model checkpoints can be added later through a model-hosting service such as Hugging Face Hub. When they are published, add their download links and the exact expected filenames here. The GPT-2 inference notebook expects the trained checkpoint and its training-generated `config.json`; the CNN-Transformer interface expects its encoder/decoder checkpoints and tokenizer assets.

## Data

The notebooks expect paired frontal and lateral chest X-ray images and associated report text. The training notebooks contain the data-loading and preprocessing workflow, including the Kaggle dataset reference used by the CNN-Transformer implementation.

The dataset is not redistributed in this repository. Obtain access directly from the original dataset provider and comply with its terms, access controls, and data-use agreement. Do not upload patient images, reports, identifiers, or other restricted data to a public repository.

## Environment

The two implementations use different deep-learning stacks. It is recommended to run them in separate Kaggle or Google Colab environments rather than installing both stacks into one environment.

- CNN + Transformer: see [`model-cnn-transformer/requirements.txt`](model-cnn-transformer/requirements.txt).
- ResNet + GPT-2: see [`model-resnet-gpt2/requirements.txt`](model-resnet-gpt2/requirements.txt).

The ResNet + GPT-2 training notebook was prepared for a Kaggle GPU environment. Its first run may download pretrained GPT-2 and ImageNet ResNet weights and requires internet access.

## Running the notebooks

1. Open the relevant training notebook in Kaggle or Google Colab.
2. Attach or mount the dataset using the paths and instructions in the notebook.
3. Confirm that the required image files and report metadata are available.
4. Run the notebook cells in order.
5. Save the generated checkpoints and configuration files to your own storage.
6. To use the Gradio interface, provide the checkpoint paths and matching preprocessing/configuration files in the interface notebook.

Exact checkpoint filenames and paths may need to be adjusted to match your training run.

## Evaluation

Both training workflows include code for text-generation evaluation using BLEU and ROUGE. Report the actual held-out test results from a completed run here once the final metrics have been verified; no metric values are claimed in this repository yet.

## License and attribution

No license is currently specified for this repository. Dataset rights and model/checkpoint redistribution rights are separate from the code. Before publishing, verify the applicable dataset terms and the licenses of all pretrained components. Add a repository license only when you have the right to license the included material.
