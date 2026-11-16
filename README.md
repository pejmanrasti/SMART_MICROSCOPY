# Smart Microscopy with AI — Practical Sessions


## Copy the materials into your Google Drive

Each TP has a shared folder with its data and pre-trained models.

Shared folder |
---|
https://drive.google.com/drive/folders/1yUZ9ifiKFdmjxZYX1eLmE30XEYx1NNO4?usp=sharing|

For the link:
1. Open the link while signed in to your Google account.
2. Click the folder name at the top of the page, then **Organize → Add shortcut**. (In some versions this is the "Add shortcut to Drive" icon.)
3. Choose **My Drive** and confirm.

The folder now appears in your **My Drive**. Note its exact name, because you will need it in the notebook.

> **Alternative:** download the folder as a ZIP, unzip it, and upload it to **My Drive**.

Please do this **before** the session. The TP1 files are fairly large.

----



Two hands-on sessions on how machine learning can help a microscope **see more** (predict a fluorescence image from a label-free one) and **act smarter** (decide where and how to illuminate the sample).

You don't need to be a programmer. Each notebook explains every step, and you only complete a few short lines marked **✏️ TODO**. Everything runs in your web browser with **Google Colab**: you need a Google account, nothing to install, and no GPU.

---

## TP1: From phase images to virtual fluorescence

**≈ 40 min, plus an optional 10 min part on uncertainty**

**Question:** can we predict a nuclear stain (Hoechst) from a label-free quantitative phase image (QPI) of living A549 cells, and how far can we trust that prediction?

You will compare three deep-learning approaches on **real microscopy data**:

| Model | What it learned from |
|---|---|
| **U-Net** | *Paired* images: the same cells imaged in phase **and** fluorescence |
| **CycleGAN** | *Unpaired* images: phase and fluorescence images from **different** fields of view, never matched |
| **Cytoland (VSCyto2D)** | A large published model, pre-trained by its authors and used as it is |

What you will do:
1. Look at the input phase images and the real fluorescence images.
2. Predict fluorescence with each model and compute the error yourself.
3. *(Optional)* Estimate how **uncertain** the U-Net is with *MC Dropout*, and check whether the uncertain pixels are also the wrong ones.
4. Score all three models (MAE, SSIM, Pearson correlation) and discuss: does the most *realistic-looking* image always give the most *biologically faithful* result?

The models are already trained, so you only use them.

## TP2: Learning to scan with reinforcement learning

**≈ 35 min, plus optional extensions (15 min + 10 min)**

**Question:** can a microscope *learn by trial and error* where to move and what to illuminate?

You will teach a virtual microscope with **Q-learning**, a simple reinforcement-learning method in which an agent learns from rewards and penalties.

- **Part A: moving the stage.** The microscope learns to navigate a 5 × 5 virtual sample and acquire an image at the region of interest found by a quick scout scan.
- **Part B (optional): smart illumination with a DMD.** A Digital Micromirror Device chooses which regions to illuminate. The agent must find hidden fluorescent targets while using as little light as possible, which limits photodamage.
- **Part C (optional): uncertainty-aware sampling.** The microscope keeps a probability map of where targets may be, measures its uncertainty, and chooses the illumination that is expected to teach it the most. You then compare this with the Q-learning agent.

TP2 uses a simulated microscope, so no real images are needed.

---

## During the session: open the notebook in Colab

1. Open the TP notebook in **Google Colab** (your instructor will show you how).
2. Connect Colab to your Google Drive by running this in the first cell, then accept the permission request:
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```
3. **TP1 only:** at the top of the notebook, set `DATA_FOLDER` to where the TP1 folder is in your Drive, for example:
   ```python
   DATA_FOLDER = "/content/drive/MyDrive/<name of the TP1 folder>"
   ```
4. Run the cells from top to bottom with `Shift + Enter`, and complete the **✏️ TODO** lines.

**If something goes wrong:**
- *"File not found"*: check that the folder name in `DATA_FOLDER` exactly matches the name in your Drive, including capital letters and spaces.
- *A cell shows an error after you restarted Colab*: run all the cells again from the top (**Runtime → Run before**).

---

### References
- Cytoland / VSCyto2D: [paper](https://doi.org/10.1038/s42256-025-01046-2) · [quickstart](https://virtualcellmodels.cziscience.com/quickstart/cytoland-quickstart)
- CycleGAN: [Zhu et al., 2017](https://arxiv.org/abs/1703.10593)
- Reinforcement learning: Sutton & Barto, *Reinforcement Learning: An Introduction* ([free online](http://incompleteideas.net/book/the-book-2nd.html))
