<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>🖤⭕ 오목 게임 (Five in a Row)</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Apple SD Gothic Neo', 'Malgun Gothic', 'Segoe UI', sans-serif;
    }

    body {
      background: linear-gradient(135deg, #1e3c72, #2a5298);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
      color: #333;
    }

    .container {
      background: white;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
      text-align: center;
      max-width: 700px;
      width: 100%;
    }

    h1 {
      color: #2c3e50;
      margin-bottom: 10px;
      font-size: 2rem;
    }

    .subtitle {
      color: #7f8c8d;
      margin-bottom: 25px;
    }

    .controls {
      display: flex;
      gap: 15px;
      align-items: center;
      justify-content: center;
      margin-bottom: 20px;
      flex-wrap: wrap;
    }

    select, button {
      padding: 10px 16px;
      border-radius: 10px;
      border: 1px solid #ddd;
      font-size: 1rem;
      background: #f8f9fa;
      cursor: pointer;
      transition: all 0.2s;
    }

    button {
      background: #3498db;
      color: white;
      border: none;
      font-weight: bold;
      box-shadow: 0 4px 8px rgba(52, 152, 219, 0.3);
    }

    button:hover {
      background: #2980b9;
      transform: translateY(-1px);
    }

    button:disabled {
      background: #bdc3c7;
      cursor: not-allowed;
      transform: none;
      box-shadow: none;
    }

    .status {
      font-size: 1.3rem;
      font-weight: bold;
      margin: 15px 0;
      min-height: 32px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 10px;
    }

    .turn-indicator {
      display: inline-block;
      width: 24px;
      height: 24px;
      border-radius: 50%;
      background: #000;
      border: 3px solid #333;
    }

    .turn-indicator.white {
      background: #fff;
      border: 3px solid #ccc;
    }

    /* 오목판 */
    .board-container {
      position: relative;
      display: inline-block;
      background: #deb887; /* 나무 색감 */
      padding: 20px;
      border-radius: 15px;
      box-shadow: inset 0 0 20px rgba(0,0,0,0.2);
    }

    .board {
      display: grid;
      background: #deb887;
      position: relative;
      touch-action: manipulation;
    }

    /* 15x15 vs 19x19 크기 조정 */
    .board.size-15 {
      grid-template-columns: repeat(15, 1fr);
      width: 450px;
      height: 450px;
    }

    .board.size-19 {
      grid-template-columns: repeat(19, 1fr);
      width: 520px;
      height: 520px;
    }

    @media (max-width: 600px) {
      .board.size-15 { width: 300px; height: 300px; }
      .board.size-19 { width: 350px; height: 350px; }
    }

    .cell {
      position: relative;
      border: 1px solid rgba(0,0,0,0.05);
      cursor: pointer;
      user-select: none;
    }

    .cell::after {
      content: '';
      display: block;
      padding-bottom: 100%;
    }

    .stone {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 85%;
      height: 85%;
      border-radius: 50%;
      box-shadow: 0 2px 5px rgba(0,0,0,0.3);
    }

    .stone.black {
      background: radial-gradient(circle at 30% 30%, #555, #000);
      border: 2px solid #000;
    }

    .stone.white {
      background: radial-gradient(circle at 30% 30%, #fff, #eee);
      border: 2px solid #aaa;
    }

    /* 승리 선 그리기용 */
    .win-line {
      position: absolute;
      background: red;
      z-index: 10;
      transform-origin: 0 0;
    }

    .win-line.horizontal { height: 4px; }
    .win-line.vertical { width: 4px; }
    .win-line.diagonal { height: 4px; transform: rotate(45deg); }
    .win-line.diagonal2 { height: 4px; transform: rotate(-45deg); }

    footer {
      margin-top: 25px;
      color: rgba(255,255,255,0.7);
      font-size: 0.9rem;
    }

    .history-info {
      margin-top: 15px;
      color: #555;
      font-size: 0.9rem;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🖤⭕ 오목 게임 (Five in a Row)</h1>
    <p class="subtitle">흑백으로 5개를 연속으로 두면 승리! (가로/세로/대각선)</p>

    <div class="controls">
      <label>
        보드 크기:
        <select id="boardSize">
          <option value="15">15×15 (전통)</option>
          <option value="19">19×19 (전문)</option>
        </select>
      </label>
      <button id="newGameBtn">새 게임</button>
      <button id="undoBtn" disabled>취소 (Undo)</button>
    </div>

    <div class="status">
      <span>현재 차례:</span>
      <div class="turn-indicator" id="turnIndicator"></div>
      <span id="statusText">흑의 차례입니다</span>
    </div>

    <div class="board-container">
      <div class="board size-15" id="board"></div>
    </div>

    <div class="history-info">
      <span id="historyInfo">총 수: 0</span>
    </div>
  </div>

  <footer>
    HTML + CSS + JS로 제작 | © 2024 Omok Game
  </footer>

  <script>
    const boardEl = document.getElementById('board');
    const boardSizeSelect = document.getElementById('boardSize');
    const newGameBtn = document.getElementById('newGameBtn');
    const undoBtn = document.getElementById('undoBtn');
    const statusText = document.getElementById('statusText');
    const turnIndicator = document.getElementById('turnIndicator');
    const historyInfo = document.getElementById('historyInfo');

    let boardSize = 15;
    let boardState = []; // 2D 배열: null, 'black', 'white'
    let currentPlayer = 'black'; // 흑부터 시작
    let gameOver = false;
    let history = []; // { x, y, player } 저장
    let winLine = null; // { type, start, end }

    function initBoard() {
      boardState = Array(boardSize).fill(null).map(() => Array(boardSize).fill(null));
      gameOver = false;
      currentPlayer = 'black';
      history = [];
      winLine = null;
      updateStatus();
      renderBoard();
      undoBtn.disabled = true;
      clearWinLine();
    }

    function renderBoard() {
      boardEl.className = `board size-${boardSize}`;
      boardEl.innerHTML = '';
      for (let y = 0; y < boardSize; y++) {
        for (let x = 0; x < boardSize; x++) {
          const cell = document.createElement('div');
          cell.classList.add('cell');
          cell.dataset.x = x;
          cell.dataset.y = y;
          cell.addEventListener('click', onCellClick);
          cell.addEventListener('contextmenu', (e) => e.preventDefault()); // 우클릭 메뉴 방지

          const stone = boardState[y][x];
          if (stone) {
            const stoneEl = document.createElement('div');
            stoneEl.classList.add('stone', stone);
            cell.appendChild(stoneEl);
          }

          boardEl.appendChild(cell);
        }
      }

      // 승리 선 그리기
      if (winLine) {
        drawWinLine(winLine);
      }

      historyInfo.textContent = `총 수: ${history.length}`;
    }

    function onCellClick(e) {
      if (gameOver) return;

      const x = parseInt(e.currentTarget.dataset.x);
      const y = parseInt(e.currentTarget.dataset.y);

      if (boardState[y][x] !== null) return;

      // 수 둠
      boardState[y][x] = currentPlayer;
      history.push({ x, y, player: currentPlayer });
      undoBtn.disabled = false;

      // 승리 체크
      const result = checkWin(x, y, currentPlayer);
      if (result.win) {
        gameOver = true;
        winLine = result.line;
        statusText.textContent = `${currentPlayer === 'black' ? '흑' : '백'} 승리! 🎉`;
        renderBoard();
        return;
      }

      // 비김 체크 (보드 가득)
      if (history.length === boardSize * boardSize) {
        statusText.textContent = '무승부!';
        gameOver = true;
        return;
      }

      // 턴 전환
      currentPlayer = currentPlayer === 'black' ? 'white' : 'black';
      updateStatus();
      renderBoard();
    }

    function updateStatus() {
      turnIndicator.className = 'turn-indicator ' + (currentPlayer === 'white' ? 'white' : '');
      statusText.textContent = `${currentPlayer === 'black' ? '흑' : '백'}의 차례입니다`;
      historyInfo.textContent = `총 수: ${history.length}`;
    }

    // 5연속 검사 (네 방향: 가로, 세로, 대각 \ , 대각 / )
    function checkWin(x, y, player) {
      const directions = [
        { dx: 1, dy: 0 },  // horizontal
        { dx: 0, dy: 1 },  // vertical
        { dx: 1, dy: 1 },  // diagonal \
        { dx: 1, dy: -1 }  // diagonal /
      ];

      for (const dir of directions) {
        let count = 1; // 현재 위치 포함
        let line = [{x, y}];

        // 양방향 탐색
        for (let sign of [-1, 1]) {
          for (let step = 1; step <= 5; step++) {
            const nx = x + sign * step * dir.dx;
            const ny = y + sign * step * dir.dy;
            if (nx < 0 || ny < 0 || nx >= boardSize || ny >= boardSize) break;
            if (boardState[ny][nx] === player) {
              count++;
              line.push({x: nx, y: ny});
            } else {
              break;
            }
          }
        }

        if (count >= 5) {
          // 정확히 연속된 5개의 선 추출
          const sortedLine = line.sort((a,b) => a.x - b.x || a.y - b.y);
          // 실제 5연속 구간 찾기 (가장 긴 연속 중 첫 5개 이상)
          const winSeq = extractFiveInLine(sortedLine, dir, player);
          return { win: true, line: { type: getDirectionName(dir), cells: winSeq } };
        }
      }

      return { win: false };
    }

    function extractFiveInLine(points, dir, player) {
      // 단순화: points에서 연속된 5개를 찾아 반환 (실제론 중복될 수 있으나 여기선 최초 발견 5개)
      // 방향에 따라 정렬 후 연속 5개 슬라이스
      if (dir.dx === 1 && dir.dy === 0) {
        points.sort((a,b) => a.x - b.x);
      } else if (dir.dx === 0 && dir.dy === 1) {
        points.sort((a,b) => a.y - b.y);
      } else if (dir.dx === 1 && dir.dy === 1) {
        points.sort((a,b) => a.x - b.x);
      } else if (dir.dx === 1 && dir.dy === -1) {
        points.sort((a,b) => a.x - b.x);
      }

      // 연속된 5개 조합 탐색 (최초 발견된 5개)
      for (let i = 0; i <= points.length - 5; i++) {
        const slice = points.slice(i, i+5);
        if (isConsecutive(slice, dir)) {
          return slice;
        }
      }

      // 길이가 5보다 클 경우에도 처리
      // 간단하게 처음 5개 반환 (실제 게임에서는 드물지만)
      return points.slice(0,5);
    }

    function isConsecutive(arr, dir) {
      arr.sort((a,b) => a.x - b.x || a.y - b.y);
      for (let i = 1; i < arr.length; i++) {
        const dx = arr[i].x - arr[i-1].x;
        const dy = arr[i].y - arr[i-1].y;
        if (dx !== dir.dx || dy !== dir.dy) return false;
      }
      return true;
    }

    function getDirectionName(dir) {
      if (dir.dx === 1 && dir.dy === 0) return 'horizontal';
      if (dir.dx === 0 && dir.dy === 1) return 'vertical';
      if (dir.dx === 1 && dir.dy === 1) return 'diagonal';
      if (dir.dx === 1 && dir.dy === -1) return 'diagonal2';
      return 'horizontal';
    }

    function drawWinLine(line) {
      if (!line || !line.cells || line.cells.length < 5) return;

      const first = line.cells[0];
      const last = line.cells[line.cells.length - 1];

      const boardRect = boardEl.getBoundingClientRect();
      const cellWidth = boardRect.width / boardSize;
      const cellHeight = boardRect.height / boardSize;

      const lineEl = document.createElement('div');
      lineEl.classList.add('win-line', line.type);

      const padding = 20; // board-container의 padding
      const offsetX = boardEl.offsetLeft + padding;
      const offsetY = boardEl.offsetTop + padding;

      if (line.type === 'horizontal') {
        const y = first.y * cellHeight + cellHeight/2 + padding;
        lineEl.style.top = `${y}px`;
        lineEl.style.left = `${first.x * cellWidth + cellWidth/2 + padding}px`;
        lineEl.style.width = `${(last.x - first.x) * cellWidth}px`;
        lineEl.style.transform = 'none';
      } else if (line.type === 'vertical') {
        const x = first.x * cellWidth + cellWidth/2 + padding;
        lineEl.style.left = `${x}px`;
        lineEl.style.top = `${first.y * cellHeight + cellHeight/2 + padding}px`;
        lineEl.style.height = `${(last.y - first.y) * cellHeight}px`;
      } else if (line.type === 'diagonal') {
        const x = first.x * cellWidth + cellWidth/2 + padding;
        const y = first.y * cellHeight + cellHeight/2 + padding;
        lineEl.style.left = `${x}px`;
        lineEl.style.top = `${y}px`;
        lineEl.style.width = `${Math.hypot((last.x - first.x)*cellWidth, (last.y - first.y)*cellHeight)}px`;
        lineEl.style.transform = 'rotate(45deg)';
        lineEl.style.transformOrigin = '0 0';
      } else if (line.type === 'diagonal2') {
        const x = last.x * cellWidth + cellWidth/2 + padding; // 끝점부터 시작 (왼쪽 위 기준)
        const y = first.y * cellHeight + cellHeight/2 + padding;
        lineEl.style.left = `${x}px`;
        lineEl.style.top = `${y}px`;
        lineEl.style.width = `${Math.hypot((last.x - first.x)*cellWidth, (first.y - last.y)*cellHeight)}px`;
        lineEl.style.transform = 'rotate(-45deg)';
        lineEl.style.transformOrigin = '0 0';
      }

      boardEl.parentElement.appendChild(lineEl);
    }

    function clearWinLine() {
      const prev = boardEl.parentElement.querySelector('.win-line');
      if (prev) prev.remove();
    }

    // Undo 기능
    undoBtn.addEventListener('click', () => {
      if (history.length === 0 || gameOver) return;
      const lastMove = history.pop();
      boardState[lastMove.y][lastMove.x] = null;
      currentPlayer = lastMove.player; // 이전 플레이어로 되돌림
      if (history.length === 0) undoBtn.disabled = true;
      updateStatus();
      clearWinLine();
      renderBoard();
    });

    // 새 게임
    newGameBtn.addEventListener('click', () => {
      boardSize = parseInt(boardSizeSelect.value);
      initBoard();
    });

    boardSizeSelect.addEventListener('change', () => {
      boardSize = parseInt(boardSizeSelect.value);
      initBoard();
    });

    // 초기화
    window.addEventListener('DOMContentLoaded', () => {
      initBoard();
    });
  </script>
</body>
</html>
