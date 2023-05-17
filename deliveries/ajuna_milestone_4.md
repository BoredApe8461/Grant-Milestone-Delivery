# Milestone Delivery :mailbox:

> ⚡ Only the GitHub account, which is responsible for the pull request of the accepted application is allowed to submit milestones. 
> 
> Don't remove any of the mandatory parts presented in bold letters or as headlines! Lines starting with `>`, such as this one, can be removed.

**The [invoice form :pencil:](https://docs.google.com/forms/d/e/1FAIpQLSfmNYaoCgrxyhzgoKQ0ynQvnNRoTmgApz9NrMp-hd8mhIiO0A/viewform) has been filled out correctly for this milestone and the delivery is according to the official [milestone delivery guidelines](https://github.com/w3f/Grants-Program/blob/master/docs/milestone-deliverables-guidelines.md).**  

* **Application Document:**  [LINK](https://github.com/w3f/Grants-Program/blob/master/applications/ajuna_network_follow_up.md) 
* **Milestone Number:** 4

> Please provide a list of all deliverables of the milestone extracted from the initial application and a link to the deliverable itself. Ideally all links inside the below table should include a commit hash, which will be used for testing. If you don't provide a commit hash, we will work off the default branch of your repository. Thus, if you plan on continuing work after delivery, we suggest you create a separate branch for either the delivery or your continuing work. 
> 
> If there is anything particular about any of the deliverables we or a future reader should know, use the respective `Notes` column.

| Number | Deliverable        | Link                                                                                                                                                                                       | Notes                                                |
|--------|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|
| 0a.    | License            | [Apache 2.0 / MIT / Unlicense](https://github.com/ajuna-network/Open-Grants-Program/issues/55)                                                                                             | Done                                                 |
| 0b.    | Documentation      | [Ducumentation](https://github.com/ajuna-network/Open-Grants-Program/issues/56)                                                                                                            | This an ongoing proccess and we are working on it.   |
| 0c.    | Testing Guide      | [Implement testing code coverage min 70%](https://github.com/ajuna-network/Open-Grants-Program/issues/57)                                                                                  | Done |
| 0d.    | Article/Tutorial   | [Article/Tutorial: Write article about the work in this grant](https://github.com/ajuna-network/Open-Grants-Program/issues/58)                                                             | Done (We keep adding videos and tutorials as we go.) |                                                                                                                                        |
| 1.     | Mobile Application | [Provide fully functional Multiplayer playable "Connect Four" for Mobile (Android), playable with bots and as real player](https://github.com/ajuna-network/Open-Grants-Program/issues/60) | Done |
| 2.     | Stress Testing     | [Providing a performance test setup that creates 1000 bots playing the game concurrently](https://github.com/ajuna-network/Open-Grants-Program/issues/61)                                  | Done |
| 3.     | Video Tutorial     | [Youtube Videos serie Step-by-Step Connect four on Substrate Mobile](https://github.com/ajuna-network/Open-Grants-Program/issues/62)                                                       | Done |

# Substrate Gaming SDK (Unity Asset Store) [in review]

![UnitAssetStore](https://user-images.githubusercontent.com/17710198/206007310-a415349b-c879-4df9-81ea-2349ded09a3d.png)

# Ajuna.NetApi & Ajuna.SDK
| Project | Description                                                                                                                                                                                                                                                                               | NuGet 
|---|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---|
| Ajuna.NetApi | Ajuna .NET API Full-featured substrate node API                                                                                                                                                                                          | [![Nuget](https://img.shields.io/nuget/v/Ajuna.NetApi)](https://www.nuget.org/packages/Ajuna.NetApi/) |
| Ajuna.ServiceLayer | Implements the fundamental layer to access substrate node storage changes with a convenient API.                                                                                                                                                                                          | [![Nuget](https://img.shields.io/nuget/v/Ajuna.ServiceLayer)](https://www.nuget.org/packages/Ajuna.ServiceLayer/) |
| Ajuna.ServiceLayer.Model | Implements standard classes to easily share types between services and clients.                                                                                                                                                                                                           | [![Nuget](https://img.shields.io/nuget/v/Ajuna.ServiceLayer.Model)](https://www.nuget.org/packages/Ajuna.ServiceLayer.Model/) |
| Ajuna.AspNetCore | Implements extensions to the service layer that allow for quickly building a RESTful service to access your substrate node storage.                                                                                                                                                       | [![Nuget](https://img.shields.io/nuget/v/Ajuna.AspNetCore)](https://www.nuget.org/packages/Ajuna.AspNetCore/) |
| Ajuna.DotNet, Ajuna.DotNet.Template | .NET developer toolchain to scaffold actual projects such as a RESTful service including all the storage classes, types, and consumer clients. The projects generated with the generator toolchain are intended to be used for scaffolding and starting a substrate node service quickly. | [![Nuget](https://img.shields.io/nuget/v/Ajuna.DotNet)](https://www.nuget.org/packages/Ajuna.DotNet/) [![Nuget](https://img.shields.io/nuget/v/Ajuna.DotNet.Template)](https://www.nuget.org/packages/Ajuna.DotNet.Template/)|
