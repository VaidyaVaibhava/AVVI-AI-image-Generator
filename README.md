# Fast Text-to-Image Generation Web App

An efficient, single-step/few-step text-to-image generator powered by
**SDXL Turbo**, with an interactive **Gradio** web interface running in
Google Colab.

Generate images from text prompts in just **1--4 inference steps**,
using a distilled diffusion model optimized for fast generation.

------------------------------------------------------------------------

## 🚀 Project Overview

This project provides an end-to-end text-to-image generation pipeline.
It uses **SDXL Turbo** (`stabilityai/sdxl-turbo`) through Hugging Face
Diffusers and exposes the generator through a simple Gradio interface.

Unlike traditional diffusion workflows that may require dozens of
inference steps, SDXL Turbo can produce images quickly with a small
number of steps. This project uses a 512 × 512 output size,
`num_inference_steps=4`, and `guidance_scale=0.0` for fast generation.

## ✨ Features

-   **Fast image generation:** Create images in 1--4 inference steps.
-   **Text-to-image pipeline:** Turn natural-language prompts into
    generated images.
-   **Interactive web UI:** Generate images through a Gradio interface.
-   **Google Colab support:** Run the project in a hosted notebook
    environment.
-   **GPU acceleration:** Uses CUDA when a compatible GPU runtime is
    available.
-   **Hugging Face authentication:** Reads the access token from Google
    Colab Secrets.

## 🛠️ Tech Stack

-   **[PyTorch](https://pytorch.org/):** Tensor operations and GPU
    execution.
-   **[Diffusers](https://github.com/huggingface/diffusers):** Loads and
    runs the text-to-image diffusion pipeline.
-   **[Transformers](https://github.com/huggingface/transformers):**
    Supporting model and text-processing components.
-   **[Accelerate](https://github.com/huggingface/accelerate):** Helps
    with efficient model loading and execution.
-   **[Gradio](https://www.gradio.app/):** Builds the interactive web
    interface.
-   **[Hugging Face Hub](https://huggingface.co/docs/huggingface_hub):**
    Provides model access and authentication.
-   **[Google Colab](https://colab.research.google.com/):** Notebook
    environment for running the app with GPU access.

## 🧠 Model

This project uses **[SDXL
Turbo](https://huggingface.co/stabilityai/sdxl-turbo)** from Stability
AI.

-   **Model ID:** `stabilityai/sdxl-turbo`
-   **Pipeline:** `AutoPipelineForText2Image`
-   **Precision:** FP16 (`torch.float16`) for reduced GPU memory usage
    on supported hardware
-   **Typical image size:** 512 × 512 pixels
-   **Inference steps:** 4
-   **Guidance scale:** 0.0

Image quality and generation time can vary depending on the prompt, GPU,
and runtime configuration.

## 🏗️ System Flow & Architecture

1.  **Dependency setup**\
    Install the required libraries in the Google Colab notebook.

2.  **Authentication**\
    Retrieve the Hugging Face access token from Colab Secrets using the
    key `HF_TOKEN`. Keep the token private and do not hard-code it into
    the notebook or repository.

3.  **Model loading**\
    Load `stabilityai/sdxl-turbo` using `AutoPipelineForText2Image` and
    FP16 precision.

4.  **GPU deployment**\
    Move the pipeline to the CUDA device when a compatible GPU runtime
    is available.

5.  **Image generation**\
    The `generate_image` function accepts a text prompt and generates an
    image with the configured inference settings.

6.  **Gradio interface**\
    Launch the Gradio app inside Colab and optionally create a public
    share link.

## ▶️ How to Run

### 1. Open the notebook

Open the project notebook in Google Colab.

### 2. Enable GPU

In Colab, open **Runtime → Change runtime type** and select a GPU
runtime, such as T4, L4, or A100 when available.

### 3. Configure the Hugging Face token

1.  Create or obtain a Hugging Face access token with the permissions
    required to access the model.
2.  In Google Colab, open the **Secrets** panel using the key icon.
3.  Add a secret named `HF_TOKEN`.
4.  Enable notebook access for the secret.

Never publish your access token or commit it to Git.

### 4. Run the notebook cells

Execute the cells in order to install dependencies, authenticate, load
the model, define the generation function, and launch the interface.

### 5. Generate images

Enter a descriptive prompt in the Gradio interface and submit it. The
generated image should appear in the output area.

### 6. Open the share link

If the notebook launches Gradio with sharing enabled, open the generated
`.gradio.live` URL to use the interface in a separate browser tab. Treat
public share links as accessible to anyone who has the link, and stop
the app when you no longer need it.

## 💻 Example Generation Settings

``` python
image = pipe(
    prompt,
    num_inference_steps=4,
    guidance_scale=0.0,
    height=512,
    width=512,
).images[0]
```

Use the same settings in your `generate_image` function if they match
the implementation in your notebook.

## 📦 Dependencies

The notebook uses these main Python packages:

``` bash
pip install torch diffusers transformers accelerate gradio huggingface_hub
```

For Google Colab, PyTorch is often preinstalled. If you install or
upgrade it manually, choose a version compatible with the active CUDA
runtime.

## ⚙️ Requirements

-   A Google account with access to Google Colab
-   A GPU-enabled Colab runtime recommended for practical generation
    speed
-   A Hugging Face access token stored as the `HF_TOKEN` Colab Secret
-   Internet access to download the model and required packages
-   Sufficient GPU memory for the selected model and configuration

CPU execution may be substantially slower than GPU execution.

## 🔐 Security Notes

-   Store `HF_TOKEN` in Colab Secrets rather than directly in notebook
    code.
-   Do not upload tokens, credentials, or other secrets to GitHub.
-   Remember that a Gradio public share URL may allow other people to
    access the running app.
-   Stop the Gradio server and disconnect the runtime when finished.

## ⚠️ Limitations

-   Generation speed depends on the GPU and current Colab availability.
-   SDXL Turbo is optimized for a small number of inference steps;
    increasing the step count does not guarantee better results.
-   Generated content may contain visual artifacts or inaccuracies.
-   The model's output is influenced by prompt wording and the model's
    capabilities.

## 📁 Suggested Project Structure

``` text
fast-text-to-image/
├── README.md
└── notebook.ipynb
```

Replace `notebook.ipynb` with the actual name of your Colab notebook if
you download it into the repository.

## 📄 License

Review the model's license and terms on the [SDXL Turbo Hugging Face
page](https://huggingface.co/stabilityai/sdxl-turbo), along with the
licenses of the libraries used, before distributing or deploying the
project.

------------------------------------------------------------------------

Built with **SDXL Turbo**, **Hugging Face Diffusers**, and **Gradio**.
