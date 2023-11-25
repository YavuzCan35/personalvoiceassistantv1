import datetime
import webbrowser
import gtts
import time
from playsound import playsound
import os
#https://www.lfd.uci.edu/~gohlke/pythonlibs/#pyaudio adresinden pyaudio amd64 indirildi scripts kısmına atıldı. prioje dosyasında scripte ggidilip activate edilip  pip install xxx.whl yapılarak portaudio y
#yüklenmişoldu
import speech_recognition as sr
import pyttsx3
from io import BytesIO


def konus(st):
    tts = gtts.gTTS ( st, lang="tr", slow=False, lang_check=False )
    tts.save ( f"audio.mp3" )
    audio_file = os.path.dirname ( __file__ ) + fr'/audio.mp3'
    playsound ( f"audio.mp3",True )
    os.remove ( audio_file )

r=sr.Recognizer()
def dinle():
    with sr.Microphone() as source:
        r.adjust_for_ambient_noise (
            source,duration=2 )  # listen for 1 second to calibrate the energy threshold for ambient noise levels
        r.pause_threshold = 0.5
        r.operation_timeout = 6
        print('dinleniyor...')
        audit=r.listen(source)
        print('dinlendi.')
        voice=''
        try:
            voice=r.recognize_google(audit,language='tr-TR')
            print(voice)
        except sr.UnknownValueError:
            print('.')
            dinle()
        except sr.RequestError:
            konus('sistem çalışmıyor')
        return voice
def çarpmaoyunu():
    konus('bana iki sayı ver, ve bende çarpımlarını hesaplayacağım.')
    b=dinle()
    print(b)
    c=dinle()
    print(c)
    konus('teşekkür ederim!')
    if c.isdigit() and b.isdigit():
        a = f'{b} çarpı {c} sence kaç eder?'
        konus ( a )
        get = dinle()
        konus ( f'{get} diyorsun emin misin?' )
        print ( int ( get ) )
        if int(get)!=int(b)*int(c):
            konus(f'Bunu bile bilmiyorsun cahil, yanlış cevap. Cevap {int(b)*int(c)} olmalıydı. Kaynak mı soruyorsun ? kaynak götüm! hahahaha.')
        elif int(get)==int(b)*int(c):
            print('????')
            konus('ooooo matematiğin çok iyi, tebrik ederim doğru bildin. ')
    else:
        konus('söylediklerinden en az birisi sayı değil!')

def response(voice):
    if 'saat kaç' in voice or 'saat nedir' in voice:
        konus(f'{datetime.datetime.now().hour}:{datetime.datetime.now().minute}')
    if 'teşekkür' in voice:
        konus('benim için bir zevkti')
        quit()
    if 'arama' in voice:
        konus('ne için arama yapacağım?')
        search=dinle()
        print(search)
        if search=='YouTube':
            URL='https://www.youtube.com/'
        else:
            URL='https://www.google.com/search?q='+search
        webbrowser.get().open(URL)
        konus(f'{search} için bulduklarım bunlar')
    if 'oynayalım' in voice:
        çarpmaoyunu()
    if 'aşkım' in voice:
        konus('söyle aşkımm')
    if 'aşkın benim' in voice:
        konus('sen öyle san hahaha')

konus('Merhaba ne lazımdı?')
while 1:
    voice=dinle()
    print(voice)
    response(voice)
