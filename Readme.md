[toc]

# 1 项目结构说明
```
|- build（构建文件夹，Latex 编译后的结果会放在这里）
   |- ...（编译文件）

|- sections（章节目录，每个人负责的章节在这里编写，被 VR-Lab.tex 文件引用，一起编译）
   |- 1-introduction.tex（第 1 章内容在此编写，一起负责）
   |- 2-related_work.tex（第 2 章内容在此编写，李亦航负责）
   |- 3-method.tex（第 3 章内容在此编写，纪海林负责）
   |- 4-user_study.tex（第 4 章内容在此编写，张怡冉负责）
   |- 5-result.tex（第 5 章内容在此编写，张怡冉负责）
   |- 6-conclusion.tex（第 6 章内容在此编写，一起负责）

|- images（将图片存放在该目录下）
   |- fig1-eps-converted-to.pdf（样例 tex 中使用到的图片，在 latex 中，图片需要转为 pdf 插入，这样编译速度会很快）

|- history.txt（包的版本历史记录）

|- llncs.cls（LaTeX2e 文档类）

|- llncsdoc.pdf（该文档类的说明文档 PDF 版本）

|- mybibliography.bib（所有的参考文献写在这里，在正文中进行引用）

|- samplepaper.tex（样例 tex，文章格式模板参考这个文件）

|- splncs04.bst（参考文献的格式文件）

|- VR-Lab.tex（我们的 tex，在这里编写总文章）
```

# 2 Latex 使用流程
## 2.1 认识整篇文章：VR-Lab.tex

VR-Lab.tex 内包含了整篇文章，打开 VR-Lab.tex 查看注释并了解文章结构：

1. 引用格式模板（不修改）
2. 标题、作者、联系方式等内容（各自添加自己的信息）
3. 摘要和关键词（最后一起修改）
4. 引入章节内容（不修改，而是在 sections 目录下每人修改自己负责的章节 tex）
5. 参考文献（不修改，而是修改 mybibliography.bib 文件，在文中 \cite{...} 进行引用）

文章结构：
```
|- VR-Lab.tex
   |- 1-introduction.tex（章节引用）
   |- 2-related_work.tex
   |- 3-method.tex
   |- 4-user_study.tex
   |- 5-result.tex
   |- 6-conclusion.tex

   |- mybibliography.bib（参考文献引用）
```

## 2.2 编写每人负责的章节：sections 目录

sections 目录存放了每章的内容，被 VR-Lab.tex 引用。我们只需要在每个章节 tex 写自己负责的内容即可，不需要修改其他人的文件，这样做到明确分工。

目前计划：
- 李亦航：2-related_word.tex
- 纪海林：3-method.tex
- 张怡冉：4-user_study.tex、5-result.tex

文章结构仅是初版，章节的文件名称可以自行修改，修改后记得更改 VR-Lab.tex 中对应的引用文件名。
![](https://raw.githubusercontent.com/zheliku/TyporaImgBed/main/ImgBed/202506180242117.png)
其他部分内容最后一起填写。

## 2.3 项目编译
配置你的 latex，教程见：<https://blog.csdn.net/zheliku/article/details/146968842>。

注意事项：

1. 确保你的 latex 输出路径为"./build"，以免破坏项目结构。
   
   将设置文件中的"latex-workshop.latex.outDir"设置为"./build"（详见教程 3.2 节）
   ![](https://raw.githubusercontent.com/zheliku/TyporaImgBed/main/ImgBed/202506180229077.png)

2. 编译时，首先打开主文件 VR-Lab.tex，再选择此编译链："xelatex -> bibtex -> xelatex*2"，这样才能正确引用参考文献。详细原理请见教程 3.3 节。

   ![](https://raw.githubusercontent.com/zheliku/TyporaImgBed/main/ImgBed/202506180234077.png)

   此外，也可以选择 LaTeXmk 进行编译，LaTeXmk 会自动识别是否需要 bibtex，只需运行一次，它会自动帮你做好所有事情。

   上述 2 种方式选一种即可，编译后参考文献引用格式没问题就行。

3. 编译时，观察左下角的图标，如果为√，则编译成功。否则点击左侧查看命令行提示。

   ![](https://raw.githubusercontent.com/zheliku/TyporaImgBed/main/ImgBed/202506180239366.png)

# 3 关于写作
## 3.1 图片引用
参考 samplepaper.tex 中 98-103 行，下面详细解释如何在 LaTeX 中插入和引用图片：

```latex
\begin{figure} % 开始插入图片的环境
    \includegraphics[width=\textwidth]{images/fig1-eps-converted-to.pdf} % 插入图片，width=\textwidth 表示图片宽度与正文一致，图片路径为 images 文件夹下
    \caption{A figure caption is always placed below the illustration.
    Please note that short captions are centered, while long ones are
    justified by the macro package automatically.} % 图片标题，显示在图片下方
    \label{fig1} % 设置图片标签，方便在正文中引用
\end{figure} % 结束图片环境
```

**使用说明：**
- 图片文件需放在 `images` 文件夹下，需要提前转换为 PDF 格式以加快编译速度。
- `\includegraphics` 命令用于插入图片，`width` 参数可调整图片大小。
- `\caption{}` 用于添加图片说明，简短标题会居中，较长标题会自动对齐。
- `\label{}` 设置图片标签，便于在正文中引用，例如：`如图~\ref{fig1}~所示`。
- 插入图片时建议放在合适的段落位置，避免图片与正文内容错位。

实际引用图片的例子如下：

```latex
如图~\ref{fig1}~所示，……
```

这样可以在文中自动引用对应图片的编号。

如果遇见有子图 (a)、(b) 的情况，可网上搜索查找 latex 引用子图的方法，然后一起交流讨论，告诉大家一声。也可以更新此文档，大家一起查看使用。目前我还没有查阅。

## 3.2 参考文献引用
在 mybibliography.bib 文件中添加文章信息即可，就像这样：
![](https://raw.githubusercontent.com/zheliku/TyporaImgBed/main/ImgBed/202506180259352.png)

这是每篇论文的 bib 引用格式，可以在谷歌学术网站中搜索文章，直接复制粘贴进来。
![](https://raw.githubusercontent.com/zheliku/TyporaImgBed/main/ImgBed/202506180300418.png)

![](https://raw.githubusercontent.com/zheliku/TyporaImgBed/main/ImgBed/202506180301127.png)

以该文献为例：
```bib
@article{luo2020dream,
  title={Dream-experiment: a MR user interface with natural multi-channel interaction for virtual experiments},
  author={Luo, Tianren and Zhang, Mingmin and Pan, Zhigeng and Li, Zheng and Cai, Ning and Miao, Jinda and Chen, Youbin and Xu, Mingxi},
  journal={IEEE Transactions on Visualization and Computer Graphics},
  volume={26},
  number={12},
  pages={3524--3534},
  year={2020},
  publisher={IEEE}
}
```
其中，@article{luo2020dream, ...} 是一个期刊论文（article）类型的文献，luo2020dream 是该文献的引用标识符（cite key），用于在 LaTeX 文档中引用。

在正文中需要引用该文献的地方，写：
```
...如文献\cite{luo2020dream}所述...
```

在 VR-Lab.tex 中，part 5 部分导入了 mybibliography.bib 文件，并设置了引用格式。编译后即可正确引用，无需管参考文献的编号顺序与引用格式。

## 3.3 其他
其他格式，例如：

- 公式
- 段落
- 表格

等，大家查看 samplepaper.tex 模仿即可。如果没有样例参考，则一起讨论。

# 4 注意事项

注意每次写之前 git 拉取查看其他成员的更新内容。
写完之后记得 git 提交，保持 github 端是最新版。
