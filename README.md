# 文献库说明

本目录使用 BibTeX 的 `.bib` 文件。三个文件之间的关系如下：

## 环境配置

这是一个纯 BibTeX 文献库，不包含 Python、Conda、LaTeX 工程或其他运行时
依赖。维护和校验只需要能够处理 UTF-8 文本和 BibTeX 的工具；如果将文献库
接入其他论文项目，应以目标论文项目自己的 TeX 和 BibTeX 版本为准。

| 文件 | 条目数 | 用途 |
| --- | ---: | --- |
| `refs_all.bib` | 351 | 总文献库，是另外两个分类库的条目并集。 |
| `refs_published.bib` | 331 | 已正式出版的期刊与会议论文，以及书籍、学位论文、技术报告和网页等非预印本来源。 |
| `refs_preprints.bib` | 20 | 尚未检索到正式期刊或会议论文集记录的预印本。 |

## 并集约束

`refs_all.bib` 必须满足：

```text
keys(refs_all.bib)
  = keys(refs_published.bib) union keys(refs_preprints.bib)

keys(refs_published.bib) intersection keys(refs_preprints.bib)
  = empty set
```

除文件头注释和排列顺序外，`refs_all.bib` 中每个条目的内容必须与其所属分类文件中的条目一致。三个文件内均不允许出现重复 citation key。

## 分类规则

- 有正式期刊、会议论文集、出版社页面或正式 DOI 的论文归入 `refs_published.bib`。
- 仅有 arXiv、bioRxiv、medRxiv、SSRN 或 TechRxiv 等预印本记录，且没有正式出版信息的论文归入 `refs_preprints.bib`。
- 仅标注为 accepted、under review、submitted，或只有会议日程而没有正式论文集记录的条目，暂归入 `refs_preprints.bib`。
- `eprint` 字段可能只是出版社提供的 PDF 链接，不能单独作为预印本判据。
- 同一会议或期刊在三个文献库中必须使用一致的规范名称和字段类型。
- 书籍、学位论文、技术报告、政策文件和网页资料不是预印本，为保证总库完整性，统一保存在 `refs_published.bib`。

## 维护方式

1. 新增或更新文献时，只编辑对应的分类文件。
2. 根据 citation key 合并两个分类文件，重新生成 `refs_all.bib`；不要独立编辑总库。
3. 生成后检查条目数量、重复 key、交集和缺失项，并运行 BibTeX 语法检查。

当前校验关系为 `351 = 331 + 20`，两个分类库之间没有重复 key。
