# 다음 FROM  까지 builder Stage임을 명시
# 이 곳의 목표는 빌드파일을 생성하는 것
# 생성한 파일과 폴더들은 /usr/src/app/build로 들어간다
FROM node:alpine as builder 
WORKDIR '/usr/src/app'
COPY package.json .
RUN npm install
COPY ./ ./
RUN npm run build

# Runer Stage
FROM nginx
# 위의 builder Stage에서 복사함을 명시
# Dockerhub 공식 nginx설명에서 기본경로 /usr/share/nginx/html 에 대한 정보가 있으며
# 수정 가능하다(그러나 아래는 기본 설정으로 사용)
COPY --from=builder /usr/src/app/build /usr/share/nginx/html