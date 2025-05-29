# KTranslate 🌍✨

A simple, lightweight, and fast Node.js library for translating text using multiple AI providers including Gemini AI, OpenAI, Claude, Cohere, Mistral, and DeepSeek. Designed for ease of use in CLI tools, web services, chatbots, and more.

---

## ✨ Features

- 🌍 Translate text easily in your Node.js applications
- 🚀 Minimal setup with zero external dependencies
- 🔑 Supports multiple AI providers with customizable models
- 🗣️ Language detection (`detectLanguage`)
- 🧩 Batch translation (`translateBatch`)
- ⚡ Smart caching for repeated translations and detections
- 🏷️ Skip translation for specified languages

---

## 🚀 Installation

Install via npm:

```sh
npm install kiou-translate
```

---

## 🛠️ Usage

```javascript
const KTranslate = require('kiou-translate');

const translator = new KTranslate({
  apiKey: 'YOUR_GEMINI_API_KEY', // Replace with your API key
  lang: 'en',                   // Target language code (ISO 639-1)
  provider: { name: 'gemini' }, // Provider name and optional model
  skipLang: ['en']              // Optional: languages to skip translation for
});

(async () => {
  // Translate a single text
  const originalText = 'Halo dunia!';
  const translated = await translator.translate(originalText);
  console.log(translated); // Output: "Hello world!"

  // Detect language of a text
  const detectedLang = await translator.detectLanguage('Bonjour le monde!');
  console.log(detectedLang); // Output: "fr"

  // Translate multiple texts in batch
  const batchTranslations = await translator.translateBatch([
    'Halo dunia!',
    'Bonjour le monde!',
    'Hola mundo!'
  ]);
  console.log(batchTranslations); // Output: [ 'Hello world!', 'Hello world!', 'Hello world!' ]
})();
```

---

## ⚙️ Configuration Options

| Option      | Type     | Required | Description                                                                                   |
|-------------|----------|----------|-----------------------------------------------------------------------------------------------|
| `apiKey`    | string   | ✅        | Your API key for the selected AI provider.                                                   |
| `lang`      | string   | ✅        | Target language code (ISO 639-1), e.g., `en`, `id`, `fr`.                                   |
| `provider`  | object   | ✅        | `{ name: 'gemini' \| 'openai' \| 'claude' \| 'cohere' \| 'mistral' \| 'deepseek', model?: string }` |
| `skipLang`  | string[] | ❌        | Array of language codes to skip translation for. Default is `[]`.                            |

---

## 🔑 Supported Providers and Default Models

| Provider | Default Model               |
|----------|-----------------------------|
| gemini   | gemini-2.0-flash-lite       |
| openai   | gpt-3.5-turbo-0125          |
| claude   | claude-3-sonnet-20240229    |
| cohere   | command-a-03-2025           |
| mistral  | mistral-medium              |
| deepseek | deepseek-chat              |

You can specify a custom model by passing the `model` property in the `provider` object.

---

## 🔧 API Methods

### `translate(text: string): Promise<string>`

Translates a single string to the target language. Throws an error if input is invalid.

### `translateBatch(texts: string[]): Promise<string[]>`

Translates an array of strings to the target language. Returns an array of translated strings. Errors in individual translations are returned as error messages in the array.

### `detectLanguage(text: string): Promise<string>`

Detects the language of the input text and returns the ISO 639-1 language code.

---

## ⚡ Caching

KTranslate caches translation and language detection results in a local file `.ktranslate/.ktranslate-cache.json` in your current working directory to speed up repeated requests.

---

## 🧑‍💻 Examples

### Basic Example with Gemini

```javascript
const KTranslate = require('kiou-translate');

const translator = new KTranslate({
  apiKey: 'YOUR_GEMINI_API_KEY',
  lang: 'en',
  provider: { name: 'gemini' }
});

(async () => {
  const text = 'Halo dunia!';
  const translated = await translator.translate(text);
  console.log(translated); // "Hello world!"
})();
```

### Using OpenAI with Skip Languages

```javascript
const KTranslate = require('kiou-translate');

const translator = new KTranslate({
  apiKey: 'YOUR_OPENAI_API_KEY',
  lang: 'id',
  provider: { name: 'openai' },
  skipLang: ['id', 'ms'] // Skip translation if text is already in Indonesian or Malay
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

### Handling Errors in Batch Translation

```javascript
const KTranslate = require('kiou-translate');

const translator = new KTranslate({
  apiKey: 'YOUR_API_KEY',
  lang: 'en',
  provider: { name: 'openai' }
});

(async () => {
  const texts = ['Hello', '', null, 'Bonjour'];
  const results = await translator.translateBatch(texts);
  console.log(results);
  // Output might include error messages for invalid inputs, e.g.:
  // [ 'Hello', '[ERROR: "text" must be a non-empty string for translation.]', '[ERROR: "text" must be a non-empty string for translation.]', 'Hello' ]
})();
```

---

## ❓ Troubleshooting

- Ensure your API key is valid and has the necessary permissions.
- Check your internet connection.
- If you encounter API errors, verify the provider name and model are correct.
- Cache file `.ktranslate/.ktranslate-cache.json` can be deleted to reset cached data.

---

## 📄 License

This project is licensed under a proprietary license. See the [LISENCE.txt](./LISENCE.txt) file for details.
