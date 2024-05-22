from tkinter import *
import pyqrcode
from tkinter import filedialog
from PIL import Image, ImageTk
import tkinter as tk
import shutil

root = Tk()
root.title("QR Code Generator")
root.geometry("550x550")

def check_entry():
    if not my_entry.get():
        my_button.config(state=tk.DISABLED)
    else:
        my_button.config(state=tk.NORMAL)

def create_code():
    # Get the text from the entry
    global text
    text = my_entry.get()

    # Check if the entry is not empty
    if text:
        # Create QR code
        qr_code = pyqrcode.create(text)

        # Save QR code as PNG file
        global file_name
        file_name = "qr_code.png"
        qr_code.png(file_name, scale=8)

        # Open the image file
        image = Image.open(file_name)

        # Convert image to Tkinter PhotoImage
        photo = ImageTk.PhotoImage(image)

        # Update label with the QR code image
        my_label.config(image=photo)
        my_label.image = photo # Keep a reference to prevent garbage collection

        # Delete text from the entry
        my_entry.delete(0, END)

        # Show a finished message
        my_entry.insert(0, "Finished!")
   

def save_qr():
    try:
        # Get the filename to save as from the user
        filename = filedialog.asksaveasfilename(defaultextension=".png", filetypes=[("PNG files", "*.png")])
    
        # If the user selected a filename
        if filename:
            # Copy the QR code image to the chosen filename
            shutil.copyfile(file_name, filename)
            print("QR code saved successfully!")
    except Exception as e:
        print("Error saving QR code:", str(e))

def clear_all():
    my_entry.delete(0, END)
    my_label.config(image="")

def show_info():
    new_window = Toplevel(root)
    new_window.title("QR Code Information")
    new_window.geometry("300x200")
    
    label_info = Label(new_window, text="QR Code Content:", font=("Helvetica", 14))
    label_info.pack(pady=10)

    content_label = Label(new_window, text=text, font=("Helvetica", 12))
    content_label.pack(pady=10)

# Create GUI
title_label =  Label(root, text="QR Code Generator",font=("Helvetica", 24, "bold"),bg="lightgray",fg="darkblue", relief=SOLID, bd=2,padx=20, pady=10)                       
title_label.pack(pady=10)

info_button = Button(root,  text="Show Info", font=("Helvetica", 14), bg="lightblue", fg="darkblue", activebackground="blue", activeforeground="white", relief=RAISED, bd=4, padx=10, pady=5 , command=show_info)
info_button.pack(anchor=NW, side=TOP, padx=10, pady=10)

my_entry = Entry(root, font=("Helvetica", 18, "italic"), bg="lightyellow", fg="blue", insertbackground="red", relief=RIDGE, bd=3, highlightbackground="gray", highlightcolor="green", highlightthickness=2)
my_entry.pack(pady=20)
my_entry.insert(0, "Input website link!")
my_entry.bind("<KeyRelease>", lambda event: check_entry())  # Bind the entry to check function


my_button = Button(root, text="Create QR code", command=create_code, state=tk.DISABLED, font=("Helvetica", 14), bg="lightblue", fg="darkblue", activebackground="blue", activeforeground="white", relief=RAISED, bd=4, padx=10, pady=5)
my_button.pack(pady=20)

my_button3 = Button(root, text="Save", command=save_qr, font=("Helvetica", 14), bg="lightblue", fg="darkblue", activebackground="blue", activeforeground="white", relief=RAISED, bd=4, padx=10, pady=5)
my_button3.pack()

my_button2 = Button(root, text="Clear", command=clear_all, font=("Helvetica", 14), bg="lightblue", fg="darkblue", activebackground="blue", activeforeground="white", relief=RAISED, bd=4, padx=10, pady=5)
my_button2.pack()

my_label = Label(root, text="")
my_label.pack(pady=20)



root.mainloop()
