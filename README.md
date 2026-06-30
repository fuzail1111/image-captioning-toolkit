# Image Captioning Toolkit

A small collection of tools that use Salesforce's **BLIP** (Bootstrapping Language-Image Pretraining) model to automatically generate natural-language captions for images. This project demonstrates three progressively more advanced ways of using a pretrained vision-language model: a single-image script, an interactive web app, and an automated web-scraping captioning pipeline.

## Project structure

```
image-captioning-toolkit/
├── src/
│   ├── caption_single_image.py   # Caption one local image from the command line
│   ├── caption_app.py            # Interactive Gradio web app for image captioning
│   └── caption_from_url.py       # Scrape a webpage, caption every image found, save results
├── examples/
│   └── sample_captions.txt       # Example output from caption_from_url.py
├── requirements.txt
└── README.md
```

## What each script does

### 1. `caption_single_image.py`
Loads a local image and generates a caption for it using BLIP.

```bash
python src/caption_single_image.py --image path/to/image.jpg
```

Example output:
```
the image of a man standing in front of a building
```

### 2. `caption_app.py`
A simple Gradio web app — upload or drag-and-drop any image in the browser and get an instant caption. Good for demoing the model interactively without writing any code.

```bash
python src/caption_app.py
```

This launches a local web server (Gradio will print a URL like `http://127.0.0.1:7860`) where you can test the model live.

### 3. `caption_from_url.py`
Given a webpage URL, this script scrapes every `<img>` tag on the page, downloads each image, filters out tiny/broken/SVG images, generates a caption for each one using BLIP, and writes all results to a text file.

```bash
python src/caption_from_url.py --url "https://en.wikipedia.org/wiki/IBM"
```

Example output (`captions.txt`):
```
https://upload.wikimedia.org/.../ibm_logo.png: the logo of a company
https://upload.wikimedia.org/.../building.jpg: a tall office building with glass windows
```

## Setup

1. Clone the repo:
   ```bash
   git clone https://github.com/<your-username>/image-captioning-toolkit.git
   cd image-captioning-toolkit
   ```

2. Create and activate a virtual environment:
   ```bash
   python -m venv my_env
   source my_env/bin/activate      # macOS/Linux
   my_env\Scripts\activate         # Windows
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Run any of the three scripts as shown above.

## Model used

[`Salesforce/blip-image-captioning-base`](https://huggingface.co/Salesforce/blip-image-captioning-base) — a pretrained vision-language model from Hugging Face that generates natural-language descriptions of images.

## What this project demonstrates

- Loading and running inference with a pretrained multimodal (vision + language) transformer model
- Building a simple, shareable interactive ML demo with Gradio
- Combining web scraping (`requests` + `BeautifulSoup`) with batch model inference to build a small end-to-end data pipeline
- Basic error handling for malformed/unsupported image formats during batch processing

## Possible next steps

- Add command-line arguments to all scripts for flexibility
- Add unit tests for the image filtering logic
- Deploy `caption_app.py` to Hugging Face Spaces for a live public demo
- Support batch captioning of a local folder of images

## License

MIT