# Fitness-challenge-app-Project-
import tkinter as tk
from tkinter import simpledialog, messagebox

def calculate_bmi(weight, height):
    return weight / (height/100)**2

def classify_bmi(bmi):
    if bmi < 18.5:
        return "underweight"
    elif bmi < 25:
        return "fit, Congratulations!!"
    else:
        return "overweight"

def submit_details():
    try:
        name = name_entry.get()
        age = int(age_entry.get())
        gender = gender_entry.get()
        height_cm = float(height_entry.get())
        weight_kg = float(weight_entry.get())
        
        bmi = calculate_bmi(weight_kg, height_cm)
        classification = classify_bmi(bmi)
        
        result_text = f"Hello {name}.\nYour BMI is {bmi:.2f}.\nYou are {classification}."
        result_label.config(text=result_text)
        
        if classification == "underweight":
            options_text.config(text="!...HERE ARE SOME CHALLENGES FOR YOU...!!!\n1. Increase your daily calorie intake with nutrient-rich foods.\n2. Start a strength training routine to build muscle mass.\n3. Incorporate healthy fats into your diet, such as avocados and nuts.\n4. Strength training to build muscle mass.\n5. 30-minute gentle yoga for relaxation.")
        elif classification == "fit, Congratulations!!":
            options_text.config(text="1. Maintain a balanced diet rich in fruits, vegetables, and whole grains.\n2. Engage in regular physical activity, such as cardio and strength training.\n3. Stay hydrated by drinking plenty of water throughout the day.\n4. Get enough sleep each night to support overall health and well-being.\n5. Practice stress-reducing techniques like meditation or yoga.")
        elif classification == "overweight":
            options_text.config(text="!!..HERE ARE SOME CHALLENGES TO BECOME A FIT..!!\n1. Reduce your daily calorie intake by avoiding sugary drinks and processed foods.\n2. Running for 30 minutes (daily).\n3. Skipping ropes for 30 minutes (daily).\n4. Brisk walking for 40 minutes (daily).\n5. Cycling for 45 minutes (daily).")
            
        target_weight = weight_kg
        if classification == "underweight":
            target_weight += int(simpledialog.askstring("Input", "How many kilograms would you like to gain in one month?"))
            result_label.after(2000, lambda: result_label.config(text=f"Tracking your progress to gain {target_weight - weight_kg} kg in one month..."))
        elif classification == "overweight":
            target_weight -= int(simpledialog.askstring("Input", "How many kilograms would you like to lose in one month?"))
            result_label.after(2000, lambda: result_label.config(text=f"Tracking your progress to lose {weight_kg - target_weight} kg in one month..."))
        
        result_label.after(4000, lambda: result_label.config(text="One month later..."))
        result_label.after(6000, lambda: result_label.config(text=f"{name}, your weight after one month is {target_weight:.2f} kg."))

    except ValueError:
        messagebox.showerror("Error", "Please enter valid details.")

root = tk.Tk()
root.title("Fitness Challenge App")

details_frame = tk.Frame(root)
details_frame.pack()

name_label = tk.Label(details_frame, text="Enter your name:")
name_label.grid(row=0, column=0, sticky="e")
name_entry = tk.Entry(details_frame)
name_entry.grid(row=0, column=1)

age_label = tk.Label(details_frame, text="Enter your age:")
age_label.grid(row=1, column=0, sticky="e")
age_entry = tk.Entry(details_frame)
age_entry.grid(row=1, column=1)

gender_label = tk.Label(details_frame, text="Enter your gender:")
gender_label.grid(row=2, column=0, sticky="e")
gender_entry = tk.Entry(details_frame)
gender_entry.grid(row=2, column=1)

height_label = tk.Label(details_frame, text="Enter your height in centimeters:")
height_label.grid(row=3, column=0, sticky="e")
height_entry = tk.Entry(details_frame)
height_entry.grid(row=3, column=1)

weight_label = tk.Label(details_frame, text="Enter your weight in kilograms:")
weight_label.grid(row=4, column=0, sticky="e")
weight_entry = tk.Entry(details_frame)
weight_entry.grid(row=4, column=1)

submit_button = tk.Button(details_frame, text="Submit", command=submit_details)
submit_button.grid(row=5, columnspan=2)

result_label = tk.Label(root, text="")
result_label.pack()

options_text = tk.Label(root, text="")
options_text.pack()

root.mainloop()
