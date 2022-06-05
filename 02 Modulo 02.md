# Modulo 02 - Gerenciamento Domínios, Usuários, Grupos, Recursos e Licenças.

# POwerShell
https://docs.microsoft.com/en-us/powershell/module/msonline/get-msoldomain?view=azureadps-1.0

# Domínios

# Importe Modulos
Import-Module MSOnline
<br>Import-Module AzureAD
<br>Import-Module AzureADPreview
<br>connect-msolservice

# Criar um Domínio 
New-MsolDomain -Name contoso.com.br
<br>New-MsolDomain –Authentication Managed –Name contoso.com.br

# Consulta Domínio
Get-MsolDomain
<br>Get-MsolDomain -Status Verified
<br>Get-MsolDomainVerificationDns –DomainName contoso.com.br –Mode DnsTxtRecord

# Confimar Domínio
Confirm-MsolEmailVerifiedDomain -DomainName contoso.com.br

# Remover Domínio
Remove-MsolDomain -DomainName contoso.com.br -Force

# Usuários

# Consultar Usuários
<br>Get-MsolUser

# Criar Usuário
<br>New-MsolUser -UserPrincipalName "userxx@contoso.com.br" -DisplayName "User XX" -FirstName "Userxx" -LastName "XX"

# Remover Usuário
<br>Remove-MsolUser -UserPrincipalName "userxx@contoso.com.br"
