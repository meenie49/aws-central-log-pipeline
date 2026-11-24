# 🏥 AWS EKS 기반 MSA 로그 중앙 수집 파이프라인

> ALB · EKS · VPC Flow · CloudTrail 4종 로그를
> Lambda → Firehose → S3 / OpenSearch로 적재하는
> 중앙 수집 파이프라인 인프라 (Terraform)

---

## 📌 프로젝트 소개

병원 예약/알람 MSA 서비스에서 발생하는 4종 로그를
중앙에서 수집·필터링·저장·시각화하는 파이프라인입니다.

- **장기 보관**: S3 (GZIP 압축, prefix별 분리)
- **실시간 분석**: OpenSearch Dashboard

---

## 🏗️ 아키텍처

![architecture](./docs/architecture.png)

| 로그 종류 | 수집 방식 | 처리 | 저장 |
|---|---|---|---|
| ALB Access Log | S3 Event Trigger | Lambda | S3 / OpenSearch |
| EKS Log | CW Subscription Filter | Lambda | S3 / OpenSearch |
| VPC Flow Log | CW Subscription Filter | Lambda | S3 / OpenSearch |
| CloudTrail Log | CW Subscription Filter | Lambda | S3 / OpenSearch |

---

## ✨ 주요 기능

- **4종 로그 중앙 수집** - 로그 소스별 최적 트리거 방식 적용
- **Lambda 필터링** - 불필요 로그 제거로 저장 비용 절감
- **목적별 파이프라인 분리** - S3(보관) / OpenSearch(분석) 이중 적재
- **실시간 대시보드** - ALB · CloudTrail · VPC Flow 시각화
- **IAM 3단계 권한 설계** - AWS IAM · 도메인 정책 · 내부 Role

---

## 🛠️ 기술 스택

| 분류 | 기술 |
|---|---|
| IaC | Terraform |
| Container | AWS EKS, Kubernetes |
| Compute | AWS Lambda (Python 3.11) |
| Streaming | Amazon Kinesis Data Firehose |
| Storage | Amazon S3 |
| Search | Amazon OpenSearch Service |
| Monitoring | Amazon CloudWatch |
| Network | AWS VPC, ALB |
| Security | AWS IAM, CloudTrail |