# SO-ARM101 抓取红块数据集（round4 · 固定朝向）

SO-ARM101 六轴机械臂「抓取红色方块并放到目标盒」真机遥操作数据集，用于 wall-oss / ACT 等 VLA 模型微调。

## 规模
- **71 episodes / 17360 帧**，12fps（每集约 245 帧 ≈ 20s）
- 双相机：global（ASC60C）+ wrist（W19），各 640×480
- 6 维关节：`shoulder_pan, shoulder_lift, elbow_flex, wrist_flex, wrist_roll, gripper`

## 格式
LeRobot **v2.1** 格式（`codebase_version: v2.1`）：
- `meta/info.json` — 数据集元信息（features / fps / 关节名）
- `data/chunk-000/episode_*.parquet` — 每帧的 observation.state / action / 时间戳
- `videos/chunk-000/observation.images.{global,wrist}/episode_*.mp4` — 相机视频

## 单位约定
- 关节 1-5：lerobot 归一化 ±100（标定范围百分比）
- gripper：0..100（0=全闭，100=全开）
- 相机 key：`observation.images.global` / `observation.images.wrist`（**无 `.rgb` 后缀**）

## 用途
- wall-oss-0.5 LoRA 微调（本项目 round4 训练数据）
- 任何 lerobot 兼容的 ACT / diffusion / VLA 训练

## 质检
已过 QA 门禁：肘跨集 std ≥10、夹爪覆盖开合（2.7~80.4）、0 NaN / 越界。
