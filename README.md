# xluh.co

A URL shortener for Excella that lives at <http://xluh.co> (Excella co. Get it?)

Click the links below to view the current status. 

| Build status  | Deployment status | Dependencies | 
| ------------- | ------------- | ---------------- |
| [![Build Status](https://dev.azure.com/excellaco/xluhco/_apis/build/status/excellalabs.xluhco?branchName=master)](https://dev.azure.com/excellaco/xluhco/_build/latest?definitionId=4&branchName=master)  | [![Deployment Status](https://vsrm.dev.azure.com/excellaco/_apis/public/Release/badge/fe08bdf8-31f0-4c33-abb5-7869d3914fdb/1/1)](https://dev.azure.com/excellaco/xluhco/_release?definitionId=1) | [![Dependabot Status](https://api.dependabot.com/badges/status?host=github&repo=excellalabs/xluhco)](https://dependabot.com) |

## Adapting xluh.co for Your Own Domain Name

See the [Adapting.md](ADAPTING.md) guide for advice on how to use this project to host your own URL shortener at your own domain.

## Issue? Idea? Code to Contribute?

Check out the [Contributing.md](CONTRIBUTING.md) document for guidelines on how to raise issues, build the project, submit PRs, etc.

## How This Works

* ASP.NET route binding to a `RedirectController`. (a basic `HomeController` matches empty routes.)
* A `RedirectController` that makes use of an `IShortLinkRepository` to obtain links and permanently redirect if a matching short code is found
* An implementation of `IShortLinkRepository` that reads a CSV file in `wwwroot` using [CsvHelper](https://joshclose.github.io/CsvHelper/).
* Google Analytics, written into the page from the server side response, that includes tracking links.
* An automatic redirect using a callback from the Google Analytics event posting.

Would you like us to expound more on any of these explanations? Please [submit an issue](http://github.com/excellalabs/xluhco/issues/new) with your question and we'll be happy to answer it!

## How to include custom text and images when sharing shortened URLs in social media

The .csv file contains 3 optional columns for each URL: `imageURL`, `title` and `description`.

* When sharing a shortened URL on social media, the social media site may use the information provided on these columns to display a preview of your target site.
* xluh.co reads the information on these columns and uses it to populate meta tags on its intermediate redirect page. These may be crawled by social media sites at the time of sharing.
* For more information please visit [https://www.addtoany.com/ext/meta-tags](https://www.addtoany.com/ext/meta-tags)

## Lessons We've Learned So Far

* Originally, we used IIS URL rewriting to redirect everything to the `RedirectController` and returned server-side 302 redirects. This worked fine and was really fast, but didn't afford us the ability to capture all of the analytics information we needed (server-side analytics experience just simply isn't as rich). So, we went back to loading a page with Google Analytics injected.

## Acknowledgements

We stand on the shoulders of giants, and would like to thank the following libraries for helping this project exist:

* [.NET Core](https://docs.microsoft.com/en-us/dotnet/core/) -- Microsoft's newest edition of the .NET framework enables a lot of cross-platform potential, and it's been a joy to work with here.
* [xUnit.NET](http://xunit.net) -- A fantastic unit testing framework that is ready to go right out of the box for .NET Core development.
* [FluentAssertions](https://fluentassertions.com/) -- This great assertions library helps our tests read better and produces great failure messages.
* [CsvHelper](https://joshclose.github.io/CsvHelper/) is a great easy utility for parsing CSV files.
* [Azure DevOps Pipelines](https://azure.microsoft.com/en-us/services/devops/) has been a great CI tool and tells us whenever something breaks, for free. They're super easy to get up and running with for .NET Core apps and the `azure-pipelines.yml` file makes it easy to port this CI to any forks of this project as well.
