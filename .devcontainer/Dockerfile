FROM mcr.microsoft.com/devcontainers/universal:linux

# Azure CLI latest
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash

# PowerShell latest
RUN sudo apt-get update && sudo apt-get install -y wget apt-transport-https software-properties-common && wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb" && sudo dpkg -i packages-microsoft-prod.deb && sudo apt-get update && sudo apt-get install -y powershell

# Bicep for PowerShell
RUN curl -Lo bicep https://github.com/Azure/bicep/releases/latest/download/bicep-linux-x64 && chmod +x ./bicep && sudo mv ./bicep /usr/local/bin/bicep

# Azure Functions Core Tools v4
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg && sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg && sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-ubuntu-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list' && sudo apt-get update && sudo apt-get install azure-functions-core-tools-4

# PowerShell Modules
RUN pwsh -Command Set-PSRepository -Name PSGallery -InstallationPolicy Trusted && \
    pwsh -Command Install-Module -Name Az -Scope AllUsers -Repository PSGallery && \
    pwsh -Command Install-Module -Name Az.ResourceGraph -Scope AllUsers -Repository PSGallery && \
    pwsh -Command Install-Module -Name Pester -Scope AllUsers -Repository PSGallery && \
    pwsh -Command Set-PSRepository -Name PSGallery -InstallationPolicy Untrusted

CMD [ "pwsh" ]