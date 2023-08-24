Как запустить:

1. Установить nodemailer: `npm install nodemailer`
2. Отредактировать 3 константы и запустить код:

```js
const nodemailer = require('nodemailer');

const user = 'user'                // Необходимо заменить на реальный логин
const pass = 'password'            // Необходимо заменить на реальный пароль
const to   = 'example@example.com' // Необходимо заменить на email получателя

let transporter = nodemailer.createTransport({
    host: 'smtp.mailer-demo.ru',
    port: 587,
    auth: {
        user: user,
        pass: pass
    }
});

/*
 * Отправителя тоже можно заменить на своего.
 * Для этого нужно к своему домену добавить TXT-запись SPF вида
 * v=spf1 include:spf.mailer-demo.ru
 */
let from = 'admin@mailer-demo.ru'

let mailOptions = {
    from: from,
    to: to,
    subject: 'test subject',
    text: 'test body', // plain text body
    // html: '<p>test html body</p>' // html body
};

transporter.sendMail(mailOptions, (error, info) => {
    if (error) {
        return console.log(error);
    }
    console.log('Message sent: %s', info.messageId);
});
```