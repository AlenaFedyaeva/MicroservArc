# MicroservArc

Плагины:
Kubcolor - для консоли


1. export KUBECONFIG=kubernetes-gb_kubeconfig.yaml

2. kubectl get node

3. kubectl create/apply/delete        -f   /home/alena/Workspace/MicroservArch/lesson_repo/geekbrains-conteinerization/practice/3.kubernetes-intro/pod.yaml

Удалить все поды и сервисы в пространстве имен my-ns
kubectl -n my-ns delete pod,svc --all                                    

4. kubectl get pod (получим список имен подов)
 kubectl get pods --all-namespaces (поды во всех namespaces)

5. проксируем и можно смотреть на localhost:8888 nginx
 
 kubectl port-forward pod-name    [port localhost'a]:[port Pod'a]
 kubectl port-forward my-pod-name         	8888:80 


6. logs
kubectl logs my-pod

7. зайти внутрь контейнера в pod
kubectl exec -it my-pod bash

8. обновить текущий ПОД и сделать apply 
kubectl create/apply/delete        -f /home/alena/Workspace/MicroservArch/lesson_repo/geekbrains-conteinerization/practice/3.kubernetes-intro/pod.yaml

9. Получить информацию об обьекте
kubectl describe po my-pod

10. СМЕНА ПАРАМЕТРОВ НАЛЕТУ
kubectl edit po my-pod


11. Просмотр подов
kubectl get po

Просмотр реплика сетов
kubectl get rs


12. проссмотр меток
kubectl get po --show-labels

kubectl get po --show-labels

13.создаем Namespace   
kubectl create ns text

14. Теперь в Namespace создадим POD
kubectl apply -f pod.yaml -n test

15. теперь посмотрим Po
kubectl get po  

16. создаем deployment
 kubectl create -f deployment.yaml 


17. cчитать поды
 kubectl get po|wc -l

18. отобразить labels
 kubectl get po --show-labels

19. прмерт удаления репликасета через yaml (можно через имя обьекта)
kubectl delete -f replicaset.yaml
kubectl get rs  //проверяем что удалилось

20. Просмотр репликасета (их кол-во меняется после деплоя)
kubectl get rs
kubectl describe rs my-deployment-76499ffb7 

21. Просмотр историй деплоя
kubectl rollout history deploy my-deployment 

22. просмотр информации о POD  в формате yaml
kubectl get po my-deployment-6467646bf7-7prsw -o yaml

23. Откат деплоя на предыдущую версию
kubectl rollout undo deploy my-deployment

24. Просмотр событий Event (все события в кластере без привязки к Nod'e)
kubctl get events

25. Prometeus :  ресурсы и потребление  (metrics server ставим на kubernates)
kubctl top po
kubctl top no

26. QoS / quality of service for resources(какие узлы(pod) когда выселяются)
guaranty - request=limit (выселяется в последнюю очередь)
best effor resoureses/limits - не указаны (выселяется в первую очередь)
middle/средний -  resouses<limit (выселяются вторыми перед Guaranted)

27. Secret (from pair)

просмотр списка секретов:
kubectl get secret

просмотр секрета yaml
kubectl get secret my-secret -oyaml

kubectl create secret generic my-secret --from-literal=key1=supersecret --from-literal=pass=topsecret

kubectl create secret generic my-secret --from-literal=pass=supersecret

27) how to decode pass from secret: (берем зашифрованный пароль из kubectl get secret my-secret -oyaml)
echo "c3VwZXJzZWNyZXQ=" | base64 -d

28) Check ENV in pod
kubectl exec -it [pod name ] env
kubectl exec -it my-deployment-6b966b985b-fqdfp env
