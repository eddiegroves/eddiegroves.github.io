---
layout: post
title:  WCF In Anger - Quick Solution To Global Error Handling
date:   2012-10-20 00:00:00
---

So after battling for an hour or more trying to get WCF to pickup my custom behaviour extension for logging I came across a handy gem in WCFContrib which got my error logging working first go, albeit with a attribute rather than configured in the web.config.

* Get WCF Contrib from [Nuget](http://nuget.org/packages/WCFContrib) (Install-Package WcfContrib)
* Follow the samples on [Codeplex](http://wcfcontrib.codeplex.com/SourceControl/changeset/view/52109#224740)

For example:

    public class ErrorHandler : IErrorContextHandler
    {
        public void HandleError(Exception error, ActivationErrorContext errorContext)
        {
            LogManager.GetLogger(GetType()).Error(error.ToString(), error);
        }

        public WcfContrib.Extensions.MessageAccessMode RequiredMessageAccess
        {
            get { return WcfContrib.Extensions.MessageAccessMode.None; }
        }
    }

...

    [ErrorContextHandler(typeof(ErrorHandler))]
    public class Service { }

That easy. Now if only I could have that hour of my day back...

