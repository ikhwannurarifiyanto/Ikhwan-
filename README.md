<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grandmaster AI Chess - Showcase Edition</title>
    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Chessboard.js CSS -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/chessboard-js/1.0.0/chessboard-1.0.0.min.css">
    
    <style>
        :root {
            --bg-dark: #0f172a;
            --accent: #6366f1;
            --accent-hover: #4f46e5;
            --board-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.7);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Inter', sans-serif;
        }

        body {
            background: radial-gradient(circle at center, #1e293b 0%, #0f172a 100%);
            color: #f8fafc;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .header-title {
            margin-bottom: 20px;
            text-align: center;
        }

        .header-title h1 {
            font-size: 1.8rem;
            font-weight: 700;
        }

        .header-title h1 span {
            color: var(--accent);
        }

        .status-text {
            font-size: 0.9rem;
            color: #94a3b8;
            margin-top: 5px;
        }

        /* HD Board Container */
        .board-wrapper {
            position: relative;
            width: 480px;
            max-width: 90vw;
            box-shadow: var(--board-shadow);
            border-radius: 12px;
            overflow: hidden;
            border: 4px solid #334155;
        }

        #board {
            width: 100%;
        }

        /* Warna Papan HD Realistis */
        .white-1e1d3 {
            background-color: #e2d6b5 !important;
            color: #b58863;
        }

        .black-3c85d {
            background-color: #b88b4a !important;
            color: #f0d9b5;
        }

        /* Highlight untuk bidak yang disentuh/diklik */
        .highlight-selected {
            background-color: rgba(99, 102, 241, 0.6) !important;
        }

        /* Action Buttons minimalis */
        .actions {
            margin-top: 20px;
            display: flex;
            gap: 12px;
            width: 480px;
            max-width: 90vw;
        }

        .btn {
            flex: 1;
            padding: 12px;
            border: none;
            border-radius: 10px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s ease;
            background: rgba(255, 255, 255, 0.1);
            color: #f8fafc;
        }

        .btn:hover {
            background: rgba(255, 255, 255, 0.2);
            transform: translateY(-2px);
        }

        .btn-restart {
            background: var(--accent);
        }

        .btn-restart:hover {
            background: var(--accent-hover);
        }
    </style>
</head>
<body>

    <div class="header-title">
        <h1>Grandmaster <span>AI Chess</span></h1>
        <div id="status" class="status-text">Sentuh bidak Anda untuk melangkah</div>
    </div>

    <!-- Papan Catur -->
    <div class="board-wrapper">
        <div id="board"></div>
    </div>

    <!-- Tombol Kontrol Minimalis -->
    <div class="actions">
        <button id="btn-restart" class="btn btn-restart">⚡ Game Baru</button>
        <button id="btn-undo" class="btn">↩️ Batal Langkah</button>
    </div>

    <!-- External CDNs -->
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/chess.js/0.10.3/chess.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/chessboard-js/1.0.0/chessboard-1.0.0.min.js"></script>

    <script>
        const game = new Chess();
        let board = null;
        let stockfish = null;
        let selectedSquare = null;

        const STOCKFISH_WORKER_URL = 'https://cdnjs.cloudflare.com/ajax/libs/stockfish.js/10.0.2/stockfish.js';

        function initStockfish() {
            fetch(STOCKFISH_WORKER_URL)
                .then(res => res.blob())
                .then(blob => {
                    const workerUrl = URL.createObjectURL(blob);
                    stockfish = new Worker(workerUrl);

                    stockfish.onmessage = function(event) {
                        const message = event.data;
                        if (message.startsWith('bestmove')) {
                            const bestMove = message.split(' ')[1];
                            if (bestMove) {
                                game.move({
                                    from: bestMove.substring(0, 2),
                                    to: bestMove.substring(2, 4),
                                    promotion: 'q'
                                });
                                board.position(game.fen());
                                updateStatus();
                            }
                        }
                    };

                    stockfish.postMessage('uci');
                    stockfish.postMessage('ucinewgame');
                    // Tingkat kesulitan AI tetap Maksimal
                    stockfish.postMessage('setoption name Skill Level value 20');
                });
        }

        function makeAIMove() {
            if (game.game_over()) return;

            document.getElementById('status').innerText = '🤖 AI sedang melangkah...';
            
            stockfish.postMessage(`position fen ${game.fen()}`);
            // Dibatasi maksimal 300 ms (0.3 detik) agar respons secepat kilat
            stockfish.postMessage('go movetime 300');
        }

        function removeHighlights() {
            $('#board .square-55d63').removeClass('highlight-selected');
        }

        // Fitur Sentuh Bidak -> Sentuh Petak Tujuan
        function handleSquareClick(square) {
            if (game.game_over() || game.turn() === 'b') return;

            if (selectedSquare === null) {
                const piece = game.get(square);
                if (piece && piece.color === 'w') {
                    selectedSquare = square;
                    $('#board .square-' + square).addClass('highlight-selected');
                }
            } else {
                const move = game.move({
                    from: selectedSquare,
                    to: square,
                    promotion: 'q'
                });

                removeHighlights();
                const previousSquare = selectedSquare;
                selectedSquare = null;

                if (move === null) {
                    const piece = game.get(square);
                    if (piece && piece.color === 'w' && square !== previousSquare) {
                        selectedSquare = square;
                        $('#board .square-' + square).addClass('highlight-selected');
                    }
                    return;
                }

                board.position(game.fen());
                updateStatus();
                // Eksekusi AI langsung tanpa penundaan
                window.setTimeout(makeAIMove, 50);
            }
        }

        function updateStatus() {
            if (game.in_checkmate()) {
                document.getElementById('status').innerText = 'Skakmat! Permainan Selesai.';
            } else if (game.in_draw()) {
                document.getElementById('status').innerText = 'Remis / Seri!';
            } else {
                if (game.turn() === 'w') {
                    document.getElementById('status').innerText = game.in_check() ? '⚠️ SKAK! Giliran Anda' : 'Giliran Anda (Sentuh bidak)';
                } else {
                    document.getElementById('status').innerText = '🤖 Giliran AI...';
                }
            }
        }

        board = Chessboard('board', {
            position: 'start',
            draggable: false, // Mengharuskan mode sentuh/klik
            pieceTheme: 'https://chessboardjs.com/img/chesspieces/wikipedia/{piece}.png'
        });

        initStockfish();

        // Listener untuk Sentuhan/Klik pada Petak Papan
        $('#board').on('click', '.square-55d63', function () {
            const square = $(this).attr('data-square');
            handleSquareClick(square);
        });

        document.getElementById('btn-restart').addEventListener('click', () => {
            game.reset();
            board.start();
            removeHighlights();
            selectedSquare = null;
            updateStatus();
        });

        document.getElementById('btn-undo').addEventListener('click', () => {
            game.undo(); // Undo AI
            game.undo(); // Undo Pemain
            board.position(game.fen());
            removeHighlights();
            selectedSquare = null;
            updateStatus();
        });
    </script>
</body>
</html>
