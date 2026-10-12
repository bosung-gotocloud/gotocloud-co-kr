---
title: "Integration of MLops HPC and CAE HPC using scheduler"
date: "2024-01-17T10:56:18+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=2338"
---

Ask to ChatGPT about the integration of MLops HPC and CAE HPC based on the scheduler.

### (Question) Integration of MLops HPC and CAE HPC using scheduler

### (Answer)

MLops HPC is a set of practices that aims to automate and streamline the end-to-end lifecycle of machine learning models, from development to deployment and monitoring, on high performance computing (HPC) systems. CAE HPC is the use of HPC systems for computer-aided engineering (CAE) applications, such as computational fluid dynamics (CFD), finite element analysis (FEA), and structural optimization.

One of the challenges of integrating MLops HPC and CAE HPC is to manage the workload distribution and resource allocation on the shared HPC clusters. A scheduler is a tool that can help with this task by accepting, scheduling, and monitoring jobs on the HPC nodes. There are different types of schedulers that can be used for MLops HPC and CAE HPC, such as:

- Slurm: an open-source, scalable, and fault-tolerant scheduler that is widely used for HPC clusters. Slurm can support various GPU libraries, such as PETSc and AmgX, for linear solvers and machine learning frameworks, such as Kubeflow, for MLOps.

MLOps on HPC/Slurm with Kubeflow (dkube.io)

- Slurm vs LSF vs Kubernetes Scheduler: Which is Right for You? (run.ai)

- LSF: a commercial, enterprise-grade scheduler that can handle complex and heterogeneous HPC workloads. LSF can integrate with various machine learning platforms, such as IBM Watson Machine Learning Accelerator, and CAE software, such as Ansys Fluent and Siemens StarCCM+

Manufacturing and CAE with Intel Select Solutions for HPC on Google Cloud

- Kubernetes Scheduler: a native scheduler for Kubernetes, which is a popular platform for containerized applications. Kubernetes Scheduler can run AI/ML workloads at scale using tools like Kubeflow and NVIDIA GPU Operator. Kubernetes Scheduler can also run CAE workloads using tools like OpenFOAM and Singularity

A HPC Co-scheduler with Reinforcement Learning | SpringerLink

The choice of the scheduler depends on the specific requirements and preferences of the MLops HPC and CAE HPC users. Some factors to consider are:

- Scalability: how well the scheduler can handle large and diverse workloads and resources

- Flexibility: how easy the scheduler can be customized and configured to suit different needs and scenarios

- Compatibility: how well the scheduler can integrate with the existing HPC infrastructure and software

- Performance: how fast and efficient the scheduler can execute and monitor the jobs

- Cost: how much the scheduler costs to acquire and maintain

 

MLops HPC는 HPC(고성능 컴퓨팅) 시스템에서 머신러닝 모델의 개발부터 배포 및 모니터링에 이르는 전체 수명주기를 자동화하고 간소화하는 일련의 관행입니다. CAE HPC는 CFD(계산 유체 역학), FEA(유한 요소 분석), 구조 최적화 등의 컴퓨터 보조 공학(CAE) 응용 프로그램을 위해 HPC 시스템을 사용하는 것입니다.

MLops HPC와 CAE HPC를 통합하는 도전 과제 중 하나는 공유 HPC 클러스터에서 작업 분배와 자원 할당을 관리하는 것입니다. 스케줄러는 HPC 노드에서 작업을 수락, 스케줄링, 모니터링하는 도구로, 이 작업을 돕습니다. MLops HPC와 CAE HPC에 사용할 수 있는 다양한 유형의 스케줄러가 있습니다. 예를 들면:

- Slurm: HPC 클러스터에 널리 사용되는 오픈소스, 확장성, 내결함성 스케줄러입니다. Slurm은 선형 솔버와 머신러닝 프레임워크를 위한 다양한 GPU 라이브러리, 예를 들어 PETSc와 AmgX, Kubeflow 등을 지원합니다

MLOps on HPC/Slurm with Kubeflow (dkube.io)

- Slurm vs LSF vs Kubernetes Scheduler: Which is Right for You? (run.ai)

- LSF: 복잡하고 이기종의 HPC 작업을 처리할 수 있는 상업용, 엔터프라이즈급 스케줄러입니다. LSF는 IBM Watson Machine Learning Accelerator와 같은 다양한 머신러닝 플랫폼과 Ansys Fluent, Siemens StarCCM+와 같은 CAE 소프트웨어와 통합할 수 있습니다

Manufacturing and CAE with Intel Select Solutions for HPC on Google Cloud

- Kubernetes Scheduler: 컨테이너화된 애플리케이션을 위한 인기있는 플랫폼인 Kubernetes의 기본 스케줄러입니다. Kubernetes Scheduler는 Kubeflow와 NVIDIA GPU Operator와 같은 도구를 사용하여 대규모 AI/ML 작업을 실행할 수 있습니다. 또한 OpenFOAM과 Singularity와 같은 도구를 사용하여 CAE 작업을 실행할 수 있습니다.

A HPC Co-scheduler with Reinforcement Learning | SpringerLink

스케줄러의 선택은 MLops HPC와 CAE HPC 사용자의 특정 요구사항과 선호도에 따라 달라집니다. 고려해야 할 몇 가지 요인은 다음과 같습니다:

- 확장성: 스케줄러가 크고 다양한 작업과 자원을 얼마나 잘 처리할 수 있는지

- 유연성: 스케줄러를 다른 요구사항과 시나리오에 맞게 얼마나 쉽게 사용자 정의하고 설정할 수 있는지

- 호환성: 스케줄러가 기존의 HPC 인프라와 소프트웨어와 얼마나 잘 통합할 수 있는지

- 성능: 스케줄러가 작업을 얼마나 빠르고 효율적으로 실행하고 모니터링할 수 있는지

- 비용: 스케줄러를 구입하고 유지하는 데 드는 비용은 얼마인지
