
# 📘 Blog Style Guide (Verilog & Digital Design Series)
_Last updated: 2025-10-22

---

## 📁 카테고리 구조

### 디지털 설계
- **Fundamentals**: 기본 개념, 원리, 정의  
  → 예: 조합회로, 순차회로, 블로킹/논블로킹  
- **Application**: 실제 설계 적용, 코드 예제, 구현 방법  
  → 예: 회로 최적화, FSM 설계, 파이프라인 설계  
- **Analysis**: 장단점, 트레이드오프, 문제 해결 경험, 고찰  
  → 예: 지연 시간 vs 면적 비교, Race Condition 분석  

### Verilog
- **Syntax**: 기본 문법 정리  
  → 예: always 블록, case문, 연산자  
- **Tips**: 유용한 팁  
  → 예: 블로킹/논블로킹 주의점, 시뮬레이션 팁  

### FPGA 개발
- **Tutorial**: 툴 사용법, Vivado/Vitis/HLS 가이드  
- **Debugging**: 실제 디버깅 경험, 에러 사례  

### 프로젝트 모음
- **Post-mortem**: 완료된 프로젝트 회고 및 분석  

### 학습 & 팁
- **Blog**: 블로그 관련 팁 (Jekyll, GitHub Pages 등)  
- **Study**: 기타 학습 내용 (논문 정리, 회로 이론 등)

---

## 📝 포스팅 기본 양식

```yaml
---
layout: post
title: "글 제목"
date: YYYY-MM-DD HH:MM:SS +0900
categories:
  - 디지털 설계  # 대분류
tags:
  - Fundamentals   # 하위 분류
  - Verilog_Study_Series  # 시리즈 통합용 공통 태그
  - LogicDesign    # 기술 주제
  - 회로설계기초    # 한글 검색용
toc: true
---
```

---

## 📚 포스팅 시리즈 예시

| 순서 | 제목 | 카테고리 | 주요 태그 | 예고 문장 |
|------|------|-----------|-----------|-----------|
| 1 | 조합회로 (Combinational Logic) | 디지털 설계 / Fundamentals | `CombinationalLogic`, `LogicDesign`, `조합회로` | 다음 글에서는 입력과 출력 사이에 **상태(State)** 개념이 추가되는 순차회로를 다룹니다. |
| 2 | 순차회로 (Sequential Logic) | 디지털 설계 / Fundamentals | `SequentialLogic`, `LogicDesign`, `순차회로` | 다음 글에서는 순차회로 내에서 자주 혼동되는 **블로킹 vs 논블로킹**의 차이를 정리합니다. |
| 3 | 블로킹 vs 논블로킹 | 디지털 설계 / Fundamentals | `Blocking`, `Nonblocking`, `블로킹논블로킹`, `Verilog` | 이번 글을 끝으로 조합–순차–동시성의 기초 시리즈를 마무리합니다. |

---

## 🏷️ 태그 운영 원칙

| 분류 | 목적 | 예시 태그 |
|------|------|------------|
| **공통 시리즈 식별용** | 시리즈 간 일관성 유지 | `Verilog_Study_Series` |
| **기술적 주제 구분용** | 회로 설계, 언어별 키워드 | `CombinationalLogic`, `SequentialLogic`, `Blocking`, `Nonblocking` |
| **검색 친화용(한글)** | 블로그 내 검색 및 독자 접근성 향상 | `조합회로`, `순차회로`, `블로킹논블로킹` |
| **영문 기술 태그** | 해외 독자 대비, 문서화용 | `LogicDesign`, `Verilog` |

---

## 🧩 운영 규칙 정리

1. **모든 기술 시리즈 글에는 `Verilog_Study_Series` 태그를 공통으로 부여.**  
2. **글 카테고리는 항상 “디지털 설계 / Fundamentals”부터 시작.**  
   - 실제 설계 예제나 구현 중심이면 “Application”으로 이동.  
3. **글 말미에는 다음 주제 예고 문장을 반드시 추가.**  
4. **글 내부는 가능한 한 개념 → 코드 → 정리 순서로 구성.**  
5. **한글 태그는 블로그 검색용, 영문 태그는 정리·연결용으로 병행.**
