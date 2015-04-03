---
title: CDN Support Overview
page_title: Overview | UI for ASP.NET AJAX Documentation
description: Overview
slug: stylesheetmanager/cdn-support/overview
tags: overview
published: True
position: 0
---

# CDN Support Overview



Starting with the __Q3 2009 Service Pack 1__ release you will be able to load the controls scripts and skins from the Telerik CDN. Telerik CDN is hosted on the Amazon CloudFront service. This is a __global content delivery service__ with edge locations in the US, Europe and Asia.

Using the Content Delivery Network has a number of advantages:

* __Reduced latency__ – requests will be automatically redirected to the nearest server

* __Compressed output__ - the css files are already compressed so they are in minimum size

* __Better use of caching__ – each resource only needs to be downloaded once

* __Reduced hosting expenses__ – we host the resources for you so you can pay less



__Caching__ is what a CDN is all about. Say you have a number of applications that all utilize RadGrid. A customer will load the RadGrid css and images just once and then use the cached version until he clears his browser’s cache. Proxies will also aggressively cache these resources.

## When NOT to use CDN?

* Intranet applications in particular are a bad candidate for it. Your Intranet is likely to be a lot faster than any type of CDN. You’ll also lose the ability to run your application without an Internet connection.

* When you are using a latest internal build (not an official one). We will not host the resources for any intermediate versions. __Only the official__ release version will support CDN.



## How to enable Telerik CDN

1. Make sure you are using Telerik.Web.UI version 2009.3.1207 (__Q3 2009 SP1__) or later.

2. Set the __CdnSettings-TelerikCdn__ property of the RadStyleSheetManager to Enabled:

````ASPNET
	    <telerik:RadStyleSheetManager 
	        ID="RadStyleSheetManager1" 
	        runat="server" 
	        CdnSettings-TelerikCdn="Enabled" />
````



Another way to set that property is to use the composite __<CdnSettings>__ property of RadStyleSheetManager:

````ASPNET
	    <telerik:RadStyleSheetManager 
	        ID="RadStyleSheetManager1" 
	        runat="server">
	        <CdnSettings TelerikCdn="Enabled" />
	    </telerik:RadStyleSheetManager>
````



Moreover, you can enable the CDN support __globally__ by adding the following keys in the <appSettings> section of your web.config file:

````XML
	    <appsettings>   
	        <add key="Telerik.ScriptManager.TelerikCdn" value="Enabled" />   
	        <add key="Telerik.StyleSheetManager.TelerikCdn" value="Enabled" />
	    </appsettings>
````



Note, that the first line will enable the CDN support for the [javascript files](3962E5BD-7414-41F5-82AA-8D144A9327AF).

## How are my users affected?

The Telerik CDN uses the following host names for loading the control resources:

* __http://aspnet-scripts.telerikstatic.com__ - for the scripts;

* __http://aspnet-skins.telerikstatic.com__ - for the skins (css and images);

Your users need to have access to the above URLs.



## What about SSL?

When a SSL connection is used RadScriptManager and RadStyleSheetManager will use the native Amazon CloudFront distribution hosts:

* __https://d2i2wahzwrm1n5.cloudfront.net__ - for the scripts;

* __https://d35islomi5rx1v.cloudfront.net__ - for the skins (css and images);



## Detailed information with an example

Let's add some RadControls on the page (RadMenu, RadTabStrip, RadListBox) and RadStyleSheetManager with enabled CDN support. When you run the page you will observe the following:

1. The needed CSS files are loaded from the CDN network. If the browser supports compression (the request has __Accept-Encoding__ HTTP header set to *gzip,deflate*) then the files are served __compressed__. The compression is done before uploading of the files to the CDN network, so there are no CPU cycles on the server to compress at run-time. If the browser is __IE6__ then the files are served __uncompressed__ (from another URL) that is because earlier versions of the browser has problems with decompressing the output.

Here is how the html output look like:

````HTML
	    <link href="http://aspnet-skins.telerikstatic.com/ajaxz/2009.3.1203/Menu.css" type="text/css"
	        rel="stylesheet" class="Telerik_stylesheet" />
	    <link href="http://aspnet-skins.telerikstatic.com/ajaxz/2009.3.1203/Outlook/Menu.Outlook.css"
	        type="text/css" rel="stylesheet" class="Telerik_stylesheet" />
	    <link href="http://aspnet-skins.telerikstatic.com/ajaxz/2009.3.1203/TabStrip.css"
	        type="text/css" rel="stylesheet" class="Telerik_stylesheet" />
	    <link href="http://aspnet-skins.telerikstatic.com/ajaxz/2009.3.1203/Default/TabStrip.Default.css"
	        type="text/css" rel="stylesheet" class="Telerik_stylesheet" />
	    <link href="http://aspnet-skins.telerikstatic.com/ajaxz/2009.3.1203/ListBox.css"
	        type="text/css" rel="stylesheet" class="Telerik_stylesheet" />
	    <link href="http://aspnet-skins.telerikstatic.com/ajaxz/2009.3.1203/Hay/ListBox.Hay.css"
	        type="text/css" rel="stylesheet" class="Telerik_stylesheet" />
````



2. If you open any of the css files (e.g. Menu.Outlook.css) you will notice that the url to the sprite images is very short and simple:

````XML
	    background-image: url('Menu/rmSprite.png');
````



There is no more long web resource urls like this:

````XML
	    background-image: url('/RadControlsWebSite2GAC/WebResource.axd?d=hgwy1jK8IjC5j7HbbfVh_E6saCEiqXDW9eAimnKa_bS60KBM4_SI-KvArO1mPviVyV_axd&t=633954571805516704');
````



Note that the CSS files from the CDN are placed in the __/ajaxz/__ folder - this means that the compressed file is downloaded. If your browser does not support content encoding (or it is IE6) then you will notice that the scripts are loaded from the __/ajax/__ folder.