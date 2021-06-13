# Considerações iniciais

Foi identificado que o projeto trata é uma aplicação http com runtime ASP.NET 3.1.

A aplicação não faz nenhum tipo de comunicação com banco de dados(relacional, não relacional ou cache) ou com outra aplicação.

Qual é a locadidade dos usuários que vão acessar a app ?  Escolher o mais próximo possível.


# Configurando repositório GIT

## Branch dev.

- [x] Criar a branch
- [x] Proteger a branch
  - [x] Apenas pull request com code review
  - [x] Configurar CODEOWNER
  - [x] Requer verificação de status antes do merge
    - [x] Teste unitário    
- [x] Code review template/checklist

## Branch prod(master)
- [x] Criar a branch
- [x] Proteger a branch
  - [x] Apenas pull request com code review
  - [x] Configurar CODEOWNER
  - [x] Requer verificação de status antes do merge
    - [x] Teste unitário
- [x] Code review template/checklist


# Definindo o serviço Azure

Baseado nas considerações iniciais e padrões identificados no projeto foi escolhido Azure App service para fazer o deploy da aplicação.

## Azure App Service

Azure App service possibilita fazer o host/deploy da aplicação sem se preocupar com a infraestrutura. O serviço oferece alta disponibilidade e auto escalonamento da aplicação. Integração com deployments automáticos com GitHub, Azure Devops, entre outras.

* É possível rodar containers
* Escalonamento da aplicação automática ou manual
  

## Azure Virtual Machines com Scale Sets

É utilizado Azure Virtual Machines quando é necessário algum controle sobre o sistema operacional. Da camada sistema operacional até o software é de responsabilidade da equipe. Inclusive o gerencimento do escalonamento e garantia de alta disponibilidade da aplicação de acordo com o tráfego, scale sets auxiliam nessa tarefa.

Fazer o setup da infra para 2 ambientes(prod e test) levará mais tempo se comparado ao Azure App Service.

## Conteiners e Azure Kubernetes Service (AKS)

Nesse momento a aplicação não está containerizada. São opções para o futuro.

## Azure functions (serverless)



# Configuração do ambiente Azure App

Uma das primeiras coisas a se considerar em um ambiente Aure App é [App Service Plan](https://azure.microsoft.com/en-us/pricing/details/app-service/windows/#pricing). Linux ou Windows ? Dev ou Prod ? Número de instâncias ? Computação compartilhada, dedicada ou isolada ?

Seguindo a documentação/recomendação da Azure:  
* Ambiente Dev - mínimo plano básico
* Ambiente Prod - mínimo plano standard

Em cada plano temos diferentes tipos de máquina com configurações de hardware. E seus respectivos preços.


## Dev
- [x] criar resource group
- [x] criar App Service plan do tipo básico
- [x] criar App service  
- [ ] criar terraform 
## Prod
- [x] criar resource group
- [x] criar App Service plan do tipo standard
- [x] criar App service  
- [ ] criar terraform

# CI/CD

## Dev
No ambiente teremos apenas um 


- [x] connectar com o repo GitHub no Deployment Center
- [x] Configurar o github actions
  - [x] Push -> Build e deploy para o App Service
  - [x] Pull request -> Unit test
## Prod
- [x] connectar com o repo GitHub no Deployment Center
- [x] Configurar o github actions
  - [x] Pull request -> Unit test
  - [x] Tag -> Build e deploy para o App Service



# Funcionalidade Health check

- [x] [Adicionar endpoint](https://docs.microsoft.com/en-us/aspnet/core/host-and-deploy/health-checks?view=aspnetcore-3.1)
- [x] Configurar health check no Azure App Services
- [] Alarme

# Issues

## Unit test
O unit test não passa 100% e impede o merge do pull request. Já que foi configurado Status check.

- [X] Tests.XUnit
  - [x] fixed ByAlphabeticalOrder.cs [reference](https://github.com/dotnet/samples/blob/main/csharp/unit-testing/XUnit.TestProject/ByAlphabeticalOrder.cs)
- [x] Tests.MSTest
  - [x] fixed ByAlphabeticalOrder.cs