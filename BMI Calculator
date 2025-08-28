# BMI Calculation
def calculate_bmi(height_cm, weight_kg):
    height_m = height_cm / 100
    bmi = weight_kg / (height_m ** 2)
    if bmi < 18.5:
        category = "Underweight"
    elif bmi < 25:
        category = "Normal"
    elif bmi < 30:
        category = "Overweight"
    else:
        category = "Obese"
    return round(bmi, 2), category

# Data Storage
import csv
from datetime import datetime

def save_record(username, height, weight, bmi, category, filename="bmi_records.csv"):
    with open(filename, mode='a', newline='') as file:
        writer = csv.writer(file)
        writer.writerow([datetime.now(), username, height, weight, bmi, category])

def load_records(filename="bmi_records.csv"):
    records = []
    try:
        with open(filename, mode='r') as file:
            reader = csv.reader(file)
            records = list(reader)
    except FileNotFoundError:
        pass
    return records

#Visualize BMI trends
import matplotlib.pyplot as plt
from datetime import datetime

def plot_bmi_trend(records, username):
    dates = []
    bmis = []
    for record in records:
        if record[1] == username:
            dates.append(datetime.strptime(record[0], "%Y-%m-%d %H:%M:%S.%f"))
            bmis.append(float(record[4]))
    if dates:
        plt.plot(dates, bmis, marker='o')
        plt.title(f"BMI Trend for {username}")
        plt.xlabel("Date")
        plt.ylabel("BMI")
        plt.grid(True)
        plt.show()

# Simple Tkinter GUI
import tkinter as tk
from bmi_logic import calculate_bmi
from data_manager import save_record, load_records
from plotter import plot_bmi_trend

def submit():
    name = name_entry.get()
    height = float(height_entry.get())
    weight = float(weight_entry.get())
    bmi, category = calculate_bmi(height, weight)
    result_label.config(text=f"BMI: {bmi} ({category})")
    save_record(name, height, weight, bmi, category)

def show_plot():
    records = load_records()
    plot_bmi_trend(records, name_entry.get())

root = tk.Tk()
root.title("BMI Calculator")

tk.Label(root, text="Name").grid(row=0)
tk.Label(root, text="Height (cm)").grid(row=1)
tk.Label(root, text="Weight (kg)").grid(row=2)

name_entry = tk.Entry(root)
height_entry = tk.Entry(root)
weight_entry = tk.Entry(root)

name_entry.grid(row=0, column=1)
height_entry.grid(row=1, column=1)
weight_entry.grid(row=2, column=1)

tk.Button(root, text="Calculate BMI", command=submit).grid(row=3, column=0)
tk.Button(root, text="Show Trend", command=show_plot).grid(row=3, column=1)

result_label = tk.Label(root, text="")
result_label.grid(row=4, columnspan=2)

root.mainloop()
