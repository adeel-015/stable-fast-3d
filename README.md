## 🛠️ Offline Setup & Packaging Documentation (Internship Task)

### Task 1: Install and Run Stable Fast 3D Offline

#### **Step-by-Step Setup**

1. **Clone the Repository**
    ```bash
    git clone https://github.com/Stability-AI/stable-fast-3d.git
    cd stable-fast-3d
    ```

2. **Set Up a Virtual Environment**
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. **Download All Dependencies for Offline Use**
    - Download all required packages for offline installation:
      ```bash
      pip install --upgrade pip
      pip download -r requirements.txt -d offline_pkgs
      ```
    - Install from local wheels (offline):
      ```bash
      pip install --no-index --find-links=offline_pkgs -r requirements.txt
      ```

4. **Download Model Files**
    - Use the Hugging Face Hub to download model files:
      ```python
      from huggingface_hub import snapshot_download
      snapshot_download(repo_id='stabilityai/stable-fast-3d', repo_type='model')
      ```
    - Copy `model.safetensors` and `config.yaml` from the Hugging Face cache to your project’s `models/` directory.

5. **Test Offline Functionality**
    - Disconnect from the internet.
    - Run the main script:
      ```bash
      python run.py demo_files/examples/chair1.png --output-dir output/
      ```
    - Confirm that the script runs and produces output without needing internet access.

---

#### **Challenges Faced & Solutions**

- **Large Dependencies:**  
  *Challenge:* Downloading and bundling large packages like `torch` and `transformers` can be slow and error-prone.  
  *Solution:* Used `pip download` to pre-fetch all wheels and installed from a local directory.

- **Model File Location:**  
  *Challenge:* Locating the downloaded model files in the Hugging Face cache.  
  *Solution:* Used the `find` command to locate files and copied them to a known `models/` directory.

- **Resource Path Handling:**  
  *Challenge:* Ensuring the script finds model files both in development and when bundled.  
  *Solution:* Added a `resource_path` function in `run.py` to handle both normal and bundled execution.

- **Offline Testing:**  
  *Challenge:* Verifying true offline capability.  
  *Solution:* Disconnected network and ran the script, confirming no downloads or network calls occurred.

---

#### **Key Lessons Learned**

- Always test in a fully offline environment to catch hidden dependencies.
- Use local wheels and local model files for reproducibility and speed.
- Automate repetitive steps (e.g., model download, dependency download) for easier onboarding.
- Document every manual step for future maintainers and users.

---

#### **Optimizations & Improvements**

- Added a `resource_path` utility to make the code robust for both development and packaged execution.
- Created an `offline_pkgs/` directory for all dependencies, making setup faster and more reliable.
- Documented the process clearly for future users.

---

#### **Demonstration**

- **Screenshots/video:**  
  - ![Dir](https://i.postimg.cc/cHgF5d91/temp-Image-Fcttv-W.avif)
  - [![Demo](https://img.youtube.com/vi/D60LXnhX-Q4/maxresdefault.jpg)](https://youtu.be/D60LXnhX-Q4)

---

#### **Quick Offline Setup Reference**

```markdown
## Quick Offline Setup

1. Clone the repo and enter the directory.
2. Create and activate a virtual environment.
3. Install dependencies from `offline_pkgs/`.
4. Ensure `models/model.safetensors` and `models/config.yaml` are present.
5. Run:
   ```
   python run.py demo_files/examples/chair1.png --output-dir output/
   ```
6. No internet required after setup!
```
