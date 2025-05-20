# KTranslate 🌍✨

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
---

# 🧩 Discord Bot Integration

You can easily integrate this library into your Discord bot to automatically detect and translate user messages. Ideal for multilingual communities, it helps your bot understand and respond in the appropriate language.

## 🔧 Example

```javascript
const KTranslate = require('ktranslate');

const translator = new KTranslate({
  apiKey: 'YOUR_GEMINI_API_KEY',
  lang: 'en', 
  skipLang: ['en']
});

module.exports = (client) => {
  const translateChannels = 'CHANNEL_ID';

  client.on('messageCreate', async (message) => {
    if (message.author.bot || !translateChannels.includes(message.channel.id)) return;

    try {
      const original = message.content;

      const detectedLang = await translator.detectLanguage(original);

      if (translator.skipLang.includes(detectedLang)) return;

      await message.channel.sendTyping();
      const replyMsg = await message.reply('`🔄` | Translating...');

      const translated = await translator.translate(original);

      if (!translated || translated === original) {
        await replyMsg.edit('`⚠️` | Could not translate or already in English.');
        return;
      }

      await replyMsg.edit(`\`🌐\` **Translated to English:**\n${translated}`);

    } catch (error) {
      console.error('❌ | Error during translation:', error);
      await message.reply({ content: '`❌` | An error occurred while translating the message.' });
    }
  });
};
```
