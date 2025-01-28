# 
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
```