# Phoeny
Chatbot Project - Phoenix Park (휘닉스 파크) 슬로프 정보 등

## Development Environment
- Vite.js (React.js) v5.2.10 (PORT:3000)
- Express.js (Node.js) (PORT:4000)
- Nodemon library
- Swagger API

```bash
// how to create vite project
npm create vite frontend -- --template react
// how to run
npm run dev

// how to create express project
// install express (by global)
npm install --global express-generator
// create express folder
express backend -e

// how to install nodemon library
npm install --save-dev nodemon
npm install -D nodemon

// how to add Swagger API
npm install -S swagger-ui-express swagger-jsdoc
```

## Swagger API tips
```javascript
// 이렇게 추가하면 Swagger가 보여줄 API 추가 가능
app.use('/api', require('./routes/api'));
```
