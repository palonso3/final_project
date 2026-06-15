'''
Recipe & Shopping List Planner

Video Demo: 

Description:

What is this project?

This project is a Recipe and Meal Planner that runs directly in the terminal. The idea is simple: instead of writing your recipes on paper or scrolling through your phone trying to remember what ingredients you need, you can store everything in one place and the program helps you manage it. You can add recipes, look them up by ingredient, see everything you have saved, remove recipes you no longer want, and even generate a shopping list for the meals you are planning to cook.

We built this as our final project for the Introduction to Programming with Python course at Hult International Business School, section SUONE2026. The two of us are Natalia Loret de Mola and Pablo Alonso.


How did we come up with this idea?

We wanted to build something practical, something we would actually use in real life. Both of us cook at home and we have both had the experience of opening the fridge, not knowing what to make, and then going to the store and forgetting half the things we needed. A simple recipe manager felt like the right scope for this project. It is not too complicated, but it uses everything we learned in the course: functions, loops, conditionals, file handling, and testing.


What files are in this project?

There are four files that matter.

project.py is the main file. It contains all the logic of the program. When you run it, a menu appears and you can choose what you want to do. Everything happens here.

test_project.py contains the tests for the project. We used pytest to write four tests, one for each of the main functions. The tests check that adding a recipe works correctly, that searching by ingredient returns the right results, that the shopping list combines ingredients without repeating them, and that removing a recipe actually deletes it from the file.

recipes.csv is where all the recipe data is stored. The program creates this file automatically the first time you add a recipe. Each row has two columns: the name of the recipe and its ingredients. The ingredients are stored separated by semicolons so that the CSV format does not get confused by commas inside the ingredient list.

requirements.txt lists any external libraries the project needs. In our case it is empty because we only used Python built-in libraries: csv and os. No extra installations are needed.


How does the program work?

When you run python project.py in the terminal, you see a menu with six options. You type a number and press enter, and the program takes you through that option step by step. The six options are: add a recipe, search recipes by ingredient, generate a shopping list, view all recipes, remove a recipe, and exit.


What does each function do?

main() runs the menu loop. It keeps showing the menu and asking for input until the user chooses to exit. It connects all the other functions together based on what the user picks.

add_recipe(name, ingredients) takes the name of a recipe and a string of ingredients separated by commas. It opens the CSV file, or creates it if it does not exist yet, and saves the recipe as a new row. The ingredients get converted from comma-separated to semicolon-separated before saving so the CSV format stays clean.

search_by_ingredient(ingredient) reads through all the saved recipes and returns a list of recipe names that contain the ingredient the user typed. The comparison is case-insensitive so it does not matter if you type Eggs or eggs, it will still find the right recipes.

generate_shopping_list(recipe_names) takes one or more recipe names, looks them up in the CSV file, and combines all their ingredients into a single list. If the same ingredient appears in more than one recipe, it only gets added to the list once. This way you do not end up with eggs listed three times when you are planning multiple meals.

view_recipes() reads all the saved recipes and prints them out in a readable format, showing the recipe name followed by its ingredients. If there are no recipes saved yet, it tells you that.

remove_recipe(name) looks for a recipe by name, removes it from the list, and rewrites the CSV file without it. It returns True if the recipe was found and deleted, and False if no recipe with that name existed. The name comparison is also case-insensitive so capitalization does not cause problems.


What design choices did we make and why?

One decision we had to make early on was how to store the ingredients inside the CSV file. The obvious choice would have been to use commas, but since CSV files already use commas to separate columns, that would have broken the file format. For example, a recipe with flour, eggs, milk would look like three separate columns instead of one. We decided to use semicolons as the separator inside the ingredients column and then split them back into a list whenever we needed to read them. This kept the file simple and easy to read.

Another choice was to make all text comparisons case-insensitive. Early on we noticed that if you saved a recipe called Pancakes and then tried to remove pancakes, the program would say it could not find it. That felt frustrating and unnecessary, so we added .strip().lower() to both sides of every comparison. This made the program feel much more natural to use.

We also decided to hardcode the fieldnames in the remove_recipe function instead of reading them from the file. The reason is that if the CSV file is empty or malformed, csv.DictReader returns None for fieldnames and the program crashes. Since we always know the column names are name and ingredients, it is safer and simpler to just write them directly.


How to run the project

Make sure you have Python installed. Download or clone the repository. In your terminal, navigate to the project folder. Run python project.py to start the program. Run python -m pytest test_project.py -v to run the tests. No additional libraries need to be installed.


Final Project, Introduction to Programming with Python, SUONE2026
Natalia Loret de Mola (natalialoret) and Pablo Alonso (palonso3)
'''
