그래서, 이번 주까지 우리는 기능을 감지하고, 설명자를 계산하고, 거리 함수를 사용하여 무차별 대입 매칭을 수행하는 방법을 배웠습니다. 우리는 자율주행 자동차 인식에 기능 감지, 설명 및 매칭을 적용할 준비가 거의 되어 있습니다. 이 비디오에서, 우리는 모호한 경기 문제와 거리 비율 제형을 통해 유사한 기능 설명자로 인한 매칭 오류에 대한 경기를 더 강력하게 만드는 방법을 탐구할 것입니다. 하지만 먼저, 지난 수업에서 논의한 두 가지 기능 매칭 사례를 검토해 봅시다. 첫 번째 경우, 우리는 기능 f2에 대한 작은 거리와 두 번째 이미지의 다른 기능과의 큰 거리를 명확하게 제공하는 유용한 기능 설명자를 가지고 있습니다. 이 경우 f1 및 이미지 1 기능과 올바른 일치 항목을 성공적으로 식별할 수 있습니다. 우리의 무차별 대입 매칭 알고리즘은 이 설명자와 잘 작동하며 이미지 2에서 올바른 일치를 원활하게 찾을 수 있습니다. 두 번째 경우, 이미지 1의 기능 f1은 이미지 2에서 전혀 일치하지 않습니다. 우리는 이 경우 잘못된 일치를 제거하기 위해 무차별 대입 매칭 알고리즘을 임계값 델타로 수정했습니다. 피처와 이미지 2 모두 거리 임계값 델타보다 큰 거리를 가지고 있기 때문에, 무차별 대입 매처는 f2와 f3 기능을 모두 잠재적인 일치로 거부하고 일치가 반환되지 않습니다. 하지만, 세 번째 사례를 고려해 봅시다, 다시 한번 우리는 이미지 1의 기능 f1을 이미지 2의 해당 기능과 일치시키려고 노력하고 있습니다. 여기에 제시된 기능 벡터를 사용하면, 기능 f1은 이미지 2의 기능 2로 9의 SSD 값을 얻습니다. 우리는 또 다른 기능 f3를 테스트하고, 또한 9개의 SSD를 얻습니다. 이 두 기능 모두 이 경우 델타보다 작은 SSD를 가지고 있으며, 따라서 유효한 일치입니다. 그래서 우리는 무엇을 해야 할까요? 우리는 3의 경우 기능 fi를 모호한 일치가 있는 기능으로 언급합니다. 이 문제에 대한 우아한 해결책은 1999년 데이비드 로우에 의해 제안되었다. 해결책은 다음과 같다. 첫째, 우리는 이전 알고리즘과 마찬가지로 이미지 1의 기능 fi와 이미지 2의 모든 기능 fj 사이의 거리를 계산하며, 가장 가까운 일치로 이미지에서 fi를 특징으로 하는 최소 거리를 가진 이미지 2의 기능 fc를 선택합니다. 그런 다음 기능 fi에 두 번째로 가까운 거리에 있는 이미지 2의 기능을 얻습니다. 마지막으로, 우리는 두 번째로 가까운 경기 fs보다 가장 가까운 경기 fc가 얼마나 가까운지 찾습니다. 이것은 거리 비율을 통해 이루어질 수 있다. 거리 비율은 이미지 1의 피처 fi와 이미지 2에서 가장 가까운 fc 사이의 거리로 정의될 수 있다. 피처 fi와 fs 사이에서 계산된 거리에서, 이미지 2에서 두 번째로 가까운 일치. 거리 비율이 하나에 가깝다면, 설명자와 거리 함수에 따라 fi가 fs와 fc와 일치한다는 것을 의미합니다. 이 경우, 이미지 2의 어느 위치가 이미지 1의 기능에 해당하는지 명확하게 알려져 있지 않기 때문에 나중에 프로세싱에 이 일치를 사용하고 싶지 않습니다. 무차별 대입 매처 알고리즘을 거리 비율 제형으로 업데이트합시다. 업데이트는 경기를 유지하기 위한 미터법으로 거리를 거리 비율로 대체합니다. 우리는 보통 약 0.5에서 행이라고 부를 거리 비율 임계값을 설정했는데, 이는 우리가 초기 기능 설명자와 두 번째로 잘 일치하는 것보다 적어도 두 배나 가까울 것을 의미합니다. 사례 3을 다시 보면, 우리는 거리 비율과 0.5로 설정된 해당 임계값 행을 사용하여 모호한 경기를 버리고 좋은 경기를 유지한다는 것을 알 수 있습니다. 이 비디오에서, 당신은 모호한 경기가 무엇인지, 그리고 거리 비율 제형을 통해 이러한 모호한 일치를 처리하는 방법을 배웠습니다. 불행하게도, 거리 비율 공식에도 불구하고, 현대 설명자를 사용할 때 일반적인 일치의 50%가 여전히 틀릴 수 있다. 이미지의 반복적인 패턴과 픽셀 값의 작은 변화는 종종 매칭 프로세스를 혼란스럽게 하기에 충분하기 때문이다. 우리는 이러한 잘못된 경기를 이상값이라고 부른다. 다음 수업을 위해, 추가 인식 작업에 일치하는 기능을 사용하기 전에 이상값을 설명하고 제거하는 방법을 설명하겠습니다.