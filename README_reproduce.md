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
    ```
    pip install groundingdino@git+https://github.com/IDEA-Research/GroundingDINO
    pip install wan@git+https://github.com/Wan-Video/Wan2.1
    pip install raft@git+https://github.com/isl-org/RAFT
    ```
    If sam2, segment-anything, recognize-anything are also needed, feel free to use the submodule cloned from this fork `git@github.com:isl-org/sam2.git` from video gen distillation github repo.
- Preprocess video.
    ```
    # process video depth
    python vace/vace_preproccess.py --task depth --video assets/videos/test.mp4
    # or
    python vace/gradios/vace_preproccess_demo.py
    ```
- Test Inference:
    - Inference with bbox.
    ```
    python vace/vace_pipeline.py --base wan --task inpainting --mode bbox --bbox 50,50,550,700 --video assets/videos/test.mp4 --prompt 'two cats are boxing on stage.'
    ```
    - Inference with videos of images and masks.
    ```
    python vace/vace_wan_inference.py --ckpt_dir /export/share/projects/videogen/checkpoints/vace/VACE-Wan2.1-1.3B-Preview --src_video /export/share/projects/videogen/data/davis/train/bear/rgb_right_0.05.mp4 --src_mask /export/share/projects/videogen/data/davis/train/bear/mask_0.05.mp4 --prompt "a brown bear is walking in a rocky area."
    ```

# Q&A
- ```
  UnboundLocalError: local variable 'Model' referenced before assignment.
  ```
  Missing groundingdino library. This can be fixed by installing GroundingDINO first.