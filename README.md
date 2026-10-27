# .github-workflows-deploy-azure-vm.yml
name: Executar em VM Windows no GitHub

on:
  push:
    branches: [ main ]
  workflow_dispatch:

jobs:
  build-on-windows-vm:
    runs-on: windows-latest  # Aqui o GitHub aloca uma VM Windows automaticamente para você

    steps:
      - name: Checkout do Repositório
        uses: actions/checkout@v4

      - name: Testar Versão do PowerShell e Sistema
        shell: pwsh
        run: |
          Write-Host "Sistema Operacional:"
          Get-ComputerInfo | Select-Object OsName, OsVersion
          
          Write-Host "Versão do PowerShell:"
          $PSVersionTable.PSVersion

      - name: Exemplo de comando na VM (Instalar algo com Chocolatey)
        shell: pwsh
        run: |
          choco install 7zip -y
          Write-Host "Ferramentas instaladas com sucesso na VM do GitHub!"
