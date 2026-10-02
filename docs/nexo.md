# Rozszerzenie modułu o Nexo

Zacznij od działającego szablonu Core. Nexo wymaga dodatkowo biblioteki Connection
oraz SDK InsERT w wersji zgodnej z bazą podmiotu.

1. Ustaw `TargetFramework` na `net8.0-windows` w projekcie modułu, testów i programu
   lokalnego. Dla projektu modułu dodaj również `UseWPF=true` oraz `PlatformTarget=x64`,
   zgodnie z [przykładem Nexo.Test](https://github.com/zapqio/dotnet-module-nexo-test).
2. W projekcie modułu dodaj publiczną paczkę:

   ```xml
   <PackageReference Include="Zapqio.Nexo.Connection" Version="1.1.3" ExcludeAssets="runtime" />
   ```

3. Przygotuj SDK InsERT na komputerze budującym. NuGet Connection zawiera referencje
   do SDK, ale nie same biblioteki InsERT. Przykładowa kompilacja na Windows:

   ```powershell
   dotnet publish Template.Module.csproj -c Release -o artifacts/publish -p:nexoSdkBinPath="C:\nexoSDK_61.1.0.9431\Bin"
   ```

   Dopasuj katalog i wersję do swojego środowiska. Możesz też ustawić `nexoSdkBinPath`
   w projekcie lub `Directory.Build.props`. Własny `Directory.Build.props` w repozytorium
   powinien importować nadrzędną konfigurację runnera, jeśli ma z niej korzystać.
4. Na serwerze z runnerem .NET 8 uruchom jako administrator
   `install-nexo.ps1 -BuildTools`, gdy budujesz na runnerze, albo `install-nexo.ps1`,
   gdy dostarczasz gotowy ZIP z CI. Instalator przygotowuje `Nexo.Connection.zip`,
   `Nexo.Sdk.zip` i konfigurację bazy. Wariant `-BuildTools` przygotowuje również SDK
   do kompilacji oraz środowisko konta usługi.
5. W CI pozostaw Windows i dodaj przygotowanie SDK przed kompilacją. Gotowy wzorzec
   restore, odczytu wersji SDK i jego pobierania znajdziesz w
   [workflowie Nexo.Test](https://github.com/zapqio/dotnet-module-nexo-test/blob/main/.github/workflows/build.yml).
   Samo dodanie PackageReference nie przygotuje SDK na maszynie GitHub Actions.

Metoda może otrzymać `Nexo.NexoClient` w konstruktorze; jego implementację dostarcza
moduł współdzielony na runnerze. Ogólny `tools/LocalRunner` tworzy tylko przykładową
metodę Hello — nie konfiguruje połączenia z Nexo. Testy wymagające Nexo przygotuj
oddzielnie wraz z kontrolowanym środowiskiem i wymaganymi zależnościami runtime.

Zachowaj zgodność NuGet Connection z ZIP-em zainstalowanym na serwerze. Biblioteki
Core, Connection i InsERT są współdzielone przez runnera, więc nie dokładaj ich kopii
do ZIP-a własnego modułu.

Pełne instrukcje SDK, konfiguracji i połączenia są w
[dokumentacji Connection](https://github.com/zapqio/dotnet-module-nexo-connection#wybór-sdk-podczas-kompilacji).
