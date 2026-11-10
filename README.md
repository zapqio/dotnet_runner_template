# .NET module template for Zapq

A module for the external runner. The `template-dotnet-hello` method accepts
`{"Name":"Anna"}` and returns `{"Message":"Cześć, Anna!"}`.

## Get started

1. Select **Use this template → Create a new repository** and clone your repository.
2. Install .NET SDK 8 or later and the .NET 8 runtime, then run the commands below from the repository root.
3. Connect the repository as **.NET** and follow the [module deployment guide](https://docs.zapq.io/guides/external-runner-modules).

```sh
dotnet test tests/Template.Module.Tests/Template.Module.Tests.csproj -c Release
dotnet run --project tools/LocalRunner/LocalRunner.csproj -- examples/input.json
dotnet publish Template.Module.csproj -c Release -o artifacts/publish
```

The package is created at `artifacts/module.zip`. The local runner does not connect to Zapq.
CI prepares the artifact; installation on the runner requires separate approval.

## Documentation

- [Developing .NET modules](https://docs.zapq.io/technical/dotnet-modules#module-template): the template, custom methods, naming, tests, packaging, and CI.
- [External runner modules](https://docs.zapq.io/guides/external-runner-modules): deployment, approval, updates, and withdrawal.

License: [Apache-2.0](LICENSE).
