# GhanaNLP Automatic Speech Recognition API v1

> **Fast & Efficient ASR** - Quick transcription for single sentences across multiple African languages

## 🎯 Overview

The GhanaNLP ASR v1 API provides our standard automatic speech recognition models, designed for fast transcription of single sentences. This API prioritizes speed and supports multiple African languages, making it ideal for real-time applications and quick transcription tasks.

## 🚀 Quick Start

### Basic Usage

```bash
curl -X POST "https://translation-api.ghananlp.org/asr/v1/transcribe?language=tw" \
  -H "Content-Type: audio/mpeg" \
  --data-binary "@your_audio_file.mp3"
```

### Python Example

```python
import requests

def transcribe_audio_v1(audio_file_path, language='tw'):
    """
    Transcribe audio using GhanaNLP ASR v1 API
    
    Args:
        audio_file_path (str): Path to your audio file
        language (str): Language code (see supported languages)
    
    Returns:
        dict: Transcription response
    """
    url = f"https://translation-api.ghananlp.org/asr/v1/transcribe?language={language}"
    
    with open(audio_file_path, 'rb') as audio_file:
        response = requests.post(
            url,
            headers={'Content-Type': 'audio/mpeg'},
            data=audio_file.read()
        )
    
    return response.json()

# Usage examples for different languages
twi_result = transcribe_audio_v1('twi_speech.mp3', 'tw')
hausa_result = transcribe_audio_v1('hausa_speech.mp3', 'ha')
yoruba_result = transcribe_audio_v1('yoruba_speech.mp3', 'yo')
```

### JavaScript Example

```javascript
async function transcribeAudioV1(audioFile, language = 'tw') {
    const url = `https://translation-api.ghananlp.org/asr/v1/transcribe?language=${language}`;
    
    const response = await fetch(url, {
        method: 'POST',
        headers: {
            'Content-Type': 'audio/mpeg'
        },
        body: audioFile
    });
    
    return await response.json();
}

// Usage with different languages
const fileInput = document.getElementById('audioFile');
const file = fileInput.files[0];

// Transcribe in Twi
transcribeAudioV1(file, 'tw').then(result => console.log('Twi:', result));

// Transcribe in Hausa
transcribeAudioV1(file, 'ha').then(result => console.log('Hausa:', result));
```

## 📋 API Reference

### Endpoint

```
POST https://translation-api.ghananlp.org/asr/v1/transcribe
```

### Parameters

| Parameter  | Type   | Required | Description                                   |
| ---------- | ------ | -------- | --------------------------------------------- |
| `language` | string | ✅        | Language code (see supported languages below) |

### Request Body

- **Content-Type:** `audio/mpeg`
- **Body:** Binary audio data

### Response

- **Status:** `200 OK`
- **Description:** Transcription successful

## 🌍 Supported Languages

| Language | Code  | Native Name |
| -------- | ----- | ----------- |
| Twi      | `tw`  | Twi         |
| Ga       | `gaa` | Gã          |
| Dagbani  | `dag` | Dagbanli    |
| Yoruba   | `yo`  | Yorùbá      |
| Ewe      | `ee`  | Eʋegbe      |
| Kikuyu   | `ki`  | Gĩkũyũ      |
| Hausa    | `ha`  | Hausa       |

## ✨ Key Features

- **Multi-language Support**: 7 African languages supported
- **Fast Processing**: Optimized for quick response times
- **Single Sentence Focus**: Ideal for short audio clips
- **Real-time Ready**: Suitable for real-time applications
- **Lightweight**: Efficient resource usage

## 🎵 Audio Requirements

- **Format**: MP3 (audio/mpeg)
- **Duration**: Best for single sentences or short phrases
- **Quality**: Clear audio recommended for optimal results
- **Language**: Must match selected language parameter

## 📝 Usage Examples by Language

### Twi (tw)

```python
# Transcribe Twi audio
result = transcribe_audio_v1('hello_twi.mp3', 'tw')
print("Twi transcription:", result)
```

### Hausa (ha)

```python
# Transcribe Hausa audio
result = transcribe_audio_v1('hello_hausa.mp3', 'ha')
print("Hausa transcription:", result)
```

### Yoruba (yo)

```python
# Transcribe Yoruba audio
result = transcribe_audio_v1('hello_yoruba.mp3', 'yo')
print("Yoruba transcription:", result)
```

## 🔧 Error Handling

```python
import requests

def safe_transcribe(audio_file_path, language):
    try:
        result = transcribe_audio_v1(audio_file_path, language)
        return result
    except requests.exceptions.RequestException as e:
        print(f"API Request failed: {e}")
        return None
    except FileNotFoundError:
        print(f"Audio file not found: {audio_file_path}")
        return None
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None

# Usage with error handling
result = safe_transcribe('speech.mp3', 'tw')
if result:
    print("Transcription successful:", result)
else:
    print("Transcription failed")
```

## 🚀 Performance Tips

1. **Audio Length**: Keep audio clips short (single sentences) for best performance
2. **Language Selection**: Ensure audio language matches the selected language parameter
3. **Audio Quality**: Use clear, noise-free audio for better accuracy
4. **Batch Processing**: For multiple files, process them sequentially to avoid rate limits

## 🔄 When to Use v1 vs v2

### Use ASR v1 when:

- You need fast response times
- Processing single sentences or short phrases
- Building real-time applications
- Working with multiple African languages
- Speed is more important than advanced features

### Use ASR v2 when:

- You need the highest accuracy
- Processing long-form audio
- You need punctuation and timing information
- Code-switching detection is required
- Accuracy is more important than speed

## 📞 Support & Contact

- **Organization**: GhanaNLP
- **Email**: natural.language.processing.gh@gmail.com
- **Website**: https://ghananlp.org/
- **License**: End User License Agreement (EULA)

## 📚 Additional Resources

- [Terms and Conditions](https://ghananlp.org/terms)
- ASR v2 API Documentation
- Text-to-Speech API
- [Community Forum](https://ghananlp.org/community)

------

*Need higher accuracy and advanced features? Check out our ASR v2 API with punctuation and timing information.*