import tkinter as tk
from tkinter import messagebox
import secrets
import string

def generate_password(length=12):
    alphabet = string.ascii_letters + string.digits + string.punctuation
    password = ''.join(secrets.choice(alphabet) for _ in range(length))
    return password

def on_generate_click():
    try:
        length = int(length_entry.get())
        if length <= 0:
            raise ValueError("Length must be a positive integer.")
        password = generate_password(length)
        password_var.set(password)
    except ValueError as e:
        messagebox.showerror("Invalid input", str(e))

# Create the main window
root = tk.Tk()
root.title("Random Password Generator")

# Create and place widgets
length_label = tk.Label(root, text="Password Length:")
length_label.pack(pady=5)

length_entry = tk.Entry(root)
length_entry.pack(pady=5)

generate_button = tk.Button(root, text="Generate Password", command=on_generate_click)
generate_button.pack(pady=10)

password_var = tk.StringVar()
password_entry = tk.Entry(root, textvariable=password_var, width=40)
password_entry.pack(pady=5)

# Start the GUI event loop
root.mainloop()
