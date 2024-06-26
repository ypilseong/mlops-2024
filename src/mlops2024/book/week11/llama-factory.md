# LLaMA Factory를 활용한 LLM 파인튜닝

대규모 언어 모델(Large Language Model, LLM)은 인공지능 분야에서 가장 혁신적인 기술 중 하나로 주목받고 있습니다. LLM은 방대한 양의 텍스트 데이터로 학습한 거대한 신경망 모델로, 자연어 이해와 생성 능력이 뛰어나 챗봇, 기계 번역, 문서 요약 등 다양한 자연어 처리 태스크에서 인상적인 성능을 보여주고 있습니다.

그러나 LLM을 실제 서비스에 적용하기 위해서는 모델을 특정 도메인이나 태스크에 맞게 미세 조정(fine-tuning)해야 하는 어려움이 있습니다. 파인튜닝은 사전 학습된 LLM을 기반으로 추가 학습을 진행하는 과정으로, 모델이 특정 분야의 지식과 어휘를 학습하고 원하는 방식으로 동작하도록 만드는 데 필수적입니다.

LLaMA Factory는 다양한 모델과 최신 파인튜닝 기법을 지원하면서도 사용이 간편하여, 전문가가 아니더라도 손쉽게 LLM을 파인튜닝하고 배포할 수 있게 해줍니다. 이는 LLM 기술의 대중화와 실용화를 앞당기는 데 크게 기여할 것으로 기대됩니다.

이 글에서는 LLM 파인튜닝의 개념과 중요성, 최신 파인튜닝 전략, LLaMA Factory의 주요 기능과 사용 방법 등을 자세히 살펴보겠습니다.

## 1. LLM 파인튜닝 소개

대규모 언어 모델(Large Language Models, LLMs)은 방대한 양의 텍스트 데이터로 사전 학습된 딥러닝 모델입니다. 이러한 모델은 GPT-3, BERT, RoBERTa 등과 같은 트랜스포머 아키텍처를 기반으로 하며, 수억 또는 수십억 개의 매개변수를 가지고 있습니다. LLM은 언어의 패턴과 구조를 학습하여 텍스트 생성, 질의 응답, 요약, 번역 등 다양한 자연어 처리(NLP) 작업에서 인상적인 성능을 보여줍니다.

그러나 LLM은 일반적인 도메인에서 학습되었기 때문에, 특정 작업이나 도메인에 직접 적용하기에는 한계가 있습니다. 이러한 한계를 극복하고 LLM을 특정 작업에 최적화하기 위해 파인튜닝(Fine-tuning) 기법이 사용됩니다.

LLM 파인튜닝은 사전 학습된 LLM을 특정 작업이나 도메인에 맞게 추가로 학습시키는 프로세스입니다. 파인튜닝은 일반적으로 사전 학습 단계에서 사용된 것보다 훨씬 적은 양의 labeled 데이터를 사용하여 수행됩니다. 파인튜닝 동안 모델의 가중치는 특정 작업에 최적화되도록 업데이트됩니다. 이를 통해 LLM은 해당 작업에 대한 성능을 크게 향상시킬 수 있습니다.

LLM 파인튜닝의 주요 단계는 다음과 같습니다:

1. 베이스 모델 선택: 일반 텍스트 데이터로 학습된 사전 학습 언어 모델을 선택합니다. 이 모델은 기본적인 언어 구조와 의미를 이해할 수 있어야 합니다.

2. 학습 데이터셋 준비: 타겟 작업과 관련된 labeled 데이터셋을 선택하거나 수집합니다. 이 데이터셋의 크기는 일반적으로 사전 학습에 사용된 데이터셋보다 훨씬 작습니다.

3. 파인튜닝 수행: 준비된 데이터셋으로 모델을 학습시킵니다. 이때 학습률은 일반적으로 사전 학습 단계보다 낮게 설정하여, 기존의 언어 지식을 유지하면서 특정 작업에 대한 지식을 습득할 수 있도록 합니다.

4. 평가: 파인튜닝된 모델의 성능을 평가 데이터셋으로 측정합니다. 이를 위해서는 별도의 검증 데이터셋이 필요합니다.

5. 배포: 평가 결과가 만족스러울 경우, 파인튜닝된 모델을 실제 애플리케이션이나 서비스에 배포합니다.

LLM 파인튜닝의 가장 큰 장점은 적은 양의 데이터와 계산 자원으로도 뛰어난 성능을 얻을 수 있다는 점입니다. 사전 학습된 LLM은 이미 방대한 양의 언어 지식을 보유하고 있기 때문에, 파인튜닝을 통해 적은 비용으로 특정 작업에 적응할 수 있습니다. 반면에 처음부터 모델을 학습시키는 것은 많은 데이터와 계산 자원을 필요로 하며, 학습 시간도 오래 걸립니다.

또한 파인튜닝은 다양한 작업과 도메인에 같은 LLM을 적용할 수 있는 유연성을 제공합니다. 하나의 사전 학습된 LLM을 다양한 작업에 파인튜닝함으로써, 각 작업에 특화된 여러 개의 모델을 만들 수 있습니다.

LLM 파인튜닝은 ChatGPT, Bard, Anthropic Claude 등 최근 각광받는 대화형 AI 시스템의 핵심 기술로 자리잡았습니다. 사전 학습된 LLM을 대화 데이터로 파인튜닝하여 사용자와 자연스럽게 상호작용할 수 있는 대화 모델을 만들 수 있기 때문입니다. 또한 특정 도메인이나 작업에 특화된 chatbot을 개발하는 데에도 LLM 파인튜닝이 활발히 사용되고 있습니다.

LLM 파인튜닝은 NLP 분야에서 중요한 역할을 하고 있으며, 다양한 애플리케이션과 서비스에 적용되고 있습니다. 특히 대화형 AI, 문서 요약, 감성 분석, 질의 응답 시스템 등의 분야에서 LLM 파인튜닝을 통해 눈부신 성과를 거두고 있습니다. 앞으로도 LLM 파인튜닝 기술은 더욱 발전하여 보다 정교하고 효율적인 방식으로 LLM을 활용할 수 있을 것으로 기대됩니다.

## 2. 최신 파인튜닝 전략

LLM 파인튜닝 기술이 발전함에 따라 다양한 파인튜닝 전략들이 등장했습니다. 최신 파인튜닝 전략들은 기존 방법의 한계를 극복하고 더욱 효율적이고 효과적으로 LLM을 파인튜닝할 수 있도록 고안되었습니다. 여기서는 LoRA, QLoRA, PEFT 등 세 가지 대표적인 최신 파인튜닝 전략을 소개하겠습니다.

### 2.1. LoRA (Low-Rank Adaptation)

LoRA는 매개변수 효율적인 파인튜닝 기법 중 하나로, 낮은 계산 및 메모리 비용으로 수십억 개의 매개변수를 가진 LLM을 특정 작업에 적응시킬 수 있습니다. LoRA는 기존 모델의 가중치 행렬에 낮은 rank의 adaptation 행렬을 추가하는 방식으로 작동합니다. 이 adaptation 행렬만 학습함으로써 파인튜닝에 필요한 학습 가능한 매개변수의 수를 크게 줄일 수 있습니다.

LoRA의 핵심 아이디어는 다음과 같습니다. 기존 모델의 가중치 행렬 W에 낮은 rank의 매개변수 행렬 A와 B를 추가하여 W' = W + AB로 표현합니다. 파인튜닝 동안에는 A와 B만 학습하고 W는 고정합니다. 이렇게 하면 기존 모델의 지식을 최대한 보존하면서도 특정 작업에 맞게 모델을 조정할 수 있습니다.

LoRA는 기존 파인튜닝 방법에 비해 다음과 같은 장점을 가지고 있습니다:

- 매개변수 효율성: LoRA는 적은 수의 학습 가능한 매개변수만을 사용하므로 메모리와 저장 공간을 절약할 수 있습니다.
- 계산 효율성: LoRA는 기존 모델의 가중치를 고정하고 추가된 adaptation 행렬만 학습하므로 계산 비용이 줄어듭니다.
- 성능 향상: LoRA는 작은 adaptation 행렬로도 기존 모델의 성능을 크게 향상시킬 수 있습니다.

### 2.2. QLoRA (Quantized LoRA)

QLoRA는 LoRA를 양자화(Quantization)하여 메모리 사용량을 더욱 줄인 파인튜닝 기법입니다. 양자화는 모델 가중치를 낮은 비트 폭으로 표현하는 방법으로, 모델 크기를 줄이고 추론 속도를 높일 수 있습니다. QLoRA는 사전 학습된 언어 모델을 4비트로 양자화하고, 낮은 rank의 adaptation 행렬을 학습합니다.

QLoRA의 학습 과정은 다음과 같습니다:

1. 사전 학습된 언어 모델을 4비트로 양자화합니다.
2. LoRA의 adaptation 행렬을 모델에 추가합니다.
3. 역전파 시 기울기를 양자화된 모델에서 계산하여 adaptation 행렬을 업데이트합니다.

QLoRA는 LoRA와 비교하여 다음과 같은 이점을 제공합니다:

- 메모리 효율성: 4비트 양자화를 통해 모델의 메모리 사용량을 대폭 절감할 수 있습니다.
- 성능 유지: QLoRA는 4비트 양자화에도 불구하고 LoRA와 유사한 성능을 보여줍니다.

### 2.3. PEFT (Parameter-Efficient Fine-Tuning)

PEFT는 사전 학습된 언어 모델의 일부 매개변수만 조정하여 효율적으로 파인튜닝하는 방법론입니다. PEFT는 Adapter, Prefix Tuning, LoRA 등 다양한 매개변수 효율적 파인튜닝 기법을 아우르는 개념으로, 과제에 따라 적절한 방법을 선택할 수 있습니다.

PEFT의 주요 목표는 다음과 같습니다:

- 계산 및 저장 비용 절감: 전체 모델을 파인튜닝하는 대신 일부 매개변수만 조정하여 계산량과 모델 크기를 줄입니다.
- 성능 유지: 적은 수의 매개변수만으로도 전체 파인튜닝에 준하는 성능을 달성합니다.
- 과적합 방지: 일부 매개변수만 조정하므로 작은 데이터셋에서도 과적합을 방지할 수 있습니다.

PEFT는 다양한 자연어 처리 작업에서 우수한 성능을 보여주었으며, 특히 제한된 자원 환경에서 유용합니다. 또한 PEFT를 통해 하나의 사전 학습된 모델을 다양한 작업에 적응시킬 수 있어 모델의 재사용성을 높일 수 있습니다.

이러한 최신 파인튜닝 전략들은 기존 방법의 한계를 극복하고 보다 효율적이고 효과적으로 LLM을 파인튜닝할 수 있게 해줍니다. LoRA와 QLoRA는 적은 수의 학습 가능한 매개변수로 모델을 조정하여 계산량과 메모리 사용량을 절감하는 반면, PEFT는 다양한 매개변수 효율적 파인튜닝 기법을 포괄하여 과제에 맞는 최적의 방법을 선택할 수 있도록 합니다.

현재 LLM 파인튜닝의 best practice로는 LoRA나 QLoRA를 사용하는 것이 권장됩니다. 이 방법들은 계산 효율성과 메모리 효율성 측면에서 뛰어날 뿐만 아니라 기존 모델의 성능을 유지하면서도 특정 작업에 빠르게 적응할 수 있기 때문입니다. 다만 과제의 특성에 따라 PEFT의 다른 방법들이 더 적합할 수 있으므로, 다양한 방법을 실험해보고 최선의 결과를 내는 방법을 선택하는 것이 좋습니다.

## 3. LLaMA Factory 소개

LLaMA Factory는 대규모 언어 모델(LLMs)을 위한 강력하고 사용자 친화적인 파인튜닝 도구입니다. 이 도구는 LLM 파인튜닝 과정을 단순화하고 파인튜닝 중에 시각화 기능을 제공하여 사용자가 모델의 학습 진행 상황을 쉽게 모니터링할 수 있도록 합니다.

### 3.1. LLaMA Factory의 주요 기능

- 다양한 모델 지원: LLaMA Factory는 ChatGLM, BaiChuan, Qwen, LLaMA 등 여러 유명 중국어 오픈 소스 LLM을 포함한 다양한 모델을 지원합니다. 이를 통해 사용자는 자신의 니즈에 맞는 모델을 선택하고 파인튜닝할 수 있습니다.
- 최신 파인튜닝 방법 통합: LLaMA Factory는 LoRA, QLoRA 등 최신 파인튜닝 방법을 내장하고 있습니다. 이를 통해 사용자는 적은 계산 자원으로도 효과적으로 LLM을 파인튜닝할 수 있습니다.

- 일반적인 파인튜닝 데이터셋 제공: LLaMA Factory는 파인튜닝에 일반적으로 사용되는 다양한 데이터셋을 제공합니다. 이는 사용자가 직접 데이터를 수집하고 전처리하는 번거로움을 줄여줍니다.

- 직관적인 WebUI 인터페이스: LLaMA Factory는 파인튜닝 과정을 안내하는 직관적인 웹 기반 사용자 인터페이스를 제공합니다. 이를 통해 프로그래밍에 익숙하지 않은 사용자도 쉽게 LLM을 파인튜닝할 수 있습니다.

### 3.2. 지원되는 학습 모드

LLaMA Factory는 다음과 같은 세 가지 학습 모드를 지원합니다:

1. Pre-Training: 대규모 텍스트 데이터로 LLM을 처음부터 학습시키는 방법입니다. 이를 통해 LLM은 언어의 일반적인 패턴과 지식을 습득할 수 있습니다.
2. Supervised Fine-Tuning: labeled 데이터셋을 사용하여 사전 학습된 LLM을 특정 작업에 맞게 파인튜닝하는 방법입니다. 이는 LLM의 성능을 특정 도메인이나 작업에 최적화할 수 있게 해줍니다.
3. Reward Modeling: 보상 함수를 학습하여 LLM이 특정 작업에서 좋은 성능을 내도록 유도하는 방법입니다. 이는 강화 학습의 일종으로, 모델이 좋은 행동을 하면 높은 보상을 주는 방식으로 학습이 이루어집니다.

### 3.3. 지원되는 파인튜닝 전략

LLaMA Factory는 다음과 같은 두 가지 파인튜닝 전략을 지원합니다:

1. LoRA: LoRA는 기존 모델의 가중치 행렬에 낮은 rank의 adaptation 행렬을 추가하여 파인튜닝하는 방법입니다. 이를 통해 적은 수의 학습 가능한 매개변수로도 효과적인 파인튜닝이 가능합니다.
2. QLoRA: QLoRA는 LoRA를 4비트로 양자화한 방법으로, 메모리 사용량을 대폭 절감하면서도 LoRA와 유사한 성능을 보여줍니다.

### 3.4. WebUI 인터페이스

LLaMA Factory는 파인튜닝 과정을 안내하는 직관적인 웹 기반 사용자 인터페이스를 제공합니다. 이 인터페이스는 사용자가 모델, 데이터셋, 하이퍼파라미터 등을 쉽게 설정할 수 있도록 구성되어 있습니다. 또한 실시간으로 학습 진행 상황을 모니터링할 수 있는 시각화 기능도 제공합니다.

WebUI 인터페이스의 주요 장점은 다음과 같습니다:

- 접근성: 프로그래밍에 익숙하지 않은 사용자도 쉽게 LLM을 파인튜닝할 수 있습니다.
- 편의성: 모든 설정을 한 곳에서 관리할 수 있어 파인튜닝 과정이 간소화됩니다.
- 모니터링: 실시간 시각화를 통해 모델의 학습 진행 상황을 쉽게 파악할 수 있습니다.

LLaMA Factory는 LLM 파인튜닝을 위한 강력하고 사용자 친화적인 도구로, 다양한 모델과 최신 파인튜닝 방법을 지원합니다. 특히 직관적인 WebUI 인터페이스를 통해 프로그래밍에 익숙하지 않은 사용자도 쉽게 LLM을 파인튜닝할 수 있다는 점이 큰 장점입니다. 이를 통해 더 많은 사용자가 자신의 니즈에 맞게 LLM을 활용할 수 있을 것으로 기대됩니다.

LLaMA Factory는 향후 더 많은 모델과 파인튜닝 방법을 지원할 예정이며, 사용자 피드백을 바탕으로 지속적으로 업데이트될 것입니다. 이를 통해 LLaMA Factory는 LLM 파인튜닝을 위한 표준 도구로 자리매김할 것으로 보입니다.

## 4. 설치 및 배포

LLaMA Factory를 사용하기 위해서는 먼저 해당 도구를 설치하고 배포해야 합니다. 여기서는 LLaMA Factory의 설치 및 배포 과정을 단계별로 안내하고, 발생 가능한 이슈에 대한 해결책을 제시하고자 합니다.

### 4.1. 필수 요구 사항

LLaMA Factory를 설치하기 전에 다음과 같은 필수 요구 사항을 충족해야 합니다:

- Python 3.8 이상
- PyTorch 1.13.1 이상
- CUDA 11.6 이상 (GPU 사용 시)

### 4.2. 설치 과정

LLaMA Factory의 설치 과정은 다음과 같습니다:

1. 저장소 클론:

```bash
git clone https://github.com/hiyouga/LLaMA-Factory.git
```

2. 가상 환경 생성:

```bash
conda create -n llama_factory python=3.10
```

3. 가상 환경 활성화:

```bash
conda activate llama_factory
```

4. 필요한 패키지 설치:

```bash
cd LLaMA-Factory
pip install -r requirements.txt
```

위 과정을 통해 LLaMA Factory를 설치할 수 있습니다. 다만 GPU를 사용하는 경우 CUDA 버전에 맞는 PyTorch를 설치해야 합니다.

### 4.3. 모델 준비

LLaMA Factory를 사용하기 위해서는 파인튜닝할 LLM을 준비해야 합니다. LLaMA Factory는 ChatGLM, BaiChuan, Qwen, LLaMA 등 다양한 모델을 지원합니다. 여기서는 BaiChuan 모델을 예시로 사용하겠습니다.

BaiChuan 모델은 다음 두 가지 방법 중 하나로 다운로드할 수 있습니다:

1. git lfs를 사용하여 저장소 직접 클론:

```bash
git lfs install
git clone https://huggingface.co/baichuan-inc/Baichuan2-13B-Chat
```

2. 저장소의 기본 정보만 다운로드한 후, Hugging Face에서 대용량 파일 다운로드:

```bash
GIT_LFS_SKIP_SMUDGE=1 git clone https://huggingface.co/baichuan-inc/Baichuan2-13B-Chat
cd Baichuan2-13B-Chat
wget "https://huggingface.co/baichuan-inc/Baichuan2-13B-Chat/resolve/main/pytorch_model-00001-of-00003.bin"
```

두 번째 방법을 사용하면 git 이력 없이 모델을 다운로드할 수 있어 저장 공간을 절약할 수 있습니다.

### 4.4. 배포 시 유의 사항

LLaMA Factory를 배포할 때는 다음과 같은 점에 유의해야 합니다:

- Alibaba Cloud의 AutoDL을 사용하는 경우, `conda activate llama_factory` 명령어 전에 `conda init bash`를 실행하여 conda 환경을 초기화해야 합니다. 그 후 터미널 창을 다시 열고 `conda activate llama_factory`를 실행합니다.
- BaiChuan 모델을 사용하는 경우, `transformers` 패키지의 버전을 `4.33.2`로 변경해야 합니다. 그렇지 않으면 `AttributeError: 'BaichuanTokenizer' object has no attribute 'sp_model'` 오류가 발생할 수 있습니다.

### 4.5. 문제 해결

LLaMA Factory 설치 및 배포 과정에서 다음과 같은 문제가 발생할 수 있습니다:

- CUDA 버전 불일치: LLaMA Factory는 CUDA 11.6 이상을 요구합니다. CUDA 버전이 맞지 않으면 PyTorch 설치 시 오류가 발생할 수 있습니다. 이 경우 CUDA 버전을 업그레이드하거나, 해당 CUDA 버전에 맞는 PyTorch를 설치해야 합니다.
- 패키지 버전 충돌: LLaMA Factory는 특정 버전의 패키지를 요구합니다. 다른 프로젝트와 패키지 버전이 충돌할 경우 설치에 실패할 수 있습니다. 이 경우 가상 환경을 사용하여 패키지 버전을 격리하는 것이 좋습니다.
- 메모리 부족: LLM 파인튜닝은 많은 메모리를 필요로 합니다. 메모리가 부족할 경우 학습이 중단되거나 오류가 발생할 수 있습니다. 이 경우 배치 크기를 줄이거나, 모델의 크기를 축소하거나, 더 큰 메모리를 가진 GPU로 학습을 진행해야 합니다.

위와 같은 문제가 발생할 경우 공식 문서나 커뮤니티에서 해결책을 찾아볼 수 있습니다. LLaMA Factory는 활발한 커뮤니티를 가지고 있어, 대부분의 문제에 대한 해결책을 쉽게 찾을 수 있습니다.

LLaMA Factory의 설치 및 배포 과정은 비교적 간단한 편이지만, 위에서 언급한 사항들에 주의해야 합니다. 특히 CUDA 버전과 패키지 버전 충돌 문제는 자주 발생하므로, 가상 환경을 사용하고 공식 문서의 지침을 잘 따르는 것이 중요합니다. 또한 LLM 파인튜닝에는 많은 메모리가 필요하므로, 충분한 메모리를 가진 GPU를 사용하는 것이 좋습니다.

마지막으로, LLaMA Factory는 활발히 업데이트되고 있는 프로젝트이므로, 최신 버전을 사용하는 것이 좋습니다. 최신 버전에는 새로운 기능과 버그 수정이 포함되어 있어, 더 나은 성능과 안정성을 제공합니다.

## 5. 파인튜닝 시작하기

LLaMA Factory를 설치하고 배포한 후에는 본격적으로 LLM 파인튜닝을 시작할 수 있습니다. 여기서는 LLaMA Factory의 WebUI를 사용하여 파인튜닝을 진행하는 방법을 단계별로 설명하겠습니다.

### 5.1. WebUI 실행

LLaMA Factory의 WebUI를 실행하려면 다음 명령어를 입력합니다:

```bash
CUDA_VISIBLE_DEVICES=0 python src/train_web.py
```

위 명령어를 입력하면 WebUI가 실행되고, 브라우저에서 해당 주소로 접속할 수 있습니다.

### 5.2. 모델 설정

WebUI의 상단에서는 파인튜닝할 모델의 기본 설정을 진행합니다. 주요 설정 항목은 다음과 같습니다:

- Model Name: ChatGLM, BaiChuan, Qwen, LLaMA 등 파인튜닝할 모델을 선택합니다. 여기서는 이전에 다운로드한 `Baichuan2-13B-Chat` 모델을 선택하겠습니다.
- Adapter Path: 다운로드한 BaiChuan 모델의 경로를 입력합니다.
- Finetuning method: 파인튜닝 방법을 선택합니다. `full`은 모든 모델 파라미터를 파인튜닝하고, `freeze`는 일부 파라미터를 동결한 채로 파인튜닝하며, `lora`는 특정 레이어의 일부 파라미터만 파인튜닝합니다.
- Model Checkpoint: 파인튜닝 전에는 비워둡니다. 파인튜닝 후에는 `Refresh Checkpoint` 버튼을 클릭하여 이전 파인튜닝 체크포인트를 불러올 수 있습니다.
- Advanced Configurations: 고급 설정으로, 일반적으로 기본값을 사용합니다.

### 5.3. 학습 설정

WebUI의 하단에서는 파인튜닝 학습 설정을 진행합니다. 주요 설정 항목은 다음과 같습니다:

- Stage: 학습 단계를 선택합니다. Pre-Training, Supervised Fine-Tuning, Reward Modeling, PPO, DPO Training 등이 있습니다. 여기서는 Supervised Fine-Tuning을 선택하겠습니다.
- Data dir: 학습 데이터셋 파일이 위치한 경로를 입력합니다. 일반적으로 LLaMA Factory 디렉토리 내의 `data` 폴더를 가리킵니다.
- Dataset: `Data Path`에서 데이터셋 파일을 선택합니다. 여기서는 `self_cognition` 데이터셋을 선택하겠습니다. 이 데이터셋은 LLM이 "너는 누구니?", "너를 누가 만들었니?" 등의 질문에 대답할 수 있도록 학습하기 위해 만들어진 것으로, 약 80개의 항목으로 구성되어 있습니다. 파인튜닝 전에 데이터셋의 내용을 수정하여 `<NAME>`과 `<AUTHOR>`를 실제 AI 모델의 이름과 제작사로 변경해야 합니다. 데이터셋을 선택한 후 `Preview Dataset` 버튼을 클릭하면 데이터셋의 첫 몇 줄을 미리 볼 수 있습니다.
- Learning rate: 학습률을 설정합니다. 값이 클수록 모델이 빠르게 학습하지만, 너무 크면 최적의 솔루션을 "건너뛸" 수 있습니다. 반대로 값이 너무 작으면 학습 속도가 느려집니다. 일반적으로 `5e-5` 정도의 값을 사용합니다.
- Epochs: 학습 횟수를 설정합니다. 값이 클수록 모델이 더 오래 학습하므로 성능이 좋아지지만, 너무 크면 과적합이 발생할 수 있습니다. 여기서는 데이터셋의 크기가 작으므로 `30`으로 설정하겠습니다.
- Max samples: 학습에 사용할 최대 샘플 수를 설정합니다. 여기서는 데이터셋의 크기가 작으므로 기본값을 사용하겠습니다.
- Compute Type: 학습에 사용할 연산 타입을 선택합니다. `fp16`과 `bf16` 중 하나를 선택할 수 있습니다. 여기서는 `bf16`을 사용하겠습니다.
- LR Scheduler: 학습률 스케줄러를 선택합니다. `cosine` 등 다양한 옵션이 있습니다.
- Maximum gradient norm: 그래디언트 클리핑에 사용할 최대 그래디언트 노름 값을 설정합니다. 여기서는 기본값을 사용하겠습니다.
- Output dir: 학습 결과를 저장할 디렉토리를 설정합니다. 기본적으로는 현재 시간을 이름으로 사용하지만, 원하는 이름으로 변경할 수 있습니다.
- 기타: 그 외 설정 항목은 기본값을 사용하겠습니다.

설정이 완료되면 `Preview Command` 버튼을 클릭하여 파인튜닝 명령어를 확인한 후, `Start` 버튼을 클릭하여 파인튜닝을 시작합니다. 데이터셋의 크기가 작으므로 파인튜닝은 몇 분 내에 완료될 것입니다 (정확한 시간은 사용하는 GPU의 성능에 따라 달라집니다. 필자의 경우 A40 48G GPU를 사용하였습니다). 파인튜닝 과정과 loss 함수 그래프는 WebUI 우측 하단에서 실시간으로 확인할 수 있습니다. 일반적으로 loss 함수의 값이 작을수록 모델의 예측 성능이 좋아집니다.

파인튜닝 과정에서 `AttributeError: 'BaichuanTokenizer' object has no attribute 'sp_model'` 오류가 발생할 경우, BaiChuan 모델의 `tokenization_baichuan.py` 파일을 수정해야 합니다. 수정 내용은 다음과 같습니다:

```python
@@ -68,6 +68,11 @@ class BaichuanTokenizer(PreTrainedTokenizer):
             if isinstance(pad_token, str)
             else pad_token
         )
+        self.vocab_file = vocab_file
+        self.add_bos_token = add_bos_token
+        self.add_eos_token = add_eos_token
+        self.sp_model = spm.SentencePieceProcessor(**self.sp_model_kwargs)
+        self.sp_model.Load(vocab_file)
         super().__init__(
             bos_token=bos_token,
             eos_token=eos_token,
             unk_token=unk_token,
             pad_token=pad_token,
             add_bos_token=add_bos_token,
             add_eos_token=add_eos_token,
             sp_model_kwargs=self.sp_model_kwargs,
             clean_up_tokenization_spaces=clean_up_tokenization_spaces,
             **kwargs,
         )
-        self.vocab_file = vocab_file
-        self.add_bos_token = add_bos_token
-        self.add_eos_token = add_eos_token
-        self.sp_model = spm.SentencePieceProcessor(**self.sp_model_kwargs)
-        self.sp_model.Load(vocab_file)
```

이에 대한 자세한 내용은 [이슈](https://github.com/baichuan-inc/Baichuan2/issues/204)를 참고하시기 바랍니다.

이상으로 LLaMA Factory를 사용하여 LLM 파인튜닝을 시작하는 방법을 알아보았습니다. WebUI를 통해 손쉽게 모델과 학습 설정을 진행할 수 있으며, 실시간으로 학습 진행 상황을 모니터링할 수 있습니다. 다만 파인튜닝 과정에서 발생할 수 있는 오류에 주의해야 하며, 필요에 따라 모델의 소스 코드를 직접 수정해야 할 수도 있습니다.

LLM 파인튜닝은 단순히 모델을 학습시키는 것에서 끝나지 않습니다. 학습이 완료된 후에는 모델의 성능을 평가하고, 필요에 따라 추가 학습을 진행해야 합니다. 또한 실제 서비스에 배포하기 위해서는 모델의 크기를 최적화하고, 안정적으로 서빙할 수 있는 환경을 구축해야 합니다. 이에 대해서는 다음 섹션에서 더 자세히 다루도록 하겠습니다.

## 6. 모델 테스트 및 평가

LLM 파인튜닝이 완료된 후에는 모델의 성능을 철저히 테스트하고 평가해야 합니다. 이 과정을 통해 모델이 의도한 대로 작동하는지 확인하고, 문제점을 파악하여 개선 방향을 설정할 수 있습니다. 여기서는 LLaMA Factory에서 파인튜닝된 모델을 테스트하고 평가하는 방법에 대해 자세히 알아보겠습니다.

### 6.1. 테스트 데이터셋 준비

모델을 테스트하기 위해서는 파인튜닝에 사용되지 않은 별도의 테스트 데이터셋을 준비해야 합니다. 테스트 데이터셋은 실제 서비스 환경에서 발생할 수 있는 다양한 상황을 포함해야 하며, 모델의 일반화 능력을 평가할 수 있어야 합니다.

테스트 데이터셋을 준비할 때는 다음과 같은 사항을 고려해야 합니다:

- 데이터셋의 크기: 테스트 데이터셋은 모델의 성능을 안정적으로 평가할 수 있을 만큼 충분한 크기를 가져야 합니다. 일반적으로 전체 데이터의 10~20% 정도를 테스트 데이터셋으로 할당합니다.
- 데이터의 다양성: 테스트 데이터셋은 실제 서비스에서 발생할 수 있는 다양한 케이스를 포함해야 합니다. 예를 들어 질문의 유형, 길이, 복잡도, 도메인 등이 다양해야 합니다.
- 데이터의 품질: 테스트 데이터셋의 품질이 모델 평가 결과에 직접적인 영향을 미칩니다. 따라서 데이터셋에 오류나 잡음이 없도록 주의 깊게 검토하고 정제해야 합니다.
- 데이터의 형식: 테스트 데이터셋의 형식은 파인튜닝에 사용된 데이터셋과 동일해야 합니다. 일관된 형식을 사용해야 모델의 성능을 정확히 평가할 수 있습니다.

### 6.2. 모델 테스트

테스트 데이터셋이 준비되면 LLaMA Factory의 Chat 탭을 사용하여 모델을 테스트할 수 있습니다. 먼저 `Refresh adapters` 버튼을 클릭하여 파인튜닝된 체크포인트를 불러온 후, 테스트하고자 하는 체크포인트를 선택하고 `Load Model` 버튼을 클릭하여 모델을 로드합니다.

모델이 로드되면 테스트 데이터셋의 샘플 질문을 입력하고 모델의 응답을 확인합니다. 이때 모델의 응답이 기대한 결과와 얼마나 일치하는지, 문맥에 맞는 자연스러운 응답을 생성하는지 등을 면밀히 검토합니다.

모델 테스트 과정에서는 다음과 같은 사항을 중점적으로 확인해야 합니다:

- 응답의 정확성: 모델이 질문의 요지를 정확히 파악하고 적절한 답변을 제공하는지 확인합니다.
- 응답의 유창성: 모델의 응답이 문법적으로 올바르고 자연스러운 언어로 구성되는지 평가합니다.
- 응답의 일관성: 유사한 질문에 대해 모델이 일관된 응답을 제공하는지 확인합니다.
- 응답 속도: 모델이 실용적인 수준의 응답 속도를 보이는지 측정합니다.
- 예외 처리: 모호하거나 부적절한 입력에 대해 모델이 합리적으로 대응할 수 있는지 테스트합니다.

### 6.3. 평가 지표 설정

모델의 성능을 객관적으로 평가하기 위해서는 적절한 평가 지표를 설정해야 합니다. 평가 지표는 모델의 용도와 목적에 따라 다를 수 있지만, 일반적으로 다음과 같은 지표들이 사용됩니다:

- 정확도(Accuracy): 모델의 응답이 정답과 얼마나 일치하는지 측정합니다. 일반적으로 응답이 정답과 완전히 일치하는 비율로 계산됩니다.
- F1 스코어(F1 Score): 정밀도(Precision)와 재현율(Recall)의 조화 평균으로, 모델의 종합적인 성능을 평가합니다.
- 사람 평가(Human Evaluation): 실제 사용자나 전문가가 모델의 응답을 직접 평가하는 방법입니다. 주관적일 수 있지만 실제 서비스 품질을 가늠할 수 있습니다.
- 퍼플렉서티(Perplexity): 언어 모델의 예측 능력을 측정하는 지표로, 모델이 실제 응답을 얼마나 잘 예측하는지 평가합니다. 낮을수록 좋은 성능을 나타냅니다.
- 응답 속도(Response Time): 모델이 입력을 받아서 응답을 생성하는 데 걸리는 시간을 측정합니다. 실시간 서비스에 중요한 지표입니다.

평가 지표는 모델의 성능을 다각도로 분석할 수 있어야 하며, 서비스의 요구 사항을 반영해야 합니다. 또한 평가 지표의 목표치를 설정하여 모델의 성능이 이를 만족하는지 확인해야 합니다.

### 6.4. 평가 결과 분석

모델 테스트와 평가 지표 측정이 완료되면 결과를 종합적으로 분석합니다. 분석 과정에서는 다음과 같은 사항을 중점적으로 검토해야 합니다:

- 목표 대비 성능: 모델의 성능이 사전에 설정한 목표치를 만족하는지 확인합니다. 목표에 미달할 경우 추가 개선이 필요합니다.
- 오류 사례 분석: 모델이 잘못된 응답을 한 경우 해당 사례를 심층 분석하여 원인을 파악합니다. 데이터셋의 품질, 모델 구조의 한계, 학습 설정의 문제 등이 원인일 수 있습니다.
- 성능 병목 파악: 모델의 응답 속도, 자원 사용량 등을 모니터링하여 성능 병목을 찾아냅니다. 병목 지점을 개선하여 전체적인 성능을 향상시킬 수 있습니다.
- 개선 방안 도출: 평가 결과를 바탕으로 모델의 개선 방안을 도출합니다. 데이터셋 보완, 모델 구조 변경, 하이퍼파라미터 조정 등 다양한 방법을 고려할 수 있습니다.

평가 결과 분석은 모델의 문제점을 파악하고 개선 방향을 설정하는 중요한 과정입니다. 분석 결과를 바탕으로 모델을 지속적으로 업데이트하고 최적화하여 서비스 품질을 높일 수 있습니다.

### 6.5. 추가 실험 및 반복 개선

평가 결과 분석을 통해 도출된 개선 방안을 적용하여 모델을 업데이트한 후, 다시 테스트와 평가를 진행합니다. 이러한 과정을 반복하여 모델의 성능을 지속적으로 향상시킵니다.

추가 실험 및 반복 개선 과정에서는 다음과 같은 사항을 고려해야 합니다:

- 체계적인 실험 설계: 개선 방안의 효과를 정확히 검증하기 위해 체계적인 실험을 설계해야 합니다. 한 번에 하나의 변수만 변경하고 다른 조건은 동일하게 유지하는 것이 좋습니다.
- 장기적인 관점: 단기적인 성능 향상뿐만 아니라 장기적인 관점에서 모델의 성능과 안정성을 고려해야 합니다. 과적합을 방지하고 일반화 능력을 유지하는 것이 중요합니다.
- 리소스 제약 고려: 모델의 성능을 향상시키는 것도 중요하지만, 실제 서비스 환경에서의 리소스 제약을 고려해야 합니다. 모델의 크기, 추론 속도, 메모리 사용량 등을 최적화해야 합니다.
- 버전 관리: 모델의 변경 사항과 실험 결과를 체계적으로 기록하고 관리해야 합니다. 이를 통해 문제 발생 시 원인을 추적하고 이전 버전으로 롤백할 수 있습니다.

추가 실험 및 반복 개선을 통해 모델을 지속적으로 발전시켜 나갈 수 있습니다. 다만 이 과정에서는 시간과 리소스가 많이 소모될 수 있으므로, 효율적인 실험 설계와 자원 관리가 필요합니다.

LLM 파인튜닝 모델의 테스트와 평가는 간과해서는 안 될 중요한 과정입니다. 체계적인 테스트와 평가를 통해 모델의 성능을 객관적으로 측정하고, 문제점을 파악하여 개선 방향을 설정할 수 있습니다. 또한 평가 지표를 설정하고 목표치를 관리함으로써 모델의 성능을 정량적으로 관리할 수 있습니다.

LLaMA Factory는 Chat 탭을 통해 파인튜닝된 모델을 쉽게 테스트할 수 있는 환경을 제공합니다. 그러나 실제 서비스에 모델을 적용하기 위해서는 보다 엄격하고 종합적인 테스트와 평가가 필요합니다. 별도의 테스트 데이터셋을 구축하고, 다양한 평가 지표를 활용하여 모델의 성능을 다각도로 분석해야 합니다.

또한 평가 결과를 바탕으로 모델을 지속적으로 개선하고 업데이트하는 것이 중요합니다. 이를 위해서는 체계적인 실험 설계와 효율적인 자원 관리가 뒷받침되어야 합니다. LLaMA Factory는 이러한 일련의 과정을 자동화하고 간소화하여 사용자가 보다 쉽게 LLM 파인튜닝 모델을 개발하고 배포할 수 있도록 지원합니다.

## 7. 모델 내보내기 및 배포

LLM 파인튜닝 모델의 개발이 완료되면 실제 서비스에 적용할 수 있도록 모델을 내보내고 배포해야 합니다. 모델 내보내기와 배포는 개발된 모델을 서비스 환경에 통합하는 중요한 과정으로, 모델의 성능과 안정성을 유지하면서도 효율적으로 수행되어야 합니다.

여기서는 LLaMA Factory를 사용하여 파인튜닝된 모델을 내보내고 배포하는 방법에 대해 자세히 알아보겠습니다.

### 7.1. 모델 내보내기

모델 내보내기는 파인튜닝된 모델의 가중치와 구조를 추출하여 서비스 환경에서 사용할 수 있는 형태로 저장하는 과정입니다. LLaMA Factory에서는 Export 탭을 통해 모델을 간편하게 내보낼 수 있습니다.

모델을 내보내기 위해서는 다음과 같은 설정이 필요합니다:

- Export Directory: 내보낸 모델이 저장될 디렉토리를 지정합니다.
- Model Checkpoint: 내보낼 모델의 체크포인트를 선택합니다. 최종 파인튜닝된 체크포인트를 선택하는 것이 일반적입니다.
- Quantization: 모델 가중치를 양자화하여 모델 크기를 줄일 수 있습니다. 4비트, 8비트 등 다양한 옵션을 선택할 수 있습니다.
- Maximum Chunk Size: 모델을 여러 개의 청크 파일로 분할할 때 각 청크의 최대 크기를 지정합니다. 모델 크기가 크거나 배포 환경의 제약 사항이 있을 때 유용합니다.
- Precision: 모델 가중치의 정밀도를 지정합니다. FP16, BF16 등의 옵션을 선택할 수 있습니다.

필요한 설정을 완료한 후 `Start Export` 버튼을 클릭하면 모델 내보내기가 시작됩니다. 내보내기가 완료되면 지정한 디렉토리에서 내보낸 모델 파일을 확인할 수 있습니다.

### 7.2. 모델 서빙 환경 구축

내보낸 모델을 서비스에 적용하기 위해서는 모델 서빙 환경을 구축해야 합니다. 모델 서빙 환경은 클라이언트의 요청을 받아 모델을 실행하고 결과를 반환하는 서버 시스템입니다.

모델 서빙 환경을 구축할 때는 다음과 같은 사항을 고려해야 합니다:

- 프레임워크 선택: TensorFlow Serving, TorchServe, FastAPI 등 다양한 모델 서빙 프레임워크 중 서비스 요구 사항에 맞는 것을 선택합니다.
- 하드웨어 구성: 모델의 크기와 추론 속도를 고려하여 적절한 하드웨어 리소스를 할당해야 합니다. GPU, CPU, 메모리 등의 사양을 결정합니다.
- 배포 환경 선택: 온프레미스, 클라우드, 엣지 디바이스 등 다양한 배포 환경 중 서비스 요구 사항에 맞는 것을 선택합니다.
- 동시성 및 확장성 고려: 동시 접속자 수와 트래픽 증가에 대비하여 서버의 동시성과 확장성을 고려해야 합니다. 로드 밸런싱, 오토 스케일링 등의 기술을 활용할 수 있습니다.
- 보안 및 접근 제어: 모델 서버에 대한 외부 접근을 제어하고, 인증 및 권한 관리를 적용하여 보안을 강화해야 합니다.

### 7.3. 모델 로딩 및 API 개발

모델 서빙 환경이 구축되면 내보낸 모델을 로딩하고 API를 개발하여 클라이언트와 통신할 수 있도록 해야 합니다.

모델 로딩 과정에서는 다음과 같은 작업이 수행됩니다:

- 모델 파일 로딩: 내보낸 모델 파일을 메모리에 로드합니다.
- 모델 구조 복원: 모델의 구조를 복원하고 가중치를 로드합니다.
- 추론 준비: 모델을 추론 모드로 전환하고, 필요한 입력 및 출력 텐서를 준비합니다.

모델이 로딩되면 API를 개발하여 클라이언트의 요청을 처리할 수 있도록 해야 합니다. API 개발 시에는 다음과 같은 사항을 고려해야 합니다:

- 입력 및 출력 포맷 정의: 클라이언트가 모델에 전달할 입력 데이터의 포맷과 모델이 반환할 출력 데이터의 포맷을 명확히 정의해야 합니다.
- 요청 및 응답 처리: HTTP, gRPC 등의 프로토콜을 사용하여 클라이언트의 요청을 받고 모델의 출력을 응답으로 반환하는 로직을 구현해야 합니다.
- 에러 처리: 잘못된 입력, 모델 오류 등 다양한 예외 상황을 처리할 수 있도록 에러 처리 로직을 구현해야 합니다.
- API 문서화: API의 사용 방법, 입력/출력 포맷, 에러 코드 등을 문서화하여 클라이언트 개발자들이 쉽게 사용할 수 있도록 해야 합니다.

### 7.4. 모델 배포 및 모니터링

모델 서버가 준비되면 실제 서비스 환경에 배포합니다. 배포 과정에서는 다음과 같은 사항을 고려해야 합니다:

- 배포 파이프라인 구축: 모델 버전 관리, 자동 빌드 및 테스트, 배포 승인 등의 과정을 자동화하는 배포 파이프라인을 구축합니다.
- 카나리아 배포: 새로운 모델 버전을 일부 사용자에게만 배포하여 안정성과 성능을 검증한 후 전체 사용자에게 배포하는 단계적 배포 전략을 사용할 수 있습니다.
- 모니터링 시스템 구축: 모델 서버의 CPU, 메모리, 디스크 사용량, 응답 시간, 에러 발생 빈도 등 주요 지표를 실시간으로 모니터링할 수 있는 시스템을 구축합니다.
- 롤백 및 재배포 대응: 배포된 모델에서 문제가 발생할 경우 신속하게 이전 버전으로 롤백하거나 수정된 버전을 재배포할 수 있도록 대응 체계를 갖춥니다.

배포 후에는 모델의 성능과 안정성을 지속적으로 모니터링하고 필요에 따라 업데이트와 개선을 진행해야 합니다. 사용자 피드백, 에러 로그, 모니터링 데이터 등을 분석하여 모델의 문제점을 파악하고 해결해 나가는 것이 중요합니다.

### 7.5. 지속적인 모델 개선

배포된 모델은 지속적으로 관리되고 개선되어야 합니다. 새로운 데이터가 수집되고 서비스 요구 사항이 변화함에 따라 주기적으로 모델을 업데이트해야 할 필요가 있습니다.

모델 개선 과정에서는 다음과 같은 작업이 수행될 수 있습니다:

- 데이터 수집 및 정제: 서비스 환경에서 수집된 새로운 데이터를 정제하고 라벨링하여 파인튜닝 데이터셋을 확장합니다.
- 모델 재학습: 확장된 데이터셋을 사용하여 모델을 재학습하고 성능을 개선합니다. 이때 기존 모델의 가중치를 초기값으로 사용하는 전이 학습 기법을 활용할 수 있습니다.
- A/B 테스트: 새로운 모델과 기존 모델의 성능을 비교하기 위해 A/B 테스트를 수행합니다. 사용자를 두 그룹으로 나누어 각각 다른 모델을 적용한 후 주요 지표를 비교합니다.
- 모델 업데이트: A/B 테스트 결과를 바탕으로 신중하게 모델을 업데이트합니다. 업데이트 과정에서 발생할 수 있는 위험을 최소화하기 위해 단계적으로 배포하는 것이 좋습니다.

지속적인 모델 개선을 통해 서비스의 품질을 높이고 사용자 만족도를 향상시킬 수 있습니다. 다만 이 과정에서는 모델 성능뿐만 아니라 비즈니스 목표, 사용자 경험, 윤리적 고려사항 등 다양한 요소를 종합적으로 고려해야 합니다.

LLaMA Factory를 사용하면 파인튜닝된 모델을 쉽게 내보내고 배포할 수 있습니다. 모델 내보내기 기능을 통해 모델의 가중치와 구조를 추출하고, 모델 서빙 환경을 구축하여 API로 서비스할 수 있습니다. 또한 배포 자동화, 모니터링, 지속적인 개선 등의 과정을 체계화하여 안정적이고 고품질의 서비스를 제공할 수 있습니다.

그러나 모델 배포는 단순히 기술적인 문제가 아닌 조직 전체의 협력이 필요한 과정입니다. 데이터 엔지니어, ML 엔지니어, 백엔드 개발자, 인프라 엔지니어 등 다양한 역할의 전문가들이 협업하여 모델의 개발, 배포, 운영을 진행해야 합니다. 또한 비즈니스 관점에서의 의사결정, 사용자 피드백 반영, 윤리 및 법규 준수 등 기술 외적인 요소들도 함께 고려되어야 합니다.

LLaMA Factory는 이러한 일련의 과정에서 모델 개발과 배포를 위한 편리한 도구를 제공함으로써 조직의 역량을 집중할 수 있도록 돕습니다. 사용자의 요구 사항을 바탕으로 지속적으로 발전해 나갈 LLaMA Factory가 LLM 파인튜닝 및 배포의 대표 도구로 자리매김하기를 기대합니다.

## 결론

지금까지 LLM 파인튜닝의 개념부터 LLaMA Factory를 활용한 실전 가이드까지 살펴보았습니다. LLM 파인튜닝은 사전 학습된 언어 모델을 특정 도메인이나 태스크에 적응시켜 성능을 극대화하는 중요한 과정입니다. 최근에는 LoRA, QLoRA, PEFT 등 효율적이고 효과적인 파인튜닝 기법들이 등장하여 LLM 파인튜닝의 진입 장벽을 낮추고 있습니다.

특히 LLaMA Factory와 같은 통합 파인튜닝 도구는 다양한 모델과 기법을 손쉽게 사용할 수 있게 함으로써 LLM 파인튜닝의 대중화에 기여하고 있습니다. LLaMA Factory는 직관적인 웹 인터페이스를 통해 파인튜닝 과정을 단계별로 안내하고, 학습 진행 상황을 실시간으로 모니터링할 수 있게 해줍니다. 뿐만 아니라 모델 내보내기 및 배포 기능을 제공하여 파인튜닝된 모델을 실제 서비스에 쉽게 적용할 수 있도록 지원합니다.

LLM 파인튜닝은 단순히 모델을 학습시키는 것에서 그치지 않습니다. 고품질의 데이터셋 구축, 적절한 하이퍼파라미터 설정, 체계적인 테스트와 평가, 지속적인 모니터링과 업데이트 등 일련의 과정이 유기적으로 연결되어야 합니다. 또한 기술적인 측면뿐만 아니라 비즈니스 목표, 사용자 경험, 윤리 및 법규 준수 등 다양한 요소를 종합적으로 고려해야 합니다. LLaMA Factory는 이러한 복잡한 과정을 최대한 자동화하고 추상화하여 사용자가 핵심 태스크에 집중할 수 있게 해줍니다.

LLM 파인튜닝은 자연어 처리 분야의 패러다임을 바꾸고 있습니다. 챗봇, 검색 엔진, 콘텐츠 생성, 코드 자동 완성 등 다양한 애플리케이션에서 LLM 파인튜닝 기술이 활용되고 있으며, 그 영향력은 날로 커지고 있습니다. 앞으로도 LLM 파인튜닝 기술은 지속적으로 발전하여 더욱 정교하고 효율적인 방식으로 언어 모델을 활용할 수 있게 될 것입니다.
