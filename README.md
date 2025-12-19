<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Luna AI - Career Guidance Bot</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            height: 100vh;
            overflow: hidden;
        }

        .chat-container {
            width: 100vw;
            height: 100vh;
            background: #ffffff;
            display: flex;
            flex-direction: column;
        }

        .chat-header {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 20px 30px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
            flex-shrink: 0;
        }

        .header-left {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .bot-avatar {
            width: 50px;
            height: 50px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 26px;
            backdrop-filter: blur(10px);
        }

        .header-info h1 {
            font-size: 24px;
            font-weight: 600;
            margin-bottom: 2px;
        }

        .header-info p {
            font-size: 13px;
            opacity: 0.95;
            margin-bottom: 3px;
        }

        .header-info .developer-credit {
            font-size: 11px;
            opacity: 0.85;
            font-style: italic;
        }

        .status-indicator {
            display: flex;
            align-items: center;
            gap: 8px;
            background: rgba(255, 255, 255, 0.2);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 13px;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            background: #4ade80;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% {
                opacity: 1;
            }
            50% {
                opacity: 0.5;
            }
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: 25px;
            background: linear-gradient(to bottom, #f8f9fa 0%, #ffffff 100%);
        }

        .chat-messages::-webkit-scrollbar {
            width: 8px;
        }

        .chat-messages::-webkit-scrollbar-track {
            background: #f1f1f1;
        }

        .chat-messages::-webkit-scrollbar-thumb {
            background: #667eea;
            border-radius: 4px;
        }

        .message {
            margin-bottom: 20px;
            display: flex;
            gap: 12px;
            animation: fadeIn 0.4s ease-out;
            max-width: 85%;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: translateY(15px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .message.bot {
            justify-content: flex-start;
        }

        .message.user {
            justify-content: flex-end;
            margin-left: auto;
        }

        .message-avatar {
            width: 38px;
            height: 38px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
            flex-shrink: 0;
        }

        .bot .message-avatar {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            box-shadow: 0 4px 8px rgba(102, 126, 234, 0.3);
        }

        .user .message-avatar {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            box-shadow: 0 4px 8px rgba(240, 147, 251, 0.3);
        }

        .message-content {
            padding: 14px 18px;
            border-radius: 16px;
            line-height: 1.6;
            word-wrap: break-word;
            font-size: 14.5px;
        }

        .bot .message-content {
            background: #ffffff;
            color: #2d3748;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
            border: 1px solid #e2e8f0;
        }

        .user .message-content {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            box-shadow: 0 2px 8px rgba(102, 126, 234, 0.3);
        }

        .course-buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 15px;
        }

        .course-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 13.5px;
            font-weight: 500;
            transition: all 0.3s ease;
            box-shadow: 0 2px 6px rgba(102, 126, 234, 0.3);
        }

        .course-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 16px rgba(102, 126, 234, 0.4);
        }

        .course-btn:active {
            transform: translateY(-1px);
        }

        .job-card {
            background: linear-gradient(to right, #f8f9fa 0%, #ffffff 100%);
            padding: 15px;
            border-radius: 12px;
            margin-top: 12px;
            border-left: 4px solid #667eea;
            box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
            transition: transform 0.2s;
        }

        .job-card:hover {
            transform: translateX(4px);
        }

        .job-card h4 {
            color: #667eea;
            margin-bottom: 8px;
            font-size: 15.5px;
            font-weight: 600;
        }

        .job-card p {
            color: #4a5568;
            font-size: 13.5px;
            margin-bottom: 6px;
            line-height: 1.5;
        }

        .salary {
            color: #10b981;
            font-weight: 600;
            font-size: 14px;
        }

        .chat-input-area {
            padding: 18px 25px 22px 25px;
            background: #ffffff;
            border-top: 1px solid #e2e8f0;
            box-shadow: 0 -4px 12px rgba(0, 0, 0, 0.05);
            flex-shrink: 0;
        }

        .footer-credit {
            text-align: center;
            font-size: 11px;
            color: #718096;
            margin-bottom: 12px;
            font-style: italic;
        }

        .footer-credit strong {
            color: #667eea;
            font-weight: 600;
        }

        .input-container {
            display: flex;
            gap: 12px;
            max-width: 1200px;
            margin: 0 auto;
        }

        #userInput {
            flex: 1;
            padding: 16px 22px;
            border: 2px solid #e2e8f0;
            border-radius: 26px;
            font-size: 15px;
            outline: none;
            transition: all 0.3s;
            background: #f8f9fa;
        }

        #userInput:focus {
            border-color: #667eea;
            background: #ffffff;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }

        #sendBtn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 16px 34px;
            border-radius: 26px;
            cursor: pointer;
            font-size: 15px;
            font-weight: 600;
            transition: all 0.3s;
            box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
        }

        #sendBtn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 16px rgba(102, 126, 234, 0.4);
        }

        #sendBtn:active {
            transform: translateY(0);
        }

        .typing-indicator {
            display: none;
        }

        .typing-indicator .message-content {
            padding: 14px 20px;
        }

        .typing-indicator span {
            display: inline-block;
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background: #667eea;
            margin: 0 3px;
            animation: typing 1.4s infinite;
        }

        .typing-indicator span:nth-child(2) {
            animation-delay: 0.2s;
        }

        .typing-indicator span:nth-child(3) {
            animation-delay: 0.4s;
        }

        @keyframes typing {
            0%, 60%, 100% {
                transform: translateY(0);
                opacity: 0.5;
            }
            30% {
                transform: translateY(-12px);
                opacity: 1;
            }
        }

        .welcome-text {
            font-size: 15px;
            line-height: 1.8;
        }

        .welcome-text strong {
            color: #667eea;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="chat-container">
        <div class="chat-header">
            <div class="header-left">
                <div class="bot-avatar">🌙</div>
                <div class="header-info">
                    <h1>Luna AI</h1>
                    <p>Professional Career Guidance Assistant</p>
                    <p class="developer-credit">Developed by BCA AI A1 PRABHU AND TEAM</p>
                </div>
            </div>
            <div class="status-indicator">
                <span class="status-dot"></span>
                <span>Online</span>
            </div>
        </div>

        <div class="chat-messages" id="chatMessages">
            <!-- Messages will appear here -->
        </div>

        <div class="chat-input-area">
            <div class="footer-credit">
                💻 Developed by <strong>BCA AI A1 PRABHU AND TEAM</strong> 🚀
            </div>
            <div class="input-container">
                <input type="text" id="userInput" placeholder="Type your message here..." autocomplete="off">
                <button id="sendBtn">Send 📤</button>
            </div>
        </div>
    </div>

    <script>
        const chatMessages = document.getElementById('chatMessages');
        const userInput = document.getElementById('userInput');
        const sendBtn = document.getElementById('sendBtn');
        let conversationState = 'initial';
        let selectedCourse = '';

        const jobData = {
            'BCA': [
                {
                    title: 'Software Developer',
                    description: 'Design, develop, and maintain software applications using modern programming languages',
                    salary: '₹3.5-8 LPA',
                    skills: 'Java, Python, C++, Problem Solving, Git'
                },
                {
                    title: 'Web Developer',
                    description: 'Create responsive and dynamic websites and web applications',
                    salary: '₹3-7 LPA',
                    skills: 'HTML, CSS, JavaScript, React, Node.js, APIs'
                },
                {
                    title: 'Database Administrator',
                    description: 'Manage, maintain, and secure database systems for organizations',
                    salary: '₹4-9 LPA',
                    skills: 'SQL, MongoDB, Oracle, PostgreSQL, Data Security'
                },
                {
                    title: 'System Analyst',
                    description: 'Analyze and design information systems to meet business needs',
                    salary: '₹4-8 LPA',
                    skills: 'Business Analysis, UML, Technical Documentation, Communication'
                },
                {
                    title: 'Mobile App Developer',
                    description: 'Develop native and cross-platform mobile applications',
                    salary: '₹3.5-10 LPA',
                    skills: 'Android, iOS, Flutter, React Native, UI/UX'
                }
            ],
            'BCA AI': [
                {
                    title: 'Machine Learning Engineer',
                    description: 'Build and deploy ML models for predictive analytics and automation',
                    salary: '₹6-15 LPA',
                    skills: 'Python, TensorFlow, PyTorch, Scikit-learn, Deep Learning'
                },
                {
                    title: 'AI Research Scientist',
                    description: 'Conduct cutting-edge research in artificial intelligence and neural networks',
                    salary: '₹8-20 LPA',
                    skills: 'Research Methodology, Neural Networks, Mathematics, Python'
                },
                {
                    title: 'Data Scientist',
                    description: 'Extract insights from complex data using statistical analysis and ML',
                    salary: '₹5-14 LPA',
                    skills: 'Python, R, Statistics, Machine Learning, Data Visualization'
                },
                {
                    title: 'Computer Vision Engineer',
                    description: 'Develop AI systems that interpret and analyze visual information',
                    salary: '₹6-16 LPA',
                    skills: 'OpenCV, Deep Learning, CNNs, Image Processing, Python'
                },
                {
                    title: 'NLP Engineer',
                    description: 'Build natural language processing applications like chatbots and translators',
                    salary: '₹6-15 LPA',
                    skills: 'NLP, Transformers, BERT, GPT, Language Models, Python'
                }
            ],
            'BCOM': [
                {
                    title: 'Chartered Accountant',
                    description: 'Provide expert financial advice, auditing, and taxation services',
                    salary: '₹6-15 LPA',
                    skills: 'Accounting, Taxation, Auditing, Financial Analysis, GST'
                },
                {
                    title: 'Financial Analyst',
                    description: 'Analyze financial data and provide investment recommendations',
                    salary: '₹4-10 LPA',
                    skills: 'Financial Modeling, Excel, Market Analysis, Forecasting'
                },
                {
                    title: 'Tax Consultant',
                    description: 'Provide tax planning, compliance, and advisory services',
                    salary: '₹3.5-9 LPA',
                    skills: 'Income Tax, GST, Tax Laws, Compliance, Planning'
                },
                {
                    title: 'Investment Banker',
                    description: 'Assist companies with mergers, acquisitions, and capital raising',
                    salary: '₹8-20 LPA',
                    skills: 'Financial Markets, M&A, Valuation, Corporate Finance'
                },
                {
                    title: 'Company Secretary',
                    description: 'Ensure corporate compliance with legal and regulatory requirements',
                    salary: '₹5-12 LPA',
                    skills: 'Corporate Law, Compliance, Governance, SEBI Regulations'
                }
            ],
            'BSC': [
                {
                    title: 'Research Scientist',
                    description: 'Conduct scientific research in specialized fields like physics, chemistry, or biology',
                    salary: '₹4-12 LPA',
                    skills: 'Research Methodology, Lab Skills, Analysis, Scientific Writing'
                },
                {
                    title: 'Data Analyst',
                    description: 'Analyze scientific and business data to derive actionable insights',
                    salary: '₹3.5-8 LPA',
                    skills: 'Statistics, Python, R, Excel, Data Visualization, SQL'
                },
                {
                    title: 'Quality Control Analyst',
                    description: 'Ensure product quality and compliance in pharmaceutical and manufacturing industries',
                    salary: '₹3-7 LPA',
                    skills: 'Quality Standards, Testing Protocols, Documentation, GMP'
                },
                {
                    title: 'Environmental Consultant',
                    description: 'Advise organizations on environmental impact and sustainability practices',
                    salary: '₹4-10 LPA',
                    skills: 'Environmental Science, EIA, Regulations, Auditing'
                },
                {
                    title: 'Laboratory Technician',
                    description: 'Operate lab equipment and conduct experiments in research facilities',
                    salary: '₹2.5-6 LPA',
                    skills: 'Lab Techniques, Equipment Handling, Safety Protocols, Analysis'
                }
            ],
            'BBA': [
                {
                    title: 'Business Analyst',
                    description: 'Analyze business processes and recommend strategic improvements',
                    salary: '₹4-10 LPA',
                    skills: 'Business Strategy, Data Analysis, SQL, Communication, Problem Solving'
                },
                {
                    title: 'Marketing Manager',
                    description: 'Plan and execute marketing campaigns to promote products and services',
                    salary: '₹5-12 LPA',
                    skills: 'Digital Marketing, SEO/SEM, Brand Management, Analytics'
                },
                {
                    title: 'Human Resource Manager',
                    description: 'Manage recruitment, training, and employee relations for organizations',
                    salary: '₹4-10 LPA',
                    skills: 'HR Management, Recruitment, Training, Employee Relations'
                },
                {
                    title: 'Operations Manager',
                    description: 'Oversee daily business operations to ensure efficiency and productivity',
                    salary: '₹5-12 LPA',
                    skills: 'Operations Management, Process Optimization, Lean Six Sigma'
                },
                {
                    title: 'Sales Manager',
                    description: 'Lead sales teams and develop strategies to drive revenue growth',
                    salary: '₹4-15 LPA',
                    skills: 'Sales Strategy, Team Leadership, CRM, Client Relations, Negotiation'
                }
            ]
        };

        function addMessage(text, isUser, includeButtons = false) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${isUser ? 'user' : 'bot'}`;
            
            const avatar = document.createElement('div');
            avatar.className = 'message-avatar';
            avatar.textContent = isUser ? '👤' : '🌙';
            
            const content = document.createElement('div');
            content.className = 'message-content';
            content.innerHTML = text;
            
            if (!isUser) {
                messageDiv.appendChild(avatar);
            }
            messageDiv.appendChild(content);
            if (isUser) {
                messageDiv.appendChild(avatar);
            }
            
            if (includeButtons) {
                const buttonsDiv = document.createElement('div');
                buttonsDiv.className = 'course-buttons';
                const courses = ['BCA', 'BCA AI', 'BCOM', 'BSC', 'BBA'];
                courses.forEach(course => {
                    const btn = document.createElement('button');
                    btn.className = 'course-btn';
                    btn.textContent = course;
                    btn.onclick = () => handleCourseSelection(course);
                    buttonsDiv.appendChild(btn);
                });
                content.appendChild(buttonsDiv);
            }
            
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function showTypingIndicator() {
            const typingDiv = document.createElement('div');
            typingDiv.className = 'message bot typing-indicator';
            typingDiv.id = 'typingIndicator';
            typingDiv.innerHTML = `
                <div class="message-avatar">🌙</div>
                <div class="message-content">
                    <span></span><span></span><span></span>
                </div>
            `;
            typingDiv.style.display = 'flex';
            chatMessages.appendChild(typingDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function hideTypingIndicator() {
            const typing = document.getElementById('typingIndicator');
            if (typing) typing.remove();
        }

        function handleCourseSelection(course) {
            selectedCourse = course;
            addMessage(course, true);
            
            setTimeout(() => {
                showTypingIndicator();
                setTimeout(() => {
                    hideTypingIndicator();
                    displayJobRoles(course);
                }, 1200);
            }, 300);
        }

        function displayJobRoles(course) {
            const jobs = jobData[course];
            let response = `<div class="welcome-text"><strong>🎯 Top Career Opportunities for ${course} Graduates:</strong><br><br>Here are the most promising career paths you can pursue:</div>`;
            
            jobs.forEach((job, index) => {
                response += `
                    <div class="job-card">
                        <h4>${index + 1}. ${job.title}</h4>
                        <p><strong>📋 Role:</strong> ${job.description}</p>
                        <p><strong>🛠️ Skills Required:</strong> ${job.skills}</p>
                        <p class="salary">💰 Average Salary: ${job.salary}</p>
                    </div>
                `;
            });
            
            response += `<br><div class="welcome-text">Would you like to know more about any specific role or explore another course? 😊</div>`;
            addMessage(response, false);
            conversationState = 'job_displayed';
        }

        function handleUserMessage(message) {
            const lowerMessage = message.toLowerCase().trim();
            
            if (lowerMessage === 'hi' || lowerMessage === 'hello' || lowerMessage === 'hey' || lowerMessage === 'start') {
                showTypingIndicator();
                setTimeout(() => {
                    hideTypingIndicator();
                    const welcomeMsg = `
                        <div class="welcome-text">
                            <strong>👋 Hello! Welcome to Luna AI Career Guidance!</strong><br><br>
                            I'm Luna, your dedicated AI career assistant. I'm here to help you discover exciting job opportunities tailored to your degree! 🎓✨<br><br>
                            <strong>🎓 I provide comprehensive career guidance for:</strong><br>
                            • <strong>BCA</strong> - Bachelor of Computer Applications<br>
                            • <strong>BCA AI</strong> - BCA with Artificial Intelligence Specialization<br>
                            • <strong>BCOM</strong> - Bachelor of Commerce<br>
                            • <strong>BSC</strong> - Bachelor of Science<br>
                            • <strong>BBA</strong> - Bachelor of Business Administration<br><br>
                            <strong>✨ Select your course below to explore amazing career paths and opportunities! 🚀</strong>
                        </div>
                    `;
                    addMessage(welcomeMsg, false, true);
                    conversationState = 'course_selection';
                }, 1200);
            } else if (['bca', 'bca ai', 'bcom', 'bsc', 'bse', 'bba'].includes(lowerMessage)) {
                let course = lowerMessage.toUpperCase();
                if (course === 'BSE') course = 'BSC';
                handleCourseSelection(course);
            } else if (lowerMessage.includes('salary') || lowerMessage.includes('pay') || lowerMessage.includes('package')) {
                showTypingIndicator();
                setTimeout(() => {
                    hideTypingIndicator();
                    addMessage('💰 <strong>About Salaries:</strong> The salary ranges I provided are for freshers to 3 years of experience in India. Actual salaries vary based on:<br>• Company size and reputation<br>• Location (metro vs non-metro cities)<br>• Your skills and certifications<br>• Industry demand<br><br>Would you like to know about any specific role? 😊', false);
                }, 1000);
            } else if (lowerMessage.includes('skill') || lowerMessage.includes('learn') || lowerMessage.includes('course')) {
                showTypingIndicator();
                setTimeout(() => {
                    hideTypingIndicator();
                    addMessage('🎯 <strong>Skill Development Tips:</strong><br>• Focus on hands-on projects and real-world applications<br>• Build a strong portfolio showcasing your work<br>• Pursue relevant internships<br>• Take online certifications from platforms like Coursera, Udemy<br>• Network with professionals in your field<br><br>Which role would you like specific guidance on? 🚀', false);
                }, 1000);
            } else if (lowerMessage.includes('thank')) {
                showTypingIndicator();
                setTimeout(() => {
                    hideTypingIndicator();
                    addMessage("You're very welcome! 😊 I'm always here to help you with career guidance. Feel free to explore more courses or ask any questions. Best wishes for your career journey! 🌟", false);
                }, 1000);
            } else if (lowerMessage.includes('help') || lowerMessage === '?') {
                showTypingIndicator();
                setTimeout(() => {
                    hideTypingIndicator();
                    addMessage("🤝 <strong>How I Can Help:</strong><br>• Choose a course to see job roles<br>• Ask about salaries for different positions<br>• Get skill development advice<br>• Learn about specific career paths<br>• Explore requirements for roles<br><br>Just type your question or select a course! 💼", false, conversationState !== 'job_displayed');
                }, 1000);
            } else {
                showTypingIndicator();
                setTimeout(() => {
                    hideTypingIndicator();
                    if (conversationState === 'initial') {
                        addMessage("👋 Hello there! Please start by typing <strong>'Hi'</strong> to begin your exciting career exploration journey with me! 🚀", false);
                    } else {
                        addMessage("I'm here to guide you! 😊 I can help with career information for <strong>BCA, BCA AI, BCOM, BSC, and BBA</strong>. You can:<br>• Select a course<br>• Ask about salaries, skills, or specific roles<br>• Get career advice<br><br>What would you like to know? 💡", false, conversationState === 'course_selection');
                    }
                }, 1000);
            }
        }

        function sendMessage() {
            const message = userInput.value.trim();
            if (message === '') return;
            
            addMessage(message, true);
            userInput.value = '';
            
            setTimeout(() => {
                handleUserMessage(message);
            }, 300);
        }

        sendBtn.addEventListener('click', sendMessage);
        userInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') {
                sendMessage();
            }
        });

        // Initial greeting
        window.onload = () => {
            setTimeout(() => {
                addMessage("<div class='welcome-text'>👋 <strong>Hi there! I'm Luna, your AI Career Advisor.</strong><br><br>Ready to explore your future career options? Type <strong>'Hi'</strong> to get started! ✨</div>", false);
                conversationState = 'initial';
            }, 600);
        };
    </script>
</body>
</html>
