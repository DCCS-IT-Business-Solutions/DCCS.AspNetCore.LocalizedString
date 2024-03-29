# DCCS.AspNetCore.LocalizedString [![Build status](https://ci.appveyor.com/api/projects/status/h3v0726076j5m81x?svg=true)](https://ci.appveyor.com/project/mgeramb/dccs-aspnetcore-localizedstring) [![NuGet Badge](https://buildstats.info/nuget/DCCS.AspNetCore.LocalizedString)](https://www.nuget.org/packages/DCCS.AspNetCore.LocalizedString/)
The DCCS.AspNetCore.LocalizedString provides a filter for ASP.NET Core application which converts LocalizedExceptions from the [DCCS.LocalizedString.NetStandard](https://github.com/DCCS-IT-Business-Solutions/DCCS.LocalizedString.NetStandard) package to http error 400 (bad request) with the error json formatted in the body and register.

## Installation

Install [DCCS.AspNetCore.LocalizedString](https://www.nuget.org/packages/DCCS.AspNetCore.LocalizedString/) with NuGet:

    Install-Package DCCS.LocalizedString.NetStandard

Or via the .NET Core command line interface:

    dotnet add package DCCS.LocalizedString.NetStandard

Either commands, from Package Manager Console or .NET Core CLI, will download and install DCCS.LocalizedString.NetStandard and all required dependencies.

## Usage

Add the namespace to the Startup.cs:

    DCCS.AspNetCore.LocalizedString

Add the building block in the ConfigureServices function:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddDccsBuildingBlockLocalizedString();
}
``` 

Sample Usage:
```csharp
[ApiController]
public class SampleController : ControllerBase
{
    private readonly ITranslationService _translationService;
    public SampleController(ITranslationService translationService)
    {
        _translationService = translationService;
    }
    
    static readonly LocalizedStringKey ErrorKey = new LocalizedStringKey("This is an error");
    [HttpGet("error")]
    public void Error()
    {
        throw new LocalizedException(_translationService.Create(ErrorKey));
    }
    
    static readonly LocalizedStringKey InformationKey = new LocalizedStringKey("This is a information");
    [HttpGet("information")]
    public ILocalizedString Information()
    {
        return _translationService.Create(InformationKey);
    }
}
```

### Usage of Localized String framework

For information about the usage the LocalizedException and LocalizedString take a look documentation of [DCCS.LocalizedString.NetStandard](https://github.com/DCCS-IT-Business-Solutions/DCCS.LocalizedString.NetStandard)

### Example

A full working sample is included in the [source](https://github.com/DCCS-IT-Business-Solutions/DCCS.AspNetCore.LocalizedString/tree/master/DCCS.AspNetCore.LocalizedString.Sample)

## Contributing
All contributors are welcome to improve this project. The best way would be to start a bug or feature request and discuss the way you want find a solution with us.
After this process, please create a fork of the repository and open a pull request with your changes. Of course, if your changes are small, feel free to immediately start your pull request without previous discussion. 
