# CRTBP.jl

お互いに万有引力が作用する３つの天体がどのような運動をするのかを問う問題を**三体問題**（Three-Body Problem)と呼ぶ．三体問題は，その軌道を与える一般解が求積法では求まらない問題として知られており（＝要は，ある時刻に対する位置・速度を解析的な式で計算できない），宇宙軌道力学の分野でも数値解法が用いられる．三体問題の中でも，第三天体が及ぼす万有引力を無視した問題を**制限三体問題**(Restricted Three-Body Problem)と呼び，更に，第一天体と第二天体がその共通重心の周りを円軌道で周回する問題を**円制限三体問題** (Circular Restricted Three-Body Problem; CRTBP)と呼ぶ．宇宙軌道力学分野でよく対象となる「太陽＝地球＝宇宙機の三体問題」や「地球＝月＝宇宙機の三体問題」は，CRTBPで非常によく近似できる．よく近似できるとは言え，あくまで近似であり，実際の宇宙機運用を考えると無視できない誤差が生じる．それにも関わらず，なぜ軌道力学の専門家が，CRTBPを使いたがるかと言うと，CRTBPの運動方程式は，**自励系**（＝独立変数を陽に含まない常微分方程式）となっているからである．自励系で表されることで，力学系理論等の解析的なテクニックを利用することが可能となる．

CRTBPでは，第一天体と第二天体の共通重心を中心として，第一天体から見た第二天体の位置ベクトル方向を $x$軸，第一天体に対する第二天体の角運動量ベクトル方向を $z$軸，右手系をなすように $y$軸（＝第二天体の速度ベクトル方向）を取った座標系において，運動方程式を記述することが多い．詳しい導出は書略するが，宇宙機の位置ベクトルを $\boldsymbol{r}$，速度ベクトルを $\boldsymbol{v}$，運動方程式を規定するパラメータを $\mu=\frac{m_2}{m_1+m_2}$としたとき，CRTBPにおける宇宙機の運動方程式は，以下のような式で計算できる

$$
\left\{
\begin{align*}
\dot{\boldsymbol{r}} &= \boldsymbol{v}\\
\dot{\boldsymbol{v}} &= -\frac{1-\mu}{\|\boldsymbol{r}_1\|^3}\boldsymbol{r}_1 -\frac{\mu}{\|\boldsymbol{r}_2\|^3}\boldsymbol{r}_2 + H_{\textrm{coli}}\boldsymbol{v} + H_{\textrm{cf}}\boldsymbol{r}
\end{align*}
\right.
$$

ただし，

$$
\begin{align*}
\boldsymbol{r}_1 &= \begin{bmatrix}x+\mu & y & z\end{bmatrix}^{\top}\\
\boldsymbol{r}_2 &= \begin{bmatrix}x-(1-\mu) & y & z\end{bmatrix}^{\top}\\
H_{\textrm{coli}} &= \begin{bmatrix}
0 & 2 & 0\\
-2 & 0 & 0\\
0 & 0 & 0
\end{bmatrix}\\
H_{\textrm{cf}} &= \begin{bmatrix}
1 & 0 & 0\\
0 & 1 & 0\\
0 & 0 & 0
\end{bmatrix}
\end{align*}
$$

である． $m_1$と $m_2$は，それぞれ第一天体と第二天体の質量を表すが，太陽＝地球系のCRTBPでは $\mu=3.036\times 10^{-6}$，地球＝月系のCRTBPでは $\mu=0.01215058426994$である．
