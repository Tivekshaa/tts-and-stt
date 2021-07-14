# tts-and-stt
project
import os
import requests
from tkinter import *
from gtts import gTTS
from playsound import playsound
from PIL import Image
import speech_recognition as sr
import pyaudio
import time
import urllib.request

urllib.request.urlretrieve('https://raw.githubusercontent.com/nyow/sample-repo/master/img_exit1.png' , "ic_exit.png")
urllib.request.urlretrieve('https://raw.githubusercontent.com/nyow/sample-repo/master/img_reset1.png' , "ic_reset.png")
urllib.request.urlretrieve('https://raw.githubusercontent.com/nyow/sample-repo/master/img_play.png' , "ic_play.png")

root = Tk()
root.geometry("500x500")
root.configure(bg='#F7E2E9')
root.title("TEXT TO SPEECH & SPEECH TO TEXT")
Label(root, text = "TEXT TO SPEECH AND SPEECH TO TEXT", font = "arial 10 bold",bg = '#F7E2E9').pack()
Label(text ="THANK YOU", bg = '#F7E2E9',font = 'arial 15 bold', width = '20').pack(side = 'bottom')
Msg = StringVar()
entry_field = Entry(root, textvariable = Msg ,width ='35',font = 'arial 12 bold')
entry_field.place(x=90,y=280)
       
def Text_to_speech():
        
        Msg=entry_field.get()
        speech = gTTS(text = Msg)
        speech.save('music.mp3')
        playsound('music.mp3')
        os.remove('music.mp3')
def Exit():
    root.destroy()
def Reset():
     Msg.set("")
def clear(widget):
     widget.destroy()
def Speech_to_text():
 recognizer = sr.Recognizer()
 with sr.Microphone() as inputs:
    recognizer.adjust_for_ambient_noise(inputs)
    #Label(text="Please speak now",width='35',font="arial 12 bold").place(x=125,y=60)
    print("Please speak now")
    listening = recognizer.listen(inputs,phrase_time_limit=4)
    #Label(text="Analysing",width='35',font="arial 12 bold").place(x=125,y=80)
    print("Analysing")

    try:
        print(recognizer.recognize_google(listening))
        Label(text=recognizer.recognize_google(listening),width='35',font="arial 12 bold").place(x=68,y=110)
        
        
    except:
        print("please speak again")
        #Label(text="Please speak again",width='35',font="arial 12 bold").pack()

#img  = Image.open("https://raw.githubusercontent.com/nyow/sample-repo/master/img_exit1.png")
imgplay= PhotoImage(file='ic_play.png')
imgreset= PhotoImage(file='ic_reset.png')
imgexit= PhotoImage(file='ic_exit.png')
Button(root, text = "Speech to text", bg = '#6dcff6',font = 'arial 15 bold' , command = Speech_to_text ,width = '20').place(x=125,y=30)
Button(root, text = "Text to speech", bg = '#6dcff6',font = 'arial 15 bold' , command = Text_to_speech ,width = '20').place(x=125,y=180)
Button(root, image=imgplay, command = Text_to_speech ,width = '100',height= '30' ,bd=0).place(x=205,y=350)
Button(root, image=imgexit, width = '100' ,height= '30' , bd=0, command = Exit).place(x=100 , y = 350)
Button(root, image=imgreset, width = '100' ,height= '30' , command = Reset,bd=0).place(x=310,y=350)



root.mainloop()

