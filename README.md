# ktranslate 🌍✨

A simple and lightweight Node.js library for translating text using Gemini AI — fast, intuitive, and easy to use! 🧠💬

---

## ✨ Features

- 🌍 Translate text easily in your Node.js app
- 🚀 Minimal setup
- 📦 Zero external dependencies
- 💡 Perfect for CLI tools, web services, or chatbots

---

## 🚀 Installation

```sh
npm install ktranslate
```

## 🛠️ Usage

```javascript
const KTranslate = require('ktranslate');

const translator = new KTranslate({
  apiKey: 'YOUR_GEMINI_API_KEY',
  lang: 'en', // Target language code (ISO 639-1)
  skipLang: ['en'] // (Optional) Languages to skip translation for
});

(async () => {
  const originalText = 'Halo dunia!';
  const translated = await translator.translate(originalText);
  console.log(translated); // "Hello world!"
})();
```

## ⚙️ Configuration

| Option     | Type   | Required | Description                                                     |
|------------|--------|----------|-----------------------------------------------------------------|
| `apiKey`   | string |    	✅     | Your Gemini API Key.                                            |
| `lang`     | string |    	✅     | Target language code (ISO 639-1), e.g., `en`, `id`, `fr`.       |
| `skipLang` | string |    	❌     | Array of language codes to skip translation for (default: `[]`) |

## 🔧 Example

```javascript
const KTranslate = require('ktranslate');

const translator = new KTranslate({
  apiKey: 'YOUR_GEMINI_API_KEY',
  lang: 'id',
  skipLang: ['id', 'ms']
});

(async () => {
  const text = 'Hello world!';
  const translated = await translator.translate(text);
  console.log(translated); // "Halo dunia!"
})();

const lang = await translator.detectLanguage('Bonjour le monde!');
console.log(lang); // "fr"
```
