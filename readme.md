# Quiz Application in JavaScript

## Problem Statement

This application is designed to function as a timed quiz application. Users are presented with multiple choice questions and are given a certain amount of time to answer each question. At the end of each question, the correct answer is presented to the user, and the number of questions answered correctly is tallied. The final score of the user is presented at the end of the quiz once all the questions have been answered.

## Functional Features

- A home page with a "Start Quiz" button that allows the user to begin the quiz.

- Once the quiz has been initiated, a rules page is presented that allows the user to understand how the quiz will proceed, the time limit for each question, how to select an answer, how to exit the quiz, etc.

- At the bottom of the rules page, there is a button that allows the user to proceed to the quiz.

- The quiz questions are in multiple choice format with 4 options presented to the user to select from.

- A countdown timer is visible, both in numerical format and in progress bar format, which allows the user to know how much time is remaining to answer the question.

- When the user selects a response, the application displays visually to the user if the response was correct using coloring and symbols.

- If the response was incorrect, the application displays visually to the user that the response was incorrect using coloring and symbols, and highlights the correct answer for the user.

- If no response was selected and the timer runs out, the correct answer is presented to the user automatically.

- The current question number and total number of questions in the quiz is presented to the user.

- The user advances to the next question by pressing a button.

- As the quiz progresses, the total number of correct answers is tallied.

- Once all questions have been answered, the total number of correctly answered questions is presented to the user, with a dynamic sentence that changes what it says according to the number of questions the user got correct.

- At the end of the quiz, the user is presented with the option to either replay the quiz, or quit.

## Directory Structure

To begin building this application, please construct the following directory structure for your project:

1. In the root directory of your project folder, create two folders entitled **css** and **js**.

2. In the root directory, also create a file entitled **index.html**. This will be the main html page that will host all of your content.

3. In the **css** folder, create a file called **style.css**. This is where all of the syling rules for the application will be documented.

4. In the **js** folder, create two files:

   - **questions.js** - This will store an array of objects that represent the questions of your quiz, along with their corresponding multiple choice options and the correct response.

   - **quizApp.js** - This will contain all of the logic of your application that allows it to function as designed.

Once the above directory structure has been created, you are now ready to begin building your application.

## Codebase

The following section will present a detailed explanation of the codebase found in each of the aforementioned files.

### HTML

---

### index.html

1. Begin your html document with standard formatting for HTML5. This will include a `<head>` and a `<body>` element.

2. In your `<head>` section, input the following code:

   ```html
   <!-- CSS FILE -->
   <link rel="stylesheet" href="css/style.css" />

   <!-- This is my personal font awesome kit code. you will have to add your own after you register with email-->
   <script
     src="https://kit.fontawesome.com/4a4f4b55b0.js"
     crossorigin="anonymous"
   ></script>

   <!-- Add questions list -->
   <script src="js/questions.js" defer></script>

   <!-- Main logic of the app -->
   <script src="js/quizApp.js" defer></script>
   ```

   These four links accomplish the following:

   - The first line links the css file to the html file, allowing the styling rules written in it to be implemented on the html document.

   - The second line allows for the use of icons from [**fontawesome.com**](https://fontawesome.com). These are free icons that you can access simply by creating an account.

   - The third line links the js file containing all the questions to the html file so that the questions can be displayed on the html page. The `defer` means that the js file will not be processed until the entire html page has been loaded.

   - The third line links the js file containing the main logic of the application to the html file. This allows the logic developed in the js file to be implemented on the html document. The `defer` performs the same function as mentioned above.

3. In the `<body>` section, write the following code:

   1. This button will be presented on the main landing page of the quiz application. It will be used to proceed to the instructions page.

   ```html
   <div class="start_btn"><button>Start Quiz</button></div>
   ```

   2. This code represents the Instruction box that is presented to the user after selecting the "Start Quiz" button. The rules are hard-coded into the html document because they are not dynamic, they rules stay the same per each instance of a quiz.

   ```html
   <!-- Instruction box wrapper -->
   <div class="info_box">
     <div class="info-title"><span>Some Rules of this Quiz</span></div>
     <div class="info-list">
       <div class="info">
         1. You will have only <span>15 seconds</span> per each question.
       </div>
       <div class="info">
         2. Once you select your answer, it can't be undone.
       </div>
       <div class="info">
         3. You can't select any option once time goes off.
       </div>
       <div class="info">
         4. You can't exit from the Quiz while you're playing.
       </div>
       <div class="info">
         5. You'll get points on the basis of your correct answers.
       </div>
     </div>
     <div class="buttons">
       <button class="quit">Exit Quiz</button>
       <button class="restart">Continue</button>
     </div>
   </div>
   ```

   3. The following code will create a template for the box holding each quiz question. Notice, some elements are hard coded into the html, such as the Title of the box, and the "Next Que" button, while other elements are empty `<div>` containers. These `<div>` containers will be dynamically populated using the javascript files, as the content changes for each question of the quiz.

   ```html
   <!-- Quiz Box -->
   <div class="quiz_box">
     <header>
       <div class="title">Demo Quiz App in JavaScript</div>
       <div class="timer">
         <div class="time_left_txt">Time Left</div>
         <div class="timer_sec">15</div>
       </div>
       <div class="time_line"></div>
     </header>
     <section>
       <div class="que_text">
         <!-- Insert questions from ./js/questions.js -->
       </div>
       <div class="option_list">
         <!-- Insert options to questions from ./js/questions.js -->
       </div>
     </section>

     <!-- footer of Quiz Box -->
     <footer>
       <div class="total_que">
         <!-- insert Question Count Number dynamically from JavaScript App logic -->
       </div>
       <button class="next_btn">Next Que</button>
     </footer>
   </div>
   ```

   4. The following code will create the final box shown at the end of the quiz. Again, notice some elements are hard-coded, which are elements that will not change, while the `<div>` that will show the user score is left empty as it will be dynamically filled by the **quizApp.js** file. Notice also the use of the `<i>` tag. This is the syntax for using icons from [**fontawesome.com**](https://fontawesome.com).

   ```html
   <!-- Result Box -->
   <div class="result_box">
     <div class="icon">
       <i class="fas fa-crown"></i>
     </div>
     <div class="complete_text">You've completed the Quiz!</div>
     <div class="score_text">
       <!-- insert dynamic user score as Result from JavaScript -->
     </div>
     <div class="buttons">
       <button class="restart">Replay Quiz</button>
       <button class="quit">Quit Quiz</button>
     </div>
   </div>
   ```

### JS

---

### questions.js

The **questions.js** file is essentially a place to store all the quiz questions that you would like the quiz application to present to the user.

Notice the following code that will be entered into your **questions.js** file:

```javascript
// creating an array of objects
// Each object consists of the following members: question number, questions, options, and answers
let questions = [
  {
    numb: 1,
    question: "What does HTML stand for?",
    answer: "Hyper Text Markup Language",
    options: [
      "Hyper Text Preprocessor",
      "Hyper Text Markup Language",
      "Hyper Text Multiple Language",
      "Hyper Tool Multi Language",
    ],
  },
  {
    numb: 2,
    question: "What does CSS stand for?",
    answer: "Cascading Style Sheet",
    options: [
      "Common Style Sheet",
      "Colorful Style Sheet",
      "Computer Style Sheet",
      "Cascading Style Sheet",
    ],
  },
  {
    numb: 3,
    question: "What does PHP stand for?",
    answer: "Hypertext Preprocessor",
    options: [
      "Hypertext Preprocessor",
      "Hypertext Programming",
      "Hypertext Preprogramming",
      "Hometext Preprocessor",
    ],
  },
  {
    numb: 4,
    question: "What does SQL stand for?",
    answer: "Structured Query Language",
    options: [
      "Stylish Question Language",
      "Stylesheet Query Language",
      "Statement Question Language",
      "Structured Query Language",
    ],
  },
  {
    numb: 5,
    question: "What does XML stand for?",
    answer: "eXtensible Markup Language",
    options: [
      "eXtensible Markup Language",
      "eXecutable Multiple Language",
      "eXTra Multi-Program Language",
      "eXamine Multiple Language",
    ],
  },
  // Duplicate the object declaration and initialization above for more questions
];
```

You may notice that this file contains only one element: an array of objects. Each object has 4 members:

- Question Number
- Question
- Answer
- Options

The above code illustrates the structure of 5 sample questions, but this file can be adjusted to meet your needs by simply following the same structure as shown above.

### quizApp.js

In order to achieve the functionality of the Quiz Application, enter the following code into your **quizApp.js** file:

1. The following code will select all necessary elements from the html document and store them in corresponding js variables to be accessed and utilized in this js file.

```javascript
//selecting all required elements from html document
const start_btn = document.querySelector(".start_btn button");
const info_box = document.querySelector(".info_box");
const exit_btn = info_box.querySelector(".buttons .quit");
const continue_btn = info_box.querySelector(".buttons .restart");
const quiz_box = document.querySelector(".quiz_box");
const result_box = document.querySelector(".result_box");
const restart_quiz = result_box.querySelector(".buttons .restart");
const quit_quiz = result_box.querySelector(".buttons .quit");
const option_list = document.querySelector(".option_list");
const time_line = document.querySelector("header .time_line");
const timeText = document.querySelector(".timer .time_left_txt");
const timeCount = document.querySelector(".timer .timer_sec");
const next_btn = document.querySelector("footer .next_btn");
const bottom_ques_counter = document.querySelector("footer .total_que");
```

2. The following code creates the functionality of many of the buttons in the Quiz application. You may notice that much of this functionality is achieved with the `.classList.add()` or `.classList.remove()` functions, which add/remove classnames to the selected variable element. This plays a role in showing/hiding respective `<div>` elements from the page, which will be discussed when going over the CSS file. Multiple functions are also called in the code below, which will be defined in the following steps.

```javascript
// if startQuiz button clicked
start_btn.addEventListener("click", (e) => {
  info_box.classList.add("activeInfo"); //show info box
});

// if exitQuiz button clicked
exit_btn.addEventListener("click", (e) => {
  info_box.classList.remove("activeInfo"); //hide info box
});

// Variables to control quiz operations
let timeValue = 15;
let que_count = 0;
let que_numb = 1;
let userScore = 0;
let counter;
let counterLine;
let widthValue = 0;

// if restartQuiz button clicked
restart_quiz.addEventListener("click", (e) => {
  quiz_box.classList.add("activeQuiz"); //show quiz box
  result_box.classList.remove("activeResult"); //hide result box
  timeValue = 15;
  que_count = 0;
  que_numb = 1;
  userScore = 0;
  widthValue = 0;
  showQuetions(que_count); //calling showQestions function
  queCounter(que_numb); //passing que_numb value to queCounter
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  startTimer(timeValue); //calling startTimer function
  startTimerLine(widthValue); //calling startTimerLine function
  timeText.textContent = "Time Left"; //change the text of timeText to Time Left
  next_btn.classList.remove("show"); //hide the next button
});

// if quitQuiz button clicked
quit_quiz.addEventListener("click", (e) => {
  window.location.reload(); //reload the current window
});

// if Next Question button is clicked
next_btn.addEventListener("click", (e) => {
  //check if it does not exceed max questions
  if (que_count < questions.length - 1) {
    que_count++; //increment the que_count value
    que_numb++; //increment the que_numb value
    showQuetions(que_count); //calling showQestions function
    queCounter(que_numb); //passing que_numb value to queCounter
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    startTimer(timeValue); //calling startTimer function
    startTimerLine(widthValue); //calling startTimerLine function
    timeText.textContent = "Time Left"; //change the timeText to Time Left
    next_btn.classList.remove("show"); //hide the next button
  } else {
    clearInterval(counter); //clear counter
    clearInterval(counterLine); //clear counterLine
    showResult(); //calling showResult function
  }
});
```

3. The following code is the definition for the `showQuestions()` function. This function in essence dynamically fills the two empty `<div>` containers for the Question Text and Option list in the **index.html** file for each question defined in the **questions.js** file.

```javascript
// getting questions and options from array
// If you have lesser or more number of options you need to change this code
function showQuetions(index) {
  const que_text = document.querySelector(".que_text");

  //creating a new span and div tag for question and option and passing the value using array index
  // self exercise: re-write the following using backtick syntax for string in JS instead of concatenation operator
  let que_tag =
    "<span>" +
    questions[index].numb +
    ". " +
    questions[index].question +
    "</span>";
  let option_tag =
    '<div class="option"><span>' +
    questions[index].options[0] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[1] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[2] +
    "</span></div>" +
    '<div class="option"><span>' +
    questions[index].options[3] +
    "</span></div>";
  que_text.innerHTML = que_tag; //adding new (child) span tag inside que_tag
  option_list.innerHTML = option_tag; //adding new (child) div tag inside option_tag

  const option = option_list.querySelectorAll(".option");

  // set onclick attribute to all available options
  for (i = 0; i < option.length; i++) {
    option[i].setAttribute("onclick", "optionSelected(this)");
  }
}
```

4. This code is the function defintion for `optionSelected()`. This function creates the functionality of the multiple choice portion of the quiz. It covers all three scenarios:

   - The user answered correctly.
   - The user answered incorrectly.
   - The user ran out of time.

   This function also aids in the visual display of correct/incorrect answer choices by using the `.classList.add()` function, as well as the `<i>` tags for the icons from [**fontawesome.com**](https://fontawesome.com). More discussion on this will be had when going over the **styles.css** file.

```javascript
// create new div tags for right or wrong tick icons
let tickIconTag = '<div class="icon tick"><i class="fas fa-check"></i></div>';
let crossIconTag = '<div class="icon cross"><i class="fas fa-times"></i></div>';

//if user clicked on option
function optionSelected(answer) {
  clearInterval(counter); //clear counter
  clearInterval(counterLine); //clear counterLine
  let userAns = answer.textContent; //getting user selected option
  let correcAns = questions[que_count].answer; //getting correct answer from array
  const allOptions = option_list.children.length; //getting all option items

  //if user selected option is equal to array's correct answer
  if (userAns == correcAns) {
    userScore += 1; //update total score value increment by 1
    answer.classList.add("correct"); //add green color to correct selected option
    answer.insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to correct selected option
    console.log("Correct Answer");
    console.log("Your correct answers = " + userScore);
  } else {
    answer.classList.add("incorrect"); //add red color to correct selected option
    answer.insertAdjacentHTML("beforeend", crossIconTag); //add cross icon to correct selected option
    console.log("Wrong Answer");

    for (i = 0; i < allOptions; i++) {
      if (option_list.children[i].textContent == correcAns) {
        //if there is an option which is matched to an array answer
        option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
        option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
        console.log("Auto selected correct answer.");
      }
    }
  }
  for (i = 0; i < allOptions; i++) {
    option_list.children[i].classList.add("disabled"); //once user select an option, disable all options
  }
  next_btn.classList.add("show"); //show the next button if user selected any option
}
```

5. This is the definition for the `showResult()` function. It contains logic that will dynamically fill the empty `<div>` container for the Score Text in the **index.html** file with a corresponding sentence based on the user's score.

```javascript
// display for result box based on user performance
function showResult() {
  info_box.classList.remove("activeInfo"); //hide info box
  quiz_box.classList.remove("activeQuiz"); //hide quiz box
  result_box.classList.add("activeResult"); //show result box
  const scoreText = result_box.querySelector(".score_text");
  if (userScore > 3) {
    // if user scored more than 3
    //create a new span tag and pass the user score number and total question number
    let scoreTag =
      "<span>and congrats! , You got <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag; //add new span tag inside score_Text
  } else if (userScore > 1) {
    // if user scored more than 1
    let scoreTag =
      "<span>and nice , You got <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag;
  } else {
    // if user scored less than 1
    let scoreTag =
      "<span>and sorry , You got only <p>" +
      userScore +
      "</p> out of <p>" +
      questions.length +
      "</p></span>";
    scoreText.innerHTML = scoreTag;
  }
}
```

6. The following is the defintion for the `startTimer()` and `startTimerLine()` functions. These take care of the timer functionality of the Quiz application in both numeric and progress bar formats.

```javascript
// control the timer and actions associated to it
function startTimer(time) {
  counter = setInterval(timer, 1000);
  function timer() {
    timeCount.textContent = time; //change the value of timeCount with time value
    time--; //decrement the time value
    if (time < 9) {
      //if timer is less than 9
      let addZero = timeCount.textContent;
      timeCount.textContent = "0" + addZero; //add a 0 before time value
    }
    if (time < 0) {
      //if timer is less than 0
      clearInterval(counter); //clear counter
      timeText.textContent = "Time Off"; //change the time text to time off
      const allOptions = option_list.children.length; //get all option items
      let correcAns = questions[que_count].answer; //get correct answer from array
      for (i = 0; i < allOptions; i++) {
        if (option_list.children[i].textContent == correcAns) {
          //if there is an option which is matched to an array answer
          option_list.children[i].setAttribute("class", "option correct"); //add green color to matched option
          option_list.children[i].insertAdjacentHTML("beforeend", tickIconTag); //add tick icon to matched option
          console.log("Time Off: Auto selected correct answer.");
        }
      }
      for (i = 0; i < allOptions; i++) {
        option_list.children[i].classList.add("disabled"); //once user select an option then disabled all options
      }
      next_btn.classList.add("show"); //show the next button if user selected any option
    }
  }
}

// Shows a progress bar mirroring timer value left
function startTimerLine(time) {
  counterLine = setInterval(timer, 29);
  function timer() {
    time += 1; //upgrading time value with 1
    time_line.style.width = time + "px"; //increasing width of time_line with px by time value
    if (time > 549) {
      //if time value is greater than 549
      clearInterval(counterLine); //clear counterLine
    }
  }
}
```

7. This is the function definition for `queCounter()`. This function handles the functionality of the question counter, that lets the user know what question they are on in the quiz.

```javascript
function queCounter(index) {
  //creating a new span tag and passing the question number and total question
  let totalQueCounTag =
    "<span><p>" +
    index +
    "</p> of <p>" +
    questions.length +
    "</p> Questions</span>";
  bottom_ques_counter.innerHTML = totalQueCounTag; //adding new span tag inside bottom_ques_counter
}
```

After entering all the above code into your **quizApp.js** file, the main logic of your Quiz application is complete. All that is left is styling, which will be covered in the next section.

### CSS

---

### style.css

The **style.css** file will handle all of the styling for your Quiz application. Enter the following code in the **style.css** file to achieve a polished look for your Quiz application.

1. This line of code imports the "Poppins" family of fonts from Google fonts.

```css
/* importing google fonts */
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap");
```

2. The following are basic styling rules for the entire page. The `*` selector covers the entire HTML document, and the styling rules listed are for removing all default styling that the browser has. The `font-family` is the one imported from Google Fonts, and is applied to the entire HTML document. The `body` selector sets the background color for the page, and the `::selection` selector sets the styling rules for selected text anywhere on the page.

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

body {
  background: #a020f0;
}

::selection {
  color: #fff;
  background: #a020f0;
}
```

3. The following 2 selectors serve the following purposes:
   - The first selector contains basic styling for the 4 major components of the quiz application:
     - The "Start Quiz" Button (`.start_btn`)
     - The Quiz Rules (`.info_box`)
     - The Quiz Questions (`.quiz_box`)
     - The Quiz Score Box (`.result_box`)
   - The second selector contains the sytling rules that allow the buttons to display the proper `<div>` container at the appropriate time. When the appropriate "active" class name is added to the corresponding `<div>` container, the `opacity` is set to `1`. This is what allows the `<div>` element to be displayed, because at the start, the `opacity` for the three elements listed in the second selector is set to `0`, hiding it from the view of the user. The buttons toggle between the `opacity` values of `0` and `1` to hide/display the appropriate elements at the appropriate times.

```css
.start_btn,
.info_box,
.quiz_box,
.result_box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.info_box.activeInfo,
.quiz_box.activeQuiz,
.result_box.activeResult {
  opacity: 1;
  z-index: 5;
  pointer-events: auto;
  transform: translate(-50%, -50%) scale(1);
}
```

4. The following is styling for the "Start Quiz" button that displays when the Quiz application is launched.

```css
.start_btn button {
  font-size: 25px;
  font-weight: 500;
  color: #a020f0;
  padding: 15px 30px;
  outline: none;
  border: none;
  border-radius: 5px;
  background: #fff;
  cursor: pointer;
}
```

5. Next is the styling for the `.info_box` element and corresponding elements, which holds the Quiz Rules. You can see here the `opacity` is set to `0`. You may also notice that CSS transitions are being used to lend to the polished look of the application.

```css
.info_box {
  width: 540px;
  background: #fff;
  border-radius: 5px;
  transform: translate(-50%, -50%) scale(0.9);
  opacity: 0;
  pointer-events: none;
  transition: all 0.3s ease;
}

.info_box .info-title {
  height: 60px;
  width: 100%;
  border-bottom: 1px solid lightgrey;
  display: flex;
  align-items: center;
  padding: 0 30px;
  border-radius: 5px 5px 0 0;
  font-size: 20px;
  font-weight: 600;
}

.info_box .info-list {
  padding: 15px 30px;
}

.info_box .info-list .info {
  margin: 5px 0;
  font-size: 17px;
}

.info_box .info-list .info span {
  font-weight: 600;
  color: #a020f0;
}
.info_box .buttons {
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding: 0 30px;
  border-top: 1px solid lightgrey;
}

.info_box .buttons button {
  margin: 0 5px;
  height: 40px;
  width: 100px;
  font-size: 16px;
  font-weight: 500;
  cursor: pointer;
  border: none;
  outline: none;
  border-radius: 5px;
  border: 1px solid #a020f0;
  transition: all 0.3s ease;
}
```

5. The following is the styling for the `.quiz_box` element and corresponding elements, which is the container for the quiz questions and options, and holds the timer (text view and progress bar view).

```css
.quiz_box {
  width: 550px;
  background: #fff;
  border-radius: 5px;
  transform: translate(-50%, -50%) scale(0.9);
  opacity: 0;
  pointer-events: none;
  transition: all 0.3s ease;
}

.quiz_box header {
  position: relative;
  z-index: 2;
  height: 70px;
  padding: 0 30px;
  background: #fff;
  border-radius: 5px 5px 0 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  box-shadow: 0px 3px 5px 1px rgba(0, 0, 0, 0.1);
}

.quiz_box header .title {
  font-size: 20px;
  font-weight: 600;
}

.quiz_box header .timer {
  color: #682a8f;
  background: #cce5ff;
  border: 1px solid #b8daff;
  height: 45px;
  padding: 0 8px;
  border-radius: 5px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 145px;
}

.quiz_box header .timer .time_left_txt {
  font-weight: 400;
  font-size: 17px;
  user-select: none;
}

.quiz_box header .timer .timer_sec {
  font-size: 18px;
  font-weight: 500;
  height: 30px;
  width: 45px;
  color: #fff;
  border-radius: 5px;
  line-height: 30px;
  text-align: center;
  background: #343a40;
  border: 1px solid #343a40;
  user-select: none;
}

.quiz_box header .time_line {
  position: absolute;
  bottom: 0px;
  left: 0px;
  height: 3px;
  background: #a020f0;
}
```

6. Next are the styling rules for the `<section>` element, which acts as a container for the individual Quiz Questions and Options. This is contained within the `.quiz_box` element. You may note the different styling rules for `.option.correct`, `.option.incorrect` and `.option.disabled`, which aids in the visual display of correct and incorrect option choices, noted with different coloring and icons.

```css
section {
  padding: 25px 30px 20px 30px;
  background: #fff;
}

section .que_text {
  font-size: 25px;
  font-weight: 600;
}

section .option_list {
  padding: 20px 0px;
  display: block;
}

section .option_list .option {
  background: aliceblue;
  border: 1px solid #84c5fe;
  border-radius: 5px;
  padding: 8px 15px;
  font-size: 17px;
  margin-bottom: 15px;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

section .option_list .option:last-child {
  margin-bottom: 0px;
}

section .option_list .option:hover {
  color: #601391;
  background: #cce5ff;
  border: 1px solid #b8daff;
}

section .option_list .option.correct {
  color: #155724;
  background: #d4edda;
  border: 1px solid #c3e6cb;
}

section .option_list .option.incorrect {
  color: #721c24;
  background: #f8d7da;
  border: 1px solid #f5c6cb;
}

section .option_list .option.disabled {
  pointer-events: none;
}

section .option_list .option .icon {
  height: 26px;
  width: 26px;
  border: 2px solid transparent;
  border-radius: 50%;
  text-align: center;
  font-size: 13px;
  pointer-events: none;
  transition: all 0.3s ease;
  line-height: 24px;
}
.option_list .option .icon.tick {
  color: #23903c;
  border-color: #23903c;
  background: #d4edda;
}

.option_list .option .icon.cross {
  color: #a42834;
  background: #f8d7da;
  border-color: #a42834;
}
```

7. These are the styling rules for the `<footer>` of the Quiz Box, and corresponding elements. These are also contained in the `.quiz_box` element. The footer holds the question counter for the quiz and the "Next Que" Button.

```css
footer {
  height: 60px;
  padding: 0 30px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-top: 1px solid lightgrey;
}

footer .total_que span {
  display: flex;
  user-select: none;
}

footer .total_que span p {
  font-weight: 500;
  padding: 0 5px;
}

footer .total_que span p:first-child {
  padding-left: 0px;
}

footer button {
  height: 40px;
  padding: 0 13px;
  font-size: 18px;
  font-weight: 400;
  cursor: pointer;
  border: none;
  outline: none;
  color: #fff;
  border-radius: 5px;
  background: #a020f0;
  border: 1px solid #a020f0;
  line-height: 10px;
  opacity: 0;
  pointer-events: none;
  transform: scale(0.95);
  transition: all 0.3s ease;
}

footer button:hover {
  background: #7803c0;
}

footer button.show {
  opacity: 1;
  pointer-events: auto;
  transform: scale(1);
}
```

8. Last are the styling rules for the `.result_box` and corresponding elements. This container is the one that displays the user's score and the two buttons to "Replay Quiz" and "Quit Quiz".

```css
.result_box {
  background: #fff;
  border-radius: 5px;
  display: flex;
  padding: 25px 30px;
  width: 450px;
  align-items: center;
  flex-direction: column;
  justify-content: center;
  transform: translate(-50%, -50%) scale(0.9);
  opacity: 0;
  pointer-events: none;
  transition: all 0.3s ease;
}

.result_box .icon {
  font-size: 100px;
  color: #a020f0;
  margin-bottom: 10px;
}

.result_box .complete_text {
  font-size: 20px;
  font-weight: 500;
}

.result_box .score_text span {
  display: flex;
  margin: 10px 0;
  font-size: 18px;
  font-weight: 500;
}

.result_box .score_text span p {
  padding: 0 4px;
  font-weight: 600;
}

.result_box .buttons {
  display: flex;
  margin: 20px 0;
}

.result_box .buttons button {
  margin: 0 10px;
  height: 45px;
  padding: 0 20px;
  font-size: 18px;
  font-weight: 500;
  cursor: pointer;
  border: none;
  outline: none;
  border-radius: 5px;
  border: 1px solid #a020f0;
  transition: all 0.3s ease;
}

.buttons button.restart {
  color: #fff;
  background: #a020f0;
}

.buttons button.restart:hover {
  background: #8304d1;
}

.buttons button.quit {
  color: #a020f0;
  background: #fff;
}

.buttons button.quit:hover {
  color: #fff;
  background: #8604d6;
}
```

## Conclusion

After implementing all the above code in the above sections into your project, you will have a fully functional Quiz application that is the solution for the Problem Statement and has all the Functional Features listed at the beginning of this document. Happy Coding!
