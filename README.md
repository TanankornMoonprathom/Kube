## spcn01 
## Kubernetes In Windows

## Wakatime
https://wakatime.com/@spcn01/projects/syzhwptxjl

## 1. Install Kubectl
   - Ref 
    - https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/

   - download Kubectl.exe to path want

      ```
      curl.exe -LO "https://dl.k8s.io/release/v1.26.0/bin/windows/amd64/kubectl.exe"
      ``` 
   - Add Path to environment variable
      - Search environment
  
        ![image](https://user-images.githubusercontent.com/119097663/224904080-a7de4fcd-c43d-4760-b483-0734aaeca796.png)


      - Click Environment Variables...

        ![image](https://user-images.githubusercontent.com/119097663/224904504-ac4bb0b8-4a35-4ddd-87c0-d0f665c86d04.png)

       - Select Path Click Edit

        ![image](https://user-images.githubusercontent.com/119097663/224904590-64c1e452-efae-41f9-861e-409f9e9b9e78.png)

       - Click New
        
        ![image](https://user-images.githubusercontent.com/119097663/224904653-d6231336-cf6a-4280-bdba-2e72043c5a5c.png)

      - Add Path that have kubectl.exe
      - Click OK
  
    - Test Kubectl enable in command
      ```
      kubectl version --client
      ```

## 2. Install minikube
   - Ref
    - https://minikube.sigs.k8s.io/docs/start/

    - download minikube.exe

      ```ruby
      New-Item -Path 'c:<path want to install>' -Name 'minikube' -ItemType Directory -Force #create folder minikube
      Invoke-WebRequest -OutFile 'c:<path want to install>\minikube\minikube.exe' -Uri 'https://github.com/kubernetes/minikube/releases/latest/download/minikube-windows-amd64.exe' -UseBasicParsing #download install to path
      ```

    - Add Path to environment variable
      ```ruby
      $oldPath = [Environment]::GetEnvironmentVariable('Path', [EnvironmentVariableTarget]::Machine)
      if ($oldPath.Split(';') -inotcontains 'C:<path folder minikube.exe>'){ `
      [Environment]::SetEnvironmentVariable('Path', $('{0};C:<path folder minikube.exe>' -f $oldPath), [EnvironmentVariableTarget]::Machine) `
      }
      ```
    - Restart Terminal

## 3. Install Docker Desktop
   - Ref
    - https://docs.docker.com/desktop/install/windows-install/

## Test minikube start
1. Start a cluster using the docker driver
   ```ruby
   minikube start --driver=docker
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224906660-5f08fbf8-5503-44e7-bb24-05a45ade8ab6.png)

2. Run with open dashboard
   ```ruby
   minikube dashboard
   ```
   ![image](https://user-images.githubusercontent.com/119097663/225030868-71ccdda7-bb69-4287-802b-5111ab70fe0f.png)

3. Test services
   ```ruby
   minikube service hello-minikube
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224907641-f32599e8-afd0-4a9e-8bf5-f8a59c476752.png)

4. Test Stop minikube
   ```ruby
   minikube pause
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224907200-c1758b1c-03a8-40b2-9d5d-258644100325.png)

## 3. Install traefik
      1. Install Traefik Resource Definitions
    ```
    kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-definition-v1.yml
    ```
    ![image](https://user-images.githubusercontent.com/119097663/226110351-c7723d93-8ae9-4f29-889f-9ed8690b1473.png)

      2. Install RBAC for Traefik
   ```
   kubectl apply -f https://raw.githubusercontent.com/traefik/traefik/v2.9/docs/content/reference/dynamic-configuration/kubernetes-crd-rbac.yml
   ```
    ![image](https://user-images.githubusercontent.com/119097663/226110502-6a296779-962a-40df-b759-3edd801cda8f.png) 

      3. Install Traefik Helmchart
    ```
    helm repo add traefik https://traefik.github.io/charts 
    helm repo update 
    helm install traefik traefik/traefik 
    ```
    ![image](https://user-images.githubusercontent.com/119097663/226110649-5b8ae072-6e3f-42b6-b231-a57d28ed1fe1.png) 

    4. Verify service is running
    ```
    kubectl get svc -l app.kubernetes.io/name=traefik
    kubectl get po -l app.kubernetes.io/name=traefik
    ```
    ![image](https://user-images.githubusercontent.com/119097663/226110849-021d582a-9f75-4685-94c1-2b1569d90ec5.png)

    5. copy user in dashboard-secret place it at user in traefik-dashboard

    ![image](https://user-images.githubusercontent.com/119097663/226111225-d3332af2-4db6-49b1-8a8f-43e3b769609f.png)

    ![image](https://user-images.githubusercontent.com/119097663/226111244-a7ec1e11-8f01-4070-88ba-0c7a88f83cc1.png)

    6. Deploy
      ```
      kubectl apply -f . 
      ```
      ![image](https://user-images.githubusercontent.com/119097663/226111342-4fa25c0d-bdf7-4beb-95fb-dc99e68fc341.png)

## Result

## 1. dashboard

![image](https://user-images.githubusercontent.com/119097663/226111510-05b6c0ae-3697-4131-9046-29b128c18153.png)

## 2. https://traefik.spcn01.local/dashboard/#/http/routers

![image](https://user-images.githubusercontent.com/119097663/226111614-134d01a9-e803-4659-8d65-8929cb80d2a2.png)

## 5. http://web.spcn01.local/

![image](https://user-images.githubusercontent.com/119097663/226111754-5f76adc7-2ad2-4eab-bcad-f3f2e19de680.png)

