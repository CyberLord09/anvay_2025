---
layout: post
title: Hangman Game
description: Hangman game coded with HTML, Javascript, and CSS
type: hacks
---

<style>
    body {
        display: flex;
        align-items: center;
        padding: 0 10px;
        justify-content: center;
        min-height: 100vh;
    }
    .container {
        width: 700px;
        background: #256086;
        display: flex;
        gap: 70px;
        align-items: flex-end;
        padding: 60px 40px;
        border-radius: 10px;
    }
    .container .hint-text {
        color: #fff;
    }
    .container .hangman-box h1 {
        color: #fff;
    }
    .hangman-box img {
        max-width: 270px;
    }
    .hangman-box h1 {
        font-size: 1.45rem;
        text-align: center;
        margin-top: 20px;
        text-transform: uppercase;
    }
    .word-display {
        display: flex;
        gap: 10px;
        list-style: none;
        align-items: center;
        justify-content: center;
    }
    .word-display .letter {
        width: 28px;
        font-size: 2rem;
        font-weight: 600;
        text-align: center;
        text-transform: uppercase;
        margin-bottom: 40px;
        border-bottom: 3px solid #fff;
    }
    .word-display .letter.guessed {
        border-color: transparent;
        margin: -40px 0 35px;
    }
    .game-box h4 {
        text-align: center;
        font-size: 1.1rem;
        font-weight: 500;
        margin-bottom: 15px;
    }
    .game-box h4 b {
        font-weight: 600;
    }
    .game-box .guesses-text b {
        color: #ff0000;
    }
    .game-box .guesses-text {
        color: #fff;
    }     
    .game-box .keyboard {
        display: flex;
        gap: 5px;
        margin-top: 40px;
        flex-wrap: wrap;
        justify-content: center;
    }
    :where(.game-modal, .keyboard) button {
        color: #346187;
        font-size: 1rem;
        font-weight: 600;
        background: #fff;
        cursor: pointer;
        outline: none;
        padding: 4px;
        border: none;
        border-radius: 4px;
        text-transform: uppercase;
    }
    .keyboard button {
        padding: 7px;
        width: calc(100% / 9 - 5px);
    } 
    .keyboard button[disabled] {
        opacity: 0.6;
        pointer-events: none;
    }  
    :where(.game-modal, .keyboard) button:hover {
        background: #74b8f7;
    }
    .game-modal {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        opacity: 0;
        padding: 0 10px;
        pointer-events: none;
        z-index: 999;
        display: flex;
        align-items: center;
        justify-content: center;
        background: rgba(0,0,0,0.6);
        transition: opacity 0.4s ease;
    }
    .game-modal.show {
        opacity: 1;
        pointer-events: auto;
    }
    .game-modal .content {
        max-width: 420px;
        background: #fff;
        width: 100%;
        text-align: center;
        border-radius: 10px;
        padding: 30px;
    }     
    .game-modal img {
        max-width: 130px;
        margin-bottom: 20px;
    }
    .game-modal h4 {
        font-size: 1.53rem;
        color: #000;
    }
    .game-modal p {
        font-size: 1.15rem;
        margin: 15px 0 30px;
        font-weight: 500;
        color: #000;
    }
    .game-modal p b {
        color: #5E63BA;
        font-weight: 600;
    }
    .game-modal button {
        padding: 12px 23px;
    }
    @media (max-width: 782px) {
    .container {
        flex-direction: column;
        padding: 30px 15px;
        align-items: center;
    }
    .hangman-box img {
        max-width: 200px;
    }
    .hangman-box h1 {
        display: none;
    }
    }
</style>

<div class="game-modal">
    <div class="content">
        <img src="{{site.baseurl}}/images/hangman/lost.gif" alt="gif">
        <h4>Game Over!</h4>
        <p>The correct word was: <b>rainbow</b></p>
        <button class="play-again">Play Again</button>
    </div>
</div>
<div class="container">
    <div class="hangman-box">
        <img src="{{site.baseurl}}/images/hangman/hangman-0.svg" alt="hangman-img">
        <h1>Hangman Game</h1>
    </div>
    <div class="game-box">
        <ul class="word-display"></ul>
        <h4 class="hint-text">
            Hint: 
            <b>ajfdiajdoijaiosdjiaosjdioajsdoijasidjasdiajsodjiasd</b>
        </h4>
        <h4 class="guesses-text">
            Incorrect Guesses: 
            <b>0 / 6</b>
        </h4>
        <div class="keyboard"></div>
    </div>
</div>

<script>
    const keyboardDiv = document.querySelector(".keyboard");
    const hangmanImage = document.querySelector(".hangman-box img");
    const guessesText = document.querySelector(".guesses-text b");
    const wordDisplay = document.querySelector(".word-display");
    const gameModal = document.querySelector(".game-modal");
    const playAgainBtn = document.querySelector(".play-again");
    
    const wordList = [
    {
        word: "guitar",
        hint: "A musical instrument with strings."
    },
    {
        word: "oxygen",
        hint: "A colorless, odorless gas essential for life."
    },
    {
        word: "mountain",
        hint: "A large natural elevation of the Earth's surface."
    },
    {
        word: "painting",
        hint: "An art form using colors on a surface to create images or expression."
    },
    {
        word: "astronomy",
        hint: "The scientific study of celestial objects and phenomena."
    },
    {
        word: "football",
        hint: "A popular sport played with a spherical ball."
    },
    {
        word: "chocolate",
        hint: "A sweet treat made from cocoa beans."
    },
    {
        word: "butterfly",
        hint: "An insect with colorful wings and a slender body."
    },
    {
        word: "history",
        hint: "The study of past events and human civilization."
    },
    {
        word: "pizza",
        hint: "A savory dish consisting of a round, flattened base with toppings."
    },
    {
        word: "jazz",
        hint: "A genre of music characterized by improvisation and syncopation."
    },
    {
        word: "camera",
        hint: "A device used to capture and record images or videos."
    },
    {
        word: "diamond",
        hint: "A precious gemstone known for its brilliance and hardness."
    },
    {
        word: "adventure",
        hint: "An exciting or daring experience."
    },
    {
        word: "science",
        hint: "The systematic study of the structure and behavior of the physical and natural world."
    },
    {
        word: "bicycle",
        hint: "A human-powered vehicle with two wheels."
    },
    {
        word: "sunset",
        hint: "The daily disappearance of the sun below the horizon."
    },
    {
        word: "coffee",
        hint: "A popular caffeinated beverage made from roasted coffee beans."
    },
    {
        word: "dance",
        hint: "A rhythmic movement of the body often performed to music."
    },
    {
        word: "galaxy",
        hint: "A vast system of stars, gas, and dust held together by gravity."
    },
    {
        word: "orchestra",
        hint: "A large ensemble of musicians playing various instruments."
    },
    {
        word: "volcano",
        hint: "A mountain or hill with a vent through which lava, rock fragments, hot vapor, and gas are ejected."
    },
    {
        word: "novel",
        hint: "A long work of fiction, typically with a complex plot and characters."
    },
    {
        word: "sculpture",
        hint: "A three-dimensional art form created by shaping or combining materials."
    },
    {
        word: "symphony",
        hint: "A long musical composition for a full orchestra, typically in multiple movements."
    },
    {
        word: "architecture",
        hint: "The art and science of designing and constructing buildings."
    },
    {
        word: "ballet",
        hint: "A classical dance form characterized by precise and graceful movements."
    },
    {
        word: "astronaut",
        hint: "A person trained to travel and work in space."
    },
    {
        word: "waterfall",
        hint: "A cascade of water falling from a height."
    },
    {
        word: "technology",
        hint: "The application of scientific knowledge for practical purposes."
    },
    {
        word: "rainbow",
        hint: "A meteorological phenomenon that is caused by reflection, refraction, and dispersion of light."
    },
    {
        word: "universe",
        hint: "All existing matter, space, and time as a whole."
    },
    {
        word: "piano",
        hint: "A musical instrument played by pressing keys that cause hammers to strike strings."
    },
    {
        word: "vacation",
        hint: "A period of time devoted to pleasure, rest, or relaxation."
    },
    {
        word: "rainforest",
        hint: "A dense forest characterized by high rainfall and biodiversity."
    },
    {
        word: "theater",
        hint: "A building or outdoor area in which plays, movies, or other performances are staged."
    },
    {
        word: "telephone",
        hint: "A device used to transmit sound over long distances."
    },
    {
        word: "language",
        hint: "A system of communication consisting of words, gestures, and syntax."
    },
    {
        word: "desert",
        hint: "A barren or arid land with little or no precipitation."
    },
    {
        word: "sunflower",
        hint: "A tall plant with a large yellow flower head."
    },
    {
        word: "fantasy",
        hint: "A genre of imaginative fiction involving magic and supernatural elements."
    },
    {
        word: "telescope",
        hint: "An optical instrument used to view distant objects in space."
    },
    {
        word: "breeze",
        hint: "A gentle wind."
    },
    {
        word: "oasis",
        hint: "A fertile spot in a desert where water is found."
    },
    {
        word: "photography",
        hint: "The art, process, or practice of creating images by recording light or other electromagnetic radiation."
    },
    {
        word: "safari",
        hint: "An expedition or journey, typically to observe wildlife in their natural habitat."
    },
    {
        word: "planet",
        hint: "A celestial body that orbits a star and does not produce light of its own."
    },
    {
        word: "river",
        hint: "A large natural stream of water flowing in a channel to the sea, a lake, or another such stream."
    },
    {
        word: "tropical",
        hint: "Relating to or situated in the region between the Tropic of Cancer and the Tropic of Capricorn."
    },
    {
        word: "mysterious",
        hint: "Difficult or impossible to understand, explain, or identify."
    },
    {
        word: "enigma",
        hint: "Something that is mysterious, puzzling, or difficult to understand."
    },
    {
        word: "paradox",
        hint: "A statement or situation that contradicts itself or defies intuition."
    },
    {
        word: "puzzle",
        hint: "A game, toy, or problem designed to test ingenuity or knowledge."
    },
    {
        word: "whisper",
        hint: "To speak very softly or quietly, often in a secretive manner."
    },
    {
        word: "shadow",
        hint: "A dark area or shape produced by an object blocking the light."
    },
    {
        word: "secret",
        hint: "Something kept hidden or unknown to others."
    },
    {
        word: "curiosity",
        hint: "A strong desire to know or learn something."
    },
    {
        word: "unpredictable",
        hint: "Not able to be foreseen or known beforehand; uncertain."
    },
    {
        word: "obfuscate",
        hint: "To confuse or bewilder someone; to make something unclear or difficult to understand."
    },
    {
        word: "unveil",
        hint: "To make known or reveal something previously secret or unknown."
    },
    {
        word: "illusion",
        hint: "A false perception or belief; a deceptive appearance or impression."
    },
    {
        word: "moonlight",
        hint: "The light from the moon."
    },
    {
        word: "vibrant",
        hint: "Full of energy, brightness, and life."
    },
    {
        word: "nostalgia",
        hint: "A sentimental longing or wistful affection for the past."
    },
    {
        word: "brilliant",
        hint: "Exceptionally clever, talented, or impressive."
    },
    ];

    let currentWord, correctLetters, wrongGuessCount;
    const maxGuesses = 6;

    const resetGame = () => {
        correctLetters = [];
        wrongGuessCount = 0;
        hangmanImage.src = `{{site.baseurl}}/images/hangman/hangman-${wrongGuessCount}.svg`;
        guessesText.innerText = `${wrongGuessCount} / ${maxGuesses}`;
        keyboardDiv.querySelectorAll("button").forEach(btn => btn.disabled = false);
        wordDisplay.innerHTML = currentWord.split("").map(() => `<li class="letter"></li>`).join("");
        gameModal.classList.remove("show");
    }

    const getRandomWord = () => {
        const { word, hint } = wordList[Math.floor(Math.random() * wordList.length)];
        currentWord = word;
        console.log(word);
        document.querySelector(".hint-text b").innerText = hint;
        resetGame();
    }

    const gameOver = (isVictory) => {
        setTimeout(() => {
            const modalText = isVictory ? `You found the word:` : `The correct word was:` ;
            gameModal.querySelector("img").src = `{{site.baseurl}}/images/hangman/${isVictory ? `victory` : 'lost'}.gif`;
            gameModal.querySelector("h4").innerText = `${isVictory ? 'Congrats!' : 'Game Over!'}`;
            gameModal.querySelector("p").innerHTML = `${modalText} <b>${currentWord}</b>`;
            gameModal.classList.add("show");
        }, 300);
    }

    const initGame = (button, clickedLetter) => {
        if(currentWord.includes(clickedLetter)) {
            [...currentWord].forEach((letter, index) => {
                if(letter === clickedLetter) {
                    correctLetters.push(letter);
                    wordDisplay.querySelectorAll("li")[index].innerText = letter;
                    wordDisplay.querySelectorAll("li")[index].classList.add("guessed");
                }
            })
        } else {
            wrongGuessCount++;
            hangmanImage.src = `{{site.baseurl}}/images/hangman/hangman-${wrongGuessCount}.svg`;
        }

        button.disabled = true;
        guessesText.innerText = `${wrongGuessCount} / ${maxGuesses}`;

        if(wrongGuessCount === maxGuesses) return gameOver(false);
        if(correctLetters.length === currentWord.length) return gameOver(true);
    }

    for (let i = 97; i <= 122; i++) {
        const button = document.createElement("button");
        button.innerText = String.fromCharCode(i);
        keyboardDiv.appendChild(button);
        button.addEventListener("click", e => initGame(e.target, String.fromCharCode(i)));
    }

    getRandomWord()
    playAgainBtn.addEventListener("click", getRandomWord);
</script>
