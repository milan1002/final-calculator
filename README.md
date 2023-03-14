import math
import tkinter as tk

class Calculator:
    def __init__(self, master):
        self.master = master
        master.title("Calculator")

        # create entry widget to display input and output
        self.display = tk.Entry(master, width=25, font=('Arial', 25))
        self.display.grid(row=0, column=0, columnspan=4, pady=5)

        # create buttons for numbers and operations
        self.create_button("7", 1, 0)
        self.create_button("8", 1, 1)
        self.create_button("9", 1, 2)
        self.create_button("0", 1, 3)

        self.create_button("4", 2, 0)
        self.create_button("5", 2, 1)
        self.create_button("6", 2, 2)
        self.create_button(".", 2, 3)

        self.create_button("1", 3, 0)
        self.create_button("2", 3, 1)
        self.create_button("3", 3, 2)
        self.create_button("C", 3, 3)

        self.create_button("/", 4, 0)
        self.create_button("*", 4, 1)
        self.create_button("-", 4, 2)
        self.create_button("+", 4, 3)

        self.create_button("^2", 5, 0)
        self.create_button("sqrt", 5, 1)
        self.create_button("=", 5, 3)

    def create_button(self, text, row, column, columnspan=1):
        button = tk.Button(self.master, text=text, width=5, height=2, font=('Arial', 20),bg="Black",fg="white",
                           command=lambda: self.button_click(text))
        button.grid(row=row, column=column, columnspan=columnspan, padx=5, pady=5)

    def button_click(self, text):
        if text == "=":
            try:
                # evaluate expression and display result
                result = eval(self.display.get())
                self.display.delete(0, tk.END)
                self.display.insert(0, result)
            except (SyntaxError, ZeroDivisionError, TypeError, ValueError):
                self.display.delete(0, tk.END)
                self.display.insert(0, "Error")
        elif text == "C":
            # clear display
            self.display.delete(0, tk.END)
        elif text == "sqrt":
            try:
                # compute square root and display result
                num = float(self.display.get())
                result = math.sqrt(num)
                self.display.delete(0, tk.END)
                self.display.insert(0, result)
            except (SyntaxError, ZeroDivisionError, TypeError, ValueError):
                self.display.delete(0, tk.END)
                self.display.insert(0, "Error")
        elif text == "^2":
            try:
                # compute square and display result
                num = float(self.display.get())
                result = num**2
                self.display.delete(0, tk.END)
                self.display.insert(0, result)
            except (SyntaxError, ZeroDivisionError, TypeError, ValueError):
                self.display.delete(0, tk.END)
                self.display.insert(0, "Error")
        else:
            # append button text to display
            self.display.insert(tk.END, text)


root = tk.Tk()
calculator = Calculator(root)
root.mainloop()
