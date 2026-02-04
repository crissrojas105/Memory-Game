<html lang="en" translate="no">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="google" content="notranslate">
    <meta http-equiv="Content-Language" content="en">
    <title>Pronoun Memory Game 🎮</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700;800&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary: #4A90E2;
            --secondary: #50C878;
            --accent: #F39C12;
            --personal: #E74C3C;
            --possessive: #27AE60;
            --object: #3498DB;
            --wildcard-yellow: #F1C40F;
            --wildcard-red: #E74C3C;
            --dark: #2C3E50;
            --light: #ECF0F1;
            --white: #FFFFFF;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 5px;
            position: relative;
            overflow-x: hidden;
        }

        /* Prevent translation */
        * {
            translate: no;
        }

        .notranslate {
            translate: no;
        }

        /* Background particles */
        .bg-particle {
            position: fixed;
            width: 10px;
            height: 10px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            pointer-events: none;
            animation: float 20s infinite ease-in-out;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0) translateX(0); }
            25% { transform: translateY(-100px) translateX(50px); }
            50% { transform: translateY(-50px) translateX(-50px); }
            75% { transform: translateY(-150px) translateX(100px); }
        }

        /* Page Container */
        .page {
            display: none;
            max-width: 1200px;
            width: 100%;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 30px;
            box-shadow: 0 30px 80px rgba(0, 0, 0, 0.3);
            padding: 10px;
            position: relative;
            backdrop-filter: blur(10px);
            animation: slideIn 0.6s ease-out;
        }

        .page.active {
            display: block;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Welcome Page */
        .welcome-content {
            text-align: center;
            padding: 10px 5px;
        }

        .welcome-title {
            font-size: 4rem;
            font-weight: 800;
            background: linear-gradient(135deg, var(--primary), var(--possessive));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 20px;
            animation: titlePulse 2s ease-in-out infinite;
        }

        @keyframes titlePulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .welcome-subtitle {
            font-size: 1.5rem;
            color: var(--dark);
            margin-bottom: 5px;
            opacity: 0.8;
        }

        .welcome-emoji {
            font-size: 8rem;
            margin: 5px 0;
            animation: bounce 2s ease-in-out infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }

        .welcome-description {
            font-size: 1.2rem;
            color: var(--dark);
            line-height: 1.8;
            margin-bottom: 5px;
            max-width: 700px;
            margin-left: auto;
            margin-right: auto;
        }

        /* Instructions Page */
        .instructions-content {
            max-width: 900px;
            margin: 0 auto;
        }

        .section-title {
            font-size: 2.5rem;
            font-weight: 800;
            color: var(--dark);
            margin-bottom: 5px;
            text-align: center;
            background: linear-gradient(135deg, var(--primary), var(--possessive));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .instruction-block {
            padding: 30px;
            border-radius: 20px;
            margin-bottom: 25px;
            border-left: 5px solid var(--primary);
        }

        .instruction-block h3 {
            font-size: 1.8rem;
            color: var(--primary);
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .instruction-block p, .instruction-block ul {
            font-size: 1.1rem;
            line-height: 1.8;
            color: var(--dark);
        }

        .instruction-block ul {
            margin-left: 20px;
        }

        .instruction-block li {
            margin-bottom: 10px;
        }

        .color-guide {
            display: flex;
            gap: 20px;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 20px;
        }

        .color-box {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 15px 25px;
            border-radius: 15px;
            border: 2px solid rgba(0,0,0,0.1);
        }

        .color-square {
            width: 40px;
            height: 40px;
            border-radius: 10px;
            border: 3px solid;
        }

        /* Grammar Examples Page */
        .examples-content {
            max-width: 1000px;
            margin: 0 auto;
        }

        .example-card {
            padding: 35px;
            border-radius: 25px;
            margin-bottom: 30px;
            border-left: 8px solid;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .example-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 45px rgba(0, 0, 0, 0.2);
        }

        .example-card.personal-ex {
            border-color: var(--personal);
        }

        .example-card.object-ex {
            border-color: var(--object);
        }

        .example-card.possessive-ex {
            border-color: var(--possessive);
        }

        .example-number {
            display: inline-block;
            background: linear-gradient(135deg, var(--primary), var(--possessive));
            color: white;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 800;
            font-size: 1.5rem;
            margin-bottom: 20px;
        }

        .example-sentence {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--dark);
            margin-bottom: 15px;
            font-family: 'Space Mono', monospace;
        }

        .example-answer {
            font-size: 2.2rem;
            font-weight: 800;
            margin: 20px 0;
            padding: 15px;
            border-radius: 15px;
            text-align: center;
            border: 3px solid;
        }

        .example-answer.personal-ans { 
            color: var(--personal); 
            border-color: var(--personal);
        }
        .example-answer.object-ans { 
            color: var(--object); 
            border-color: var(--object);
        }
        .example-answer.possessive-ans { 
            color: var(--possessive); 
            border-color: var(--possessive);
        }

        .example-explanation {
            padding: 20px;
            border-radius: 15px;
            margin-top: 20px;
            border-left: 4px solid var(--primary);
        }

        .example-explanation strong {
            color: var(--primary);
            font-size: 1.2rem;
        }

        .example-explanation p {
            font-size: 1.1rem;
            line-height: 1.8;
            color: var(--dark);
            margin-top: 10px;
        }

        /* Game Page */
        .header {
            text-align: center;
            margin-bottom: 30px;
        }

        h1 {
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(135deg, var(--primary), var(--possessive));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            margin-bottom: 10px;
            letter-spacing: -1px;
        }

        .subtitle {
            font-size: 1.2rem;
            color: var(--dark);
            opacity: 0.7;
            font-weight: 400;
        }

        .game-stats {
            display: flex;
            justify-content: space-around;
            margin-bottom: 30px;
            gap: 20px;
            flex-wrap: wrap;
        }

        .stat-box {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 20px 30px;
            border-radius: 20px;
            text-align: center;
            flex: 1;
            min-width: 150px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
            transition: transform 0.3s ease;
        }

        .stat-box:hover {
            transform: translateY(-5px);
        }

        .stat-value {
            font-size: 2.5rem;
            font-weight: 800;
            font-family: 'Space Mono', monospace;
        }

        .stat-label {
            font-size: 0.9rem;
            opacity: 0.9;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: 5px;
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .btn {
            padding: 15px 35px;
            border: none;
            border-radius: 50px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-family: 'Poppins', sans-serif;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--secondary), #27ae60);
            color: white;
        }

        .btn-secondary {
            background: linear-gradient(135deg, var(--accent), #e67e22);
            color: white;
        }

        .btn-info {
            background: linear-gradient(135deg, var(--primary), #3498db);
            color: white;
        }

        .btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.3);
        }

        .btn:active {
            transform: translateY(-1px);
        }

        .game-board {
            display: grid;
            grid-template-columns: repeat(6, 1fr);
            gap: 15px;
            margin-bottom: 30px;
            perspective: 1000px;
            max-width: 1100px;
            margin-left: auto;
            margin-right: auto;
        }

        .card {
            aspect-ratio: 2.5/3.5;
            position: relative;
            cursor: pointer;
            transform-style: preserve-3d;
            transition: transform 0.6s cubic-bezier(0.4, 0.0, 0.2, 1);
            max-width: 160px;
        }

        .card.flipped {
            transform: rotateY(180deg);
        }

        .card.matched {
            animation: matchAnimation 0.6s ease-out;
            pointer-events: none;
        }

        @keyframes matchAnimation {
            0% { transform: rotateY(180deg) scale(1); }
            50% { transform: rotateY(180deg) scale(1.1); }
            100% { transform: rotateY(180deg) scale(1); opacity: 0.5; }
        }

        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 15px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 12px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
        }

        .card-front {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }

        .card-back {
            background: white;
            transform: rotateY(180deg);
            border: 4px solid;
        }

        .card-back.personal {
            border-color: var(--personal);
            background: linear-gradient(135deg, #fff, #ffe6e6);
        }

        .card-back.possessive {
            border-color: var(--possessive);
            background: linear-gradient(135deg, #fff, #f3e6ff);
        }

        .card-back.object {
            border-color: var(--object);
            background: linear-gradient(135deg, #fff, #e6f3ff);
        }

        .card-back.wildcard-extra {
            border-color: var(--wildcard-yellow);
            background: linear-gradient(135deg, #FFF9E6, var(--wildcard-yellow));
        }

        .card-back.wildcard-lose {
            border-color: var(--wildcard-red);
            background: linear-gradient(135deg, #FFE6E6, var(--wildcard-red));
        }

        .card-icon {
            font-size: 2rem;
            margin-bottom: 5px;
        }

        .card-content {
            text-align: center;
            font-size: 0.9rem;
            font-weight: 600;
            color: var(--dark);
            line-height: 1.3;
        }

        .card-type {
            font-size: 0.65rem;
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-top: 8px;
            opacity: 0.7;
            font-weight: 700;
        }

        .pronoun-answer {
            font-size: 2rem;
            font-weight: 800;
            font-family: 'Space Mono', monospace;
        }

        .personal .pronoun-answer { color: var(--personal); }
        .possessive .pronoun-answer { color: var(--possessive); }
        .object .pronoun-answer { color: var(--object); }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.8);
            justify-content: center;
            align-items: center;
            z-index: 1000;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            background: white;
            padding: 50px;
            border-radius: 30px;
            text-align: center;
            max-width: 500px;
            animation: popIn 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        @keyframes popIn {
            0% {
                transform: scale(0.5);
                opacity: 0;
            }
            100% {
                transform: scale(1);
                opacity: 1;
            }
        }

        .modal-title {
            font-size: 2.5rem;
            margin-bottom: 20px;
            color: var(--dark);
        }

        .modal-message {
            font-size: 1.2rem;
            margin-bottom: 30px;
            color: var(--dark);
            opacity: 0.8;
        }

        .celebration {
            font-size: 4rem;
            margin-bottom: 20px;
        }

        .legend {
            display: flex;
            justify-content: center;
            gap: 30px;
            flex-wrap: wrap;
            margin-top: 20px;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 0.9rem;
        }

        .legend-color {
            width: 30px;
            height: 30px;
            border-radius: 8px;
            border: 3px solid;
        }

        .legend-color.personal {
            background: var(--personal);
            border-color: var(--personal);
        }

        .legend-color.possessive {
            background: var(--possessive);
            border-color: var(--possessive);
        }

        .legend-color.object {
            background: var(--object);
            border-color: var(--object);
        }

        .wildcard-message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) scale(0);
            background: white;
            padding: 40px;
            border-radius: 30px;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4);
            z-index: 999;
            text-align: center;
            font-size: 1.5rem;
            font-weight: 700;
            animation: wildcardPop 0.6s ease-out forwards;
        }

        @keyframes wildcardPop {
            0% {
                transform: translate(-50%, -50%) scale(0) rotate(0deg);
            }
            50% {
                transform: translate(-50%, -50%) scale(1.2) rotate(10deg);
            }
            100% {
                transform: translate(-50%, -50%) scale(1) rotate(0deg);
            }
        }

        /* Celebration Effects */
        .celebration-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.85);
            z-index: 2000;
            display: none;
            justify-content: center;
            align-items: center;
        }

        .celebration-overlay.active {
            display: flex;
            animation: fadeIn 0.5s ease;
        }

        .celebration-content {
            text-align: center;
            background: white;
            padding: 60px 40px;
            border-radius: 30px;
            max-width: 600px;
            position: relative;
            animation: celebrationBounce 0.8s cubic-bezier(0.68, -0.55, 0.265, 1.55);
        }

        @keyframes celebrationBounce {
            0% {
                transform: scale(0) rotate(-180deg);
                opacity: 0;
            }
            50% {
                transform: scale(1.1) rotate(10deg);
            }
            100% {
                transform: scale(1) rotate(0deg);
                opacity: 1;
            }
        }

        .celebration-emoji {
            font-size: 6rem;
            margin-bottom: 20px;
            animation: emojiPulse 1s ease-in-out infinite;
        }

        @keyframes emojiPulse {
            0%, 100% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.2) rotate(10deg); }
        }

        .celebration-title {
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(135deg, #FFD700, #FFA500);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 20px;
        }

        .celebration-message {
            font-size: 1.5rem;
            color: var(--dark);
            margin-bottom: 30px;
            line-height: 1.6;
        }

        .celebration-stats {
            background: linear-gradient(135deg, #f5f7fa, #c3cfe2);
            padding: 25px;
            border-radius: 20px;
            margin-bottom: 30px;
        }

        .celebration-stat {
            font-size: 1.3rem;
            color: var(--dark);
            margin: 10px 0;
        }

        /* Confetti */
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background: #f0f;
            position: fixed;
            top: -10px;
            z-index: 2001;
            animation: confettiFall 3s linear forwards;
        }

        @keyframes confettiFall {
            to {
                transform: translateY(100vh) rotate(360deg);
                opacity: 0;
            }
        }

        /* Fireworks */
        .firework {
            position: fixed;
            width: 4px;
            height: 4px;
            border-radius: 50%;
            z-index: 2001;
        }

        .firework-particle {
            animation: fireworkExplode 1s ease-out forwards;
        }

        @keyframes fireworkExplode {
            0% {
                transform: scale(1) translate(0, 0);
                opacity: 1;
            }
            100% {
                opacity: 0;
            }
        }

        /* Flash effect */
        .flash {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: white;
            z-index: 1999;
            opacity: 0;
            pointer-events: none;
            animation: flashEffect 0.5s ease-out;
        }

        @keyframes flashEffect {
            0%, 100% { opacity: 0; }
            50% { opacity: 0.8; }
        }

        /* References Page */
        .references-content {
            max-width: 1000px;
            margin: 0 auto;
        }

        .reference-item {
            padding: 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border-left: 5px solid var(--primary);
        }

        .reference-item p {
            font-size: 1.1rem;
            line-height: 1.8;
            color: var(--dark);
            margin: 0;
        }

        .learning-summary {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            padding: 40px;
            border-radius: 25px;
            margin-bottom: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
        }

        .learning-point {
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 15px;
            border-left: 5px solid var(--dark);
        }

        .learning-point h4 {
            font-size: 1.5rem;
            margin-bottom: 10px;
        }

        .learning-point p {
            font-size: 1.1rem;
            line-height: 1.6;
            opacity: 0.95;
        }

        /* Sound Toggle */
        .sound-toggle {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            font-size: 1.8rem;
            cursor: pointer;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            transition: all 0.3s ease;
            z-index: 100;
        }

        .sound-toggle:hover {
            transform: scale(1.1);
        }

        @media (max-width: 768px) {
            h1, .welcome-title {
                font-size: 1.8rem;
            }

            .welcome-emoji {
                font-size: 5rem;
            }

            .section-title {
                font-size: 1.8rem;
            }

            .game-board {
                grid-template-columns: repeat(4, 1fr);
                gap: 10px;
            }

            .card {
                max-width: none;
            }

            .card-content {
                font-size: 0.75rem;
            }

            .pronoun-answer {
                font-size: 1.5rem;
            }

            .example-sentence {
                font-size: 1.2rem;
            }

            .example-answer {
                font-size: 1.6rem;
            }

            .card-icon {
                font-size: 1.5rem;
            }

            .game-container, .page {
                padding: 20px;
                margin: 10px;
            }

            .stat-box {
                padding: 15px 20px;
                min-width: 120px;
            }

            .stat-value {
                font-size: 2rem;
            }

            .btn {
                padding: 12px 25px;
                font-size: 0.9rem;
            }

            .controls {
                gap: 10px;
            }

            .instruction-block, .example-card, .reference-item, .learning-point {
                padding: 20px;
                margin-bottom: 20px;
            }

            .celebration-content, .modal-content {
                padding: 30px 20px;
                margin: 10px;
                max-width: 90%;
            }

            .celebration-title, .modal-title {
                font-size: 2rem;
            }

            .celebration-emoji {
                font-size: 4rem;
            }
        }

        @media (max-width: 480px) {
            h1, .welcome-title {
                font-size: 1.5rem;
            }

            .welcome-emoji {
                font-size: 4rem;
            }

            .section-title {
                font-size: 1.5rem;
            }

            .game-board {
                grid-template-columns: repeat(3, 1fr);
                gap: 8px;
            }

            .card-content {
                font-size: 0.65rem;
            }

            .pronoun-answer {
                font-size: 1.2rem;
            }

            .stat-box {
                padding: 12px 15px;
                min-width: 100px;
            }

            .stat-value {
                font-size: 1.8rem;
            }

            .btn {
                padding: 10px 20px;
                font-size: 0.85rem;
            }

            .game-container, .page {
                padding: 15px;
                margin: 5px;
            }

            .example-sentence {
                font-size: 1rem;
            }

            .example-answer {
                font-size: 1.4rem;
            }

            .instruction-block h3 {
                font-size: 1.4rem;
            }

            .instruction-block p, .instruction-block ul {
                font-size: 0.95rem;
            }

            .learning-point h4 {
                font-size: 1.2rem;
            }

            .learning-point p {
                font-size: 0.95rem;
            }
        }
    </style>
</head>
<body translate="no" class="notranslate">
    <!-- Sound Toggle -->
    <button class="sound-toggle" id="soundToggle" onclick="toggleSound()">🔊</button>

    <!-- Background particles -->
    <div class="bg-particle" style="top: 10%; left: 20%; animation-delay: 0s;"></div>
    <div class="bg-particle" style="top: 60%; left: 80%; animation-delay: 3s;"></div>
    <div class="bg-particle" style="top: 80%; left: 10%; animation-delay: 6s;"></div>
    <div class="bg-particle" style="top: 30%; left: 70%; animation-delay: 9s;"></div>

    <!-- PRESENTATION PAGE (Student Information) -->
    <div class="page active" id="presentationPage">
        <div class="welcome-content">
            <div style="text-align: center; margin-bottom: 40px;">
                <h1 style="font-size: 3.5rem; font-weight: 800; background: linear-gradient(135deg, #2C3E50, #3498DB); -webkit-background-clip: text; -webkit-text-fill-color: transparent; margin-bottom: 10px;" class="notranslate">
                    Memory Card Game
                </h1>
                <p style="font-size: 1.5rem; color: var(--dark); opacity: 0.7;" class="notranslate">Pronoun Match</p>
            </div>

            <div style="padding: 5px; border-radius: 25px; margin-bottom: 5px;">
                <h2 style="font-size: 2.2rem; margin-bottom: 30px; font-weight: 700; text-align: center; color: var(--dark);" class="notranslate">
                    Student Information
                </h2>
                <div style="padding: 5px; border-radius: 20px;">
                    <div style="text-align: left; max-width: 700px; margin: 0 auto; line-height: 2;">
                        <p style="font-size: 1.3rem; margin-bottom: 5px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Student:</strong> Cristian Alexander Rojas
                        </p>
                        <p style="font-size: 1.2rem; margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">University:</strong> Corporación Universitaria Minuto de Dios
                        </p>
                        <p style="font-size: 1.2rem; margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Program:</strong> Administración de Empresas
                        </p>
                        <p style="font-size: 1.2rem; margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Course:</strong> NRC-744 - Inglés I
                        </p>
                        <p style="font-size: 1.2rem; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Date:</strong> January 2026
                        </p>
                    </div>
                </div>
            </div>

            <div style="background: linear-gradient(135deg, #f5f7fa, #c3cfe2); padding: 5px; border-radius: 20px; margin-bottom: 40px;">
                <h3 style="font-size: 1.8rem; color: var(--dark); margin-bottom: 15px; text-align: center;" class="notranslate">
                    🎯 Project Objective
                </h3>
                <p style="font-size: 1.2rem; line-height: 1.8; color: var(--dark); text-align: center;" class="notranslate">
                    Interactive web-based memory game designed to practice and master English pronouns (Personal, Possessive, and Object) through engaging gameplay and educational examples.
                </p>
            </div>

            <div class="controls">
                <button class="btn btn-primary" onclick="playSound('click'); showPage('welcomePage')" style="font-size: 1.2rem; padding: 18px 40px;">
                    ▶️ Begin Experience
                </button>
            </div>
        </div>
    </div>

    <!-- WELCOME PAGE -->
    <div class="page" id="welcomePage">
        <div class="welcome-content">
            <div class="welcome-emoji">🎮</div>
            <h1 class="welcome-title notranslate">Pronoun Memory Game</h1>
            <p class="welcome-subtitle notranslate">Master English Pronouns Through Interactive Play!</p>
            
            <div class="welcome-description notranslate">
                <p><strong>Welcome to the ultimate pronoun learning experience!</strong></p>
                <p>Test your knowledge of <strong>Personal</strong>, <strong>Possessive</strong>, and <strong>Object</strong> pronouns through an engaging memory matching game.</p>
                <p>Flip cards, find matches, and master English grammar while having fun!</p>
            </div>

            <div class="controls">
                <button class="btn btn-primary" onclick="playSound('click'); showPage('instructionsPage')">
                    📖 View Instructions
                </button>
                <button class="btn btn-info" onclick="playSound('click'); showPage('examplesPage')">
                    📚 Grammar Examples
                </button>
                <button class="btn btn-secondary" onclick="playSound('click'); showPage('gamePage'); startGame()">
                    🎮 Start Playing!
                </button>
                <button class="btn btn-info" onclick="playSound('click'); showPage('finalPage')" style="background: linear-gradient(135deg, #FFD700, #FFA500);">
                    🏆 View Final Page
                </button>
            </div>
        </div>
    </div>

    <!-- INSTRUCTIONS PAGE -->
    <div class="page" id="instructionsPage">
        <div class="instructions-content">
            <h2 class="section-title notranslate"> How to Play</h2>

            <div class="instruction-block">
                <h3 notranslate>🎯 Game Objective</h3>
                <p class="notranslate">Match all 10 sentence cards with their correct pronoun cards. Each sentence has a blank space that needs to be filled with the appropriate pronoun.</p>
            </div>

            <div class="instruction-block">
                <h3 class="notranslate">🎮 How to Play</h3>
                <ul class="notranslate">
                    <li><strong>Step 1:</strong> Click on any card to flip it and reveal its content</li>
                    <li><strong>Step 2:</strong> Click on a second card to flip it</li>
                    <li><strong>Step 3:</strong> If the sentence and pronoun match correctly, they stay flipped!</li>
                    <li><strong>Step 4:</strong> If they don't match, both cards flip back over</li>
                    <li><strong>Step 5:</strong> Continue until you've matched all 10 pairs!</li>
                </ul>
            </div>

            <div class="instruction-block">
                <h3 class="notranslate">⭐ Special Wildcard Cards</h3>
                <ul class="notranslate">
                    <li><strong>⭐ Extra Turn:</strong> Lucky you! You get to flip again immediately</li>
                    <li><strong>❌ Lose a Pair:</strong> Oh no! Your last matched pair will be removed</li>
                </ul>
            </div>

            <div class="instruction-block">
                <h3 class="notranslate">🎨 Color Guide</h3>
                <p class="notranslate">Each pronoun type has its own color to help you learn:</p>
                <div class="color-guide">
                    <div class="color-box">
                        <div class="color-square" style="background: var(--personal); border-color: var(--personal);"></div>
                        <strong class="notranslate">Red = Personal Pronouns</strong>
                    </div>
                    <div class="color-box">
                        <div class="color-square" style="background: var(--possessive); border-color: var(--possessive);"></div>
                        <strong class="notranslate">Green = Possessive Pronouns</strong>
                    </div>
                    <div class="color-box">
                        <div class="color-square" style="background: var(--object); border-color: var(--object);"></div>
                        <strong class="notranslate">Blue = Object Pronouns</strong>
                    </div>
                </div>
            </div>

            <div class="controls">
                <button class="btn btn-secondary" onclick="playSound('click'); showPage('welcomePage')">
                    ⬅️ Back to Welcome
                </button>
                <button class="btn btn-info" onclick="playSound('click'); showPage('examplesPage')">
                    📚 Grammar Examples
                </button>
                <button class="btn btn-primary" onclick="playSound('click'); showPage('gamePage'); startGame()">
                    🎮 Start Game
                </button>
                <button class="btn btn-info" onclick="playSound('click'); showPage('finalPage')" style="background: linear-gradient(135deg, #FFD700, #FFA500);">
                    🏆 Final Page
                </button>
            </div>
        </div>
    </div>

    <!-- GRAMMAR EXAMPLES PAGE -->
    <div class="page" id="examplesPage">
        <div class="examples-content">
            <h2 class="section-title notranslate"> Grammar Examples</h2>
            <p style="text-align: center; font-size: 1.2rem; color: var(--dark); margin-bottom: 40px;" class="notranslate">
                Understanding the three types of pronouns with detailed explanations
            </p>

            <!-- Example 1: Personal Pronoun -->
            <div class="example-card personal-ex">
                <div class="example-number" style="background: var(--personal);">1</div>
                <div class="example-sentence notranslate">
                    "___ is my best friend at school"
                </div>
                <div class="example-answer personal-ans notranslate">
                    → SHE
                </div>
                <div class="example-explanation">
                    <strong class="notranslate">💡 Explanation:</strong>
                    <p class="notranslate">
                        We use a <strong>Subject Pronoun</strong> (Personal Pronoun) because it represents the person performing the action in the sentence. "She" is the subject who "is" a best friend. Subject pronouns replace the name of a person and act as the doer of the action.
                    </p>
                    <p class="notranslate" style="margin-top: 10px; font-style: italic; color: var(--personal);">
                        <strong>Other Personal Pronouns:</strong> I, you, he, she, it, we, they
                    </p>
                </div>
            </div>

            <!-- Example 2: Object Pronoun -->
            <div class="example-card object-ex">
                <div class="example-number" style="background: var(--object);">2</div>
                <div class="example-sentence notranslate">
                    "I bought a gift for ___"
                </div>
                <div class="example-answer object-ans notranslate">
                    → HIM
                </div>
                <div class="example-explanation">
                    <strong class="notranslate">💡 Explanation:</strong>
                    <p class="notranslate">
                        We use an <strong>Object Pronoun</strong> because it receives the action and follows the preposition "for". The gift was bought for whom? For "him". Object pronouns come after verbs or prepositions and receive the action.
                    </p>
                    <p class="notranslate" style="margin-top: 10px; font-style: italic; color: var(--object);">
                        <strong>Other Object Pronouns:</strong> me, you, him, her, it, us, them
                    </p>
                </div>
            </div>

            <!-- Example 3: Possessive Pronoun -->
            <div class="example-card possessive-ex">
                <div class="example-number" style="background: var(--possessive);">3</div>
                <div class="example-sentence notranslate">
                    "The house on the corner is ___"
                </div>
                <div class="example-answer possessive-ans notranslate">
                    → OURS
                </div>
                <div class="example-explanation">
                    <strong class="notranslate">💡 Explanation:</strong>
                    <p class="notranslate">
                        We use a <strong>Possessive Pronoun</strong> to indicate ownership of the house without repeating the noun "house". Instead of saying "The house is our house", we simply say "The house is ours". Possessive pronouns show ownership and stand alone.
                    </p>
                    <p class="notranslate" style="margin-top: 10px; font-style: italic; color: var(--possessive);">
                        <strong>Other Possessive Pronouns:</strong> mine, yours, his, hers, its, ours, theirs
                    </p>
                </div>
            </div>

            <div class="controls">
                <button class="btn btn-secondary" onclick="playSound('click'); showPage('welcomePage')">
                    ⬅️ Back to Welcome
                </button>
                <button class="btn btn-info" onclick="playSound('click'); showPage('instructionsPage')">
                    📖 Instructions
                </button>
                <button class="btn btn-primary" onclick="playSound('click'); showPage('gamePage'); startGame()">
                    🎮 Start Game
                </button>
                <button class="btn btn-info" onclick="playSound('click'); showPage('finalPage')" style="background: linear-gradient(135deg, #FFD700, #FFA500);">
                    🏆 Final Page
                </button>
            </div>
        </div>
    </div>

    <!-- GAME PAGE -->
    <div class="page" id="gamePage">
        <div class="header">
            <h1 class="notranslate">Pronoun Memory Game</h1>
            <p class="subtitle notranslate">Match sentences with their correct pronouns!</p>
        </div>

        <div class="game-stats">
            <div class="stat-box">
                <div class="stat-value" id="moves">0</div>
                <div class="stat-label notranslate">Moves</div>
            </div>
            <div class="stat-box">
                <div class="stat-value" id="matches">0</div>
                <div class="stat-label notranslate">Matches</div>
            </div>
            <div class="stat-box">
                <div class="stat-value" id="timer">00:00</div>
                <div class="stat-label notranslate">Time</div>
            </div>
        </div>

        <div class="controls">
            <button class="btn btn-primary" onclick="playSound('click'); startGame()">🔄 New Game</button>
            <button class="btn btn-secondary" onclick="playSound('click'); showPage('welcomePage')">🏠 Home</button>
            <button class="btn btn-info" onclick="playSound('click'); showPage('instructionsPage')">📖 Help</button>
            <button class="btn btn-info" onclick="playSound('click'); showPage('finalPage')" style="background: linear-gradient(135deg, #FFD700, #FFA500);">🏆 Final Page</button>
        </div>

        <div class="legend">
            <div class="legend-item">
                <div class="legend-color personal"></div>
                <span class="notranslate"><strong>Personal</strong> Pronouns</span>
            </div>
            <div class="legend-item">
                <div class="legend-color possessive"></div>
                <span class="notranslate"><strong>Possessive</strong> Pronouns</span>
            </div>
            <div class="legend-item">
                <div class="legend-color object"></div>
                <span class="notranslate"><strong>Object</strong> Pronouns</span>
            </div>
        </div>

        <div class="game-board" id="gameBoard"></div>
    </div>

    <!-- Win Modal -->
    <div class="modal" id="winModal">
        <div class="modal-content">
            <div class="celebration">🎉🏆🎊</div>
            <h2 class="modal-title notranslate">Congratulations!</h2>
            <p class="modal-message notranslate">You completed the game!</p>
            <p class="modal-message notranslate">
                <strong>Moves:</strong> <span id="finalMoves"></span><br>
                <strong>Time:</strong> <span id="finalTime"></span>
            </p>
            <button class="btn btn-primary" onclick="playSound('win'); closeModal()">Play Again</button>
        </div>
    </div>

    <!-- Celebration Overlay -->
    <div class="celebration-overlay" id="celebrationOverlay">
        <div class="celebration-content">
            <div class="celebration-emoji">🎉</div>
            <h2 class="celebration-title notranslate">PERFECT MATCH!</h2>
            <p class="celebration-message notranslate">
                🌟 Amazing! You've successfully matched all 10 pronoun pairs! 🌟
            </p>
            <div class="celebration-stats">
                <div class="celebration-stat notranslate">
                    <strong>🎯 Total Moves:</strong> <span id="celebrationMoves"></span>
                </div>
                <div class="celebration-stat notranslate">
                    <strong>⏱️ Time Elapsed:</strong> <span id="celebrationTime"></span>
                </div>
                <div class="celebration-stat notranslate">
                    <strong>🏆 Success Rate:</strong> <span id="celebrationRate"></span>%
                </div>
            </div>
            <p class="celebration-message notranslate" style="font-size: 1.2rem;">
                You've mastered Personal, Possessive, and Object Pronouns!
            </p>
            <div class="controls">
                <button class="btn btn-primary" onclick="goToFinalPage()">
                    ✨ View Summary & References
                </button>
            </div>
        </div>
    </div>

    <!-- FINAL PAGE: Congratulations, References and Farewell -->
    <div class="page" id="finalPage">
        <div class="references-content">
            <!-- Congratulations Header -->
            <div style="text-align: center; margin-bottom: 40px;">
                <h1 style="font-size: 2.5rem; font-weight: 800; color: #1a252f; margin-bottom: 20px;" class="notranslate">
                    Congratulations!
                </h1>
                <h2 class="section-title notranslate" style="font-size: 2rem; margin-top: 0; color: var(--dark);">
                    Project Successfully Completed
                </h2>
            </div>

            <!-- Project Summary -->
            <div style="padding: 5px; border-radius: 25px; margin-bottom: 40px;">
                <h3 style="font-size: 2rem; margin-bottom: 25px; text-align: center; color: #1a252f;" class="notranslate">
                    Project Overview
                </h3>
                <div style="padding: 15px; border-radius: 20px;">
                    <div style="line-height: 2; font-size: 1.1rem;">
                        <p style="margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Student:</strong> Cristian Alexander Rojas
                        </p>
                        <p style="margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Institution:</strong> Corporación Universitaria Minuto de Dios
                        </p>
                        <p style="margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Program:</strong> Administración de Empresas
                        </p>
                        <p style="margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Course:</strong> NRC-744 - Inglés I
                        </p>
                        <p style="margin-bottom: 15px; color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Completion Date:</strong> January February 2026
                        </p>
                        <p style="color: var(--dark);" class="notranslate">
                            <strong style="color: #1a252f;">Project:</strong> Interactive Memory Card Game - Pronoun Mastery
                        </p>
                    </div>
                </div>
            </div>

            <!-- Learning Summary -->
            <div style="padding: 5px; border-radius: 25px; margin-bottom: 5px;">
                <h3 style="font-size: 2.5rem; margin-bottom: 30px; text-align: center; color: #1a252f;" class="notranslate">
                    Learning Summary
                </h3>

                <div class="learning-point">
                    <h4 style="color: #1a252f;" class="notranslate">1️⃣ Personal Pronouns (Subject Pronouns)</h4>
                    <p style="color: var(--dark);" class="notranslate">
                        Through this project, I mastered personal pronouns <strong>(I, you, he, she, it, we, they)</strong> which replace the subject of a sentence and represent the person or thing performing the action. These pronouns are essential for avoiding repetition and making communication more natural. For example: "She is my best friend at school" - where "She" acts as the subject performing the action of "being."(Eastwood, 2002).
                    </p>
                </div>

                <div class="learning-point">
                    <h4 style="color: #1a252f;" class="notranslate">2️⃣ Possessive Pronouns</h4>
                    <p style="color: var(--dark);" class="notranslate">
                        I learned that possessive pronouns <strong>(my, your, his, her, its, our, their, mine, yours, hers, ours, theirs)</strong> show ownership and eliminate the need to repeat nouns (Murphy, 2019). I discovered the crucial distinction between possessive adjectives used with nouns (my book, your house) and possessive pronouns that stand alone (the book is mine, the house is yours). This understanding is fundamental for proper English usage and helps create more elegant, concise sentences (Eastwood, 2002).
                    </p>
                </div>

                <div class="learning-point">
                    <h4 style="color: #1a252f;" class="notranslate">3️⃣ Object Pronouns</h4>
                    <p style="color: var(--dark);" class="notranslate">
                        Object pronouns <strong>(me, you, him, her, it, us, them)</strong> receive the action in a sentence or follow prepositions. Through practical examples like "I bought a gift for him," I understood that these pronouns come after verbs or prepositions (Swan, 2016). This knowledge helps me construct grammatically correct sentences and understand the flow of English grammar, particularly in identifying who or what receives an action (Eastwood, 2002).
                    </p>
                </div>

                <div class="learning-point">
                    <h4 style="color: #1a252f;" class="notranslate">4️⃣ Interactive Learning Through Gamification</h4>
                    <p style="color: var(--dark);" class="notranslate">
                        Creating this interactive memory game transformed abstract grammar rules into contextualized, real-world applications. By designing sentences about school, friends, family, and daily activities, I practiced pronouns in authentic situations rather than memorizing isolated rules. This hands-on, gamified approach made learning engaging, memorable, and significantly more effective than traditional study methods (Kapp, 2012).
                    </p>
                </div>

                <div class="learning-point">
                    <h4 style="color: #1a252f;" class="notranslate">5️⃣ Visual Learning & Color-Coding Strategy</h4>
                    <p style="color: var(--dark);" class="notranslate">
                        The implementation of a color-coding system (Red for Personal, Green for Possessive, Blue for Object pronouns) enhanced my ability to quickly identify and categorize pronouns. This multi-sensory approach, combining visual, auditory (sound effects), and kinesthetic (card interaction) learning styles, reinforced grammatical concepts through multiple pathways, resulting in deeper comprehension and longer retention (Paivio, 1991).
                    </p>
                </div>
            </div>

            <!-- References Section -->
            <div style="margin-top: 50px;">
                <h3 style="font-size: 2.5rem; color: var(--dark); margin-bottom: 30px; text-align: center; font-weight: 800;" class="notranslate">
                    References
                </h3>

                <div class="reference-item">
                    <p class="notranslate">
                        <strong>1.</strong> Deterding, S. D. (20 de enero de 2026). From Game Design Elements to Gamefulness: Defining . Obtenido de From Game Design Elements to Gamefulness: Defining  https://www.researchgate.net
                      /publication/230854710_From_Game_
                      Design_Elements_to_Gamefulness_
                      Defining_Gamification
                    </p>
                </div>

                <div class="reference-item">
                    <p class="notranslate">
                        <strong>2.</strong> Eastwood. (15 de junio de 2002). Oxford University Press. Obtenido de Oxford practice grammar: Intermediate: https://sbcatarman.wordpress.com/
                      wp-content/uploads/2024/06/
                      oxford_guide_to_english_
                      grammar.pdf
                    </p>
                </div>

                <div class="reference-item">
                    <p class="notranslate">
                        <strong>3.</strong> Muñoz-Ortiz, F. (2020). <em>Inglés A1</em> (pp. 136-146). Editorial Tutor Formación.
                    </p>
                </div>

                <div class="reference-item">
                    <p class="notranslate">
                        <strong>4.</strong> Pérez-Morales, J. I. (Comp.). (2021). <em>Using Information and Communication Technologies (ICT) in the Teaching and Learning Process of English as a Foreign Language</em> (pp. 17-25). Editorial Feijóo.
                    </p>
                </div>

                <div class="reference-item">
                    <p class="notranslate">
                        <strong>5.</strong> Kapp, K. M. (1 de mayo de 2012). The Gamification of Learning and Instruction: Game-based ... Obtenido de The Gamification of Learning and Instruction: Game-based https://books.google.com.co/
                      books/about/The_Gamification_
                      of_Learning_and_Instruc
                      .html?id=M2Rb9ZtFxccC&redir_esc=y
                    </p>
                </div>

                <div class="reference-item">
                    <p class="notranslate">
                        <strong>6.</strong> Fleming, N. D. (13 de agosto de 1992). (PDF) Not Another Inventory, Rather a Catalyst for Reflection. Obtenido de (PDF) Not Another Inventory, Rather a Catalyst for Reflection: https://www.academia.edu/291884/
                      Not_Another_Inventory_
                      Rather_a_Catalyst_for_Reflection
                    </p>
                </div>
            </div>

            <!-- Final Reflection -->
            <div style="padding: 20px; border-radius: 25px; margin-top: 50px; margin-bottom: 40px;">
                <h3 style="font-size: 2.2rem; margin-bottom: 25px; text-align: center; color: #1a252f;" class="notranslate">
                    Conclusion
                </h3>
                <p style="font-size: 1.2rem; line-height: 1.9; text-align: justify; color: var(--dark);" class="notranslate">
                    This interactive memory game project successfully demonstrates the integration of technology, creativity, and language education. By combining game design principles with grammatical instruction, I have created an innovative learning tool that transforms pronoun practice from a tedious memorization task into an engaging, interactive experience. The project showcases not only technical proficiency in web development but also pedagogical understanding of effective language learning strategies.
                </p>
                <p style="font-size: 1.2rem; line-height: 1.9; text-align: justify; margin-top: 20px; color: var(--dark);" class="notranslate">
                    Through the development process, I gained valuable insights into user interface design, interactive animations, responsive web development, and educational game mechanics. More importantly, I deepened my understanding of English pronoun usage by creating contextualized examples and categorizing them systematically. This hands-on approach to learning has proven far more effective than passive study methods, resulting in both practical language skills and technical competencies that will serve me well in my academic and professional journey.
                </p>
            </div>

            <!-- Farewell Message -->
            <div style="background: linear-gradient(135deg, #f5f7fa, #c3cfe2); padding: 5px; border-radius: 25px; margin-bottom: 40px; text-align: center; box-shadow: 0 10px 30px rgba(0,0,0,0.1);">
                <div style="font-size: 4rem; margin-bottom: 20px;">👋</div>
                <h3 style="font-size: 2.2rem; color: var(--dark); margin-bottom: 20px; font-weight: 800;" class="notranslate">
                    Thank You for Playing!
                </h3>
                <p style="font-size: 1.3rem; line-height: 1.8; color: var(--dark); margin-bottom: 20px;" class="notranslate">
                    Thank you for taking the time to experience this interactive learning journey. I hope this game has made practicing English pronouns both educational and enjoyable. Remember, consistent practice is the key to language mastery!
                </p>
                <p style="font-size: 1.2rem; color: var(--dark); opacity: 0.8; font-style: italic;" class="notranslate">
                    "Learning is not a spectator sport." - D. Blocher
                </p>
                <div style="margin-top: 30px; padding-top: 30px; border-top: 2px solid rgba(0,0,0,0.1);">
                    <p style="font-size: 1.1rem; color: var(--dark);" class="notranslate">
                        <strong>Created with dedication by:</strong><br>
                        Cristian Alexander Rojas<br>
                        Corporación Universitaria Minuto de Dios<br>
                        January 2026
                    </p>
                </div>
            </div>

            <div class="controls">
                <button class="btn btn-secondary" onclick="playSound('click'); showPage('presentationPage')">
                    🏠 Return to Start
                </button>
                <button class="btn btn-primary" onclick="playSound('click'); showPage('gamePage'); startGame()">
                    🔄 Play Again
                </button>
            </div>
        </div>
    </div>

    <script>
        // Prevent translation
        document.documentElement.setAttribute('translate', 'no');
        
        // Game data
        const gameData = [
            { id: 1, type: 'sentence', text: '_____ am a student.', match: 'I', category: 'personal' },
            { id: 2, type: 'pronoun', text: 'I', match: '_____ am a student.', category: 'personal' },
            
            { id: 3, type: 'sentence', text: 'This is _____ house.', match: 'my', category: 'possessive' },
            { id: 4, type: 'pronoun', text: 'my', match: 'This is _____ house.', category: 'possessive' },
            
            { id: 5, type: 'sentence', text: 'Please call _____ tomorrow.', match: 'me', category: 'object' },
            { id: 6, type: 'pronoun', text: 'me', match: 'Please call _____ tomorrow.', category: 'object' },
            
            { id: 7, type: 'sentence', text: '_____ is my best friend.', match: 'She', category: 'personal' },
            { id: 8, type: 'pronoun', text: 'She', match: '_____ is my best friend.', category: 'personal' },
            
            { id: 9, type: 'sentence', text: 'That car is _____.', match: 'hers', category: 'possessive' },
            { id: 10, type: 'pronoun', text: 'hers', match: 'That car is _____.', category: 'possessive' },
            
            { id: 11, type: 'sentence', text: 'I saw _____ at the park.', match: 'him', category: 'object' },
            { id: 12, type: 'pronoun', text: 'him', match: 'I saw _____ at the park.', category: 'object' },
            
            { id: 13, type: 'sentence', text: '_____ are going to school.', match: 'We', category: 'personal' },
            { id: 14, type: 'pronoun', text: 'We', match: '_____ are going to school.', category: 'personal' },
            
            { id: 15, type: 'sentence', text: '_____ dog is friendly.', match: 'Our', category: 'possessive' },
            { id: 16, type: 'pronoun', text: 'Our', match: '_____ dog is friendly.', category: 'possessive' },
            
            { id: 17, type: 'sentence', text: 'The teacher helped _____.', match: 'us', category: 'object' },
            { id: 18, type: 'pronoun', text: 'us', match: 'The teacher helped _____.', category: 'object' },
            
            { id: 19, type: 'sentence', text: '_____ play soccer daily.', match: 'They', category: 'personal' },
            { id: 20, type: 'pronoun', text: 'They', match: '_____ play soccer daily.', category: 'personal' },
            
            { id: 21, type: 'wildcard', text: '⭐ EXTRA TURN!', subtext: 'Flip again!', category: 'wildcard-extra' },
            { id: 22, type: 'wildcard', text: '❌ LOSE A PAIR!', subtext: 'Return last match', category: 'wildcard-lose' }
        ];

        let cards = [];
        let flippedCards = [];
        let matchedPairs = 0;
        let moves = 0;
        let timer = 0;
        let timerInterval;
        let gameStarted = false;
        let lastMatchedPair = null;
        let soundEnabled = true;

        // Sound effects using Web Audio API
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();

        function playSound(type) {
            if (!soundEnabled) return;
            
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            switch(type) {
                case 'flip':
                    oscillator.frequency.value = 400;
                    gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.1);
                    oscillator.start(audioContext.currentTime);
                    oscillator.stop(audioContext.currentTime + 0.1);
                    break;
                case 'match':
                    oscillator.frequency.value = 800;
                    gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.3);
                    oscillator.start(audioContext.currentTime);
                    oscillator.stop(audioContext.currentTime + 0.3);
                    break;
                case 'wrong':
                    oscillator.frequency.value = 200;
                    gainNode.gain.setValueAtTime(0.2, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.2);
                    oscillator.start(audioContext.currentTime);
                    oscillator.stop(audioContext.currentTime + 0.2);
                    break;
                case 'win':
                    // Victory fanfare
                    [523, 659, 784, 1047].forEach((freq, i) => {
                        const osc = audioContext.createOscillator();
                        const gain = audioContext.createGain();
                        osc.connect(gain);
                        gain.connect(audioContext.destination);
                        osc.frequency.value = freq;
                        gain.gain.setValueAtTime(0.3, audioContext.currentTime + i * 0.1);
                        gain.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + i * 0.1 + 0.3);
                        osc.start(audioContext.currentTime + i * 0.1);
                        osc.stop(audioContext.currentTime + i * 0.1 + 0.3);
                    });
                    break;
                case 'click':
                    oscillator.frequency.value = 600;
                    gainNode.gain.setValueAtTime(0.2, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.05);
                    oscillator.start(audioContext.currentTime);
                    oscillator.stop(audioContext.currentTime + 0.05);
                    break;
            }
        }

        function toggleSound() {
            soundEnabled = !soundEnabled;
            document.getElementById('soundToggle').textContent = soundEnabled ? '🔊' : '🔇';
            playSound('click');
        }

        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId).classList.add('active');
        }

        function shuffle(array) {
            const newArray = [...array];
            for (let i = newArray.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [newArray[i], newArray[j]] = [newArray[j], newArray[i]];
            }
            return newArray;
        }

        function startGame() {
            cards = shuffle([...gameData]);
            flippedCards = [];
            matchedPairs = 0;
            moves = 0;
            timer = 0;
            gameStarted = false;
            lastMatchedPair = null;
            clearInterval(timerInterval);
            
            document.getElementById('moves').textContent = '0';
            document.getElementById('matches').textContent = '0';
            document.getElementById('timer').textContent = '00:00';
            
            renderBoard();
        }

        function renderBoard() {
            const board = document.getElementById('gameBoard');
            board.innerHTML = '';
            
            cards.forEach((card, index) => {
                const cardElement = document.createElement('div');
                cardElement.className = 'card';
                cardElement.dataset.index = index;
                cardElement.setAttribute('translate', 'no');
                
                const frontFace = document.createElement('div');
                frontFace.className = 'card-face card-front';
                frontFace.innerHTML = '<div class="card-icon">🎴</div><div class="card-content notranslate">Click to flip!</div>';
                
                const backFace = document.createElement('div');
                backFace.className = `card-face card-back ${card.category}`;
                backFace.setAttribute('translate', 'no');
                
                if (card.type === 'sentence') {
                    backFace.innerHTML = `
                        <div class="card-content notranslate">${card.text}</div>
                        <div class="card-type notranslate">${card.category} pronoun</div>
                    `;
                } else if (card.type === 'pronoun') {
                    backFace.innerHTML = `
                        <div class="pronoun-answer notranslate">${card.text}</div>
                        <div class="card-type notranslate">${card.category}</div>
                    `;
                } else {
                    backFace.innerHTML = `
                        <div class="card-content notranslate" style="font-size: 1.4rem; font-weight: 800;">${card.text}</div>
                        <div class="card-content notranslate" style="font-size: 0.85rem; margin-top: 8px;">${card.subtext}</div>
                    `;
                }
                
                cardElement.appendChild(frontFace);
                cardElement.appendChild(backFace);
                cardElement.addEventListener('click', () => flipCard(index));
                
                board.appendChild(cardElement);
            });
        }

        function flipCard(index) {
            if (!gameStarted) {
                gameStarted = true;
                startTimer();
            }
            
            const cardElement = document.querySelectorAll('.card')[index];
            
            if (flippedCards.length >= 2 || 
                cardElement.classList.contains('flipped') || 
                cardElement.classList.contains('matched')) {
                return;
            }
            
            playSound('flip');
            cardElement.classList.add('flipped');
            flippedCards.push(index);
            
            if (flippedCards.length === 2) {
                moves++;
                document.getElementById('moves').textContent = moves;
                setTimeout(checkMatch, 800);
            }
        }

        function checkMatch() {
            const [index1, index2] = flippedCards;
            const card1 = cards[index1];
            const card2 = cards[index2];
            
            const cardElements = document.querySelectorAll('.card');
            
            // Check for wildcards
            if (card1.type === 'wildcard' || card2.type === 'wildcard') {
                handleWildcard(card1.type === 'wildcard' ? card1 : card2);
                cardElements[index1].classList.remove('flipped');
                cardElements[index2].classList.remove('flipped');
                flippedCards = [];
                return;
            }
            
            // Check for match (only count sentence-pronoun pairs)
            if ((card1.type === 'sentence' && card2.type === 'pronoun' && card1.match === card2.text) ||
                (card2.type === 'sentence' && card1.type === 'pronoun' && card2.match === card1.text)) {
                
                playSound('match');
                cardElements[index1].classList.add('matched');
                cardElements[index2].classList.add('matched');
                matchedPairs++;
                lastMatchedPair = [index1, index2];
                document.getElementById('matches').textContent = matchedPairs;
                
                // Win condition: all 10 pronoun pairs matched (not including wildcards)
                if (matchedPairs === 10) {
                    setTimeout(showWinModal, 500);
                }
            } else {
                playSound('wrong');
                cardElements[index1].classList.remove('flipped');
                cardElements[index2].classList.remove('flipped');
            }
            
            flippedCards = [];
        }

        function handleWildcard(wildcard) {
            const message = document.createElement('div');
            message.className = 'wildcard-message';
            message.setAttribute('translate', 'no');
            
            if (wildcard.category === 'wildcard-extra') {
                playSound('match');
                message.innerHTML = '⭐<br><strong style="color: #F1C40F;">EXTRA TURN!</strong><br>Keep playing!';
                message.style.background = 'linear-gradient(135deg, #FFF9E6, #F1C40F)';
            } else {
                playSound('wrong');
                message.innerHTML = '❌<br><strong style="color: #E74C3C;">LOSE A PAIR!</strong><br>Last match removed';
                message.style.background = 'linear-gradient(135deg, #FFE6E6, #E74C3C)';
                
                if (lastMatchedPair && matchedPairs > 0) {
                    const cardElements = document.querySelectorAll('.card');
                    // Remove matched class to flip cards back
                    cardElements[lastMatchedPair[0]].classList.remove('matched');
                    cardElements[lastMatchedPair[1]].classList.remove('matched');
                    cardElements[lastMatchedPair[0]].classList.remove('flipped');
                    cardElements[lastMatchedPair[1]].classList.remove('flipped');
                    
                    // Decrease match counter
                    matchedPairs--;
                    document.getElementById('matches').textContent = matchedPairs;
                    lastMatchedPair = null;
                }
            }
            
            document.body.appendChild(message);
            setTimeout(() => message.remove(), 2000);
        }

        function startTimer() {
            timerInterval = setInterval(() => {
                timer++;
                const minutes = Math.floor(timer / 60).toString().padStart(2, '0');
                const seconds = (timer % 60).toString().padStart(2, '0');
                document.getElementById('timer').textContent = `${minutes}:${seconds}`;
            }, 1000);
        }

        function showWinModal() {
            clearInterval(timerInterval);
            
            // Show celebration overlay with effects
            showCelebration();
        }

        function showCelebration() {
            const overlay = document.getElementById('celebrationOverlay');
            overlay.classList.add('active');
            
            // Calculate success rate
            const successRate = ((10 / moves) * 100).toFixed(1);
            
            const minutes = Math.floor(timer / 60).toString().padStart(2, '0');
            const seconds = (timer % 60).toString().padStart(2, '0');
            
            document.getElementById('celebrationMoves').textContent = moves;
            document.getElementById('celebrationTime').textContent = `${minutes}:${seconds}`;
            document.getElementById('celebrationRate').textContent = successRate;
            
            // Play celebration sound
            playCelebrationSound();
            
            // Create confetti
            createConfetti();
            
            // Create fireworks
            createFireworks();
            
            // Flash effect
            createFlash();
        }

        function playCelebrationSound() {
            if (!soundEnabled) return;
            
            // Victory fanfare with multiple notes
            const notes = [523, 587, 659, 698, 784, 880, 988, 1047];
            notes.forEach((freq, i) => {
                setTimeout(() => {
                    const oscillator = audioContext.createOscillator();
                    const gainNode = audioContext.createGain();
                    oscillator.connect(gainNode);
                    gainNode.connect(audioContext.destination);
                    oscillator.frequency.value = freq;
                    gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
                    gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
                    oscillator.start(audioContext.currentTime);
                    oscillator.stop(audioContext.currentTime + 0.5);
                }, i * 100);
            });
        }

        function createConfetti() {
            const colors = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#FFA07A', '#98D8C8', '#F7DC6F', '#BB8FCE', '#85C1E2'];
            
            for (let i = 0; i < 100; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = Math.random() * 100 + '%';
                    confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.animationDelay = Math.random() * 2 + 's';
                    confetti.style.animationDuration = (Math.random() * 2 + 2) + 's';
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => confetti.remove(), 5000);
                }, i * 30);
            }
        }

        function createFireworks() {
            const colors = ['#FF6B6B', '#4ECDC4', '#45B7D1', '#FFA07A', '#F7DC6F'];
            
            for (let i = 0; i < 15; i++) {
                setTimeout(() => {
                    const x = Math.random() * window.innerWidth;
                    const y = Math.random() * window.innerHeight * 0.6;
                    
                    for (let j = 0; j < 20; j++) {
                        const firework = document.createElement('div');
                        firework.className = 'firework firework-particle';
                        firework.style.left = x + 'px';
                        firework.style.top = y + 'px';
                        firework.style.background = colors[Math.floor(Math.random() * colors.length)];
                        
                        const angle = (Math.PI * 2 * j) / 20;
                        const velocity = 50 + Math.random() * 50;
                        const tx = Math.cos(angle) * velocity;
                        const ty = Math.sin(angle) * velocity;
                        
                        firework.style.animation = `fireworkExplode 1s ease-out forwards`;
                        firework.style.transform = `translate(${tx}px, ${ty}px)`;
                        
                        document.body.appendChild(firework);
                        
                        setTimeout(() => firework.remove(), 1000);
                    }
                }, i * 300);
            }
        }

        function createFlash() {
            const flash = document.createElement('div');
            flash.className = 'flash';
            document.body.appendChild(flash);
            setTimeout(() => flash.remove(), 500);
        }

        function goToFinalPage() {
            playSound('click');
            document.getElementById('celebrationOverlay').classList.remove('active');
            showPage('finalPage');
        }

        function closeModal() {
            document.getElementById('winModal').classList.remove('active');
            showPage('finalPage');
        }

        // Initialize game data on load
        document.addEventListener('DOMContentLoaded', function() {
            // Prevent right-click translation
            document.addEventListener('contextmenu', function(e) {
                e.preventDefault();
            });
        });
    </script>
</body>
</html>
