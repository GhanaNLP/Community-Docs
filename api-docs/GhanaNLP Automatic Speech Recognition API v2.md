# GhanaNLP Automatic Speech Recognition API v2

> **Most Accurate ASR Models** - Advanced speech recognition with punctuation, word-level timing, and code-switching support

## 🎯 Overview

The GhanaNLP ASR v2 API provides our most accurate automatic speech recognition models, designed for high-quality transcription of long-form audio. This API includes advanced features like punctuation insertion, word-level timing information, and code-switching detection (English speech within local languages).

**⚠️ Note:** This API is optimized for accuracy over speed and is not suitable for real-time applications.

## 🚀 Quick Start

### Basic Usage

```bash
curl -X POST "https://translation-api.ghananlp.org/asr/v2/transcribe?language=tw" \
  -H "Content-Type: audio/mpeg" \
  --data-binary "@your_audio_file.mp3"
```

### Python Example

```python
import requests

def transcribe_audio(audio_file_path, language='tw'):
    """
    Transcribe audio using GhanaNLP ASR v2 API
    
    Args:
        audio_file_path (str): Path to your audio file
        language (str): Language code (default: 'tw' for Twi)
    
    Returns:
        dict: Transcription response
    """
    url = f"https://translation-api.ghananlp.org/asr/v2/transcribe?language={language}"
    
    with open(audio_file_path, 'rb') as audio_file:
        response = requests.post(
            url,
            headers={'Content-Type': 'audio/mpeg'},
            data=audio_file.read()
        )
    
    return response.json()

# Usage
result = transcribe_audio('speech.mp3', 'tw')
print(result)
```

### JavaScript Example

```javascript
async function transcribeAudio(audioFile, language = 'tw') {
    const url = `https://translation-api.ghananlp.org/asr/v2/transcribe?language=${language}`;
    
    const response = await fetch(url, {
        method: 'POST',
        headers: {
            'Content-Type': 'audio/mpeg'
        },
        body: audioFile
    });
    
    return await response.json();
}

// Usage with file input
const fileInput = document.getElementById('audioFile');
const file = fileInput.files[0];
transcribeAudio(file, 'tw').then(result => console.log(result));
```

## 📋 API Reference

### Endpoint

```
POST https://translation-api.ghananlp.org/asr/v2/transcribe
```

### Parameters

| Parameter  | Type   | Required | Description                                     |
| ---------- | ------ | -------- | ----------------------------------------------- |
| `language` | string | ✅        | Language code (currently supports `tw` for Twi) |

### Request Body

- **Content-Type:** `audio/mpeg`
- **Body:** Binary audio data

### Response

- **Status:** `200 OK`
- **Description:** Transcription successful with enhanced features

## 🌍 Supported Languages

| Language | Code |
| -------- | ---- |
| Twi      | `tw` |

## ✨ Key Features

- **High Accuracy**: Our most precise ASR models
- **Punctuation**: Automatic punctuation insertion
- **Word-level Timing**: Detailed timing information for each word
- **Code-switching**: Detects and handles English speech within local languages
- **Long-form Audio**: Optimized for extended audio content

## 🎵 Audio Requirements

- **Format**: MP3 (audio/mpeg)
- **Quality**: Higher quality audio yields better results
- **Duration**: Optimized for long-form content
- **Language**: Clear speech in supported languages

## 📝 Best Practices

1. **Audio Quality**: Use high-quality audio recordings for best results
2. **Clear Speech**: Ensure speakers articulate clearly
3. **Minimize Background Noise**: Reduce ambient noise for better accuracy
4. **File Size**: Consider file size limits for your use case
5. **Error Handling**: Always implement proper error handling for API calls

## 🔧 Error Handling

```python
try:
    result = transcribe_audio('speech.mp3', 'tw')
    print("Transcription:", result)
except requests.exceptions.RequestException as e:
    print(f"API Error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
```

## 📞 Support & Contact

- **Organization**: GhanaNLP
- **Email**: natural.language.processing.gh@gmail.com
- **Website**: https://ghananlp.org/
- **License**: End User License Agreement (EULA)

## 📚 Additional Resources

- [Terms and Conditions](https://ghananlp.org/terms)
- [API Documentation](https://ghananlp.org/docs)
- [Community Forum](https://ghananlp.org/community)

------

*For real-time applications, consider using our ASR v1 API which is optimized for speed.*