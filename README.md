## spcn01 
## Kubernetes

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
  
    - Test Kubectl enable 
      ```
      kubectl version --client
      ```
