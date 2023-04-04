# Support

if you find this Repo was helpful don't forget to give it a star. Thank you
Supports me : [Ko-fi](https://ko-fi.com/ardhach)

# Update

V3.0 Now not only supports Japanese TTS using VoiceVox. But also supports TTS for RU (Russian), EN (English), DE (German), ES (Spanish), FR (French), TT (Tatar), UA (Ukrainian), UZ (Uzbek), XAL (Kalmyk), Indic (Hindi), using Seliro TTS. Change `voicevox_tts` on `run.py` to `seliro_tts`, for detailed information of how to use [Seliro TTS](https://github.com/snakers4/silero-models#text-to-speech)

# AI Waifu Vtuber & Assistant

This project is inspired by shioridotdev and utilizes various technologies such as VoiceVox Engine, DeepL, Whisper OpenAI, Seliro TTS and VtubeStudio to create an AI waifu virtual YouTuber.

![My Remote Image](https://github.com/ardha27/AI-Waifu-Vtuber/blob/master/ss.png?raw=true)

## Demo
 - [Demo](https://www.youtube.com/shorts/_mKVr3ZaM9Q)
 - [Live Test](https://youtu.be/h6UEgJxH1-E?t=1616)
 - [Code Explain](https://youtu.be/qpNG9qrcmrQ)

## Technologies Used

 - [VoiceVox Docker](https://hub.docker.com/r/voicevox/voicevox_engine) or [VoiceVox Colab](https://github.com/SociallyIneptWeeb/LanguageLeapAI/blob/main/src/run_voicevox_colab.ipynb)
 - [DeepL](https://www.deepl.com/fr/account/summary)
 - [Deeplx](https://github.com/OwO-Network/DeepLX)
 - [Whisper OpenAI](https://platform.openai.com/account/api-keys)
 - [Seliro TTS](https://github.com/snakers4/silero-models#text-to-speech)
 - [VB-Cable](https://vb-audio.com/Cable/)
 - VtubeStudio


## Installation

1. Install the dependencies

```
pip install -r requirements.txt
```

2. Create config.py and store your Openai API key

```
api_key = 'yourapikey'
```

3. Change the owner name

```
owner_name = "Ardha"
```

4. Change the lore or identity of your assistant. Change the txt file at `characterConfig\Pina\identity.txt`

5. Choose which TTS you want to use, `VoiceVox` or `Silero`. Uncomment and Comment to switch between them

```
# Choose between the available TTS engines
# Japanese TTS
voicevox_tts(tts)

# Silero TTS, Silero TTS can generate English, Russian, French, Hindi, Spanish, German, etc. Uncomment the line below. Make sure the input is in that language
# silero_tts(tts_en, "en", "v3_en", "en_21")
```

If you want to use VoiceVox, you need to run VoiceVox Engine first. You can run them on local using [VoiceVox Docker](https://hub.docker.com/r/voicevox/voicevox_engine) or on Google Colab using [VoiceVox Colab](https://github.com/SociallyIneptWeeb/LanguageLeapAI/blob/main/src/run_voicevox_colab.ipynb). If you use the Colab one, change `voicevox_url` on `utils\TTS.py` using the link you get from Colab.

```
voicevox_url = 'http://localhost:50021'
```

6. Choose which translator you want to use depends on your use case (optional if you need translation for the answers). Choose between google translate or deeplx. You need to convert the answer to Japanese if you want to use `VoiceVox`, because VoiceVox only accepts input in Japanese. The language answer from OpenAI will depens on your assistant lore language `characterConfig\Pina\identity.txt` and the input language

```
tts = translate_deeplx(text, f"{detect}", "JA")
tts = translate_google(text, f"{detect}", "JA")
```

`DeepLx` is free version of `DeepL` (No API Key Required). You can run [Deeplx](https://github.com/OwO-Network/DeepLX) on docker, or if you want to use the normal version of deepl, you can make the function on `utils\translate.py`. I use `DeepLx` because i can't register on `DeepL` from my country. The translate result from `DeepL` is more accurate and casual than Google Translate. But if you want the simple way, just use Google Translate.

7. If you want to use the audio output from the program as an input for your `Vtubestudio`. You will need to capture your desktop audio using `Virtual Cable` and use it as input on VtubeStudio microphone.

8. If you planning to use this program for live streaming Use `chat.txt` and `output.txt` as an input on OBS Text for Realtime Caption/Subtitles

## FAQ

1. Error Transcribing Audio

```
def transcribe_audio(file):
    global chat_now
    try:
        audio_file= open(file, "rb")
        # Translating the audio to English
        # transcript = openai.Audio.translate("whisper-1", audio_file)
        # Transcribe the audio to detected language
        transcript = openai.Audio.transcribe("whisper-1", audio_file)
        chat_now = transcript.text
        print ("Question: " + chat_now)
    except:
        print("Error transcribing audio")
        return

    result = owner_name + " said " + chat_now
    conversation.append({'role': 'user', 'content': result})
    openai_answer()
```

Change this Line of Code to this. This will help you to get more information about the error

```
def transcribe_audio(file):
    global chat_now
    audio_file= open(file, "rb")
    # Translating the audio to English
    # transcript = openai.Audio.translate("whisper-1", audio_file)
    # Transcribe the audio to detected language
    transcript = openai.Audio.transcribe("whisper-1", audio_file)
    chat_now = transcript.text
    print ("Question: " + chat_now)


    result = owner_name + " said " + chat_now
    conversation.append({'role': 'user', 'content': result})
    openai_answer()
```

Another option to solve this problem, you can upgrade the OpenAI library to the latest version. Make sure the program capture your voice/sentence, try to hear the `input.wav`

2. Mecab Error

this library is a little bit tricky to install. If you facing this problem, you can just delete and don't use the `katakana_converter`. That function is optional, you can run the program without it

```
katakana_text = katakana_converter(tts)
```

delete this line on `run.py` and just pass the `tts` to next line of the code

## Credits

This project is inspired by the work of shioridotdev. Special thanks to the creators of the technologies used in this project including VoiceVox Engine, DeepL, Whisper OpenAI, and VtubeStudio.

