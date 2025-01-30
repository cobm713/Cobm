b# 
```
import speech_recognition as sr
import pyttsx3

# Inicializa el reconocedor de voz
r = sr.Recognizer()

# Inicializa el sintetizador de voz
engine = pyttsx3.init()

# Función para procesar la entrada de voz
def procesar_voz(audio):
    # Reconoce la entrada de voz
    texto = r.recognize_google(audio, language='es-ES')
    
    # Realiza la acción correspondiente
    if texto == 'hola':
        engine.say('Hola, ¿cómo estás?')
        engine.runAndWait()
    elif texto == 'adiós':
        engine.say('Adiós, hasta luego')
        engine.runAndWait()

# Función para escuchar la entrada de voz
def escuchar_voz():
    with sr.Microphone() as source:
        audio = r.listen(source)
        procesar_voz(audio)

# Escucha la entrada de voz
escuchar_voz()
```python
import telebot
from telebot import types
import speech_recognition as sr
import pyttsx3
bot = telebot.TeleBot('comb.713token')
r = sr.Recognizer()
engine = pyttsx3.init()
def procesar_voz(audio):
    try:
        texto = r.recognize_google(audio, language='es-ES')
        if texto == 'hola':
            bot.reply_to(audio, 'Hola, ¿cómo estás?')
        elif texto == 'adiós':
            bot.reply_to(audio, 'Adiós, hasta luego')
    except sr.UnknownValueError:
        bot.reply_to(audio, 'Lo siento, no entendí lo que dijiste.')
    except sr.RequestError as e:
        bot.reply_to(audio, 'Error al procesar la voz: '+ str(e))
def escuchar_voz(message):
    file_id = message.voice.file_id
    file = bot.get_file(file_id)
    file_path = file.file_path
    audio = bot.download_file(file_path)
    with sr.AudioFile(audio) as source:
        audio_data = r.record(source)
        procesar_voz(audio_data)
@bot.message_handler(content_types=['voice'])
def voice_message(message):
    escuchar_voz(message)
bot.polling()

```