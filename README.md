# Outbound Behavior Test
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Find Your Outbound Personality - Cold Email Quiz</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --ocean-deep: #0a2540;
            --ocean-medium: #1a4d7a;
            --ocean-light: #4a90e2;
            --ocean-foam: #7ec8e3;
            --sand: #f8f4e8;
            --coral: #ff6b6b;
            --seaweed: #2ecc71;
            --pearl: #ffffff;
        }

        body {
            font-family: 'DM Sans', sans-serif;
            background: linear-gradient(180deg, #0a2540 0%, #1a4d7a 50%, #4a90e2 100%);
            min-height: 100vh;
            color: var(--pearl);
            overflow-x: hidden;
            position: relative;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 20% 30%, rgba(126, 200, 227, 0.1) 0%, transparent 50%),
                radial-gradient(circle at 80% 70%, rgba(46, 204, 113, 0.08) 0%, transparent 50%),
                radial-gradient(circle at 50% 50%, rgba(255, 107, 107, 0.05) 0%, transparent 50%);
            pointer-events: none;
            animation: drift 20s ease-in-out infinite;
        }

        @keyframes drift {
            0%, 100% { transform: translate(0, 0); }
            50% { transform: translate(-20px, 20px); }
        }

        .bubbles {
            position: fixed;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            overflow: hidden;
        }

        .bubble {
            position: absolute;
            bottom: -100px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            opacity: 0.6;
            animation: rise 15s infinite ease-in;
        }

        .bubble:nth-child(1) { left: 10%; width: 40px; height: 40px; animation-delay: 0s; animation-duration: 12s; }
        .bubble:nth-child(2) { left: 25%; width: 20px; height: 20px; animation-delay: 2s; animation-duration: 10s; }
        .bubble:nth-child(3) { left: 45%; width: 30px; height: 30px; animation-delay: 4s; animation-duration: 14s; }
        .bubble:nth-child(4) { left: 65%; width: 25px; height: 25px; animation-delay: 1s; animation-duration: 11s; }
        .bubble:nth-child(5) { left: 80%; width: 35px; height: 35px; animation-delay: 3s; animation-duration: 13s; }
        .bubble:nth-child(6) { left: 90%; width: 15px; height: 15px; animation-delay: 5s; animation-duration: 9s; }

        @keyframes rise {
            0% {
                bottom: -100px;
                transform: translateX(0);
            }
            50% {
                transform: translateX(100px);
            }
            100% {
                bottom: 110vh;
                transform: translateX(-100px);
            }
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 1;
        }

        /* Hero Section */
        .hero {
            text-align: center;
            padding: 60px 20px 80px;
            margin-bottom: 60px;
            position: relative;
        }

        .hero h1 {
            font-family: 'Playfair Display', serif;
            font-size: clamp(2.5rem, 6vw, 5rem);
            font-weight: 900;
            margin-bottom: 20px;
            background: linear-gradient(135deg, #ffffff 0%, #7ec8e3 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            line-height: 1.1;
            animation: fadeInUp 0.8s ease-out;
        }

        .hero-subtitle {
            font-size: clamp(1.1rem, 2vw, 1.4rem);
            color: rgba(255, 255, 255, 0.9);
            margin-bottom: 50px;
            animation: fadeInUp 0.8s ease-out 0.2s both;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Sea Creatures Showcase */
        .creatures-showcase {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(130px, 1fr));
            gap: 20px;
            margin-bottom: 80px;
            padding: 0 20px;
        }

        .creature-card {
            background: rgba(255, 255, 255, 0.08);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.15);
            border-radius: 20px;
            padding: 25px 15px;
            text-align: center;
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
            animation: fadeInUp 0.6s ease-out both;
        }

        .creature-card:nth-child(1) { animation-delay: 0.1s; }
        .creature-card:nth-child(2) { animation-delay: 0.15s; }
        .creature-card:nth-child(3) { animation-delay: 0.2s; }
        .creature-card:nth-child(4) { animation-delay: 0.25s; }
        .creature-card:nth-child(5) { animation-delay: 0.3s; }
        .creature-card:nth-child(6) { animation-delay: 0.35s; }
        .creature-card:nth-child(7) { animation-delay: 0.4s; }
        .creature-card:nth-child(8) { animation-delay: 0.45s; }

        .creature-card:hover {
            transform: translateY(-10px) scale(1.05);
            background: rgba(255, 255, 255, 0.15);
            border-color: rgba(126, 200, 227, 0.5);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
        }

        .creature-icon {
            font-size: 3.5rem;
            margin-bottom: 12px;
            display: block;
            filter: drop-shadow(0 4px 8px rgba(0, 0, 0, 0.2));
        }

        .creature-name {
            font-size: 0.95rem;
            font-weight: 700;
            color: rgba(255, 255, 255, 0.95);
            margin-bottom: 5px;
        }

        .creature-subtitle {
            font-size: 0.75rem;
            color: rgba(255, 255, 255, 0.6);
            line-height: 1.3;
        }

        /* Quiz Introduction */
        .quiz-intro {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border: 1px solid rgba(255, 255, 255, 0.2);
            border-radius: 30px;
            padding: 50px 40px;
            margin-bottom: 40px;
            text-align: center;
            animation: fadeInUp 0.8s ease-out 0.5s both;
        }

        .quiz-intro h2 {
            font-family: 'Playfair Display', serif;
            font-size: 2.2rem;
            margin-bottom: 20px;
            color: var(--ocean-foam);
        }

        .quiz-intro p {
            font-size: 1.1rem;
            line-height: 1.6;
            color: rgba(255, 255, 255, 0.85);
            max-width: 700px;
            margin: 0 auto 30px;
        }

        .start-button {
            display: inline-block;
            padding: 18px 50px;
            background: linear-gradient(135deg, var(--coral) 0%, #ff8787 100%);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 1.2rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.4);
            text-decoration: none;
        }

        .start-button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(255, 107, 107, 0.5);
        }

        /* Quiz Container */
        .quiz-section {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 30px;
            padding: 50px;
            max-width: 900px;
            margin: 0 auto;
            box-shadow: 0 30px 80px rgba(0, 0, 0, 0.3);
            color: var(--ocean-deep);
            display: none;
        }

        .quiz-section.active {
            display: block;
            animation: fadeInUp 0.6s ease-out;
        }

        .progress-container {
            margin-bottom: 40px;
        }

        .progress-text {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
            font-size: 0.95rem;
            color: var(--ocean-medium);
            font-weight: 600;
        }

        .progress-bar {
            width: 100%;
            height: 10px;
            background: rgba(10, 37, 64, 0.1);
            border-radius: 10px;
            overflow: hidden;
            position: relative;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, var(--ocean-light) 0%, var(--ocean-foam) 100%);
            width: 0%;
            transition: width 0.5s cubic-bezier(0.65, 0, 0.35, 1);
            position: relative;
            overflow: hidden;
        }

        .progress-fill::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            bottom: 0;
            right: 0;
            background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
            animation: shimmer 2s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%); }
            100% { transform: translateX(100%); }
        }

        .question-container {
            margin-bottom: 40px;
        }

        .question-number {
            display: inline-block;
            background: var(--ocean-light);
            color: white;
            padding: 8px 20px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 700;
            margin-bottom: 20px;
        }

        .question-container h3 {
            font-family: 'Playfair Display', serif;
            font-size: 1.6rem;
            color: var(--ocean-deep);
            margin-bottom: 25px;
            line-height: 1.4;
        }

        .options {
            display: grid;
            gap: 15px;
        }

        .option {
            padding: 20px 25px;
            background: rgba(10, 37, 64, 0.04);
            border: 2px solid rgba(10, 37, 64, 0.1);
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            font-size: 1.05rem;
            color: var(--ocean-deep);
            position: relative;
            overflow: hidden;
        }

        .option::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(74, 144, 226, 0.1), transparent);
            transition: left 0.5s;
        }

        .option:hover::before {
            left: 100%;
        }

        .option:hover {
            border-color: var(--ocean-light);
            background: rgba(74, 144, 226, 0.08);
            transform: translateX(5px);
        }

        .option.selected {
            background: linear-gradient(135deg, var(--ocean-light) 0%, var(--ocean-medium) 100%);
            color: white;
            border-color: var(--ocean-medium);
            transform: scale(1.02);
        }

        .navigation-buttons {
            display: flex;
            gap: 15px;
            justify-content: space-between;
            margin-top: 40px;
        }

        .btn {
            padding: 15px 35px;
            border: none;
            border-radius: 50px;
            font-size: 1.05rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'DM Sans', sans-serif;
        }

        .btn-secondary {
            background: rgba(10, 37, 64, 0.1);
            color: var(--ocean-deep);
        }

        .btn-secondary:hover {
            background: rgba(10, 37, 64, 0.15);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--ocean-light) 0%, var(--ocean-medium) 100%);
            color: white;
            box-shadow: 0 8px 20px rgba(74, 144, 226, 0.3);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 12px 30px rgba(74, 144, 226, 0.4);
        }

        .btn-primary:disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        /* Result Section */
        .result-container {
            display: none;
            text-align: center;
        }

        .result-container.active {
            display: block;
            animation: fadeInUp 0.8s ease-out;
        }

        .personality-icon-large {
            font-size: 140px;
            margin: 30px 0;
            display: block;
            filter: drop-shadow(0 10px 30px rgba(0, 0, 0, 0.2));
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        .personality-title {
            font-family: 'Playfair Display', serif;
            font-size: 3rem;
            color: var(--ocean-deep);
            margin-bottom: 10px;
        }

        .personality-subtitle {
            font-size: 1.4rem;
            color: var(--ocean-medium);
            font-style: italic;
            margin-bottom: 40px;
        }

        .personality-meaning {
            font-size: 1.2rem;
            color: var(--ocean-deep);
            margin-bottom: 50px;
            padding: 25px;
            background: rgba(74, 144, 226, 0.08);
            border-radius: 15px;
            border-left: 4px solid var(--ocean-light);
        }

        .personality-section {
            text-align: left;
            margin: 30px 0;
            padding: 30px;
            background: rgba(10, 37, 64, 0.04);
            border-radius: 20px;
        }

        .personality-section h4 {
            font-family: 'Playfair Display', serif;
            color: var(--ocean-light);
            font-size: 1.6rem;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .section-icon {
            font-size: 1.8rem;
        }

        .personality-section ul {
            list-style: none;
            padding-left: 0;
        }

        .personality-section li {
            padding: 12px 0;
            padding-left: 35px;
            position: relative;
            color: var(--ocean-deep);
            line-height: 1.7;
            font-size: 1.05rem;
        }

        .personality-section li:before {
            content: "→";
            position: absolute;
            left: 0;
            color: var(--ocean-light);
            font-weight: bold;
            font-size: 1.3rem;
        }

        .restart-btn {
            margin-top: 40px;
            padding: 18px 50px;
            background: linear-gradient(135deg, var(--coral) 0%, #ff8787 100%);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 1.15rem;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 10px 30px rgba(255, 107, 107, 0.3);
            transition: all 0.3s ease;
        }

        .restart-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(255, 107, 107, 0.4);
        }

        @media (max-width: 768px) {
            .creatures-showcase {
                grid-template-columns: repeat(4, 1fr);
                gap: 12px;
            }

            .creature-card {
                padding: 20px 10px;
            }

            .creature-icon {
                font-size: 2.5rem;
            }

            .creature-name {
                font-size: 0.85rem;
            }

            .creature-subtitle {
                font-size: 0.7rem;
            }

            .quiz-section {
                padding: 30px 25px;
            }

            .quiz-intro {
                padding: 35px 25px;
            }

            .navigation-buttons {
                flex-direction: column;
            }

            .personality-title {
                font-size: 2.2rem;
            }
        }
    </style>
</head>
<body>
    <div class="bubbles">
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
        <div class="bubble"></div>
    </div>

    <div class="container">
        <!-- Hero Section -->
        <div class="hero" id="hero-section">
            <h1>🌊 Discover Your Outbound Personality</h1>
            <p class="hero-subtitle">What type of cold emailer are you? Find out in 2 minutes.</p>
        </div>

        <!-- Sea Creatures Showcase -->
        <div class="creatures-showcase" id="creatures-showcase">
            <div class="creature-card">
                <span class="creature-icon">🐋</span>
                <div class="creature-name">The Whale</div>
                <div class="creature-subtitle">Volume Broadcaster</div>
            </div>
            <div class="creature-card">
                <span class="creature-icon">🦈</span>
                <div class="creature-name">The Shark</div>
                <div class="creature-subtitle">Aggressive Hunter</div>
            </div>
            <div class="creature-card">
                <span class="creature-icon">🐙</span>
                <div class="creature-name">The Octopus</div>
                <div class="creature-subtitle">Adaptive Strategist</div>
            </div>
            <div class="creature-card">
                <span class="creature-icon">🦑</span>
                <div class="creature-name">The Squid</div>
                <div class="creature-subtitle">Invisible Sender</div>
            </div>
            <div class="creature-card">
                <span class="creature-icon">🦭</span>
                <div class="creature-name">The Seal</div>
                <div class="creature-subtitle">Friendly Builder</div>
            </div>
            <div class="creature-card">
                <span class="creature-icon">⭐</span>
                <div class="creature-name">The Starfish</div>
                <div class="creature-subtitle">Balanced Performer</div>
            </div>
            <div class="creature-card">
                <span class="creature-icon">🐢</span>
                <div class="creature-name">The Turtle</div>
                <div class="creature-subtitle">Patient Hesitator</div>
            </div>
            <div class="creature-card">
                <span class="creature-icon">🦀</span>
                <div class="creature-name">The Crab</div>
                <div class="creature-subtitle">Defensive Avoider</div>
            </div>
        </div>

        <!-- Quiz Introduction -->
        <div class="quiz-intro" id="quiz-intro">
            <h2>Ready to dive in?</h2>
            <p>Answer 20 quick questions about your cold email approach and we'll reveal which sea creature matches your outbound personality — along with personalized insights to improve your results.</p>
            <button class="start-button" onclick="startQuiz()">Start the Quiz</button>
        </div>

        <!-- Quiz Section -->
        <div class="quiz-section" id="quiz-section">
            <div class="progress-container">
                <div class="progress-text">
                    <span id="current-question">Question 1 of 20</span>
                    <span id="progress-percent">5%</span>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" id="progress"></div>
                </div>
            </div>

            <div id="question-display"></div>

            <div class="navigation-buttons">
                <button class="btn btn-secondary" id="prev-btn" onclick="prevQuestion()" style="display: none;">← Previous</button>
                <button class="btn btn-primary" id="next-btn" onclick="nextQuestion()" disabled>Next →</button>
            </div>
        </div>

        <!-- Result Container -->
        <div class="quiz-section result-container" id="result-container">
            <!-- Results will be shown here -->
        </div>
    </div>

    <script>
        const questions = [
            {
                id: 1,
                question: "How many cold emails do you send per day on average?",
                options: [
                    { text: "1–10", value: "snail" },
                    { text: "11–30", value: "fish" },
                    { text: "31–75", value: "shark" },
                    { text: "76+", value: "whale" }
                ]
            },
            {
                id: 2,
                question: "How much time do you spend researching each prospect before emailing?",
                options: [
                    { text: "10+ minutes", value: "deep" },
                    { text: "3–5 minutes", value: "quick" },
                    { text: "Under 1 minute", value: "surface" },
                    { text: "What research?", value: "none" }
                ]
            },
            {
                id: 3,
                question: "What's your typical email length?",
                options: [
                    { text: "Under 50 words", value: "bite" },
                    { text: "50–100 words", value: "balanced" },
                    { text: "101–200 words", value: "detailed" },
                    { text: "200+ words", value: "novel" }
                ]
            },
            {
                id: 4,
                question: "How personalized is your first line?",
                options: [
                    { text: "Unique insight about them/their company", value: "unique" },
                    { text: "Mentions their role or industry specifically", value: "specific" },
                    { text: "Generic compliment or observation", value: "generic" },
                    { text: "Jumps straight to pitch", value: "pitch" }
                ]
            },
            {
                id: 5,
                question: "What do you lead with in your emails?",
                options: [
                    { text: "A valuable insight or resource", value: "value" },
                    { text: "A thought-provoking question", value: "question" },
                    { text: "Your product/service pitch", value: "pitch" },
                    { text: "Your credentials/social proof", value: "credentials" }
                ]
            },
            {
                id: 6,
                question: "How many follow-ups do you typically send to a non-responder?",
                options: [
                    { text: "0–1", value: "none" },
                    { text: "2–3", value: "gentle" },
                    { text: "4–6", value: "determined" },
                    { text: "7+", value: "never" }
                ]
            },
            {
                id: 7,
                question: "What's your average response time when a prospect replies?",
                options: [
                    { text: "Within 1 hour", value: "lightning" },
                    { text: "1–4 hours", value: "quick" },
                    { text: "Same day", value: "steady" },
                    { text: "Next day or later", value: "slow" }
                ]
            },
            {
                id: 8,
                question: "What's your typical spacing between follow-ups?",
                options: [
                    { text: "2–3 days", value: "aggressive" },
                    { text: "4–7 days", value: "standard" },
                    { text: "8–14 days", value: "patient" },
                    { text: "15+ days", value: "verypatient" }
                ]
            },
            {
                id: 9,
                question: "Your subject lines are usually:",
                options: [
                    { text: "Creative/curiosity-driven", value: "creative" },
                    { text: "Direct/value-focused", value: "direct" },
                    { text: "Personal/conversational", value: "personal" },
                    { text: "Formal/professional", value: "formal" }
                ]
            },
            {
                id: 10,
                question: "When someone doesn't respond, you assume:",
                options: [
                    { text: "They didn't see it", value: "didntsee" },
                    { text: "Bad timing", value: "timing" },
                    { text: "Wrong fit", value: "wrongfit" },
                    { text: "Need more touches", value: "moretouches" }
                ]
            },
            {
                id: 11,
                question: "Your call-to-action typically asks for:",
                options: [
                    { text: "A meeting/call", value: "bigask" },
                    { text: "A simple reply/opinion", value: "smallask" },
                    { text: "To check out a resource", value: "mediumask" },
                    { text: "Nothing specific", value: "noask" }
                ]
            },
            {
                id: 12,
                question: "How often do you A/B test your emails?",
                options: [
                    { text: "Always testing something", value: "always" },
                    { text: "Occasionally test big changes", value: "occasionally" },
                    { text: "Rarely or never test", value: "rarely" },
                    { text: "What's A/B testing?", value: "never" }
                ]
            },
            {
                id: 13,
                question: "Your email signature includes:",
                options: [
                    { text: "Full contact info + social links + calendar", value: "full" },
                    { text: "Name, title, company, and one link", value: "standard" },
                    { text: "Just the basics", value: "basic" },
                    { text: "No signature", value: "none" }
                ]
            },
            {
                id: 14,
                question: "How do you handle your 'not interested' replies?",
                options: [
                    { text: "Thank them and ask to stay in touch", value: "graceful" },
                    { text: "Ask why/what would make it relevant", value: "curious" },
                    { text: "Acknowledge and remove them", value: "acknowledge" },
                    { text: "Ignore and continue sequence", value: "ignore" }
                ]
            },
            {
                id: 15,
                question: "You track which metrics most closely?",
                options: [
                    { text: "Open rates", value: "opens" },
                    { text: "Reply rates", value: "replies" },
                    { text: "Meeting booked rate", value: "meetings" },
                    { text: "Don't really track", value: "notrack" }
                ]
            },
            {
                id: 16,
                question: "Your prospect list is built by:",
                options: [
                    { text: "Hand-picked ideal fits only", value: "handpicked" },
                    { text: "Filtered by specific criteria", value: "filtered" },
                    { text: "Broad category targeting", value: "broad" },
                    { text: "Anyone in the industry", value: "anyone" }
                ]
            },
            {
                id: 17,
                question: "How often do you update your email copy?",
                options: [
                    { text: "Weekly based on results", value: "weekly" },
                    { text: "Monthly or when it stops working", value: "monthly" },
                    { text: "Rarely, stick with what works", value: "rarely" },
                    { text: "Using the same template forever", value: "never" }
                ]
            },
            {
                id: 18,
                question: "Your email warmup/deliverability setup is:",
                options: [
                    { text: "Fully optimized", value: "full" },
                    { text: "Partially set up", value: "partial" },
                    { text: "Basic setup", value: "basic" },
                    { text: "What's email warmup?", value: "none" }
                ]
            },
            {
                id: 19,
                question: "When you get a reply, your next email:",
                options: [
                    { text: "Directly addresses their specific response", value: "custom" },
                    { text: "Follows a pre-written sequence", value: "sequence" },
                    { text: "Mix of template + personalization", value: "mix" },
                    { text: "Completely custom every time", value: "fullcustom" }
                ]
            },
            {
                id: 20,
                question: "Your main goal with cold email is:",
                options: [
                    { text: "Start genuine conversations", value: "conversations" },
                    { text: "Book meetings fast", value: "meetings" },
                    { text: "Generate as many leads as possible", value: "leads" },
                    { text: "Educate and build awareness", value: "educate" }
                ]
            }
        ];

        const personalities = {
            whale: {
                icon: "🐋",
                title: "The Whale",
                subtitle: "The Volume Broadcaster",
                meaning: "You prioritize volume over everything - mass outreach with minimal personalization.",
                strengths: [
                    "You're not afraid of rejection and understand it's a numbers game",
                    "You can fill your pipeline quickly when you need leads fast"
                ],
                problems: [
                    "Your emails look like spam because they lack any personal touch",
                    "You're burning your domain reputation and landing in spam folders"
                ],
                fixes: [
                    "Cut volume in half, spend 3-5 minutes researching each prospect for specific insights",
                    "Set up proper email infrastructure (SPF, DKIM, DMARC, warmed domains) immediately"
                ]
            },
            shark: {
                icon: "🦈",
                title: "The Shark",
                subtitle: "The Aggressive Hunter",
                meaning: "You're relentlessly aggressive with fast responses and constant follow-ups.",
                strengths: [
                    "You catch prospects at the right moment when competitors have already given up",
                    "Your quick response time shows you're serious and available"
                ],
                problems: [
                    "You follow up too frequently and come across as pushy and desperate",
                    "Prospects feel hunted, not helped - you burn bridges with your intensity"
                ],
                fixes: [
                    "Space follow-ups to 5-7 days and cap sequences at 4-5 touches maximum",
                    "Add unique value in every follow-up instead of 'just checking in' messages"
                ]
            },
            octopus: {
                icon: "🐙",
                title: "The Octopus",
                subtitle: "The Adaptive Strategist",
                meaning: "You're adaptive and strategic, constantly testing and optimizing your approach.",
                strengths: [
                    "You learn from what works and don't repeat the same mistakes",
                    "Your data-driven approach means you improve consistently over time"
                ],
                problems: [
                    "You overthink and test too many variables, losing consistency",
                    "Your rhythm is inconsistent - sometimes too slow, sometimes scattered"
                ],
                fixes: [
                    "Lock in your winning formula and stop reinventing - document your playbook",
                    "Test one variable at a time, then scale what works consistently"
                ]
            },
            squid: {
                icon: "🦑",
                title: "The Squid",
                subtitle: "The Invisible Sender",
                meaning: "Your emails vanish into the void - invisible and forgettable.",
                strengths: [
                    "You're probably not annoying anyone since they're not seeing your emails anyway",
                    "You have room for massive improvement with small technical fixes"
                ],
                problems: [
                    "Your deliverability is broken or your emails land in spam",
                    "Your messaging is so bland that prospects scroll right past it"
                ],
                fixes: [
                    "Fix email infrastructure now: SPF, DKIM, DMARC, separate warmed domain",
                    "Rewrite subject lines for curiosity and lead with insights, not pitches"
                ]
            },
            seal: {
                icon: "🦭",
                title: "The Seal",
                subtitle: "The Friendly Relationship Builder",
                meaning: "You're friendly and relationship-focused, warm and conversational in your approach.",
                strengths: [
                    "Prospects actually like you and remember you positively",
                    "You build genuine relationships that can pay off long-term"
                ],
                problems: [
                    "You're too nice and indirect - scared to ask for meetings",
                    "Your emails meander without clear urgency or direct CTAs"
                ],
                fixes: [
                    "Be direct - clearly ask for the meeting after building rapport",
                    "Double your outreach volume while maintaining your personal touch"
                ]
            },
            starfish: {
                icon: "⭐",
                title: "The Starfish",
                subtitle: "The Balanced Performer",
                meaning: "You balance everything well - volume, personalization, persistence, and testing.",
                strengths: [
                    "You've figured out what works and execute it consistently",
                    "Your approach is sustainable and gets results without burning out"
                ],
                problems: [
                    "You're a top performer but risk getting comfortable",
                    "You're optimizing incrementally instead of testing bigger swings"
                ],
                fixes: [
                    "Document your playbook so others can replicate your success",
                    "Test contrarian approaches with 10% of outreach - push boundaries"
                ]
            },
            turtle: {
                icon: "🐢",
                title: "The Turtle",
                subtitle: "The Patient Hesitator",
                meaning: "You're patient and methodical, overthinking every detail before sending.",
                strengths: [
                    "Your emails are thoughtful and well-researched when you send them",
                    "You rarely make careless mistakes or burn bridges with rushed outreach"
                ],
                problems: [
                    "You're too slow between follow-ups - prospects forget you exist",
                    "Your hesitation and perfectionism cost you deals and momentum"
                ],
                fixes: [
                    "Speed up to 5-7 days between follow-ups and commit to 4-5 touches minimum",
                    "Cut research time to 3-5 minutes - perfectionism is killing your momentum"
                ]
            },
            crab: {
                icon: "🦀",
                title: "The Crab",
                subtitle: "The Defensive Avoider",
                meaning: "You're defensive and indirect, avoiding direct asks or clear positioning.",
                strengths: [
                    "You don't come across as salesy or aggressive",
                    "You're comfortable staying in your lane without chasing trends"
                ],
                problems: [
                    "You sidestep clear value propositions with vague, meandering messages",
                    "You're stuck in your shell - resistant to feedback and unwilling to adapt"
                ],
                fixes: [
                    "Be direct with your value proposition and what you're asking for",
                    "Test new approaches weekly - your resistance to change is keeping you mediocre"
                ]
            }
        };

        let currentQuestionIndex = 0;
        const answers = {};

        function startQuiz() {
            document.getElementById('hero-section').style.display = 'none';
            document.getElementById('creatures-showcase').style.display = 'none';
            document.getElementById('quiz-intro').style.display = 'none';
            document.getElementById('quiz-section').classList.add('active');
            displayQuestion();
        }

        function displayQuestion() {
            const question = questions[currentQuestionIndex];
            const questionDisplay = document.getElementById('question-display');
            
            questionDisplay.innerHTML = `
                <div class="question-container">
                    <span class="question-number">Question ${currentQuestionIndex + 1} of 20</span>
                    <h3>${question.question}</h3>
                    <div class="options">
                        ${question.options.map(opt => `
                            <div class="option ${answers[question.id] === opt.value ? 'selected' : ''}" 
                                 onclick="selectOption(${question.id}, '${opt.value}')">
                                ${opt.text}
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;

            updateProgress();
            updateButtons();
        }

        function selectOption(questionId, value) {
            answers[questionId] = value;
            
            // Update UI
            document.querySelectorAll('.option').forEach(opt => {
                opt.classList.remove('selected');
            });
            event.target.classList.add('selected');
            
            // Enable next button
            document.getElementById('next-btn').disabled = false;
        }

        function updateProgress() {
            const progress = ((currentQuestionIndex + 1) / questions.length) * 100;
            document.getElementById('progress').style.width = progress + '%';
            document.getElementById('current-question').textContent = `Question ${currentQuestionIndex + 1} of 20`;
            document.getElementById('progress-percent').textContent = Math.round(progress) + '%';
        }

        function updateButtons() {
            const prevBtn = document.getElementById('prev-btn');
            const nextBtn = document.getElementById('next-btn');

            prevBtn.style.display = currentQuestionIndex > 0 ? 'block' : 'none';
            
            if (currentQuestionIndex === questions.length - 1) {
                nextBtn.textContent = 'Show My Result →';
            } else {
                nextBtn.textContent = 'Next →';
            }

            // Check if current question is answered
            const currentQuestion = questions[currentQuestionIndex];
            nextBtn.disabled = !answers[currentQuestion.id];
        }

        function nextQuestion() {
            if (currentQuestionIndex < questions.length - 1) {
                currentQuestionIndex++;
                displayQuestion();
            } else {
                showResult();
            }
        }

        function prevQuestion() {
            if (currentQuestionIndex > 0) {
                currentQuestionIndex--;
                displayQuestion();
            }
        }

        function calculatePersonality() {
            const scores = {
                whale: 0,
                shark: 0,
                octopus: 0,
                squid: 0,
                seal: 0,
                starfish: 0,
                turtle: 0,
                crab: 0
            };

            // Whale indicators
            if (answers[1] === 'whale') scores.whale += 3;
            if (answers[2] === 'surface' || answers[2] === 'none') scores.whale += 2;
            if (answers[4] === 'generic' || answers[4] === 'pitch') scores.whale += 2;
            if (answers[16] === 'broad' || answers[16] === 'anyone') scores.whale += 2;
            if (answers[15] === 'notrack') scores.whale += 2;

            // Shark indicators
            if (answers[6] === 'never' || answers[6] === 'determined') scores.shark += 3;
            if (answers[7] === 'lightning') scores.shark += 2;
            if (answers[8] === 'aggressive') scores.shark += 3;
            if (answers[10] === 'didntsee' || answers[10] === 'moretouches') scores.shark += 2;
            if (answers[20] === 'meetings') scores.shark += 2;

            // Octopus indicators
            if (answers[2] === 'quick') scores.octopus += 2;
            if (answers[6] === 'gentle' || answers[6] === 'determined') scores.octopus += 2;
            if (answers[4] === 'unique' || answers[4] === 'specific') scores.octopus += 2;
            if (answers[12] === 'always' || answers[12] === 'occasionally') scores.octopus += 3;
            if (answers[15] === 'replies' || answers[15] === 'meetings') scores.octopus += 2;
            if (answers[19] === 'mix') scores.octopus += 2;

            // Squid indicators
            if (answers[15] === 'notrack' || answers[15] === 'opens') scores.squid += 3;
            if (answers[18] === 'basic' || answers[18] === 'none') scores.squid += 3;
            if (answers[13] === 'none' || answers[13] === 'basic') scores.squid += 2;
            if (answers[4] === 'pitch') scores.squid += 2;
            if (answers[9] === 'formal') scores.squid += 2;
            if (answers[17] === 'never') scores.squid += 2;

            // Seal indicators
            if (answers[1] === 'snail' || answers[1] === 'fish') scores.seal += 2;
            if (answers[9] === 'personal') scores.seal += 2;
            if (answers[5] === 'question') scores.seal += 2;
            if (answers[11] === 'smallask' || answers[11] === 'noask') scores.seal += 3;
            if (answers[7] === 'steady' || answers[7] === 'slow') scores.seal += 2;
            if (answers[20] === 'conversations') scores.seal += 2;

            // Starfish indicators
            if (answers[1] === 'shark') scores.starfish += 2;
            if (answers[2] === 'quick' || answers[2] === 'deep') scores.starfish += 2;
            if (answers[4] === 'unique') scores.starfish += 2;
            if (answers[6] === 'determined') scores.starfish += 2;
            if (answers[7] === 'lightning' || answers[7] === 'quick') scores.starfish += 2;
            if (answers[8] === 'standard') scores.starfish += 2;
            if (answers[5] === 'value') scores.starfish += 2;
            if (answers[12] === 'always') scores.starfish += 2;
            if (answers[18] === 'full') scores.starfish += 2;
            if (answers[19] === 'custom' || answers[19] === 'fullcustom') scores.starfish += 2;

            // Turtle indicators
            if (answers[1] === 'snail') scores.turtle += 3;
            if (answers[2] === 'deep') scores.turtle += 2;
            if (answers[6] === 'none' || answers[6] === 'gentle') scores.turtle += 3;
            if (answers[7] === 'slow') scores.turtle += 2;
            if (answers[8] === 'patient' || answers[8] === 'verypatient') scores.turtle += 3;
            if (answers[10] === 'timing' || answers[10] === 'wrongfit') scores.turtle += 2;
            if (answers[12] === 'rarely' || answers[12] === 'never') scores.turtle += 2;

            // Crab indicators
            if (answers[11] === 'noask') scores.crab += 3;
            if (answers[14] === 'ignore') scores.crab += 3;
            if (answers[17] === 'rarely' || answers[17] === 'never') scores.crab += 2;
            if (answers[9] === 'formal') scores.crab += 2;
            if (answers[12] === 'rarely' || answers[12] === 'never') scores.crab += 2;
            if (answers[19] === 'sequence') scores.crab += 2;

            let maxScore = 0;
            let resultPersonality = 'octopus';
            
            for (let [personality, score] of Object.entries(scores)) {
                if (score > maxScore) {
                    maxScore = score;
                    resultPersonality = personality;
                }
            }

            return resultPersonality;
        }

        function showResult() {
            const personalityType = calculatePersonality();
            const personality = personalities[personalityType];
            
            document.getElementById('quiz-section').classList.remove('active');
            document.getElementById('quiz-section').style.display = 'none';
            
            const resultContainer = document.getElementById('result-container');
            resultContainer.innerHTML = `
                <span class="personality-icon-large">${personality.icon}</span>
                <h2 class="personality-title">${personality.title}</h2>
                <p class="personality-subtitle">${personality.subtitle}</p>
                
                <div class="personality-meaning">
                    ${personality.meaning}
                </div>

                <div class="personality-section">
                    <h4><span class="section-icon">💪</span> Your Strengths</h4>
                    <ul>
                        ${personality.strengths.map(s => `<li>${s}</li>`).join('')}
                    </ul>
                </div>

                <div class="personality-section">
                    <h4><span class="section-icon">⚠️</span> The Problem</h4>
                    <ul>
                        ${personality.problems.map(p => `<li>${p}</li>`).join('')}
                    </ul>
                </div>

                <div class="personality-section">
                    <h4><span class="section-icon">🎯</span> What to Fix</h4>
                    <ul>
                        ${personality.fixes.map(f => `<li>${f}</li>`).join('')}
                    </ul>
                </div>

                <button class="restart-btn" onclick="location.reload()">Take Quiz Again</button>
            `;
            
            resultContainer.classList.add('active');
            resultContainer.style.display = 'block';
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
    </script>
</body>
</html>
