---
layout: default
title: Connecting to MS SQL Server
nav_order: 2
parent: On-premise Data
---
# Connecting to MS SQL Server

On Windows, the Agent runs using the Windows Local System account by default. This may or may not be sufficient, depending on your business' security protocols.

If the integration is unable to connect to a SQL Server instance that you can see, you likely need to re-configure the service to log on as a domain user with the appropriate access. Each time the Agent starts, it will log on as that user.

1. Open Windows Administrative Tools → Services
2. Locate and Right-click Actian Integration Agent → Click Properties
3. Select the Log On tab
4. Select the radio button for "This account:"
5. Enter the Domain User credentials which have appropriate access to the local storage or database
6. Click OK
7. Right-click Actian Integration Agent → Click Restart
