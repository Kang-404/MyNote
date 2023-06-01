# 信号与系统复习

## 傅里叶变换

### 典型信号的傅里叶变换

- 单边指数信号
  $$
  f(t) = e^{-at}u(t), a>0
  $$

  $$
  F(w) = \dfrac{1}{a+jw}
  $$

- 单位冲激信号
  $$
  f(t) = \delta(t)
  $$

  $$
  F(w) = 1
  $$

  

- 单位阶跃信号
  $$
  u(t) = \dfrac{1}{2} + \dfrac{1}{2}sgn(t)
  $$

  $$
  \mathscr{F}(u(t)) = \pi\delta(t) + \dfrac{1}{jw}
  $$

  

### 傅里叶变换的性质

- 线性

- 对偶性

  若$ \mathscr{F}[f(t)] = F(w) $, 则
  $$
  \mathscr{F}[F(t)] = 2\pi f(-w)
  $$
  

- 展缩性质

  若$ \mathscr{F}[f(t)] = F(w) $, 则
  $$
  \mathscr{F}[f(at)] = \dfrac{1}{|a|} F(\dfrac{w}{a})
  $$
  

- 时移特性

  若$ \mathscr{F}[f(t)] = F(w) $, 则
  $$
  \mathscr{F}[f(t-t_0)]=e^{-jwt_0}F(w)
  $$
  

- 频移特性

  若$ \mathscr{F}[f(t)] = F(w) $, 则
  $$
  \mathscr{F}[f(t)e^{jw_0t}]=F(w-w_0)
  $$
  

- 时域卷积定理

  若$ \mathscr{F}[f_1(t)] = F_1(w),\mathscr{F}[f_2(t)] = F_2(w) $, 则
  $$
  \mathscr{F}[f_1(t) \ast f_2(t) ]= F_1(w)\cdot F_2(w)
  $$
  

- 频域卷积定理

  若$ \mathscr{F}[f_1(t)] = F_1(w),\mathscr{F}[f_2(t)] = F_2(w) $, 则
  $$
  \mathscr{F}[f_1(t) \cdot f_2(t) ]= \dfrac{1}{2\pi}F_1(w)\ast F_2(w)
  $$
  

- 时域积分性质

  若$ \mathscr{F}[f(t)] = F(w) $, 则
  $$
  \mathscr{F}[\int_{-\infty}^{t} f(\tau)d\tau]=\dfrac{F(w)}{jw} + \pi F(0)\delta(w)
  $$
  

- 时域微分特性

  若$ \mathscr{F}[f(t)] = F(w) $, 则
  $$
  \mathscr{F}[\frac{d}{dt}f(t)]=jwF(w)
  $$

- 频域微分性质

  若$ \mathscr{F}[f(t)] = F(w) $, 则
  $$
  \mathscr{F}[-jtf(t)] = \frac{d}{dw}F(w)
  $$
  

常用公式：
$$
e^{at}\delta ^\prime (t) = \delta ^\prime (t) - a \delta(t)
$$




## 拉普拉斯变换

### 典型信号的拉普拉斯变换

| 序号 | 信号$f(t)$      | 拉普拉斯变换$F(s)$          |
| ---- | --------------- | --------------------------- |
| 1    | $\delta(t)$     | $1$                         |
| 2    | $u(t)$          | $\frac{1}{s}$               |
| 3    | $e^{at}u(t)$    | $\frac{1}{s+a}$             |
| 4    | $cos(w_0t)u(t)$ | $\frac{s}{s^2+w_0^2}$       |
| 5    | $sin(w_0t)u(t)$ | $\frac{w_0}{(s+a)^2+w_0^2}$ |



### 拉普拉斯变换的性质

| 序号 | 时域（t>0）                      | s域                                             |
| ---- | -------------------------------- | ----------------------------------------------- |
| 1    | $K_1f_1(t)+K_2f_2(t)$            | $K_1F_1(s)+K_2F_2(s)$                           |
| 2    | $\frac{d^2}{dt^2}f(t)$           | $s^2F(s)-sf(0_-)-f^\prime (0_-)$                |
| 3    | $\int_{-\infty}^{t}f(\tau)d\tau$ | $\frac{F(s)}{s}+\frac{f^{(-1)}(0)}{s}$          |
| 4    | $f(t-t_0)u(t-t_0)$               | $e^{-st_0}F(s)$                                 |
| 5    | $e^{-at}f(t)$                    | $F(s+a)$                                        |
| 6    | $f(at),a>0$                      | $(1/a)F(s/a),a>0$                               |
| 7    | $(-t)^{n}f(t)$                   | $\frac{d^n}{ds^n}F(s)$                          |
| 8    | $\frac{f(t)}{t}$                 | $\int_{s}^{+\infty}F(v)dv$                      |
| 9    | $f_1(t) \ast f_2(t)$             | $F_1(s)F_2(s)$                                  |
| 10   | 初值定理                         | $f(0_+)= \lim_{s \to \infty}sF(s)$              |
| 11   | 终值定理                         | $\lim_{t \to +\infty}f(t)= \lim_{s \to 0}sF(s)$ |