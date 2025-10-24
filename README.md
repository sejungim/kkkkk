<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>🎉 빙고 게임</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 20px;
      color: #333;
    }

    .container {
      background: white;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
      text-align: center;
      max-width: 550px;
      width: 100%;
    }

    h1 {
      color: #4a4a4a;
      margin-bottom: 10px;
      font-size: 2.2rem;
    }

    .subtitle {
      color: #666;
      margin-bottom: 25px;
      font-size: 1rem;
    }

    .controls {
      display: flex;
      gap: 15px;
      align-items: center;
      justify-content: center;
      margin-bottom: 25px;
      flex-wrap: wrap;
    }

    button {
      background: #ff6b6b;
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 50px;
      cursor: pointer;
      font-weight: bold;
      transition: all 0.3s ease;
      box-shadow: 0 4px 10px rgba(255, 107, 107, 0.3);
    }

    button:hover {
      background: #ff5252;
      transform: translateY(-2px);
      box-shadow: 0 6px 15px rgba(255, 107, 107, 0.4);
    }

    .stats {
      display: flex;
      justify-content: space-around;
      background: #f8f9fa;
      padding: 12px;
      border-radius: 12px;
      margin-bottom: 20px;
      font-weight: bold;
    }

    .stat-item span {
      display: block;
      font-size: 1.8rem;
      color: #ff6b6b;
    }

    /* 빙고 판 */
    .bingo-board {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 8px;
      max-width: 500px;
      margin: 0 auto;
      padding: 10px;
      background: #f1f3f4;
      border-radius: 15px;
    }

    .cell {
      aspect-ratio: 1 / 1;
      display: flex;
      align-items: center;
      justify-content: center;
      background: white;
      border-radius: 12px;
      font-size: 1.4rem;
      font-weight: bold;
      cursor: pointer;
      user-select: none;
      transition: all 0.2s ease;
      box-shadow: 0 3px 8px rgba(0,0,0,0.1);
    }

    .cell:hover {
      transform: scale(1.05);
      box-shadow: 0 5px 15px rgba(0,0,0,0.15);
    }

    .cell.marked {
      background: #ffd166;
      color: #1a1a1a;
      transform: scale(0.95);
      box-shadow: inset 0 0 0 3px #ff9e00;
    }

    /* 중앙 FREE 칸 */
    .cell.free {
      background: #06d6a0;
      color: white;
      font-weight: bold;
      cursor: default;
    }

    .cell.free:hover {
      transform: none;
      box-shadow: 0 3px 8px rgba(0,0,0,0.1);
    }

    /* 완성된 줄 강조 */
    .bingo-line {
      background: #ff9e00 !important;
      color: white !important;
      animation: bingoFlash 1.5s infinite alternate;
    }

    @keyframes bingoFlash {
      0% { box-shadow: 0 0 0 4px rgba(255, 158, 0, 0.6); }
      100% { box-shadow: 0 0 0 8px rgba(255, 158, 0, 0.3); }
    }

    /* 완료 메시지 */
    .bingo-message {
      margin-top: 20px;
      font-size: 1.3rem;
      font-weight: bold;
      color: #06d6a0;
      height: 28px;
    }

    footer {
      margin-top: 30px;
      color: rgba(255,255,255,0.8);
      font-size: 0.9rem;
      text-align: center;
    }

    /* 반응형 */
    @media (max-width: 500px) {
      .container { padding: 20px; }
      h1 { font-size: 1.8rem; }
      .cell { font-size: 1.1rem; }
      button { padding: 10px 20px; font-size: 0.95rem; }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🎯 빙고 게임</h1>
    <p class="subtitle">숫자를 클릭해 체크! 가로/세로/대각선 5개 완성 시 빙고!</p>

    <div class="controls">
      <button id="newGameBtn">새 게임 시작</button>
      <div>클릭한 칸이 초록색으로 변합니다</div>
    </div>

    <div class="stats">
      <div class="stat-item">
        <span id="bingoCount">0</span>
        <div>빙고 개수</div>
      </div>
      <div class="stat-item">
        <span id="clickedCount">0</span>
        <div>클릭 수</div>
      </div>
      <div class="stat-item">
        <span id="linesCompleted">0</span>
        <div>완성 라인</div>
      </div>
    </div>

    <div class="bingo-board" id="bingoBoard"></div>

    <div class="bingo-message" id="bingoMessage"></div>
  </div>

  <footer>
    Made with HTML, CSS, JS | © 2024 Bingo Game
  </footer>

  <script>
    const boardSize = 5;
    const totalCells = boardSize * boardSize;
    let numbers = [];
    let marked = Array(totalCells).fill(false);
    let bingoLines = []; // 완성된 라인 저장 (중복 방지)

    const boardEl = document.getElementById('bingoBoard');
    const newGameBtn = document.getElementById('newGameBtn');
    const bingoCountEl = document.getElementById('bingoCount');
    const clickedCountEl = document.getElementById('clickedCount');
    const linesCompletedEl = document.getElementById('linesCompleted');
    const bingoMessageEl = document.getElementById('bingoMessage');

    // 중앙 FREE 칸 인덱스 (0-based, 2,2 -> index 12)
    const FREE_INDEX = 12;

    function generateNumbers() {
      // 1~25 중복 없이 섞기
      const arr = Array.from({ length: 25 }, (_, i) => i + 1);
      for (let i = arr.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [arr[i], arr[j]] = [arr[j], arr[i]];
      }
      // FREE 칸은 항상 중앙에 "FREE" 표시
      arr[FREE_INDEX] = "FREE";
      return arr;
    }

    function createBoard() {
      boardEl.innerHTML = '';
      numbers = generateNumbers();
      marked.fill(false);
      marked[FREE_INDEX] = true; // FREE는 처음부터 체크됨
      bingoLines = [];
      updateStats();
      bingoMessageEl.textContent = '';

      numbers.forEach((num, index) => {
        const cell = document.createElement('div');
        cell.classList.add('cell');
        cell.dataset.index = index;
        cell.textContent = num;

        if (index === FREE_INDEX) {
          cell.classList.add('free', 'marked');
        } else {
          cell.addEventListener('click', () => toggleCell(index, cell));
        }

        boardEl.appendChild(cell);
      });
    }

    function toggleCell(index, cellEl) {
      if (index === FREE_INDEX) return;

      marked[index] = !marked[index];
      if (marked[index]) {
        cellEl.classList.add('marked');
      } else {
        cellEl.classList.remove('marked');
      }

      checkBingo();
      updateStats();
    }

    function checkBingo() {
      const lines = [];

      // 가로
      for (let row = 0; row < boardSize; row++) {
        const line = [];
        for (let col = 0; col < boardSize; col++) {
          line.push(row * boardSize + col);
        }
        lines.push(line);
      }

      // 세로
      for (let col = 0; col < boardSize; col++) {
        const line = [];
        for (let row = 0; row < boardSize; row++) {
          line.push(row * boardSize + col);
        }
        lines.push(line);
      }

      // 대각선 \
      lines.push([0,6,12,18,24]);
      // 대각선 /
      lines.push([4,8,12,16,20]);

      let completedThisTurn = 0;
      const newBingoLines = [];

      lines.forEach(line => {
        const isCompleted = line.every(idx => marked[idx]);
        if (isCompleted) {
          const lineKey = line.sort((a,b)=>a-b).join('-');
          if (!bingoLines.includes(lineKey)) {
            completedThisTurn++;
          }
          newBingoLines.push(lineKey);
        }
      });

      // 기존 라인 제거 스타일 초기화
      document.querySelectorAll('.cell').forEach(cell => {
        cell.classList.remove('bingo-line');
      });

      // 새로 완성된 라인이 있다면 강조
      if (completedThisTurn > 0) {
        const newlyCompleted = newBingoLines.filter(ln => !bingoLines.includes(ln));
        newlyCompleted.forEach(lineKey => {
          const idxs = lineKey.split('-').map(Number);
          idxs.forEach(idx => {
            const cell = boardEl.querySelector(`.cell[data-index="${idx}"]`);
            if (cell) cell.classList.add('bingo-line');
          });
        });

        bingoLines = [...new Set([...bingoLines, ...newBingoLines])];

        if (completedThisTurn > 0) {
          let msg = '';
          if (completedThisTurn === 1 && newBingoLines.length > bingoLines.length - completedThisTurn) {
            msg = '빙고! 🎉';
          } else if (completedThisTurn > 1) {
            msg = `${completedThisTurn}개의 빙고! 🥳`;
          }
          bingoMessageEl.textContent = msg;
          setTimeout(() => {
            if (msg) bingoMessageEl.textContent = ''; // 메시지 잠시 후 사라짐
          }, 2500);
        }
      }

      updateStats();
    }

    function updateStats() {
      const clicked = marked.filter((m, i) => i !== FREE_INDEX && m).length;
      clickedCountEl.textContent = clicked;
      linesCompletedEl.textContent = bingoLines.length;
      bingoCountEl.textContent = bingoLines.length;
    }

    // 초기화
    newGameBtn.addEventListener('click', createBoard);

    // 페이지 로드 시 게임 시작
    window.addEventListener('DOMContentLoaded', createBoard);
  </script>
</body>
</html>
```

---


---

필요하다면 **음성 효과 추가**, **다중 플레이어 모드**, **숫자 자동 호출 기능** 등을 확장할 수 있습니다. 원하시는 기능이 있다면 말씀해 주세요!
