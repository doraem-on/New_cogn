# Assignment 9 · Vision-based cognitive assistants

Open [the executed notebook](main.ipynb) to see a bottle label transcribed and a portrait analyzed. The final cells check the labeled fields and exercise the blank-image, no-face and multiple-face cases.

## Run the lab

Use Python 3.12 and install the Tesseract executable with English language data. On macOS use `brew install tesseract`. On Ubuntu use `sudo apt install tesseract-ocr tesseract-ocr-eng`.

From the repository root run

```sh
cd assignment9
python3.12 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt jupyterlab
python -m jupyterlab main.ipynb
```

Select the environment's Python kernel and run all cells. The first expression run downloads two checksum-verified OpenCV Zoo models (about 5 MB total) into `.models/`. Later runs can work offline. Change the two image paths in the notebook to try a cropped English bottle label or a single front-facing portrait.

The optional LandingAI cell uploads the selected label for parsing when you enable it and supply a `VISION_AGENT_API_KEY` in the environment. The default run processes both images locally. [LandingAI Parse API](https://docs.landing.ai/ade/ade-quickstart)

## Example inputs

- `examples/demo-label.png` is a fictional teaching label. Its printed fields provide a known reference for checking OCR.
- `examples/astronaut.png` is NASA's public-domain photograph of Eileen Collins, distributed by scikit-image. [Image provenance](https://scikit-image.org/docs/stable/api/skimage.data.html#skimage.data.astronaut)
- The detector and classifier use pretrained OpenCV Zoo weights. The notebook uses five facial landmarks to align the crop before expression classification. [YuNet](https://github.com/opencv/opencv_zoo/tree/main/models/face_detection_yunet) · [Facial expression recognition](https://github.com/opencv/opencv_zoo/tree/main/models/facial_expression_recognition)
