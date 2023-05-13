# USERNAME-GUI
code that reads username and password form an excel file. It also shows a login GUI.
import os
import tkinter as tk
import openpyxl
import datetime

#read username and password from excel file
#words that are all caps are what you need to change to your own file path and file name 

excel_file = os.path.abspath("C:/Users/YOURUSER/Documents/DOCUMENTNAME.xlsx")

log_file_path = os.path.abspath("log.txt")
print("Log file path:", log_file_path)

root = tk.Tk()
root.title("Login Screen")
root.geometry("300x250")

username_label = tk.Label(root, text="Username")
username_entry = tk.Entry(root)

password_label = tk.Label(root, text="Password")
password_entry = tk.Entry(root, show="*")

new_password_label = tk.Label(root, text="New Password")
new_password_entry = tk.Entry(root, show="*")

username_label.pack()
username_entry.pack()
password_label.pack()
password_entry.pack()
new_password_label.pack()
new_password_entry.pack()

def validate(action):
    workbook = openpyxl.load_workbook(excel_file)
    worksheet = workbook["Sheet1"]

    entered_username = username_entry.get()
    entered_password = password_entry.get()

    for row in worksheet.iter_rows(min_row=2):
        username = row[0].value
        password = row[1].value

        if entered_username == username and entered_password == password:
            timestamp = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            if action == "login":
                with open("log.txt", "a") as log_file:
                    log_file.write(f"{entered_username} logged in at {timestamp}\n")
            elif action == "logout":
                with open("log.txt", "a") as log_file:
                    log_file.write(f"{entered_username} logged out at {timestamp}\n")
            elif action == "change_password":
                row[1].value = new_password_entry.get()
                workbook.save(excel_file)
                with open("log.txt", "a") as log_file:
                    log_file.write(f"{entered_username} changed password at {timestamp}\n")
            root.destroy()
            break
    else:
        error_label = tk.Label(root, text="Invalid username or password")
        error_label.pack()

def login():
    validate("login")


def change_password():
    validate("change_password")

login_button = tk.Button(root, text="Login", command=login)
login_button.pack()

roles = ["admin", "manager", "employee"] 

change_password_button = tk.Button(root, text="Change Password", command=change_password)
change_password_button.pack()

root.mainloop()
