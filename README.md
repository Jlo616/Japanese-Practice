<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>片假名練習</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        .container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
            gap: 10px;
        }
        .kana-box {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: center;
        }
        .kana {
            font-size: 24px;
            margin-bottom: 5px;
        }
        input {
            width: 90%;
            padding: 5px;
            border: 1px solid #ccc;
        }
        .correct {
            background-color: #90EE90;
        }
        .incorrect {
            background-color: #FFB6C6;
        }
        button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div class="container" id="kanaContainer"></div>
    <button onclick="resetGame()">再來一次</button>

    <script>
        const katakana = [
            {char: 'ア', roma: 'a'}, {char: 'イ', roma: 'i'}, {char: 'ウ', roma: 'u'},
            {char: 'エ', roma: 'e'}, {char: 'オ', roma: 'o'}, {char: 'カ', roma: 'ka'},
            {char: 'キ', roma: 'ki'}, {char: 'ク', roma: 'ku'}, {char: 'ケ', roma: 'ke'},
            {char: 'コ', roma: 'ko'}, {char: 'サ', roma: 'sa'}, {char: 'シ', roma: 'shi'},
            {char: 'ス', roma: 'su'}, {char: 'セ', roma: 'se'}, {char: 'ソ', roma: 'so'},
            {char: 'タ', roma: 'ta'}, {char: 'チ', roma: 'chi'}, {char: 'ツ', roma: 'tsu'},
            {char: 'テ', roma: 'te'}, {char: 'ト', roma: 'to'}, {char: 'ナ', roma: 'na'},
            {char: 'ニ', roma: 'ni'}, {char: 'ヌ', roma: 'nu'}, {char: 'ネ', roma: 'ne'},
            {char: 'ノ', roma: 'no'}, {char: 'ハ', roma: 'ha'}, {char: 'ヒ', roma: 'hi'},
            {char: 'フ', roma: 'fu'}, {char: 'ヘ', roma: 'he'}, {char: 'ホ', roma: 'ho'},
            {char: 'マ', roma: 'ma'}, {char: 'ミ', roma: 'mi'}, {char: 'ム', roma: 'mu'},
            {char: 'メ', roma: 'me'}, {char: 'モ', roma: 'mo'}, {char: 'ヤ', roma: 'ya'},
            {char: 'ユ', roma: 'yu'}, {char: 'ヨ', roma: 'yo'}, {char: 'ラ', roma: 'ra'},
            {char: 'リ', roma: 'ri'}, {char: 'ル', roma: 'ru'}, {char: 'レ', roma: 're'},
            {char: 'ロ', roma: 'ro'}, {char: 'ワ', roma: 'wa'}, {char: 'ヲ', roma: 'wo'},
            {char: 'ン', roma: 'n'}
        ];

        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function createKanaBoxes() {
            const container = document.getElementById('kanaContainer');
            container.innerHTML = '';
            
            const shuffledKatakana = shuffleArray([...katakana]).slice(0, 40);
            
            shuffledKatakana.forEach((item, index) => {
                const box = document.createElement('div');
                box.className = 'kana-box';
                box.innerHTML = `
                    <div class="kana">${item.char}</div>
                    <input type="text" onInput="checkAnswer(this, '${item.roma}')" data-index="${index}">
                `;
                container.appendChild(box);
            });
        }

        function checkAnswer(input, correct) {
            if (input.value.toLowerCase() === correct) {
                input.classList.add('correct');
                input.classList.remove('incorrect');
            } else {
                input.classList.add('incorrect');
                input.classList.remove('correct');
            }
        }

        function resetGame() {
            createKanaBoxes();
        }

        // Initial setup
        createKanaBoxes();
    </script>
</body>
</html>