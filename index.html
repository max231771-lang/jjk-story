HTML
<!DOCTYPE html>
<html>
<head>
    <title>JJK Story Game</title>
    <style>
        body { margin: 0; background: black; display: flex; justify-content: center; align-items: center; height: 100vh; color: white; font-family: sans-serif; }
        canvas { border: 2px solid #444; background: #111; }
        #ui-layer { position: absolute; top: 20px; left: 20px; pointer-events: none; }
    </style>
</head>
<body>

    <div id="title-screen">
        <h1>JJK Story</h1>
        <button id="start-button">Start Game</button>
    </div>

    <canvas id="game-canvas" width="640" height="480"></canvas>

    <script src="game.js"></script>
</body>
</html>
const canvas = document.getElementById('game-canvas');
const ctx = canvas.getContext('2d');
const titleScreen = document.getElementById('title-screen');
const startButton = document.getElementById('start-button');

const tileSize = 32;
const gridWidth = 20;
const gridHeight = 15;
let keys = {};
let gameStarted = false;
let gameState = 'explore';

let player = {
  x: 9,
  y: 7,
  color: '#f8c230',
  hp: 20,
  maxHp: 20,
  technique: 7,
  defending: false,
};

const tileMap = [
  '####################',
  '#...........C......#',
  '#....TTT....TTT....#',
  '#...T...T...T......#',
  '#....TTT....TTT.....#',
  '#..................#',
  '#..C......###......#',
  '#......#####...C...#',
  '#...TTT..#...#.....#',
  '#...T....#...#.....#',
  '#...TTT..#####.....#',
  '#.........S........#',
  '#....P.............#',
  '#...........C......#',
  '####################',
];

const tiles = {
  '#': { color: '#283646', walkable: false },
  '.': { color: '#4b5c85', walkable: true },
  'T': { color: '#6e8a4f', walkable: false },
  'C': { color: '#8c2d4f', walkable: true, special: 'cursed' },
  'S': { color: '#8bd4ff', walkable: true, special: 'sorcerer' },
  'P': { color: '#f5d06f', walkable: true, special: 'portal' },
};

const enemies = {
  cursed: {
    name: 'Cursed Spirit',
    maxHp: 12,
    attack: 4,
    color: '#ff6b8a',
  },
};

const battleOptions = ['Attack', 'Defend', 'Technique', 'Flee'];
let battle = {
  enemy: null,
  optionIndex: 0,
  message: 'Choose your action',
};

const messages = {
  cursed: 'A cursed spirit has appeared!',
  sorcerer: 'The sorcerer heals your wounds.',
  portal: 'A leyline portal whisks you away.',
};

function setTile(x, y, glyph) {
  const row = tileMap[y].split('');
  row[x] = glyph;
  tileMap[y] = row.join('');
}

function drawTile(x, y, tile) {
  ctx.fillStyle = tile.color;
  ctx.fillRect(x * tileSize, y * tileSize, tileSize, tileSize);
  if (tile.special === 'cursed') {
    ctx.fillStyle = '#ff6b8a';
    ctx.fillRect(x * tileSize + 10, y * tileSize + 10, 12, 12);
  }
  if (tile.special === 'sorcerer') {
    ctx.fillStyle = '#ffffff';
    ctx.fillRect(x * tileSize + 10, y * tileSize + 6, 12, 8);
    ctx.fillRect(x * tileSize + 6, y * tileSize + 14, 20, 6);
  }
  if (tile.special === 'portal') {
    ctx.fillStyle = '#e3d16f';
    ctx.beginPath();
    ctx.arc(x * tileSize + 16, y * tileSize + 16, 10, 0, Math.PI * 2);
    ctx.fill();
  }
}

function drawGrid() {
  for (let y = 0; y < gridHeight; y++) {
    const row = tileMap[y] || ''.padEnd(gridWidth, '.');
    for (let x = 0; x < gridWidth; x++) {
      const glyph = row[x] || '.';
      const tile = tiles[glyph] || tiles['.'];
      drawTile(x, y, tile);
    }
  }
}

function drawPlayer() {
  const px = player.x * tileSize;
  const py = player.y * tileSize;
  ctx.fillStyle = '#ffffff';
  ctx.fillRect(px + 6, py + 6, 20, 20);
  ctx.fillStyle = player.color;
  ctx.fillRect(px + 10, py + 10, 12, 12);
}

function drawHUD() {
  ctx.fillStyle = 'rgba(12, 15, 24, 0.8)';
  ctx.fillRect(0, canvas.height - 40, canvas.width, 40);
  ctx.fillStyle = '#d8e2ff';
  ctx.font = '14px sans-serif';
  ctx.fillText('HP: ' + player.hp + '/' + player.maxHp + '  Technique: ' + player.technique, 12, canvas.height - 20);
  ctx.fillText('Move with arrows/WASD. In battle, use arrows + Enter.', 230, canvas.height - 20);
}

function drawBattleUI() {
  ctx.fillStyle = 'rgba(4, 8, 18, 0.85)';
  ctx.fillRect(20, 320, canvas.width - 40, 140);
  ctx.strokeStyle = '#7c8db2';
  ctx.strokeRect(20, 320, canvas.width - 40, 140);

  ctx.fillStyle = '#f8f8ff';
  ctx.font = '16px sans-serif';
  ctx.fillText('Battle: ' + battle.enemy.name, 32, 348);
  ctx.fillText('Enemy HP: ' + battle.enemy.hp + '/' + battle.enemy.maxHp, 32, 370);

  ctx.fillText('> ' + battle.message, 32, 402);
  for (let i = 0; i < battleOptions.length; i++) {
    const option = battleOptions[i];
    ctx.fillStyle = i === battle.optionIndex ? '#f4f7ff' : '#9bb0d5';
    ctx.fillText((i === battle.optionIndex ? '▶ ' : '  ') + option, 420, 348 + i * 24);
  }
}

function getTile(x, y) {
  if (y < 0 || y >= gridHeight || x < 0 || x >= gridWidth) return { walkable: false };
  const glyph = tileMap[y][x] || '.';
  return tiles[glyph] || tiles['.'];
}

function spawnBattle() {
  const enemyStats = enemies.cursed;
  battle.enemy = {
    name: enemyStats.name,
    hp: enemyStats.maxHp,
    maxHp: enemyStats.maxHp,
    attack: enemyStats.attack,
    color: enemyStats.color,
  };
  battle.optionIndex = 0;
  battle.message = 'A cursed spirit appears!';
  gameState = 'battle';
  player.defending = false;
  showFlash(battle.message);
}

function resolveEnemyAttack() {
  const baseAttack = Math.floor(Math.random() * battle.enemy.attack) + 1;
  const damage = player.defending ? Math.max(1, Math.floor(baseAttack / 2)) : baseAttack;
  player.hp -= damage;
  showFlash('The enemy hits you for ' + damage + ' damage.');
  player.defending = false;
  if (player.hp <= 0) {
    player.hp = 0;
    endBattle('lost');
  }
}

function endBattle(outcome) {
  if (outcome === 'won') {
    battle.message = 'You defeated the cursed spirit.';
    showFlash(battle.message);
    setTile(player.x, player.y, '.');
    gameState = 'explore';
  } else if (outcome === 'escaped') {
    battle.message = 'You escaped the confrontation.';
    showFlash(battle.message);
    gameState = 'explore';
  } else {
    battle.message = 'You were defeated by the curse.';
    showFlash(battle.message);
    player.hp = Math.max(1, Math.floor(player.maxHp / 2));
    gameState = 'explore';
  }
}

function handleBattleInput(eventCode) {
  if (eventCode === 'ArrowUp' || eventCode === 'KeyW') {
    battle.optionIndex = (battle.optionIndex + battleOptions.length - 1) % battleOptions.length;
  } else if (eventCode === 'ArrowDown' || eventCode === 'KeyS') {
    battle.optionIndex = (battle.optionIndex + 1) % battleOptions.length;
  } else if (eventCode === 'Enter' || eventCode === 'NumpadEnter') {
    const action = battleOptions[battle.optionIndex];
    if (action === 'Attack') {
      const damage = Math.floor(Math.random() * 6) + 3;
      battle.enemy.hp -= damage;
      battle.message = 'You strike the curse for ' + damage + ' damage.';
      showFlash(battle.message);
    } else if (action === 'Defend') {
      player.defending = true;
      battle.message = 'You brace for the next attack.';
      showFlash(battle.message);
    } else if (action === 'Technique') {
      const techDamage = Math.floor(Math.random() * player.technique) + 4;
      battle.enemy.hp -= techDamage;
      battle.message = 'You unleash a cursed technique for ' + techDamage + ' damage.';
      showFlash(battle.message);
    } else if (action === 'Flee') {
      if (Math.random() < 0.5) {
        endBattle('escaped');
        return;
      }
      battle.message = 'You failed to escape!';
      showFlash(battle.message);
    }

    if (battle.enemy && battle.enemy.hp > 0 && gameState === 'battle') {
      resolveEnemyAttack();
    }

    if (battle.enemy && battle.enemy.hp <= 0 && gameState === 'battle') {
      endBattle('won');
    }
  }
}

function movePlayer(dx, dy) {
  if (gameState !== 'explore') return;
  const target = getTile(player.x + dx, player.y + dy);
  if (!target.walkable) return;
  player.x += dx;
  player.y += dy;
  if (target.special === 'cursed') {
    spawnBattle();
  } else if (target.special === 'sorcerer') {
    player.hp = player.maxHp;
    showFlash(messages.sorcerer);
  } else if (target.special === 'portal') {
    player.x = 2;
    player.y = 2;
    showFlash(messages.portal);
  }
}

function handleInput() {
  if (keys.ArrowUp || keys.KeyW) movePlayer(0, -1);
  else if (keys.ArrowDown || keys.KeyS) movePlayer(0, 1);
  else if (keys.ArrowLeft || keys.KeyA) movePlayer(-1, 0);
  else if (keys.ArrowRight || keys.KeyD) movePlayer(1, 0);
}

let flashTimer = 0;
let flashText = '';

function showFlash(text) {
  flashText = text;
  flashTimer = 90;
}

function drawFlash() {
  if (flashTimer <= 0) return;
  ctx.fillStyle = 'rgba(0, 0, 0, 0.85)';
  ctx.fillRect(20, 20, canvas.width - 40, 50);
  ctx.fillStyle = '#f5f5f5';
  ctx.font = '16px sans-serif';
  ctx.fillText(flashText, 28, 52);
}

function loop() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  drawGrid();
  drawPlayer();
  drawHUD();
  if (gameState === 'battle') drawBattleUI();
  drawFlash();
  if (flashTimer > 0) flashTimer -= 1;
  requestAnimationFrame(loop);
}

window.addEventListener('keydown', (event) => {
  keys[event.code] = true;
  if (!gameStarted) return;
  event.preventDefault();
  if (gameState === 'battle') {
    handleBattleInput(event.code);
  } else {
    handleInput();
  }
});

window.addEventListener('keyup', (event) => {
  keys[event.code] = false;
});

startButton.addEventListener('click', () => {
  titleScreen.style.display = 'none';
  gameStarted = true;
  showFlash('Welcome to JJK Story! Seek out cursed energy.');
  requestAnimationFrame(loop);
});
