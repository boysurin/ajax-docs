---
title: Controls Not Compatible with RadAjax
page_title: Controls Not Compatible with RadAjax | UI for ASP.NET AJAX Documentation
description: Controls Not Compatible with RadAjax
slug: ajax/troubleshooting/controls-not-compatible-with-radajax
tags: controls,not,compatible,with,radajax
published: True
position: 6
---

# Controls Not Compatible with RadAjax



## 

The following ASP.NET controls are not compatible with partial-page updates, and are therefore not supported inside an[UpdatePanel](http://msdn.microsoft.com/en-us/library/bb386454.aspx) control:

* [TreeView](http://msdn2.microsoft.com/en-us/k5c13faz) and [Menu](http://msdn2.microsoft.com/en-us/07b8w058) controls.

* Web Parts controls. For more information, see [ASP.NET Web Parts Controls](http://msdn2.microsoft.com/en-us/library/ab78a66e-9feb-4391-b3c3-8c07555e2308).

* [FileUpload](http://msdn2.microsoft.com/en-us/ysf0192b) controls when they are used to upload files as part of an asynchronous postback.

* [GridView](http://msdn2.microsoft.com/en-us/4w7ya1ts) and [DetailsView](http://msdn2.microsoft.com/en-us/7z482d0y) controls when their __EnableSortingAndPagingCallbacks__ property is set to __true__. The default is __false__.

* [Login](http://msdn2.microsoft.com/en-us/t863ehhh), [PasswordRecovery](http://msdn2.microsoft.com/en-us/t92zy5x0), [ChangePassword](http://msdn2.microsoft.com/en-us/s1xhe282), and [CreateUserWizard](http://msdn2.microsoft.com/en-us/6s8b6814) controls whose contents have not been converted to editable templates.

* The [Substitution](http://msdn2.microsoft.com/en-us/9ze89as6) control.

See a full list of controls that are not compatible with __RadAjax for ASP.NET AJAX__ from the official Microsoft AJAX documentation [here (scroll about halfway down the article.))](http://msdn.microsoft.com/en-us/library/cc295545.aspx).

# See Also

 * [Microsoft UpdatePanel Control](http://msdn.microsoft.com/en-us/library/cc295545.aspx)

 * [ASP.NET Web Parts Controls](http://msdn.microsoft.com/en-us/library/ab78a66e-9feb-4391-b3c3-8c07555e2308)