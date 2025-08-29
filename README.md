<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Business & Finance Terms</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #2c3e50 0%, #4ca1af 100%);
            min-height: 100vh;
            padding: 20px;
            color: #333;
        }

        .container {
            max-width: 1100px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #2c3e50, #4ca1af);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><circle cx="20" cy="20" r="2" fill="rgba(255,255,255,0.1)"/><circle cx="80" cy="30" r="1.5" fill="rgba(255,255,255,0.1)"/><circle cx="40" cy="70" r="1" fill="rgba(255,255,255,0.1)"/><circle cx="90" cy="80" r="2.5" fill="rgba(255,255,255,0.1)"/></svg>');
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.2em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #2c3e50, #4ca1af);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(44,62,80,0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 30px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #f5f7fa, #e8f4f2);
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 25px;
            border: 2px solid #2c3e50;
            box-shadow: 0 4px 15px rgba(44,62,80,0.2);
        }

        .word-bank h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.4em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #2c3e50, #4ca1af);
            color: white;
            padding: 10px 18px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 16px;
            box-shadow: 0 3px 10px rgba(44,62,80,0.3);
            transition: all 0.3s ease;
            cursor: default;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(44,62,80,0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid #2c3e50;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 16px;
            margin: 0 5px;
            min-width: 120px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }

        .option {
            padding: 15px 20px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .option:hover {
            border-color: #2c3e50;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(44,62,80,0.2);
        }

        .option.selected {
            background: #2c3e50;
            color: white;
            border-color: #2c3e50;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #2c3e50;
            font-size: 1.2em;
        }

        .match-item {
            padding: 15px;
            margin: 8px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
        }

        .match-item:hover {
            border-color: #2c3e50;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(44,62,80,0.2);
        }

        .match-item.selected {
            background: #e8f4f2;
            border-color: #2c3e50;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #2c3e50, #4ca1af);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: bold;
            margin: 20px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(44,62,80,0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(44,62,80,0.4);
        }

        .feedback {
            margin-top: 15px;
            padding: 15px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #2c3e50, #4ca1af);
            color: white;
            padding: 15px 20px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(44,62,80,0.3);
            z-index: 1000;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 20px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 200px;
            }
            
            .score {
                position: static;
                margin: 20px auto;
                display: block;
                width: fit-content;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/33</div>
    
    <div class="container">
        <div class="header">
            <h1>🌟 Business & Finance Vocabulary</h1>
            <p>Practice these useful English expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Meanings</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section active">
            <div class="word-bank">
                <h3>📝 Word Bank - Choose from these words:</h3>
                <div class="word-options">
                    <span class="word-option">tied</span>
                    <span class="word-option">pity</span>
                    <span class="word-option">start from scratch</span>
                    <span class="word-option">frugal</span>
                    <span class="word-option">write down</span>
                    <span class="word-option">drop</span>
                    <span class="word-option">the bottom line</span>
                    <span class="word-option">therefore</span>
                    <span class="word-option">at the end of the day</span>
                    <span class="word-option">stable</span>
                    <span class="word-option">on the same page</span>
                </div>
            </div>

            <div class="question">
                <h3>Question 1:</h3>
                <p>After the computer crash, we lost all our data and had to <input type="text" class="fill-blank" data-answer="start from scratch" placeholder="answer"> with the project.</p>
                <div class="feedback" id="feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2:</h3>
                <p>It's a <input type="text" class="fill-blank" data-answer="pity" placeholder="answer"> that the company had to close after 50 years in business.</p>
                <div class="feedback" id="feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3:</h3>
                <p>We need to <input type="text" class="fill-blank" data-answer="write down" placeholder="answer"> these ideas before we forget them.</p>
                <div class="feedback" id="feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4:</h3>
                <p>The stock market saw a significant <input type="text" class="fill-blank" data-answer="drop" placeholder="answer"> after the unexpected economic news.</p>
                <div class="feedback" id="feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5:</h3>
                <p><input type="text" class="fill-blank" data-answer="At the end of the day" placeholder="answer">, what matters most is whether the product satisfies customer needs.</p>
                <div class="feedback" id="feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6:</h3>
                <p>Our sales are <input type="text" class="fill-blank" data-answer="tied" placeholder="answer"> to seasonal fluctuations, with peaks during the holiday season.</p>
                <div class="feedback" id="feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7:</h3>
                <p>Before we proceed, we need to make sure everyone is <input type="text" class="fill-blank" data-answer="on the same page" placeholder="answer"> regarding our objectives.</p>
                <div class="feedback" id="feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8:</h3>
                <p>The company's finances have remained <input type="text" class="fill-blank" data-answer="stable" placeholder="answer"> despite economic uncertainties.</p>
                <div class="feedback" id="feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9:</h3>
                <p><input type="text" class="fill-blank" data-answer="The bottom line" placeholder="answer"> is that we need to increase profitability to survive.</p>
                <div class="feedback" id="feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10:</h3>
                <p>She's very <input type="text" class="fill-blank" data-answer="frugal" placeholder="answer"> with company resources, always finding ways to reduce expenses.</p>
                <div class="feedback" id="feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11:</h3>
                <p>The market research was inconclusive; <input type="text" class="fill-blank" data-answer="therefore" placeholder="answer">, we need to conduct additional studies.</p>
                <div class="feedback" id="feedback-11" style="display: none;"></div>
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #2c3e50;">Match the terms with their meanings</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Terms</h4>
                    <div class="match-item" data-word="tied" onclick="selectMatch(this)">tied</div>
                    <div class="match-item" data-word="pity" onclick="selectMatch(this)">pity</div>
                    <div class="match-item" data-word="start from scratch" onclick="selectMatch(this)">start from scratch</div>
                    <div class="match-item" data-word="frugal" onclick="selectMatch(this)">frugal</div>
                    <div class="match-item" data-word="write down" onclick="selectMatch(this)">write down</div>
                    <div class="match-item" data-word="drop" onclick="selectMatch(this)">drop</div>
                    <div class="match-item" data-word="the bottom line" onclick="selectMatch(this)">the bottom line</div>
                    <div class="match-item" data-word="therefore" onclick="selectMatch(this)">therefore</div>
                    <div class="match-item" data-word="at the end of the day" onclick="selectMatch(this)">at the end of the day</div>
                    <div class="match-item" data-word="stable" onclick="selectMatch(this)">stable</div>
                    <div class="match-item" data-word="on the same page" onclick="selectMatch(this)">on the same page</div>
                </div>
                <div class="match-column">
                    <h4>Meanings</h4>
                    <div class="match-item" data-meaning="on the same page" onclick="selectMatch(this)">In agreement; having the same understanding</div>
                    <div class="match-item" data-meaning="the bottom line" onclick="selectMatch(this)">The most important fact in a situation</div>
                    <div class="match-item" data-meaning="pity" onclick="selectMatch(this)">A feeling of sadness for someone else's misfortune</div>
                    <div class="match-item" data-meaning="start from scratch" onclick="selectMatch(this)">To begin from the beginning with no advantage</div>
                    <div class="match-item" data-meaning="frugal" onclick="selectMatch(this)">Economical; avoiding waste</div>
                    <div class="match-item" data-meaning="tied" onclick="selectMatch(this)">Connected or linked to something</div>
                    <div class="match-item" data-meaning="write down" onclick="selectMatch(this)">To record information on paper</div>
                    <div class="match-item" data-meaning="drop" onclick="selectMatch(this)">A decrease or fall in value</div>
                    <div class="match-item" data-meaning="therefore" onclick="selectMatch(this)">For that reason; consequently</div>
                    <div class="match-item" data-meaning="at the end of the day" onclick="selectMatch(this)">When everything is considered; ultimately</div>
                    <div class="match-item" data-meaning="stable" onclick="selectMatch(this)">Firmly established; not changing</div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "start from scratch" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To begin with minor adjustments</div>
                    <div class="option" onclick="selectOption(this, true)">To begin from the beginning with no advantage</div>
                    <div class="option" onclick="selectOption(this, false)">To make superficial changes</div>
                    <div class="option" onclick="selectOption(this, false)">To continue from where others left off</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: Which phrase means "the most important fact"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">at the end of the day</div>
                    <div class="option" onclick="selectOption(this, true)">the bottom line</div>
                    <div class="option" onclick="selectOption(this, false)">on the same page</div>
                    <div class="option" onclick="selectOption(this, false)">start from scratch</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: "Frugal" refers to:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Being overly generous</div>
                    <div class="option" onclick="selectOption(this, false)">Spending money freely</div>
                    <div class="option" onclick="selectOption(this, true)">Being economical and avoiding waste</div>
                    <div class="option" onclick="selectOption(this, false)">Investing in risky ventures</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: What does "on the same page" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Working in the same location</div>
                    <div class="option" onclick="selectOption(this, true)">Having the same understanding or agreement</div>
                    <div class="option" onclick="selectOption(this, false)">Reading the same document</div>
                    <div class="option" onclick="selectOption(this, false)">Sharing the same opinions about everything</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: "Therefore" is used to express:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Uncertainty</div>
                    <div class="option" onclick="selectOption(this, false)">A condition</div>
                    <div class="option" onclick="selectOption(this, true)">A conclusion or result</div>
                    <div class="option" onclick="selectOption(this, false)">An alternative</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "stable" mean in a business context?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Rapidly growing</div>
                    <div class="option" onclick="selectOption(this, false)">Unpredictable</div>
                    <div class="option" onclick="selectOption(this, true)">Firmly established and not changing</div>
                    <div class="option" onclick="selectOption(this, false)">Newly formed</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 7: "At the end of the day" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">When the workday finishes</div>
                    <div class="option" onclick="selectOption(this, true)">When everything is considered; ultimately</div>
                    <div class="option" onclick="selectOption(this, false)">Late in the evening</div>
                    <div class="option" onclick="selectOption(this, false)">After all calculations are done</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 8: What does a "drop" in the stock market refer to?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A small increase</div>
                    <div class="option" onclick="selectOption(this, true)">A decrease or fall in value</div>
                    <div class="option" onclick="selectOption(this, false)">Stability in prices</div>
                    <div class="option" onclick="selectOption(this, false)">A sudden surge</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 9: "Tied" in a business context means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Restricted or limited</div>
                    <div class="option" onclick="selectOption(this, true)">Connected or linked to something</div>
                    <div class="option" onclick="selectOption(this, false)">Finished or completed</div>
                    <div class="option" onclick="selectOption(this, false)">Equally balanced</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 10: What does "pity" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A small amount</div>
                    <div class="option" onclick="selectOption(this, true)">A feeling of sadness for someone else's misfortune</div>
                    <div class="option" onclick="selectOption(this, false)">A necessary action</div>
                    <div class="option" onclick="selectOption(this, false)">An unfortunate event</div>
                </div>
                <div class="feedback" id="mc-feedback-10" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 11: "Write down" means:</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To decrease the value of something</div>
                    <div class="option" onclick="selectOption(this, true)">To record information on paper</div>
                    <div class="option" onclick="selectOption(this, false)">To lower expectations</div>
                    <div class="option" onclick="selectOption(this, false)">To simplify a concept</div>
                </div>
                <div class="feedback" id="mc-feedback-11" style="display: none;"></div>
            </div>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === 11) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            updateScore();
        }

        function updateScore() {
            // Calculate score for fill-in-the-blank
            let fillScore = 0;
            document.querySelectorAll('.fill-blank.correct').forEach(blank => {
                if (!blank.classList.contains('counted')) {
                    fillScore++;
                    blank.classList.add('counted');
                }
            });
            
            // Calculate score for matching (each pair is 1 point)
            const matchScore = matchedPairs.length;
            
            // Calculate score for multiple choice (each correct is 1 point)
            let mcScore = 0;
            document.querySelectorAll('.option.correct.selected').forEach(opt => {
                mcScore++;
            });
            
            // Total score
            score = fillScore + matchScore + mcScore;
            document.getElementById('score').textContent = score;
        }
    </script>
</body>
</html>
