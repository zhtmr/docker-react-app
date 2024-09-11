
## memo
- `docker-compose.yml`
  - 로컬 용
  - volumes : 로컬에는 컨테이너 내부의 `node_modules` 를 제외한 나머지만 매핑한다.   
    ![image](https://github.com/user-attachments/assets/6d23fca3-418b-45bd-a269-36ead4d53ad3)

- `Dockerfile.dev`
  - 로컬 용
  - 이미지 빌드 시 npm install 은 package.json 파일이 변경되었을 때만 실행하도록 하기 위해 COPY 부분을 둘로 나눈다.  
    ![image](https://github.com/user-attachments/assets/8fdc4f16-5bb3-4a81-8bd0-3c2f58a0dc91)

- `Dockerfile`
  - 운영 용
  - 로컬에서 터미널로 돌릴때와 달리 클라우드 환경에서 가동될 가볍고 빠른 서버가 필요함. (live-reload 등 개발 환경에 특화된 기능을 제외한 서버)
  - buildStage 에서 빌드한 파일을 nginx 에게 전달한다. (`COPY --from=builder /usr/src/app/build /usr/share/nginx/html`)
  - nginx 이미지의 경우 `/usr/share/nginx/html` 경로 아래로 static 파일 넣을 경우 알아서 페이지 찾아줌
    ![image](https://github.com/user-attachments/assets/81a52df6-449a-4d5e-ae03-5e7dc400090d)
    
    참고 : [https://hub.docker.com/_/nginx/](https://hub.docker.com/_/nginx/)
