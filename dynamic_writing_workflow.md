# Paper Writing Workflow Prompt

这个文件用于下次写其他主题论文时直接阅读或复制给 Codex。目标是复用本次流程：静态 writing skills + 目标期刊动态 skill + 原稿小节重点 + 指定参考文献结构 + Word 输出。

## 1. 需要提前准备的材料

把所有材料放在同一个论文工作文件夹中，例如：

```text
F:\sunshine\paperwriting
```

至少准备：

```text
English.docx
Appendix.docx
reference\
reference\文中参考\
```

各文件含义：

- `English.docx`：论文母本。每个小节前应写清楚分析重点、对应结果、表格解释、重点参考文献。
- `Appendix.docx`：附录。放变量解释、计算过程、稳健性细节、补充表格、附录结果。
- `reference\`：目标期刊文章、背景参考文献、其他参考文献。
- `reference\文中参考\`：正文小节明确标注需要学习或引用的重点参考文献 PDF。

如果某个小节要模仿某篇文章，直接在 `English.docx` 对应小节写：

```text
REFERENCE: Author, Year, Title. 参考这篇文章的 X.X 小节结构和内容安排来写。
```

如果某个小节要参考某篇文章的解释方式，写：

```text
参考 Author Year 对某类结果的解释方式，来解释本文对应回归结果。
```

## 2. 推荐使用的静态 skills 组合

下次直接指定使用以下组合：

```text
writing/journal-adapt：生成目标期刊动态规则。
topjournal/econ-write：主静态经济学写作规则。
topjournal/econ-writing-workflow：全文结构、经济学论文流程、结果解释。
topjournal/econ-table-figure-design：表格、图、caption、notes、变量解释。
tworeview/academic-paper-reviewer：写完后做审稿式检查。
fullwrite/docfigure/docx：生成和修改 Word 文件。
fullwrite/humanizer/humanizer：最后做语言自然化、去 AI 味。
```

注意：

- `topjournal` 主要用于写作、结构和经济学表达。
- 真正的审稿 skill 是 `tworeview/academic-paper-reviewer`。
- 如果需要完整审稿，必须明确要求“运行 tworeview/academic-paper-reviewer 做完整审稿式检查”。

## 3. 推荐总 prompt

下次可以直接发送：

```text
此对话下的所有操作，都放在 "[论文工作文件夹]" 中。

我的目标期刊是：[目标期刊名称]。

请使用以下 skills 组合重新写作论文：
1. writing/journal-adapt：根据目标期刊参考文章生成动态写作规则；
2. topjournal/econ-write：作为主静态经济学写作规则；
3. topjournal/econ-writing-workflow：控制全文结构、经济学论文流程和结果解释；
4. topjournal/econ-table-figure-design：统一表格、图、caption、notes 和变量解释；
5. tworeview/academic-paper-reviewer：写完后进行审稿式检查；
6. fullwrite/docfigure/docx：生成和修改 Word 文件；
7. fullwrite/humanizer/humanizer：最后进行语言自然化，降低 AI 味。

我的论文母本是：
"[论文工作文件夹]\English.docx"

我的附录是：
"[论文工作文件夹]\Appendix.docx"

目标期刊参考文章和其他参考文献在：
"[论文工作文件夹]\reference"

正文中标注的重点参考文献 PDF 在：
"[论文工作文件夹]\reference\文中参考"

请先读取 English.docx 和 Appendix.docx，检查每个小节的分析重点、表格、变量解释、参考文献和附录信息是否足够。

然后生成或更新 dynamic_writing_skill.md。动态规则必须包含：
1. 每一小节先读 English.docx 中的分析重点、结果总述、表格说明和标注参考文献；
2. 每一小节如果指定了参考文献，就按该参考文献的结构或解释方式写；
3. 参考文献默认只读 abstract、introduction、conclusion；
4. 如果我指定“按某篇文章某一节写”，才读取该文对应小节；
5. 写结果前必须建立“表格-列-变量-系数-标准误-显著性-变量类型-解释单位”核对表；
6. 正文中的系数解释必须和表格一致；
7. 缺引用时保留 [CITE: 建议引用xxx，理由xxx]，不要编造正式引用；
8. 表格缺具体数值时，保留 [COEF]、[SE] 占位符，不编造数值；
9. 表格、caption、notes 按目标期刊格式统一。

请不要修改原始 English.docx 和 Appendix.docx。
正文请新建一个 Word 文件。
附录如需整理，也请新建一个 Word 文件。
```

## 4. dynamic skill 必须写入的通用规则

每次生成目标期刊 dynamic skill 时，都应加入以下硬规则。

### 4.1 Manuscript-first rule

写每一节前，必须先读 `English.docx` 中该小节的：

- 分析重点；
- 结果总述；
- 对应表格；
- 表格 notes；
- 图注；
- 指定参考文献；
- 作者备注。

目标期刊风格只能优化这些内容，不能替代作者原本的实证内容。

### 4.2 Section-specific reference rule

如果某一小节标注了参考文献，该参考文献不是普通背景文献，而是该小节的结构或解释模板。

使用方式：

- robustness：学习参考文献如何组织稳健性小节；
- mechanism：学习参考文献如何解释机制结果；
- heterogeneity：学习参考文献如何解释异质性；
- welfare / discussion：学习参考文献如何从结果过渡到经济含义；
- introduction：学习参考文献如何安排研究问题、数据、结果、贡献。

不能复制参考文献的事实、结论和句子。只能学习结构和表达方式。

### 4.3 Reading rule for references

默认只读：

- abstract；
- introduction；
- conclusion。

只有当作者明确要求“按某篇文章某一节写”时，才读对应小节。

例子：

```text
REFERENCE: Cui et al. (2025). 参考 4.2 Robustness checks 写。
```

此时只需要额外读取 Cui et al. (2025) 的 robustness 小节。

### 4.4 Citation placeholder rule

不要擅自添加正式引用。

需要引用但未确认时，用：

```text
[CITE: suggested reference - reason]
```

例子：

```text
[CITE: Oster, 2019 - coefficient-stability test for omitted-variable bias]
[CITE: Huang et al., 2026 - local income effects and reallocation toward low-skilled services]
```

## 5. 结果解释硬规则

写任何 regression results 前，先建立核对表：

```text
Table
Column
Dependent variable
Variable type
Coefficient
Standard error
Significance
Correct interpretation
```

变量解释规则：

- log 因变量：解释为百分比变化。
- 0-1 分类变量：解释为概率变化或百分点变化。
- 0-1 比例变量：解释为百分点变化。
- 0-100 百分比变量：解释为百分点变化，但数值不能乘 100。
- resilience / index / score：解释为指标值变化，除非脚本明确说明可转为百分比。
- variance / burden / inequality / risk：必须结合变量含义解释方向，负系数可能代表改善。
- 不显著结果：不能写成有效影响。
- 表格没有具体数值：只写方向，保留 `[COEF]`、`[SE]` 占位符。

禁止：

- 把 0.046 的 0-1 变量写成提高 4.6%；
- 把负向 fuel burden 写成福利下降；
- 只照搬原稿解释而不核对表格；
- 表中无数值时编造系数。

## 6. 全文写作顺序

推荐顺序：

```text
1. 更新 dynamic_writing_skill.md
2. 读取 English.docx 和 Appendix.docx
3. 读取目标期刊参考文章
4. 读取小节指定参考文献
5. 建立章节-表格-参考文献索引
6. 写 Introduction
7. 写 Background
8. 写 Data and empirical strategy
9. 写 Event study
10. 写 Baseline results
11. 写 Robustness checks
12. 写 Mechanisms
13. 写 Heterogeneity
14. 写 Welfare / spillovers
15. 写 Conclusion
16. 统一表格、caption、notes
17. 生成新的 Word 文件
18. 用 tworeview/academic-paper-reviewer 做审稿式检查
19. 用 humanizer 做语言自然化
20. 输出修改说明和剩余 TODO
```

## 7. 表格和 notes 规则

每张表都应有：

- table title；
- column description；
- dependent variable explanation；
- variable unit；
- fixed effects；
- controls；
- clustering level；
- observation explanation；
- significance stars explanation。

英文统一使用：

```text
Notes:
```

不要混用：

```text
注：
NOTES:
Note:
```

如果目标期刊常用 `Notes:`，统一用 `Notes:`。

## 8. 附录整理 prompt

下次整理附录时可以直接发送：

```text
采用 fullwrite/docfigure/docx 等 docx 处理 skills，
将 "[论文工作文件夹]\Appendix.docx" 整理成英文，格式统一。

要求：
1. 不修改原始 Appendix.docx；
2. 新建一个英文附录 Word；
3. 中文正文全部英文化；
4. 表格表头和变量名英文化；
5. 表格 notes 统一为 Notes:；
6. 标题层级统一为 Appendix A, A.1, A.2；
7. 字体统一为 Times New Roman；
8. 检查中文残留；
9. 保留所有表格和原始数值，不改系数、标准误、显著性。
```

## 9. 完成后的自检清单

生成 Word 后必须检查：

```text
原始 English.docx 是否未被修改
原始 Appendix.docx 是否未被修改
新 Word 是否成功生成
段落数和表格数是否合理
是否还有中文残留
是否还有旧模板词，如 PSH、firm output 等
是否有表格没有 notes
是否有 0-1 变量被误写成百分比
是否有 log 变量未解释为百分比
是否有不显著结果被写成显著影响
是否有 [COEF]、[SE]、[CITE] 等占位符需要后续补充
```

## 10. 本次生成文件示例

本次输出过的文件：

```text
F:\sunshine\paperwriting\English_ERE_rewritten_full_draft.docx
F:\sunshine\paperwriting\Appendix_English_formatted.docx
F:\sunshine\paperwriting\English_revised\dynamic_writing_skill.md
```

其中：

- `English_ERE_rewritten_full_draft.docx` 是正文新版；
- `Appendix_English_formatted.docx` 是英文附录新版；
- `dynamic_writing_skill.md` 是针对 Environmental and Resource Economics 与本篇文章生成的动态规则。

换文章或换期刊时，应重新生成新的 `dynamic_writing_skill.md`，不要直接套用旧的。

