MindAR + HTML AR 보물찾기 스타터
=================================

구성
----
1) index.html
   - 내 사진 A를 인식하는 실제 프로젝트용
   - ./targets.mind 파일을 필요로 함
   - 사진 A를 찾으면 ./assets/A_1.svg 가 AR로 나타남
   - A_1을 터치하면 퀴즈
   - 정답이면 점수 +10 / 진행률 1/1 / 다음 힌트 표시

2) demo.html
   - MindAR 공식 샘플 target(.mind)을 사용
   - 구조 확인용
   - HTTPS 서버에 올린 뒤 스마트폰에서 테스트

3) assets/A_1.svg
   - 임시 캐릭터 이미지
   - 원하는 PNG/JPG/SVG로 교체 가능


내 사진 A로 바꾸는 방법
----------------------
[1] 사진 A 준비
- JPG/PNG 권장
- 글자, 무늬, 대비가 충분하고 특징점이 많은 이미지가 좋음
- 흰 벽, 단색 문, 비슷한 복도 사진은 인식률이 낮을 수 있음

[2] targets.mind 만들기
MindAR Target Compiler:
https://hiukim.github.io/mind-ar-js-doc/tools/compile/

- 사진 A 업로드
- Compile
- targets.mind 다운로드
- index.html과 같은 폴더에 저장

폴더 구조:
mindar_treasure_starter/
  index.html
  targets.mind
  assets/
    A_1.svg

[3] A_1 이미지 바꾸기
- assets/A_1.svg 대신 assets/A_1.png 등을 넣어도 됨
- index.html의 아래 부분을 수정:
  <img id="overlayA1" src="./assets/A_1.svg" ...>

[4] 문제/정답/힌트 바꾸기
index.html 하단의 GAME 설정:
const GAME = {
  totalMissions: 1,
  pointsPerMission: 10,
  correctAnswer: "AI",
  nextHint: "다음 장소는 책이 가장 많은 곳입니다."
};

문제 문장은 id="questionText" 부분,
선택지는 data-answer="..." 부분에서 수정.

[5] 실행
카메라 사용 때문에 실제 스마트폰 테스트는 HTTPS 주소에서 실행하는 것을 권장.
예: GitHub Pages / Netlify / Vercel 등 정적 웹 호스팅.

중요
----
- index.html을 PC에서 더블클릭하는 것만으로는 스마트폰 카메라 테스트가 제대로 되지 않을 수 있음.
- targets.mind 안에서 첫 번째로 컴파일한 이미지 = targetIndex 0 = 사진 A
- 여러 사진(A/B/C...)으로 확장하려면 한 번에 여러 이미지를 컴파일하고
  targetIndex 0, 1, 2... 를 각각 연결하면 됨.
