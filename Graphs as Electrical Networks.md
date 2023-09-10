이 문서에서 벡터 $e_i$는 $i$번 원소만 $1$이고 나머지는 $0$인 벡터를 의미한다. 즉, 기본 단위벡터이다.
## 가중치 없는 그래프
### Incidence Matrix $B$
정점이 $n$개이고 간선이 $m$개인 가중치 없는 무향 그래프에서부터, 모든 간선에 임의로 방향을 준 그래프 $G = (V, E)$를 생각하자. 이때, **incidence matrix** $B \in {\left\{ -1,0,1 \right\}}^{m \times n}$은 다음과 같은 행렬이다.
- $B$의 행 번호는 $G$의 간선 번호로, 열 번호는 정점 번호로 인덱싱된다.
- $e$번 간선이 $u \rightarrow v$라면 $B_{eu} = 1$, $B_{ev} = -1$이며, $B$의 $e$번 행의 나머지 값은 전부 $0$이다.

그러면 incidence matrix는 아래 성질을 만족한다.
$$ B^T B = L $$
다르게 표현하면 아래와 같다.
$$ \sum_e B_{eu} B_{ev} = L_{uv} $$
### Current Vector $i$ and Voltage Vector $v$
가중치 없는 그래프는 모든 간선에 크기 $1$의 저항이 있는 회로에 대응된다.
이때 $i \in \mathbb{R}^m$과 $v \in \mathbb{R}^n$을 각각 간선의 전류와 정점의 전압에 대응시킬 수 있다.
또한 $c_{ext} \in \mathbb{R}^n$은 각 정점으로 들어가는 전류의 양을 의미한다.
### Electrical Networks and Laplacian System
키르히호프의 법칙은 아래와 같이 쓸 수 있다.
$$ B^T i = c_{ext} $$
옴의 법칙은 아래와 같이 쓸 수 있다.
$$ i = Bv $$
이 둘을 합치면 아래 식을 얻는다.
$$ B^T B v = Lv = c_{ext} $$
즉, Laplacian system을 얻는다.
### $\Pi$ Matrix
**$\Pi$ matrix**는 아래와 같이 정의된다.
$$ \Pi = B L^+ B^T $$
즉, $\Pi$는 각 원소가 아래와 같이 정의되는 $m \times m$ 행렬이다. 여기서 $B_e$는 $B$의 $e$번째 행벡터이다.
$$ \Pi_{fe} = B_f L^+ B_e^T $$
$\Pi_{fe}$는 $e$의 시작점에 $1$의 전류가 들어와서 $e$의 끝점으로 나가는 상황에서, $f$에 흐르는 전류이다.
특히, $\Pi_{ee}$는 간선 $e$에서의 **effective resistance $R_{\mathrm{eff}}(e)$**라고 부른다.
$\Pi$는 다음과 같은 특성을 갖는다.
- $\Pi = \Pi^T$
- $\Pi$는 projection matrix이다.
- $\Pi^2 = \Pi$
- $\Pi$의 eigenvalues 는 전부 $0$ 또는 $1$이다.
- $G$가 연결 그래프라면 $\mathrm{rank}(\Pi) = n-1$이다.
- $G$의 모든 스패닝 트리 중 하나를 균일한 확률로 하나 고른 것을 $T$라고 하자. 그러면, 어떤 간선 $e$가 $T$에 속할 확률은 $R_{\mathrm{eff}}(e)$이다.
### Electrical Flow $f^\star$
$1$만큼의 전류가 $s$번 정점으로 들어와서 $t$번 정점으로 나가는 상황을 **unit *s*-*t* flow**라고 한다. 때의 current vector $i$를 **electrical flow $f^\star$**라고 한다.
$$ f^\star = B L^+ (e_s - e_t) $$
Current vector (flow vector) $f$가 주어졌을 때, 이 전류 흐름이 소모하는 **에너지**는 아래와 같다.
$$ E(f) = \sum_e f_e^2 $$
즉 각 성분의 제곱의 합이다. $f = f^\star$일 땐 아래 식이 성립한다.
$$ E(f^\star) = (e_s - e_t)^T L^+ (e_s - e_t) $$
또한, $f^\star$는 **에너지 $E(f)$를 최소화**하는 $f$이다.
## 가중치 있는 그래프
$e$번 간선의 가중치를 $w(e)$라고 할 때, $m \times m$ 행렬인 **weight matrix** $W$는 다음과 같이 정의된다.
$$ W_{rc} = \delta_{rc} w(r)$$
**Incidence matrix** $B$는 동일하게 정의한다. 즉, 아래와 같이 정의한다.
- $B$의 행 번호는 $G$의 간선 번호로, 열 번호는 정점 번호로 인덱싱된다.
- $e$번 간선이 $u \rightarrow v$라면 $B_{eu} = 1$, $B_{ev} = -1$이며, $B$의 $e$번 행의 나머지 값은 전부 $0$이다.

그러면 incidence matrix는 아래 성질을 만족한다.
$$ B^T W B = L $$
**$\Pi$ matrix**는 아래와 같은 식을 만족한다.
$$ \Pi = W^{1/2} B L^+ B^T W^{1/2} $$
각 **간선의 저항**은 $r(e) = 1 / w(e)$로 설정한다. 그러면 옴의 법칙은 $i = WBv$로 쓸 수 있다.

Unit *s*-*t* flow에서의 **flow vector** $f^\star$는 아래와 같다.
$$ f^\star = W B L^+ (e_s - e_t) $$
에너지의 정의는 $E(f) = \sum r_e (f_e)^2$으로 바뀐다. 그러면 $f = f^\star$일 때의 에너지는 아래와 같다.
$$ E(f^\star) = (e_s - e_t)^T L^+ (e_s - e_t) $$