# Mealboard_Demo

학교 급식실 대기시간 + 급식 영양 대시보드.

## 0. 현재 상태 (2026-08)
- 홈 Pi 5 = 스테이징. 카메라 없음 → `mealboard-vision` 미설치, `mealboard-mock` 이 대역.
  로드맵 ④는 개발 PC 웹캠·동영상 파일로, ⑤의 `calibrate` 는 학교 Pi 이전 시.
- PI_HOST 는 Tailscale 주소 (.env 참조). 공용 체크아웃 `/opt/mealboard` — Pi 에서 직접 편집 금지, `git pull` 만.
- 같은 Pi 에 Plant 프로젝트(`~/plant/`, planthub·plantdash·plantsnap 유닛) 가 정지 상태로 공존.
  `~/plant/` 와 그 DB 에는 어떤 이유로도 접근·수정하지 않는다. 포트 8000·8501·1883 은 Plant 소유.
- API 포트는 8100 (.env `API_PORT`). NEIS 갱신은 systemd timer 05:40.
- 영양 지표는 코사인 유사도가 아니라 에너지 충족률 · 에너지 적정비율 · MAR 세 가지 (`jobs/fetch_neis.py` 참조).
- vision 프레임 소스는 `webcam|file|picamera` 로 추상화. 홈 Pi 에서는 picamera 를 쓰지 않는다 (Plant 카메라 타이머와 배터...)
