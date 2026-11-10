# Szablon modułu .NET dla Zapq

Moduł dla runnera zewnętrznego. Metoda `template-dotnet-hello` przyjmuje
`{"Name":"Anna"}` i zwraca `{"Message":"Cześć, Anna!"}`.

## Zacznij

1. Wybierz **Use this template → Create a new repository** i sklonuj własne repozytorium.
2. Zainstaluj .NET SDK 8 lub nowszy oraz runtime .NET 8 i uruchom poniższe polecenia z katalogu repozytorium.
3. Podłącz repozytorium jako **.NET** i przejdź przez [wgrywanie modułu](https://docs.zapq.io/pl/guides/external-runner-modules).

```sh
dotnet test tests/Template.Module.Tests/Template.Module.Tests.csproj -c Release
dotnet run --project tools/LocalRunner/LocalRunner.csproj -- examples/input.json
dotnet publish Template.Module.csproj -c Release -o artifacts/publish
```

Paczka powstaje w `artifacts/module.zip`. Program lokalny nie łączy się z Zapq.
CI przygotowuje artefakt; instalacja na runnerze wymaga osobnego zatwierdzenia.

## Dokumentacja

- [Tworzenie modułów .NET](https://docs.zapq.io/pl/technical/dotnet-modules#module-template): szablon, własne metody, nazwy, testy, pakowanie i CI.
- [Moduły runnera zewnętrznego](https://docs.zapq.io/pl/guides/external-runner-modules): wgranie, zatwierdzenie, aktualizacja i wycofanie.

Licencja: [Apache-2.0](LICENSE).
