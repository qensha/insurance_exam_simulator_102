# insurance_exam_simulator_102
insurance_exam_simulator_102
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Insurance Exam Simulator</title>
    <style>
        :root {
            --primary-color: #2e6da4;
            --secondary-color: #5bc0de;
            --success-color: #5cb85c;
            --warning-color: #f0ad4e;
            --danger-color: #d9534f;
            --light-bg: #f5f5f5;
            --dark-text: #333;
            --border-color: #ddd;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--light-bg);
            color: var(--dark-text);
            line-height: 1.6;
        }

        .container {
            max-width: 1200px;
            margin: 20px auto;
            padding: 0 20px;
            display: flex;
            flex-direction: column;
            min-height: 95vh;
            background: white;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }

        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 20px;
            border-bottom: 1px solid var(--border-color);
            background-color: #fff;
        }

        h1 {
            margin: 0;
            font-size: 1.5rem;
            color: var(--primary-color);
            flex-grow: 1;
        }

        nav a {
            padding: 10px 15px;
            text-decoration: none;
            color: var(--dark-text);
            font-weight: 600;
            border-bottom: 3px solid transparent;
            transition: all 0.3s ease;
        }

        nav a.active {
            border-bottom-color: var(--primary-color);
            color: var(--primary-color);
        }

        nav a:hover {
            color: var(--primary-color);
        }

        .main-content {
            flex-grow: 1;
            padding: 20px;
            display: none; /* All sections are hidden by default */
        }

        .main-content.active {
            display: block;
        }

        /* Home Page Styling */
        .home-section {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
        }

        .home-section h2 {
            font-size: 2.5rem;
            color: var(--primary-color);
            margin-bottom: 10px;
        }

        .home-section p {
            max-width: 600px;
            font-size: 1.1rem;
            margin-bottom: 30px;
            color: #666;
        }

        .settings-form {
            background-color: var(--light-bg);
            padding: 30px;
            border-radius: 8px;
            width: 100%;
            max-width: 500px;
            text-align: left;
        }

        .settings-form label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
        }

        .settings-form input,
        .settings-form select {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid var(--border-color);
            border-radius: 4px;
            box-sizing: border-box;
        }

        .settings-form button {
            background-color: var(--success-color);
            color: white;
            padding: 12px 20px;
            border: none;
            border-radius: 4px;
            font-size: 1rem;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
            transition: background-color 0.3s ease;
        }

        .settings-form button:hover {
            background-color: #4cae4c;
        }

        /* Exam Page Styling */
        .exam-page {
            display: flex;
            gap: 20px;
        }

        .exam-main {
            flex: 3;
            display: flex;
            flex-direction: column;
        }

        .exam-sidebar {
            flex: 1;
            background-color: var(--light-bg);
            padding: 15px;
            border-radius: 8px;
            position: sticky;
            top: 20px;
            height: fit-content;
        }

        .timer-progress {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }

        .timer {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--danger-color);
        }

        .timer.warning {
            color: var(--warning-color);
        }

        .timer.danger {
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.05); }
            100% { transform: scale(1); }
        }

        .progress-bar-container {
            width: 60%;
            background-color: #e0e0e0;
            border-radius: 5px;
            overflow: hidden;
        }

        .progress-bar {
            height: 10px;
            background-color: var(--success-color);
            transition: width 0.3s ease;
        }

        .question-container {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
            margin-bottom: 20px;
        }

        .question-text {
            font-size: 1.2rem;
            margin-bottom: 15px;
            font-weight: 500;
        }

        .choices label {
            display: flex;
            align-items: center;
            padding: 10px;
            margin-bottom: 8px;
            background-color: var(--light-bg);
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.2s ease;
        }

        .choices label:hover {
            background-color: #e9e9e9;
        }

        .choices input[type="radio"] {
            margin-right: 15px;
            accent-color: var(--primary-color);
        }

        .navigation-buttons {
            display: flex;
            justify-content: space-between;
            gap: 10px;
        }

        .navigation-buttons button {
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s ease;
            color: white;
            flex-grow: 1;
        }

        #prev-btn {
            background-color: var(--secondary-color);
        }
        #prev-btn:hover { background-color: #46b8da; }

        #next-btn {
            background-color: var(--primary-color);
        }
        #next-btn:hover { background-color: #286090; }

        #mark-btn {
            background-color: var(--warning-color);
        }
        #mark-btn:hover { background-color: #ec971f; }

        #submit-btn {
            background-color: var(--danger-color);
        }
        #submit-btn:hover { background-color: #c9302c; }

        .sidebar-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(40px, 1fr));
            gap: 8px;
            margin-top: 15px;
        }

        .sidebar-grid button {
            width: 40px;
            height: 40px;
            border: 1px solid var(--border-color);
            background-color: #fff;
            color: var(--dark-text);
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.2s ease;
            font-weight: bold;
        }

        .sidebar-grid button:hover {
            background-color: #eee;
        }

        .sidebar-grid button.answered {
            background-color: var(--success-color);
            color: white;
        }

        .sidebar-grid button.marked {
            background-color: var(--warning-color);
            color: white;
        }

        .sidebar-grid button.current {
            background-color: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
            transform: scale(1.1);
        }

        /* Results Page Styling */
        .results-page {
            text-align: center;
        }

        .results-page h2 {
            font-size: 2rem;
            color: var(--primary-color);
        }

        .score-display {
            font-size: 2.5rem;
            font-weight: bold;
            color: var(--success-color);
            margin-bottom: 20px;
        }

        .results-filters {
            margin-bottom: 20px;
        }

        .wrong-questions-list {
            text-align: left;
            margin-top: 30px;
            background-color: var(--light-bg);
            padding: 20px;
            border-radius: 8px;
        }

        .result-item {
            border-bottom: 1px solid var(--border-color);
            padding: 15px 0;
        }

        .result-item:last-child {
            border-bottom: none;
        }

        .result-item .question-text {
            font-weight: bold;
            color: var(--primary-color);
        }

        .result-item .correct-answer {
            color: var(--success-color);
            font-weight: bold;
        }

        .result-item .your-answer {
            color: var(--danger-color);
            font-weight: bold;
        }

        .result-item .explanation {
            font-style: italic;
            color: #666;
            margin-top: 5px;
        }

        .hide-show-toggle {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            margin-top: 15px;
        }

        .hide-show-toggle input {
            accent-color: var(--primary-color);
        }

        .export-pdf-btn {
            background-color: var(--danger-color);
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 20px;
        }

        /* General UI components */
        button {
            transition: all 0.3s ease;
        }

        .hidden {
            display: none !important;
        }

        @media (max-width: 768px) {
            .container {
                margin: 10px;
            }
            .exam-page {
                flex-direction: column;
            }
            .exam-sidebar {
                position: static;
                width: auto;
            }
            header {
                flex-direction: column;
                align-items: flex-start;
            }
            nav {
                margin-top: 10px;
            }
            .settings-form {
                padding: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Insurance Exam Simulator</h1>
            <nav id="nav-tabs">
                <a href="#home" class="active" data-page="home">Home</a>
                <a href="#exam" data-page="exam">Exam</a>
                <a href="#results" data-page="results">Results</a>
            </nav>
        </header>

        <main id="main-content-area">
            <section id="home-page" class="main-content active">
                <div class="home-section">
                    <h2>Welcome to the Insurance Exam Simulator</h2>
                    <p>Prepare for your exam with our comprehensive simulator. Customize your practice session below and start your test.</p>
                    <form id="settings-form" class="settings-form">
                        <h3>Exam Settings</h3>
                        <label for="exam-duration">Exam Duration (minutes):</label>
                        <input type="number" id="exam-duration" value="120" min="10" max="240" aria-label="Exam duration in minutes">

                        <label for="question-order">Question Order:</label>
                        <select id="question-order" aria-label="Question order">
                            <option value="sequential">Sequential</option>
                            <option value="random">Random</option>
                        </select>

                        <label for="option-order">Option Order:</label>
                        <select id="option-order" aria-label="Option order">
                            <option value="fixed">Fixed</option>
                            <option value="shuffled">Shuffled</option>
                        </select>
                        
                        <label for="language-select">Language:</label>
                        <select id="language-select" aria-label="Language selection">
                            <option value="en">English</option>
                            <option value="zh-hans">Simplified Chinese</option>
                            <option value="zh-hant">Traditional Chinese</option>
                        </select>

                        <button type="submit" id="start-exam-btn" aria-label="Start Exam">Start Exam</button>
                    </form>
                </div>
            </section>

            <section id="exam-page" class="main-content">
                <div class="exam-page">
                    <div class="exam-main">
                        <div class="timer-progress">
                            <span id="exam-timer" class="timer" aria-live="polite">00:00</span>
                            <div class="progress-bar-container">
                                <div id="progress-bar" class="progress-bar"></div>
                            </div>
                            <span id="question-counter" aria-live="polite">0/0</span>
                        </div>

                        <div id="question-container" class="question-container">
                            <p id="question-text" class="question-text">Loading question...</p>
                            <form id="choices-form" class="choices"></form>
                            <p id="correct-answer-display" class="correct-answer-text hidden"></p>
                        </div>

                        <div class="navigation-buttons">
                            <button id="prev-btn" aria-label="Previous question">Previous</button>
                            <button id="next-btn" aria-label="Next question">Next</button>
                            <button id="mark-btn" aria-label="Mark question as doubtful">Mark as Doubtful</button>
                            <button id="submit-btn" aria-label="Submit exam">Submit Exam</button>
                        </div>
                    </div>
                    <div class="exam-sidebar">
                        <h3>Question Navigation</h3>
                        <div id="question-grid" class="sidebar-grid" role="navigation"></div>
                    </div>
                </div>
            </section>

            <section id="results-page" class="main-content">
                <div class="results-page">
                    <h2>Exam Results</h2>
                    <p>Your Score: <span id="score-display" class="score-display">0%</span></p>
                    <div class="results-filters">
                        <button id="show-wrong-btn">Show Wrong Questions</button>
                        <button id="show-all-btn">Show All Questions</button>
                    </div>
                    <div class="hide-show-toggle">
                        <label>
                            <input type="checkbox" id="show-correct-toggle" aria-label="Toggle showing correct answers"> Show Correct Answers
                        </label>
                    </div>
                    <div id="wrong-questions-list" class="wrong-questions-list"></div>
                    <button id="export-pdf-btn" class="export-pdf-btn" aria-label="Export results as PDF">Export Results as PDF</button>
                </div>
            </section>
        </main>
    </div>

    <script>
        // Use a placeholder string for the TXT file data
        const insuranceQuestionsTXT = `
            # 01. Code & Ethic
            Choice	Question	Translation - Chinese	Answer
            A	What is the primary purpose of insurance?	保险的主要目的是什么？	B
            A	To provide investment opportunities.	提供投资机会。	A
            B	To transfer the risk of financial loss.	转移财务损失的风险。	B
            C	To provide a tax shelter.	提供避税港。	D
            D	To create a monopoly.	创建垄断。	C

            # 02. Life-Only
            Choice	Question	Translation - Chinese	Answer
            A	What is term life insurance?	什么是定期人寿保险？	A
            A	Coverage for a specified period of time.	在特定时间内提供保障。	A
            B	Coverage for the entire lifetime of the insured.	为被保险人提供终身保障。	C
            C	A policy that builds cash value.	一种可以积累现金价值的保单。	B
            D	A policy that provides dividends.	一种提供红利的保单。	B

            # 03. Accident & Health
            Choice	Question	Translation - Chinese	Answer
            A	What does a deductible in health insurance mean?	健康保险中的免赔额是什么意思？	C
            A	The amount the insurer pays.	保险公司支付的金额。	A
            B	The premium amount.	保费金额。	B
            C	The amount the insured must pay before the insurer pays.	被保险人在保险公司支付前必须支付的金额。	C
            D	The maximum amount the insurer will pay.	保险公司将支付的最高金额。	D
        `;

        // The main application state object
        const appState = {
            questions: [],
            examQuestions: [],
            userAnswers: {},
            doubtfulQuestions: new Set(),
            currentQuestionIndex: 0,
            timer: null,
            timeRemaining: 0,
            settings: {
                duration: 120,
                questionOrder: 'sequential',
                optionOrder: 'fixed',
                language: 'en'
            },
            isExamStarted: false
        };

        // --- DOM Elements ---
        const navTabs = document.getElementById('nav-tabs');
        const mainContentArea = document.getElementById('main-content-area');
        const homePage = document.getElementById('home-page');
        const examPage = document.getElementById('exam-page');
        const resultsPage = document.getElementById('results-page');
        const settingsForm = document.getElementById('settings-form');
        const examTimerEl = document.getElementById('exam-timer');
        const progressBarEl = document.getElementById('progress-bar');
        const questionCounterEl = document.getElementById('question-counter');
        const questionTextEl = document.getElementById('question-text');
        const choicesFormEl = document.getElementById('choices-form');
        const prevBtn = document.getElementById('prev-btn');
        const nextBtn = document.getElementById('next-btn');
        const markBtn = document.getElementById('mark-btn');
        const submitBtn = document.getElementById('submit-btn');
        const questionGridEl = document.getElementById('question-grid');
        const scoreDisplayEl = document.getElementById('score-display');
        const wrongQuestionsListEl = document.getElementById('wrong-questions-list');
        const showWrongBtn = document.getElementById('show-wrong-btn');
        const showAllBtn = document.getElementById('show-all-btn');
        const showCorrectToggle = document.getElementById('show-correct-toggle');
        const exportPdfBtn = document.getElementById('export-pdf-btn');
        const showCorrectAnswerDisplayEl = document.getElementById('correct-answer-display');
        const languageSelectEl = document.getElementById('language-select');

        // --- Data Parsing and Structuring ---
        function parseQuestions(txt) {
            const lines = txt.trim().split('\n').filter(line => line.trim() !== '');
            const questions = [];
            let currentQuestion = null;
            let currentSection = '';

            for (const line of lines) {
                if (line.startsWith('#')) {
                    currentSection = line.substring(1).trim();
                } else if (!line.startsWith('Choice') && line.trim() !== '') {
                    const parts = line.split('\t').map(p => p.trim());
                    if (parts.length < 4) continue;

                    const choice = parts[0];
                    const question = parts[1];
                    const translation = parts[2];
                    const answer = parts[3];

                    if (choice.match(/[A-D]/) && answer.match(/[A-D]/)) {
                        // This is a new question entry
                        if (currentQuestion) {
                            questions.push(currentQuestion);
                        }
                        currentQuestion = {
                            id: questions.length + 1,
                            section: currentSection,
                            question: question,
                            translation: {
                                'zh-hans': translation,
                                'zh-hant': translation
                            },
                            choices: [{
                                choice: choice,
                                text: question
                            }],
                            answer: answer
                        };
                    } else if (currentQuestion) {
                        // This is another choice for the same question
                        currentQuestion.choices.push({
                            choice: choice,
                            text: question
                        });
                    }
                }
            }
            if (currentQuestion) {
                questions.push(currentQuestion);
            }
            // Add a simple Spanish placeholder for demonstration
            questions.forEach(q => {
                q.translation.es = 'Spanish translation not available.';
            });
            return questions;
        }

        // --- Core Application Logic ---
        function navigateTo(pageId) {
            document.querySelectorAll('.main-content').forEach(page => page.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
            document.querySelectorAll('nav a').forEach(link => link.classList.remove('active'));
            document.querySelector(`[data-page="${pageId.replace('-page', '')}"]`).classList.add('active');
            // If we're leaving the exam page, save state
            if (pageId !== 'exam-page' && appState.isExamStarted) {
                saveProgress();
            }
        }

        function saveProgress() {
            try {
                const progress = {
                    userAnswers: appState.userAnswers,
                    doubtfulQuestions: Array.from(appState.doubtfulQuestions),
                    currentQuestionIndex: appState.currentQuestionIndex,
                    timeRemaining: appState.timeRemaining,
                    settings: appState.settings
                };
                localStorage.setItem('examProgress', JSON.stringify(progress));
            } catch (e) {
                console.error("Could not save to localStorage", e);
            }
        }

        function loadProgress() {
            try {
                const savedProgress = localStorage.getItem('examProgress');
                if (savedProgress) {
                    const progress = JSON.parse(savedProgress);
                    appState.userAnswers = progress.userAnswers || {};
                    appState.doubtfulQuestions = new Set(progress.doubtfulQuestions || []);
                    appState.currentQuestionIndex = progress.currentQuestionIndex || 0;
                    appState.timeRemaining = progress.timeRemaining || appState.settings.duration * 60;
                    appState.settings = progress.settings || appState.settings;
                    // Update UI with loaded settings
                    document.getElementById('exam-duration').value = appState.settings.duration;
                    document.getElementById('question-order').value = appState.settings.questionOrder;
                    document.getElementById('option-order').value = appState.settings.optionOrder;
                    document.getElementById('language-select').value = appState.settings.language;
                    return true;
                }
            } catch (e) {
                console.error("Could not load from localStorage", e);
            }
            return false;
        }

        function startExam() {
            const duration = parseInt(document.getElementById('exam-duration').value, 10);
            const questionOrder = document.getElementById('question-order').value;
            const optionOrder = document.getElementById('option-order').value;
            const language = document.getElementById('language-select').value;
            
            appState.settings.duration = duration;
            appState.settings.questionOrder = questionOrder;
            appState.settings.optionOrder = optionOrder;
            appState.settings.language = language;

            appState.isExamStarted = true;
            appState.examQuestions = [...appState.questions];

            if (questionOrder === 'random') {
                shuffleArray(appState.examQuestions);
            }
            
            appState.userAnswers = {};
            appState.doubtfulQuestions = new Set();
            appState.currentQuestionIndex = 0;
            appState.timeRemaining = duration * 60;
            
            startTimer();
            renderQuestion();
            renderQuestionGrid();
            navigateTo('exam-page');
        }

        function renderQuestion() {
            if (appState.examQuestions.length === 0) {
                questionTextEl.textContent = 'No questions loaded.';
                choicesFormEl.innerHTML = '';
                return;
            }
            
            const q = appState.examQuestions[appState.currentQuestionIndex];
            const lang = appState.settings.language;

            let questionText = q.question;
            if (lang !== 'en' && q.translation[lang]) {
                questionText = q.translation[lang];
            }
            questionTextEl.textContent = questionText;

            let choices = [...q.choices];
            if (appState.settings.optionOrder === 'shuffled') {
                shuffleArray(choices);
            }

            choicesFormEl.innerHTML = '';
            choices.forEach(choice => {
                const label = document.createElement('label');
                const radio = document.createElement('input');
                radio.type = 'radio';
                radio.name = `q${q.id}`;
                radio.value = choice.choice;
                radio.addEventListener('change', () => {
                    appState.userAnswers[q.id] = choice.choice;
                    updateQuestionGridButton(q.id, 'answered');
                    saveProgress();
                });
                
                if (appState.userAnswers[q.id] === choice.choice) {
                    radio.checked = true;
                }

                const span = document.createElement('span');
                span.textContent = `${choice.choice}. ${choice.text}`;
                
                label.appendChild(radio);
                label.appendChild(span);
                choicesFormEl.appendChild(label);
            });
            
            // Hide the correct answer display
            showCorrectAnswerDisplayEl.classList.add('hidden');
            updateNavigationButtons();
            updateProgressDisplay();
            updateQuestionGridButton(q.id, 'current');
        }

        function updateNavigationButtons() {
            prevBtn.disabled = appState.currentQuestionIndex === 0;
            nextBtn.textContent = appState.currentQuestionIndex === appState.examQuestions.length - 1 ? 'Finish Exam' : 'Next';
        }

        function updateProgressDisplay() {
            const current = appState.currentQuestionIndex + 1;
            const total = appState.examQuestions.length;
            questionCounterEl.textContent = `${current}/${total}`;
            const progress = (current / total) * 100;
            progressBarEl.style.width = `${progress}%`;
        }

        function renderQuestionGrid() {
            questionGridEl.innerHTML = '';
            appState.examQuestions.forEach((q, index) => {
                const btn = document.createElement('button');
                btn.textContent = index + 1;
                btn.setAttribute('aria-label', `Go to question ${index + 1}`);
                btn.addEventListener('click', () => {
                    appState.currentQuestionIndex = index;
                    renderQuestion();
                });
                if (appState.userAnswers[q.id]) {
                    btn.classList.add('answered');
                }
                if (appState.doubtfulQuestions.has(q.id)) {
                    btn.classList.add('marked');
                }
                questionGridEl.appendChild(btn);
            });
            updateQuestionGridButton(appState.examQuestions[appState.currentQuestionIndex].id, 'current');
        }
        
        function updateQuestionGridButton(questionId, stateClass) {
            const btn = questionGridEl.querySelector(`[aria-label="Go to question ${appState.examQuestions.findIndex(q => q.id === questionId) + 1}"]`);
            if (btn) {
                // Remove all state classes before adding the new one
                btn.classList.remove('answered', 'marked', 'current');
                // Re-add based on current state
                if (appState.userAnswers[questionId]) btn.classList.add('answered');
                if (appState.doubtfulQuestions.has(questionId)) btn.classList.add('marked');
                if (stateClass === 'current') btn.classList.add('current');
            }
        }

        function startTimer() {
            if (appState.timer) clearInterval(appState.timer);
            appState.timer = setInterval(() => {
                appState.timeRemaining--;
                const minutes = Math.floor(appState.timeRemaining / 60);
                const seconds = appState.timeRemaining % 60;
                examTimerEl.textContent = `${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;
                
                if (appState.timeRemaining <= 300 && appState.timeRemaining > 0) { // 5-minute warning
                    examTimerEl.classList.add('warning');
                    if (appState.timeRemaining % 60 === 0) {
                        playAudio('warning');
                    }
                } else if (appState.timeRemaining <= 60 && appState.timeRemaining > 0) { // 1-minute danger
                    examTimerEl.classList.remove('warning');
                    examTimerEl.classList.add('danger');
                }

                if (appState.timeRemaining <= 0) {
                    clearInterval(appState.timer);
                    playAudio('finish');
                    showResults();
                    alert("Time's up! The exam has been submitted.");
                }
            }, 1000);
        }

        function stopTimer() {
            if (appState.timer) clearInterval(appState.timer);
        }

        function showResults() {
            stopTimer();
            navigateTo('results-page');
            
            let correctCount = 0;
            const incorrectQuestions = [];

            appState.examQuestions.forEach(q => {
                const userAnswer = appState.userAnswers[q.id];
                if (userAnswer && userAnswer === q.answer) {
                    correctCount++;
                } else if (userAnswer !== undefined) {
                    incorrectQuestions.push({
                        question: q,
                        userAnswer: userAnswer
                    });
                }
            });

            const totalQuestions = appState.examQuestions.length;
            const percentage = (correctCount / totalQuestions) * 100;
            scoreDisplayEl.textContent = `${correctCount}/${totalQuestions} (${percentage.toFixed(2)}%)`;
            
            renderResultsList(incorrectQuestions, appState.examQuestions);
        }
        
        function renderResultsList(wrongQuestions, allQuestions) {
            wrongQuestionsListEl.innerHTML = '';
            const questionsToShow = wrongQuestions;
            const questions = (questionsToShow === wrongQuestions) ? questionsToShow : allQuestions;
            
            questions.forEach(item => {
                const q = (item.question) ? item.question : item;
                const userAnswer = (item.userAnswer) ? item.userAnswer : appState.userAnswers[q.id];
                
                const resultItem = document.createElement('div');
                resultItem.className = 'result-item';

                const questionText = document.createElement('p');
                questionText.className = 'question-text';
                questionText.textContent = `${q.id}. ${q.question}`;
                resultItem.appendChild(questionText);

                const answers = document.createElement('p');
                answers.innerHTML = `
                    <span class="correct-answer">Correct Answer: ${q.answer}</span>
                    ${userAnswer ? `<br><span class="your-answer">Your Answer: ${userAnswer}</span>` : '<br><span class="your-answer">Your Answer: Skipped</span>'}
                `;
                resultItem.appendChild(answers);

                if (!showCorrectToggle.checked) {
                    resultItem.querySelectorAll('.correct-answer, .your-answer').forEach(el => el.classList.add('hidden'));
                }

                wrongQuestionsListEl.appendChild(resultItem);
            });
        }
        
        // --- Helper Functions ---
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
        }

        function playAudio(type) {
            // Note: In a real app, we'd use a real audio element.
            // This is a placeholder for the logic.
            const audio = new Audio();
            if (type === 'warning') {
                // audio.src = 'path/to/warning.mp3';
            } else if (type === 'finish') {
                // audio.src = 'path/to/finish.mp3';
            }
            // audio.play().catch(e => console.log('Audio playback failed:', e));
        }

        // --- Event Listeners ---
        document.addEventListener('DOMContentLoaded', () => {
            appState.questions = parseQuestions(insuranceQuestionsTXT);
            // Attempt to load progress on page load
            const hasSavedProgress = loadProgress();
            if (hasSavedProgress) {
                // If there's saved progress, update UI elements to reflect it
                // e.g., enable the "Continue Exam" button or similar logic
            }
        });

        navTabs.addEventListener('click', (e) => {
            if (e.target.tagName === 'A') {
                e.preventDefault();
                const pageId = e.target.getAttribute('data-page') + '-page';
                navigateTo(pageId);
            }
        });

        settingsForm.addEventListener('submit', (e) => {
            e.preventDefault();
            startExam();
        });

        nextBtn.addEventListener('click', () => {
            if (appState.currentQuestionIndex < appState.examQuestions.length - 1) {
                appState.currentQuestionIndex++;
                renderQuestion();
            } else {
                showResults();
            }
        });

        prevBtn.addEventListener('click', () => {
            if (appState.currentQuestionIndex > 0) {
                appState.currentQuestionIndex--;
                renderQuestion();
            }
        });
        
        markBtn.addEventListener('click', () => {
            const currentQuestionId = appState.examQuestions[appState.currentQuestionIndex].id;
            if (appState.doubtfulQuestions.has(currentQuestionId)) {
                appState.doubtfulQuestions.delete(currentQuestionId);
            } else {
                appState.doubtfulQuestions.add(currentQuestionId);
            }
            updateQuestionGridButton(currentQuestionId, 'marked');
            saveProgress();
        });

        submitBtn.addEventListener('click', showResults);
        showWrongBtn.addEventListener('click', () => renderResultsList(appState.examQuestions.filter(q => appState.userAnswers[q.id] !== q.answer), null));
        showAllBtn.addEventListener('click', () => renderResultsList(appState.examQuestions, appState.examQuestions));
        
        showCorrectToggle.addEventListener('change', () => {
            const listItems = wrongQuestionsListEl.querySelectorAll('.result-item .correct-answer, .result-item .your-answer');
            listItems.forEach(el => el.classList.toggle('hidden', !showCorrectToggle.checked));
        });

        // The PDF export functionality is a placeholder as jsPDF is an external library
        exportPdfBtn.addEventListener('click', () => {
            alert('PDF Export functionality would use a library like jsPDF. This is a placeholder.');
            // A simplified alternative is to print the page
            // window.print();
        });

        // Simple "Show Correct Answer" toggle on Exam Page (not in final code, but for completeness)
        // This feature would require a new button on the exam page
        // For example:
        // const showCorrectAnswerToggle = document.createElement('button');
        // showCorrectAnswerToggle.textContent = 'Show Answer';
        // showCorrectAnswerToggle.addEventListener('click', () => {
        //     const q = appState.examQuestions[appState.currentQuestionIndex];
        //     showCorrectAnswerDisplayEl.textContent = `Correct Answer: ${q.answer}`;
        //     showCorrectAnswerDisplayEl.classList.remove('hidden');
        // });
        // The HTML already includes a placeholder for this functionality
        
    </script>
</body>
</html>
