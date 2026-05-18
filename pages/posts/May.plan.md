---
title: 五月计划
date: 2026-05-01
updated: 2026-05-2
categories: 计划
copyright: false
tags:
  - 规划
top: 1
---
- [ ] 检查毕设实验正常运行
- [ ] 整理不同领域mem方法
- [ ] mem-rmbench跑现有方法并整理
- [ ] mem-rmbench修改baseline
- [ ] 继续关注分层

<mark style="background-color: #fef3c7; color: #92400e; padding: 0 4px; border-radius: 4px;">这里是认知黄高亮</mark>

<mark style="background-color: #dcfce7; color: #166534; padding: 0 4px; border-radius: 4px;">这里是淡绿色高亮</mark>

<mark style="background-color: #e0f2fe; color: #0369a1; padding: 0 4px; border-radius: 4px;">这里是概念蓝高亮</mark>

<mark style="background-color: #f3e8ff; color: #6b21a8; padding: 0 4px; border-radius: 4px;">这里是理论紫高亮</mark>

<mark style="background-color: #ccfbf1; color: #0f766e; padding: 0 4px; border-radius: 4px;">这里是数据青高亮</mark>

<mark style="background-color: #f1f5f9; color: #334155; padding: 0 4px; border-radius: 4px;">这里是实验灰高亮</mark>

<mark style="background-color: #ffe4e6; color: #be123c; padding: 0 4px; border-radius: 4px;">这里是警示粉高亮</mark>

```bash [token]
# modelscope
ms-6b6ac6eb-1f59-4dec-9638-6878e25c4f67
# wandb
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
```

```bash [ssh]
# 连接地址: js4.blockelite.cn
# 端口: 16828
# 用户: root / vipuser
# 密码: mu3Aixag
ssh root@js4.blockelite.cn -p 16828

# 连接地址: js1.blockelite.cn
# 端口: 33212
# 用户: root / vipuser
# 密码: JaCh3Eed
ssh root@js1.blockelite.cn -p 33212
```

```bash [pi-train]
# data process
cd /mnt/data3/RMBench/policy/pi05
source .venv/bin/activate
uv run python scripts/process_data.py {$task} demo_clean 50
uv run examples/aloha_real/convert_aloha_data_to_lerobot_robotwin.py \
    --raw_dir processed_data/{$task}-demo_clean-50 \
    --repo_id {$task}_demo_clean_50
uv run scripts/compute_norm_stats.py --config-name  pi05_aloha_full_base
bash finetune.sh pi05_aloha_full_base {$task}_50 0
bash eval.sh {$task} demo_clean pi05_aloha_full_base {$task}_50 0 0
```