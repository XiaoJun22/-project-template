# 新项目初始化检查清单

> 本文档随模板仓库一起分发，使用 GitHub/GitLab "Template Repository" 功能创建新项目后，
> 请对照本清单逐项确认，避免遗留模板残留配置导致后期问题。

---

## 使用方式（方案一：Git Template Repo）

1. 在模板仓库（如 `motor-fw-template`）的平台设置中启用 **Template Repository**
   - GitHub: `Settings → General → Template repository` 勾选
   - GitLab: 新建项目时选择 "Create from template"，或将本仓库加入群组模板列表
2. 新项目通过 **"Use this template"**（GitHub）或对应入口创建，会生成全新仓库，
   不携带模板的 commit 历史，保持干净起点。
3. clone 新仓库到本地后，按下方清单逐项检查/修改。
4. 全部完成后，将本文件中已勾选项提交一次 commit，作为项目初始化的记录。

---

## 检查清单

### 基础信息
- [ ] 项目名称已替换（README.md、CLAUDE.md 标题、MDK工程名 `.uvprojx`）
- [ ] `01_docs/需求规格说明书.md` 已替换为本项目实际需求，不是模板占位内容
- [ ] git remote 已指向新项目仓库地址，而非模板仓库（`git remote -v` 确认）

### 硬件相关
- [ ] `MDK-ARM/` 工程的 **Device（芯片型号）** 已确认/更换为实际使用的MCU
- [ ] MDK工程的 Flash/RAM 起始地址、大小配置已核对
- [ ] `02_library/` 里的厂商 HAL 库版本已确认匹配新MCU型号（不同MCU家族HAL库不通用）
- [ ] `02_hardware/` 原理图、PCB、BOM 是否需要从参考设计导入或从零开始，已明确

### 软件参数
- [ ] `05_app/system_param.h`（或对应参数文件）里的硬件参数（引脚定义、PWM频率、
      ADC通道映射等）已清空模板旧值，待按新硬件填写
- [ ] `03_bsp/` 下外设初始化代码（GPIO/PWM/ADC/I2C）已核对是否匹配新硬件引脚分配
- [ ] 恒流/保护阈值等控制参数（如有模板默认值）已标记为"待确认"，不能直接用于新项目

### 工程配置
- [ ] `.gitignore` 已确认覆盖：
  - [ ] `MDK-ARM/Listing/`
  - [ ] `MDK-ARM/Objects/`
  - [ ] `*.uvoptx`
  - [ ] `*.uvguix.*`
- [ ] `MDK-ARM/*.uvprojx` 中的源文件路径引用（相对路径）在新项目结构下可正常编译
- [ ] 空目录占位文件 `.gitkeep` 是否需要保留或可删除（有实际文件后可删除对应.gitkeep）

### 文档与记录
- [ ] `CHANGELOG.md`（如有）已重置为空/初始版本
- [ ] `06_management/项目计划.md`、`风险登记表.md` 已按新项目重新填写，不是模板样例数据
- [ ] `06_management/变更记录_ECN/` 目录已清空模板历史记录（如有）
- [ ] `CLAUDE.md` 中项目特定描述（如项目背景、当前阶段）已更新，分层规范部分可保留不变

### 编译验证
- [ ] 新项目在完成上述修改后，可以成功完整编译一次（哪怕功能未实现，先验证工程配置无误）
- [ ] 编译产物（.hex/.bin）已确认输出路径正确，未来交付走 `05_output/固件_bin/`

---

## 完成后

全部勾选完成后，建议：
```bash
git add NEW_PROJECT_CHECKLIST.md
git commit -m "chore: complete project initialization checklist"
```
作为该项目已完成初始化的记录，便于后续追溯。
