# USERNAME-GUI
code that reads username and password form an excel file. It also shows a login GUI.
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

def login():
    validate("login")
