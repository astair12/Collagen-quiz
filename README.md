<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Skin Deficiency Quiz</title>
    <script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 min-h-screen py-8">
    <div id="root"></div>

    <script type="text/babel">
        const { useState } = React;

        // Lucide icons as SVG components
        const AlertCircle = () => (
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
                <circle cx="12" cy="12" r="10"></circle>
                <line x1="12" y1="8" x2="12" y2="12"></line>
                <line x1="12" y1="16" x2="12.01" y2="16"></line>
            </svg>
        );

        const CheckCircle2 = () => (
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
                <circle cx="12" cy="12" r="10"></circle>
                <path d="m9 12 2 2 4-4"></path>
            </svg>
        );

        const SkinDeficiencyQuiz = () => {
            const [currentQuestion, setCurrentQuestion] = useState(0);
            const [answers, setAnswers] = useState({});
            const [showResults, setShowResults] = useState(false);

            const questions = [
                {
                    id: 'age',
                    question: 'How old are you?',
                    options: [
                        { value: 'under20', label: 'Under 20', score: { collagen: 0 } },
                        { value: '20-30', label: '20-30', score: { collagen: 1 } },
                        { value: '31-40', label: '31-40', score: { collagen: 2 } },
                        { value: '41-50', label: '41-50', score: { collagen: 3 } },
                        { value: 'over50', label: 'Over 50', score: { collagen: 4 } }
                    ]
                },
                {
                    id: 'wrinkles',
                    question: 'How would you describe fine lines and wrinkles on your face?',
                    options: [
                        { value: 'none', label: 'None visible', score: { collagen: 0 } },
                        { value: 'minimal', label: 'Minimal, only when I smile', score: { collagen: 1 } },
                        { value: 'moderate', label: 'Noticeable around eyes and mouth', score: { collagen: 2 } },
                        { value: 'significant', label: 'Significant and deepening', score: { collagen: 3 } }
                    ]
                },
                {
                    id: 'elasticity',
                    question: 'When you pinch your skin, how quickly does it bounce back?',
                    options: [
                        { value: 'immediate', label: 'Immediately', score: { collagen: 0 } },
                        { value: 'quick', label: 'Within 1-2 seconds', score: { collagen: 1 } },
                        { value: 'slow', label: '3-5 seconds', score: { collagen: 2 } },
                        { value: 'veryslow', label: 'More than 5 seconds', score: { collagen: 3 } }
                    ]
                },
                {
                    id: 'dryness',
                    question: 'How often does your skin feel dry, tight, or flaky?',
                    options: [
                        { value: 'never', label: 'Rarely or never', score: { vitaminC: 0, iron: 0 } },
                        { value: 'occasional', label: 'Occasionally in winter', score: { vitaminC: 1, iron: 1 } },
                        { value: 'frequent', label: 'Frequently throughout the year', score: { vitaminC: 2, iron: 2 } },
                        { value: 'constant', label: 'Constantly, even with moisturizer', score: { vitaminC: 3, iron: 3 } }
                    ]
                },
                {
                    id: 'wounds',
                    question: 'How quickly do cuts, scrapes, or blemishes heal on your skin?',
                    options: [
                        { value: 'fast', label: 'Very quickly (3-5 days)', score: { vitaminC: 0 } },
                        { value: 'normal', label: 'Normal pace (5-7 days)', score: { vitaminC: 1 } },
                        { value: 'slow', label: 'Slowly (1-2 weeks)', score: { vitaminC: 2 } },
                        { value: 'veryslow', label: 'Very slowly (2+ weeks)', score: { vitaminC: 3 } }
                    ]
                },
                {
                    id: 'bruising',
                    question: 'Do you bruise easily?',
                    options: [
                        { value: 'no', label: 'Rarely bruise', score: { vitaminC: 0, copper: 0 } },
                        { value: 'sometimes', label: 'Occasionally', score: { vitaminC: 1, copper: 1 } },
                        { value: 'yes', label: 'Frequently', score: { vitaminC: 2, copper: 2 } },
                        { value: 'veryeasy', label: 'Very easily, unexplained bruises', score: { vitaminC: 3, copper: 3 } }
                    ]
                },
                {
                    id: 'diet',
                    question: 'How often do you eat collagen-rich foods (bone broth, gelatin, slow-cooked meats)?',
                    options: [
                        { value: 'daily', label: 'Daily', score: { glycine: 0 } },
                        { value: 'weekly', label: 'A few times per week', score: { glycine: 1 } },
                        { value: 'rarely', label: 'Rarely', score: { glycine: 2 } },
                        { value: 'never', label: 'Never', score: { glycine: 3 } }
                    ]
                },
                {
                    id: 'fruits',
                    question: 'How many servings of fresh fruits and vegetables do you eat daily?',
                    options: [
                        { value: '5plus', label: '5 or more', score: { vitaminC: 0 } },
                        { value: '3-4', label: '3-4 servings', score: { vitaminC: 1 } },
                        { value: '1-2', label: '1-2 servings', score: { vitaminC: 2 } },
                        { value: 'none', label: 'Less than 1 serving', score: { vitaminC: 3 } }
                    ]
                },
                {
                    id: 'meat',
                    question: 'How often do you eat red meat or liver?',
                    options: [
                        { value: 'weekly', label: 'Several times per week', score: { iron: 0, copper: 0 } },
                        { value: 'sometimes', label: 'Once a week', score: { iron: 1, copper: 1 } },
                        { value: 'rarely', label: 'Rarely', score: { iron: 2, copper: 2 } },
                        { value: 'never', label: 'Never (vegetarian/vegan)', score: { iron: 3, copper: 3 } }
                    ]
                },
                {
                    id: 'salt',
                    question: 'Do you restrict salt in your diet?',
                    options: [
                        { value: 'no', label: 'No, I salt my food normally', score: { sodium: 0 } },
                        { value: 'moderate', label: 'Somewhat cautious', score: { sodium: 1 } },
                        { value: 'yes', label: 'Yes, I actively avoid salt', score: { sodium: 3 } },
                        { value: 'lowsodium', label: 'Doctor-recommended low-sodium diet', score: { sodium: 2 } }
                    ]
                }
            ];

            const handleAnswer = (option) => {
                const newAnswers = { ...answers, [questions[currentQuestion].id]: option };
                setAnswers(newAnswers);

                if (currentQuestion < questions.length - 1) {
                    setCurrentQuestion(currentQuestion + 1);
                } else {
                    setShowResults(true);
                }
            };

            const calculateResults = () => {
                const scores = {
                    collagen: 0,
                    glycine: 0,
                    vitaminC: 0,
                    iron: 0,
                    copper: 0,
                    sodium: 0
                };

                Object.values(answers).forEach(answer => {
                    Object.entries(answer.score).forEach(([nutrient, value]) => {
                        scores[nutrient] += value;
                    });
                });

                const deficiencies = [];

                if (scores.collagen >= 5) {
                    deficiencies.push({
                        name: 'Collagen Loss',
                        severity: scores.collagen >= 8 ? 'High' : 'Moderate',
                        description: 'Your skin is showing signs of significant collagen loss, likely due to age and insufficient glycine intake.',
                        recommendations: [
                            'Take 10-15g of collagen peptides daily',
                            'Consume bone broth or gelatin regularly',
                            'Include slow-cooked meats with connective tissue'
                        ]
                    });
                }

                if (scores.glycine >= 2) {
                    deficiencies.push({
                        name: 'Glycine Deficiency',
                        severity: scores.glycine >= 4 ? 'High' : 'Moderate',
                        description: 'You may not be getting enough glycine to support optimal collagen synthesis (body needs 12g daily, makes only 3g).',
                        recommendations: [
                            'Supplement with collagen peptides or glycine powder',
                            'Eat more bone broth, skin-on chicken, pork rinds',
                            'Consider gelatin in smoothies or desserts'
                        ]
                    });
                }

                if (scores.vitaminC >= 4) {
                    deficiencies.push({
                        name: 'Vitamin C Deficiency',
                        severity: scores.vitaminC >= 7 ? 'High' : 'Moderate',
                        description: 'Vitamin C is essential for collagen formation. Low levels lead to poor wound healing and skin issues.',
                        recommendations: [
                            'Eat citrus fruits, berries, bell peppers daily',
                            'Include broccoli, Brussels sprouts, kiwi',
                            'Consider a vitamin C supplement (500-1000mg)',
                            'Ensure adequate sodium intake for vitamin C absorption'
                        ]
                    });
                }

                if (scores.iron >= 4) {
                    deficiencies.push({
                        name: 'Iron Deficiency',
                        severity: scores.iron >= 6 ? 'High' : 'Moderate',
                        description: 'Iron is required for the hydroxylation process that creates functional collagen from procollagen.',
                        recommendations: [
                            'Eat red meat 2-3 times per week',
                            'Include iron-rich foods like liver, shellfish',
                            'Pair iron sources with vitamin C for better absorption',
                            'Consider iron testing and supplementation if needed'
                        ]
                    });
                }

                if (scores.copper >= 4) {
                    deficiencies.push({
                        name: 'Copper Deficiency',
                        severity: scores.copper >= 6 ? 'High' : 'Moderate',
                        description: 'Copper is essential for cross-linking collagen fibers, making them strong and functional.',
                        recommendations: [
                            'Eat liver (best source) once or twice weekly',
                            'Include oysters, mushrooms, nuts and seeds',
                            'Ensure adequate vitamin A intake to transport copper'
                        ]
                    });
                }

                if (scores.sodium >= 3) {
                    deficiencies.push({
                        name: 'Low Sodium Intake',
                        severity: 'Moderate',
                        description: 'Sodium is required for vitamin C absorption through SVCT transporters. Low sodium reduces collagen synthesis.',
                        recommendations: [
                            'Use high-quality sea salt on your food',
                            'Drink mineral water',
                            'Don\'t restrict salt unless medically necessary',
                            'Note: If on low-sodium diet for medical reasons, consult your doctor'
                        ]
                    });
                }

                return deficiencies;
            };

            const restartQuiz = () => {
                setCurrentQuestion(0);
                setAnswers({});
                setShowResults(false);
            };

            if (showResults) {
                const deficiencies = calculateResults();

                return (
                    <div className="max-w-3xl mx-auto p-6 bg-gradient-to-br from-pink-50 to-purple-50 rounded-lg shadow-lg">
                        <h2 className="text-3xl font-bold text-gray-800 mb-6 text-center">Your Skin Health Results</h2>
                        
                        {deficiencies.length === 0 ? (
                            <div className="bg-green-50 border-2 border-green-200 rounded-lg p-6 mb-6">
                                <div className="flex items-start gap-3">
                                    <div className="w-6 h-6 text-green-600 flex-shrink-0 mt-1">
                                        <CheckCircle2 />
                                    </div>
                                    <div>
                                        <h3 className="text-xl font-bold text-green-800 mb-2">Great News!</h3>
                                        <p className="text-green-700">Your answers suggest you're doing well with collagen-supporting nutrition. Keep up your current habits for healthy, youthful skin!</p>
                                    </div>
                                </div>
                            </div>
                        ) : (
                            <>
                                <p className="text-gray-700 mb-6 text-center">Based on your answers, you may benefit from addressing these potential deficiencies:</p>
                                
                                {deficiencies.map((def, index) => (
                                    <div key={index} className="bg-white rounded-lg p-6 mb-4 shadow-md border-l-4 border-purple-500">
                                        <div className="flex items-start gap-3 mb-3">
                                            <div className="w-6 h-6 text-purple-600 flex-shrink-0 mt-1">
                                                <AlertCircle />
                                            </div>
                                            <div>
                                                <h3 className="text-xl font-bold text-gray-800">{def.name}</h3>
                                                <span className={`inline-block px-3 py-1 rounded-full text-sm font-semibold mt-1 ${
                                                    def.severity === 'High' ? 'bg-red-100 text-red-700' : 'bg-yellow-100 text-yellow-700'
                                                }`}>
                                                    {def.severity} Priority
                                                </span>
                                            </div>
                                        </div>
                                        
                                        <p className="text-gray-700 mb-4 ml-9">{def.description}</p>
                                        
                                        <div className="ml-9">
                                            <h4 className="font-semibold text-gray-800 mb-2">Recommendations:</h4>
                                            <ul className="space-y-2">
                                                {def.recommendations.map((rec, idx) => (
                                                    <li key={idx} className="flex items-start gap-2">
                                                        <span className="text-purple-600 font-bold">•</span>
                                                        <span className="text-gray-700">{rec}</span>
                                                    </li>
                                                ))}
                                            </ul>
                                        </div>
                                    </div>
                                ))}
                            </>
                        )}

                        <div className="bg-gradient-to-r from-purple-600 to-pink-600 rounded-lg p-8 mb-6 text-white shadow-xl">
                            <h3 className="text-2xl font-bold mb-3 text-center">Ready to Transform Your Skin?</h3>
                            <p className="text-center mb-6 text-purple-50">Get the premium collagen supplement recommended by experts to address your specific deficiencies.</p>
                            
                            
                                href="https://bit.ly/crefresh"
                                target="_blank"
                                rel="noopener noreferrer"
                                className="block w-full bg-white text-purple-600 font-bold py-4 px-6 rounded-lg text-center hover:bg-gray-100 transition-colors shadow-lg text-lg mb-4"
                            >
                                🎁 Get Your Collagen Now - Special Offer
                            </a>
                            
                            <div className="flex items-center justify-center gap-4 text-sm text-purple-100">
                                <span>✓ Clinically Proven Results</span>
                                <span>✓ Premium Quality</span>
                                <span>✓ Money-Back Guarantee</span>
                            </div>
                        </div>

                        <div className="bg-blue-50 border-2 border-blue-200 rounded-lg p-6 mb-6">
                            <h3 className="font-bold text-blue-900 mb-3">Important Note:</h3>
                            <p className="text-blue-800 text-sm">This quiz provides general guidance based on common nutrient deficiencies related to skin health. It is not a medical diagnosis. For persistent skin issues or before starting any supplementation regimen, please consult with a healthcare provider or dermatologist.</p>
                        </div>

                        <button
                            onClick={restartQuiz}
                            className="w-full bg-gray-600 hover:bg-gray-700 text-white font-semibold py-3 px-6 rounded-lg transition-colors"
                        >
                            Take Quiz Again
                        </button>
                    </div>
                );
            }

            return (
                <div className="max-w-2xl mx-auto p-6 bg-gradient-to-br from-pink-50 to-purple-50 rounded-lg shadow-lg">
                    <div className="mb-6">
                        <h2 className="text-3xl font-bold text-gray-800 mb-2 text-center">Skin Deficiency Quiz</h2>
                        <p className="text-gray-600 text-center">Discover what nutrients your skin might be missing</p>
                    </div>

                    <div className="mb-6">
                        <div className="flex justify-between items-center mb-2">
                            <span className="text-sm font-medium text-gray-600">Question {currentQuestion + 1} of {questions.length}</span>
                            <span className="text-sm font-medium text-purple-600">{Math.round(((currentQuestion + 1) / questions.length) * 100)}%</span>
                        </div>
                        <div className="w-full bg-gray-200 rounded-full h-2">
                            <div
                                className="bg-purple-600 h-2 rounded-full transition-all duration-300"
                                style={{ width: `${((currentQuestion + 1) / questions.length) * 100}%` }}
                            ></div>
                        </div>
                    </div>

                    <div className="bg-white rounded-lg p-6 shadow-md mb-6">
                        <h3 className="text-xl font-semibold text-gray-800 mb-6">{questions[currentQuestion].question}</h3>
                        
                        <div className="space-y-3">
                            {questions[currentQuestion].options.map((option, index) => (
                                <button
                                    key={index}
                                    onClick={() => handleAnswer(option)}
                                    className="w-full text-left p-4 rounded-lg border-2 border-gray-200 hover:border-purple-500 hover:bg-purple-50 transition-all duration-200 font-medium text-gray-700"
                                >
                                    {option.label}
                                </button>
                            ))}
                        </div>
                    </div>

                    {currentQuestion > 0 && (
                        <button
                            onClick={() => setCurrentQuestion(currentQuestion - 1)}
                            className="text-purple-600 hover:text-purple-700 font-medium"
                        >
                            ← Previous Question
                        </button>
                    )}
                </div>
            );
        };

        ReactDOM.render(<SkinDeficiencyQuiz />, document.getElementById('root'));
    </script>
</body>
</html>
```

- Click "Commit changes" at the bottom

### 4. **Enable GitHub Pages**
- Go to your repository's "Settings" tab
- Scroll down to "Pages" in the left sidebar
- Under "Source", select **"main"** branch
- Click "Save"
- Wait 1-2 minutes for it to deploy

### 5. **Access Your Quiz**
Your quiz will be live at:
```
https://astair12.github.io/skin-quiz/
