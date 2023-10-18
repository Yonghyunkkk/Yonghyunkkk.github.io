---
title: "[운영체제와 정보기술의 원리] 6장. CPU Scheduling"
date: 2023-10-18
categories: [CS, Algorithm]
tags: [Algorithm]
---

## CPU Scheduling

기계어 명령은 크게 CPU내에서 수행되는 명령, 메모리 접근을 필요로 하는 명령, 입출력을 동반하는 명령으로 나눌 수 있다.

1. Register 간의 연산으로 구성되는 ADD (명령): CPU Burst
2. 메모리에 접근하는 load / store (명령): CPU Burst
3. I/O (명령): I/O Burst

여기서 CPU를 직접 가지고 빠른 명령을 수행하는 작업을 ***CPU BURST***라 하고, I/O와 관련된 작업을 ***I/O BURST***라고 한다. 

이와 같은 기준에서 프로세스를 두 가지 종류로 나눌 수 있다. 

1. **CPU Bound Process:** CPU burst가 길게 나타나는 프로세스.
2. **I/O Bound Process:** CPU burst가 짧게 나타나는 프로세스.

***I/O Bound Process***는 주로 사용자로부터 인터랙션을 계속해서 받아가며 프로그램을 수행시키는 **대화형 프로그램(interactive program)**에 해당하고, ***CPU Bound Process***는 CPU 작업에 소모하는 계산 위주의 프로그램에 해당된다.

따라서 CPU 스케줄링을 할 때 CPU Bound Process 인지 아니면 I/O Bound Process인지에 따라서 다른 CPU 스케줄링을 사용하는 것이 바람직하다.

## CPU Scheduler

***CPU Scheduler***는 타이머 인터럽트가 발생 시, ready queue에서 CPU를 기다리는 프로세스 중 하나를 선택해 CPU를 할당하게 된다.

CPU 스케줄링 방식에는 두 가지 경우가 있다.

1. **비선점형 (nonpreemptive):**
  - CPU를 획득한 프로세스가 CPU를 반납하기 전까지는 CPU를 빼앗을 수 없다.
3. **선점형 (preemptive):**
  - 다른 프로세스가 CPU를 빼앗을 수 있다.

## Dispatcher

***Dispatcher***는 새롭게 선택된 프로세스가 CPU를 할당받고 작업을 수행 할 수 있도록 하는 운영체제의 코드이다.

여기서 하나의 프로세스를 정지시키고 다른 프로세스에게 CPU를 전달하기까지 걸리는 시간을 **디스패치 지연시간 (dispatch latency)** 이라고 한다. (also known as context switch overhead)

## 스케줄링의 성능 평가

스케줄링 기법의 성능을 평가하기 위해 여러 지표들이 사용하는데, 크게 5가지로 나누어볼 수 있다.

1. **이용률 (cpu utilization):**
  - 전체 시간 중에서 cpu 가 일을 한 시간. (not being idle)
2. **처리량 (throughput):**
  - 주어진 시간 동안 준비 큐에서 기다리고 있는 프로세스 중 몇 개를 끝마쳤는지.
3. **소요시간 (turnaround time):**
  - 준비큐에서 기다린 시간과 cpu burst가 끝나기까지 걸린 시간.
4. **대기시간 (waiting time):**
  - 프로세스가 cpu를 얻기 위해 기다린 시간의 합.
5. **응답시간 (response time):**
  - 프로세스가 준비큐에 들어온 후 첫 번째 cpu를 획득하기까지 기다린 시간.

## 스케줄링 알고리즘

1. **선입선출 스케줄링 (First-Come First-Served: FCFS):**
  - 비선점형 방식 (nonpreemptive).
  - 말 그대로 준비큐에 먼저 온 프로세스에게 cpu를 할당하는 방식.
  - 공평하나 평균 대기시간이 엄청 길어 질 수가 있다.
  - cpu burst가 긴 하나의 프로세스 때문에 cpu burst가 짧은 프로세스들이 모두 기다려야 한다 (convoy effect).
2. **최단작업우선 스케줄링 (Shortest-Job First: SJF):**
  - 비선점형 방식 (nonpreemptive).
  - cpu burst가 가장 짧은 프로세스에게 제일 먼저 cpu를 할당하는 방식.
  - **starvation**이 일어날 수도 있다 (cpu burst시간이 긴 프로세스가 기다리고 있는데 그 사이, 계속해서 burst시간이 짧은 프로세스들이 준비큐에 들어오는 경우).
3. **Shortest Remaining Time First (SRTF):**
  - 선점형 방식 (preemptive).
  - 준비큐에 들어온 프로세스의 cpu burst가 현재 실행되고 있는 cpu burst보다 짧으면 준비큐에 들어온 프로세스로 대체된다.
  - 평균대기시간을 가장 많이 줄일 수 있는 방식이다.
4. **우선순위 스케줄링 (Priority Scheduling):**
  - 선점형과 비선점형 둘 다 구현 할 수 있다.
  - 우선순위가 가장 높은 프로세스에게 먼저 cpu를 할당한다 (priority number).
  - 마찬가지로 **starvation**현상이 일어난다.
  - **aging**을 사용하여 프로세스의 우선순위를 조금씩 높여, starvation 현상을 해결 할 수 있다.
5. **라운드 로빈 스케줄링 (Round Robin Scheduling):**
  - 할당시간 (time quantum)을 사용하여 각 프로세스가 cpu를 사용할 수 있는 시간을 제한한다.
  - 할당시간이 너무 짧아서도 안되고 너무 길어서도 안된다.
  - 공평하면서도 cpu busrt시간이 짧은 프로세스가 빨리 cpu를 얻을 수 있도록 한다. 
