# Typing-Speed-Test-Game
### Hosted Link: https://divyanshrajpoot9.github.io/Typing-Speed-Test-Game/
## Yup

### HTML Structure:
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>typing test</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
<section class="main-body">
    <h2>Typing Speed Test Game</h2>
    <p id="showSentence"></p>
    <div class="typing_section">
        <label for="textarea"></label>
        <textarea name="textarea" id="textarea" cols="30" rows="10" disabled></textarea>
        <br>
        <button id="btn">Start</button>
    </div>
    <p id="score"></p>
</section>
<script src="script.js"></script>
</body>
</html>

### JavaScript:
#### Step 1: Variable Declarations
const typing_ground = document.querySelector('#textarea');
const btn = document.querySelector('#btn');
const score = document.querySelector('#score');
const show_sentence = document.querySelector('#showSentence');
let startTime, endTime, totalTimeTaken;

These variables store references to HTML elements (`textarea`, `button`, `score`, `showSentence`) and variables to track the start time, end time, and total time taken during the typing test.

#### Step 2: Event Listener for Button Click
javascript
btn.addEventListener('click', () => {
    switch (btn.innerText.toLowerCase()) {
        case "start":
            typing_ground.removeAttribute('disabled');
            startTyping();
            break;

        case "done":
            typing_ground.setAttribute('disabled' , 'true');
            endTypingTest();
            break;
    }
});

This event listener checks the text content of the button. If it's "Start," it enables the textarea and starts the typing test. If it's "Done," it disables the textarea and ends the typing test.

#### Step 3: `startTyping` Function
const startTyping = () => {
    let randomNumber = Math.floor(Math.random() * sentences.length);
    show_sentence.innerHTML = sentences[randomNumber];

    let date = new Date();
    startTime = date.getTime();

    btn.innerText = "Done";
};

This function selects a random sentence from the `sentences` array, displays it, and records the start time. It also changes the button text to "Done."

#### Step 4: `endTypingTest` Function
const endTypingTest = () => {
    btn.innerText = "Start";

    let date = new Date();
    endTime = date.getTime();
    totalTimeTaken = (endTime - startTime) / 1000;

    calculateTypingSpeed(totalTimeTaken);

    show_sentence.innerHTML = "";
    typing_ground.value = "";
};


This function sets the button text back to "Start," records the end time, calculates the total time taken, and then calls the `calculateTypingSpeed` function.

#### Step 5: calculateTypingSpeed Function
const calculateTypingSpeed = (time_taken) => {
    let totalWords = typing_ground.value.trim();
    let actualWords = totalWords === '' ? 0 : totalWords.split(" ").length;

    if (actualWords !== 0) {
        let typing_speed = (actualWords / time_taken) * 60;
        typing_speed = Math.round(typing_speed);
        score.innerHTML = `Your typing speed is ${typing_speed} words per minute & you wrote ${actualWords} words & time taken ${time_taken} sec`;
    } else {
        score.innerHTML = `Your typing speed is 0 words per minute & time taken ${time_taken} sec`;
    }
};
This function calculates the typing speed based on the total words typed, time taken, and displays the result in the `score` element.

### Conclusion:
This code creates a simple typing speed test game where users can start typing a randomly selected sentence, and upon completion, the game calculates and displays the typing speed. The user can start a new test by clicking the "Start" button.
