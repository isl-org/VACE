- Download models using huggingface-cli (Already done):
    ```
    pip install "huggingface_hub[cli]"
    huggingface-cli download ali-vilab/VACE-Annotators --local-dir /export/share/projects/videogen/vace/VACE-Annotators
    huggingface-cli download ali-vilab/VACE-Wan2.1-1.3B-Preview --local-dir /export/share/projects/videogen/vace/VACE-Wan2.1-1.3B-Preview
    ```
- Install dependencies (TODO).
    ```
    <!-- pip install -r requirements/annotator.txt -->
    ```
    I have cloned dependencies as, you can try `pip install -e .` if `pip install git+https` fails:
    ```
    https://github.com/isl-org/GroundingDINO
    https://github.com/isl-org/RAFT
    ```
    If sam2, segment-anything, recognize-anything are also needed, feel free to fork them to isl-org as well before adding them as submodules.
- Preprocess video.
    ```
    # process video depth
    python vace/vace_preproccess.py --task depth --video assets/videos/test.mp4
    # or
    python vace/gradios/vace_preprocess_demo.py
    ```
- Test Inference:
    ```
    python vace/vace_wan_inference.py --ckpt_dir /export/share/projects/videogen/vace/VACE-Wan2.1-1.3B-Preview --src_video assets/videos/test.mp4 --src_mask <path-to-src-mask> --src_ref_images <paths-to-src-ref-images> --prompt "xxx"
    ```

# Q&A
- ```
  UnboundLocalError: local variable 'Model' referenced before assignment.
  ```
  Missing groundingdino library.
  