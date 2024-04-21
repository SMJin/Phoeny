# Phoeny
Chatbot Project - Phoenix Park (휘닉스 파크) 슬로프 정보 등

## Development Environment (Local)
- Vite.js (React.js) v5.2.10 (PORT:3000)
- Express.js (Node.js) (PORT:4000)
- Nodemon library
- Swagger API

## Linux Server Environment (AWS ec2)
- pm2 (Node.js)
- Nginx

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

## AWS ec2 연결
1. ec2 서버 생
2. key.pem 생성 후 keys 폴더 같은 곳에 넣어놓기
3. ssh 로 접속하기
```
ssh -i ./keys/key.pem ec2-user@[ec2 주소]
```
4. Linux 서버에 git 설치
```bash
// git download
sudo yum install git htop -y
```
5. Linux 서버에 node.js 설치
```bash
// node js download
sudo wget https://nodejs.org/dist/v16.17.0/node-v16.17.0-linux-x64.tar.xz
// node js 압축파일 풀기
tar xvf node-v16.17.0-linux-x64.tar.xz
// 푼 압축파일에 들어가서, ~/.bash_profile 파일에 PATH 추가하기
PATH=$PATH:$HOME/.local/bin:$HOME/bin
PATH=$PATH:/home/ec2-user/local/node-v16.14.0-linux-x64/bin
export PATH
// 실행시켜주면 node -v 했을 때 node version 나온다. 정상 설치 완료.
source ~/.bash_profile
node -v
```
6. Linux 서버에 nginx 설치
```bash
sudo yum install nginx
// nginx 설정파일 경로 및 여는 법
sudo vi /etc/nginx/nginx.conf
```
```conf
// nginx.conf 파일에 다음과 같은 코드 추
location / {
        sendfile off;
        proxy_pass         http://127.0.0.1:4000;
        proxy_redirect     default;
        proxy_http_version 1.1;
        proxy_set_header   Host              $host;
        proxy_set_header   X-Real-IP         $remote_addr;
        proxy_set_header   X-Forwarded-For   $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
        proxy_max_temp_file_size 0;
    }
```
```bash
// nginx server start
sudo systemctl start nginx
// linux 서버를 껐다가 켜도 nginx 자동 실행 되도록 설정
sudo systemctl enable nginx
```
7. Linux 서버에 pm2 설치
```bash
npm install -g pm2
```
8. Linux 서버에 git clone 후 서버 실행
```bash
mkdir ~/git
cd ~/git
git clone https://github.com/SMJin/Phoeny
cd Phoeny/frontend/
npm i
npm run build
cp -rf dist/* ../backend/public
cd ../backend/
npm i
pm2 start bin/www --name web
pm2 list
```
9. 
