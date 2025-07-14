# GhanaNLP Translation REST API

> **Multilingual Translation** - Seamlessly translate between English and African languages

## 🎯 Overview

The GhanaNLP Translation REST API provides powerful translation capabilities between English and multiple African languages. With support for 10+ languages, you can easily integrate translation functionality into your applications for better accessibility and reach.

## 🚀 Quick Start

### Basic Translation

```bash
curl -X POST "https://translation-api.ghananlp.org/v1/translate" \
  -H "Content-Type: application/json" \
  -d '{
    "in": "Hello, how are you?",
    "lang": "en-tw"
  }'
```

### Python Example

```python
import requests
import json

def translate_text(text, language_pair):
    """
    Translate text using GhanaNLP Translation API
    
    Args:
        text (str): Text to translate (max 1000 characters)
        language_pair (str): Language pair in format "from-to" (e.g., "en-tw")
    
    Returns:
        str: Translated text
    """
    url = "https://translation-api.ghananlp.org/v1/translate"
    
    payload = {
        "in": text,
        "lang": language_pair
    }
    
    response = requests.post(
        url,
        headers={'Content-Type': 'application/json'},
        data=json.dumps(payload)
    )
    
    if response.status_code == 200:
        return response.json()  # Returns translated text
    else:
        error_data = response.json()
        raise Exception(f"Translation error: {error_data.get('message', 'Unknown error')}")

# Usage examples
english_to_twi = translate_text("Hello, how are you?", "en-tw")
print(f"English to Twi: {english_to_twi}")

twi_to_english = translate_text("Ɛte sɛn?", "tw-en")
print(f"Twi to English: {twi_to_english}")

# Translate to multiple languages
text = "Good morning"
languages = ["en-tw", "en-gaa", "en-ee", "en-yo"]

for lang_pair in languages:
    result = translate_text(text, lang_pair)
    print(f"{lang_pair}: {result}")
```

### JavaScript Example

```javascript
async function translateText(text, languagePair) {
    const url = 'https://translation-api.ghananlp.org/v1/translate';
    
    const payload = {
        in: text,
        lang: languagePair
    };
    
    try {
        const response = await fetch(url, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(payload)
        });
        
        if (response.ok) {
            return await response.json();
        } else {
            const error = await response.json();
            throw new Error(error.message || 'Translation failed');
        }
    } catch (error) {
        console.error('Translation error:', error);
        throw error;
    }
}

// Usage examples
translateText("Hello, how are you?", "en-tw")
    .then(result => console.log("English to Twi:", result))
    .catch(error => console.error("Error:", error));

translateText("Ɛte sɛn?", "tw-en")
    .then(result => console.log("Twi to English:", result))
    .catch(error => console.error("Error:", error));
```

## 📋 API Reference

### Translation Endpoint

```
POST https://translation-api.ghananlp.org/v1/translate
```

### Get Languages Endpoint

```
GET https://translation-api.ghananlp.org/v1/languages
```

### Translation Request Body

| Parameter | Type   | Required | Description                             |
| --------- | ------ | -------- | --------------------------------------- |
| `in`      | string | ✅        | Text to translate (max 1000 characters) |
| `lang`    | string | ✅        | Language pair in format "from-to"       |

### Example Request

```json
{
    "in": "Hello, how are you?",
    "lang": "en-tw"
}
```

### Successful Response (200 OK)

```json
"Ɛte sɛn?"
```

### Error Response (400 Bad Request)

```json
{
    "type": "validation_error",
    "message": "Input text exceeds maximum length of 1000 characters"
}
```

## 🌍 Supported Languages

| Language | Code  | Native Name |
| -------- | ----- | ----------- |
| English  | `en`  | English     |
| Twi      | `tw`  | Twi         |
| Ga       | `gaa` | Gã          |
| Ewe      | `ee`  | Eʋegbe      |
| Fante    | `fat` | Fante       |
| Dagbani  | `dag` | Dagbanli    |
| Gurene   | `gur` | Gurene      |
| Yoruba   | `yo`  | Yorùbá      |
| Kikuyu   | `ki`  | Gĩkũyũ      |
| Luo      | `luo` | Luo         |
| Kimeru   | `mer` | Kimeru      |

## 🔄 Common Language Pairs

### English to African Languages

- `en-tw` - English to Twi
- `en-gaa` - English to Ga
- `en-ee` - English to Ewe
- `en-fat` - English to Fante
- `en-dag` - English to Dagbani
- `en-gur` - English to Gurene
- `en-yo` - English to Yoruba
- `en-ki` - English to Kikuyu
- `en-luo` - English to Luo
- `en-mer` - English to Kimeru

### African Languages to English

- `tw-en` - Twi to English
- `gaa-en` - Ga to English
- `ee-en` - Ewe to English
- `fat-en` - Fante to English
- `dag-en` - Dagbani to English
- `gur-en` - Gurene to English
- `yo-en` - Yoruba to English
- `ki-en` - Kikuyu to English
- `luo-en` - Luo to English
- `mer-en` - Kimeru to English

## 🎵 Advanced Usage Examples

### Batch Translation

```python
def batch_translate(texts, language_pair):
    """Translate multiple texts with the same language pair"""
    results = []
    
    for text in texts:
        try:
            if len(text) > 1000:
                print(f"Skipping text (too long): {text[:50]}...")
                continue
                
            result = translate_text(text, language_pair)
            results.append({
                'original': text,
                'translated': result,
                'success': True
            })
            
        except Exception as e:
            results.append({
                'original': text,
                'error': str(e),
                'success': False
            })
    
    return results

# Example usage
texts = [
    "Good morning",
    "Thank you",
    "How are you?",
    "What is your name?",
    "Nice to meet you"
]

results = batch_translate(texts, "en-tw")
for result in results:
    if result['success']:
        print(f"'{result['original']}' -> '{result['translated']}'")
    else:
        print(f"Error translating '{result['original']}': {result['error']}")
```

### Multi-Language Translation

```python
def translate_to_multiple_languages(text, target_languages):
    """Translate text to multiple target languages"""
    results = {}
    
    for lang_code in target_languages:
        language_pair = f"en-{lang_code}"
        try:
            translation = translate_text(text, language_pair)
            results[lang_code] = {
                'translation': translation,
                'success': True
            }
        except Exception as e:
            results[lang_code] = {
                'error': str(e),
                'success': False
            }
    
    return results

# Example usage
text = "Welcome to our application"
target_languages = ["tw", "gaa", "ee", "yo", "ki"]

results = translate_to_multiple_languages(text, target_languages)
for lang_code, result in results.items():
    if result['success']:
        print(f"{lang_code}: {result['translation']}")
    else:
        print(f"{lang_code}: Error - {result['error']}")
```

### Get Available Languages

```python
def get_available_languages():
    """Get list of all available languages"""
    url = "https://translation-api.ghananlp.org/v1/languages"
    
    try:
        response = requests.get(url)
        if response.status_code == 200:
            return response.json()
        else:
            raise Exception(f"Failed to get languages: {response.status_code}")
    except Exception as e:
        print(f"Error getting languages: {e}")
        return None

# Usage
languages = get_available_languages()
if languages:
    print("Available languages:")
    for lang_code, lang_name in languages.items():
        print(f"  {lang_code}: {lang_name}")
```

### Web Translation Interface

```html
<!DOCTYPE html>
<html>
<head>
    <title>GhanaNLP Translation Demo</title>
    <style>
        .container { max-width: 800px; margin: 0 auto; padding: 20px; }
        textarea { width: 100%; height: 100px; margin: 10px 0; }
        select, button { padding: 10px; margin: 5px; }
        .result { background: #f0f0f0; padding: 15px; margin: 10px 0; }
    </style>
</head>
<body>
    <div class="container">
        <h1>GhanaNLP Translation</h1>
        
        <div>
            <label>From Language:</label>
            <select id="fromLang">
                <option value="en">English</option>
                <option value="tw">Twi</option>
                <option value="gaa">Ga</option>
                <option value="ee">Ewe</option>
                <option value="yo">Yoruba</option>
            </select>
            
            <label>To Language:</label>
            <select id="toLang">
                <option value="tw">Twi</option>
                <option value="en">English</option>
                <option value="gaa">Ga</option>
                <option value="ee">Ewe</option>
                <option value="yo">Yoruba</option>
            </select>
        </div>
        
        <textarea id="inputText" placeholder="Enter text to translate (max 1000 characters)..."></textarea>
        <button onclick="translateText()">Translate</button>
        
        <div id="result" class="result" style="display: none;"></div>
    </div>

    <script>
        async function translateText() {
            const inputText = document.getElementById('inputText').value;
            const fromLang = document.getElementById('fromLang').value;
            const toLang = document.getElementById('toLang').value;
            const resultDiv = document.getElementById('result');
            
            if (!inputText.trim()) {
                alert('Please enter text to translate');
                return;
            }
            
            if (inputText.length > 1000) {
                alert('Text exceeds maximum length of 1000 characters');
                return;
            }
            
            if (fromLang === toLang) {
                alert('Please select different source and target languages');
                return;
            }
            
            const languagePair = `${fromLang}-${toLang}`;
            
            try {
                resultDiv.style.display = 'block';
                resultDiv.innerHTML = 'Translating...';
                
                const translation = await translateTextAPI(inputText, languagePair);
                resultDiv.innerHTML = `<strong>Translation:</strong> ${translation}`;
                
            } catch (error) {
                resultDiv.innerHTML = `<strong>Error:</strong> ${error.message}`;
            }
        }
        
        async function translateTextAPI(text, languagePair) {
            const url = 'https://translation-api.ghananlp.org/v1/translate';
            
            const response = await fetch(url, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    in: text,
                    lang: languagePair
                })
            });
            
            if (response.ok) {
                return await response.json();
            } else {
                const error = await response.json();
                throw new Error(error.message || 'Translation failed');
            }
        }
        
        // Character counter
        document.getElementById('inputText').addEventListener('input', function(e) {
            const length = e.target.value.length;
            const maxLength = 1000;
            
            if (length > maxLength) {
                e.target.value = e.target.value.substring(0, maxLength);
            }
        });
    </script>
</body>
</html>
```

## 🔧 Error Handling

### Common Error Types

```python
def safe_translate(text, language_pair):
    """Translate with comprehensive error handling"""
    try:
        # Validate input length
        if len(text) > 1000:
            raise ValueError("Text exceeds maximum length of 1000 characters")
        
        # Validate language pair format
        if '-' not in language_pair:
            raise ValueError("Invalid language pair format. Use 'from-to' format")
        
        result = translate_text(text, language_pair)
        return result
        
    except requests.exceptions.RequestException as e:
        print(f"Network error: {e}")
        return None
        
    except ValueError as e:
        print(f"Validation error: {e}")
        return None
        
    except Exception as e:
        print(f"Translation error: {e}")
        return None

# Usage with error handling
result = safe_translate("Hello world", "en-tw")
if result:
    print(f"Translation: {result}")
else:
    print("Translation failed")
```

### Error Response Handling

```python
def handle_translation_response(response):
    """Handle different response scenarios"""
    if response.status_code == 200:
        return response.json()
    
    elif response.status_code == 400:
        error_data = response.json()
        error_type = error_data.get('type', 'unknown')
        error_message = error_data.get('message', 'Unknown error')
        
        if error_type == 'validation_error':
            print(f"Validation error: {error_message}")
        elif error_type == 'language_error':
            print(f"Language error: {error_message}")
        else:
            print(f"Error: {error_message}")
            
        return None
        
    else:
        print(f"Unexpected error: {response.status_code}")
        return None
```

## 📝 Best Practices

1. **Text Length**: Keep texts under 1000 characters for single requests
2. **Language Pairs**: Verify language pair format ("from-to")
3. **Error Handling**: Always implement proper error handling
4. **Rate Limiting**: Be mindful of API rate limits
5. **Text Preprocessing**: Clean and format text appropriately
6. **Caching**: Cache translations to reduce API calls
7. **Validation**: Validate inputs before sending requests

## 🚀 Performance Tips

1. **Batch Processing**: Process multiple texts efficiently
2. **Text Optimization**: Remove unnecessary formatting
3. **Connection Reuse**: Use session objects for multiple requests
4. **Async Processing**: Use async/await for better performance
5. **Error Recovery**: Implement retry logic for failed requests

## 🔄 Integration Examples

### Flask Web App Integration

```python
from flask import Flask, request, jsonify
import requests

app = Flask(__name__)

@app.route('/translate', methods=['POST'])
def translate_endpoint():
    data = request.json
    text = data.get('text', '')
    language_pair = data.get('language_pair', 'en-tw')
    
    try:
        translation = translate_text(text, language_pair)
        return jsonify({
            'success': True,
            'translation': translation,
            'original': text,
            'language_pair': language_pair
        })
    except Exception as e:
        return jsonify({
            'success': False,
            'error': str(e)
        }), 400

if __name__ == '__main__':
    app.run(debug=True)
```

### Django Integration

```python
# views.py
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
import json

@csrf_exempt
def translate_view(request):
    if request.method == 'POST':
        data = json.loads(request.body)
        text = data.get('text', '')
        language_pair = data.get('language_pair', 'en-tw')
        
        try:
            translation = translate_text(text, language_pair)
            return JsonResponse({
                'success': True,
                'translation': translation
            })
        except Exception as e:
            return JsonResponse({
                'success': False,
                'error': str(e)
            }, status=400)
    
    return JsonResponse({'error': 'Method not allowed'}, status=405)
```

## 📞 Support & Contact

- **Organization**: GhanaNLP
- **Email**: natural.language.processing.gh@gmail.com
- **Website**: https://ghananlp.org/
- **License**: End User License Agreement (EULA)

## 📚 Additional Resources

- [Terms and Conditions](https://ghananlp.org/terms)
- ASR v1 API Documentation
- ASR v2 API Documentation
- Text-to-Speech API
- [Community Forum](https://ghananlp.org/community)

------

*Break down language barriers with seamless translation between English and African languages. Perfect for applications, websites, and accessibility tools.*