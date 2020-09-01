GCP에 쿠버네티스 설치 및 실행
1. GCP 계정 생성 
2. project 생성 
  이름 : cndgud-gke-test-20200901
3. Kubernetes Engine -> 클러스터 ->클러스터 만들기
  *처음 클러스터를 만드는 경우 "클러스터 만들기" 가 활성화 될때까지 시간이 걸림
4. 클러스터 설정
  4-1. 클러스터 기본사항
    영역 : asia-northeast-3
  4-2. 노드풀 (    default-pool )
    크기 노드수 :3
5. 클러스터 연결
5-1. CloudShell에서 실행
5-2. kubectl 명령줄 액세스 구성(자동으로 입력됨 엔터만 치면됨)
gcloud container clusters get-credentials cluster-1 --zone asia-northeast3-a --project cnd
gud-gke-test-2020901-288213
6. 간단한 서비스 배포
6-1. 노드 확인
kubectl get nodes

6-2. run?
kubectl run nginx --image=nginx 

-------------------------
*ISSUE : run만 하는 경우 6-4 expose를 하면 Error from server (NotFound): deployments.extensions "nginx" not found
*해결 : https://github.com/ivanfioravanti/kubernetes-the-hard-way-on-azure/issues/31
6-3. deployment 생성
*문제 :  run 
![image](https://user-images.githubusercontent.com/39398450/91866246-42a79e00-ecad-11ea-9057-18ddef0be24e.png)

---------------------------------------------------
6-3. deployment 생성
kubectl create deployment nginx --image=nginx
6-4. expose
kubectl expose deployment "nginx" --port=80 --type=LoadBalancer
