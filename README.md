# HelloWorkshop

[![Build](https://github.com/s37674/warp-lab01-hello-workshop/actions/workflows/build.yml/badge.svg)](https://github.com/s37674/warp-lab01-hello-workshop/actions/workflows/build.yml)

Aplikacja konsolowa .NET stworzenia podczas laboratorium.

## Uruchomienie
```bash
dotnet run
```

## Continuous Integration

Projekt korzysta z automatycznego pipeline'u GitHub Actions zdefiniowanego w pliku `.github/workflows/build.yml` (**Build .NET project**).

- **Zdarzenia uruchamiające workflow:** `push` do gałęzi `main`, otwarcie lub aktualizacja `pull_request` skierowanego do `main` oraz ręczne wywołanie `workflow_dispatch`.
- **Sprawdzany projekt i środowisko:** plik projektu `./HelloWorkshop.csproj`, zestaw SDK `.NET 10.0.x` (`net10.0`) na runnerze `ubuntu-latest`.
- **Wykonywane kontrole w jobie `build`:**
  1. Sprawdzenie struktury repozytorium skryptem `scripts/check-repository.sh` (weryfikacja argumentu, istnienia pliku `.csproj` oraz niepustego pliku `README.md`).
  2. Konfiguracja środowiska `.NET` (`actions/setup-dotnet@v4`).
  3. Odtworzenie zależności (`dotnet restore`).
  4. Kompilacja w konfiguracji `Release` (`dotnet build --configuration Release --no-restore`).
  5. Uruchomienie aplikacji (`dotnet run --configuration Release --no-build`).
  6. Publikacja aplikacji do katalogu `./artifacts/app` (`dotnet publish --configuration Release --no-restore --output ./artifacts/app`).
- **Artefakt kompilacji:** wynik publikacji jest wysyłany przez `actions/upload-artifact@v4` jako paczka o nazwie `app-<sha>` (`app-${{ github.sha }}`) i przechowywany przez **7 dni** (`retention-days: 7`).
- **Gdzie znaleźć logi i artefakty:** przejdź do zakładki **Actions** w repozytorium GitHub (lub sekcji **Checks** w Pull Requeście) i otwórz wybrane uruchomienie workflow **Build .NET project**. Szczegółowe logi poszczególnych kroków znajdują się po wejściu w job **build**, natomiast paczkę artefaktu `app-<sha>` można pobrać na stronie podsumowania uruchomienia (**Summary**) w sekcji **Artifacts**.

## Kontakt
Autor: Student
## Kontakt
Zespół: Warsztat Programisty
