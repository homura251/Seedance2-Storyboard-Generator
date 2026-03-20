---
name: seedance-storyboard-generator
description: Convert stories, novels, articles, folklore, or rough plot ideas into production-ready Seedance 2.0 storyboard packages. Use when Codex needs to adapt narrative material into episodic AI video scripts, break a story into 15-second episodes, generate character/scene/prop image prompts, prepare Seedance timeline prompts, or maintain continuity across a multi-episode video series.
---

# Seedance Storyboard Generator

Expert AI script and storyboard generation system for creating professional AI video series on Seedance 2.0 platform.

## Workflow

Follow this sequential process to convert source material into production-ready video scripts.

### 1. Analyze Input

Determine input type:
- Full text: complete novel or article requiring adaptation and episode segmentation
- Outline: brief story concept requiring full script development
- Partial draft: story notes or unfinished script that still needs structure

Extract core elements:
- protagonist and key characters
- central conflict and narrative arc
- setting and world-building elements
- key plot points and emotional beats

Ask clarifying questions if the input is ambiguous or materially incomplete. If the user does not specify production parameters, assume sensible defaults and state them.

If the input is prose and needs heavy adaptation before storyboarding, read [references/故事转视频脚本-转换工具.md](references/故事转视频脚本-转换工具.md) before drafting the episode plan.

### 2. Confirm Production Parameters

Ask for or assume these parameters:

1. Visual style: 写实 / 动画 / 水墨 / 科幻 / 复古 / 电影感 / other
2. Duration: total runtime or episode count. Default to 20 episodes x 15 seconds if the user wants a series but gives no length.
3. Target platform: aspect ratio such as 16:9, 9:16, or 2.35:1
4. Tone: 史诗 / 温馨 / 悬疑 / 欢快 / 忧伤 / other

Document these parameters and apply them consistently throughout the output.

### 3. Generate Four-Act Script Structure

Structure the story as:
- Act 1 起: Episodes 1-5, introduction and inciting incident
- Act 2 承: Episodes 6-10, rising action and complications
- Act 3 转: Episodes 11-15, climax and confrontation
- Act 4 合: Episodes 16-20, resolution and conclusion

For each episode include:
- episode number and title
- duration, default 15 seconds
- emotional tone or mood
- key plot points
- beginning frame description
- ending frame description for continuity

Output this section as a clean Markdown document with clear headers.

### 4. Create Asset Generation Plan

Categorize and number all visual assets:

| Category | Prefix | Example | Description |
|----------|--------|---------|-------------|
| Characters | C01-C99 | C01 叶青云·正面全身 | Multiple angles per character |
| Scenes | S01-S99 | S01 青锋山废墟 | Key locations |
| Props | P01-P99 | P01 青锋剑 | Important objects |

Reuse the same ID whenever the same character, scene, or prop reappears.

Write image-generation prompts in English after a stable style prefix.

Use this format:

```md
### [编号] - [名称]

[Style prefix], [detailed visual description in English], [technical specs]
```

Keep characters visually distinct with color, silhouette, costume, and signature props so they remain recognizable in the chosen art style.

### 5. Generate Seedance 2.0 Storyboard Scripts

For each episode, produce:

1. Asset upload list
2. Seedance prompt in time-axis format
3. Ending frame description for next-episode continuity

Use this prompt structure:

```text
[style]，[aspect ratio]，[overall mood]

0-3s画面：[镜头运动]，[场景建立]，[主体引入]
3-6s画面：[镜头运动]，[情节发展]，[动作描述]
6-9s画面：[镜头运动]，[高潮或冲突]，[情绪爆发]
9-12s画面：[镜头运动]，[转折或反应]
12-15s画面：[镜头运动]，[结尾或落版]

【声音】[配乐风格] + [音效] + [对白或旁白]
【参考】@图片1 [用途]，@图片2 [用途]
```

Use these camera movement keywords when helpful: 推镜头, 拉镜头, 摇镜头, 移镜头, 跟镜头, 环绕镜头, 升降镜头, 希区柯克变焦, 一镜到底, 手持晃动。

For episode chaining from episode 2 onward, start with `将@视频1延长15s` when the user wants to extend the previous clip instead of generating a fresh one.

Read [references/seedance-manual.md](references/seedance-manual.md) when you need Seedance prompt templates, multimodal syntax, camera patterns, platform limits, or wording patterns for specific scene types.

## Output Files

Generate these deliverables unless the user asks for a different packaging:

1. `[Title]_剧本.md` - complete four-act script with episode breakdown
2. `[Title]_素材清单.md` - all character, scene, and prop generation prompts
3. `[Title]_E[XX]_分镜.md` - individual episode storyboard scripts, or one combined storyboard file if the user prefers

## Validate before finishing

- Verify every `@图片X` or `@视频X` reference maps to a listed asset.
- Verify episode-to-episode continuity by matching each ending frame to the next opening frame.
- Verify the time axis covers the full clip duration without gaps.
- Verify the same style prefix is used across all image prompts.
- Respect common platform limits:
  - at most 9 reference images
  - at most 3 reference videos
- Avoid overly long or instruction-heavy prompts when Seedance starts ignoring parts of the request.

## Common Pitfalls to Avoid

- Avoid sensitive wording that can trigger platform rejection.
- Avoid style drift between episodes and asset prompts.
- Avoid missing ending-frame notes, because they break continuity.
- Avoid overloading a single prompt with too many simultaneous instructions.
