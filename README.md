# Pratical Python Milestone Project

## Riddle-Me-This (Brief)

A web application game that asks players to guess the answer to geogrpahy based questions (Capital cities of the world).

The player is presented with a selection of regions/continents to select from and is then presented with multiple choice questions. Players enter their answer into a textarea and submit their answer using a form.

After each answer is submitted, the player is redirected to the next question.

If a player guesses incorrectly, their incorrect guess is stored and printed below the next question and their score remains the same.
If a player guesses correctly, their score implements by 1 point and the next question is displayed.

Their current score will be displayed throughout the quiz.

After answering 10 questions, the players final score will be displayed, along with a table showing their correct and incorrect answers.

A leaderboard showing the top 10 players for each quiz will also be available (currently some issues with this functionality, see below)

Full project is deployed on Heroku at this <a href="https://world-cities-quiz.herokuapp.com/" target="_blank" >location</a>.

**_Method of Deployment:_**
1. New Heroku Python App created, entitled "world-cities-quiz"
2. Launched Heroku in the C9 environment
3. Git repo was already initiated, so ran **```git remote add heroku https://git.heroku.com/world-cities-quiz.git```** to allow a push to the Heroku server
4. To prevent a "push fail", the requirements.txt was updated using the following command **```sudo pip3 freeze --local >requirements.txt```** to keep track of dependancies
5. A Procfile was created using the following code: **```echo web: python run.py > Procfile```** to inform Heroku which file to run for initiating the app
6. To esnure that Web Processes are running the following command line was run in C9: **```heroku ps:scale web=1```**
7. Config Vars set as follows: **IP=0.0.0.0 and PORT=5000**
8. Lastly, dynos were restarted in Heroku app
9. Code added, committed and pushed to both GitHub and Heroku
10. App launched successfully

## Technologies used

Technologies used in this project include:

* Bootstrap: Bootstrap was used for a basic HTML template.
* HTML5/CSS: Used for the layout and styling of the application.
* Python 3.4.3: The back end functionality of the application was written entirely in python 3.0.
  Was originally running on Python 2, following code was executed to upgrade:
  ~~~~
  jagger81:~/workspace (master) $ sudo mv /usr/bin/python /usr/bin/python2
  jagger81:~/workspace (master) $ sudo ln -s /usr/bin/python3 /usr/bin/python
  jagger81:~/workspace (master) $ python --version
  Python 3.4.3
  ~~~~
* Flask Microframework: Flask was used to extend pythons functionality to the frond end (uses Jinja2 as template engine).
* Balsamiq: Used to create the below wireframes.
* Cloud9 IDE used as development environment workspace

## Bootstrap template used

As the main focus of this project is Python and the use of the Flask Framework, it was felt that there was no need to start the HTML & CSS from scratch
and so instead appropriate template files were imported to Cloud9 using the 'wget' command.

Folders that were not necessary were then deleted.

The template used is called Freelancer and is downloadable from https://startbootstrap.com/template-overviews/freelancer/

## Image Credits

All 6 Continent Images used were designed by Vexels.  www.vexels.com

## Mockups / Wireframes

The following are the initial mockups of each page/section - the final prodcut may vary slightly depending on functionaility:

### Sample; Index Page (Section 1 - Masthead):

![index1](https://user-images.githubusercontent.com/28737216/46905476-4761de00-ceec-11e8-9697-a98ed4ba3694.PNG)

### Sample; Index Page (Section 2 - How To Play):

![index2](https://user-images.githubusercontent.com/28737216/46905489-6e201480-ceec-11e8-97c6-798edd54d395.PNG)

### Sample; Index Page (Section 3 - Quiz Selection):

![index3](https://user-images.githubusercontent.com/28737216/46905492-7710e600-ceec-11e8-990e-c86b83ab2834.PNG)

### Sample; Index Page (Section 4 - Contact Form):

![index4](https://user-images.githubusercontent.com/28737216/46905575-cc012c00-ceed-11e8-92ac-30050322ac49.PNG)

## UX

Users knowledge of world capital cities will be tested, with each section being scored out of 10 and a chance to claim their place on the relevant leaderboard.

Upon visiting the site, the user will first be presented with the opening page (index.html) with options to see "How To Play" or "Select a Quiz".  Selecting "How To Play", will bring them to the following instructions section:

![howtoplay](https://user-images.githubusercontent.com/28737216/46914999-7a17df00-cf9d-11e8-82c2-e63205a09aa4.PNG)
(provisional instructions - due to change as project development progresses)

Upon moving to the Quiz Selection area, they will be presented with the following options, per continent:

![quizselect](https://user-images.githubusercontent.com/28737216/46915030-d3800e00-cf9d-11e8-8deb-0a1c2231ab86.PNG)

The user then selects the button for the quiz of their choice, and this will open the following modal which allows them to enter their Username:

![username](https://user-images.githubusercontent.com/28737216/46915087-6b7df780-cf9e-11e8-9e5e-6ce690a39362.PNG)

"Close" will simply close the modal and return them to the Quiz Selection, whereas "Start Quiz" will redircet them to the appropriate Quiz Page based on their original choice:

![quizpage](https://user-images.githubusercontent.com/28737216/46915116-b7c93780-cf9e-11e8-93dc-3c923e63e0d5.PNG)
(example of Africa Quiz Page - with Welcome Note on the left, and questions on the right {for lager screens})

### Flowchart of processes

![flowchart](https://user-images.githubusercontent.com/28737216/47255466-88686e00-d469-11e8-9d4b-5ca332dfc775.PNG)

### Functions requiring additional work before being fully implemented

There were persistent problems displaying the Leaderboard data correctly (e.g. "africa_scoreboard.json"), due the data file not being read correctly. Although the file extension is .json the data itself is not in a JSON format.  With some more time, I am confident that this I could find a solution to this issue.

The code for adding the data to the file, and sorting it in descending order (to the top 10 only) is working fine:

Lines 84-89 of run.py
```python
def get_africa_leaderboard():  # used to get the Leaderboard data from 'africa_leaderboard.json'
    africa_leaderboard = []
    with open("data/africa/africa_scoreboard.json", "r") as africa_leaderboard:
        africa_leaderboard = json.load(africa_leaderboard)
        #africa_leaderboard = [row for row in africa_leaderboard]
        return africa_leaderboard[-10:]
```

Line 190 of run.py

```python
leaderboard = sorted(get_africa_leaderboard(),reverse=True)
```

Ideally, the storing and retrieving of certain data (e.g. Username, User Answer) would be achieved by using `Sessions`, however this was not covered in the learning material.

Lastly, when rendering the `Username`and `Score`variables on the results/end of game page, the data displays with square brackets around it:

![username_score_display](https://user-images.githubusercontent.com/28737216/52918042-7351fd80-32ea-11e9-9c62-d603f5fd2c59.png)

## Testing

Mainly manual testing used throughout - for routing and checking if data is properly rendered in the correct template and format, 
"test_run.py" was used, whereby on satisfactory completion, the clean functional code would then be transferred to the "run.py" file

Pep 8 was used to assist with cleaning the data - indentation, whitespaces, non-spaces, 2 lines expected

http://pep8online.com/
