# Speech_To_Text_py
Create a Speech to Text system in Python

import tkinter as tk
import speech_recognition as sr
from tkinter import messagebox

def speech_to_text():
    r = sr.Recognizer()
    try:
        with sr.Microphone() as source:
            audio = r.listen(source)
            text = r.recognize_google(audio)
            txtspeech.insert(tk.END, text + "\n")
    except sr.UnknownValueError:
        txtspeech.insert(tk.END, "Could not understand audio\n")
    except sr.RequestError as e:
        txtspeech.insert(tk.END, f"Could not request results; {e}\n")
    except Exception as e:
        txtspeech.insert(tk.END, f"An error occurred: {e}\n")

def reset():
    txtspeech.delete("1.0", tk.END)

def exit():   
    result = messagebox.askquestion("Exit Application", "Are you sure you want to exit the application?", icon='warning')
    if result == 'yes':
        messagebox.showinfo("GoodBye", "Good bye")
        root.quit()

root = tk.Tk()
root.title("Speech To Text")
MainFrame = tk.Frame(root, bd=20, width=900, height=300)
MainFrame.pack()

lblTitle = tk.Label(MainFrame, font=('arial', 80, 'bold'), text="Speech To Text", width=18)
lblTitle.pack()

txtspeech = tk.Text(MainFrame, font=('arial', 30, 'bold'), width=68, height=12)
txtspeech.pack()

btnConvert = tk.Button(MainFrame, font=('arial', 30, 'bold'), text="Convert To Text", width=18, height=2, command=speech_to_text)
btnConvert.pack(side=tk.LEFT, padx=5)

btnReset = tk.Button(MainFrame, font=('arial', 30, 'bold'), text="Reset", width=18, height=2, command=reset)
btnReset.pack(side=tk.LEFT, padx=5)

btnExit = tk.Button(MainFrame, font=('arial', 30, 'bold'), text="Exit", width=18, height=2, command=exit)
btnExit.pack(side=tk.LEFT, padx=5)

root.mainloop()
