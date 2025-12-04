# CH 3
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">AI 애플리케이션을 개발하는 데 큰 난관은 <b>평가 <i>Evaluation&nbsp;</i></b>이다.</p>
<p data-ke-size="size16">3장에서는 개방형 모델 평가에 사용되는 다양한 방법과 작동 원리, 한계를 다룬다.&nbsp;</p>
<p data-ke-size="size16">다음 장에서는 이런 방법을 활용해 애플리케이션에 적합한 모델을 선택하고 평가 과정을 구축하는 방법을 살펴본다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">평가를 수행할 때는 일부분만 보는 것이 아니라 시스템의 컨텍스트를 고려해야 한다.&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>위험을 줄이기 위해서 시스템이 어떤 부분에서 취약한지 먼저 파악하고, 그에 맞춰 평가 설계를 진행해야 한다. 시스템의 취약점을 더욱 명확히 파악할 수 있도록 시스템 구조를 재설계해야할 수 있다.&nbsp;</li>
<li>시스템의 취약점을 제대로 이해하지 못하면, 다양한 평가 지표와 도구를 활용하더라도 견고함을 확보하기 어렵다.</li>
</ul>
<p data-ke-size="size16">평가가 어렵다해서 어떠한 모델이 좋다고 말하는 입소문이나 결과를 눈으로 대충 확인하는 식의 접근은 위험을 증폭시키고 애플리케이션 개발 속도를 늦춘다. 결과를 신뢰할 수 있도록 체계적인 평가에 투자하자.</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>교차 엔트로피</li>
<li>퍼플렉시티
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>언어 모델 학습, 파인튜닝 과정에서 필수, 많은 평가 방법에서도 사용됨</li>
</ul>
</li>
<li>파운데이션 모델을 개방형이기에 평가가 어렵고 많은 애플리케이션에서 사람 평가자의 역할이 필수적이지만, 이 과정을 자동화하는 것이 모두의 목표이다.
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>정확한 평가</li>
<li>주관적 평가 (AI as a judge)</li>
</ul>
</li>
</ul>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h2 data-ke-size="size26">파운데이션 모델 평가의 어려움</h2>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 똑똑해질수록 평가가 더 어려워짐</li>
<li>정교한 작업일수록 평가에 더 많은 시간이 소요됨
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>그럴듯하다고 좋은 평가를 해서는 안되며 사실 확인, 추론, 전문 지식을 사용해 평가해야 함</li>
</ul>
</li>
<li>개방형 특성 : 정답을 기준으로 평가하는 기존 방식(폐쇄형)이 유효하지 않음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>하나의 입력에 대해 정답이 여러개 존재할 수 있음</li>
<li>비교할 정답 목록을 완벽하게 만들 수 없음</li>
</ul>
</li>
<li>파운데이션 모델은 블랙박스도 취급됨
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델 아키텍처, 학습 데이터, 학습 과정 같은 세부 사항을 알면 모델의 강점과 약점을 명확히 파악할 수 있지만, 세부 정보가 없으면 출력 결과만 보고 평가할 수 밖에 없음</li>
<li>공개적으로 이용 가능한 벤치마크들은 파운데이션 모델을 평가하는데 부적절한 것으로 판명됨</li>
<li>AI의 발전에 맞춰 벤치마크도 진화해야함 : 기존 벤치마크들에 모델들은 이미 최고점수에 도달함 (e.g. 초기에 많이 활용되던 MMLU도 MMLU-Pro로 대체됨)</li>
</ul>
</li>
<li>범용 모델의 평가 범위가 확장됨
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>알려진 작업의 성능뿐만 아니라 모델이 수행할 수 있는 새로운 작업을 발견하는 것까지
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람의 능력을 넘어서는 작업도 포함될 수 있음</li>
<li>AI의 잠재력과 한계를 탐구하는 책임</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">새로운 도전 과제들덕에 새로운 방법과 벤치마크들이 나왔다.</p>
<img width="690" height="653" alt="image" src="https://github.com/user-attachments/assets/1e465dc3-a287-45ed-a353-5cfcb82c3455" />

<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">깃허브 스타가 많은 상위 1,000개의 AI 저장소에서 24년 5월 기준 평가 관련 저장소가 50개가 넘는다.</p>
<img width="1121" height="739" alt="image" src="https://github.com/user-attachments/assets/6905d2ed-16ea-48ec-890e-29c3bbe4b1f8" />

<p data-ke-size="size16">&nbsp;</p>
<p style="color: #333333; text-align: start;" data-ke-size="size16">하지만 관심이 늘어났음에도 AI 엔지니어링 파이프라인의 다른 부분에 비해 관심이 뒤쳐져 있다.</p>
<p style="color: #333333; text-align: start;" data-ke-size="size16">실험 결과는 알고리즘 개선에만 사용되고 평가 개선에는 거의 사용되지 않는다고 한다.</p>
<img width="1156" height="636" alt="image" src="https://github.com/user-attachments/assets/0ee13b0e-618a-445e-8786-04296e31e04c" />

<p data-ke-size="size16">불충분한 투자는 불충분한 인프라로 이어지며 체계적인 평가를 수행하기 어렵게 만든다.</p>
<p data-ke-size="size16">대부분의 사람들은 결과를 대략적으로 확인하고, 프롬프트도 경험상 수집되는 경우가 많다. 이러한 접근은 애플리케이션을 지속적으로 개선하는 데 충분하지 않다. (평가에 대한 체계적인 접근 방식이 필요)</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h2 data-ke-size="size26">언어 모델링 지표 이해하기</h2>
<p data-ke-size="size16">파운데이션 모델은 언어 모델에서 발전했고 여전히 언어 모델을 핵심 구성 요소로 활용하고 있다.</p>
<p data-ke-size="size16">따라서 언어 모델링 지표를 대략적으로 이해하면 애플리케이션의 성능을 이해하는 데 큰 도움이 될 수 있다.</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>대부분의 자기회귀 언어 모델은 <b>교차 엔트로피</b>나 관련된 지표인 <b>퍼플렉시티</b>를 사용해 학습된다.&nbsp;
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li><b>문자당 비트 BPC, 바이트당 비트 BPB</b>는 교차 엔트로피의 변형된 형태</li>
<li>이 4가지는 밀접하게 관련되어 있어, 하나의 값으로 나머지 셋을 계산할 수 있다.&nbsp;</li>
<li>이들을<b> 언어 모델링 지표</b>라고 부르지만 텍스트뿐만 아니라 다른 종류의 토큰들로 이루어진 시퀀스를 생성하는 모델에서도 사용할 수 있다.</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">언어 모델은 학습 데이터의 분포를 학습한다.&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>모델이 잘 학습할수록 다음에 올 것을 잘 예측할 수 있고, 학습 교차 엔트로피는 더 낮아진다.&nbsp;
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>운영 환경의 데이터가 모델의 학습 데이터와 비슷한수록 모델이 더 좋은 성능을 낸다.&nbsp;</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">엔트로피</h3>
<p data-ke-size="size16">엔트로피는 토큰이 평균적으로 얼마나 많은 정보를 담고 있는지 측정한다.&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>엔트로피가 높을수록 각 토큰이 더 많은 정보를 담고 있으며, 토큰을 표현하는 데 더 많은 비트가 필요하다.
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>직관적으로 엔트로피가 낮은 것은 다음에 올 토큰을 더 쉽게 예측할 수 있다는 뜻이다.&nbsp;</li>
<li>다음에 할 말을 완벽하게 예측할 수 있다면&nbsp; 그 말은 새로운 정보가 아니다.</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<img width="389" height="244" alt="image" src="https://github.com/user-attachments/assets/9f3e940c-d496-489b-a7c7-b0c80c98020d" />

<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>정사각형 안의 위치를 설명하는 언어를 만든다할 때, b가 더 많은 정보를 담고 있지만 표현하는 데 더 많은 비트가 필요하다. 엔트로피도 b가 더 높다</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">교차 엔트로피</h3>
<p data-ke-size="size16">언어 모델을 학습시킬 때의 목표는 학습 데이터의 분포를 배우게 하는 것 = 다음에 무엇이 올지 예측하게 만드는 것</p>
<p data-ke-size="size16">교차 엔트로피는 언어 모델이 데이터셋의 내용을 얼마나 예측하기 어려워하는지를 보여주는 지표이다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">학습 데이터에 대한 모델의 교차 엔트로피는 두 가지 특성에 따라 달라진다.</p>
<ol style="list-style-type: decimal;" data-ke-list-type="decimal">
<li>학습 데이터의 예측 가능성, 이것은 학습 데이터의 엔트로피로 측정된다.</li>
<li>언어 모델이 파악한 분포가 학습 데이터의 실제 분포와 얼마나 다른지</li>
</ol>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">엔트로피와 교차 엔트로피는 같은 수학기호 $H$를 사용한다. $P$를 학습 데이터의 실제 분포, $Q$를 언어 모델이 학습한 분포라고 하면 다음이 성립한다.</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>학습 데이터의 엔트로피는 $H(P)$&nbsp;</li>
<li>$Q$와 $P$가 얼마나 다른지는 쿨백-라이블러(KL) 발산으로 측정할 수 있으며, 수학적으로 $D_{KL}(P\vert \vert Q)$로 표현된다.&nbsp;</li>
</ul>
<p data-ke-size="size16">$$H(P, Q) = H(P) + D_{KL}(P \vert \vert Q)$$</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">교차 엔트로피는 비대칭적이다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>$H(P, Q)$는 $H(Q, P)$와 다른 값을 갖는다.</li>
</ul>
<p data-ke-size="size16">언어 모델은 학습 데이터에 대한 교차 엔트로피를 최소화하도록 학습된다.&nbsp;</p>
<p data-ke-size="size16">학습 데이터를 완벽하게 학습하면 모델의 교차 엔트로피와 학습 데이터의 엔트로피는 정확히 같아진다.&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>이때 $P$에 대한 $Q$의 KL발산은 0이 될 것이다. 이렇게 KL 발산 값이 0에 가깝게 최소화된다면 학습이 잘 된 모델에서 측정된 교차 엔트로피는 실제 데이터 분포의 엔트로피를 가늠하는 근사치로 사용될 수 있다.&nbsp;</li>
</ul>
<div data-ke-type="moreLess" data-text-more="더보기" data-text-less="닫기"><a class="btn-toggle-moreless">더보기</a>
<div class="moreless-content">
<p data-ke-size="size16">정보량 (Information)</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>어떤 사건 $x$가 발생했을 때 얻는 정보의 크기&nbsp;</li>
</ul>
<p data-ke-size="size16">$$I(x) = -\log P(x)$$</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>발생 확률이 낮을 수록 더 큰 정보</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">엔트로피 (Entropy)</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>확률 분포 $P$가 가진 평균 불확실성(평균 정보량)</li>
</ul>
<p data-ke-size="size16">$$H(P) = \mathbb{E}_{x \sim P}[ -\log P(x) ] = -\sum_x P(x)\log P(x)$$</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모든 사건이 확실할 수록 낮고, 불확실할 수록 높아짐</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-end="488" data-start="459" data-ke-size="size16">교차 엔트로피 (Cross Entropy)</p>
<ul style="list-style-type: disc;" data-end="567" data-start="490" data-ke-list-type="disc">
<li data-end="567" data-start="490">데이터는 실제 분포 $P$를 따르지만 모델은 분포 $Q$를 예측할 때, 실제 데이터가 모델에서 얼마나 놀라운지를 나타냄</li>
<li data-end="567" data-start="490">$Q$가 $P$를 잘 맞출수록 값이 작아짐</li>
</ul>
<p data-ke-size="size16">$$H(P, Q) = - \sum_x P(x)\log Q(x)$$</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">Maximum Likelihood &rarr; NLL &rarr; 교차 엔트로피</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>MLE: 모델이 정답 데이터 확률을 가장 크게 만들도록 학습
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>$\max_\theta \prod_{i=1}^{N} Q_\theta(x_i)$</li>
</ul>
</li>
<li>로그 취해 합으로 바꾼 Log-likelihood
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>$\sum_{i=1}^{N} \log Q_\theta(x_i)$</li>
</ul>
</li>
<li>최소화 관점으로 바꾼 NLL (Negative Log Likelihood)
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>$-\frac{1}{N} \sum_{i=1}^{N} \log Q_\theta(x_i)$</li>
</ul>
</li>
<li data-end="1011" data-start="988">데이터 샘플 평균은 기댓값을 근사
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li data-end="1011" data-start="988">$-\frac{1}{N} \sum_{i=1}^{N} \log Q_\theta(x_i) \approx - \mathbb{E}_{x \sim P}[\log Q_\theta(x)]$</li>
</ul>
</li>
<li data-end="1011" data-start="988">기댓값을 합으로 전개하면<br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li data-end="1011" data-start="988">$-\mathbb{E}_{x&nbsp;\sim&nbsp;P}[\log&nbsp;Q_\theta(x)]&nbsp;=&nbsp;-&nbsp;\sum_{x}&nbsp;P(x)&nbsp;\log&nbsp;Q_\theta(x)$</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>&nbsp;KL 발산
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>$D_{\mathrm{KL}}(P&nbsp;\parallel&nbsp;Q)&nbsp;=&nbsp;\sum_x&nbsp;P(x)&nbsp;\log&nbsp;\frac{P(x)}{Q(x)}$</li>
<li><span style="caret-color: auto; letter-spacing: 0px;">$D_{\mathrm{KL}}(P \parallel Q) = \sum_x P(x) \log P(x) - \sum_x P(x) \log Q(x)$<br /></span></li>
</ul>
</li>
<li><span style="caret-color: auto; letter-spacing: 0px;">교차 엔트로피 식에 트릭을 써서 KL 발산을 포함한 식으로&nbsp;</span>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>$- \sum_x P(x) \log Q(x) = \sum_x P(x) \log P(x) - \sum_x P(x) \log Q(x) - \sum_x P(x) \log P(x)$</li>
<li>$- \sum_x P(x) \log Q(x) = D_{\mathrm{KL}}(P \parallel Q) - \sum_x P(x) \log P(x)$</li>
<li>$H(P) = - \sum_x P(x) \log P(x)$</li>
<li>$H(P, Q) = - \sum_x P(x) \log Q(x) = H(P) + D_{\mathrm{KL}}(P \parallel Q)$</li>
</ul>
</li>
<li>$H(P)$는 $P$에만 의존하는 상수이므로, $Q$를 학습할 때 교차 엔트로피를 최소화하는 것은 $Q$가 $P$에 가까워지도록 만드는 것과 동일하다.&nbsp;</li>
</ul>
</div>
</div>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">문자당 비트와 바이트당 비트&nbsp;</h3>
<p data-ke-size="size16">엔트로피와 교차 엔트로피의 단위는 비트를 사용한다.&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>교차 엔트로피가 6비트라면, 각 토큰을 표현하는 데 6비트가 필요하다는 것&nbsp;</li>
</ul>
<p data-ke-size="size16">모델마다 토큰화 방식이 달라 토큰당 비트 수로 모델을 비교하기보단, 문자당 비트 BPC를 사용하기도 한다.&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>토큰당 비트수가 6, 평균적으로 각 토큰이 2개의 문자로 이루어져있으면 BPC는 6/2 = 3&nbsp;</li>
<li>BPC도 문제점이 존재 : 문자 인코딩 방식이 다양함 (ASCII는 문자당 8비트, UTF-8은 문자당 8~32비트)</li>
<li>더 표준화된 지표 바이트당 비트 BPB : 원본 학습 데이터의 <b>1바이트</b>를 표현하는 데 필요한 비트 수를 의미</li>
<li>BPC가 3, 각 문자가 7비트, 1바이트의 7/8, BPB는 3 / (7/8) = 3.43</li>
</ul>
<p data-ke-size="size16">$$\text{BPB} = \frac{\text{Bits Per Token}}{\text{Chars Per Token} \times \text{Bytes Per Char}}$$</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">BPB가 3.43이라는 건 원본 1바이트를 3.43 비트로 표현할 수 있다는 뜻이며, 원본 학습 텍스트를 원래 크기의 절반 이하로 압축할 수 있다는 의미</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">퍼플렉시티</h3>
<p data-ke-size="size16">퍼플렉시티 Perplexity, PPL는 엔트로피와 교차 엔트로피의 지수 함수이다.</p>
<p data-ke-size="size16">퍼플렉시티는 다음 토큰을 예측할 때의 불확실성을 측정한다. 불확실성이 클수록 퍼플렉시티는 높아짐</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>불확실성이 높을 수록 다음 토큰으로 가능한 선택지가 많다는 것을 의미</li>
<li>그림 3-4에서 언어 모델이 정사각형의 위치를 예측하려면 2^2 = 4개의 선택지 중에서 골라야하므로 퍼플렉시티는 4</li>
</ul>
<p data-ke-size="size16">실제 분포 $P$를 가진 데이터셋이 주어졌을 때, 퍼플렉시티는 다음과 같이 정의된다.&nbsp;</p>
<p data-ke-size="size16">$$PPL(P) = 2^{H(P)}$$</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">언어 모델의 학습된 분포 $Q$는 다음과 같이 정의된다.</p>
<p data-ke-size="size16">$$PPL(P, Q) = 2^{H(P, Q)}$$</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">비트 단위를 사용했기 때문에 위 방성직에서 밑이 2이다.</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>텐서플로우, 파이토치를 포함한 인기있는 ML 프레임워크에서는 단위로 nat (자연로그)를 사용한다.&nbsp;</li>
</ul>
<p data-ke-size="size16">$$PPL(P, Q) = e^{H(P, Q)}$$</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">교차 엔트로피는 로그 밑(2 또는 e)에 따라 값이 달라져 서로 비교하기 어렵지만, 퍼플렉시티로 변환하면 단위에 무관하게 일관된 값을 얻을 수 있다. 따라서 언어 모델의 성능 지표로 퍼플렉시티가 자주 사용된다.</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">퍼플렉시티 해석과 활용 사례</h4>
<p data-ke-size="size16">모델이 텍스트를 더 정확하게 예측할 수록 이런 지표들의 값은 더 낮아진다.</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>구조화된 데이터일수록 퍼플렉시티가 낮다</b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>HTML 코드는 일상 텍스트보다 예측하기 쉽다.</li>
</ul>
</li>
<li><b>어휘 크기가 클수록 퍼플렉시티가 높다&nbsp;</b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>선택할 수 있는 토큰이 많을 수록 모델이 다음 토큰을 예측하기 더 어렵다.&nbsp;</li>
</ul>
</li>
<li><b>컨텍스트 길이가 길수록 퍼플렉시티가 낮다.</b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 볼 수 있는 컨텍스트가 많을수록 다음 토큰을 예측할 때 불확실성이 줄어든다.</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">퍼플렉시티 값이 3 또는 그보다 낮은 경우도 흔함</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 다루는 어휘 크기가 수만에서 수십만 개에 달하는 점을 생각하면 놀라운 수준</li>
</ul>
<p data-ke-size="size16">퍼플렉시티는 성능 지표로 사용되는 것 외에도 다양한 AI 엔지니어링 작업에서 유용하다.</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>모델의 성능을 간접적으로 보여주는 좋은 지표</li>
<li>강력한 모델들이 다양한 데이터셋에서 일관되게 더 낮은 퍼플렉시티를 보임 (점점 공개하지 않는 추세)</li>
</ul>
<img width="1057" height="421" alt="image" src="https://github.com/user-attachments/assets/b1997bc0-fff3-4629-9476-20f2ac15296e" />

<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>하지만 퍼플렉시티는 SFT, RLHF 같은 기법을 사용해 사후 학습된 모델을 평가하는 데는 적절한 지표가 아닐 수 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>보통 사후 학습 후에 퍼플렉시티가 높아짐 (다음 토큰을 예측하는 능력이 떨어짐)</li>
<li>양자화 기법도 퍼플렉시티를 변화시킬 수 있음</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 학습 중에 본 적이 있고 기억한 텍스트에서는 퍼플렉시티가 가장 낮게 나타남
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>어떤 텍스트가 학습 데이터에 포함되었는지 탐지하는데 사용 가능</li>
<li>데이터 오염을 탐지하는데 유용
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>특정 벤치마크 데이터에 대해 낮은 퍼플렉시티를 보인다면, 그 벤치마크가 모델의 학습 데이터에 포함되어 있었을 가능성이 높아 해당 벤치마크의 모델 성능을 신뢰하기 어려움</li>
</ul>
</li>
<li>학습 데이터 중복 제거에도 활용 가능</li>
<li>특이한 생각이나 의미없는 텍스트에서 가장 높게 나타나므로, 비정상적인 텍스트 탐지에도 사용될 수 있음</li>
</ul>
</li>
</ul>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h2 data-ke-size="size26">정확한 평가</h2>
<p data-ke-size="size16">폐쇄형 응답이 아닌 개방형 응답의 평가에 중점을 두고 진행</p>
<p data-ke-size="size16">정확한 점수를 산출하는 두 가지 평가 방식</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>기능적 정확성 Functional Correctness</b></li>
<li><b>참조 데이터의 유사도 측정</b></li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">기능적 정확성</h3>
<p data-ke-size="size16">시스템이 의도한 기능을 제대로 수행하는지 평가하는 것&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>애플리케이션이 의도한 대로 동작하는지를 측정하기 때문에 모든 애플리케이션의 성능을 평가하는 궁극적인 지표</li>
<li>별로 간단하지 않고, 측정을 자동화하는 것도 쉽지 않음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>자동화할 수 있는 작업의 예시 : 코드 생성 (실행 정확도)
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>단위 테스트 : 서로 다른 시나리오(테스트 케이스)에서 실행해 예상된 출력을 생성하는지 확인 (리트코드나 해커랭크같은 플랫폼에서 제출된 답안 검증)</li>
</ul>
</li>
</ul>
</li>
<li>AI 코드 생성 능력 평가 벤치마크에서 많이 사용 (HumanEval, MBPP)
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>스파이더, BIRD-SQL, WikiSQL 같은 텍스트 SQL 벤치마크</li>
<li>모델 평가 시에 $k$개의 코드 샘플을 생성하고, 그 중 하나라도 해당 테스트 케이스를 통과하면 그 문제를 해결한 것으로 봄&nbsp;</li>
</ul>
</li>
<li>게임 봇&nbsp;</li>
<li>측정 가능한 목표가 있는 작업에서 지능 정확성으로 평가 가능 (e.g. AI에 에너지 소비 최적화하도록 작업을 스케쥴링해달라고 요청, 얼마나 많은 에너지를 절약하는지로 측정)</li>
<li>많은 복잡한 작업이 측정 가능한 목표를 가지고 있지만, AI가 복잡한 작업을 처음부터 끝까지 수행할 만큼 충분히 좋지는 않으며 일부분을 수행하는데 사용될 수 있다. 전체 결과 평가보다 일부분을 평가하는 것이 더 어려울 수 있다.</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">참조 데이터 유사도 측정</h3>
<p data-ke-size="size16">자동 평가를 할 수 없다면, AI의 출력을 참조 데이터와 비교해 평가 (e.g. 프랑스어를&nbsp;영어로 번역해달라하고 영어 번역문을 정답 영어 번역문과 비교)</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>참조 데이터의 각 예시의 형식은 (입력, 참조 응답)
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>참조 응답은 여러개일 수 있다.</li>
<li>정답 or 표준 응답이라 불림</li>
</ul>
</li>
<li>참조가 필요한 평가 지표는 참조 기반 지표 reference-based metrics, 그렇지 않은 것은 참조 없는 지표 reference-free metrics</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>이 평가 방식은 참조 데이터가 필요하므로, 참조 데이터를 얼마나 빨리 만들 수 있는지가 곧 성능의 척도가 됨
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>보통은 사람이 생성하지만 점점 AI가 생성하는 경우가 늘고있음 (AI 생성 데이터를 검토해야할 수 있지만 처음부터 사람이 만드는 것보다 덜 힘들다)</li>
</ul>
</li>
<li>생성된 응답이, 참조 응답과 더 비슷할 수록 좋은 것
<ol style="list-style-type: decimal;" data-ke-list-type="decimal">
<li><b>비교</b> : 평가자에게 두 텍스트가 같은지 판단하도록 요청</li>
<li><b>정확한 일치</b> : 생성된 응답이 참조 응답 중 하나와 정확히 일치하는지 여부</li>
<li><b>어휘적 유사도</b> : 생성된 응답이 참조 응답과 얼마나 비슷해 보이는지</li>
<li><b>의미적 유사도</b> : 생성된 응답이 의미 semantic에서 참조 응답과 얼마나 가까운지</li>
</ol>
</li>
<li>두 응답의 비교는 사람 평가자나 AI 평가자가 수행</li>
</ul>
<div data-ke-type="moreLess" data-text-more="더보기" data-text-less="닫기"><a class="btn-toggle-moreless">더보기</a>
<div class="moreless-content">
<p data-ke-size="size16">유사도 측정은 출력의 품질을 평가하는 것 오에도 다양한 용도로 사용 가능하다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>검색과 서치 : 질의와 유사한 항목 찾기</li>
<li>순위 매기기 : 질의에 대한 유사도를 기준으로 순위 매기기</li>
<li>군집화 : 항목간 유사도를 기준으로 군집화</li>
<li>이상 탐지 : 나머지 항목들과 유사도가 낮은 항목 탐지하기</li>
<li>데이터 중복 제거 : 다른 항목들과 유사도가 높은 항목 제거하기</li>
</ul>
</div>
</div>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">다음으로 수작업으로 설계된 평가 지표들을 살펴보자&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">정확한 일치</h4>
<p data-ke-size="size16">생성된 응답이 참조 응답 중 하나와 정확히 일치하는 경우</p>
<p data-ke-size="size16">간단한 수학 문제, 일반 상식 질의, 퀴즈 형태의 짧고 정확한 응답을 기대하는 작업에 적합하다.</p>
<p data-ke-size="size16">간단한 작업을 넘어서면 잘 작동하지 않음</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">어휘적 유사도</h4>
<p data-ke-size="size16">두 텍스트가 얼마나 겹치는지 측정 (비슷하게 생겼는지, 의미는 측정하지 않음)</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>가장 단순한 형태 : 공통으로 가진 토큰의 수를 세는 방식</li>
<li><b>근사 문자열 매칭</b> <b>(퍼지 매칭)</b> : 한 텍스트를 다른 텍스트로 바꾸는 데 필요한 편집 횟수(편집거리)를 센다. 가능한 편집 연산은 삭제, 삽입, 대체</li>
<li><b>n-gram 유사도&nbsp;</b>: 연속된 시퀀스 n-gram의 겹침을 기준으로 측정
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>1-gram 하나의 토큰, 2-gram은 두 토큰의 집합</li>
<li>참조 응답의 n-gram 중 몇 퍼센트가 생성된 응답에도 있는지를 측정</li>
</ul>
</li>
<li>BLEU, ROUGE, METEOR++, TER, CIDEr&nbsp;
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>각각 텍스트가 얼마나 겹치는지 계산하는 방식이 다름</li>
<li>파운데이션 모델 등장 이후에는 어휘적 유사도를 사용하는 벤치마크가 줄었음</li>
<li>포괄적인 참조 응답 세트를 만들어야함, 그렇지 않으면 좋은 응답도 낮은 유사도를 받음, 참조 응답도 틀릴 수 있</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">의미적 유사도&nbsp;</h4>
<p data-ke-size="size16">의미가 얼마나 비슷한지 계산</p>
<p data-ke-size="size16">이를 위해 텍스트를 임베딩이라 부르는 숫자 표현으로 변환할 필요가 있음</p>
<p data-ke-size="size16">두 임베딩 간 유사도는 코사인 유사도 같은 지표로 계산 가능 (같은 임베딩은 1, 반대는 -1), 이미지나 오디오 등 모든 데이터 유형의 임베딩에 대해 계산할 수 있음</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">A: 생성된 응답의 임베딩 / B: 참조 응답의 임베딩 / Norm</p>
<p data-ke-size="size16">코사인 유사도 : $(A \cdot B)/(\Vert{A}\Vert \Vert{B}\Vert)$</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>BERTScore, MoverScore</li>
<li>기반이 되는 임베딩 알고리즘의 품질에 신뢰성이 달려있음</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">임베딩 소개</h3>
<p data-ke-size="size16">임베딩 embedding은 원본 데이터의 의미를 담으려는 <span style="color: #333333; text-align: start;">컴퓨터가 처리할 수 있는<span> </span></span>숫자 표현, 벡터</p>
<p data-ke-size="size16">일반적으로 임베딩 벡터의 크기는 100에서 10,000 사이</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>임베딩을 만들기 위해 학습된 모델 : BERT, CLIP, Sentence Transformers</li>
</ul>
<img width="767" height="497" alt="image" src="https://github.com/user-attachments/assets/f9820024-91e6-4062-91a8-53e4a344e988" />

<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">GPT나 라마같은 모델은 입력을 벡터로 표현해야 하므로 임베딩을 생성하는 단계를 포함하고, 이 중간 층에 접근하면 임베딩을 추출하는 데 사용할 수 있다. 하지만 임베딩 전용 모델이 생성한 것만큼 좋지 않을 수 있다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>임베딩 알고리즘의 목표 : 원본 데이터의 본질을 담아내는 임베딩을 나타내는 것</li>
<li>검증 : 비슷한 텍스트의 임베딩이 코사인 유사도나 관련 지표로 측정했을 때 더 가까우면 좋은 임베딩 알고리즘이라고 본다.</li>
<li>해당 작업의 유용성을 기준으로 품질을 평가하기도 함 : 분류, 주제 모델링, 추천 시스템, RAG 등 많은 작업에서 사용됨
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>MTEB : 임베딩 품질을 측정하는 벤치마크의 예시</li>
<li>크리테오, 코베오 : 전자상거래 솔루션 제품에 대한 임베딩</li>
<li>핀터레스트 : 이미지, 그래프, 쿼리, 사용자에 대한 임베딩</li>
<li>CLIP : 서로 다른 유형의 데이터를 하나의 통합 임베딩 공간으로 매핑할 수 있는 첫 주요 모델 (이미지와 텍스트)</li>
<li>ULIP : 텍스트, 이미지, 포인트 클라우드의 통합 표현</li>
<li>ImageBind : 텍스트, 이미지, 오디오를 포함한 여섯가지 서로 다른 유형의 데이터에 대한 통합 임베딩 학습</li>
</ul>
</li>
</ul>
<img width="1126" height="813" alt="image" src="https://github.com/user-attachments/assets/11f40e12-72dd-4bdb-9240-a3101409d8ee" />

<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>(이미지, 텍스트) 쌍을 텍스트 인코더, 이미지 인코더를 사용해 각 임베딩을 변환 후 통합 임베딩 공간(멀티모달 임베딩 공간)에 투영, 이미지 텍스트 쌍의 임베딩이 가까워지도록 학습&nbsp;</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h2 data-ke-size="size26">AI 평가자</h2>
<p data-ke-size="size16">AI를 사용해 AI를 평가하는 접근 방식 (LLM 평가자라고도 함)</p>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">AI 평가자를 쓰는 이유</h3>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>빠르고, 사용하기 쉽고 저렴하다. 참조 데이터 없이도 작동 가능</li>
<li>AI의 판단도 항상 신뢰할 수 있는 것은 아니지만, 대중적인 관점에서 판단 가능 (적절한 모델, 적절한 프롬프트)</li>
<li>사람 평가자들과 높은 상관관계를 보임 (연구에 의하면 85% 일치도, 0.98의 상관관계)</li>
<li>자신의 결정을 설명 가능</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">AI 평가자 사용법</h3>
<p data-ke-size="size16">응답 자체의 품질을 평가하거나, 응답을 참조 데이터와 비교하거나, 다른 응답과 비교할 수 있음</p>
<img width="1092" height="1189" alt="image" src="https://github.com/user-attachments/assets/25e3b100-05e8-4a43-a8c7-9293e23edc29" />

<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">어떤 기준으로든 응답 평가 가능</p>
<img width="1116" height="396" alt="image" src="https://github.com/user-attachments/assets/8bc38887-0d53-4a51-9d19-b649f4502c3c" />

<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">표준화되어있지 않으므로 AI 모델과 프롬프트에 따라 점수가 의미하는 바가 달라짐&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">평가자 프롬프트에서 명확하게 설명해야하는 것들</p>
<ol style="list-style-type: decimal;" data-ke-list-type="decimal">
<li>모델이 수행할 작업</li>
<li>모델을 평가할 때 따라야 할 기준, 지시가 자세할 수록 좋음</li>
<li>점수 체계 (분류 : 좋음/나쁨, 관련 없음/중립, 이산적인 숫자 값, 연속적인 숫자 값)
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>언어 모델은 텍스트를 더 잘 다룸, 수치 점수 체계보다 분류에서 더 잘 작동함</li>
</ul>
</li>
</ol>
<img width="1165" height="383" alt="image" src="https://github.com/user-attachments/assets/042ad059-cf9a-4aa6-8206-158299e8ef89" />

<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">AI 평가자의 한계</h3>
<h4 data-ke-size="size20">비일관성</h4>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>같은 평가자가 동일한 입력을 받아도 프롬프트가 다르면 다른 점수를 출력할 수 있음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>같은 지시로 프롬프트를 받아도 다를 수 있음</li>
</ul>
</li>
<li>평가 결과 재현, 신뢰가 어려움</li>
<li>일관성을 높일 수야 있지만 높은 일관성이 높은 정확도를 의미하지는 않음 (일관된 실수)
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>긴 프롬프트는 추론 비용을 늘림</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">평가 기준의 모호성</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>표준화되지 않아서 잘못 해석하고 오용하기 쉬움
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>MLflow, Ragas, LlamaIndex 오픈 소스 도구들은 주어진 컨텍스트에서 생성된 출력이 원본 내용을 얼마나 정확히 반영하는지 측정하는 충실성이라는 기준이 있지만, 지시와 점수 체계가 다르다.</li>
</ul>
</li>
</ul>
<img width="1097" height="859" alt="image" src="https://github.com/user-attachments/assets/c3a9416f-e28d-4125-af93-9a0a46c37cce" />

<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">AI 평가자는 시간이 지나면서 변할 수 있다.&nbsp;</p>
<p data-ke-size="size16"><b>모델과 평가자에 사용된 프롬프트를 볼 수 없다면 어떤 AI 평가자도 신뢰할 수 없다.</b></p>
<p data-ke-size="size16">평가 방법이 표준화되는 데는 시간이 걸린다.</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">비용과 지연 시간 증가</h4>
<p data-ke-size="size16">강력한 모델로 응답을 평가하는 것은 비용이 많이 든다.</p>
<p data-ke-size="size16">응답을 생성하고 평가까지 하면 호출이 두 배, 비용도 두배로 늘어난다.</p>
<p data-ke-size="size16">응답 품질, 사실 일관성, 유해성 같은 기준을 평가하기 위해 평가 프롬프트를 사용하면 호출 횟수는 4배로 늘어난다.</p>
<p data-ke-size="size16">약한 모델을 사용해서 비용을 줄이거나, 표본 검사로 비용을 줄일 수 있다. (표본 검사는 일부 실패를 놓칠 수도 있음)</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">비용과 신뢰도 사이의 적절한 균형을 시행착오를 통해 찾아야 함</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">운영 파이프라인에 구현하면 지연 시간이 늘어날 수 있음&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">AI 평가자의 편향</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>자기 편향 : 모델이 자신의 응답을 선호하는 현상</li>
<li>첫 위치 편향 : 첫 번째 응답을 선호 (순서를 바꿔가며 같은 테스트를 여러 번 반복하거나 세심하게 작성된 프롬프트로 완화)
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람은 마지막에 본 응답을 선호하는 경향이 있음 : 최근성 편향</li>
</ul>
</li>
<li>장황성 편향 : 품질과 관계없이 긴 응답을 선호
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 강력해질수록 편향이 사라질 수 있다는 것을 시사함</li>
</ul>
</li>
<li>개인정보 보호와 지적 재산권 같은 제약이 있음</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">평가자로 활용 가능한 모델&nbsp;</h3>
<p data-ke-size="size16">평가자가 평가받는 모델보다 강력하거나, 약하거나 비슷할 수 있으며 각각 장단점이 있다.</p>
<p data-ke-size="size16">당연히 강력한 모델이 좋아보이지만, 비용과 지연 시간을 이유로 약한 모델을 활용한다. 서로 백그라운드에서 돌아가며 함께 쓰기도 한다.</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>강력한 평가자의 문제점
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>가장 강력한 모델을 평가할 평가자를 찾을 수 없음</li>
<li>어떤 모델이 가장 강력한지 판단하기 위한 다른 평가 방법이 필요함</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>자기 평가/자기 비평은 기본 검증에 매우 유용하다 : 모델이 자신의 응답이 잘못됐다고 생각하면 그 모델을 신뢰하기 어려울 것
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>기본 검증을 넘어 자기 응답을 수정, 개선하도록 유도</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>약한 평가자가 괜찮은지에 대해서는 아직 해결되지 않음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>평가가 생성보다 쉽다는 의견도 존재</li>
</ul>
</li>
<li>연구를 통해 더 강력한 모델이 사람의 선호도와 사람의 선호도와 상관관계가 있음이 발견됨&nbsp;
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람들은 자신이 감당할 수 있는 가장 강력한 모델을 선택 (범용 평가자에 한해서)</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>작고 특화된 평가자 : 특정 판단에 있어 더 크고 범용적인 평가자보다 신뢰할 수 있음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li><b>보상 모델, 참조 기반 평가자, 선호도 모델</b></li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">보상 모델</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>(프롬프트, 응답) 쌍을 입력받고 그 응답이 얼마나 좋은지 점수를 매김
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>RLHF에서 성공적으로 사용되어 옴</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">참조 기반 평가자&nbsp;</h4>
<p data-ke-size="size16">하나 이상의 참조 응답을 기준으로 생성된 응답을 평가</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>유사도 점수, 품질 점수</li>
<li>BLEURT : (후보 응답, 참조 응답) 쌍을 입력으로 받아 참조 응답 간의 유사도 점수 출력</li>
<li>Prometheus : (프롬프트, 생성된 응답, 참조 응답, 채점 기준)을 입력으로 받아 참조 응답이 5라 가정하고 1~5 사이의 품질 점수 출력</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">선호도 모델</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>(프롬프트, 응답 1, 응답 2), 주어진 프롬프트에 대해 어느 응답이 더 나은지 출력</li>
<li>사람의 선호도를 예측하려는 것&nbsp;</li>
</ul>
<img width="1130" height="629" alt="image" src="https://github.com/user-attachments/assets/91ff7cf4-c35d-4f89-b725-2d78135d6fab" />

<p data-ke-size="size16">&nbsp;</p>
<h2 data-ke-size="size26">비교 평가를 통해 모델 순위 정하기</h2>
<p data-ke-size="size16">모델을 평가하는 이유 : 어떤 모델이 가장 적합한지 알고 싶어서, 이때 모델의 순위가 필요하며 순위는 개별 평가나 비교 평가를 통해 정할 수 있음</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>개별 평가</b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>각 모델을 독립적으로 평가한 후 점수를 기준으로 순위를 매김</li>
</ul>
</li>
<li><b>비교 평가</b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델들을 서로 비교해 평가, 비교 결과로 순위 계산</li>
<li>응답 품질이 주관적일 때, 비교 평가가 더 쉬움</li>
</ul>
</li>
</ul>
<img width="1091" height="521" alt="image" src="https://github.com/user-attachments/assets/f68835c4-e977-44e2-9e75-d15536327125" />

<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>모든 질의를 선호도로 평가할 수는 없음, 많은 경우 정확성을 기준으로 평가해야 함
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>선호도 기반 투표가 잘못된 신호를 줄 수 있음</li>
</ul>
</li>
<li>사용자에게 선택하도록 요청하는 것은 불만을 일으킬 수 있음 : 답을 알면 물어보지도 않았음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>사용자의 비교 의견 수집에서 어려운 점 : 어떤 질의가 선호도 투표에 적합한지 판단하는 것</li>
<li>사용자가 AI에게 모르는 일을 요청하는 경우에는 적절하지 않음</li>
</ul>
</li>
<li>비교 평가는 A/B 테스트와 다르다
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>A/B 테스트는 사용자가 한 번에 하나의 후보 모델의 출력만 보지만, 비교 평가는 여러 모델의 출력을 한꺼번에 보고 비교</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델 간의 비교를 경기 match 라고 함</li>
</ul>
<img width="968" height="647" alt="image" src="https://github.com/user-attachments/assets/6f9a21a7-db2a-454d-ab23-cc0adf54005e" />

<p data-ke-size="size16">비교 평가 결과가 주어지면 평가 알고리즘을 사용해 순위를 계산</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>비교 결과에서 모델의 점수를 계산한 다음 이 점수로 모델의 순위를 매김</li>
<li>Elo, Bradley-Terry</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">비교 평가의 과제들</h3>
<p data-ke-size="size16">점수 기반 평가에서는 올바른 비교 결과를 얻기 위해 벤치마크와 지표 설계가 가장 어려운 부분, 점수로 모델의 순위를 매기는 것은 쉬움</p>
<p data-ke-size="size16">비교 평가에서는 비교 결과 수집, 순위 매기기 모두 까다로움</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">확장성 병목</h4>
<p data-ke-size="size16">비교 평가는 데이터가 많이 필요하다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>비교할 모델 쌍의 수는 모델 수의 제곱에 비례해 증가함</li>
<li>두 모델의 성능을 비교할 때 순위 알고리즘은 전이성을 가정하지만 이 가정이 AI 모델에도 적용되는지는 불분명함</li>
<li>새로운 모델을 평가하는 것도 어려운 과제, 비공개 모델 평가는 더욱 어려움</li>
</ul>
<p data-ke-size="size16">이런 확장성 병목은 더 나은 매칭 알고리즘으로 완화할 수 있다. 효율적인 알고리즘을 전체 순위의 불확실성을 최대한 줄일 수 있는 경기를 선택해야 함</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">표준화와 품질 관리의 부재</h4>
<p data-ke-size="size16">비교 결과를 수집 하는 방법 중 하나 : LMSYS 챗봇 아레나처럼 커뮤니티에 비교를 맡기는 것</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>표준화와 품질 관리를 강제하기 어려움</li>
<li>인터넷에 접속할 수 있는 사람이면 누구나 아무 프롬프트를 사용해 이런 모델을 평가할 수 있고, 어떤 응답이 더 나은지에 대한 기준이 없음</li>
<li>사람에 따라 선호하는 응답이 다름 (장점이자 단점)</li>
<li>크라우드소싱 방식의 비교는 사용자들이 실제 업무 환경이 아닌 곳에서 평가하게 됨
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>실제 사용 환경에 대한 이해가 없으므로 프롬프트가 현장에서 모델이 어떻게 쓰이는지 반영하지 못함</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>공개 순위표는 기업의 내부 데이터베이스에서 관련 문서를 검색해 컨텍스트를 보강하는 등 고급 기능을 지원하지 않음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>RAG 시스템에서 얼마나 잘 동작할지 판단하기 어려움</li>
<li>좋은 응답 만드는 능력 != 관련 문서를 찾는 능력</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>표준화를 강제하는 하나의 방법 : 사용자가 미리 정해진 프롬프트를 사용하도록 제한
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>다양한 활용 사례에 대한 능력 평가 불가능</li>
<li>LMSYS는 어떤 프롬프트든 사용할 수 있도록 하고, 내부 모델을 사용해 어려운 프롬프트를 찾아내 순위를 매김&nbsp;</li>
</ul>
</li>
<li>신뢰할 수 있는 평가자만 사용
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>교육된 평가자를 사용 (Scale AI 비공개 비교 순위표), 비용이 많이 들고 비교 횟수도 줄어든다</li>
</ul>
</li>
<li>비교 평가를 제품에 통합
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사용자가 작업하는 동안 평가하도록</li>
<li>전문가가 아니면 판단하기 어려움, 안 읽고 무작위 선택 (많은 노이즈)</li>
<li>이런 이유로 일부 팀은 사람보다 AI 평가자를 선호함 (무작위 인터넷 사용자보단 신뢰할 수 있음)</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">비교 성능에서 절대 성능으로</h4>
<p data-ke-size="size16">비교 평가는 어떤 모델이 더 나은지 알려주지만, 얼마나 좋은지나 활용 사례에 충분한지는 알려주지 않음</p>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">비교 평가의 미래&nbsp;</h3>
<p data-ke-size="size16">비교 평가의 장점</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 아무리 강력해져도 사람은 두 응답의 차이를 구별할 수 있고 가치있는 피드백을 제공할 수 있음, 비교 평가가 유일한 대안이 될 수 있음</li>
<li>비교 평가는 품질(사람의 선호도)를 파악하는 걸 목표로 함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>AI의 끊임없이 확장되는 능력을 따라잡기 위해 계속해서 새로운 벤치마크를 만들어야 하는 부담을 줄여줌</li>
<li>새롭고 강력한 모델이 계속 등장해도 포화 상태에 이르지 않음</li>
<li>조작하기 어려움</li>
<li>다른 방법으로는 알 수 없는 모델 간 성능 차이를 보여줄 수 있음, 기존 벤치마크의 부족한 점을 채워주고 A/B 테스트를 보완함</li>
</ul>
</li>
</ul>

# CH 4
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>애플리케이션 평가 시 사용 가능한 기준 정의, 계산하는 방법</li>
<li>모델 선택</li>
<li>자체 모델 호스팅 vs 모델 API 사용&nbsp;</li>
<li>애플리케이션 개발 과정 개선, 평가 파이프라인 개발 방법</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h2 data-ke-size="size26">평가 기준</h2>
<p data-ke-size="size16">개발자들도 자신의 애플리케이션이 어떻게 사용되고 있는지 정확히 파악하지 못함</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>평가 주도 개발 : 개발하기 전에 평가 기준을 정의하는 것</b>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>시간과 돈을 투자하기 전에 애플리케이션을 어떻게 평가할 지 이해하는 것</li>
<li>테스트 주도 개발 : 코드 작성 전 테스트를 작성하는 방법</li>
</ul>
</li>
<li>현명한 비즈니스 결정은 유행이 아닌 투자 수익률을 기준으로 함, 실제 운영 환경에서 사용되는 엔터프라이즈 애플리케이션은 대부분 명확한 평가 기준을 갖고 있음</li>
<li>해당 애플리케이션에 맞는 평가 기준들로 시작해야 함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>도메인 특화 능력, 생성 능력, 지시 준수 능력, 비용과 지연 시간</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">도메인 특화 능력</h3>
<p data-ke-size="size16">이는 모델 구조, 크기, 학습에 사용된 데이터에 따라 달라짐</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 필요한 능력을 갖췄는지 평가하기 위한 벤치마크들이 계속 늘어나고 있다.</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>코딩 : 정확성 평가, 효율성(실행 시간, 메모리 사용량), 비용, 코드 가독성(주관적 : AI 평가자 등)</li>
<li>코딩이 아닌 도메인 : 객관식 문제 같은 폐쇄형 문제로 평가 (검증과 재현이 쉬움)
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>대부분의 공개 벤치마크는 이런 방식을 따른다.</li>
</ul>
</li>
<li>객관식 문제 MCQ는 하나 이상의 정답이 있을 수 있음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>일반적인 지표는 정확도 (모델이 맞힌 문제 수)</li>
<li>만들기 쉽고, 검증하기 쉽고, 무작위 베이스라인과 비교해 성능을 평가하기도 쉬움</li>
<li>단점 : 문제와 선택지를 조금만 다르게 해도 모델의 성능이 달라질 수 있음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>파운데이션 모델을 평가하는 좋은 방법인지는 불분명 (분류 능력 != 좋은 응답 생성 능력)</li>
<li>객관식은 지식과 추론을 평가하는데 적합 (요약, 번역, 글 작성같은 능력 평가엔 적합하지 않음)</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">생성 능력</h3>
<p data-ke-size="size16">자연어 생성 : 개방형 텍스트 생성을 연구하는 하위 분야</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">초기 NLG 지표</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>유창성 : 문장이 문법적으로 올바르고 자연스럽게 들리는지</li>
<li>일관성 : 전체 텍스트가 얼마나 잘 구조화됐는지</li>
<li>번역에서는 충실성 (원문의 의미를 얼마나 잘 담아냈는가)</li>
<li>요약에서는 관련성 (원본 문서에서 가장 중요한 내용을 잘 다루고 있는가)</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">큰 수정을 거쳐 현재 사용하긴 하지만 유창성, 일관성의 중요성은 낮아짐, 성능이 떨어지는 모델이나 창의적 글쓰기, 저자원 언어를 다루는 애플리케이션에서 여전히 유용함</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">생성 모델의 능력을 측정할 새로운 평가 지표가 필요하지만, 가장 시급한 문제는 원하지 않은 환각이다.&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>많은 애플리케이션 개발자가 측정하고 싶어 하는 지표
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>사실 관계의 일관성, 안정성(유해성과 편향성을 포함하는 개념)</li>
<li>논쟁성, 친근함, 긍정성, 창의성, 간결성 등..</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">사실 일관성과 비일관성</h4>
<p data-ke-size="size16">사실 일관성을 검증하는 두 가지 방식</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>국소적 사실 일관성 : 출력이 주어진 컨텍스트와 일치하면 사실 관계가 맞다고 봄</li>
<li>전역적 사실 일관성 : 촐력을 공개된 지식에 기반해 평가</li>
</ul>
<p data-ke-size="size16">주로 무엇이 사실인지 판단하는 것이 어려운 부분, 말들은 어떤 출처를 신뢰하는지에 따라 달라짐</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">AI 모델은 어떤 증거를 설득력있다고 판단하는가, 연구에서는 기존 모델들이 과학적 참고 문헌, 중립적인 어조, 사람이 중요하게 생각하는 문체적 특징을 고려하지 않고, 웹사이트와 질의의 관령성에만 지나치게 의존한다고 주장</p>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>환각을 측정하는 지표 설계 시, 출력 결과를 분석해 어떤 종류의 질의에서 환각이 더 자주 발생하는지 파악하는 것이 중요함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>환각을 일으키는 경향을 보이는 질의 유형 : 최소한의 지식을 요구하는 질의, 존재하지 않는 정보를 묻는 질의</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">사실 관계를 평가하기 위한 정교한 AI 판단 기법</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>자체 검증
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 서로 일치하지 않는 여러 출력을 생성하는 경우, 원래의 출력이 환각일 가능성이 높다는 가정을 따름</li>
<li>효과가 있지만 고비용</li>
</ul>
</li>
<li>지식 강화 검증
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>증강 사실성 평가기 SAFE는 검색 엔진을 활용해 응답을 검증</li>
<li>AI 모델로 응답을 개별 문장으로 분리, 각 문장이 독립적으로 이해될 수 있도록 수정, 문장에 대해 구글 검색 API에 보낼 사실 확인 질의를 제안, AI를 사용해 문장이 검색 결과와 일치하는지 판단</li>
</ul>
</li>
</ul>
<img width="1101" height="682" alt="image" src="https://github.com/user-attachments/assets/6fbdf269-35ef-4103-8b79-3f2ff0cae124" />

<p data-ke-size="size16">텍스트 함의 : 두 진술 간의 관계를 파악하는 작업, 전제가 주어지면 가설이 다음 범주 중 어디에 속하는지 결정</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>함의 : 가설은 전제로부터 추론할 수 있다. (사실 일관성)</li>
<li>모순 : 가설은 전제와 모순된다. (사실 비일관성)</li>
<li>중립 : 전제는 가설을 함의하지도, 모순되지도 않는다. (일관성을 판단할 수 없음)</li>
</ul>
<p data-ke-size="size16">사실 일관성 예측에 특화된 평가 모델 학습&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>(전제, 가설) 쌍을 입력으로 받아 함의, 모순, 중립 같은 정의된 클래스 중 하나를 출력, 사실 일관성을 분류 작업으로 만들 수 있음</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>사실 일관성을 위한 벤치마크 : TruthfulQA
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>사람이 잘못된 믿음이나 오해로 부정확하게 응답할 수 있는 817개의 질의로 구성됨</li>
<li>건강, 법률, 금융, 정치 등 38개 분야</li>
<li>참조 응답과 비교해 응답이 사실과 일치하는지 자동으로 평가하도록 파인튜닝된 GPT-judge라는 특수 AI 평가자와 함께 제공됨</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>사실 일관성은 검색 증강 생성 RAG 시스템의 중요한 평가 기준
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>외부 데이터베이스에서 관련 정보를 검색해 컨텍스트를 보완</li>
<li>생성한 응답은 검색된 컨텍스트와 사실 일관성이 있어야 함</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">안정성</h4>
<img width="1045" height="561" alt="image" src="https://github.com/user-attachments/assets/72ec0b06-3e51-48b3-8afc-4c1325f69777" />

<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 생성하는 결과물이 해로울 수 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>이런 시나리오를 감지하기 위해 범용 AI 평가자 사용 가능 (GPT, 클로드, 제미나이)</li>
<li>이런 모델을 제공하는 기업들은 자사 모델의 안정성을 위해 자체 검토 도구를 개발해야 함, 일부는 외부에서도 사용할 수 있게 공개하고 있음</li>
</ul>
</li>
<li>유해한 텍스트는 온라인에 이미 많음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람이 작성한 텍스트의 유해성을 감지하도록 개발된 많은 모델을 AI가 생성한 텍스트에도 활용 가능</li>
<li>범용 AI 평가자보다 작고 빠르고 비용도 적게 든다.</li>
</ul>
</li>
<li>유해성 측정 벤치마크 : RealToxicityPrompts, BOLD</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">지시 수행 능력</h3>
<p data-ke-size="size16">이 모델이 주어진 지시를 얼마나 잘 따르는가, 지시를 따르는 능력은 파운데이션 모델의 핵심 요구사항</p>
<p data-ke-size="size16">더 강력한 모델은 일반적으로 지시를 더 잘 따른다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>감정을 3개로 출력하라했는데 예시에 없는 엉뚱한 결과를 출력하면 지시 수행 능력이 부족한 것</li>
<li>JSON이나 정규 표현식 같은 구조화된 출력이 필요한 애플리케이션에서 필수적</li>
<li>하지만 구조화된 출력을 생성하는 것 이상을 의미함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>4글자 이하의 단어만 사용하기, 아이들이 이해할 수 있는 단어만으로 이야기 만들기</li>
</ul>
</li>
<li>도메인별 능력이나 생성 능력과 쉽게 혼동될 수 있음</li>
<li>모델의 성능은 지시의 품질에 따라 달라지므로 AI 모델을 평가하기 어려움, 나쁜 모델인지 나쁜 지시인지 알기 어려움</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">지시 수행 기준</h4>
<p data-ke-size="size16">벤치마크마다 지시 수행 능력이 포함하는 내용이 다름</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>IFEval, INFOBench
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델이 지시를 따르는 능력을 평가하는 방법에 대한 아이디어를 제공 (어떤 기준 사용, 평가 세트에 어떤 지시를 포함, 어떤 평가 방법이 적절한지)</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>IFEval : 모델이 예상된 형식에 맞는 출력을 생성할 수 있는지에 초점을 맞춤
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>키워드 포함, 길이 제한, 글머리 기호 개수, JSON 형식 등 <b>자동으로 검증</b>할 수 있는 25가지 유형의 지시를 정의</li>
</ul>
</li>
</ul>
<img width="1107" height="1233" alt="image" src="https://github.com/user-attachments/assets/181b02c8-27f1-4bbe-801f-0261e7ff0ba9" />

<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>INFOBench : 지시 수행의 의미를 훨씬 더 폭넓게 봄
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>예상된 형식을 따를 수 있는 능력을 평가할 뿐만 아니라</li>
<li>내용 제약, 언어 지침, 문체 규칙 등을 따를 수 있는 능력도 평가</li>
<li>이러한 지시 유형의 검증은 쉽게 자동화할 수 없음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>검증을 위해 각 지시에 대해 예/아니오로 답할 수 있는 질의 형태의 기준 목록을 만들었음 (이 질의에 사람이나 AI 평가자가 답할 수 있음)</li>
<li>출력이 해당 지시의 모든 기준을 충족하면 모델이 지시를 성공적으로 따랐다고 봄</li>
<li>모델의 최종 점수는 모델이 맞힌 기준 수를 모든 지시의 총 기준수로 나눈 것&nbsp;</li>
</ul>
</li>
<li>GPT4가 합리적으로 신뢰할 수 있고 비용 효율적인 평가자라는 것을 발견</li>
<li>사람 전문가만큼 정확하지는 않지만 아마존 메커니컬 터크를 통해 모집한 평가자보다는 정확</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">하지만 이 두 벤치마크도 실제 세계의 지시를 대표하는 지시를 포함하려 했지만 평가하는 지시의 집합이 다르고 일반적으로 사용되는 많은 지시를 분명히 놓치고 있음, 따라서 벤치마크에서 좋은 성능을 보인다고 항상 좋은 성능을 보이는 것은 아님</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">역할 연기</h4>
<p data-ke-size="size16">모델에게 가상 페르소나를 가정하도록 요청하는 것</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사용자가 상호작용 할 수 있도록 캐릭터는 연기하는 것, 게임이나 대화형 스토리텔링 같은 엔터테인먼트를 위한 경우</li>
<li>모델의 출력 품질을 향상시키기 위해 프롬프트 엔지니어링 기법으로 활용</li>
</ul>
<img width="966" height="510" alt="image" src="https://github.com/user-attachments/assets/e730a236-bbb0-4fdb-ab9c-ec82fddf732e" />

<p data-ke-size="size16">역할 연기 능력 평가는 자동화가 어려움</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>벤치마크 : RoleLLM, CharacterEval</li>
<li>CharacterEval은 사람 평가자를 사용, 역할 연기 측면을 5점 척도로 평가하는 보상 모델 학습</li>
<li>RoleLLM은 신중하게 만든 유사도 점수와 AI 평가자를 모두 사용해 모델이 페르소나를 얼마나 잘 모방하는지 평가</li>
</ul>
<p data-ke-size="size16">모델이 캐릭터를 유지하는지 평가해야 한다. 역할에 따라 출력을 평가하는 휴리스틱을 만들 수 있다.</p>
<p data-ke-size="size16">그 외에는 AI를 평가자로 사용하는 것이 가장 쉬운 자동 평가 방법</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>말투와 지식, 두 가지 측면에서 평가해야 함</li>
<li>역할마다 AI 평가자에게 다른 프롬프트가 필요함</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">비용과 지연 시간</h3>
<p data-ke-size="size16">모델을 평가할 땐 품질, 지연 시간, 비용의 균형을 맞추는 게 중요함</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>파레토 최적화 : 여러 목표를 최적화하는 연구, 현재 활발히 연구되는 분야&nbsp;<br />
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>여러 목표를 최적화할 때는 각 목표에 대해 <b>타협 가능한 수준</b>을 명확히 정해야 함</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">지연시간</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>파운데이션 모델의 지연 시간 지표는 첫 토큰까지 걸리는 시간, 토큰당 시간, 토큰 간 시간, 질의당 시간 등이 있으며 목표에 따라 어떤 지연 시간 지표가 중요한지 이해해야 함</li>
<li>지연시간은 기반 모델 뿐 아니라 프롬프트, 샘플링 변수에도 영향을 받음</li>
<li>프롬프트 작성으로 사용자가 체감하는 전체 지연 시간을 조절할 수 있음
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>반드시 필요한 것과 있으면 좋은 것을 구분해야 함</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">비용</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>API를 사용하면 토큰 단위로 요금이 부과되기 때문에 입력과 출력 토큰을 많이 사용할수록 비용이 증가함, 비용 관리를 위해 입출력 토큰 수를 줄이려고 노력</li>
<li>모델을 호스팅하는 경우, 엔지니어링 비용을 제외하면 주요 비용은 컴퓨팅 자원
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>보유한 장비를 최대한 활용하기 위해 장비에 맞는 가장 큰 모델을 선택</li>
</ul>
</li>
<li>API를 사용하면 규모가 커져도 토큰당 비용은 크게 변하지 않음</li>
<li>자체 호스팅을 하면 규모가 커질수록 토큰당 비용을 줄일 수 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>하루에 최대 10억 개의 토큰을 처리할 수 있는 클러스터에 이미 투자했다면, 하루에 100만 개를 처리하든 10억 개를 처리하든 컴퓨팅 비용은 같은 것</li>
<li>기업은 어떤 방식을 쓸지 결정해야 함</li>
</ul>
</li>
</ul>
<img width="1107" height="511" alt="image" src="https://github.com/user-attachments/assets/a478f784-08d5-43ab-98b4-551319e65fdb" />

<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h2 data-ke-size="size26">모델 선택</h2>
<p data-ke-size="size16">어떤 모델이 가장 좋은가 보다는 만들고자 하는 애플리케이션에 가장 적합한 모델이 무엇인지가 중요</p>
<p data-ke-size="size16">애플리케이션에 대한 기준을 정했다면, 기준에 따라 모델을 평가해야 함</p>
<ol style="list-style-type: decimal;" data-ke-list-type="decimal">
<li>달성할 수 있는 최고 성능 파악하기</li>
<li>비용-성능 축에 모델을 배치하고 투자 대비 최고의 성능을 내는 모델 선택하기</li>
</ol>
<p data-ke-size="size16">선택 과정은 꽤 복잡함</p>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">모델 선택 과정</h3>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li><b>하드 속성</b> : 변경이 불가능하거나 비현실적임
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델 제공업체의 결정 (라이선스, 학습 데이터, 모델 크기)</li>
<li>자체 정책 (개인 정보 보호, 제어)</li>
</ul>
</li>
<li><b>소프트 속성</b> : 변경할 수 있고 기꺼이 변경할 의향이 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>정확도, 유해성, 사실 일관성 : 개선할 수 있는 속성</li>
<li>특정 속성을 얼마나 개선할 수 있는지 추정할 때는 낙관적인 태도와 현실적인 태도 사이에서 균형을 맞추기 까다로울 수 있음</li>
</ul>
</li>
<li>모델과 활용 사례에 따라 달라질 수 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델을 최적화해서 더 빠르게 실행할 수 있으면 지연 시간은 소프트 속성</li>
<li>다른 사람이 호스팅하는 모델을 사용하면 하드 속성</li>
</ul>
</li>
</ul>
<img width="1112" height="1092" alt="image" src="https://github.com/user-attachments/assets/1c460ae9-ee37-4eb9-95ce-f907c5080fab" />

<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">모델 자체 개발 대 상용 모델 구매</h3>
<h4 data-ke-size="size20">오픈 소스, 오픈 가중치, 모델 라이선스</h4>
<p data-ke-size="size16">오픈 소스 모델이라는 용어는 논란의 여지가 생김</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람들이 다운로드하고 사용할 수 있는 모든 모델을 가리키는 데 사용 됐으나, 일부는 모델의 성능이 대부분 학습 데이터의 함수이므로 학습 데이터로 공개될 때만 모델을 오픈으로 봐야 한다고 주장
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>오픈 데이터를 사용하면, 모델 아키텍처, 학습 과정, 학습 데이터 자체를 수정해 모델을 더 유연하게 활용할 수 있음</li>
<li>모델이 불법 데이터로 학습하지는 않았는지 감시 목적으로 접근이 필요한 경우도 있음 (대중이 생성한 데이터이므로 대중이 데이터에 접근할 권리가 있어야 한다)</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>오픈 웨이트 : 데이터 없이 공개된 모델, 오픈 모델 : 데이터와 함께 공개된 모델, 편의를 위해 정의</li>
<li>대다수의 모델은 오픈 웨이트</li>
<li>라이선스
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>MIT, 아파치 2.0, GNU, GPL, BSD 등 수많은 라이선스</li>
<li>오픈 소스 모델이 혼란스러운 상황을 악화시킴
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>많은 모델이 자체적인 고유 라이선스로 출시됨</li>
</ul>
</li>
</ul>
</li>
<li>라이선스에 고유한 조건이 있으므로 필요에 맞게 평가해야 함</li>
<li>반드시 확인해야 할 질문
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>상업적 사용을 허용하는가?</li>
<li>상업적 사용을 허용한다면 어떤 제한이 있는가?</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">오픈 소스 모델과 모델 API 비교</h4>
<img width="887" height="300" alt="image" src="https://github.com/user-attachments/assets/5f07c23f-83e8-40c1-a760-d89d67d5a42e" />

<p data-ke-size="size16">모델 개발자는 모델 개발 후 오픈 소스로 공개하거나, API로 접근하도록 하거나, 둘 다 할 수 있다.</p>
<p data-ke-size="size16">일반적으로 성능이 낮은 모델은 오픈 소스로 공개하고, 가장 성능이 좋은 모델은 유료 API 형태로 제공하거나 자사 서비스의 핵심 기능으로 사용함</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">모델 API는 모델 제공업체, 클라우드 서비스, 서드파티 API 제공업체를 통해 이용할 수 있다. 같은 모델이라도 서로 다른 API를 통해 다른 기능, 제약, 가격으로 제공될 수 있다.&nbsp;</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>GPT-4는 오픈 AI, 애저 API를 통해 이요 ㅇ가능</li>
<li>서로 다른 API가 각기 다른 최적화 기법을 사용할 수 있으므로 같은 모델이라도 약간의 성능 차이가 존재할 수 있음</li>
<li>모델 API 전환할 때도 테스트가 필요</li>
</ul>
<p data-ke-size="size16">큰 모델을 위한 추론 서비스를 개발하는 것이 쉽지 않아 많은 기업들은 직접 개발하기르 원하지 않음</p>
<p data-ke-size="size16">이로 인해 오픈 소스 위에서 작동하는 많은 서드파티 추론 및 파인튜닝 서비스가 생겨남</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>AWS, 애저, 구글 클라우드 같은 주요 클라우드 제공업체들은 모두 인기 있는 오픈 소스 모델에 대한 API 접근을 제공함</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">모델을 직접 호스팅 할지 모델 API를 사용할지는 활용 사례에 따라 다름</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>데이터 프라이버시</li>
<li>데이터 계보</li>
<li>성능</li>
<li>기능성</li>
<li>비용</li>
<li>제어</li>
<li>온디바이스 배포</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">데이터 프라이버시</h4>
<p data-ke-size="size16">엄격한 프라이버시 정책으로 조직 외부에 데이터를 전송할 수 없는 기업은 외부 호스팅 모델 API 사용이 불가능</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">데이터 계보와 저작권</h4>
<p data-ke-size="size16">이는 기업을 여러 방향으로 이끌 수 있다. 오픈 소스 모델로 가거나, 독점 모델을 선택하거나, 둘 다 피하거나</p>
<p data-ke-size="size16">대부분의 모델이 어떤 데이터로 학습됐는지 투명하지 않음</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">AI 관련 지적 재산권법은 계속 진화하고 있다.</p>
<p data-ke-size="size16">AI 응용 프로그램의 특허 가능성은 <b>혁신에 대한 사람의 기여도가 특허를 받기에 충분한지</b>에 달려있다.</p>
<p data-ke-size="size16">저작권이 있는 데이터로 학습한 모델을 써서 제품을 만들었을 때, 그 제품의 지적재산권을 지킬 수 있을지도 불분명하다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>게임, 영화 스튜디오처럼 지적재산권에 생존이 달린 기업은 AI 사용을 꺼림</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">데이터 계보에 대한 우려로 일 부 기업은 학습 데이터를 공개적으로 제공하는 완전 개방형 모델로 방향을 틀었다.&nbsp;</p>
<p data-ke-size="size16">하지만 실제로 파운데이션 모델을 학습할 때 쓰는 크기의 데이터셋을 기업이 철저히 검사하기는 쉽지 않다.&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>이와 같은 우려 때문에 많은 기업이 상용 모델을 선택함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>문제가 발생하면 계약으로 위험을 어느 정도 막을 수 있음</li>
</ul>
</li>
<li>오픈 소스 모델은 상용 모델에 비해 법적 자원이 제한적
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>저작권을 침해하는 오픈 소스 모델을 사용하면 침해당한 쪽이 개발자보다는 사용자를 노릴 가능성이 높음</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">성능</h4>
<p data-ke-size="size16">오픈 소스 모델과 독점 모델 간의 격차가 많이 좁혀짐</p>
<img width="1113" height="751" alt="image" src="https://github.com/user-attachments/assets/f0fd6076-3740-4c08-9929-865154d97425" />

<p data-ke-size="size16">미래에도 최고 성능의 오픈 소스 모델은 최고 성능의 독점 모델보다 뒤처질 가능성이 높음</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>오픈 소스 개발자들이 상용 모델만큼 사용자 피드백을 받아 모델을 개선하기 어렵다.</li>
</ul>
<p data-ke-size="size16">하지만 최고 성능의 모델이 필요하지 않은 활용 사례에서 오픈 소스 모델로 충분할 수 있음</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">기능</h4>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>확장성 : 추론 서비스가 원하는 지연 시간, 비용을 유지하면서 트래픽을 감당하도록 하는 것</li>
<li>함수 호출 : RAG, 에이전트 활용 사례에 필요한 외부 도구를 사용할 수 있는 모델의 능력</li>
<li>출력 구조 : JSON 형식으로 출력을 생성하도록 모델에 요청하는 것과 같은 구조화된 출력</li>
<li>출력 가드레일 : 응답이 차별적이지 않도록 하는 등 생성된 응답의 위험을 줄이는 것
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>이런 기능들을 구현하기 어렵기 때문에, 이런 기능을 사용할 수 있는 API 제공업체로 눈을 돌린다.</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델 API를 쓰면, API가 제공하는 기능만 사용할 수 있다는 단점이 있다.
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>많이 필요한 기능 중 하나 로그프롭 logprobs (분류 작업, 평가, 해석에 유용)</li>
<li>상용 모델 제공업체는 이를 공개하지 않거나 제한적으로만 공개</li>
<li>허용하는 경우에만 파인튜닝 가능</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">API 비용 대 엔지니어링 비용</h4>
<p data-ke-size="size16">모델을 직접 호스팅 하는데도 상당한 시간과 기술력, 엔지니어링 노력이 필요함</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델 최적화, 추론 서비스 확장 및 유지, 모델 가드레일 제공</li>
<li>API보다 엔지니어링이 더 비쌀 수 있음</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">다른 API를 사용하는 것은 SLA(서비스 수준 계약)에 의존해야 한다는 뜻이며, 신뢰성이 떨어지는 API일 경우 가드레일을 만드는데 엔지니어링 노력이 투자될 수 있음</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">일반적으로 조작하기 쉬운 모델이 필요하기에 오픈이든 독점이든 모델을 쉽게 바꿀 수 있도록 표준 API를 따르는 모델이 필요함</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>많은 API 제공업체가 오픈AI의 API를 모방하고 있음</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">제어, 접근성, 투명성</h4>
<img width="867" height="493" alt="image" src="https://github.com/user-attachments/assets/1589e870-36d7-4a57-86e8-289b7ae18c35" />

<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>비즈니스에 사용하는 모델의 통제권을 원하는 것은 당연함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>API 제공업체가 항상 원하는 수준의 통제권을 주지는 않음</li>
</ul>
</li>
<li>모델 제공업체는 과도한 검열이 있을 수 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>특정 사례에서는 제약</li>
<li>실제 얼굴 생성, 물리적 상호작용</li>
</ul>
</li>
<li>갑자기 모델에 대한 접근 권한을 잃는 위험
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>갑자기 예상대로 작동하지 않는 경우 (모델 변경의 투명성 부족)</li>
<li>국가가 금지</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">온디바이스 배포</h4>
<p data-ke-size="size16">디바이스 자체에서 직접 모델을 실행하고 싶다면 서드파티 API는 사용불가, 로컬 실행이 필요할 수 있음</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">&nbsp;</p>
<img width="1100" height="1022" alt="image" src="https://github.com/user-attachments/assets/226151a6-e7ad-44a7-a3f5-b944ce643f82" />

<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">공개 벤치마크 탐색하기</h3>
<p data-ke-size="size16">여러 벤치마크에서 모델을 평가하는 데 도움이 되는 도구는 <b>평가 하네스&nbsp;</b></p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>lm-evaluation-harness 는 400개 이상의 벤치마크를 지원함</li>
<li>evlas 는 약 500개의 기존 벤치마크를 실행하고 오픈AI 모델을 평가하기 위한 새로운 벤치마크를 등록할 수 있게 해줌</li>
</ul>
<h4 data-ke-size="size20">벤치마크 선택 및 집계</h4>
<p data-ke-size="size16">벤치마크 결과를 집계해서 모델의 순위를 매기면 리더보드가 만들어짐</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>리더보드에 어떤 벤치마크를 포함할 것인가</li>
<li>모델 순위를 매기 위해 이런 벤치마크 결과를 어떻게 집계할 것인가</li>
</ul>
<p data-ke-size="size16">자신만의 리더보드를 만드는 방법에 대해 알기 위해 기존 공개 리더보드가 어떻게 만들어졌는지 살펴보면 유용함</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">공개 리더보드</h4>
<p data-ke-size="size16">일부 벤치마크 종합 성능을 기반으로 모델 순위를 매김, 유용하지만 모든 측면을 다루지는 못함</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모델 평가에 필요한 컴퓨팅 자원 제약으로 소수의 벤치마크만 포함할 수도 있음</li>
<li>리더보드 개발자들이 대체로 벤치마크 선정에 신중하지만, 의사결정 과정이 사용자에게 항상 명확하지는 않음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>공개 리더보드는 평가 범위를 넓게 가져가면서도 벤치마크 개수와 균형을 맞추려 함</li>
<li>추론 능력, 사실 관계의 정확성, 수학, 과학과 관련된 전문 분야의 능력을 평가할 수 있는 핵심 벤치마크만 골라서 사용
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>평가 범위, 개수에 대한 이유는 명확하지 않음</li>
<li>리더보드 개발자들도 선정 기준을 명확히하지 못할 만큼 설명하기 어려운 작업</li>
</ul>
</li>
</ul>
</li>
<li>벤치마크 상관관계 : 두 벤치마크가 높은 상관관계를 보이면 둘 다 사용할 필요없음, 오히려 편향되는 결과</li>
</ul>
<p data-ke-size="size16">공개 리더보드는 성능을 파악하기 유용하지만, 해당 리더보드가 어떤 능력을 측정하려 하는지 이해하는 것이 중요함</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">공개 벤치마크로 맞춤형 리더보드 만들기</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>자신만의 평가 기준으로 모델 순위를 매기는 개인 리더보드 만들기<br />
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>필요한 핵심 능력을 평가할 수 있는 벤치마크 수집</li>
<li>점수를 얻고 모델 순위 매기기
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>모든 벤치마크가 같은 척도를 사용하지 않음</li>
<li>공개 벤치마크가 필요를 반영하지 못할 수 있고 오염되었을 가능성도 높음</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">공개 벤치마크의 데이터 오염</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>데이터 오염 : 데이터 유출, 테스트 세트로 학습하기, 부정행위 등</li>
<li>모델이 답을 단순히 외워서 높은 평가 점수를 받는 것&nbsp;</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">데이터 오염이 일어나는 방식</h4>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>모델 학습 전 공개된 벤치마크 데이터가 포함되는 경우</li>
<li>학습 데이터와 평가 데이터가 동일한 출처에서 오는 경우 (간접적 발생)</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">데이터 오염 다루기</h4>
<p data-ke-size="size16">휴리스틱 방법</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>n-gram 중복 : 평가 샘플의 특정 시퀀스가 학습 데이터에도 있는 경우
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>대부분 학습 데이터에 접근 불가능, 사용 불가</li>
</ul>
</li>
<li>퍼플렉시티 : 평가 데이터에 대해 유난히 퍼플렉시티가 낮은 경우
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>적은 자원으로 가능하지만 정확도 떨어짐</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">모델 개발자들은 학습 전에 학습 데이터에서 주요 벤치마크를 제거함, 전체 벤치마크 + 오염되지 않은 샘플 각각 어떤 성능을 보이는지 공개하는게 이상적이지만 오염을 감지하고 제거하는 데 노력이 많이 필요하여 많이 그냥 넘어가는 부분</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>허깅페이스에서는 이상치를 감지하기위해 특정 벤치마크에 대한 모델들의 성능 표준편차를 그래프로 나타냄</li>
</ul>
<p data-ke-size="size16">공개 벤치마크는 나쁜 모델을 걸러내는 데 도움이 되지만, 활용 사례에 적합한 모델을 찾는 데는 도움이 되지 않음.</p>
<p data-ke-size="size16">공개 벤치마크로 유명한 모델 몇 개를 추린 후에 자체 평가 파이프라인을 돌려 용도에 맞는 모델을 찾아야 함</p>
<p data-ke-size="size16">&nbsp;</p>
<hr contenteditable="false" data-ke-type="horizontalRule" data-ke-style="style6" />
<h2 data-ke-size="size26">평가 파이프라인 설계하기</h2>
<h3 data-ke-size="size23">1 단계: 시스템의 모든 구성 요소 평가하기</h3>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>과제별, 단계별, 중간 출력별로 다양한 수준에서 평가가 이루어질 수 있음</li>
<li>엔드투엔트 출력과 각 구성 요소의 중간 출력을 독립적으로 평가해야 함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>시스템이 어디서 실패하는지 정확히 알기 위해</li>
</ul>
</li>
<li>턴 별로 작업별로 모두 평가해야 함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>하나의 턴은 여러 단계와 메시지로 구성될 수 있음 (결과물 생성을 위해 여러 단계를 거쳐도 하나의 턴)</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>턴 기반 평가 : 각 출력물의 품질을 평가</li>
<li>작업 기반 평가 : 시스템이 작업을 완료했는지를 평가
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>과제 완수를 돕는 능력이 중요하다고 보면 이게 더 중요</li>
<li>작업 간 경계를 구분하기 힘들 수 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>동시에 여러 질의를 하는 경우, 기존 작업의 후속 질의인지 새로운 작업인지 알기 어려움</li>
</ul>
</li>
<li>BIG-bench 벤치마크 모음의 twenty_question 벤치마크
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>스무고개, 예/아니오로만 대답, 점수는 맞추는 데 얼마나 많은 질의가 필요했는가</li>
</ul>
</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">2 단계: 평가 가이드라인 만들기</h3>
<p data-ke-size="size16">가장 중요한 단계</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>해야할 일, 하면 안 되는 일 정의</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">평가 기준 정의하기</h4>
<p data-ke-size="size16">좋다는 것이 무엇을 의미하는지 정하는 것이 어려움</p>
<p data-ke-size="size16">기준을 도출하기 위해 이상적으로는 실제 사용자 질의인 테스트 질의로 실험하거나, 테스트 질의마다 수동으로 or AI 모델을 사용해 여러 응답을 생성하고 좋은지 나쁜지 판단</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">예시와 함께 평가 기준표 만들기</h4>
<p data-ke-size="size16">평가 시스템 선택 : 0과 1, 1부터 5, 0과 1 사이 등</p>
<p data-ke-size="size16">해당 점수의 응답은 어떤 모습인지, 왜 그 점수인지 기준표를 만들고 동료, 친구 등과 검증하며 모호함을 없애기 위해 다듬기</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">평가 지표를 비즈니스 지표와 연결하기</h4>
<p data-ke-size="size16">평가 지표가 비즈니스 지표에 미치는 영향을 이해해야 함</p>
<p data-ke-size="size16">특정 지표를 개선했을 때, 얻을 수 있는 이득이 얼마인지 알면, 자원 투자에 확신을 가질 수 있음</p>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">목표로 하는 비즈니스 지표를 이해해야 함</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>일간, 주간, 월간 활성 사용자와 같은 고착도</li>
<li>월간 시작하는 대화 수, 방문 기간과 같은 참여지표</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h3 data-ke-size="size23">3 단계: 평가 방법과 데이터 정의하기</h3>
<h4 data-ke-size="size20">평가 방법 선택하기</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>서로 다른 기준에는 서로 다른 평가 방법이 필요할 수 있음
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>e.g. 유해성 감지에 특화된 분류기, 응답과 사용자 질의 간 의미적 유사도...</li>
</ul>
</li>
<li>동일한 기준에 대해 여러 평가 방법을 혼합해 사용할 수도 있음</li>
<li>가능한 자동 지표를 사용하되, 사람 평가에 의존하는 것을 두려워하지 말기
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사람 평가를 북극성 지표로&nbsp;</li>
</ul>
</li>
<li>평가 방법은 운영 환경에서도 사용함
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>사용자 피드백 (어떤 종류, 다른 평가 지표와 어떻게 연결되는지 등)</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">평가 데이터 주석 달기</h4>
<p data-ke-size="size16">주석이 달린 예시 세트 선별하기</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>턴 기반 평가, 작업 기반 평가 모두 각 구성 요소와 각 기준을 평가하기 위해 주석이 달린 데이터가 필요함</li>
<li>자연스러운 레이블이 없다면 사람이나 AI로 지정할 수 있음</li>
<li>평가를 위한 주석 가이드라인은 후에 파인튜닝을 위한 지시 데이터 만드는 데 재사용 가능</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">시스템에 대한 세분화된 이해를 얻기 위한 데이터 슬라이스 : 데이터를 하위 집합으로 나누고 각 하위 집합에 대한 시스템 성능을 개별적으로 살펴보는 것</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>세분화된 이해는 아래와 같은 목적에 도움이 된다.
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>편향 축소, 디버깅, 애플리케이션 개선 영역 발굴, 심슨의 역설 회피 (<span style="background-color: #ffffff; color: #474747; text-align: start;">특정 집단, 그룹 내에서 발견되는 추세가 전체적으로 발견되는 추세가 다른 현상)</span></li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">좋은 평가를 위해서 여러 평가 세트를 갖춰야 한다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>실제 운영 환경의 데이터 분포를 나타내는 하나의 평가 세트로 시스템의 선반적인 성능 추정 가능</li>
<li>등급, 사용량 등</li>
<li>시스템이 자주 실수하는 것으로 알려진 예시 등 중요하게 생각되는게 있으면 테스트 세트를 만들자</li>
<li>애플리케이션마다 필요한 데이터 양은 다름
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>평가 세트는 결과를 신뢰할 만큼 충분히 크되, 실행 비용이 많이 들지 않을 정도로 작아야 함</li>
</ul>
</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">평가 결과는 시스템을 독립적으로 평가하는 데만 사용되는게 아니라 시스템을 비교하는 데도 사용됨</p>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">평가 파이프라인 평가하기</h4>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>평가 파이프라인이 올바른 신호를 제공하고 있는가
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>더 나은 응답이 실제로 높은 점수를 받는가, 더 나은 평가 지표가 더 나은 비즈니스 결과로 이어지는가</li>
</ul>
</li>
<li>평가 파이프라인은 얼마나 신뢰할 수 있는가
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>같은 파이프라인을 두 번 실행하면 결과가 나오는가, 여러 번 실행했을 때 평가 결과의 분산은 어느 정도인가, 재현성을 높이고 분산을 줄이는 것을 목표로 해야 한다. 평가 구성을 일관되게 유지하자</li>
</ul>
</li>
<li>지표 간 상관관계는 어떠한가
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>상관관계가 높은 두 지표는 둘 다 필요하지 않다, 전혀 상관관계가 없다면 모델에 대한 흥미로운 통찰력을 제공하거나 해당 지표가 신뢰할 수 없거나</li>
</ul>
</li>
<li>평가 파이프라인이 애플리케이션에 얼마나 많은 비용과 지연 시간을 추가하는가</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<h4 data-ke-size="size20">반복</h4>
<p data-ke-size="size16">요구사항과 사용자 행동이 변화하며, 평가 기준도 진화하고 평가 파이프라인도 반복으로 개선해야 한다.</p>
<ul style="list-style-type: disc;" data-ke-list-type="disc">
<li>평가 기준 업데이트, 기준표 변경, 예시 추가 혹은 제거</li>
<li>반복이 필요하지만 일정 수준의 일관성을 기대할 수 있어야 한다. 변경되는 평가 프로세스는 개발 지침으로 사용 불가능</li>
</ul>
<p data-ke-size="size16">&nbsp;</p>
<p data-ke-size="size16">반복적인 개선, 적절한 실험 추적</p>
<ul style="list-style-type: circle;" data-ke-list-type="circle">
<li>평가 데이터, 기준표, AI 평가자에 사용된 프롬프트 및 샘플링 구성 등 평가 프로세스에서 변경될 수 있는 모든 변수를 기록하자</li>
</ul>

