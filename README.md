# Enhancing Query Understanding in LLMs via Ambiguity Classification and Clarification Question Generation

> **모호성 유형 분류와 DPO 기반 질문 생성을 통한 LLM의 쿼리 이해능력 강화**

본 리포지토리는 거대 언어 모델(LLM)이 사용자 쿼리의 모호성을 능동적으로 식별하고, 명확화 질문(Clarification Question)을 생성하여 해소하는 **2단계 다중 에이전트 시스템**의 공식 구현 코드를 포함하고 있습니다. 모든 코드는 학습 과정의 시각화와 단계별 참조가 용이하도록 **Jupyter Notebook (.ipynb)** 형식으로 제공됩니다.

## 📖 Abstract

대규모 언어 모델(LLM)과 사용자 간의 상호작용에서 쿼리의 모호성은 모델의 해석 오류를 유발하고 신뢰성을 저해하는 주요 요인입니다. 그러나 기존 LLM은 모호한 입력을 탐지하거나 명시적으로 해소하는 데 한계를 보입니다. **따라서 본 연구의 주된 목표는 모호성 해소 프로세스를 자동화하여 LLM의 쿼리 이해 능력을 강화하고 사용자의 노력을 최소화하는 것입니다.**

이를 위해 본 연구는 **1) 쿼리의 모호성 유형을 8가지로 정밀 분류**하고, **2) 식별된 유형에 최적화된 명확화 질문을 생성**하는 파이프라인을 제안합니다. 특히, 생성 모델에는 **직접 선호도 최적화(DPO)**를 적용하여 질문이 인간의 선호도와 의도에 부합하도록 정렬(Alignment)하였습니다. 본 시스템은 경량화된 모델(SLM)만으로 구성되어 있으며, 99.32%의 높은 구동 안정성과 SFT 대비 향상된 질문 품질을 입증했습니다.

## 💻 Interactive Demo

Google Colab 환경에서 전체 파이프라인과 **Gradio 기반 챗봇 인터페이스**를 직접 실행해 볼 수 있습니다. 아래 배지를 클릭하여 데모를 확인해 보세요.
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/jihyeyu33/LLM-Interactive-Clarification/blob/main/04_demo/01_ambiguity_classification_demo.ipynb)

* **참고**: 데모 실행을 위해서는 GPU 환경이 권장됩니다.
* 노트북 내의 셀을 순서대로 실행하면 Gradio Web UI가 실행됩니다.

## 📂 Repository Structure

```bash
.
├── 00_dataset/                 # 모델 학습 및 평가에 사용된 데이터셋 (.jsonl, .csv)
├── 01_classification/          # 모호성 유형 분류 모델 학습 및 추론 코드 (.ipynb)
├── 02_question_generation_sft/ # 명확화 질문 생성 모델 SFT 학습 코드 (.ipynb)
├── 03_question_generation_dpo/ # 인간 선호도 정렬을 위한 DPO 학습 코드 (.ipynb)
└── 04_evaluation/              # 모델 성능 평가 지표 측정 및 결과 분석 (.ipynb)

```

## 🚀 Key Features

* **Two-Stage Pipeline**: 'Classification (분류)'  'Generation (생성)'의 구조로 모호성을 체계적으로 처리합니다.
* **Ambiguity Classification**: 사용자 쿼리를 `NONE`(비모호) 혹은 8가지 모호성 유형(Ambiguity Types) 중 하나로 분류합니다.
* **DPO Alignment**: Direct Preference Optimization을 통해 모델이 더 자연스럽고 유용한 명확화 질문을 생성하도록 학습되었습니다.
* **Efficient SLM**: 거대 모델 대신 소형 언어 모델(Phi-4, Qwen-2.5 등)과 LoRA 파인튜닝을 사용하여 자원 효율성을 극대화했습니다.

## 🛠️ Getting Started

본 프로젝트의 코드는 `.ipynb` 파일로 구성되어 있습니다. GitHub에서 코드를 직접 확인하거나 Jupyter 환경(Colab, Jupyter Lab)에서 실행할 수 있습니다.

### Usage Guide

1. **Data Preparation**: `00_dataset` 폴더에서 학습에 사용된 `.jsonl` 및 `.csv` 형식의 데이터셋을 확인할 수 있습니다.
2. **Ambiguity Classification**: `01_classification` 폴더에서 분류 모델(LoRA)을 학습시킵니다.
3. **Question Generation**:
* `02_question_generation_sft`: 기본 SFT 모델을 학습합니다.
* `03_question_generation_dpo`: SFT 모델을 기반으로 DPO 정렬을 수행합니다.


4. **Evaluation**: `05_evaluation` 폴더에서 LLM-as-a-judge 방식 등을 통해 성능을 평가합니다.

## 📊 Performance

* **Classification Accuracy**: 66.04% (8-class classification)
* **Generation Quality**: BERTScore F1 **0.8811**
* **Preference Improvement**: DPO 적용 후 SFT 대비 승률 **+4.4%p** 향상
* **System Stability**: **99.32%** success rate in end-to-end execution

## 👥 Authors & Context

이 연구는 한양대학교 정보시스템학과에서 수행되었습니다.

* **저자 (Authors)**:
* **유지혜** (Jihye Yu)
* **김다연** (Dayeon Kim)


* **지도교수 (Advisor)**:
* **김은찬 교수** (Prof. Eunchan Kim, Dept. of Information Systems, Hanyang University)


* **연구 분야**: Large Language Models (LLM), Human-AI Interaction (HAI), HCI
* **연구 기간**: 2025.08 - 2025.12

## 📝 Citation

본 연구 내용을 인용하거나 참고하실 경우 아래 형식을 사용해 주세요.

```bibtex
@misc{yu2025enhancing,
  title={Enhancing Query Understanding in Large Language Models via Ambiguity Classification and Clarification Question Generation},
  author={Yu, Jihye and Kim, Dayeon},
  year={2025},
  publisher={GitHub},
  journal={GitHub repository},
  howpublished={\url{https://github.com/jihyeyu33/LLM-Interactive-Clarification}}
}

```
