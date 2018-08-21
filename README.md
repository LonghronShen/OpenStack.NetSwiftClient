# OpenStack .Net SwiftClient

A client developed in .Net Standard 2.0 to access OpenStack servers and perform the most frequent actions.

A WPF client is included to demonstrate some of the most important functions, as well as a ASP.NET Core project.

It has been developed to address the lack of .Net client for the OVH object storage service.

## Contribution

Feel free to pull request, the client is not exhaustive and will get new features.

## ASP.NET Core demo project

Just launch the project, on first start, the site should ask for your authentication endpoint and credentials. 
Then you may browse your account.

The ASP.NET Core project demonstrates:
- Authentication on OpenStack Identity server (the token is stored in an encrypted cookie)
- List an account properties and its containers (in the library, account = object store)
- Set temporary link keys to generate temporary links for objects
- Create containers with all relevant metadata availables
- List a container properties and its files
- Upload files
- Download files
- Get files properties
- Delete files
- Create a temporary link to access a non-public file

TODO:
- Update container properties
- Update file properties
- Upload large files
- Manage containers ACL


## WPF demo project

Add a `DemoContext.NotIncluded.cs` file on the WPF demo project, with the following code in order to test the project more easily:

```csharp
    namespace NetSwiftClient.Demo
    {
        public partial class DemoContext
        {
            public DemoContext()
            {
                _AuthUrl = "https://auth.cloud.ovh.net/v3";
                _AuthName = "XXXXX";
                _AuthPassword = "YYYYY";
                _AuthDomain = "Default";
                _ObjectStoreUrl = "https://storage.sbg3.cloud.ovh.net/v1/AUTH_zzzz"; 
            }
        }
    }
```
The WPF project demonstrates:
- Authentication on OpenStack Identity server (the token is stored in an encrypted cookie)
- List an account properties and its containers (in the library, account = object store)
- List a container properties and its files
- Upload files
- Download files

## OVH

OVH provides a object storage service based on the OpenStack API (OpenStack identity + swift).

They propose a cheap storage, with 3x replication, quite cheap and simple prices (0.01€/month/GB + free incoming + 0.01€/outgoing GB):
- Static hosting => Store your entire static website, all files are public
- Public container => Store your website media, all files are public (the difference with the static hosting is unclear)
- Private container => Store your website media, files are not accessible to the public, but you can allow temporary links via the API
- Cold storage => Storage is much cheaper, but incoming traffic is paid (0.002€/month/GB + 0.01€/incoming GB + 0.01€/outgoing GB)

https://www.ovh.ie/public-cloud/storage/object-storage/

