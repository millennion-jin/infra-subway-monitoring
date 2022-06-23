<p align="center">
    <img width="200px;" src="https://raw.githubusercontent.com/woowacourse/atdd-subway-admin-frontend/master/images/main_logo.png"/>
</p>
<p align="center">
  <img alt="npm" src="https://img.shields.io/badge/npm-%3E%3D%205.5.0-blue">
  <img alt="node" src="https://img.shields.io/badge/node-%3E%3D%209.3.0-blue">
  <a href="https://edu.nextstep.camp/c/R89PYi5H" alt="nextstep atdd">
    <img alt="Website" src="https://img.shields.io/website?url=https%3A%2F%2Fedu.nextstep.camp%2Fc%2FR89PYi5H">
  </a>
  <img alt="GitHub" src="https://img.shields.io/github/license/next-step/atdd-subway-service">
</p>

<br>

# 인프라공방 샘플 서비스 - 지하철 노선도

<br>

## 🚀 Getting Started

### Install
#### npm 설치
```
cd frontend
npm install
```
> `frontend` 디렉토리에서 수행해야 합니다.

### Usage
#### webpack server 구동
```
npm run dev
```
#### application 구동
```
./gradlew clean build
```
<br>


### 1단계 - 웹 성능 테스트
1. 웹 성능예산은 어느정도가 적당하다고 생각하시나요

경쟁사 사이트들의 웹 성능을 테스트해본 결과

| \            | FCP | TTI | SI  | TBT(ms) | LCP |
|--------------|-----|-----|-----|---------|-----|
| 서울교통공사(모바일)  | 6.4 | 8.8 | 8.5 | 1140    | 6.6 |
| 네이버지도(모바일)   | 2.2 | 5.8 | 5.2 | 260     | 7.8 |
| 카카오맵(모바일)    | 1.7 | 4.1 | 7.3 | 40      | 6.4 |
| 서울교통공사(데스크탑) | 1.5 | 2.0 | 3.6 | 220     | 3.6 |
| 네이버지도(데스크탑)  | 0.5 | 0.5 | 2.1 | 0       | 1.6 |
| 카카오맵(데스크탑)   | 0.5 | 0.7 | 2.2 | 0       | 1.3 |

위의 결과를 확인해본 결과<br>
서울교통공사는 관공서 사이트 답게 타 사이트들에 비하여 압도적으로 느린것을 확인 할 수 있었습니다.<br>
이에 서울교통공사 사이트는 참조 표본에서 제외하기로 하였습니다.<br>
주요 성능목표로 잡은 FCP, TTI, LCP 의 측정치를 확인해본 결과<br>
카카오맵이 네이버지도에 비하여 속도가 빠른 것을 확인할 수 있었으며<br>
새롭게 시장에 진입하는 후발주자로서 타 시스템에 비하여 속도가 느린것은 마이너스 요소가 될 수 있기에<br>
카카오맵과 동일한 수준의 속도를 목표치로 설정하기로 하였습니다.


| \                                         | FCP  | TTI  | SI   | TBT(ms) | LCP  |
|-------------------------------------------|------|------|------|---------|------|
| https://subway-testing.kro.kr(모바일 - 측정치)  | 14.9 | 15.5 | 14.9 | 600     | 15.5 |
| https://subway-testing.kro.kr(모바일 - 목표치)  | 1.7  | 4.1  | 7.3  | 40      | 6.4  |
| https://subway-testing.kro.kr(데스크탑 - 측정치) | 2.6  | 2.7  | 2.6  | 40      | 2.7  |
| https://subway-testing.kro.kr(데스크탑 - 목표치)  | 0.5  | 0.7  | 2.2  | 0       | 1.3  |

이에 위와 같은 목표치를 잡게되었습니다.
<br>
<br>

2. 웹 성능예산을 바탕으로 현재 지하철 노선도 서비스는 어떤 부분을 개선하면 좋을까요
- FCP 측정치가 목표치에 비하여 현저하게 느린 것을 확인
  - gzip 압축 등의 적용이 필요
- 모바일에서의 SI 측정치가 목표치에 비해 많이 느린 것을 확인 
  - 지연로딩을 사용하여 렌더링 차단 리소스 제거하기
- LCP 측정치 또한 목표치에 비하여 많이 느린 것을 확인 
  - 컨텐츠를 압축하여 네트워크 비용을 줄일 필요가 있음


---

### 2단계 - 부하 테스트 
1. 부하테스트 전제조건은 어느정도로 설정하셨나요

2. Smoke, Load, Stress 테스트 스크립트와 결과를 공유해주세요

---

### 3단계 - 로깅, 모니터링
1. 각 서버내 로깅 경로를 알려주세요

2. Cloudwatch 대시보드 URL을 알려주세요
