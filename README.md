# Grade-Calculator

```
#CIS-443-01-4248
#Program 2
#10/21/24
#this program accepts a number of students. It then asks for each student's name, amount of grades, and each grade.
#It then returns an average grade for each student along with their name and a bar chart to visualize the grades

import matplotlib as plt
import seaborn as sns
import numpy as np

#Gathers the data of the student's names and grades
def input_scoring():
    students = {}
    num_students = int(input("Enter the number of students: "))
    
    for _ in range(num_students):
        name = input("Enter the student's name: ")
        num_grades = int(input(f"How many grades for {name}? "))
        grades = []
        
        for i in range(num_grades):
            grade = float(input(f"Enter grade {i+1} for {name}: "))
            grades.append(grade)
        
        students[name] = grades
    return students

#Translates the average percentage grades into letter grades
def summarize_grades(students):
    letter_grades = []
    
    for name, grades in students.items():
        mean_score = np.mean(grades)
        
        if mean_score >= 90:
            letter = 'A'
        elif mean_score >= 80:
            letter = 'B'
        elif mean_score >= 70:
            letter = 'C'
        elif mean_score >= 60:
            letter = 'D'
        else:
            letter = 'F'
        
        letter_grades.append(letter)
        print(f"{name}'s average score is {mean_score:.2f} which corresponds to a {letter} grade.")

    #Gathers a count of every grade 
    grade_counts = {grade: letter_grades.count(grade) for grade in ['A', 'B', 'C', 'D', 'F']}
    sns.color_palette("flare")
    #not sure if I was able to get the color palette to work. It might only work with larger data sets showing the length of the palette
    #Creates the bar chart with the grade keys and values as the x and y
    graph = sns.barplot(x=list(grade_counts.keys()), y=list(grade_counts.values()))
    

    graph.set_title("Letter Grade Totals")
    graph.set(xlabel="Letter Grade", ylabel="Frenquency")

students = input_scoring()
summarize_grades(students)
```
