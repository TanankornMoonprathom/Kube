## spcn01 
## Kubernetes In Windows

1. Install Kubectl

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

2. Install minikube
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

3. Install Docker Desktop
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
   ![image](https://user-images.githubusercontent.com/119097663/224907200-c1758b1c-03a8-40b2-9d5d-258644100325.png)

3. Test services
   ```ruby
   minikube service hello-minikube
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224907641-f32599e8-afd0-4a9e-8bf5-f8a59c476752.png)

4. Test Stop minikube
   ```ruby
   minikube pause
   ```
   ![image](https://user-images.githubusercontent.com/119097663/224907641-f32599e8-afd0-4a9e-8bf5-f8a59c476752.png)





