# Modulo 02 - Gerenciamento Domínios, Usuários, Grupos, Recursos e Licenças.

# Consultas Propagação DNS
https://www.digwebinterface.com/

# PowerShell
https://docs.microsoft.com/en-us/powershell/module/msonline/get-msoldomain?view=azureadps-1.0

# Importe Modulos
Import-Module MSOnline
<br>Import-Module AzureAD
<br>Import-Module AzureADPreview
<br>connect-msolservice

# Gerenciamento Domínios

#Criar um Domínio 
<br>New-MsolDomain -Name contoso.com.br
<br>New-MsolDomain –Authentication Managed –Name contoso.com.br

#Consulta Domínio
Get-MsolDomain
<br>Get-MsolDomain -Status Verified
<br>Get-MsolDomainVerificationDns –DomainName contoso.com.br –Mode DnsTxtRecord

#Confimar Domínio
<br>Confirm-MsolEmailVerifiedDomain -DomainName contoso.com.br

#Remover Domínio
<br>Remove-MsolDomain -DomainName contoso.com.br -Force

# Gerenciamento Usuários

#Consultar Usuários
<br>Get-MsolUser

#Criar Usuário
<br>New-MsolUser -UserPrincipalName "userxx@contoso.com.br" -DisplayName "User XX" -FirstName "Userxx" -LastName "XX"

#Remover Usuário
<br>Remove-MsolUser -UserPrincipalName "userxx@contoso.com.br"
