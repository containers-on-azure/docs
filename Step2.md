# Step 2 - FrontEnd team adding Docker Support

## Goal

FrontEnd team is resonsible for a small part of the whole solution build by the company. Others teams will build services that might be, direct or indirectally, dependents on their services.

They needed a place to deploy their applications with security, rolling updates, networking, discovery, capable of running multiple stacks (they wish to migrate their web FrontEnd to Angular in the future).

[Add info about decision of using Docker and Kubernetes]

[Adding kubernetes support]

[Running locally with Docker Compose]

[Running locally with Kubernetes in Docker]


## Projects

|Project|Description|Stack|Dependencies|Branch|
|-|-|-|-|-|
|[FrontEnd.Web](https://github.com/containers-on-azure/FrontEnd)|Web UI|ASP.NET Razor Pages|FrontEnd.Api|version-00|
|[FrontEnd.Api](https://github.com/containers-on-azure/FrontEnd)|Web API|ASP.NET Web Api||version-00|

[FrontEnd.Web] &rarr; [FrontEnd.Api]

To debug the application run both projects in Visual Studio. Open the browser on http://localhost:5100/ which will show you the start page containing information about Stocks Market. This information is being pulled from http://localhost:5200/api/v1/contents. The base URI of the API is defined in the configuration setting ```FrontEndApi```, found in file ```appsettings.Development.json``` in FrontEnd.Web project.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information"
    }
  },
  "FrontEndApi": "http://localhost:5200",
  "Kestrel": {
    "EndPoints": {
      "Http": {
        "Url": "http://localhost:5100"
      },
      "Https": {
        "Url": "https://localhost:5101"
      }
    }
  }
}
```

[Go to Start](./ReadMe.md)\
[Go to previous step](./ReadMe.md)\
[Go to next step](./Step2.md)