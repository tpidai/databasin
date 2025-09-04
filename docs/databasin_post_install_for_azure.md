# Overview

This guide details the initial configuration that need to be completed after installing the managed Azure Marketplace offering: **Databasin -Data Automation for Healthcare and AI**

## Post-Installation Steps:

### Setup DNS / Forwarding

Databasin's API and UI, by default, are installed within a private Azure
Container Apps Environment (ACA). The installation does expose a VM for
you to log into (Instructions directly below), but that is only used for
initial configuration / troubleshooting. To enable all users access to
the Databasin UI, you must setup forwarding from your on-prem/cloud
network, into the ACA environment.

1.  Log into the Azure portal and find your Databasin installation.

2.  At the top right-hand corner, you will find a "databasin" resource
    group. Click that to enter the resource group. In this group, you
    will find all the installed components of Databasin.

3.  One of the components will be a "Container Apps Environment". Click
    that to enter.

4.  In this view, please copy/note the "Static IP". You will need this.

5.  Below, you will find both the UI and API containers. Typically, they
    are named "databasin-api" and "databasin-ui". You only need to be
    concerned with the "UI" container. Please click into the
    "databasin-ui" container.

6.  Azure will generate an "Application URL" you will find at the top
    left-hand corner. The ACA environment and its components will be
    under this URL. Please note the "databasin-ui" at the start of the
    URL. That is specific to this container. For example, the API
    container would start with "databasin-api", but the rest of the URL
    is static/specific to your environment. You will need to copy this.

    a.  Example: If your UI has the following URL:
        https://databasin-ui.agreeablemoss-ee3bea84.northcentralus.azurecontainerapps.io,
        then you will need to copy
        "agreeablemoss-ee3bea84.northcentralus.azurecontainerapps.io"
        for the routing.

7.  At this point, you will need to set up routing, with a wildcard
    cert, from your on-prem network to the ACA env.

    a.  Example:

        i.  DNS Zone:
            agreeablemoss-ee3bea84.northcentralus.azurecontainerapps.io

        ii. Name \* (Wildcard)

        iii. Type A

        iv. IP =\> (The Static IP from point 4)

        v.  TTL =\> 3600

## Databasin Permissions Consent

1.  Open Microsoft Edge browser and navigate to the **databasin_url**
    copied in the previous step
    (databasin-ui.\<uniquename\>.azurecontainerapps.io) and you should
    see the **Databasin** login page:\
    
    ![](./post_install/media/image1.png)

2.  Sign in with the **Installer Email Address** previously supplied and **Consent on behalf of your organization** to approve the     arequired **Databasin** permissions

    ![](./post_install/media/image2.png)

## Configuring VNet Peering & DNS

1.  Set up **VNet Peering** to enable communication across different VNets.

2.  Navigate to **Azure DNS Zone**.

3.  Add an **A record** pointing to the Databasin service's IP or custom
    domain.

4.  Verify DNS resolution and access.

5.  Create a DNS A-record for
    databasin-ui.uniquename.region.azurecontainerapp.io within your hub
    DNS zone, so users coming from your VPN/On-prem network can resolve
    this DNS name need to find the IP address assigned to the container
    app managed resource group and use that to create the entry.

##  Complete Project Configuration

![](./post_install/media/image3.png)


## Troubleshooting & Support

- If encountering **connectivity issues**:

  - Check **VNet and firewall settings**.

  - Verify that PostgreSQL is accepting connections from the correct
    subnet.

- Logs can be reviewed in **Azure Monitor** and **Container App Logs**.

- If further assistance is needed, contact **Databasin Support**.
