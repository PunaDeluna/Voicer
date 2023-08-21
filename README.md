# Voicer
Voice helper
import speech_recognition as sr
from gtts import gTTS
import os

def listen_for_command():
    recognizer = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening for a command...")
        audio = recognizer.listen(source)

    try:
        command = recognizer.recognize_google(audio)
        print("You said:", command)
        return command.lower()
    except sr.UnknownValueError:
        print("Could not understand audio.")
        return None

def respond(text):
    tts = gTTS(text=text, lang='en')
    tts.save("response.mp3")
    os.system("mpg321 response.mp3")

def main():
    print("Voice Assistant - Ready for commands!")
    
    while True:
        command = listen_for_command()
        
        if command:
            if "hello" in command:
                respond("Hello! How can I assist you?")
            elif "time" in command:
                respond("The current time is 3:30 PM.")
            elif "weather" in command:
                respond("The weather is sunny with a high of 25°C.")
            elif "goodbye" in command:
                respond("Goodbye! Have a great day.")
                break
            else:
                respond("Sorry, I couldn't understand that command.")

if __name__ == "__main__":
    main()
