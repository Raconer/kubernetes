### 쿠버네티스(Kubernetes, 쿠베르네테스, "K8s")

  **쿠버네티스** 란?

    쿠버네티스 는 디플로이 자동화, 스케일링, 컨테이너화된 애플리케이션의 관리를 위한 오픈 소스 시스템 으로 
    원래 구글에 의해 설계되었고 현재 리눅스 재단에 의해 관리되고 있다.
    
   **쿠버네티스** 사용 목적
    
    여러 클러스터의 호스트 간에 애플리 케이션 컨테이너의 배치, 스케일링, 운영을 자동화 하기 위한 플랫폼을 제공하기 위함 이다.
    도커를 포함하여 일련의 컨테이너 도구들과 함께 동작한다.

  쿠버네티스를 설명하기 앞서 필요한 정보

    1. 컨테이너란 무엇인가?

      사전적 의미로 컨테이너는 어떤 물체를 격리하는 공간 을 뜻한다.
      클라우드에서 컨테이너 는 어떤 의미를 가질까?

        "컨테이너는 애플리케이션 과 애플리케이션 을 구동하는 환경을 격리한 공간을 뜻한다."

      컨테이너 기술은 약 10여 년 전에 리눅스에 내장된 기술로 소개되었으며, 
      현재는 차세대 트렌드 기술(2018.01.12 기준) 로 주목 받으며 클라우드 서비스 환경에 적용되고 있다.

    2. 왜 컨테이너 인가?

      ㄱ. 가상 머신 과 컨테이너 의 차이점

          가상머신 서버 에서는 하이퍼바이저로 하드웨어를 가상화하고, 그 위에 Guest OS가 설치된 가상 머신들을 구동시킨다.
          반면에 컨테이너 서버 는 운영체제 레벨에서 CPU, RAM, Dist, Network 등의 자원을 격리하여 컨테이너 할당하기 때문에 
          Guest OS가 필요 없다.

          1) 효율성

            기업환경에서는 안정적인 운영을 위해, 1개의 가상머신(VM, Virtual Machine)에 1개의 서비스를 구동하는 것이 권장된다.
            이의 경우 가상머신 의 모든 자원을 사용하는 것이 아니기 때문에 성능적 오버헤드가 발생합니다.
            반면 컨테이너 의 경우, OS 커널을 공유하기 때문에 자원을 필요한 만큼 효율적으로 사용할수있다.

          2) 신속성

            사용자의 서비스 요청량이 증가함에 따라, 기업에서는 가성머신이나 컨테이너를 추가적으로 배포한다.
            가상머신의 크기는 최소 몇 GB이지만, 컨테이너의 경우 Guest OS가 없어 MB단위의 크기를 가집니다.
            
            결과적으로 
             가상머신은 배포하는데 수 분에서 수십분의 시간이 소요되지만, 
             컨테이너는 배포에 소요되는 시간이 수 초 에 불과합니다.

          3) 라이센스 비용절감

            가상화 서버 의 경우 가상머신의 개수 만큼 Guest OS의 라이센스 비용이 발생한다.
            반면 컨테이너 서버 의 경우 Host OS 1대의 라이센스 비용만 발생한다.
            만약 서버의 수가 많아진다면 비용의 차이도 기하 급수적으로 증가 할 것이다.

          4) 안정성

            가상머신 의 경우 정확히 할당된 자원 내에서 가상머신이 운영되기 때문에, 컨테이너 에 비해 안정적 으로 운영할 수 있다.
            반면에 컨테이너들 은 OS커널을 공유하기 때문에, 하나의 컨테이너가 무리하게 자원을 사용 하게 될수 있다.
            자원 할당량을 사전에 지정시켜줄수 있지만, 만약 이런 상황이 발생하면 컨테이너에 장애가 발생한다.

      ㄴ. 개발 환경 이전 솔루션

        주로 애플리케이션을 개발할 때는 개인 환경에서 개발을 하고, 통합 환경에서 코드를 통합한다. 
        그 다음 테스트 환경을 거쳐 실제 운영 환경으로 이전하게 된다.
        이렇게 수차례 환경을 이전하다 보면 소프트웨어의 버전이나 서버 설정의 차이로 인해 다양한 장애가 발생하기도 한다.
        이때, 컨테이너에 애플리케이션과 애플리케이션을 구동하는 환경을 그대로 담아서 환경을 이전하면, 
        장애 걱정 없이 신속하고 안정적으로 환경을 이전할 수 있다.

      ㄷ. 마이크로 서비스화 솔루션

        기업에서는 애플리케이션을 배포할 때 오랜 시간이 소요되거나, 작은 부분을 수정했을 뿐인데 애플리케이션 전체에 
        문제가 발생하는 것을 경험한다.
        
        이는 애플리케이션이 거대한 덩어리 처럼 구성되어 있기 때문인데, 이런 애플리케이션을 기능별로 나누어 변경과 조합이 
        가능한 것을 마이크로 서비스 라고 한다.
        
        마이크로 서비스를 컨테이너로 구성하면 애플리케이션을 기능 혹은 서비스 단위로 신속하게 배포 할수 있다.
        또한 컨테이너는 독립적인 구조이기 때문에 하나의 변경 사항이 다른 기능들에 영향을 미치지 않는다.

  왜 쿠버네티스 인가?

    1. 무중단(Fault Tolerance-FT) 서비스 제공

      때때로 서비스를 받는 사용자들은, 서비스 개선을 위해 서버점검 중이라는 안내문을 보게 된다.
      기업에서는 서버 업데이트를 위해서 사용자들이 잠든 새벽 시간을 활용하거나, 긴급 점검의 형태로 서비스를 일시 중단해 왔다.
      하지만, 쿠버네티스는 점진적 업데이트를 제공 하기 때문에 서비스를 중단 하지 않고도 서버를 업데이트 할수있다.
      또한, 쿠버네티스는 자가 회복 기능을 가지고 있어, 특정 컨테이너에 갑작스러운 장애가 발생하더라도 곧바로 
      복제 컨테이너 를 생성해서 서비스를 유지할수있다.

    2. Vendor Lock In 해결.


      고객이 A사의 클라우드를 사용하다가 I사의 클라우드로 환경을 이전하고 싶을 때, 제품간에 호환 문제가 발생하여 이전하기 어려운 상황을
      Vendor Lock In이라고 한다. 쿠버네티스는 도커 컨테이너 기반의 오픈 소스 이기 때문에, 
      사용자는 특정 업체에 종속되지 않기 클라우드를 이전 할수 있다.

 기본 개발 순서

 /***Cloud 기본 명령어***/

 활성 계정 리스트 : gcloud auth list
 프로젝트 ID : gcloud config list project

/***Docker 기본 명령어***/
 컨테이너 시작  : docker run "Image_Name"
   ex) docker run hello-world

 컨테이너 이미지 : docker image

 실행중인 컨테이너 확인 : docker ps
    -> 실행 완료한 컨테이너 까지 포함 : docker ps -a

  폴더 생성 및 이동 : mkdir "file_name" && cd "file_name"
    ex) mkdir test && cd test

  1. Dockerfile 생성, 이미지 생성 컨테이너 실행, GCR 게시

    /*예제*/
    -> 1. Docker File 만들기
      ex) cat > Dockerfile <<EOF
          # 기본 상위 이미지 지정, 이 경우 노드 버전 6의 공식 Docker이미지 설정
          FROM node:6

          # 컨테이너의 작업 디렉토리(현재)를 설정
          WORKDIR /app

          # 현재 디렉토리의 내용("."이 가리키는)을 컨테이너에 추가
          ADD . /app

          # 컨테이너 포트를 공개하여 해당 포트에서 연결을 허용
          EXPOSE 80

          # 마지막으로 node 명령어를 실행하여 응용프로그램 시작
          CMD ["node", "app.js"]
          EOF

    -> 2.노드 응용 프로그램 생성

      ex) cat > app.js <<EOF
          const http = require('http');

          const hostname = '0.0.0.0';
          const port = 80;

          const server = http.createServer((req, res) => {
              res.statusCode = 200;
                res.setHeader('Content-Type', 'text/plain');
                  res.end('Hello World\n');
          });

          server.listen(port, hostname, () => {
              console.log('Server running at http://%s:%s/', hostname, port);
          });

          process.on('SIGINT', function() {
              console.log('Caught interrupt signal and will exit');
              process.exit();
          });
          EOF

     -> 1,2를 이용한 이미지 생성 : docker build <옵션> <Dockerfile 경로>
        (데이터를 수정하면 이미지를 생성하고 실행 하여야 한다.)

        설명) docker build -t node-app:0.1 .
              ->  docker : docker 명령어 사용
                  build  : 이미지를 생성
                  -t     :(--tag=””)저장소 이름, 이미지 이름, 태그를 설정
                          <저장소 이름>/<이미지 이름>:<태그> 형식
                  node-app:0.1 : -t에 대한 이미지 이름
                  . : 디렉토리 주소(".""는 현재 디렉토리를 의미)

      -> 컨테이너 실행 : docker run <옵션> <이미지 이름, ID> <명령> <매개 변수>

         설명) docker run -p 4000:80 --name my-app node-app:0.1
               -> docker : docker 명령어 사용
                  run : 이미지를 기반으로 컨테이너 실행
                  -p : 포트 설정
                  4000:80 : -p에 대한 포트 번호
                  --name : 컨테이너 이름 설정
                  my-app : --name에 대한 컨테이너 이름
                  node-app:0.1 : 실행할 이미지 이름

                -추가 옵션
                  -d : detache 모드, 컨테이너가 백그라운드로 실행된다.

      -> 컨테이너 중지 및 제거 :
            -> 중지 : docker stop <컨테이너 이름 or 컨테이너 ID>
            -> 제거 : docker rm <컨테이너 이름 or 컨테이너 ID>

      -> 실행 로그 확인 : docker logs [container_id]

      -> 디버그 :
          docker logs -f [container_id] :  컨테이너가 실행 중일 때 로그 출력

          -> 배쉬 세션 시작 : docker exec -it [container_id] bash

          -> docker 메타 데이터 검사 : docker inspect [container_id]

      -> 게시

          정의 : 이미지를 Google 컨테이너 레지스트리(GCR)로 푸쉬 한다.

          1. gcr이 호스팅하는 비공개 레지스트리에 이미지를 푸시하려면 레지스트리 이름으로 이미지에 태그를 지정
              형식 : [hostname]/[project-id]/[image]:[tag]
              설명 :
              [hostname]= gcr.io
              [project-id]= 귀하의 프로젝트 ID (프로젝트 ID 찾기 : gcloud config list project)
              [image]= 귀하의 이미지 이름
              [tag]= 원하는 문자열 태그. 지정하지 않으면 기본값은 "latest"입니다.

          2. 태그 수정 : docker tag <옵션> <이미지 이름>:<태그> <저장소 주소, 사용자명>/<이미지 이름>:<태그>
              이미지에 태그를 설정하는 tag 명령어 이다.

             설명) docker tag node-app:0.2 gcr.io/[project-id]/node-app:0.2
                  docker : docker 명령어 실행
                  tag : 이미지 태그를 설정하는 명령어
                  node-app:0.2 : 이미지 이름 node-app:0.2의 태그를 아래의
                  gcr.io/[project-id]/node-app:0.2 : gcr.io/[project-id]/node-app:0.2로 변경

          3. 모든 컨테이너 중지 및 제거
                docker stop $(docker ps -q)
                docker rm $(docker ps -aq)

                -> node:6노드 이미지를 제거하기 전에 하위 이미지를 제거
                    docker rmi node-app:0.2 gcr.io/[project-id]/node-app node-app:0.1
                    docker rmi node:6
                    docker rmi $(docker images -aq) # remove remaining images
                    docker images

          4. 이미지를 pull 하여 실행 한다.
                    gcloud docker -- pull gcr.io/[project-id]/node-app:0.2
                    docker run -p 4000:80 -d gcr.io/[project-id]/node-app:0.2
                    curl http://localhost:4000

  2. 이미지 생성 ~ 쿠버네티스 생성

      ㄱ. Node.js 애플리케이션 생성

          server.js 파일 생성( vi server.js )
            var http = require('http');
            var handleRequest = function(request, response) {
            response.writeHead(200);
            response.end("Hello World!");
            }
            var www = http.createServer(handleRequest);
            www.listen(8080);

      ㄴ. Docker 컨테이너 이미지 생성

          -> 1.Dockerfile생성 ( vi dockerfile )
               FROM node:6.9.2
               EXPOSE 8080
               COPY server.js .
               CMD node server.js #이전에 수동으로 수행 한 것 처럼 노트 서버를 시작하시요

          -> 2.Docker 이미지 생성
               docker build -t gcr.io/PROJECT_ID/hello-node:v1 .

          -> 3.생성된 이미지 run 테스트
               docker run -d -p 8080:8080 gcr.io/PROJECT_ID/hello-node:v1

          -----테스트 완료 했다면---------

          -> 4. 컨테이너 실행중지

              -> docker ps 로 컨테이너 ID를 찾고
                 docker stop [Container ID]로 중지 시킨다.

      ㄷ. Google Container Registry 로 이미지 푸쉬
          -> 이미지가 의도한대로 작동했으므로 Google Cloud 프로젝트에서 액세스 할 수있는
            Docker 이미지의 비공개 저장소인 Google Container Registry 로 이미지를 푸시 한다.

          이 명령어를 사용하여 연결 세부 정보 섹션에 있는 Project_ID를 GCP Project_ID로 변경한다.  

          gcloud docker -- push gcr.io/PROJECT_ID/hello-node:v1

      ㄹ. push가 완료 됬다면 Navigation Menu > Container registry에 들어가 생성된 도커이미지를 확인 할수 있다.

  3. Cluster 만들기
      ->  쿠버네티스 엔진 클러스터를 만들수 있는 조건이 갖춰졌다.
          클러스터는 Google에서 호스팅하는 쿠버네티스 마스터 API서버와 일련의 작업자 노드로 구성된다.
          작업자 노드는 Compute Engine 가상 시스템이다.

          ㄱ. 프로젝트 설정 확인
              gcloud config set project [Project_ID]

          ㄴ. 두개의 n1-standard-1 node 클러스터를 만든다.
              gcloud container clusters create hello-world \
                --num-nodes 2 \
                --machine-type n1-standard-1 \
                --zone us-central1-a

                참고 : Kubernetes Engine > Kubernetes clusters > Create cluster 을 선택하여 콘솔을 통해 클러스터를 생성할수도 있다.

  4. Navigation menu > Kubernetes Engine을 선택하면 쿠버네티스 엔진으로 구동되는 완전 작동 쿠버네티스 클러스터가 있을을 확인 가능하다.

  ------------------------------------------ 여기 까지가 PODS와 Service를 생성할수 있는 기본 설정을 끝낸 것이다.---------------------------------------------------------------

  5. POD 만들기
     정의 : 쿠버네티스 POD는 관리 및 네트워킹 목적으로 함께 묶인 컨테이너 그룹입니다.
            단일 또는 다중 컨테이너를 포함 할 수 있다.
            현재 여기서는 개인 컨테이너 레지스트리에 저장된 Node.js 이미지로 빌드된 하나의 컨테이너를 사용한다.
            그것은 8080포트에서 콘텐츠를 제공한다.

            ㄱ. kubectl run명령어를 사용하여 창 만들기
                -input-
                kubectl run hello-node \
                      --image=gcr.io/PROJECT_ID/hello-node:v1 \
                      --port=8080

                -output-
                  deployment "hello-node" created

            ㄴ. 배포
                ㄱ에서 배포 객체를 만들었다. POD를 만들고 크기를 조정하는데 배포 객체가 권장된다.
                여기서 새 배포 객체는 hellow-node:v1 이미지를 실행하는 단일 POD 복제본을 관리한다.

                -> 배포를 보려면 kubectl get deployments 실행
                -> 배포로 만든 pod를 보려면 kubectl get pods를 실행

                참고
                kubectl cluster-info,kubectl config view  명령어는 cluster 상태를 변경하지 않으면 실해이 되지 않는다.
                (해결 명령어 : kubectl get events,kubectl logs <pod-name>)

  6. 외부 트래픽 허용
      정의: 기본적으로 POD는 클러스터 내의 내부 IP로만 액세스 할 수 있다.
            외부에서 쿠버네티스 가상 네트워크에 접 속하기 위해서 쿠버네티스 서비스로 POD를 expose 해주어야 한다.


            -> Cloud Shell kubectl expose 에서 --type="LoadBalancer"와 결합된 명령으로 창을 공개 인터넷에 노출 시킬수 있다.
              이 명령으로 외부에서 엑세스 할수 있는 IP작성하는데 필요하다.
              -- input --
              kubectl expose deployment hello-node --type="LoadBalancer"
              -- output --
              service "hello-node" exposed

            -> 공개적으로 액세스 할 수있는 서비스의 IP주소를 찾으려면 kubectl 모든 클러스터 서비스 리스트를 확인한다.
              명령어 : kubectl get services
                  외부 아이피 뿐 아니라 내부 아이피등 정보를 얻을수 있다.
            -> http://<EXTERNAL_IP>:8080로 서비스에 접근 가능하다.

  7. 서비스 확대
      정의 : Kubernetes가 제공하는 강력한 기능 중 하나는 응용 프로그램을 확장하는 것이 쉽다.
             갑자기 으용 프로그램에 더 많은 용량이 필요하다고 가정하였을 경우
             POD에 대한 복제본의 새로운 수를 관리 하도록 복제 컨트롤러에 지시 할수 있다.

            ->PODS 복제
              -- input --
              kubectl scale deployment hello-node --replicas=4
              -- output --
              deployment "hello-node" scaled

            -> 업데이트 된 배포 속성
              -- input --
              kubectl get deployment
              -- output --
              NAME         DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
              hello-node   4         4         4            4           16m

            -> 모든 창 나열
              -- input --
              kubectl get pods
              -- output --
              NAME                         READY     STATUS    RESTARTS   AGE
              hello-node-714049816-g4azy   1/1       Running   0          1m
              hello-node-714049816-rk0u6   1/1       Running   0          1m
              hello-node-714049816-sh812   1/1       Running   0          1m
              hello-node-714049816-ztzrb   1/1       Running   0          16m

  8. 서비스 업그레이드
      정의 : 어떤 시점에서 프로덕션 환경에 배포 한 응용 프로그램에는 버그 수정이나 추가 기능이 필요
             쿠버네티스는 사용자에게 영향을 주지 않고 새로운 버전을 프로덕션 환경에 배포 할 수 있도록 도와준다.

             -> server.js 수정 후 저장
             -> 수정된 새로운 컨테이너 이미지를 빌드 하고 버전업 하여 레지스트리에 게시할수 있다.

             docker build -t gcr.io/PROJECT_ID/hello-node:v2 . // 컨테이너 이미지 빌드 (v1 -> v2 :  버전업)
             gcloud docker -- push gcr.io/PROJECT_ID/hello-node:v2 // 레지스트리에 게시

             -> 쿠버네티스는 원활하게 복제 컨트롤럴를 새 버전의 응용 프로그램으로 업데이트 한다.
                ex) 이미지 레이블을 변경한다면
                  kubectl edit deployment hello-node를 열어
                  spec.template.spec.containers.image를 수정한다.

                  내용 수정후
                  kubectl get deployments 명령어를 사용하여 배포를 업데이트 한다.
                  (새 이미지로 새 창을 만들고 기존 창을 삭제 한다.)

  9. 그래픽 대시 보드(선택 단원)
      정의 :  그래픽 대시 보드를 사용하여 신속하게 사용 가능하고
              CLI에 있는 일부 기능을 시스템에 보다 쉽게 접근 할 수 있고
              발견 할수 있는 방법으로 사용할수있다.

            ㄱ.그래픽 대시 보드르 사용할려면 클러스터 수준 권한을 부여해야 한다.

              kubectl create clusterrolebinding cluster-admin-binding --clusterrole=cluster-admin --user=$(gcloud config get-value account)

            ㄴ. 적절한 권한이 설정 되었으면 다음 명령을 실해앟여 새 대시 보드 서비스를 만든다.

              kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml

            ㄷ. yaml 대시 보드 서비스의 표현을 수정한다.(대시 보드 형식으로 설정파일 수정)

              kubectl -n kube-system edit service kubernetes-dashboard
              에서 type:ClusterIP, type:NodePort 로 변경한다.

            ㄹ. 쿠버네티스 대시 보드에 로그인 하려면 토큰을 사용하여 인증해야 한다.
                namespace-controller와 같은 서비스 계정에 할당된 토큰을 사용하여야 한다.

                -- input 토큰 값을 받는다.(공백도 포함 하여야 한다.) --
                kubectl -n kube-system describe $(kubectl -n kube-system \
                get secret -n kube-system -o name | grep namespace) | grep token:

            ㅁ 토큰을 복사하여 쿠버네티스 대시보드에 들어가 다음 명령어를 실행하여 연결을 연다
                -- input --
                kubectl proxy --port 8081

            ㅂ Cloud Shell 웹 미리보기 기능을 사용하여 포트를 8081로 변경한다.

            ㅅ 이후
            https://8081-dot-5177448-dot-devshell.appspot.com/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#!/overview?namespace=default
            와 비슷한 주소로 이동후 토큰 입력을 하면 그래픽 대시보드를 사용가능하다.

            -- 쿠버네티스와 클라우드 조율--
            목표 : Kubernetes Engine을 사용하여 완전한 Kubernetes 클러스터를 제공
                  kubectl을 사용하여 Docker 컨테이너를 배포하고 관리
                  Kubernetes의 배포 및 서비스를 사용하여 응용 프로그램을 마이크로 서비스로 전환
  1. 기본 셋팅
        -> 클라우드 쉘 환경에서 다음 명령을 실행하여 영역을 설정
          gcloud config set compute/zone us-central1-b

        -> 영역 설정후 클러스터를 시작한다.
          gcloud container clusters create io

        -> 샘플 코드 얻기
          git clone https://github.com/googlecodelabs/orchestrate-with-kubernetes.git

          폴더 이동
          cd orchestrate-with-kubernetes/kubernetes

  2. Quick 쿠버네티스 데모
        ->쿠버네티스를 시작하는 가장 쉬운 방법은 kubectl run 명령어를 사용하는 것이다.
          kubectl run을 사용하여 nginx컨테이너의 단일 인스턴스를 시작한다.
          -- input --
          kubectl run nginx --image=nginx:1.10.0

        ->실행중인 nginx 컨테이너를 확인한다( 쿠버네티스 에서는 모든 컨테이너가 PODS에서 실행한다.)
          -- input --
          kubectl get pods

        -> nginx 컨테이너가 실행되면 쿠버네티스 expose명령어를 사용하여 노출 시킬수 있다.
          -- input --
          kubectl expose deployment nginx --port 80 --type LoadBalancer

        -> 사용중인 서비스 리스트 확인
          -- input --
          kubectl get services

  3. PODS 만들기
    정의 : PODS는 하나이상의 컨테이너 컬랙션을 나타내고 보유 한다.
          일반적으로 서로에 대한 의존성이 강한 여러 컨테이너가 있는 경우 컨테이너를 하나의 창안에 패키지 한다.

        PODS 만들기
          (PODS는 PODS구성 파일을 사용하여 만들수 있다.)

          -> cat pods/monolith.yaml
              (구성파일 출력)
          -> kubectl create -f pods/monolith.yaml
              (monolith PODS 생성)

          -> kubectl get pods
              (검사)

          -> kubectl describe pods monolith
              (설명 출력)

  4. PODS 와 상호 작용
      정의 : 기본적으로 PODS는 사설 IP주소가 할당되며 클러스터 외부에 도달 할수 없다.
              이떄 kubectl port-forward명령을 사용하여 로컬 포트를 모노리스 창안의 포트에 매핑 한다.

            -> 2개의 Cloud Shell 터미널을 연다.
                하나는 kubectl port-forward 명령을 실행 하고
                다른 하나는 curl 명령을 실행 한다.

            -> kubectl port-forward monolith 10080:80
                  제 2 터미널에서, 포트 포워딩을 설정 한다.

            -> curl http://127.0.0.1:10080
                  첫 번째 터미널에서 PODS와 연결을 한다.

            ------- 이제 이 CURL 명령을 사용하여 보안 엔드 포인트에 도달했을때 어떤일이 발생하는지 확인한다.

            -> curl http://127.0.0.1:10080/secure

            -> monolith에서 인증 토큰을 다시 얻으려면 로그인을 해야한다.

            -> 로그인 프로프트에서 초기 암호 "password"를 사용하여 로그인 한다.

            -> TOKEN=$(curl http://127.0.0.1:10080/login -u user|jq -r '.token')
                로그인 하면 JWT 토큰이 인쇄되고. 클라우드 쉘은 기 문자열 복사를 제대로 처리 하지 않으므로 토큰에 대한 환경변수를 만든다.

            -> curl -H "Authorization: Bearer $TOKEN" http://127.0.0.1:10080/secure
                토큰을 복사한 후 토큰을 사용하여 보안 엔드 포인트에 도달 하려면 위의 명령어를 사용한다.

            -> kubectl logs monolith
                monolith 로그를 본다.

            -> kubectl logs -f monolith
                3번쨰 터미널을 열고 -f 플래그를 사용하여 실시간으로 일어나는 로그 스트림을 가져온다.

            -> curl http://127.0.0.1:10080
                이제 curl 명령어로 제1 터미널에서도 상호 작용할수 있다.

            -> kubectl exec monolith --stdin --tty -c monolith /bin/sh
                kubectl exec을 사용하여 Monolith Pod에서 대화형 셀을 실행한다.
                이는 컨테이너 내에서 문제를 해결할때 유용하다.
                ex) 예를 들어 모노리스 컨테이너에 셸이 있으면
                    다음 ping명령을 사용하여 외부 연결을 테스트 할 수 있습니다 .

                    ping -c 3 google.com

            -> exit
                사용 종료 명령어

  5. 서비스(로드벨런스)
      정의: PODS는 영구적인게 아니다. 다양한 원인으로 중단 될수 잇다.
            일련의 PODS와 통신하고 싶을때 다시 시작시 IP주소가 다를수있다.
            서비스가 들어오는 시점에 PODS는 안정적인 종점을 제공한다.

            서비스가 PODS집합에 제공하는 액세스 수준은 서비스 유형에 따라 다르다
              -> ClusterIP (내부) - 기본 유형은 서비스가 클러스터 내부에서만 볼 수 있음을 의미한다
              -> NodePort - 클러스터의 각 노드에 외부에서 액세스 할 수있는 IP를 제공한다.
              -> LoadBalancer - 클라우드 제공 업체의로드 밸런서를 추가합니다.로드 밸런서는 서비스의 트래픽을 노드로 전달합니다.

          --- 서비스 만들기 ---
                * 서비스를 만들기 전에 https 트래픽을 처리 할 수 있는 보안 PODS를 만들어 보겠습니다.

                -> kubectl create secret generic tls-certs --from-file tls/
                -> kubectl create configmap nginx-proxy-conf --from-file nginx/proxy.conf
                -> kubectl create -f pods/secure-monolith.yaml

            -> cd ~/orchestrate-with-kubernetes/kubernetes
            -> cat pods/secure-monolith.yaml
                보안 monolith 및 해당 구성 데이터 생성

                -- output --
                kind: Service
                apiVersion: v1
                metadata:
                  name: "monolith"
                spec:
                  selector:
                    app: "monolith"
                    secure: "enabled"
                  ports:
                    - protocol: "TCP"
                      port: 443
                      targetPort: 443
                      nodePort: 31000
                  type: NodePort
                주의 사항 :
                 1. 선택기는 자동으로 "pod = monolith"및 "secure = enabled"레이블이있는 모든 꼬투리를 찾고 노출하는 데 사용됩니다.
                 2. 이제 우리는 포트 31000에서 nginx (포트 443)로 외부 트래픽을 전달하는 방법이므로 여기에서 노드 포트를 노출해야합니다.

            -> kubectl create -f services/monolith.yaml
                kubectl create모노리스 서비스 구성 파일에서 모노리스 서비스를 생성 하려면 위의 명령어를 실행한다.

            -> 포트를 사용하여 서비스를 노출 하고 있습니다. 즉 다른 앱이 서버중 하나의 포트 31000에 바인딩 하려고 하면 port 충돌이 일어 날수 있다.
                일반적으로 쿠버네티스는 이 포트 지정을 처리한다. 이 실습에서는 나중에 포트 상태 검사를 구성하는 것이 더 쉽도록 포트를 선택했다.

            -> gcloud compute firewall-rules노출 된 노드 포트의 모노리스 서비스에 대한 트래픽을 허용 하려면 다음 명령을 사용하시요.    
            gcloud compute firewall-rules create allow-monolith-nodeport \ --allow=tcp:31000

            -> 모든것이 설정 되어 있으므로 포트 전달을 사용하지 않고 클러스터 외부에서 보안 일체형 서비스에 접근 할수 있어야한다.

            -> 먼저 노드중 하나에 대한 외부 IP주소를 가져온다.
                gcloud compute instances list
            -> 이제 curl다음을 사용하여 보안 -단일체 서비스를 시도해본다.
                curl -k https://<EXTERNAL_IP>:31000

            --> ERROR 타임 초과 에러!!!!
                라벨 설정 오류로 인한 에러

            -> 에러가 발생한 이유는 현재 monolith 서비스에는 끝점이 없다.
                이와 같은 문제를 해결하기 위해 kubectl get pods는 레이블 쿼리와 함께 명령어를 사용한다.

                kubectl get pods -l "app=monolith,secure=enabled"

            -> kubectl label명령을 사용하여 누락 된 secure=enabled레이블을 보안 일체형 PODS 에 추가합니다

                  kubectl label pods secure-monolith 'secure=enabled'
                  kubectl get pods secure-monolith --show-labels

            -> 이제 우리 PODS에 올바르게 레이블이 지정되었으므로, monolith 서비스에서 끝점 목록을 봅니다.

                  kubectl describe services monolith | grep Endpoints

            -> 다시 접속을 시작하면 접속이 완료 된다.

                  gcloud compute instances list
                  curl -k https://<EXTERNAL_IP>:31000

  6. 배포 만들기
      설명 : 우리는 monolith 앱을 세가지 별도의 part로 나눌것이다.

        auth - 인증 된 사용자에 대해 JWT 토큰을 생성합니다.
        hello - Greet 인증된 사용자.
        frontend - 트래픽을 auth 및 hello 서비스로 라우팅합니다.

        각 서비스 마다 하나씩 배포를 만들 준비가 되었다.
        그런 다음, frontend 배포를 위한 외부 서비스 및 auth 및 hello 배포를위한 내부 서비스를 정의합니다.
        완료되면 Monolith와 마찬가지로 마이크로 서비스와 상호 작용할 수있게되며 이제는 각 part을 개별적으로 확장 및 배포 할 수있게됩니다!

        -> 인증 배포 구성 파일을 검토하여 시작 한다.

            cat deployments/auth.yaml

            출력된 데이터를 확인후 시작
            배포 되면 복제본이 생성되며 버전 1.0.0의 인증 컨테이너를 사용하고 있다.

        -> 배포 객체 생성
            kubectl create 명령을 실행하여 인증 배포를 생성하면 배포 매니페스트의 데이터를 준수하는 하나의 PODS가 생성 된다.
            즉, 복제본 필드에 지정된 번호를 변경하여 포드의 수를 조정할수있다.

            kubectl create -f deployments/auth.yaml

        -> 인증 배포 서비스 생성

            kubectl create -f services/auth.yaml

        -> 이제 hello 배포를 만들고 노출 하려면 하단 명령어 실행

            kubectl create -f deployments/hello.yaml
            kubectl create -f services/hello.yaml

        -> 프론트 엔드 배포를 만들고 노출한다.

            kubectl create configmap nginx-frontend-conf --from-file=nginx/frontend.conf
            kubectl create -f deployments/frontend.yaml
            kubectl create -f services/frontend.yaml

        -> 프론트 엔드와 인터랙트 하여 외부 ip잡아서 CURL 한다.

            kubectl get services frontend
            curl -k https://<EXTERNAL-IP>
=======
      고객이 A사의 클라우드를 사용하다가 I사의 클라우드로 환경을 이전하고 싶을 때, 제품간에 호환 문제가 발생하여 이전하기 
      어려운 상황을 Vendor Lock In이라고 한다. 쿠버네티스는 도커 컨테이너 기반의 오픈 소스 이기 때문에, 
      사용자는 특정 업체에 종속되지 않기 클라우드를 이전 할수 있다.
>>>>>>> d9270a00641123c01b12912eb49edb6309c87414
