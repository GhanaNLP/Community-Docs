# GhanaNLP Text-to-Speech API

> **Natural Voice Synthesis** - Convert text to natural-sounding speech in African languages

## 🎯 Overview

The GhanaNLP Text-to-Speech (TTS) API converts text into natural-sounding speech in multiple African languages. With various speaker voices available for each language, you can create engaging audio content for your applications.

## 🚀 Quick Start

### Basic Text-to-Speech

```bash
curl -X POST "https://translation-api.ghananlp.org/tts/v1/synthesize" \
  -H "Content-Type: application/json" \
  -d '{
    "text": "Ɛte sɛn?",
    "language": "tw",
    "speaker_id": "twi_speaker_4"
  }'
```

### Python Example

```python
import requests
import json

def synthesize_speech(text, language='tw', speaker_id='twi_speaker_4'):
    """
    Convert text to speech using GhanaNLP TTS API
    
    Args:
        text (str): Text to convert to speech
        language (str): Language code
        speaker_id (str): Voice/speaker ID
    
    Returns:
        bytes: Audio data in WAV format
    """
    url = "https://translation-api.ghananlp.org/tts/v1/synthesize"
    
    payload = {
        "text": text,
        "language": language,
        "speaker_id": speaker_id
    }
    
    response = requests.post(
        url,
        headers={'Content-Type': 'application/json'},
        data=json.dumps(payload)
    )
    
    if response.status_code == 200:
        return response.content  # WAV audio data
    else:
        raise Exception(f"TTS API error: {response.status_code}")

# Usage example
text = "Ɛte sɛn?"  # "How are you?" in Twi
audio_data = synthesize_speech(text, 'tw', 'twi_speaker_4')

# Save audio to file
with open('output.wav', 'wb') as f:
    f.write(audio_data)
```

### JavaScript Example

```javascript
async function synthesizeSpeech(text, language = 'tw', speakerId = 'twi_speaker_4') {
    const url = 'https://translation-api.ghananlp.org/tts/v1/synthesize';
    
    const payload = {
        text: text,
        language: language,
        speaker_id: speakerId
    };
    
    const response = await fetch(url, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(payload)
    });
    
    if (response.ok) {
        return await response.blob(); // Audio blob
    } else {
        throw new Error(`TTS API error: ${response.status}`);
    }
}

// Usage example
synthesizeSpeech("Ɛte sɛn?", "tw", "twi_speaker_4")
    .then(audioBlob => {
        // Create audio element and play
        const audioUrl = URL.createObjectURL(audioBlob);
        const audio = new Audio(audioUrl);
        audio.play();
    })
    .catch(error => console.error('Error:', error));
```

## 📋 API Reference

### Main Synthesis Endpoint

```
POST https://translation-api.ghananlp.org/tts/v1/synthesize
```

### Get Available Speakers

```
GET https://translation-api.ghananlp.org/tts/v1/speakers
```

### Get Supported Languages

```
GET https://translation-api.ghananlp.org/tts/v1/languages
```

### Request Body (Synthesis)

| Parameter    | Type   | Required | Description               |
| ------------ | ------ | -------- | ------------------------- |
| `text`       | string | ✅        | Text to convert to speech |
| `language`   | string | ✅        | Language code             |
| `speaker_id` | string | ✅        | Voice/speaker identifier  |

### Response

- **Status:** `200 OK`
- **Content-Type:** `audio/wav`
- **Body:** Audio file in WAV format

## 🌍 Supported Languages & Voices

### Twi (tw)

- `twi_speaker_4`
- `twi_speaker_5`
- `twi_speaker_6`
- `twi_speaker_7`
- `twi_speaker_8`
- `twi_speaker_9`

### Kikuyu (ki)

- `kikuyu_speaker_1`
- `kikuyu_speaker_5`

### Ewe (ee)

- `ewe_speaker_3`
- `ewe_speaker_4`

## 🎵 Advanced Usage Examples

### Voice Comparison Tool

```python
def compare_voices(text, language, speaker_ids):
    """Compare different voices for the same text"""
    audio_files = {}
    
    for speaker_id in speaker_ids:
        try:
            audio_data = synthesize_speech(text, language, speaker_id)
            filename = f"{language}_{speaker_id}.wav"
            
            with open(filename, 'wb') as f:
                f.write(audio_data)
            
            audio_files[speaker_id] = filename
            print(f"Generated: {filename}")
            
        except Exception as e:
            print(f"Error with {speaker_id}: {e}")
    
    return audio_files

# Compare all Twi voices
twi_speakers = ['twi_speaker_4', 'twi_speaker_5', 'twi_speaker_6', 
                'twi_speaker_7', 'twi_speaker_8', 'twi_speaker_9']
audio_files = compare_voices("Ɛte sɛn?", "tw", twi_speakers)
```

### Batch Text Processing

```python
def batch_synthesize(texts, language, speaker_id):
    """Process multiple texts at once"""
    audio_files = []
    
    for i, text in enumerate(texts):
        try:
            audio_data = synthesize_speech(text, language, speaker_id)
            filename = f"audio_{i+1}.wav"
            
            with open(filename, 'wb') as f:
                f.write(audio_data)
            
            audio_files.append(filename)
            print(f"Generated: {filename} - '{text}'")
            
        except Exception as e:
            print(f"Error processing '{text}': {e}")
    
    return audio_files

# Example usage
texts = [
    "Ɛte sɛn?",
    "Me din de Kofi",
    "Medaase"
]
audio_files = batch_synthesize(texts, "tw", "twi_speaker_4")
```

### Web Audio Player

```html
<!DOCTYPE html>
<html>
<head>
    <title>GhanaNLP TTS Demo</title>
</head>
<body>
    <div>
        <textarea id="textInput" placeholder="Enter text to synthesize..."></textarea>
        <select id="languageSelect">
            <option value="tw">Twi</option>
            <option value="ki">Kikuyu</option>
            <option value="ee">Ewe</option>
        </select>
        <select id="speakerSelect">
            <option value="twi_speaker_4">Twi Speaker 4</option>
            <option value="twi_speaker_5">Twi Speaker 5</option>
            <!-- Add more speakers -->
        </select>
        <button onclick="synthesizeAndPlay()">Synthesize Speech</button>
    </div>
    <audio id="audioPlayer" controls style="display: none;"></audio>

    <script>
        async function synthesizeAndPlay() {
            const text = document.getElementById('textInput').value;
            const language = document.getElementById('languageSelect').value;
            const speakerId = document.getElementById('speakerSelect').value;
            
            try {
                const audioBlob = await synthesizeSpeech(text, language, speakerId);
                const audioUrl = URL.createObjectURL(audioBlob);
                
                const audioPlayer = document.getElementById('audioPlayer');
                audioPlayer.src = audioUrl;
                audioPlayer.style.display = 'block';
                audioPlayer.play();
                
            } catch (error) {
                alert('Error synthesizing speech: ' + error.message);
            }
        }
        
        // Include the synthesizeSpeech function from earlier
        // ... (JavaScript function from above)
    </script>
</body>
</html>
```

## 🔧 API Information Endpoints

### Get Available Speakers

```python
def get_speakers():
    """Get list of all available speakers"""
    url = "https://translation-api.ghananlp.org/tts/v1/speakers"
    response = requests.get(url)
    return response.json()

speakers = get_speakers()
print("Available speakers:", speakers)
```

### Get Supported Languages

```python
def get_languages():
    """Get list of all supported languages"""
    url = "https://translation-api.ghananlp.org/tts/v1/languages"
    response = requests.get(url)
    return response.json()

languages = get_languages()
print("Supported languages:", languages)
```

## 📝 Best Practices

1. **Text Quality**: Use properly formatted text with correct spelling
2. **Speaker Selection**: Try different speakers to find the best voice for your use case
3. **Audio Format**: The API returns WAV format - convert if needed
4. **Error Handling**: Always implement proper error handling
5. **Caching**: Cache generated audio files to reduce API calls
6. **Rate Limiting**: Be mindful of API rate limits

## 🔧 Error Handling

```python
import requests
import json

def safe_synthesize(text, language, speaker_id):
    """Synthesize speech with comprehensive error handling"""
    try:
        audio_data = synthesize_speech(text, language, speaker_id)
        return audio_data
        
    except requests.exceptions.RequestException as e:
        print(f"Network error: {e}")
        return None
        
    except json.JSONDecodeError as e:
        print(f"JSON error: {e}")
        return None
        
    except Exception as e:
        print(f"Unexpected error: {e}")
        return None

# Usage with error handling
result = safe_synthesize("Ɛte sɛn?", "tw", "twi_speaker_4")
if result:
    with open('output.wav', 'wb') as f:
        f.write(result)
    print("Speech synthesis successful!")
else:
    print("Speech synthesis failed")
```

## 🚀 Performance Tips

1. **Pre-generate Common Phrases**: Cache frequently used audio
2. **Optimize Text**: Remove unnecessary characters and formatting
3. **Speaker Consistency**: Use the same speaker for consistent user experience
4. **Batch Processing**: Process multiple texts efficiently
5. **Audio Compression**: Consider compressing WAV files for storage

## 📞 Support & Contact

- **Organization**: GhanaNLP
- **Email**: natural.language.processing.gh@gmail.com
- **Website**: https://ghananlp.org/
- **License**: End User License Agreement (EULA)

## 📚 Additional Resources

- [Terms and Conditions](https://ghananlp.org/terms)
- ASR v1 API Documentation
- ASR v2 API Documentation
- [Community Forum](https://ghananlp.org/community)

------

*Create natural-sounding speech in African languages with our comprehensive TTS API. Perfect for applications, accessibility tools, and content creation.*