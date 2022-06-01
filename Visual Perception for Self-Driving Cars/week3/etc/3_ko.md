[음악] 지금까지 이 모듈에서, 우리는 피드포워드 신경망 모델로 구성된 것과 손실 함수를 사용하여 신경망 모델의 성능을 평가하는 방법을 검토했습니다. 이 수업은 신경망 설계의 최종 주요 구성 요소인 훈련 과정을 설명할 것이다. 구체적으로, 우리는 다음 질문에 대답할 것이다. 주어진 훈련 데이터에 대한 피드포워드 신경망에 대한 최고의 매개 변수 세트 세타를 어떻게 얻을 수 있을까요? 답은 적절한 매개 변수 초기화와 함께 반복적인 최적화 절차를 사용하는 것이다. 먼저 이전에 설명한 피드포워드 신경망 훈련 절차를 다시 살펴보겠습니다. 훈련 데이터 입력 x와 해당 올바른 출력인 f star of x를 감안할 때, 우리는 먼저 숨겨진 레이어를 통해 입력 x를 통과한 다음 출력 레이어를 통과하여 최종 출력 y를 얻습니다. 여기서 출력 y는 매개 변수 세타의 함수라는 것을 알 수 있습니다. 그리고 세타는 네트워크 내부의 아핀 변환의 가중치와 편견을 포함한다는 것을 기억하세요. 다음으로, 우리는 x의 예측된 출력 f와 세타를 손실 함수를 통해 올바른 출력인 x의 f 별과 비교합니다. 손실 함수는 네트워크 출력과 실제 출력 사이의 오류가 얼마나 큰지 측정한다는 것을 기억하십시오. 우리의 목표는 전체 데이터 세트에서 손실 함수에 대한 작은 가치를 얻는 것입니다. 손실 함수를 가이드로 사용하여 손실 함수의 더 낮은 값을 제공할 것으로 예상되는 새로운 매개 변수 세타 세트를 생성합니다. 특히, 우리는 매개 변수 세타를 수정하기 위해 손실 함수의 그라디언트를 사용합니다. 이 최적화 절차는 그라데이션 하강으로 알려져 있다. 그라데이션 하강을 자세히 설명하기 전에, 신경망 손실 기능을 다시 살펴봅시다. 보통, 우리는 자율주행 작업에 사용할 수 있는 수천 개의 훈련 예제 쌍, x와 f star of x가 있습니다. 우리는 개별 훈련 사례에 대한 손실의 의미로 모든 훈련 예에 대한 손실을 계산할 수 있습니다. 그런 다음 모든 훈련 예에서 개인 손실의 그라디언트의 평균과 동일한 매개 변수 세타에 대해 훈련 손실의 그라디언트를 계산할 수 있습니다. 여기서 우리는 그라디언트와 합이 선형 연산자라는 사실을 사용합니다. 따라서 합계의 그라디언트는 개별 그라디언트의 합과 같다. 공식화된 그라데이션 방정식을 사용하여, 우리는 이제 배치 그라데이션 하강 최적화 알고리즘을 설명할 수 있습니다. 배치 그라데이션 하강은 선형 1차 최적화 방법이다. 반복은 매개 변수 세타의 초기 추측에서 시작하여 이러한 매개 변수를 반복적으로 개선한다는 것을 의미합니다. 첫 번째 순서는 알고리즘이 매개 변수 세타를 개선하기 위해 첫 번째 순서 미분만 사용한다는 것을 의미합니다. 배치 그라데이션 하강은 다음과 같습니다. 첫째, 신경망의 매개 변수 세타가 초기화된다. 둘째, 알고리즘을 종료하고 최종 매개 변수 세트를 반환하는 정지 조건이 결정됩니다. 반복 절차가 시작되면, 알고리즘에 의해 가장 먼저 수행되는 것은 델 서브 세타로 표시된 매개 변수 세타에 대한 손실 함수의 그라디언트를 계산하는 것이다. 그라디언트는 이전에 파생된 방정식을 사용하여 계산할 수 있습니다. 마지막으로, 매개 변수 세타는 계산된 그라디언트에 따라 업데이트됩니다. 여기서 엡실론은 학습 속도라고 불리며 모든 반복에서 음수 그라디언트 방향으로 매개 변수를 조정하는 양을 제어합니다. 2D 케이스에서 배치 그라데이션 하강의 시각적 예를 살펴보겠습니다. 여기서, 우리는 세타의 함수 J를 최소화하는 매개 변수 세타 원과 세타 2를 찾으려고 노력하고 있습니다. 세타는 동등한 가치의 윤곽선으로 표시된 직사각형 공 모양이다. 그라디언트 하강은 각 반복에서 그릇을 한 단계 내려가는 새로운 매개 변수 세타를 반복적으로 찾습니다. 알고리즘의 첫 번째 단계는 매개 변수 세타를 초기화하는 것이다. 초기 매개 변수를 사용하여 빨간색 점으로 표시된 손실 함수의 초기 값에 도달합니다. 우리는 초기 매개 변수 값 세타 1과 세타 2에서 손실 함수의 그라디언트를 계산하여 그라디언트 하강을 시작합니다. 업데이트 단계를 사용하여 손실 함수의 더 낮은 지점에 도달하기 위해 새로운 매개 변수를 얻습니다. 우리는 정지 기준을 달성할 때까지 이 과정을 반복한다. 그런 다음 손실 함수를 최소화하는 최적의 세트로 매개 변수 세타 1과 세타 2의 마지막 세트를 얻습니다. 제시된 알고리즘에서 두 조각이 여전히 누락되었다. 매개 변수의 데이터를 어떻게 초기화하고 알고리즘을 실제로 중지할 시기를 어떻게 결정하나요? 이 두 질문에 대한 답은 여전히 실제로 잘 작동하는 휴리스틱에 기반을 두고 있다. 매개 변수 초기화를 위해, 우리는 보통 표준 정규 분포를 사용하여 가중치를 초기화하고 편향을 0으로 설정합니다. 문학에서 널리 사용되는 특정 활성화 기능에 특정한 다른 휴리스틱이 있다는 것은 언급할 가치가 있다. 우리는 이러한 휴리스틱 중 일부를 보충 재료로 제공합니다. 그라데이션 하강의 정지 조건을 정의하는 것은 조금 더 복잡하다. 훈련 알고리즘을 언제 중단할지 결정하는 세 가지 방법이 있다. 가장 간단히 말해서, 우리는 미리 정의된 최대 그라디언트 하강 반복 수에 도달하면 중단하기로 결정할 수 있다. 또 다른 휴리스틱은 반복 사이에 매개 변수 세타가 얼마나 변했는지에 달려 있다.  작은 변화는 알고리즘이 더 이상 매개 변수를 효과적으로 업데이트하지 않는다는 것을 의미하며, 이는 최소값에 도달했다는 것을 의미할 수 있다. 마지막으로 널리 사용되는 정지 기준은 반복 간의 손실 함수 값의 변화이다. 다시 말하지만, 반복 간의 손실 함수의 변화가 작아짐에 따라, 최적화는 최소한으로 수렴되었을 가능성이 높다. 이러한 정지 조건 중 하나를 선택하는 것은 당면한 문제에 가장 적합한 것의 문제이다. 우리는 훈련 과정의 함정 중 일부와 이를 피하는 방법을 연구하면서 다음 수업에서 정지 조건을 재검토할 것입니다. 불행하게도, 배치 그라데이션 하강 알고리즘은 심각한 단점을 겪고 있다. 그라디언트를 계산하기 위해 우리는 백프로포그를 사용한다. 백프로포깅은 그라디언트를 평가하려는 예시에 대한 네트워크의 출력을 계산하는 것을 포함한다. 그리고 배치 그라디언트 하강은 전체 훈련 세트에서 그라디언트를 평가합니다. 단일 업데이트 단계를 수행하는 것이 매우 느리게 만든다. 다행히도, 법칙은 기능하고 그라디언트는 훈련 데이터 세트에 대한 수단이다. 예를 들어, 우리는 N 샘플 세트에서 추정된 평균의 표준 오류가 N의 제곱근 위의 시그마라는 것을 알고 있습니다. 여기서 시그마는 분포의 표준 편차이고 N은 평균을 추정하는 데 사용되는 샘플의 수이다. 그것은 그라데이션 추정치의 오차 감소율이 샘플 수에서 선형보다 적다는 것을 의미합니다. 이 관찰은 이제 훈련 데이터의 작은 하위 샘플이나 미니 배치를 사용하여 그라데이션 추정치를 계산할 수 있기 때문에 매우 중요합니다. 그렇다면 미니 배치를 사용하여 배치 그라데이션 하강 알고리즘을 어떻게 수정하나요? 수정은 사실 꽤 간단하다. 기본 알고리즘의 유일한 변경은 샘플링 단계이다. 여기서 우리는 훈련 데이터의 하위 샘플 n 프라임을 미니 배치로 선택합니다. 이제 그라디언트를 평가하고 배치 등급 하강과 동일한 방식으로 업데이트 단계를 수행할 수 있습니다. 이 알고리즘은 각 반복의 미니배치에 포함할 샘플을 무작위로 선택하기 때문에 확률 또는 미니배치 그라데이션 하강이라고 불린다. 그러나, 이 알고리즘은 우리가 사용하려는 미니배치의 크기인 추가 매개 변수를 결정하게 한다. 적절한 미니배치를 선택하려면, 어떤 종류의 하드웨어가 특정 크기의 데이터 어레이로 더 나은 런타임을 달성한다는 점에 유의해야 합니다. 특히 GPU를 사용할 때, GPU 컴퓨팅과 메모리 아키텍처와 일치하는 두 가지 미니 배치 크기의 힘을 사용하는 것이 일반적이다. 따라서 GPU 리소스를 효율적으로 사용하세요. 배치 크기 선택을 주도하는 몇 가지 요소를 살펴봅시다. GPU와 같은 멀티코어 아키텍처는 일반적으로 매우 작은 배치 크기에 의해 활용도가 낮으며, 이는 미니배치를 처리하는 시간을 줄일 수 없는 절대적인 최소 배치 크기를 사용하도록 동기를 부여합니다. 게다가, 큰 배치 크기는 보통 그라디언트의 더 정확한 추정치를 제공한다. 네트워크 성능을 더 안정적으로 향상시키는 방향으로 하강을 보장합니다. 그러나 앞서 언급했듯이, 추정치의 정확성의 개선은 선형보다 적다. 반면에 작은 배치 크기는 정규화 효과를 제공하는 것으로 보였다. 종종 배치 크기로 볼 수 있는 최고의 일반화. 일반화가 무엇을 의미하는지 잘 모르겠다면, 걱정하지 마세요. 우리는 다음 수업에서 그것을 더 자세히 탐구할 것이다. 게다가, 최적화 알고리즘은 일반적으로 그라디언트의 대략적인 추정치를 빠르게 계산하고 정확한 그라디언트를 계산하고 더 적은 반복을 수행하기보다는 더 자주 반복할 수 있다면 더 빨리 수렴한다. 이러한 절충의 결과로, 두 개의 미니 배치 크기의 일반적인 전력은 32에서 256까지 다양하며, 더 작은 크기는 때때로 대형 모델이나 일반화를 개선하려고 시도된다. 명심해야 할 마지막 문제는 미니배치를 샘플링하기 전에 데이터 세트를 섞어야 한다는 것이다. 데이터 세트를 전혀 섞지 않으면 네트워크의 효율성을 줄일 수 있습니다. 문학에는 확률적 그라데이션 하강의 많은 변형이 존재하며, 각각 고유한 장점과 단점이 있다. 사용할 변형을 선택하는 것은 어려울 수 있으며, 때로는 변형 중 하나가 다른 문제보다 특정 문제에 더 잘 작동합니다. 자율주행 애플리케이션을 위한 간단한 경험 법칙으로서, 안전한 선택은 ADAM 최적화 방법이다. 그것은 초기 매개 변수 세타에 매우 강력하며, 널리 사용된다. 이 차이에 대해 더 알고 싶다면, 보충 노트에 나열된 리소스를 살펴보세요. 이 수업에서는 배치 그라데이션 하강을 사용하여 신경망의 매개 변수를 최적화하는 방법을 배웠습니다. 당신은 또한 이 최적화 알고리즘의 제안된 차이가 많다는 것을 배웠고, 안전 결함 선택은 ADAM입니다. 축하합니다, 당신은 신경망을 구축하고 훈련시키는 데 필요한 필수 단계를 마쳤습니다. 다음 수업에서는 학습 속도와 같은 네트워크 교육을 개선하기 위해 최적화 매개 변수를 선택하는 방법에 대해 논의할 것입니다. 또한 검증 세트를 사용하여 신경망의 성능을 평가하는 방법에 대해 논의할 것입니다. 다음에 보자. [음악]