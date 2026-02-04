# Outbound Behavior Test
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Find Your Outbound Personality</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            padding: 40px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
        }

        .header {
            text-align: center;
            margin-bottom: 40px;
        }

        .header h1 {
            color: #333;
            font-size: 2.5em;
            margin-bottom: 10px;
        }

        .header p {
            color: #666;
            font-size: 1.1em;
        }

        .question-container {
            margin-bottom: 35px;
            padding: 25px;
            background: #f8f9fa;
            border-radius: 12px;
            border-left: 4px solid #667eea;
        }

        .question-container h3 {
            color: #333;
            margin-bottom: 15px;
            font-size: 1.2em;
        }

        .options {
            display: flex;
            flex-direction: column;
            gap: 12px;
        }

        .option {
            padding: 15px 20px;
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1em;
        }

        .option:hover {
            border-color: #667eea;
            background: #f0f4ff;
            transform: translateX(5px);
        }

        .option.selected {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }

        .submit-btn {
            display: block;
            width: 100%;
            padding: 18px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            margin-top: 30px;
            transition: transform 0.2s;
        }

        .submit-btn:hover {
            transform: scale(1.02);
        }

        .submit-btn:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }

        .result-container {
            display: none;
            text-align: center;
            animation: fadeIn 0.5s;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .personality-icon {
            font-size: 120px;
            margin: 20px 0;
        }

        .personality-title {
            font-size: 2.5em;
            color: #333;
            margin-bottom: 10px;
        }

        .personality-subtitle {
            font-size: 1.3em;
            color: #666;
            margin-bottom: 30px;
            font-style: italic;
        }

        .personality-section {
            text-align: left;
            margin: 25px 0;
            padding: 20px;
            background: #f8f9fa;
            border-radius: 10px;
        }

        .personality-section h4 {
            color: #667eea;
            font-size: 1.3em;
            margin-bottom: 12px;
        }

        .personality-section ul {
            list-style: none;
            padding-left: 0;
        }

        .personality-section li {
            padding: 8px 0;
            padding-left: 25px;
            position: relative;
            color: #444;
            line-height: 1.6;
        }

        .personality-section li:before {
            content: "•";
            position: absolute;
            left: 0;
            color: #667eea;
            font-weight: bold;
            font-size: 1.5em;
        }

        .restart-btn {
            margin-top: 30px;
            padding: 15px 40px;
            background: white;
            color: #667eea;
            border: 2px solid #667eea;
            border-radius: 8px;
            font-size: 1.1em;
            cursor: pointer;
            transition: all 0.3s;
        }

        .restart-btn:hover {
            background: #667eea;
            color: white;
        }

        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 10px;
            margin-bottom: 30px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea 0%, #764ba2 100%);
            width: 0%;
            transition: width 0.3s ease;
        }

        @media (max-width: 600px) {
            .container {
                padding: 25px;
            }
            
            .header h1 {
                font-size: 1.8em;
            }
            
            .personality-title {
                font-size: 2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🌊 Find Your Outbound Personality</h1>
            <p>Discover what type of cold emailer you are</p>
        </div>

        <div id="quiz-container">
            <div class="progress-bar">
                <div class="progress-fill" id="progress"></div>
            </div>

            <form id="quiz-form">
                <!-- Questions will be inserted here by JavaScript -->
            </form>

            <button type="button" class="submit-btn" id="submit-btn" disabled>Show My Personality</button>
        </div>

        <div id="result-container" class="result-container">
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

        const answers = {};
        let totalQuestions = questions.length;

        function renderQuestions() {
            const form = document.getElementById('quiz-form');
            questions.forEach((q, index) => {
                const questionDiv = document.createElement('div');
                questionDiv.className = 'question-container';
                questionDiv.innerHTML = `
                    <h3>${index + 1}. ${q.question}</h3>
                    <div class="options" id="options-${q.id}">
                        ${q.options.map(opt => `
                            <div class="option" data-question="${q.id}" data-value="${opt.value}">
                                ${opt.text}
                            </div>
                        `).join('')}
                    </div>
                `;
                form.appendChild(questionDiv);
            });

            // Add click handlers
            document.querySelectorAll('.option').forEach(option => {
                option.addEventListener('click', function() {
                    const questionId = this.dataset.question;
                    const value = this.dataset.value;
                    
                    // Remove selected from siblings
                    document.querySelectorAll(`[data-question="${questionId}"]`).forEach(opt => {
                        opt.classList.remove('selected');
                    });
                    
                    // Add selected to this option
                    this.classList.add('selected');
                    
                    // Store answer
                    answers[questionId] = value;
                    
                    // Update progress
                    updateProgress();
                    
                    // Enable submit if all answered
                    checkAllAnswered();
                });
            });
        }

        function updateProgress() {
            const answered = Object.keys(answers).length;
            const percentage = (answered / totalQuestions) * 100;
            document.getElementById('progress').style.width = percentage + '%';
        }

        function checkAllAnswered() {
            const submitBtn = document.getElementById('submit-btn');
            if (Object.keys(answers).length === totalQuestions) {
                submitBtn.disabled = false;
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

            // Scoring logic based on the patterns
            
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

            // Find highest score
            let maxScore = 0;
            let resultPersonality = 'octopus'; // default
            
            for (let [personality, score] of Object.entries(scores)) {
                if (score > maxScore) {
                    maxScore = score;
                    resultPersonality = personality;
                }
            }

            return resultPersonality;
        }

        function showResult(personalityType) {
            const personality = personalities[personalityType];
            const quizContainer = document.getElementById('quiz-container');
            const resultContainer = document.getElementById('result-container');

            resultContainer.innerHTML = `
                <div class="personality-icon">${personality.icon}</div>
                <h2 class="personality-title">${personality.title}</h2>
                <p class="personality-subtitle">${personality.subtitle}</p>
                
                <div class="personality-section">
                    <h4>What This Means</h4>
                    <p>${personality.meaning}</p>
                </div>

                <div class="personality-section">
                    <h4>Your Strengths</h4>
                    <ul>
                        ${personality.strengths.map(s => `<li>${s}</li>`).join('')}
                    </ul>
                </div>

                <div class="personality-section">
                    <h4>The Problem</h4>
                    <ul>
                        ${personality.problems.map(p => `<li>${p}</li>`).join('')}
                    </ul>
                </div>

                <div class="personality-section">
                    <h4>What to Fix</h4>
                    <ul>
                        ${personality.fixes.map(f => `<li>${f}</li>`).join('')}
                    </ul>
                </div>

                <button class="restart-btn" onclick="location.reload()">Take Quiz Again</button>
            `;

            quizContainer.style.display = 'none';
            resultContainer.style.display = 'block';
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Initialize
        renderQuestions();

        document.getElementById('submit-btn').addEventListener('click', function() {
            const result = calculatePersonality();
            showResult(result);
        });
    </script>
</body>
</html>
