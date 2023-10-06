<template>
    <div class="p-4 sm:p-8"> <!-- Add padding to the entire container, increase padding on small screens (sm) -->
      <div v-if="currentQuestionIndex < questions.length" class="text-center">
        <h1 class="text-3xl sm:text-4xl font-semibold mb-4">HTML Quiz</h1> <!-- Increase font size on small screens -->
        <p class="mb-2">Question {{ currentQuestionIndex + 1 }}:</p>
        <p class="text-lg sm:text-xl mb-4">{{ questions[currentQuestionIndex].question }}</p> <!-- Increase font size on small screens -->
        <ul>
            <li
              v-for="(option, index) in questions[currentQuestionIndex].options"
              :key="index"
              class="mb-2"
            >
              <input
                type="radio"
                :id="'option' + index"
                :value="option"
                v-model="selectedAnswer"
                class="mr-2"
              />
              <label :for="'option' + index" class="text-base" :class="{'bg-green-500 text-white font-semibold p-2 rounded': selectedAnswer === option}">
                {{ option }}
              </label>
            </li>
          </ul>
        <div class="space-x-4 mt-4"> <!-- Add space between buttons -->
          <button @click="goBack" :disabled="currentQuestionIndex === 0" class="bg-blue-500 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded">
            Back
          </button>
          <button @click="saveAnswer" class="bg-green-500 hover:bg-green-700 text-white font-semibold py-2 px-4 rounded">
            Save Answer
          </button>
          <button @click="checkAnswer" class="bg-blue-500 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded">
            Next
          </button>
        </div>
      </div>
      <div v-else class="text-left"> <!-- Left-align content -->
        <h1 class="text-3xl sm:text-4xl font-semibold mb-4">Quiz Completed!</h1> <!-- Increase font size on small screens -->
        <p class="mb-2">Your Score: {{ score }} / {{ questions.length }}</p>
      </div>
    </div>
  </template>
  

  

<script>
export default {
  data() {
    return {
      currentQuestionIndex: 0,
      selectedAnswer: null,
      score: 0,
      questions: [
        {
          question: "What does HTML stand for?",
          options: [
            " Home Tool Markup Language",
            " Hyperlinks and Text Markup Language",
            "Hyper Text Markup Language",
          ],
          correctAnswer: "Hyper Text Markup Language",
        },
        {
          question: "Choose the correct HTML element for the largest heading?",
          options: ["<h1>", "<h6>", "<head>"],
          correctAnswer: "<h1>",
        },
        {
          question:
            "What is the correct HTML element for inserting a line break?",
          options: ["<lb>", "<br>", "<break>"],
          correctAnswer: "<br>",
        },
        {
          question: "Choose the correct HTML element to define important text?",
          options: ["<important>", "<strong>", "<b>"],
          correctAnswer: "<strong>",
        },
        {
          question: "What is the correct HTML for creating a hyperlink??",
          options: [
            '<a name="http://www.w3schools.com">W3Schools.com</a>',
            '<a href="http://www.w3schools.com">W3Schools</a>',
            '<a url="http://www.w3schools.com">W3Schools.com</a>',
          ],
          correctAnswer: '<a href="http://www.w3schools.com">W3Schools</a>',
        },
        {
          question: "Which character is used to indicate an end tag?",
          options: ["^", "/", "."],
          correctAnswer: "/",
        },
        {
          question: "How can you open a link in a new tab/browser window??",
          options: [
            '<a href="https://www.WordPress.com" target="_blank">WordPress</a>',
            '<a href="https://www.WordPress.com" target="new">WordPress</a>',
            '<a href="https://www.WordPress.com" target="new_tab">WordPress</a>',
          ],
          correctAnswer:
            '<a href="https://www.WordPress.com" target="_blank">WordPress</a>',
        },
        {
          question: "How can you make a numbered list??",
          options: ["<dl>", "<ol>", "<ul>"],
          correctAnswer: "<ol>",
        },
        {
          question:
            "What is the correct way to comment out multiple lines of HTML code?",
          options: [
            "<!-- This is a comment -->",
            "/* This is a comment */",
            "// This is a comment",
          ],
          correctAnswer: "<!-- This is a comment -->",
        },
        {
          question:
            "Which HTML attribute is used to specify the URL of the image to be displayed in an <img> element?",
          options: ["src", "alt", "href"],
          correctAnswer: "src",
        },
        {
          question:
            "Which HTML tag is used to create a hyperlink to send an email?",
          options: ["<email>", '<a href="mailto:">', "<mail>"],
          correctAnswer: '<a href="mailto:">',
        },
        {
          question: "What is the purpose of the HTML <nav> element?",
          options: [
            "To define navigation links",
            "To create a new webpage",
            "To add a video",
          ],
          correctAnswer: "To define navigation links",
        },
        {
          question: "Which HTML tag is used to create a table?",
          options: ["<table>", "<tab>", "<tr>"],
          correctAnswer: "<table>",
        },
        {
          question: "What is the purpose of the HTML <form> element?",
          options: [
            "To display images",
            "To create hyperlinks",
            "To create a web form for user input",
          ],
          correctAnswer: "To create a web form for user input",
        },
        {
          question:
            "Which attribute is used to specify the alternative text for an image?",
          options: ["src", "alt", "title"],
          correctAnswer: "alt",
        },
        {
          question: "Which HTML element is used to create a button?",
          options: ['<input type="button">', "<button>", "<submit>"],
          correctAnswer: "<button>",
        },
        {
          question: "Which HTML element is used to create a dropdown menu?",
          options: ["<select>", '<input type="dropdown">', "<menu>"],
          correctAnswer: "<select>",
        },
        {
          question: "Which HTML tag is used to define a video element?",
          options: ["<media>", "<video>", "<movie>"],
          correctAnswer: "<video>",
        },
        {
          question:
            "Which HTML element is used to define the structure of an HTML document?",
          options: ["<html>", "<body>", "<structure>"],
          correctAnswer: "<html>",
        },
        {
          question:
            "Which HTML attribute is used to specify a tooltip for an element when the mouse pointer hovers over it?",
          options: ["<hover>", "tooltip", "title"],
          correctAnswer: "title",
        },
      ],
    };
  },
  methods: {
    checkAnswer() {
      if (
        this.selectedAnswer ===
        this.questions[this.currentQuestionIndex].correctAnswer
      ) {
        this.score++;
      }
      this.selectedAnswer = null;
      this.currentQuestionIndex++;
    },
    goBack() {
      if (this.currentQuestionIndex > 0) {
        this.currentQuestionIndex--;
      }
    },
    saveAnswer() {
      this.userAnswers[this.currentQuestionIndex] = this.selectedAnswer;
    },
  },
};
</script>
