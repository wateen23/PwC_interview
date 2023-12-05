# Documentation
## User Guide
Welcome to Wateen's Quiz. In order to have a pleasant experience using my programme, please refer to the following step by step instructions:

1. Clone repository
    `git clone [LINK]`
2. navigate into the directory with this command:
    `cd [FileName]`
3. copy and paste the following snippet into the terminal:
    `streamlit run pwc_mcq_app.py`

Now a new tab in your browser appears with my application. In order to use it without facing any errors, there are some rules you need to follow:
1. If you want to change the number(Min: 1, Max: 5) of questions, the Quiz topic field has to be empty
2. By entering any topic and clicking enter on your keyboard, a certain number of questions will appear.
3. After answering the questions, click Submit and the results of the quiz will appear.


### Have fun!


## Developer Documentation

The project contains two python classes: API_key.py and pwc_mcq_app.py

The former only contains the needed API key and can be ignored from this point forth.

The file pwc_mcq_app.py contains the complete logic of the application.

### Class QuizQuestion
This class is used to save the information of a complete question. It is used to quickly assign and retrieve question data.


### Method generate_question(prompt, number)

This method is used to retrieve the questions from our API.
It takes prompt and number as input parameters.

Prompt represents the quiz topic and number the amount of questions.
The method shows inconsistent behaviour when the inputted number is larger than 5, on account of the character limit of the response by OpenAI.

The response of the API is a large string with all the questions and answers together. First the string is split into the questions. Then a for loop runs through each question block and parses its information into an object of the class QuizQuestion.
It then returns an array of type QuizQuestion.

As for the input variables for the question template, I used the topic and number prompts so the user can identify the desired topic and number of questions.

@st.cache_data is used to cache data and not trigger a rerun of the method whenever the user interacts with the application.

### Method main
This is the main method which is run when the file is run.
First general site information is set.
Then two input fields are created, one for the topic and the other for the number of questions.

In this method the method generate_question is called and its return array saved locally. With this array, Each question is displayed in the application and with it its possible answers(radioButton 0 as default)
This is done in a for loop and a reference to the radio buttons is saved in user_answers.

A button (Submit) appears and is clickable. When clicked, the results of the quiz are calculated and shown in the application
