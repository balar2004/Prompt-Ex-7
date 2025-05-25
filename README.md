# Ex.No:7 Prompt-Based AI Application for Personal Needs
## Aim: 
To Develop a prompt-based application tailored to their personal needs, fostering creativity and practical problem-solving skills while leveraging the capabilities of large language models.


## Algorithm: 
- Create HTML file with basic structure
- Include CSS for styling and JavaScript for functionality
- Set up responsive design framework
- Build task categorization logic (work, personal, health, finance keywords)
- Add priority assignment based on urgency indicators
- Generate time estimates and productivity tips
- Create visual output with color-coded priority levels

## Program:
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prompt-Based Task Organizer</title>
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
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5em;
            margin-bottom: 10px;
            font-weight: 300;
        }

        .header p {
            opacity: 0.9;
            font-size: 1.1em;
        }

        .main-content {
            padding: 30px;
        }

        .input-section {
            background: #f8fafc;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
            border: 2px solid #e2e8f0;
        }

        .input-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #374151;
        }

        textarea {
            width: 100%;
            padding: 15px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            font-size: 16px;
            resize: vertical;
            min-height: 100px;
            transition: border-color 0.3s ease;
        }

        textarea:focus {
            outline: none;
            border-color: #4facfe;
            box-shadow: 0 0 0 3px rgba(79, 172, 254, 0.1);
        }

        .prompt-selector {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .prompt-option {
            padding: 15px;
            border: 2px solid #e2e8f0;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            text-align: center;
            background: white;
        }

        .prompt-option:hover {
            border-color: #4facfe;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }

        .prompt-option.active {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            border-color: #4facfe;
        }

        .prompt-option h3 {
            margin-bottom: 5px;
            font-size: 1.1em;
        }

        .prompt-option p {
            font-size: 0.9em;
            opacity: 0.8;
        }

        .generate-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            width: 100%;
        }

        .generate-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
        }

        .results-section {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-top: 30px;
        }

        .result-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            border: 2px solid #e2e8f0;
        }

        .result-card h3 {
            color: #374151;
            margin-bottom: 15px;
            font-size: 1.3em;
            border-bottom: 2px solid #e2e8f0;
            padding-bottom: 10px;
        }

        .prompt-display {
            background: #f1f5f9;
            padding: 15px;
            border-radius: 8px;
            margin-bottom: 15px;
            font-family: 'Courier New', monospace;
            font-size: 14px;
            color: #475569;
            border-left: 4px solid #4facfe;
        }

        .output-display {
            background: #f8fafc;
            padding: 20px;
            border-radius: 10px;
            border: 1px solid #e2e8f0;
            line-height: 1.6;
        }

        .task-item {
            background: white;
            padding: 12px 15px;
            margin: 8px 0;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            border-left: 4px solid #10b981;
        }

        .priority-high { border-left-color: #ef4444; }
        .priority-medium { border-left-color: #f59e0b; }
        .priority-low { border-left-color: #10b981; }

        @media (max-width: 768px) {
            .results-section {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2em;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🎯 Prompt-Based Task Organizer</h1>
            <p>Discover how prompt design affects AI task organization quality</p>
        </div>

        <div class="main-content">
            <div class="input-section">
                <div class="input-group">
                    <label for="tasks">📝 Enter your daily tasks (one per line):</label>
                    <textarea id="tasks" placeholder="Example:
Buy groceries
Finish project report
Call mom
Go to gym
Pay bills
Read for 30 minutes"></textarea>
                </div>

                <div class="input-group">
                    <label>🎨 Choose Prompt Complexity Level:</label>
                    <div class="prompt-selector">
                        <div class="prompt-option active" data-level="basic">
                            <h3>Basic</h3>
                            <p>Simple organization</p>
                        </div>
                        <div class="prompt-option" data-level="intermediate">
                            <h3>Intermediate</h3>
                            <p>Priority & categories</p>
                        </div>
                        <div class="prompt-option" data-level="advanced">
                            <h3>Advanced</h3>
                            <p>Smart scheduling</p>
                        </div>
                    </div>
                </div>

                <button class="generate-btn" onclick="generateTasks()">
                    ✨ Generate Organized Tasks
                </button>
            </div>

            <div class="results-section" id="results" style="display: none;">
                <div class="result-card">
                    <h3>🔍 Prompt Used</h3>
                    <div class="prompt-display" id="prompt-display"></div>
                </div>
                <div class="result-card">
                    <h3>📋 Organized Output</h3>
                    <div class="output-display" id="output-display"></div>
                </div>
            </div>
        </div>
    </div>

    <script>
        const prompts = {
            basic: "Organize these tasks: {tasks}",
            
            intermediate: `Organize these daily tasks by priority and category:
Tasks: {tasks}

Please organize them into:
1. High Priority (urgent/important)
2. Medium Priority (important but not urgent)  
3. Low Priority (can be done later)

Also group by categories like: Work, Personal, Health, etc.`,

            advanced: `Act as a productivity expert. Analyze and organize these daily tasks:
Tasks: {tasks}

Provide a comprehensive organization including:
1. Priority levels (High/Medium/Low) with reasoning
2. Categories (Work, Personal, Health, Finance, etc.)
3. Estimated time for each task
4. Suggested order of completion
5. Tips for efficiency

Format as a clear, actionable daily plan.`
        };

        const sampleOutputs = {
            basic: {
                tasks: ["Buy groceries", "Finish project report", "Call mom", "Go to gym", "Pay bills", "Read for 30 minutes"],
                output: `<div class="task-item">Buy groceries</div>
<div class="task-item">Finish project report</div>
<div class="task-item">Call mom</div>
<div class="task-item">Go to gym</div>
<div class="task-item">Pay bills</div>
<div class="task-item">Read for 30 minutes</div>`
            },
            
            intermediate: {
                tasks: ["Buy groceries", "Finish project report", "Call mom", "Go to gym", "Pay bills", "Read for 30 minutes"],
                output: `<strong>HIGH PRIORITY:</strong>
<div class="task-item priority-high">Finish project report - Work</div>
<div class="task-item priority-high">Pay bills - Finance</div>

<strong>MEDIUM PRIORITY:</strong>
<div class="task-item priority-medium">Buy groceries - Personal</div>
<div class="task-item priority-medium">Call mom - Personal</div>

<strong>LOW PRIORITY:</strong>
<div class="task-item priority-low">Go to gym - Health</div>
<div class="task-item priority-low">Read for 30 minutes - Personal</div>`
            },
            
            advanced: {
                tasks: ["Buy groceries", "Finish project report", "Call mom", "Go to gym", "Pay bills", "Read for 30 minutes"],
                output: `<strong>🎯 OPTIMIZED DAILY PLAN</strong><br><br>

<strong>HIGH PRIORITY (Complete First):</strong>
<div class="task-item priority-high">
<strong>Finish project report</strong> - Work Category<br>
⏱️ Estimated time: 2-3 hours<br>
💡 Tip: Do this when your energy is highest (morning)
</div>
<div class="task-item priority-high">
<strong>Pay bills</strong> - Finance Category<br>
⏱️ Estimated time: 30 minutes<br>
💡 Tip: Set up auto-pay for recurring bills
</div>

<strong>MEDIUM PRIORITY (Schedule Afternoon):</strong>
<div class="task-item priority-medium">
<strong>Buy groceries</strong> - Personal Category<br>
⏱️ Estimated time: 45 minutes<br>
💡 Tip: Make a list and shop during off-peak hours
</div>
<div class="task-item priority-medium">
<strong>Call mom</strong> - Personal Category<br>
⏱️ Estimated time: 20 minutes<br>
💡 Tip: Call during her preferred time
</div>

<strong>LOW PRIORITY (Evening/Flexible):</strong>
<div class="task-item priority-low">
<strong>Go to gym</strong> - Health Category<br>
⏱️ Estimated time: 1 hour<br>
💡 Tip: Go after work to de-stress
</div>
<div class="task-item priority-low">
<strong>Read for 30 minutes</strong> - Personal Development<br>
⏱️ Estimated time: 30 minutes<br>
💡 Tip: Perfect wind-down activity before bed
</div>

<strong>📅 SUGGESTED TIMELINE:</strong>
9AM-12PM: Project report<br>
12PM-12:30PM: Pay bills<br>
2PM-3PM: Groceries & call mom<br>
6PM-7PM: Gym<br>
9PM-9:30PM: Reading`
            }
        };

        let currentLevel = 'basic';

        // Handle prompt selection
        document.querySelectorAll('.prompt-option').forEach(option => {
            option.addEventListener('click', function() {
                document.querySelectorAll('.prompt-option').forEach(opt => opt.classList.remove('active'));
                this.classList.add('active');
                currentLevel = this.dataset.level;
            });
        });

        function generateTasks() {
            const tasksInput = document.getElementById('tasks').value.trim();
            
            if (!tasksInput) {
                alert('Please enter some tasks first!');
                return;
            }

            const tasks = tasksInput.split('\n').filter(task => task.trim());
            const prompt = prompts[currentLevel].replace('{tasks}', tasks.join(', '));
            
            // Display the prompt
            document.getElementById('prompt-display').textContent = prompt;
            
            // Generate and display the output
            const output = generateOutput(tasks, currentLevel);
            document.getElementById('output-display').innerHTML = output;
            
            // Show results
            document.getElementById('results').style.display = 'grid';
            document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
        }

        function generateOutput(tasks, level) {
            // Simulate different levels of AI organization
            if (level === 'basic') {
                return tasks.map(task => `<div class="task-item">${task}</div>`).join('');
            }
            
            if (level === 'intermediate') {
                const categorized = categorizeTasks(tasks);
                let output = '';
                
                if (categorized.high.length > 0) {
                    output += '<strong>HIGH PRIORITY:</strong><br>';
                    categorized.high.forEach(task => {
                        output += `<div class="task-item priority-high">${task.text} - ${task.category}</div>`;
                    });
                    output += '<br>';
                }
                
                if (categorized.medium.length > 0) {
                    output += '<strong>MEDIUM PRIORITY:</strong><br>';
                    categorized.medium.forEach(task => {
                        output += `<div class="task-item priority-medium">${task.text} - ${task.category}</div>`;
                    });
                    output += '<br>';
                }
                
                if (categorized.low.length > 0) {
                    output += '<strong>LOW PRIORITY:</strong><br>';
                    categorized.low.forEach(task => {
                        output += `<div class="task-item priority-low">${task.text} - ${task.category}</div>`;
                    });
                }
                
                return output;
            }
            
            if (level === 'advanced') {
                const categorized = categorizeTasks(tasks);
                let output = '<strong>🎯 OPTIMIZED DAILY PLAN</strong><br><br>';
                
                if (categorized.high.length > 0) {
                    output += '<strong>HIGH PRIORITY (Complete First):</strong><br>';
                    categorized.high.forEach(task => {
                        const timeEst = getTimeEstimate(task.text);
                        const tip = getProductivityTip(task.text);
                        output += `<div class="task-item priority-high">
                            <strong>${task.text}</strong> - ${task.category} Category<br>
                            ⏱️ Estimated time: ${timeEst}<br>
                            💡 Tip: ${tip}
                        </div>`;
                    });
                    output += '<br>';
                }
                
                if (categorized.medium.length > 0) {
                    output += '<strong>MEDIUM PRIORITY (Schedule Afternoon):</strong><br>';
                    categorized.medium.forEach(task => {
                        const timeEst = getTimeEstimate(task.text);
                        const tip = getProductivityTip(task.text);
                        output += `<div class="task-item priority-medium">
                            <strong>${task.text}</strong> - ${task.category} Category<br>
                            ⏱️ Estimated time: ${timeEst}<br>
                            💡 Tip: ${tip}
                        </div>`;
                    });
                    output += '<br>';
                }
                
                if (categorized.low.length > 0) {
                    output += '<strong>LOW PRIORITY (Evening/Flexible):</strong><br>';
                    categorized.low.forEach(task => {
                        const timeEst = getTimeEstimate(task.text);
                        const tip = getProductivityTip(task.text);
                        output += `<div class="task-item priority-low">
                            <strong>${task.text}</strong> - ${task.category} Category<br>
                            ⏱️ Estimated time: ${timeEst}<br>
                            💡 Tip: ${tip}
                        </div>`;
                    });
                    output += '<br>';
                }
                
                output += '<strong>📅 SUGGESTED TIMELINE:</strong><br>';
                output += generateTimeline(categorized);
                
                return output;
            }
        }

        function categorizeTasks(tasks) {
            const workKeywords = ['project', 'report', 'meeting', 'work', 'deadline', 'presentation', 'email'];
            const financeKeywords = ['bill', 'pay', 'bank', 'money', 'budget', 'tax'];
            const healthKeywords = ['gym', 'exercise', 'doctor', 'workout', 'run', 'walk'];
            const urgentKeywords = ['urgent', 'deadline', 'important', 'asap', 'today'];
            
            const categorized = { high: [], medium: [], low: [] };
            
            tasks.forEach(task => {
                const taskLower = task.toLowerCase();
                let category = 'Personal';
                let priority = 'medium';
                
                // Determine category
                if (workKeywords.some(keyword => taskLower.includes(keyword))) {
                    category = 'Work';
                } else if (financeKeywords.some(keyword => taskLower.includes(keyword))) {
                    category = 'Finance';
                } else if (healthKeywords.some(keyword => taskLower.includes(keyword))) {
                    category = 'Health';
                }
                
                // Determine priority
                if (urgentKeywords.some(keyword => taskLower.includes(keyword)) || 
                    taskLower.includes('project') || taskLower.includes('bill')) {
                    priority = 'high';
                } else if (taskLower.includes('read') || taskLower.includes('exercise') || 
                          taskLower.includes('gym')) {
                    priority = 'low';
                }
                
                categorized[priority].push({ text: task, category: category });
            });
            
            return categorized;
        }

        function getTimeEstimate(task) {
            const taskLower = task.toLowerCase();
            if (taskLower.includes('project') || taskLower.includes('report')) return '2-3 hours';
            if (taskLower.includes('grocery') || taskLower.includes('shopping')) return '45 minutes';
            if (taskLower.includes('gym') || taskLower.includes('workout')) return '1 hour';
            if (taskLower.includes('call')) return '20 minutes';
            if (taskLower.includes('bill') || taskLower.includes('pay')) return '30 minutes';
            if (taskLower.includes('read')) return '30 minutes';
            return '30-60 minutes';
        }

        function getProductivityTip(task) {
            const taskLower = task.toLowerCase();
            if (taskLower.includes('project') || taskLower.includes('report')) return 'Do this when your energy is highest (morning)';
            if (taskLower.includes('grocery')) return 'Make a list and shop during off-peak hours';
            if (taskLower.includes('gym')) return 'Go after work to de-stress';
            if (taskLower.includes('call')) return 'Call during their preferred time';
            if (taskLower.includes('bill')) return 'Set up auto-pay for recurring bills';
            if (taskLower.includes('read')) return 'Perfect wind-down activity before bed';
            return 'Focus on one task at a time for better results';
        }

        function generateTimeline(categorized) {
            let timeline = '';
            let currentTime = 9;
            
            categorized.high.forEach(task => {
                const duration = task.text.toLowerCase().includes('project') ? 3 : 0.5;
                timeline += `${currentTime}:00${currentTime < 12 ? 'AM' : 'PM'}-${currentTime + duration}:${duration === 0.5 ? '30' : '00'}${(currentTime + duration) < 12 ? 'AM' : 'PM'}: ${task.text}<br>`;
                currentTime += duration;
            });
            
            timeline += '<br>';
            currentTime = 14; // 2 PM
            
            categorized.medium.forEach(task => {
                const duration = 1;
                timeline += `${currentTime}:00PM-${currentTime + duration}:00PM: ${task.text}<br>`;
                currentTime += duration;
            });
            
            timeline += '<br>';
            currentTime = 18; // 6 PM
            
            categorized.low.forEach(task => {
                const duration = task.text.toLowerCase().includes('gym') ? 1 : 0.5;
                timeline += `${currentTime}:00PM-${currentTime + duration}:${duration === 0.5 ? '30' : '00'}PM: ${task.text}<br>`;
                currentTime += duration;
            });
            
            return timeline;
        }

        // Load sample data on page load
        window.onload = function() {
            document.getElementById('tasks').value = `Buy groceries
Finish project report
Call mom
Go to gym
Pay bills
Read for 30 minutes`;
        };
    </script>
</body>
</html>
```
## Output 


## Basic
![image](https://github.com/user-attachments/assets/06119767-55d5-4623-b3ef-92f5ce3be3fe)

![image](https://github.com/user-attachments/assets/24b72738-14c9-4e06-ae24-d565059b8f53)


## Intermediate
![image](https://github.com/user-attachments/assets/7323f91f-b267-42bc-b74c-40378d5c81b9)

![image](https://github.com/user-attachments/assets/881384ed-b136-4981-972d-dc2ef095664e)


## Advanced
![image](https://github.com/user-attachments/assets/6af44324-a897-4596-8bec-fc58cb534ed1)

![image](https://github.com/user-attachments/assets/41faf0f1-249e-4ae2-a5eb-d1a5122a89d9)

![image](https://github.com/user-attachments/assets/8aa01b35-0cb6-43bf-a821-b3dcf5b816f3)


## Result: 
The Prompt is executed successfully

