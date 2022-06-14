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

# Conectores Meio Hibrido - Gateway Symantec Usado - Apoio a Aluno 

Configuring Exchange 2016
Use the EAC to create a Send connector that uses smart host routing
In the EAC, navigate to Mail flow > Send connectors, and then click Add Add icon. This starts the New Send connector wizard.

On the first page, enter the following information:

Name   Enter a descriptive name for the Send connector, for example, Smart host to Internet.

Type   Select a descriptive value. For example, Internet or Custom.

When you are finished, click Next.

On the next page, select Route mail through smart hosts, and then click Add Add icon. In the Add smart host dialog box that appears, identify the smart host by using the following value:

Fully qualified domain name (FQDN)   For example, securitydevice01.contoso.com. Note that the Exchange source servers for the Send connector must be able to resolve the smart host in DNS by using this FQDN.

When you are finished, click Save.

You can enter multiple smart hosts by repeating Step 3. When you are finished, click Next.

On the next page, in the Route mail through smart hosts section, select the authentication method that's required by the smart host. Valid values are:

 
Authentication mechanism	Description
None

No authentication. For example, when access to the smart host is restricted by the source IP address.

Basic authentication

Basic authentication. Requires a user name and password. The user name and password are sent in clear text.

Offer basic authentication only after starting TLS

Basic authentication that's encrypted with TLS. This requires a server certificate on the smart host that contains the exact FQDN of the smart host that's defined on the Send connector.

Exchange Server authentication

Generic Security Services application programming interface (GSSAPI) and Mutual GSSAPI authentication.

Externally secured

The connection is presumed to be secured by using a security mechanism that's external to Exchange. The connection may be an Internet Protocol security (IPsec) association or a virtual private network (VPN). Alternatively, the servers may reside in a trusted, physically controlled network.

When you are finished, click Next.

On the next page, in the Address space section, click Add Add icon. In the Add domain dialog box that appears, enter the following information:

Type   Verify SMTP is entered.

Fully Qualified Domain Name (FQDN)   Enter an asterisk (*) to indicate the Send connector applies to messages addressed to all external domains. Alternatively, you can enter a specific external domain (for example, contoso.com), or a domain and all subdomains (for example, *.contoso.com).

Cost   Verify 1 is entered. A lower value indicates a more preferred route for the domains you specified.

When you are finished, click Save.

Back on the previous page, the Scoped send connector setting is important if your organization has Exchange servers installed in multiple Active Directory sites:

If you don't select Scoped send connector, the connector is usable by all transport servers (Exchange 2016 Mailbox servers, Exchange 2013 Mailbox servers, and Exchange 2010 Hub Transport servers) in the entire Active Directory forest. This is the default value.

If you select Scoped send connector, the connector is only usable by other transport servers in the same Active Directory site.

When you are finished, click Next.

On the next page, in the Source server section, click Add Add icon. In the Select a Server dialog box that appears, select one or more Mailbox servers that you want to use to send outbound mail to the smart host. If you have multiple Mailbox servers in your environment, select the ones that can route mail to the smart host. If you have only one Mailbox server, select that one. After you've selected at least one Mailbox server, click Add, click OK, and then click Finish.

After you create the Send connector, it appears in the Send connector list.

How do you know this worked?
To verify that you have successfully created a Send connector to route outbound email through a smart host, send a message from a user in your organization to an external domain that's serviced by the Send connector.

 
Configuring Exchange 2013
Use the EAC to create a Send connector that uses smart host routing
In the EAC, navigate to Mail flow > Send connectors, and then click Add Add Icon.

In the New send connector wizard, specify a name for the send connector and then select Custom for the Type. You typically choose this selection when you want to route messages to computers not running Microsoft Exchange Server 2013. Click Next.

Choose Route mail through smart hosts, and then click Add Add Icon. In the Add smart host window, specify the the fully qualified domain name (FQDN), such as cluster8out.eu.messagelabs.com. Click Save. (Note that the correct smarthost to use will have been provided in your welcome documentation)

For Smart host authentication, choose the type of authentication required by the smart host. If you choose Basic authentication, you must provide a user name and password.

NoteNote:
If you choose Basic authentication, we recommend that you use an encrypted connection because the user name and password are sent in clear text.
Under Address space, click Add Add Icon. In the Add domain window, make sure SMTP is listed as the Type. For Fully Qualified Domain Name (FQDN), enter * to specify that this send connector applies to messages sent to any domain. Click Save.

For Source server, click Add Add Icon. In the Select a server window, choose a server and click Add Add Icon. Click OK.

Click Finish.

Once you have created the send connector, it appears in the Send connector list.

How do you know this worked?
To verify that you have successfully created a Send connector to route outbound email through a smart host, send a message from a user in your organization (you can use the Outlook Web App) to the domain you specified for the Address space. If the recipient receives the message, you've successfully configured the send connector.

FIM
