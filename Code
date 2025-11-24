import random
import string
import tkinter as tk
from tkinter import messagebox

def generate_password(length, characters):
    return ''.join(random.choice(characters) for _ in range(length))

def evaluate_password(password):
    score = 0
    if any(c.isdigit() for c in password):
        score += 2
    if any(c.islower() for c in password):
        score += 2
    if any(c.isupper() for c in password):
        score += 2
    if any(c in string.punctuation for c in password):
        score += 2
    if len(password) >= 8:
        score += 2
    return score

def generate():
    num_passwords = int(entry_num_passwords.get())
    length = int(entry_length.get())
    use_numbers = var_use_numbers.get()
    use_uppercase = var_use_uppercase.get()
    use_lowercase = var_use_lowercase.get()
    use_special_chars = var_use_special_chars.get()

    characters = ""
    if use_numbers:
        characters += string.digits
    if use_uppercase:
        characters += string.ascii_uppercase
    if use_lowercase:
        characters += string.ascii_lowercase
    if use_special_chars:
        characters += string.punctuation

    for _ in range(num_passwords):
        password = generate_password(length, characters)
        password_listbox.insert(tk.END, password)

def evaluate():
    password = entry_password.get()
    score = evaluate_password(password)
    messagebox.showinfo("Security Evaluation", f"Password security score: {score} out of 10")

# Function to update text from virtual keyboard buttons
def update_choice(key):
    focused_widget = root.focus_get()
    if focused_widget:
        focused_widget.insert(tk.END, key)

# Delete last character
def delete():
    focused_widget = root.focus_get()
    if focused_widget:
        current_text = focused_widget.get()
        focused_widget.delete(0, tk.END)
        focused_widget.insert(tk.END, current_text[:-1])

# Copy text
def copy():
    focused_widget = root.focus_get()
    if focused_widget:
        root.clipboard_clear()
        root.clipboard_append(focused_widget.get())

# Paste text
def paste():
    focused_widget = root.focus_get()
    if focused_widget:
        focused_widget.insert(tk.END, root.clipboard_get())

# Update button font size
def update_icon_size(event):
    font_size = scale.get()
    for button in buttons:
        button.config(font=("Helvetica", font_size))

# GUI creation
root = tk.Tk()
root.title("Password Generator")

root.geometry("2000x1400")

frame_left = tk.Frame(root)
frame_left.pack(side=tk.LEFT, padx=20, pady=20, expand=True, fill='both')

frame_right = tk.Frame(root)
frame_right.pack(side=tk.RIGHT, padx=20, pady=20, expand=True, fill='both')

# Password generation area (Right)
tk.Label(frame_right, text="Passwords", font=("Helvetica", 16)).pack()
password_listbox = tk.Listbox(frame_right, font=("Helvetica", 12))
password_listbox.pack(expand=True, fill='both')

# Settings section (Left)
tk.Label(frame_left, text="Settings", font=("Helvetica", 16)).pack()

tk.Label(frame_left, text="How many passwords to generate?", font=("Helvetica", 12)).pack()
entry_num_passwords = tk.Entry(frame_left, font=("Helvetica", 12))
entry_num_passwords.pack()

tk.Label(frame_left, text="Length of each password:", font=("Helvetica", 12)).pack()
entry_length = tk.Entry(frame_left, font=("Helvetica", 12))
entry_length.pack()

var_use_numbers = tk.BooleanVar()
tk.Checkbutton(frame_left, text="Use numbers", variable=var_use_numbers, font=("Helvetica", 12)).pack()

var_use_uppercase = tk.BooleanVar()
tk.Checkbutton(frame_left, text="Use uppercase letters", variable=var_use_uppercase, font=("Helvetica", 12)).pack()

var_use_lowercase = tk.BooleanVar()
tk.Checkbutton(frame_left, text="Use lowercase letters", variable=var_use_lowercase, font=("Helvetica", 12)).pack()

var_use_special_chars = tk.BooleanVar()
tk.Checkbutton(frame_left, text="Use special characters", variable=var_use_special_chars, font=("Helvetica", 12)).pack()

tk.Button(frame_left, text="Generate", command=generate, font=("Helvetica", 12)).pack(pady=5)
tk.Button(frame_left, text="Exit", command=root.quit, font=("Helvetica", 12)).pack(pady=5)

tk.Label(frame_left, text="Write your password to evaluate its security:", font=("Helvetica", 12)).pack()
entry_password = tk.Entry(frame_left, font=("Helvetica", 12))
entry_password.pack()
tk.Button(frame_left, text="Evaluate", command=evaluate, font=("Helvetica", 12)).pack(pady=5)

# Icon size slider
scale = tk.Scale(frame_left, from_=8, to=30, orient='horizontal',
                 label="Icon Size", command=update_icon_size, font=("Helvetica", 12))
scale.set(12)
scale.pack(pady=10)

# Keyboard section (Bottom)
frame_keyboard = tk.Frame(root)
frame_keyboard.pack(side=tk.BOTTOM, pady=20, expand=True, fill='both')

keys = [
    '1', '2', '3', '4', '5', '6', '7', '8', '9', '0',
    'Delete', 'Ctrl+C', 'Ctrl+V'
]

buttons = []
for key in keys:
    if key == 'Delete':
        button = tk.Button(frame_keyboard, text=key, command=delete, font=("Helvetica", 12))
    elif key == 'Ctrl+C':
        button = tk.Button(frame_keyboard, text=key, command=copy, font=("Helvetica", 12))
    elif key == 'Ctrl+V':
        button = tk.Button(frame_keyboard, text=key, command=paste, font=("Helvetica", 12))
    else:
        button = tk.Button(frame_keyboard, text=key,
                           command=lambda k=key: update_choice(k),
                           font=("Helvetica", 12))
    button.pack(side=tk.LEFT, padx=1)
    buttons.append(button)

root.mainloop()
