# Changelog

## 2026-03-18

### Environment Setup
- Fixed venv shebang paths: USB drive mount changed from `708E1F058E1EC40E1` to `708E1F058E1EC40E2`, updated 97 files in `.venv/bin/` and `pyvenv.cfg`

### Training
- Reduced `batch_size` from 16 to 2 in `configs/train_act.yaml` to fit RTX 4060 (8GB VRAM)
- Trained ACT policy for 30K steps on `top_long_merged` dataset (loss: 4.226 → 0.266)
- Checkpoints saved at 5K intervals in `outputs/train/act_top_long/checkpoints/`

### Docker
- Added `--shm-size=16g` to resolve PyTorch DataLoader shared memory error
- Added `--entrypoint /bin/bash` to override Isaac Sim default entrypoint
- Required volume mounts: `Datasets`, `configs`, `Assets`, `outputs`
- Required `xhost +local:docker` and X11/Xauthority forwarding for display

### Evaluation
- Ran headless evaluation with video saving (2 episodes x 12 garments)
- Results: **29.17% success rate**, avg return 142.43 ± 53.54
- Best garments: Top_Long_Seen_1 (100%), Top_Long_Seen_4 (100%)
- Videos saved to `outputs/eval_videos/success/` and `outputs/eval_videos/failure/`

### Docker Run Scripts
- `/tmp/docker_eval.sh` — headless eval with video saving
- `/tmp/docker_eval_gui.sh` — GUI mode (requires >8GB VRAM)
- `/tmp/docker_eval_live.sh` — WebRTC livestream mode (port 8011)

### .gitignore
- Added `get-docker.sh` and `*.tar.gz`
