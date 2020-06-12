# hcaptcha.js

Validate your hCaptcha token using a middleware.

## Usage

```
npm i hcaptcha.js --save
```

```js
const bodyParser = require('body-parser');
const express = require('express');
const hcaptcha = require('hcaptcha.js');

// your hcaptcha secret key
const SECRET = process.env.HCAPTCHA_SECRET_KEY;
const PORT = process.env.PORT || 8080;

const app = express();

// middleware
app.use(bodyParser.json()); // required by express-hcaptcha

// validate the token and proceed to the route when token is valid
// the middleware also sets the req.hcaptcha to what ever the verify call returns
app.post('/verify', hcaptcha.middleware.validate(SECRET), (req, res) => {
  if (req.hcaptcha) {
    // Captcha was successful
  } else {
    // Captcha was not filled out.
  }
});

app.listen(PORT, () => {
  console.log(`listening on http://0.0.0.0:${PORT}`);
});
```