# python-CBC-APP
A Python Tkinter desktop app to input and analyze CBC parameters, providing automated diagnostic feedback and interactive visual results for anemia, erythrocytosis, leukopenia, and infection indicators.
import tkinter as tk
from tkinter import messagebox

class CBCApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Hematology CBC Parameter App")

        # Create input fields for CBC parameters
        self.red_blood_cell_count_label = tk.Label(root, text="Red Blood Cell Count (cells/L):")
        self.red_blood_cell_count_label.pack()
        self.red_blood_cell_count_entry = tk.Entry(root)
        self.red_blood_cell_count_entry.pack()

        self.hemoglobin_label = tk.Label(root, text="Hemoglobin (grams/dL):")
        self.hemoglobin_label.pack()
        self.hemoglobin_entry = tk.Entry(root)
        self.hemoglobin_entry.pack()

        self.hematocrit_label = tk.Label(root, text="Hematocrit (%):")
        self.hematocrit_label.pack()
        self.hematocrit_entry = tk.Entry(root)
        self.hematocrit_entry.pack()

        self.white_blood_cell_count_label = tk.Label(root, text="White Blood Cell Count (cells/L):")
        self.white_blood_cell_count_label.pack()
        self.white_blood_cell_count_entry = tk.Entry(root)
        self.white_blood_cell_count_entry.pack()

        # Create button to submit input values
        self.submit_button = tk.Button(root, text="Submit", command=self.analyze_cbc)
        self.submit_button.pack()

        # Create label to display diagnosis
        self.diagnosis_label = tk.Label(root, text="")
        self.diagnosis_label.pack()

        # Create animated character
        self.character_label = tk.Label(root, text="", font=("Arial", 24))
        self.character_label.pack()

    def analyze_cbc(self):
        # Get input values
        red_blood_cell_count = float(self.red_blood_cell_count_entry.get())
        hemoglobin = float(self.hemoglobin_entry.get())
        hematocrit = float(self.hematocrit_entry.get())
        white_blood_cell_count = float(self.white_blood_cell_count_entry.get())

        # Analyze CBC parameters
        diagnosis = ""
        if red_blood_cell_count < 4.35e12:
            diagnosis += "Anemia (low red blood cell count)\n"
        elif red_blood_cell_count > 5.65e12:
            diagnosis += "Erythrocytosis (high red blood cell count)\n"

        if hemoglobin < 13.2:
            diagnosis += "Anemia (low hemoglobin)\n"
        elif hemoglobin > 16.6:
            diagnosis += "Erythrocytosis (high hemoglobin)\n"

        if hematocrit < 38.3:
            diagnosis += "Anemia (low hematocrit)\n"
        elif hematocrit > 48.6:
            diagnosis += "Erythrocytosis (high hematocrit)\n"

        if white_blood_cell_count < 3.4e9:
            diagnosis += "Leukopenia (low white blood cell count)\n"
        elif white_blood_cell_count > 9.6e9:
            diagnosis += "Infection or inflammation (high white blood cell count)\n"

        # Display diagnosis
        self.diagnosis_label.config(text=diagnosis)

        # Animate character
        self.animate_character(diagnosis)

    def animate_character(self, diagnosis):
        if "Anemia" in diagnosis:
            self.character_label.config(text="😓", font=("Arial", 48))
        elif "Erythrocytosis" in diagnosis:
            self.character_label.config(text="🤯", font=("Arial", 48))
        elif "Leukopenia" in diagnosis:
            self.character_label.config(text="😕", font=("Arial", 48))
        elif "Infection or inflammation" in diagnosis:
            self.character_label.config(text="🤒", font=("Arial", 48))
        else:
            self.character_label.config(text="😊", font=("Arial", 48))

root = tk.Tk()
app = CBCApp(root)
root.mainloop()

