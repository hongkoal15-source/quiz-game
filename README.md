<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>퀴즈 게임</title>
  <style>
    body { font-family: Arial, sans-serif; background:#111; color:#fff; text-align:center; }
    input, button { font-size:16px; padding:8px; }
    .box { max-width:500px; margin:40px auto; padding:20px; border:1px solid #444; border-radius:10px; }
  </style>
</head>
<body>
  <div class="box">
    <h1>퀴즈 게임</h1>
    <p id="question"></p>
    <input id="answer" placeholder="정답 입력 (서술형)" />
    <br><br>
    <button onclick="submitAnswer()">제출</button>
    <p id="result"></p>
    <p>점수: <span id="score">0</span></p>
    <p>연속 정답: <span id="combo">0</span></p>
    <p>등급: <span id="rank">나무</span></p>
  </div>

  <script>
    <script>
  const quiz = [
    { q: "대한민국의 수도는?", a: "서울" },
    { q: "지구에서 가장 큰 바다는?", a: "태평양" },
    { q: "1+1은?", a: "2" },
    { q: "태양계에서 가장 큰 행성은?", a: "목성" },
    { q: "한글을 만든 왕은?", a: "세종대왕" },
    { q: "물의 화학식은?", a: "H2O" },
    { q: "대한민국의 국기는?", a: "태극기" },
    { q: "지구는 몇 번째 행성인가?", a: "3" },
    { q: "피카츄는 어느 회사 캐릭터인가?", a: "닌텐도" },
    { q: "밤하늘에서 가장 밝은 별은?", a: "시리우스" },
    { q: "대한민국의 국화는?", a: "무궁화" },
    { q: "사람의 심장은 몇 개일까?", a: "1" },
    { q: "컴퓨터의 뇌 역할을 하는 부품은?", a: "CPU" },
    { q: "지구가 태양을 도는 데 걸리는 시간은?", a: "1년" },
    { q: "한국의 화폐 단위는?", a: "원" },
    { q: "바다의 물은 짠가 싱거운가?", a: "짠" },
    { q: "대한민국의 수도권에 포함되지 않는 도시는?", a: "부산" },
    { q: "사람은 보통 몇 개의 손가락을 가지고 있을까?", a: "10" },
    { q: "인터넷 주소에서 https의 의미는?", a: "보안" },
    { q: "게임에서 점수를 뜻하는 영어 단어는?", a: "score" }
  ];
</script>quiz.sort(() => Math.random() - 0.5);
    ];

    let score = 0;
    let combo = 0;
    let current = 0;

    function normalize(text) {
      return text.replace(/\s/g, "");
    }

    function getRank(s) {
      if (s >= 10000) return "신";
      if (s >= 1000) return "우주";
      if (s >= 300) return "방사능 물질";
      if (s >= 200) return "그랜드 핑크 다이아";
      if (s >= 150) return "블루 다이아";
      if (s >= 100) return "레드 다이아";
      if (s >= 66) return "다이아";
      if (s >= 50) return "플래티넘";
      if (s >= 30) return "골드";
      if (s >= 20) return "실버";
      if (s >= 10) return "브론즈";
      return "나무";
    }

    function loadQuestion() {
      document.getElementById("question").innerText = quiz[current].q;
      document.getElementById("answer").value = "";
    }

    function submitAnswer() {
      const user = normalize(document.getElementById("answer").value);
      const correct = normalize(quiz[current].a);

      if (user === correct) {
        combo++;
        score += combo;
        document.getElementById("result").innerText = `정답! +${combo}점`;
      } else {
        combo = 0;
        document.getElementById("result").innerText = "틀림!";
      }

      document.getElementById("score").innerText = score;
      document.getElementById("combo").innerText = combo;
      document.getElementById("rank").innerText = getRank(score);

      current = (current + 1) % quiz.length;
      loadQuestion();
    }

    loadQuestion();
  </script>
</body>
</html>
