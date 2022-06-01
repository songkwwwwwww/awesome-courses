이 과정의 세 번째 주에 오신 것을 환영합니다. 이번 주에 우리는 자율주행 차량 설계에 안전을 통합하는 기본 사항을 살펴볼 것입니다. 이 모듈을 통해, 우리는 최근의 자율주행 차량 충돌 보고서 중 일부를 논의한 다음, 자율주행 자동차의 안전 개념을 공식적으로 정의하고, 발생하는 가장 일반적인 위험 원인에 대해 논의할 것입니다. 우리는 안전에 대한 몇 가지 업계의 관점에 대해 논의할 것이며, 마지막으로 안전한 시스템 설계에 사용되는 몇 가지 공통 프레임워크에 대해 논의함으로써 마무리할 것입니다. 이 수업에서, 우리는 2017년과 2018년의 자율주행 자동차 충돌의 첫 번째 발생률에 대해 논의할 것입니다. 그런 다음, 우리는 몇 가지 기본 안전 개념을 정의하고 자율주행 차량 위험의 가장 일반적인 원인 중 일부를 나열하고, 안전에 대한 낮은 수준의 높은 수준의 요구 사항에 대해 논의할 것입니다. 우리는 이 모듈의 자료가 대부분 국제표준기구, ISO에 의해 출판된 지침에서 가져온 것임을 지적해야 한다. 온라인에서 이러한 프레임워크의 보다 포괄적인 버전을 찾을 수 있습니다. 지금까지 더 눈에 띄는 자율주행차 고장의 일부에 대한 논의부터 시작합시다. 2016년 3월, 자율주행 구글 자동차인 웨이모는 장애물 뒤에서 철수하려고 시도했을 때 버스 옆으로 달려갔다. 버스가 뒤쪽에서 접근하고 있었고 돌릴 준비가 된 차선 오른쪽에 있는 차선에서 구글 자동차를 통과하는 것을 목표로 하고 있었다. 구글 자동차 소프트웨어는 버스와 다음 차선에서 자동차 사이의 격차가 너무 좁기 때문에 버스가 그것을 통과하려고 시도하지 않을 것이라고 믿었다. 버스는 구글이 예상했던 것보다 더 작은 격차를 통해 습관적으로 충돌로 이어지는 것으로 밝혀졌다. 구글 자동차가 버스 위치의 새로운 측정에 반응할 수 있을 때, 너무 늦었다. 이것은 다른 모든 차량 행동이 일어나기 전에 예측하는 것이 얼마나 어려운지에 대한 한 예일 뿐입니다. 1년 후, 우버 자율주행 차량은 다른 차량으로 인한 경미한 충돌 중에 과민반응하여 결국 전복했다. 차량의 동적 모델은 자동차에 작용하는 다른 차량의 상당한 교란력을 가정하지 않기 때문에, 컨트롤러는 그러한 시나리오에 대해 테스트되지 않았고 과민반응했을 가능성이 높다. 이 충돌은 제어 시스템에 통합된 견고성과 가능한 한 많은 예측 가능한 많은 이벤트를 다루는 탐색 테스트의 필요성을 강조한다. 2017년 말, GM 크루즈 시보레 볼트는 차선 변경 기동을 중단한 후 오토바이 운전자를 쓰러뜨렸다. 볼트가 기동을 시작한 후, 인접한 차선에서 제동 리드 차량으로 인해 들어가기를 희망했던 간격이 빠르게 닫혔다. 차선이 갈라지고 있던 오토바이 운전자는 볼트 옆으로 앞으로 나아가 돌아오는 기동을 막았다. 볼트는 오토바이와 충돌하거나 인접한 차선에서 두 차에 충돌하기 위해 딜레마 상황에 갇혔다. 여기서 하나 또는 다른 결과를 선택하기 위한 구체적인 결정이 내려졌다는 것은 분명하지 않으며, 소송이 사건의 세부 사항을 묻었다. 그러나, 다른 요원들도 자율주행 자동차 행동을 예측하고 있기 때문에, 많은 상황에서 올바른 행동이 무엇인지 평가하는 것은 매우 어렵다. 가능하다면, 더 공격적인 운전 스타일로 합병이 가능했을 수도 있고 약간 지연된 중단은 오토바이 운전자를 피하기에 충분한 시간이었을 수도 있다. 의사 결정의 빡빡한 상호 작용은 여전히 자율주행 자동차에서 큰 도전이다. 마지막으로, 우리는 2018년 초에 보행자 사망자로 이어진 우버 사고에 대해 조금 이야기해야 합니다. 애리조나주 템피에서 운영되는 우버는 당시 안전 운전자들이 자율 소프트웨어를 모니터링하는 광범위한 테스트 프로그램을 가지고 있었다. 그 사건은 밤에 넓은 다층 분할 도로에서 발생했으며, 보행자가 표시가 없는 지역의 도로를 가로질러 자전거를 걷고 있었다. 희생자인 일레인 헤르츠버그는 템피 출신의 49세 여성이었다. 이것은 새의 시선에서 묘사된 차와 장면이다. 왼쪽에서 들어오는 보행자와 이미지 하단에서 도로를 따라 이동하는 차량을 볼 수 있습니다. 예비 조사에 따르면 그 사건으로 이어진 여러 실패가 있었다. 다양한 기여 요인을 살펴보자. 첫째, 안전 운전자에 대한 실시간 검사는 없었다. 이 경우, 안전 운전자는 부주의했고 당시 훌루를 보고 있었다고 한다. 안전 운전자는 무엇이든 할 수 있었고 우버는 운전자의 주의를 평가할 방법이 없었다. 자율주행 시스템이 작동하는 것을 보는 것은 집중하기 어려운 일이기 때문에, 안전 운전자 모니터링 시스템을 갖는 것이 정말 중요하다. 둘째, 소프트웨어 탐지 시스템에 상당한 혼란이 있었다. 영향을 미치기 위해 6초에 처음 감지되었을 때, 피해자는 먼저 알려지지 않은 물체로 분류된 다음 차량으로 잘못 분류된 다음 자전거로 잘못 분류되었다. 결국, 자율 소프트웨어가 내린 결정은 탐지를 무시하는 것이었는데, 아마도 너무 신뢰할 수 없었기 때문일 것이다. 인식은 완벽하지 않으며 스위칭 분류로 인해 차량이 그런 물체를 완전히 무시하지 말았어야 했다. 마침내, 충돌 1.3초 전에, 볼보 비상 제동 시스템은 보행자를 감지했고 충격 속도를 줄이기 위해 브레이크를 빠르게 적용하여 잠재적으로 일레인 헤르츠버그의 생명을 구했을 것이다. 그러나 테스트 중에 여러 충돌 방지 시스템이 동시에 작동하는 것은 안전하지 않으므로 우버는 자율 모드에서 볼보 시스템을 비활성화했습니다. 궁극적으로, 자율주행차는 보행자의 경로에 반응하지 않았고 부주의한 운전자는 충돌을 피할 만큼 충분히 빨리 반응할 수 없었다. 보행자를 올바르게 식별하지 못하는 인식 시스템의 실패와 자전거 및 탐정 물체를 피하기 위한 계획 시스템의 조합은 불확실했고, 자율 실패로 이어졌고, 인간 또는 비상 제동 백업의 부족은 궁극적으로 사망자로 이어졌다. 그래서, 우리는 이러한 일련의 사건에서 자율주행 시스템의 모든 측면, 인식, 계획 및 통제가 모두 실패와 충돌로 이어질 수 있으며, 종종 여러 시스템이나 여러 의사 결정권자의 상호 작용이 예상치 못한 결과를 초래할 수 있다는 것을 알 수 있습니다. 사실, 자율 시스템이 실패할 수 있는 더 많은 방법이 있다.  우리가 안전에 대한 엄격하고 철저한 접근이 필요하다는 것은 분명하며, 산업과 규제 기관 모두 안전 문제를 정면으로 해결하고 있다. 알았어. 이제 안전 평가의 과제에 대한 감각이 있으니, 몇 가지 기본적인 안전 용어를 공식적으로 정의해 봅시다. 우리는 이 용어를 사용하여 생명체에 대한 신체적 해를 지칭할 것이며, 사건이 발생할 확률과 함께 사건이 발생할 확률을 설명하기 위해 위험이라는 용어를 사용할 것입니다. 우리는 이제 안전을 생명체에 해를 끼칠 불합리한 위험을 피하는 과정으로 묘사할 수 있다. 예를 들어, 교통 신호가 빨간색일 때 교차로로 운전하는 것은 차량의 탑승자와 교차로를 통과하는 다른 차량에 해를 끼칠 불합리한 위험을 초래하기 때문에 안전하지 않을 것이다. 마지막으로, 위험은 불합리한 피해 위험이나 안전 위협의 잠재적인 원인이다. 그래서, 내 시스템 소프트웨어에 잠재적으로 사고를 일으킬 수 있는 버그가 있다면, 소프트웨어 버그는 위험할 것이다. 이제, 자율주행 차량 위험의 가장 흔한 원원은 무엇이라고 생각하십니까? 음, 위험은 기계적일 수 있으므로, 조숙한 고장을 일으키는 브레이크 시스템의 잘못된 조립일 수도 있습니다. 그것들은 전기적일 수 있으므로 내부 배선에 결함이 있어 표시등이 손실됩니다. 위험은 또한 자율주행에 사용되는 하드웨어 칩을 계산하는 실패일 수 있다. 앞서 설명한 바와 같이, 그들은 자율 소프트웨어의 오류나 버그 때문일 수 있다. 센서 데이터가 나쁘거나 시끄럽거나 부정확한 인식으로 인해 발생할 수 있습니다. 잘못된 계획이나 의사 결정으로 인해 위험도 발생할 수 있으며, 특정 시나리오의 행동 선택이 올바르게 설계되지 않았기 때문에 실수로 위험한 행동을 선택할 수 있습니다. 또한 인간 운전자에 대한 대체가 운전자에게 책임을 재개할 충분한 경고를 제공하지 않거나 자율주행 자동차가 악의적인 단체에 의해 해킹당할 수도 있다. 이것들은 정기적으로 고려되는 위험의 모든 주요 범주입니다; 기계, 전기, 컴퓨팅 하드웨어, 소프트웨어, 인식, 계획, 운전 작업 대체 및 사이버 보안. 이러한 각 위험은 전반적인 시스템 안전을 평가할 때 다른 접근 방식을 요구한다. 우리는 이후 비디오에서 이러한 카테고리를 다루는 방법에 대해 더 많이 볼 것입니다. 이제 안전과 관련된 기본 용어를 알았으니, 다음 질문에 대해 생각해 봅시다. 자율주행차가 정말 안전한지 어떻게 보장할 수 있을까요? 즉, 복잡한 운전 작업과 발생할 수 있는 많은 위험을 어떻게 취하고 완전한 자율주행 시스템을 위한 안전 평가 프레임워크를 정의합니까? 미국에서는 국립 고속도로 교통 안전국 또는 NHTSA가 자율주행을 위한 안전 평가를 구성하기 위한 12부작 안전 프레임워크를 정의했다. 이 모듈의 다음 비디오에서 볼 수 있듯이, 이 프레임워크는 이미 업계에서 여러 기존 방법과 표준을 결합한 출발점이며 다른 접근 방식이 이미 등장했습니다. 그럼, 먼저 NHTSA의 안전 권장 사항에 대해 논의해 봅시다. 이 프레임워크는 2017년에 따라야 할 필수 프레임워크가 아닌 제안된 프레임워크로 출시되었다. 프레임워크 자체는 자율주행 회사가 집중해야 하거나 오히려 집중하도록 권장되는 12가지 영역이나 요소로 구성되어 있다. 첫째, 안전에 대한 시스템 설계 접근 방식을 채택해야 하며, 이는 전체 프레임워크 문서에 실제로 스며든다. 잘 계획되고 통제된 소프트웨어 개발 프로세스는 필수적이며, 자동차, 항공 우주 및 기타 관련 산업의 기존 SAE 및 ISO 표준의 적용은 적절한 경우 적용되어야 합니다. 나머지 11개 영역의 경우, 우리는 그것들을 느슨하게 두 가지 범주로 구성할 수 있다. 자율 소프트웨어 스택에 특정 구성 요소를 포함하고 고려해야 하는 자율 설계와 자율 기능 테스트 접근 방식과 실패의 부정적인 영향을 줄이고 학습하는 방법을 다루는 테스트 및 충돌 완화. 자율 설계 범주에서, 우리는 이미 익숙한 몇 가지 구성 요소를 볼 수 있다. NHTSA는 설계자가 이것의 결함과 시스템의 한계를 잘 인식하고 테스트 또는 배포 전에 어떤 시나리오가 지원되고 안전한지 평가할 수 있도록 잘 정의된 운영 설계 도메인을 장려합니다. 다음으로, 그것은 인식과 충돌 회피에 중요한 잘 테스트된 물체와 이벤트 탐지 및 대응 시스템을 장려한다. 그런 다음, 그것은 자동차가 운전자에게 경고를 받거나 자동차가 자율적으로 안전에 복귀하는 안정적이고 편리한 대체 메커니즘을 갖도록 장려한다. 운전자가 부주의할 수 있다는 것을 명심하고 이 메커니즘을 개발하는 것이 필수적이다. 그래서, 이런 일이 발생하면 시스템을 최소한의 위험 상태로 만드는 방법에 대한 몇 가지 생각이 들어가야 한다. 운전 시스템은 또한 모든 연방 수준, 주 수준 및 지역 교통법이 ODD 내에서 준수되고 준수되도록 설계되어야 한다. 다음으로, 이 프레임워크는 디자이너들이 사이버 보안 위협과 악성 에이전트로부터 운전 시스템을 보호하는 방법에 대해 생각하도록 장려한다. 마지막으로, 인간 기계 인터페이스 또는 HMI에 약간의 생각이 있어야 한다. 그래서, 자동차는 언제든지 승객이나 운전자에게 기계의 상태를 잘 전달할 수 있어야 한다. 표시할 수 있는 상태 정보의 중요한 예는 모든 센서가 작동하는지 여부, 현재 모션 계획이 무엇인지, 환경의 어떤 물체가 우리의 운전 행동에 영향을 미치는지 등입니다. 우리는 이제 테스트 및 충돌 완화 영역으로 이동합니다. 무엇보다도, NHTSA는 대중에게 서비스가 시작되기 전에 강력하고 광범위한 테스트 프로그램을 권장합니다. 이 테스트는 세 가지 일반적인 기둥에 의존할 수 있다; 시뮬레이션, 근접 트랙 테스트 및 공공 도로 운전. 다음으로, 충돌 사건 중에 발생하는 부상이나 손상의 정도를 완화하는 방법을 신중하게 고려해야 한다. 충돌은 충돌 제한, 에어백 및 충돌 가치 측면에서 충돌 에너지를 최소화하고 승객 안전 기준을 초과할 수 있는 공공 도로 운전 및 자율 시스템의 현실로 남아있다. 다음으로, 충돌 후 행동에 대한 지원이 있어야 한다. 예를 들어, 자동차는 연료 펌프가 연료를 고정하고 멈추는 안전한 상태로 빠르게 반환되어야 하며, 첫 번째 응답자들은 경고했다. 또한, 자동화된 데이터 기록 기능이나 블랙박스 레코더가 있어야 합니다. 이 충돌 데이터를 사용하여 향후 특정 종류의 충돌을 피할 수 있는 시스템을 분석하고 설계하고, 무엇이 잘못되었는지, 그리고 이벤트 중에 누가 잘못되었는지에 대한 질문을 해결하는 것은 매우 도움이 된다. 마지막으로, 잘 정의된 소비자 교육과 훈련이 있어야 한다. 따라서 소비자 운전자와 승객을 테스트하고 훈련하는 동안 대체 운전자가 배치된 자율 시스템의 기능과 한계를 더 잘 이해할 수 있는 과정. 이 마지막 단계는 자동화에 대한 자연스러운 과신뢰를 보장하는 데 필수적이며, 얼리 어답터들이 불필요한 위험을 도입하지 않는다. 이것들은 모든 회사가 작업해야 할 제안된 영역이라는 것을 명심하세요. 아직 필수 요건은 아니다. NHTSA의 주요 목표는 혁신을 과도하게 제한하지 않고 자율주행 자동차를 만드는 회사를 안내하는 것이다. 우리는 기술을 미리 선택하고 있다. 시장 진입이 등장하기 시작하면서, 안전 평가에 대한 더 확실한 요구 사항도 나타날 가능성이 높다. 알았어. 요약해 봅시다. 이 비디오에서, 우리는 자율주행 산업이 본 첫 번째 사고 중 몇 가지에 대해 논의했고, 자율 소프트웨어가 실패할 수 있는 여러 가지 방법을 밝혀냈다. 그런 다음 우리는 공식적으로 피해, 위험, 위험 및 안전을 정의하고 자율주행 차량 위험의 주요 원인을 나열했습니다. 그런 다음 NHTSA 안전 프레임워크를 검토했습니다. 다음 비디오에서, 우리는 자율주행 안전에 대한 업계의 관점과 자율주행 자동차에 대한 몇 가지 안전 권장 사항에 대해 논의할 것입니다. 그때 보자.