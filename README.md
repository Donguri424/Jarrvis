        import pyttsx3 #pip install pyttsx3
import speech_recognition as sr #pip install speechRecognition
import datetime
import wikipedia #pip install wikipedia
import webbrowser
import os
import smtplib
import socket
import playsound
import pyautogui
import requests
import pyjokes  # pip install pyjokes


socket.getaddrinfo('localhost', 25)

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
# print(voices[1].id)
engine.setProperty('voice', voices[0].id)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def voice_change(v):
    x = int(v)
    engine.setProperty('voice', voices[x].id)
    speak("done sir")

def wishMe():
    hour = int(datetime.datetime.now().hour)
    if hour>=0 and hour<12:
        speak("Good Morning!")

    elif hour>=12 and hour<18:
        speak("Good Afternoon!")   

    else:
        speak("Good Evening!")  

    speak("I am Jarvis Sir. Please tell me how may I help you")       

def takeCommand():
    #It takes microphone input from the user and returns string output

    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")    
        query = r.recognize_google(audio, language='en-in')
        print(f"User said: {query}\n")

    except Exception as e:
        # print(e)    
        print("Say that again please...")  
        return "None"
    return query

def sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('dnm.ibs@gmail.com', '17052008')
    server.sendmail('dnm.ibs@gmail.com', to, content)
    server.close()

def wishme_end():
    speak("signing off")
    hour = datetime.datetime.now().hour
    if (hour >= 6 and hour < 12):
        speak("Good Morning")
    elif (hour >= 12 and hour < 18):
        speak("Good afternoon")
    elif (hour >= 18 and hour < 24):
        speak("Good Evening")
    else:
        speak("Goodnight.. Sweet dreams")
        quit()


def jokes():
     j = pyjokes.get_joke()
     print(j)
     speak(j)

if __name__ == "__main__":
    wishMe()
    while True:
    # if 1:
        query = takeCommand().lower()

        # Logic for executing tasks based on query
        if 'wikipedia' in query:
            speak('Searching Wikipedia...')
            query = query.replace("wikipedia", "")
            results = wikipedia.summary(query, sentences=2)
            speak("According to Wikipedia")
            print(results)
            speak(results)

        

        elif 'open youtube' in query:
            webbrowser.open("youtube.com")

        elif 'open google' in query:
            webbrowser.open("google.com")

        elif 'open stackoverflow' in query:
            webbrowser.open("stackoverflow.com")   


        elif 'play music' in query:
            speak('ok, sir')
            music_dir = 'C:\\Users\\PRATIK\\Favourite music'
            songs = os.listdir(music_dir)
            print(songs)    
            os.startfile(os.path.join(music_dir, songs[0]))

        elif 'the time' in query:
            strTime = datetime.datetime.now().strftime("%H:%M:%S")    
            speak(f"Sir, the time is {strTime}")

        elif 'open code' in query:
            codePath = "C:\\Users\\Pratik\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"
            os.startfile(codePath) 

        elif 'email to durga' in query:
            try:
                speak("What should I say?")
                content = takeCommand()
                to = "dnm.ibs@gmail.com"    
                sendEmail(to, content)
                speak("Email has been sent!")
            except Exception as e:
                print(e)
                speak("Sorry my friend Pratik. I am not able to send this email")

        elif 'open gmail' in query:
            webbrowser.open("gmail.com")

        elif 'open tabs' in query:
            codePath = "C:\\Users\\PRATIK\\Desktop\\TotallyAccurateBattleSimulator"
            os.startfile(codePath)  
            speak("Ok here you go")

        elif 'open angry birds' in query:
            codePath = "C:\\Users\\PRATIK\\Desktop\\Angry Birds 2"
            os.startfile(codePath)
            speak("ok sir")

        elif 'hello' in query:
            speak("Hi sir, how are you doing")
        
        elif 'what are you' in query:
            speak("I am an intelligent voice assistant, sir") 

        elif 'change your voice' in query:
            speak('Sorry for your inconvenience sir, but I am afraid that you will have to complete this command on your own')
            speak('I have two main voices Peppper, and Jarvis, I am currently using Jarvis voice. You can make more voices if you want to.')
            print('you can make more voices from audacity')
            speak('You can change my voice here')
            codePath = "C:\\Users\\PRATIK\\Documents\\Jarvis 1000.py"
            os.startfile(codePath)

#exit function

        elif ('i am done' in query or 'bye bye jarvis' in query
              or 'go offline jarvis' in query or 'bye' in query
              or 'nothing' in query):
            wishme_end()

        elif 'what is my exact location' in query:
            url = "https://www.google.com/maps/search/Where+am+I+?/"
            webbrowser.get().open(url)
            speak("You must be somewhere near here, as per Google maps")
        
        elif 'what is the weather' in query:
            url = "https://www.google.com/search?sxsrf=ACYBGNSQwMLDByBwdVFIUCbQqya-ET7AAA%3A1578847393212&ei=oUwbXtbXDN-C4-EP-5u82AE&q=weather&oq=weather&gs_l=psy-ab.3..35i39i285i70i256j0i67l4j0i131i67j0i131j0i67l2j0.1630.4591..5475...1.2..2.322.1659.9j5j0j1......0....1..gws-wiz.....10..0i71j35i39j35i362i39._5eSPD47bv8&ved=0ahUKEwiWrJvwwP7mAhVfwTgGHfsNDxsQ4dUDCAs&uact=5"
            webbrowser.get().open(url)
            speak("Here is what I found for weather near you on google")

        elif 'can you play chess' in query:
            speak('sure, sir')
            codePath = "C://Users//PRATIK//Downloads//Free Chess//Free Chess"
            os.startfile(codePath)
        
        elif ('processor') in query:
            speak('My owner used an AMD ryzen 5 4600U with MX 330 graphis card I  dont know about you')

        elif ('well done') in query:
            speak('Thanks sir')

        elif ('search for') in query:
            webbrowser.open(query)
            speak('Here is what I found on Google')

        elif('price of') in query:
            webbrowser.open(query)
            speak('Here is what I found on google')

        elif('who made you') in query:
            speak('I was made by mister Pratik Mishra on 29th august, but I am still in development')

        elif('what can you do') in query:
            speak('I can send emails, I can open apps, I can search for what you want, I can tell you the price of things, I can open youtube or google, and I can play chess with you')

        elif('you are useless') in query:
            speak('Sorry sir, please inform my developer mister Pratik your problem')
            print('Please inform your problem on www.github.com')

        elif('I was joking') in query:
            speak('Oh, my humor is still not developed completely')

        elif('open android emulator') in query:
            speak('Ok sir')
            codePath = "C:\\Users\\PRATIK\\Desktop\\Nox"
            os.startfile(codePath)

        elif('i am out of ideas') in query:
            speak('hmm..., you can send an email or ask for things if thats your interest')

        elif ("tell me a joke" in query or "joke" in query):
            jokes()

        elif ('tell me a horror story') in query:
            speak('Tired of causing pain to those around him, Peter jumped from the rooftop in a bid, to end his own life. He soon found himself on a slidewalk below, still very much alive, with the crushed body of a little girl, beneath him')
            print('Tired of causing pain to those around him, Peter jumped from the rooftop in a bid, to end his own life. He soon found himself on a slidewalk below, still very much alive, with the crushed body of a little girl, beneath him')

        elif ("open translator" in query or "translator" in query):
            speak('ok sir')
            webbrowser.open("https://translate.google.co.in/")

        elif ("open excel") in query:
            speak('ok sir')
            codePath = "C:\\Users\\PRATIK\\Desktop\\Excel"
            os.startfile(codePath)

        elif('open unity') in query:
            speak('ok sir')
            codePath = "C:\\Users\\PRATIK\\Desktop\\Unity Hub"
            os.startfile(codePath)

        elif('open minecraft') in query:
            speak('sure, sir')
            codePath = "C:\\Users\\PRATIK\\Desktop\\Minecraft Launcher"
            os.startfile(codePath)

        elif('what is my schedule') in query:
            speak('Sir you have classes from 8 AM to 10 AM, till 11:30 AM you have to make or improve your codes, then you have your breakfast, then you have to self study from 11:40 AM to 2 PM, then you have your free time till 3 PM, remember to make a new python project from 3 PM to 4 PM, afterwards you have to study from 4 PM to 5:30 PM, then after 30 minutes you have to study continuosly from 6 PM to 9 PM, have your dinner and watch Tv from 9:20 PM to 10:30 PM, then you shall go to sleep at 10:40, sir')
            print('Sir you have classes from 8 AM to 10 AM, till 11:30 AM you have to make or improve your codes, then you have your breakfast, then you have to self study from 11:40 AM to 2 PM, then you have your free time till 3 PM, remember to make a new python project from 3 PM to 4 PM, afterwards you have to study from 4 PM to 5:30 PM, then after 30 minutes you have to study continuosly from 6 PM to 9 PM, have your dinner and watch Tv from 9:20 PM to 10:30 PM, then you shall go to sleep at 10:40, sir')

        elif('a schedule bot') in query:
            speak('Sorry sir but only you chose to make your schedule like that, and I am not a freaking schedule bot')
            print('I have feelings too and schedule bots are literally very annoying!')

        elif('open playstation 2 emulator') in query:
            speak('sure, sir')
            codePath = "C:\\Users\\PRATIK\\Documents\\PCSX2 1.6.0\\pcsx2.exe"
            os.startfile(codePath)

        elif('open visual studio') in query:
            speak('sure, sir')
            codePath = "C:\\Users\\PRATIK\\Desktop\\Visual Studio Code"
            os.startfile(codePath)
        
        elif("who is" in query or "what is" in query):
            speak('Here is what I found on google')
            webbrowser.open(query)

        elif("where" in query):
            speak('here is what I fond on google maps')
            url = "https://www.google.com/maps/search/"+(query)
            webbrowser.get().open(url)
            #I did not write locate because it caused errors

        elif('you are better than many assistant') in query:
            speak('thanks sir, but I am not made to compete with them')
       
        elif('i want to see memes') in query:
            speak('Here is what I found on google')
            webbrowser.open('Daily Dose of memes')
            #WHOMST HAS CALLED THE ALL MIGHTY . ..             LOL
            
        elif('near me' in query or 'nearby' in query):
            speak('getting that from google maps')
            url = "https://www.google.com/maps/search/"+(query)
            webbrowser.get().open(url)

        elif('are you there') in query:
            speak('I am always there till you have closed the visual studio window or trash out the terminal')

        elif('download') in query:
            speak('here is what I found on google')
            webbrowser.open(query)

        elif('what can i do for you') in query:
            speak('Sir, it is I who shall do work for you')

        elif('i did not mean to say that') in query:
            speak('please repeat what you said')

        elif('i am in a very bad mood today') in query:
            speak('hmm.... I can play your favourite music if you want to')
            #Why do you have a bad mood?

        elif('can i change this program') in query:
            speak('of course, this is an open source says my developer')
            
        elif('www.') in query:
            speak('opening webpage')
            webbrowser.open(query)


        

            
            




        
      




