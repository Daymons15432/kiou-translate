# KTranslate 🌍✨

A simple and lightweight Node.js library for translating text using Gemini AI, OpenAI, Claude, Cohere, Mistral, DeepSeek — fast, intuitive, and easy to use! 🧠💬

---

## ✨ Features

- 🌍 Translate text easily in your Node.js app
- 🚀 Minimal setup
- 📦 Zero external dependencies
- 💡 Perfect for CLI tools, web services, or chatbots
- 🔑 Supports multiple AI providers: Gemini, OpenAI, Claude, Cohere, Mistral, DeepSeek
- 🏷️ Custom model selection per provider
- 🗣️ Language detection (`detectLanguage`)
- 🧩 Batch translation (`translateBatch`)
- ⚡ Smart caching for repeated translations and detections

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
  provider: { name: 'gemini' }, // Required: provider name, e.g., 'gemini', 'openai', etc.
  skipLang: ['en'] // (Optional) Languages to skip translation for
});

(async () => {
  const originalText = 'Halo dunia!';
  const translated = await translator.translate(originalText);
  console.log(translated); // "Hello world!"

  // Detect language
  const lang = await translator.detectLanguage('Bonjour le monde!');
  console.log(lang); // "fr"

  // Batch translation
  const batch = await translator.translateBatch([
    'Halo dunia!',
    'Bonjour le monde!',
    'Hola mundo!'
  ]);
  console.log(batch); // [ 'Hello world!', 'Hello world!', 'Hello world!' ]
})();
```

## ⚙️ Configuration

| Option      | Type     | Required | Description                                                                 |
|-------------|----------|----------|-----------------------------------------------------------------------------|
| `apiKey`    | string   | ✅        | Your API Key for the selected provider.                                     |
| `lang`      | string   | ✅        | Target language code (ISO 639-1), e.g., `en`, `id`, `fr`.                   |
| `provider`  | object   | ✅        | `{ name: 'gemini' \| 'openai' \| 'claude' \| 'cohere' \| 'mistral' \| 'deepseek', model?: string }` |
| `skipLang`  | string[] | ❌        | Array of language codes to skip translation for (default: `[]`)              |

### Provider Examples

- **Gemini**: `{ name: 'gemini', model: 'gemini-2.0-flash-lite' }`
- **OpenAI**: `{ name: 'openai', model: 'gpt-3.5-turbo-0125' }`
- **Claude**: `{ name: 'claude', model: 'claude-3-sonnet-20240229' }`
- **Cohere**: `{ name: 'cohere', model: 'command-a-03-2025' }`
- **Mistral**: `{ name: 'mistral', model: 'mistral-medium' }`
- **DeepSeek**: `{ name: 'deepseek', model: 'deepseek-chat' }`

If `model` is omitted, a sensible default is used for each provider.

## 🔧 API

### `translate(text: string): Promise<string>`

Translates a single string to the target language.

### `translateBatch(texts: string[]): Promise<string[]>`

Translates an array of strings to the target language.

### `detectLanguage(text: string): Promise<string>`

Detects the language of the input text (returns ISO 639-1 code).

---

## 🧑‍💻 Example: Using OpenAI

```javascript
const KTranslate = require('ktranslate');

const translator = new KTranslate({
  apiKey: 'YOUR_OPENAI_API_KEY',
  lang: 'id',
  provider: { name: 'openai' },
  skipLang: ['id', 'ms']
});

(async () => {
  const text = 'Hello world!';
  const translated = await translator.translate(text);
  console.log(translated); // "Halo dunia!"

  const lang = await translator.detectLanguage('Bonjour le monde!');
  console.log(lang); // "fr"

  const batch = await translator.translateBatch([
    'Good morning!',
    'How are you?',
    'See you soon!'
  ]);
  console.log(batch); // [ 'Selamat pagi!', 'Apa kabar?', 'Sampai jumpa!' ]
})();
```
