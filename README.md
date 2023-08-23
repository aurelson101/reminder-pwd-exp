# Welcome Reminder Password Expiration !

This script aims to send a reminder to users that the password will expire in x days. Optimized for Microsoft Outlook but I had no issues with Thunderbird or Apple Mail.
You can edit the HTML/CSS code as you wish, displays also compatible for smarthpone and tablet.


# Requirement

Have RSAT active directory installed and the powershell active directory module installed from the windows server.

## Edit the script

You need to change a few lines before setting it up in production to follow your production setup. Testing ok with :

 1. Exchange 365
 3. Local Exchange + Hybrid
 4. Iredmail.
 5.  SMTP2GO relay smtp (Recommend or another service if you use port 587 if you cannot create connector in Exchange 365).


## Line to Edit :

**Line 5** change the day to start the alert (8 days by default) :

    $daysBeforeExpiration = 8
    
**Line 8** edit your OU=Users :

    $ous= "OU=Users,OU=User Accounts,DC=yourdirectory,DC=lan"

**Line 10** Add your email IT :

    $emailSender = "it.helpdesk@exemple.com"

**Line 13** add your smtp 25 or 587 etc ....

    $smtpServer = "smtp.exemple.com"
    $smtpPort = 25

If you define user add this exemple :

    $smtpUsername = "your_username"
    $smtpPassword = "your_password"
    $smtpSecurePassword = ConvertTo-SecureString $smtpPassword -AsPlainText -Force
    $smtpCredentials = New-Object System.Management.Automation.PSCredential ($smtpUsername, $smtpSecurePassword)


**Line 136** add your URL logo :

    src="https://exemple.com/images/logo.png"

**The end of line 169** add your url exemple to change password :

    href="YOURURLHOWTOCHANGEPASSWORD"> tutorial</a></p></td>

**Line 192** change the number from your IT number :

    +33 01 50 80 50 80 (call only for emergency)

**Line 229** add some option if you use port like 587

    Send-MailMessage -To $user.EmailAddress -From $emailSender -Subject "Password Expiration Reminder" -Body $emailBody -BodyAsHtml -SmtpServer $smtpServer -Port 587 -UseSsl -Credential $smtpCredentials


![enter image description here](https://i.ibb.co/p3fCn87/expire.jpg)
