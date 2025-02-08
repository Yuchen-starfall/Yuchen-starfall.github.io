---
title: Latex
date: 2024-12-14 14:33
categories: Foundation of programming
tags:
    - "Latex"
    - "Programe"
    - "Mathematical formula"
mathjax: true
excerpt: false
---

**LaTeX**是一种用于高质量排版的文档编写语言，特别适合处理复杂的数学公式、科学文献和技术文档。它通过代码描述文档的结构和内容，然后生成排版精美的输出。

许多 Markdown 工具和平台支持嵌入 LaTeX 语法，特别是用于数学公式的部分。你可以通过 $ 或 $$ 包裹 LaTeX 代码来实现

## 希腊字母

```markdown
$$
\delta,\lambda\\
\Delta,\Lambda\\
\phi,\varphi\\
\epsilon,\varepsilon
$$

```

$$
\delta,\lambda\\
\Delta,\Lambda\\
\phi,\varphi\\
\epsilon,\varepsilon
$$

| 字母名称 | 大写 | markdown | 小写 | markdown |
| -------- | ---- | -------- | ---- | -------- |
| alpha    | A    | A        | α    | \alpha   |
| beta     | B    | B        | β    | \beta    |
| gamma    | Γ    | \Gamma   | γ    | \gamma   |
| delta    | Δ    | \Delta   | δ    | \delta   |
| epsilon  | E    | E        | ϵ    | \epsilon |
| zeta     | Z    | Z        | ζ    | \zeta    |
| eta      | E    | E        | η    | \eta     |
| theta    | Θ    | \Theta   | θ    | \theta   |
| iota     | I    | I        | ι    | \iota    |
| kappa    | K    | K        | κ    | \kappa   |
| lambda   | Λ    | \Lambda  | λ    | \lambda  |
| Mu       | M    | M        | μ    | \mu      |
| nu       | N    | N        | ν    | \nu      |
| xi       | Ξ    | \Xi      | ξ    | \xi      |
| omicron  | O    | O        | ο    | \omicron |
| pi       | Π    | \Pi      | π    | \omicron |
| rho      | P    | P        | ρ    | \rho     |
| sigma    | Σ    | \Sigma   | σ    | \sigma   |
| tau      | T    | T        | τ    | \tau     |
| upsilon  | Υ    | \Upsilon | υ    | \upsilon |
| phi      | Φ    | \Phi     | ϕ    | \phi     |
| chi      | X    | X        | χ    | \chi     |
| psi      | Ψ    | \Psi     | ψ    | \psi     |
|          |      |          | ε    | \varepsilon|
|          |      |          | φ    | \varphi  |

## 上下标

注意斜体与罗马题数字使用 例如

$x_i$：$i=1,2,\cdots,n$,为变量

$x_{\rm i}$：$\rm i$为“input”，输入值，为普通文本

$\text e,\text i,\text j$:自然对数底数，虚数单位为常量

```markdown
$$
a_1,a^2\\
90\degree\\
x^{y+z},p_{ij}\\
x_i,x_{\rm i}\\
\text e,\text i,\text j
$$
```

$$
a_1,a^2\\
90\degree\\
x^{y+z},p_{ij}\\
x_i,x_{\rm i}\\
\text e,\text i,\text j
$$

## 分式与跟式

```markdown
$$
\frac {1} {2}\\
\frac 1 {x+y}\\
\frac {\frac 1 2} {x+y}
\sqrt 2\\
\sqrt {\frac 1 {x+y}}\\
\sqrt [3]{x}
$$
```

$$
\frac {1} {2}\\
\frac 1 {x+y}\\
\frac {\frac 1 2} {x+y}
\sqrt 2\\
\sqrt {\frac 1 {x+y}}\\
\sqrt [3]{x}
$$

## 普通运算符

```markdown
$$
+-\\
\times,\sdot,\div\\
\pm,\mp\\
<>\\
\ge,\le\\
\gg,\ll\\
\ne,\approx,\equiv\\
\cap,\cup\\
\in,\notin\\
\subset,\subseteq,\subseteqq,\subsetneqq\\
\varnothing,\\
\forall,\exists,\nexists\\
\because,\therefore\\
\mathbb R,\R,\Q,\N,\Z_+\\
\mathcal F,\mathscr F\\
\cdots,\vdots,\ddots\\
\infty,\partial,\nabla,\propto,\degree
\sin x ,\cos x,\\cosh x\\
\log_2{x},\ln x,\lg x\\
\lim_\limits {x \to 0} \frac x {\sin x}\\
\max_\limits {x \to 0}
$$
```

$$
+-\\
\times,\sdot,\div\\
\pm,\mp\\
<>\\
\ge,\le\\
\gg,\ll\\
\ne,\approx,\equiv\\
\cap,\cup\\
\in,\notin\\
\subset,\subseteq,\subseteqq,\subsetneqq\\
\varnothing,\\
\forall,\exists,\nexists\\
\because,\therefore\\
\mathbb R,\R,\Q,\N,\Z_+\\
\mathcal F,\mathscr F\\
\cdots,\vdots,\ddots\\
\infty,\partial,\nabla,\propto,\degree
\sin x ,\cos x,\\cosh x\\
\log_2{x},\ln x,\lg x\\
\lim_\limits {x \to 0} \frac x {\sin x}\\
\max_\limits {x \to 0}
$$

## 大型运算符

```markdown
$$
\sum,\prod\\
\sum_{i = 0}^{N}\\
\frac{\sum_\limits {i = 0}^{n} x_i} {\prod_\limits {i = 0}^{n} x_i}
\int,\iint,\iiint,\oint,\oiint\\
\int_{-\infty}^0 f(x)\,\rm dx
$$
```

$$
\sum,\prod\\
\sum_{i = 0}^{N}\\
\frac{\sum_\limits {i = 0}^{n} x_i} {\prod_\limits {i = 0}^{n} x_i}
\int,\iint,\iiint,\oint,\oiint\\
\int_{-\infty}^0 f(x)\,\rm dx
$$

注意间隔区别`\,`

```markdown
$$
a\,a\\
a\ a\\
a\quad a\\
a\qquad a
$$
```

$$
a\,a\\
a\ a\\
a\quad a\\
a\qquad a
$$

## 标注符号

```markdown
$$
\vec x,\overrightarrow {AB}\\
\bar x,\overline {AB}\\
\hat{a}\\
\widetilde{a}\\
\dot{a}\\
\ddot{a}\\
$$
```

$$
\vec x,\overrightarrow {AB}\\
\bar x,\overline {AB}\\
\hat{a}\\
\widetilde{a}\\
\dot{a}\\
\ddot{a}\\
$$

## 箭头

```markdown
$$
\leftarrow,\longleftarrow,\rightarrow,\longrightarrow,\Leftarrow,\Rightarrow\\
\Leftrightarrow,
$$
```

$$
\leftarrow,\longleftarrow,\rightarrow,\longrightarrow,\Leftarrow,\Rightarrow\\
\Leftrightarrow,
$$

## 括号与定界符

```markdown
$$
\{\}\\
\lceil,\rceil,\lfloor,\rfloor\\
\left(0,\frac 1 a\right]\\
\left.\frac {∂f} {∂x} \right|_{x = 0}
$$
```

$$
\{\}\\
\lceil,\rceil,\lfloor,\rfloor\\
\left(0,\frac 1 a\right]\\
\left.\frac {∂f} {∂x} \right|_{x = 0}
$$

## 多行公式

```markdown
$$
\begin{align}

a&=b+c+d\\
&=e+f

\end{align}
$$
```

$$
\begin{align}

a&=b+c+d\\
&=e+f

\end{align}
$$

## 大括号

```markdown
$$
f(x)=

\begin{cases}
 
 \sin x,& -\pi \le x \le \pi\\
 0,& \text {other}
 
\end{cases}
$$
```

$$
f(x)=

\begin{cases}
 
 \sin x,& -\pi \le x \le \pi\\
 0,& \text {other}
 
\end{cases}
$$



## 矩阵

```
$$
\begin{matrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{matrix}
$$

$$
\begin{bmatrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{bmatrix}
$$

$$
\begin{pmatrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{pmatrix}
$$

$$
\begin{vmatrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{vmatrix}\
$$

$$
\bf A,\bf B^{\rm T}
$$
```

$$
\begin{matrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{matrix}
$$


$$
\begin{bmatrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{bmatrix}
$$


$$
\begin{pmatrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{pmatrix}
$$


$$
\begin{vmatrix}

a & b & \cdots & c \\
\vdots & \vdots & \ddots & \vdots \\
e & f & \cdots & g

\end{vmatrix}
$$


$$
\bf A,\bf B^{\rm T}
$$
