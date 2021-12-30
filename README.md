# 모두를 위한 클라우드 네이티브 한국어 자연어 처리 모델 훈련 및 활용법 (부제: 허깅페이스(Hugging Face)와 Amazon SageMaker가 만났다!)

텍스트 분석, 번역, 문장 요약, 엔티티 분류 등 자연어 처리의 AI/ML 적용 사례들이 매우 많지만, 여전히 많은 고객들이 기술적인 진입 장벽으로 도입에 어려움을 겪고 있습니다. 일부 분들은 이미 Hugging Face 트랜스포머 라이브러리와 SageMaker의 많은 예제 코드들로 AIML 적용을 가속화하고 있지만, 2021년 초까지는 SageMaker가 Hugging Face 전용 컨테이너를 네이티브하게 지원하지 않아 커스텀 스크립트와 커스텀 컨테이너를 따로 작성해야 하는 어려움이 있었습니다.

하지만, 최근 AWS는 Amazon SageMaker에서 Hugging Face의 트랜스포머 모델을 더 쉽게 훈련하고 배포할 수 있는 Hugging Face 딥러닝 훈련 컨테이너 및 추론 컨테이너를 도입했습니다. 따라서, 인프라 설정에 대한 고민 없이 몇 줄의 코드만으로 빠르게 자연어 처리 모델의 훈련 및 프로덕션 배포가 가능하게 되었습니다.

본 핸즈온은 3개 파트(훈련, 추론, MLOps)의 핸즈온 랩으로 구성되어 있으며, 각 랩은 독립적으로 수행 가능합니다. SageMaker에 보다 익숙해지고 싶다면 모든 랩을 수행하시는 것을 권장드리지만, 니즈에 적합한 파트만 수행하셔도 됩니다. 각 파트는 1시간 정도 소요되며, 모든 핸즈온 수행에는 총 3시간 정도 소요됩니다. (코드만 돌리면 1시간 이내에 수행 가능합니다.)

**_Note: 한국 고객들은 영어가 아닌 한국어 모델에 대한 샘플 코드를 필요로 하고 있습니다. 따라서 이 핸즈온은 모두 한국어를 우선으로 작성하였습니다. 만약 영어 버전에 대한 니즈가 있다면 저자에게 연락을 부탁드립니다._**

## Lab 1: Training

- **Training on Local Environment**: SageMaker API 호출 없이 기존에 온프레미스/로컬 환경에서 한국어 자연어 처리 모델을 훈련하는 방법을 그대로 재현합니다. 한국어 자연어 처리 및 Hugging Face 라이브러리 사용법에 익숙치 않다면 이 핸즈온을 수행하는 것을 권장합니다.

- **Training on SageMaker**: Hugging Face 한국어 자연어 처리 모델을 클라우드 네이티브 방식으로 훈련하는 법을 익히게 됩니다. 훈련 및 추론 수행 시 인프라 설정에 대한 추가 작업이 필요하지 있기에, 단일 GPU 기반의 딥러닝 훈련을 포함한 멀티 GPU 및 멀티 인스턴스 분산 훈련을 보다 쉽고 빠르게 수행할 수 있습니다. 

## Lab 2: Serving

- **SageMaker Real-time Endpoint**: SageMakers는 사전 빌드된 Hugging Face 추론 컨테이너와 Hugging Face Inference Toolkit을 제공하고 있기 때문에, 기존 SageMaker 엔드포인트 배포와 동일한 방법으로 진행할 수 있습니다. 또한, Hugging Face 전용 기능으로 Hugging Face Hub(https://huggingface.co/models) 에 등록된 모델을 직접 임포트해서 엔드포인트를 배포하는 법을 익힐 수 있습니다.

- **SageMaker Batch Transform**: SageMaker 리얼타임 엔드포인트(SageMaker real-time endpoint)는 실시간으로 추론 결괏값을 빠른 응답속도 내에 전송받을 수 있지만, 호스팅 서버가 최소 1대 이상 구동되어야 하므로 비용적인 측면에서 부담이 됩니다. 이런 경우 SageMaker 배치 변환(batch transform) 기능을 사용해 훈련 인스턴스처럼 배치 변환을 수행하는 때에만 컴퓨팅 인스턴스를 사용하여 비용을 절감할 수 있습니다.

- **SageMaker Serverless Endpoint**: SageMaker Serverless Inference는 re:Invent 2021에 런칭된 신규 추론 옵션으로 호스팅 인프라 관리에 대한 부담 없이 머신 러닝을 모델을 쉽게 배포하고 확장할 수 있도록 제작된 신규 추론 옵션입니다. SageMaker Serverless Inference는 컴퓨팅 리소스를 자동으로 시작하고 트래픽에 따라 자동으로 스케일 인/아웃을 수행하므로 인스턴스 유형을 선택하거나 스케일링 정책을 관리할 필요가 없습니다. 따라서, 트래픽 급증 사이에 유휴 기간이 있고 콜드 스타트를 허용할 수 있는 워크로드에 이상적입니다.

## Lab 3: MLOps

- **SageMaker Pipelines**: SageMaker Pipelines은 re:Invent 2020 서비스 런칭 이후 지속적으로 업데이트되고 있으며, 2021년 8월 업데이트된 주요 기능인 Lambda Step을 사용하면 호스팅 엔드포인트 모델 배포를 비롯한 서버리스 작업들을 쉽게 수행할 수 있습니다. 또한 캐싱(caching) 기능을 사용하면 모든 파이프라인을 처음부터 재시작할 필요 없이 변경된 파라메터에 대해서만 빠르게 실험해볼 수 있습니다.
  
# References

- KoELECTRA: https://github.com/monologg/KoELECTRA
- Naver Sentiment Movie Corpus v1.0: https://github.com/e9t/nsmc
- Hugging Face on Amazon SageMaker: https://huggingface.co/docs/sagemaker/main
- Hugging Face examples: https://github.com/huggingface/notebooks/tree/master/sagemaker