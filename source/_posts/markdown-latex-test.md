---
title: Markdown 與 LaTeX 渲染測試
date: 2026-09-05 15:30:00
categories:
  - 測試
tags:
  - markdown
  - latex
mathjax: true
---

這篇文章用來測試各種 Markdown 語法和 LaTeX 數學公式的渲染效果。

<!-- more -->

## 1. Markdown 基本語法

### 文字樣式

**粗體**、*斜體*、***粗斜體***、~~刪除線~~、`行內程式碼`、[連結](https://hexo.io/)。

### 清單

- 無序清單一
  - 巢狀項目
- 無序清單二

1. 有序清單一
2. 有序清單二

### 引用

> 這是一段引用文字。
> 可以很多行。

### 表格

| 語法 | 說明 | 支援 |
| ---- | ---- | ---- |
| `**粗體**` | 粗體 | ✅ |
| `$x^2$` | 行內公式 | ✅ |

### 程式碼區塊

```python
def fib(n: int) -> int:
    a, b = 0, 1
    for _ in range(n):
        a, b = b, a + b
    return a

print([fib(i) for i in range(10)])
```

### 任務清單

- [x] 支援 Markdown
- [ ] 支援 LaTeX
- [ ] 部署成功

## 2. LaTeX 數學公式

### 行內公式

質能方程 $E = mc^2$ 是物理學最有名的公式之一，其中 $c \approx 3 \times 10^8 \,\text{m/s}$。

### 區塊公式

歐拉恆等式：

$$
e^{i\pi} + 1 = 0
$$

二次公式求解：

$$
x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}
$$

### 矩陣

$$
A = \begin{pmatrix} a & b \\ c & d \end{pmatrix}, \quad
\det(A) = ad - bc
$$

### 對齊多行公式

$$
\begin{aligned}
f(x) &= (x+1)^2 \\
     &= x^2 + 2x + 1 \\
     &\geq 0
\end{aligned}
$$

### 求和與積分

$$
\sum_{i=1}^{n} i = \frac{n(n+1)}{2}, \qquad
\int_0^\infty e^{-x} \, dx = 1
$$

### 希臘字母與符號

$\alpha, \beta, \gamma, \theta, \lambda, \pi, \sigma, \omega$ 以及 $\forall x \in \mathbb{R}, \; \exists \varepsilon > 0$。