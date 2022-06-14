# Modulo 4 - Exchange Online

#Links Documentações
<br>https://docs.microsoft.com/pt-br/powershell/exchange/?view=exchange-ps
<br>https://docs.microsoft.com/pt-br/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits
<br>https://docs.microsoft.com/pt-br/microsoft-365/compliance/unlimited-archiving?view=o365-worldwide
<br>https://docs.microsoft.com/pt-br/office365/servicedescriptions/exchange-online-archiving-service-description/exchange-online-archiving-service-description#unlimited-archive-storage-quota
<br>https://docs.microsoft.com/da-dk/exchange/troubleshoot/configure-mailboxes/set-automatic-replies
<br>https://docs.microsoft.com/pt-br/microsoft-365/compliance/use-network-upload-to-import-pst-files?view=o365-worldwide
<br>https://dicasdeinfra.com.br/13-comandos-obrigatorios-do-microsoft-365-powershell/#
<br>https://www.codetwo.com/blog/mailbox-backup-options-across-available-office-365-plans/
<br>https://docs.microsoft.com/pt-br/exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes
<br>https://docs.microsoft.com/pt-br/microsoft-365/enterprise/use-powershell-to-perform-an-imap-migration-to-microsoft-365?view=o365-worldwide
<br>https://docs.microsoft.com/pt-br/Exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes?redirectSourcePath=%252farticle%252fWhat-you-need-to-know-about-migrating-your-IMAP-mailboxes-to-Office-365-3fe19996-29bc-4879-aab9-5a622b2f1481
<br>https://docs.microsoft.com/pt-br/exchange/mailbox-migration/office-365-migration-best-practices

# Tipos de Migração do Exchange Online 

![image](https://user-images.githubusercontent.com/49683486/173575591-de85ae98-bbf1-42de-8dee-ea3d80350abf.png)

# Fluxo de lotes para migrações  do Exchange Online 

![image](https://user-images.githubusercontent.com/49683486/173575962-8404f9a6-3689-4ce2-b5c6-47e163fc3582.png)

# Topologia dos Portais Exchange Online e Segurança

![image](https://user-images.githubusercontent.com/49683486/173577767-5db15ca7-06aa-44dd-a9b0-48e5e46f1196.png)

# Migração do Tipo IMAP

#Exemplo de ponto de extremidade 
<br>Configuração IMAP
<br>Nome do servidor: imap.hostinger.com
<br>Porta: 993
<br>Método de criptografia: SSL

#Exemplo de arquivo .CSV pra migrações 
<br>EmailAddress,UserName,Password
<br>contato@filial365.cf,contato@filial365.cf,Mk230159@
<br>comercial@filial365.cf,comercial@filial365.cf,Mk230159@
<br>joao@filial365.cf,joao@filial365.cf,Mk230159@

# Scripts para Exchange Online 

#Conecta Exchange Online
<br>Install-Module ExchangeOnlineManagement -AllowClobber
<br>Import-Module ExchangeOnlineManagement
<br>Connect-ExchangeOnline

#consulta migracao
<br>Test-MigrationServerAvailability -IMAP -RemoteServer imap.hostinger.com -Port 993 -Security Ssl
<br>Get-MigrationBatch -Identity IMAP01 | Format-List
<br>Get-MigrationBatch -Identity IMAP01 | Format-List Status
<br>Get-MigrationUser | Get-MigrationUserStatistics

#Antigo
<br>Get-Mailbox
<br>Get-Mailbox -ResultSize 20
<br>Get-mailbox -Identity alex.sousa@matriz365.cf | fl
<br>Get-Mailbox –RecipientType 'UserMailbox' | Get-MailboxStatistics | Sort-Object LastLogonTime | Where {$_.LastLogonTime –lt ([DateTime]::Now).AddDays(-1) } | Format-Table DisplayName, LastLogonTime # 1 dia
<br>Get-MailTrafficATPReport # Inbound and Outbound
<br>Get-MailboxFolderPermission -Identity alex.sousa@matriz365.cf | fl
<br>Get-Recipient -Identity alex.sousa@matriz365.cf | fl
<br>Get-RecipientPermission -Identity alex.sousa@matriz365.cf | fl   

#Novo
<br>Get-EXOMailbox   
Get-EXOMailboxFolderPermission -Identity alex.sousa@matriz365.cf | fl
<br>Get-EXOMailboxPermission -Identity alex.sousa@matriz365.cf | fl
<br>Get-EXOMailboxStatistics -Identity alex.sousa@matriz365.cf | fl 
<br>Get-EXORecipient -Identity alex.sousa@matriz365.cf | fl
<br>Get-EXORecipientPermission -Identity alex.sousa@matriz365.cf | fl

#Criar Mailbox Compartilhada
<br>New-Mailbox -Name "Mailbox Compartilhada" -Alias mbcompartilhada –Shared -PrimarySmtpAddress mbcompartilhada@matriz365.cf
<br>Get-Mailbox -Filter {recipienttypedetails -eq "SharedMailbox"}
<br>Remove-Mailbox "Mailbox Compartilhada" 

#Criar Mailbox 
<br>New-Mailbox -Alias Mailbox -Name Mailbox -FirstName Mailbox -LastName Teste -DisplayName "Mailbox Teste" -MicrosoftOnlineServicesID mbteste@matriz365.cf -Password (ConvertTo-SecureString -String 'P@ssw0rd' -AsPlainText -Force) -ResetPasswordOnNextLogon $true
<br>Get-Mailbox
<br>Remove-Mailbox "Mailbox" 
<br>Get-Mailbox

#Archive
<br>Enable-Mailbox -Identity alex.sousa@matriz365.cf -Archive
<br>Get-Mailbox -Archive
<br>Get-Mailbox | Enable-Mailbox -Archive
<br>Get-Mailbox | Disable-Mailbox -Archive

#disconect
<br>Remove-PSSession $exchangeSession

# Limites do Exchange Online 

![image](https://user-images.githubusercontent.com/49683486/173577813-f64b8584-4a79-41a4-816e-d3e8285e80b8.png)

![image](https://user-images.githubusercontent.com/49683486/173577890-213925b2-a011-4951-9231-da485d034252.png)

![image](https://user-images.githubusercontent.com/49683486/173577935-bfbb0ee2-ef11-4cef-9fd6-398c5af35864.png)

![image](https://user-images.githubusercontent.com/49683486/173577984-3a72de32-95c7-40c9-bc16-9dfed94a6c1d.png)

![image](https://user-images.githubusercontent.com/49683486/173578074-69ee3ade-4a37-4b85-b19a-92d66d68b703.png)

![image](https://user-images.githubusercontent.com/49683486/173578118-4246844c-ee0f-4560-a22b-8dfd057af887.png)

FIM
