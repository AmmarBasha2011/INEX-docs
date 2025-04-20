# Enable Multi Language

<figure><img src="../../.gitbook/assets/ChatGPT Image Apr 20, 2025, 06_26_02 PM.png" alt="" width="375"><figcaption></figcaption></figure>

You can enable multi languages in your website:

* 1- update .env:

```ini
DETECT_LANGUAGE=true
```

* 2- create a language file in `lang` folder, for example `en.json` or `ar.json` :

```json
// en.json
{
    "title": "Hello"
}
```

```json
// ar.json
{
    "title": "أهلا"
}
```

* 3- Use in any part in application:

```html
<h1><?= Language::get('title'); ?></h1>
<form>
    <button type="button" onclick="submitData('setLanguage', [], 'POST', '', ['lang':'en'])">English</button>
    <button type="button" onclick="submitData('setLanguage', [], 'POST', '', ['lang':'ar'])">العربية</button>
</form>
```
