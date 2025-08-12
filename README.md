# DLP 3D Stereolithography: Volumetric Printing 기술의 현재와 미래

## 초록

Volumetric 3D printing은 센티미터 스케일의 물체를 수 초 만에 제작할 수 있는 혁신적인 적층 제조 기술로, 지난 7년간 급속한 발전을 이루며 전통적인 층별 제조 방식의 한계를 극복하고 있다. 본 논문은 DLP(Digital Light Processing) 기반 volumetric printing 기술의 핵심 원리와 최신 연구 동향을 분석하고, 특히 holography-based 방법, computational tomography-based 방법, xolography, roll-to-roll based 제조, 그리고 dynamic interface printing 기술의 발전 방향을 제시한다. 이러한 기술들은 광학 및 음향 필드를 이용하여 재료 내부에서 직접적으로 3차원 화학 반응을 유도함으로써, 기존의 층별 적층 방식 대비 획기적인 속도 향상과 설계 자유도를 실현하고 있다. 본 연구는 volumetric printing 기술의 산업화를 위한 재료 화학 및 공정 엔지니어링 분야의 핵심 과제와 연구 방향을 제시함으로써, 이 기술이 초기 단계를 넘어 광범위한 적용 단계로 발전할 수 있는 로드맵을 제공한다.

## 서론

### 층별 제조에서 무층 제조로의 패러다임 전환

3D printing 기술은 지난 40년간 layer-by-layer fabrication 원리에 기반하여 발전해왔다. Fused deposition modeling, selective laser sintering, stereolithographic methods 등의 전통적인 적층 제조 기술들은 단일 voxel, 선, 또는 면 단위로 재료를 순차적으로 적층하여 2차원 패턴을 형성하고, 이를 반복적으로 쌓아 올려 3차원 구조체를 제작한다. 하지만 이러한 방식은 근본적으로 느린 생산 속도(수 입방센티미터 부품 제작에 수 시간 소요), 제한적인 재료 선택권, 그리고 복잡한 형상 제작을 위한 지지 구조물 의존성 등의 한계를 가지고 있다.

Volumetric printing, 또는 volumetric additive manufacturing(VAM)은 이러한 전통적 제조 방식의 한계를 극복하는 새로운 제조 패러다임이다. 이 기술은 층별 제조 없이 전체 부품을 한 번에 제작할 수 있으며, 가장 빠른 기술의 경우 수십 마이크로미터 해상도로 입방센티미터 부품을 10초 이내에 제작할 수 있다. Volumetric printing의 핵심은 field-based manufacturing 개념으로, 센티미터 스케일의 거리에서도 작동할 수 있는 복잡하고 불균질한 물리적 필드(주로 광학 및 음향 필드)를 재료 내부로 방사하여 공간적으로 해석된 에너지 도즈 분포를 생성하고, 이를 통해 제어된 화학 반응을 유도하여 원하는 객체를 형성한다.

### Field-based Volumetric Manufacturing 기술의 분류

Volumetric printing 기술은 사용하는 물리적 필드의 종류에 따라 크게 광학 기반 방법과 음향 기반 방법으로 분류할 수 있다. 광학 기반 방법들은 photochemical reaction에 대한 풍부한 문헌과 stereolithographic printing에서 축적된 light-responsive materials에 대한 경험을 바탕으로 먼저 발전했다. 파장, 강도, 공간 분포 등의 광학 매개변수를 제어함으로써 재료 내부 깊숙한 곳에서도 시공간적으로 해석된 photochemical reaction을 유도할 수 있다.

## Holography-based Volumetric Printing 기술

### 홀로그래피 원리의 적용

Holography-based volumetric printing은 홀로그래피의 기본 원리를 3D 제조에 적용한 혁신적인 기술이다. 이 방법은 복잡한 3차원 광학 패턴을 생성하기 위해 홀로그래픽 투사를 활용하며, 특히 음향 기반 시스템에서 주목할 만한 발전을 보이고 있다. Holographic direct sound printing(HDSP)은 3D 프린팅된 acoustic holographic phase plate를 초음파 변환기 위에 배치하여, 초음파 파면을 임의의 초점으로 성형하는 데 필요한 위상 정보를 인코딩한다.

### 음향 홀로그래피의 구현

음향 홀로그래피 시스템에서는 holographic phase plate가 목표 기하학적 형상의 단면에 해당하는 임의의 초점을 생성하도록 초음파 파면을 성형한다. 이 접근 방식의 주요 장점은 여러 영역을 동시에 중합할 수 있어 single shot으로 원하는 객체를 형성할 수 있다는 점이다. 하지만 3D 프린팅된 phase plate는 변조가 불가능하므로, 초점 평면에서의 강도 패턴이 고정되어 있어 더 복잡한 3D 구조체는 이 평면의 translation을 통해서만 제작할 수 있다는 한계가 있다.

### 광학 홀로그래피의 발전 방향

광학 기반 홀로그래피에서는 phase-modulation hardware가 중요한 발전을 보이고 있다. Phase-based spatial light modulator는 역사적으로 낮은 frame rate(<10 Hz)로 제한되어 왔지만, 최근 하드웨어 개선으로 two-photon printing에서 널리 채택되고 있으며, VAM에서의 적용은 아직 초기 단계에 있다. 이러한 개선은 lens를 spatial light modulator의 phase mask로 대체하여 광학 시스템을 단순화하고, printing vial이나 resin 내의 aberration을 wavefront control을 통해 보정할 수 있게 한다.

HoloTile 기술은 phase-only spatial light modulator를 sub-hologram으로 분할하여 reconstruction plane에서 복잡한 강도 분포를 생성하는 computer-generated holographic 방법이다. 이 방법은 tomographic VAM과 light-sheet 접근법 모두에서 speckle-reduced fabrication, 높은 photon efficiency, 향상된 공간 해상도, 그리고 개선된 depth of focus 등의 여러 장점을 제공한다.

### 프로그래밍 가능한 음향 홀로그래피

음향 기반 printing에서는 acoustic wavefront를 동적으로 변조하는 새로운 방법을 찾기 위한 노력이 계속되고 있다. 이는 single-voxel crosslinking이나 passive holographic projection에서 대규모의 임의 기하학적 형상을 빠르게 제작할 수 있는 영역으로의 전환을 목표로 한다. Programmable acoustic holography는 가장 일반적으로 phased array를 사용하는 활발한 연구 분야이지만, 해상도, 전력, 주파수 제한의 문제가 있다. Programmable acoustic metasurface는 실시간 위상 변조를 위해 능동적으로 조정될 수 있어 잠재적인 해결책으로 여겨진다.

## Computational Tomography-based Volumetric Printing

### Tomographic 재구성 원리

Computational tomography-based volumetric printing은 3D 의료 영상의 computed tomography에서 영감을 얻은 기술로, volumetric printing 분야에서 가장 획기적인 발전을 이룬 방법이다. Multibeam superposition과 달리, tomographic volumetric printing은 회전하는 원통형 photosensitive resin 부피에 여러 각도에서 사전 계산된 일련의 2D 광패턴을 투사하여 목표 3D 광 도즈를 재구성한다.

투사는 tomographic algorithm(Radon transform과 filtered back projection)에 따라 계산되며, LED나 laser source로 조명되는 digital micromirror device와 같은 amplitude-type spatial light modulator를 통해 전달된 후 print volume의 중심으로 영상화된다. 모든 각도에서 이러한 투사들의 누적합은 목표 기하학적 형상의 경계 내에서 최대화되는 복잡한 광 도즈의 형성을 초래하여, 원하는 영역 내에서 photopolymerization을 유도하는 반면, 반응하지 않은 재료는 공정 끝에서 씻어낸다.

### 재구성 알고리즘의 발전

Tomographic VAM에서 해상도와 정확도를 향상시키기 위해서는 reactive resin에 전달되는 물리적 필드(광 도즈나 acoustic energy의 공간적 제어를 통한)의 패터닝을 정밀하게 변조하는 재구성 알고리즘이 핵심이다. 이 문제의 학제간 특성을 고려할 때, 재료 과학자와 컴퓨터 과학자 간의 협력이 필요하다.

표준 filtered tomographic 접근법을 넘어서는 다양한 최적화 접근법들이 더 충실한 재구성을 달성하기 위해 사용되고 있다. Object-space optimization of tomographic reconstruction, gradient descent optimization, wave optical optimization, maximum likelihood-expectation maximization, 3D ray tracing 등의 기법들이 소프트웨어 수준에서 적용되고 있다.

### 물리학 기반 모델링의 통합

최근 연구들은 photopolymerization 공정의 화학적 동역학을 다양한 세부 수준으로 모델링하고 결합하려는 시도를 하고 있으며, 이는 tomographic과 light sheet-based volumetric printing 접근법 모두에 영향을 미치고 있다. 이러한 연구들은 radical과 oxygen 확산 속도와 같은 매개변수를 조사하여 정확도와 printing 균질성을 향상시키며, global parameter조차도 계산 효율성을 희생하더라도 print fidelity를 크게 개선할 수 있음을 보여주고 있다.

Resin 내의 scattering 완화를 위한 알고리즘적 접근법도 탐구되고 있다. Imaging과 Fourier domain에서의 투사에 대한 선택적 수정의 조합을 사용하거나, 물리 기반 inverse rendering 문제를 활용하거나, 임의의 scattering 또는 absorptive volume 내에서 light ray의 differentiable simulation을 사용하는 방법들이 개발되고 있다. 이러한 발전은 특히 불투명한 복합 재료와 cell-laden 재료와 호환되는 light-based VAM의 범위를 확장하는 데 중요하다.

### 실시간 모니터링과 피드백 제어

Tomographic VAM에서 주요 도전 과제 중 하나는 실시간 모니터링과 metrology이다. 이는 print 진행 상황을 평가하고 잠재적으로 print 품질을 최적화하기 위한 동적 조정을 가능하게 하는 데 중요하다. 대부분의 경우, volume의 단순한 영상화는 중합된 영역과 중합되지 않은 영역 사이의 충분한 대비를 제공하지 못한다. 이 문제는 polymer 함량이 낮은 resin이나 scattering agent를 포함하는 resin을 다룰 때 더욱 복잡해지며, 이는 bioprinting 애플리케이션에서 흔히 발생하는 상황이다.

저대비 시나리오에서 이러한 문제를 해결하기 위해 shadowgraph imaging과 Schlieren imaging이 tomographic VAM과 함께 사용되고 있다. 이러한 기법들은 중합 과정의 결과로 발생하는 굴절률의 미세한 변화를 시각화할 수 있다. Schlieren imaging은 또한 tomographic imaging modality에서 활용되어 printing 과정의 3D 재구성을 생성하고 내부 굴절률의 정량적 측정을 수행할 수 있다.

## Xolography 기술

### Dual-colour Photopolymerization의 원리

Xolography는 dual-colour photopolymerization printing의 대표적인 예로, 두 개의 광학 경로를 활용하는 혁신적인 기술이다. UV light sheet가 volume을 가로질러 스위프하여 photoswitchable photoinitiator를 일시적으로 활성화하고, 동시에 직교하는 패턴된 가시광 투사가 두 빔의 겹치는 부분에서 국소적으로 중합과 가교를 유도한다. Light sheet가 volume을 스캔하면서 투사는 목표 기하학적 형상의 해당 단면으로 지속적으로 업데이트된다.

### Fast Thermal Reversible Photoswitchable Initiator

이 접근법의 주요 장점은 fast thermal reversible photoswitchable initiator의 사용이다. 이러한 initiator는 thermal relaxation을 통해 비반응성 상태로 되돌아간 후 out-of-plane crosslinking을 방지한다. 이러한 중합 반응의 구속은 tomographic 접근법에 비해 더 높은 도즈 대비를 가능하게 한다. 따라서 xolography는 수 마이크로미터까지의 feature size로 센티미터 스케일의 객체를 수 분 내에 생산할 수 있다.

Xolography와 유사한 접근법인 light sheet 3D microprinting은 microscale에서 작동하며 two-step photoinitiator를 활용한다. Light sheet 생성과 수직 투사 경로 모두에 microscope objective를 사용함으로써 printable volume을 희생하여 더 높은 해상도 특징(~1μm)을 얻을 수 있으며, 이는 이 방법을 복잡한 정밀도가 요구되는 애플리케이션에 특히 적합하게 만든다.

### 광학적 구속과 해상도 향상

보다 일반적인 photoinitiator를 사용하려는 노력은 specialized photochemistry보다는 빛의 정밀한 공간적 제어에 의존하는 다른 기술들로 이어졌다. 동일한 파장의 두 직교하는 광원의 교차점을 활용하여 photo-crosslinking 반응을 구속함으로써 고해상도 volumetric printing이 달성되었다. 여기서 2D galvanometer가 light sheet의 평면을 따라 빔을 직교로 스캔하며, 노출 조건은 in-plane 영역을 제외한 모든 곳에서 도즈가 crosslinking threshold 이하로 유지되도록 설정된다.

이 접근법은 out-of-plane 노출을 최소화하려고 시도하지만 완전히 제거하지는 못한다. 따라서 high-contrast 도즈 목표는 feature height가 증가함에 따라 비례적으로 더 어려워지므로, 이 방법은 더 얇은 평면 구조체에 더 적합하다.

### Light Sheet 기반 프린팅의 도전과제

Light sheet에 기반한 printing 접근법의 주요 도전과제는 더 빠른 relaxing initiator를 도입하여 printing 속도를 향상시키고, 사용자 기반을 넓히기 위해 더 일반적인 initiator를 사용하는 것이다. 또한, 연속 흐름을 light sheet 설정과 통합하는 것은 생산 처리량을 향상시키고 중단 없는 다중 재료 제조 공정을 가능하게 하는 방법을 제시한다.

## Roll-to-roll Based Volumetric Printing

### 연속 생산을 위한 혁신적 접근

Roll-to-roll based volumetric printing은 volumetric printing 기술의 산업화와 대량 생산을 위한 혁신적인 접근법이다. 이 기술은 전통적인 layer-based 3D printing에서의 continuous liquid interface production과 tomographic VAM에서 모두 활용되고 있다. Roll-to-roll tomographic printing에서는 photoresin이 spool-driven tape에 증착되고, 독특한 평면 기하학과 연속적인 기판 움직임을 고려한 tomogram이 계산된다.

### 평면 기하학적 형상의 대량 생산

현재는 thermally gelling photoresist나 hydrogel과 같은 기계적으로 순응성 있는 재료로 제한되어 있지만, 이 접근법은 이론적으로 무제한의 길이를 가진 평면 기하학적 형상의 printing을 가능하게 한다. 이는 특히 유연한 전자 장치, 생체 의학 패치, 또는 대면적 광학 구성 요소와 같은 애플리케이션에서 중요한 장점을 제공한다.

### 연속 흐름 시스템의 구현

Light sheet 설정을 vat 내의 연속 재료 흐름과 통합하는 것은 생산 처리량을 향상시키고 중단 없는 multimaterial 제조 공정을 가능하게 하는 또 다른 방법이다. Xolography를 사용한 최근의 실증에서, light sheet가 정적인 재료 volume을 횡단하는 기존 방법과는 달리, 이 기법은 정지된 light sheet를 통해 photosensitive resin의 정밀하게 제어된 laminar flow를 사용한다.

신중하게 설계된 flow cell의 사용을 통해, 경계에서 바람직하지 않은 중합을 완화하면서 printing zone에서 상대적으로 균일한 속도 분포를 달성하는 것이 가능했다. 이 구성은 최대 1.75 mm³/s의 volumetric fabrication rate와 10μm에 근접하는 feature resolution으로 여러 객체의 동시 및 연속 생산을 가능하게 했으며, 이는 복잡한 미세 구조의 대량 생산이 요구되는 애플리케이션에 특히 적합하다.

### 대규모 생산을 위한 하드웨어 혁신

VAM을 산업 규모 생산으로 발전시키는 것은 증가된 처리량, 감소된 인간 개입, 향상된 신뢰성을 갖춘 시스템이 필요하므로 하드웨어 설계와 최적화 측면에서 상당한 도전을 제시한다. Light-based printing에서 주요 장애물은 일반적으로 resin 내의 지수적 light absorption으로 인해 수 센티미터로 제한되는 printable object size의 한계를 극복하는 것이다.

최근의 하드웨어 혁신은 전통적인 원통형 vial을 넘어서는 tomographic VAM으로 접근 가능한 기하학적 형상들을 재구상하고 있다. 한 구성은 높은 원통형 volume의 길이를 따라 나선형 경로를 따라 투사를 전달한다. 이러한 설정에서 volume은 회전하는 반면 방사상으로 offset된 투사들은 회전축을 따라 선형으로 translation되어, vat의 길이에 의해서만 제한되는 높은 aspect ratio 구조체의 제조를 가능하게 한다. 그러나 light attenuation은 여전히 이러한 print의 최대 단면적을 제한하는 역할을 한다.

## Dynamic Interface Printing 기술

### 적응형 제조 환경의 구현

Dynamic interface printing은 volumetric printing 기술의 가장 진보된 형태 중 하나로, 실시간으로 변화하는 제조 환경에 적응할 수 있는 능력을 제공한다. 이 기술의 핵심은 GRACE(Generative, Adaptive, Context-aware 3D printing) workflow로, volumetric imaging과 computer vision의 조합이 printing 환경의 내용물을 감지하고, parametric modeling과 VAM이 vat에 로드된 객체의 기하학적, 화학적, 또는 생물학적 특성에 정확히 정렬되거나 적응하도록 정밀하게 생성된 구조체의 생산을 가능하게 한다.

### 실시간 모니터링과 피드백 시스템

Dynamic interface printing의 핵심 기술 중 하나는 실시간 모니터링과 metrology이다. 이는 print 진행 상황을 평가하고 잠재적으로 print 품질을 최적화하기 위한 동적 조정을 가능하게 하는 데 중요하다. 저대비 시나리오에서 이러한 문제를 해결하기 위해 다양한 imaging 기술들이 개발되고 있다.

Optical scattering tomography는 3D 시각화를 위해 사용되며, 굴절률 변화를 측정하는 대신 top-down 조명 설정에 의해 제공되는 side-scattered light를 영상화하여 대비를 제공한다. 이 접근법은 resin의 scattering 특성이 photopolymerization에 반응하여 변할 때 특히 효과적이다. 주목할 만한 점은 이 방법이 재구성 데이터로부터의 피드백에 기반하여 필요한 광 도즈를 달성했을 때 printing 과정을 자동으로 종료하는 피드백 제어 루프에 통합되었다는 것이다.

### 인공지능과 기계학습의 통합

Computer vision과 machine-learning tool들은 printing error의 조기 발견과 on-the-fly 품질 제어, 그리고 printing quality를 향상시키기 위한 printing parameter의 closed-loop correction에 대한 명확한 잠재력을 가지고 있다. Neural network model과 같은 훈련된 artificial intelligence tool들은 잠재적으로 imaging data의 처리, context-driven architecture의 생성, 그리고 corrective measure의 계산을 가속화할 수 있다.

이러한 모델들은 print outcome의 광범위한 data set에서 훈련될 수 있으며, 예를 들어 deviation을 빠르게 인식하고 correction을 수행하며 잠재적으로 주어진 재료에 대한 공정을 시뮬레이션하고 실제 volumetric printing 세션에서 corrective action을 실행할 수 있게 한다. Field-programmable gate array도 특정 계산 작업을 높은 효율로 수행하는 데 사용될 수 있어, imaging data의 더 빠른 처리와 light-dose correction의 계산을 가능하게 한다.

### Context-aware Manufacturing의 발전

Dynamic interface printing의 주요 능력 중 하나는 build volume 내의 기존 feature에 구조체를 비침습적으로 overprinting하는 것이다. 이러한 잠재력을 바탕으로, context-aware 3D printing은 printing environment의 내용물을 감지하고, 복합 resin(예: living cell, particle, fiber 또는 기타 inclusion을 포함하는)을 printing하기 위한 응용과 함께 구조적으로 복잡한 객체를 생산할 수 있는 additive manufacturing의 능력을 확장하면서, 고도로 맞춤화된 multimaterial part의 생산에 중요한 역할을 할 수 있다.

이러한 context-driven 제조의 도입은 bioengineering, soft robotics, high-performance metamaterial 분야에서 응용될 수 있으며, additive manufacturing이 구조적으로 복잡한 객체를 생산할 수 있는 능력을 확장한다. 대규모 volumetric imaging data set의 검색, 재구성, 업데이트와 관련된 도전과제와, 빠른 printing 과정과 보조를 맞추면서 새로운 최적화된 투사를 생성하는 것을 다루는 것은 고급 계산 프레임워크가 필요함을 의미한다.

## 재료 설계와 미래 전망

### 차세대 Photoinitiator 시스템

미래의 volumetric printing 재료 설계에서 가장 중요한 발전 방향 중 하나는 새로운 photoinitiator 기술의 개발이다. 기존의 radical-based polymerization 접근법을 위해서는 새로운 photoswitchable photoinitiator, two-step photoinitiator, 그리고 더 일반적으로는 nonlinear photoinitiator들이 광 흡수의 지수적 감소를 보상하여 이러한 기술의 확장을 가능하게 하는 데 사용될 수 있다.

또 다른 중요한 발전은 높은 반응성을 유지하면서 흡수와 scattering을 줄이기 위한 initiator의 excitation wavelength의 red-shifting과 대안적인 photochemistry의 가능성을 여는 것이다. 이는 dual-colour photopolymerization printing chemistry에서 특히 중요하며, tomographic printing의 경우 가시광 영역에서 흡수를 갖는 initiator 조합을 사용함으로써 이러한 redshift가 부분적으로 실현되었지만, 효율적인 적색 및 적외선 initiator가 여전히 요구되고 있다.

### 다중 화학 반응 시스템

Light-based volumetric printing을 위한 새로운 재료 개발에서 흥미로운 관점 중 하나는 radical과 직교하는 대안적인 photochemistry의 사용이다. 이러한 방식으로 기존의 radical-based reaction을 다른 light-triggered polymerization reaction과 결합하여 sequential printing 단계나 multitechnology 접근법의 필요 없이 동일한 printing 과정 내에서 서로 다른 재료와 성분들을 매끄럽게 도입할 수 있다.

예를 들어, 최근 연구는 서로 다른 파장에 반응하는 photoinitiator와 함께 acrylate와 epoxide로 구성된 resin을 사용하여 이러한 개념을 실증했으며, 각각 free radical과 cationic polymerization을 통해 중합된다. 두 반응은 단순히 printer의 광원을 변조함으로써 서로 독립적으로 trigger될 수 있다.

### 미래 기술의 융합

미래의 volumetric printing 기술은 machine learning과 artificial intelligence, 고급 imaging, multimodal printing 등의 emerging technology의 융합을 요구한다. 이는 사용자로부터 최소한의 또는 전혀 교정적 개입 없이 원하는 print를 자동으로 수행할 수 있고, printable material의 유형에 제한이 없는 smart printer의 개발을 가능하게 할 것이다.

Field-based printing 기법이 기존 구조체와 inclusion에 'overprint'할 수 있는 능력은 volumetric printing을 multitechnology printing device에서 이상적인 tool로 만든다. 이 개념은 기존의 layerwise 기법으로 생산되어야 하는 요소들이 VAM-produced print로 빠르게 수정, 캡슐화 또는 연결되어 복잡한 복합 재료를 생성할 수 있는 미래로의 길을 열어준다.

## 결론

DLP 3D stereolithography와 volumetric printing 기술은 지난 몇 년간 급속한 발전을 이루며 다양한 연구 분야에 영향을 미치고 있다. Holography-based, computational tomography-based, xolography, roll-to-roll based, 그리고 dynamic interface printing 등의 기술들은 각각 고유한 장점과 응용 영역을 가지고 있으며, 이들의 융합을 통해 더욱 혁신적인 제조 솔루션이 창출될 것으로 예상된다.

미래의 발전 방향은 재료 설계의 혁신, 특히 다중 화학 반응 시스템과 orthogonal reaction의 구현, 그리고 radical-free 및 장파장 반응성 화학의 개발에 초점을 맞추어야 한다. 또한 magnetic field, microwave radiation, 심지어 X-ray field와 같이 대부분의 매체를 거의 방해받지 않고 통과할 수 있는 다른 유형의 field로 field-based printing 개념을 확장하는 것이 volumetric printing의 추가적인 확장을 가능하게 할 것이다.

이러한 발전들은 volumetric printing을 초기 단계에서 성숙한 기술로 끌어올려, 산업, 연구 센터, 의료 시설에서의 광범위한 채택을 위한 길을 열고, 궁극적으로 모든 디지털 구조 계획의 거의 즉시 제조를 가능하게 할 것이다. Volumetric printing 기술의 지속적인 발전은 제조업의 패러다임을 완전히 바꾸어 놓을 혁신적 잠재력을 가지고 있으며, 이는 21세기 제조업의 핵심 기술로 자리잡을 것으로 전망된다.
