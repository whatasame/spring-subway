# 지하철 노선도

## 진행 방법

* 지하철 노선도 요구 사항을 파악한다.
* 요구 사항에 대한 구현을 완료한 후 자신의 Github 아이디에 해당하는 브랜치에 Pull request를 통해 코드 리뷰 요청을 한다.
* 코드 리뷰 피드백에 대한 개선 작업을 하고 다시 Push한다.
* 모든 피드백을 완료하면 다음 단계를 도전하고 앞의 과정을 반복한다.

## 페어 프로그래밍

### 목표

* 서승훈: 즐기면서 하자
* 최정규: 모든걸 의심하자

### 규칙

* 잡담을 많이 하자
* 시간적 압박 등의 부담 없이 하자
* 너무 완벽하려고 하지 말자
* 고민이 길어지면 가위바위보로 정하자

## 용어 사전

| 한글명 | 영문      |
|-----|---------|
| 역   | Station |
| 구간  | Section |
| 노선  | Line    |

## 요구 사항

### ConnectedSections

- [x] 구간은 최소 하나 이상 있어야 한다.
- [x] 구간들은 모두 같은 노선이어야한다.
- [x] 구간들은 서로 이어져있어야한다.
- [x] 구간들을 상행 종점역부터 하행 종점역까지의 순서로 저장한다.
- [x] 구간을 추가할 수 있다.
    - [x] 새로운 구간의 모든 역이 이미 기존 구간에 있으면 추가할 수 없다.
    - [x] 새로운 구간의 역 중 하나는 기존 구간에 존재해야한다.
    - [x] 상행 종점역 앞에 구간을 추가한다.
    - [x] 하행 종점역 뒤에 구간을 추가한다.
    - [x] 기존 구간의 사이에 구간을 추가한다.
        - [x] 추가하는 구간은 기존 구간보다 짧아야한다.
        - [x] 기존 구간의 상행역 뒤에 구간을 추가한다.
        - [x] 기존 구간의 하행역 앞에 구간을 추가한다.
- [x] 구간을 삭제할 수 있다.
    - [x] 구간이 하나인 경우 삭제할 수 없다.
    - [x] 하행 종점역을 포함하는 구간만 삭제할 수 있다.

### Station

- [x] 하나의 역은 하나의 StationName을 갖는다.
- [x] 서로 다른 역의 역 이름이 같으면 서로 같다.

### StationName

- [x] 역 이름은 반드시 존재해야한다.
- [x] 역 이름은 한 글자 이상이어야한다.
- [x] 역 이름이 같으면 같다.

### Distance

- [x] 거리는 0보다 길어야한다.
- [x] 거리 값이 같으면 같다.
- [x] 거리끼리 더할 수 있다.
- [x] 거리끼리 뺄 수 있다.
    - [x] 뺄 거리가 더 긴 경우 뺄 수 없다.

### 1단계

- [x] 구간에 대한 도메인을 정의한다.
    - [x] 구간은 **상행 역의 정보**와 **하행 역의 정보**를 갖는다.
    - [x]  상행 역과 하행 역 중 하나 이상 없을 경우 정의할 수 없다.
    - [x] 상행 역과 하행 역 사이의 **길이 정보**를 갖는다.
- [x] 구간 등록 기능
    - [x] 노선에 새로운 구간을 등록할 수 있다. 단, 아래 조건을 만족해야한다. 그렇지 않으면 예외를 던진다.
        - [x] 새로운 구간의 상행역은 해당 노선에 등록되어 있는 하행 종점역이어야 한다.
        - [x] 새로운 구간의 하행역은 해당 노선에 등록되어 있는 역일 수 없다.
- [x] 구간 제거 기능
    - [x] 노선에 존재하는 구간을 제거할 수 있다. 단, 아래 조건을 만족해야한다. 그렇지 않으면 예외를 던진다.
        - [x] 지하철 노선에 등록된 하행 종점역만 제거할 수 있다.
        - [x] 지하철 노선에 구간이 하나인 경우 역을 제거할 수 없다.

### 2단계

- [x] 구간 추가 기능 심화
    - [x] 노선 조회 시 상행 종점역부터 하행 종점역까지 순서대로 응답한다.
    - [x] 역 사이에 새로운 역을 등록할 수 있다.
        - [x] 요청의 상행역과 노선에 속한 구간의 상행역이 같고, 요청의 하행역이 해당 노선에 존재하지 않는 경우 해당 구간의 사이에 등록한다.
        - [x] 요청의 하행역과 노선에 속한 구간의 하행역이 같고, 요청의 상행역이 해당 노선에 존재하지 않는 경우 해당 구간의 사이에 등록한다.
    - [x] 새로운 역을 상행 종점역으로 등록할 수 있다.
        - [x] 요청의 하행역과 노선의 상행 종점역이 같고, 요청의 상행역이 해당 노선에 존재하지 않는 경우, 상행 종점역으로 등록한다.
    - [x] 새로운 역을 하행 종점역으로 등록할 수 있다.
        - [x] 요청의 상행역과 노선의 하행 종점역이 같고, 요청의 하행역이 해당 노선에 존재하지 않는 경우, 하행 종점역으로 등록한다.
    - [x] 예외 케이스
        - [x] 역 사이에 새로운 역을 등록할 경우 기존 역 사이 길이보다 크거나 같으면 등록할 수 없다.
        - [x] 상행 역과 하행 역이 이미 노선에 모두 등록되어 있다면 추가할 수 없다.
        - [x] 상행 역과 하행 역 둘 다 포함되어 있지 않으면 추가할 수 없다.

### 3단계

- [x] 구간 삭제 기능 심화
    - [x] 노선에 구간이 하나인 경우 구간을 삭제할 수 없다.
    - [x] 삭제하려는 역은 전체 구간에 존재하는 역이어야한다.
    - [x] 상행 종점 역을 포함하는 구간을 삭제할 수 있다.
    - [x] 하행 종점 역을 포함하는 구간을 삭제할 수 있다.
    - [x] 서로 다른 역 사이의 중간역을 포함하는 구간을 삭제할 수 있다.
        - [x] 중간역 삭제에 성공하면 서로 다른 역 사이를 잇는 노선으로 합쳐진다.

### 4단계

- [x] 경로 명세
    - [x] 경로는 출발 역에서 도착 역까지의 구간의 모음을 말한다.
    - [x] 최단 경로는 구간 길이의 합이 가장 짧은 경로를 말한다.
    - [x] 최단 경로는 출발역, 지나치는 역, 도착역, 경로 길이 정보를 가진다.

- [ ] 경로 조회 기능
    - [ ] 경로 조회에 대한 컨트롤러를 만든다.
    - [x] 특정 역에서 출발하여 특정 역에 도착하는 최단 경로를 구할 수 있다.
        - [x] 출발 역과 도착 역이 같을수 없다
        - [x] 출발 역과 도착 역 모두 존재해야한다.
        - [x] 출발 역과 도착 역은 연결되어 있어야 한다.
