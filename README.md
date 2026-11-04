# jenkins – przykładowa aplikacja Java z pipeline'em Jenkins

[![CI](https://github.com/rafalski76/jenkins/actions/workflows/ci.yml/badge.svg)](https://github.com/rafalski76/jenkins/actions/workflows/ci.yml)

Prosta aplikacja Java (Maven) wypisująca `Hello World!`, wraz z testami jednostkowymi
(JUnit 5) i deklaratywnym pipeline'em Jenkins. Projekt powstał na bazie tutoriala
[Build a Java app with Maven](https://www.jenkins.io/doc/tutorials/build-a-java-app-with-maven/)
z dokumentacji Jenkinsa.

## Wymagania

- JDK 21 (LTS) lub nowszy
- Maven 3.9+

## Struktura

| Ścieżka | Opis |
| --- | --- |
| `src/main/java` | Kod aplikacji (`com.mycompany.app.App`) |
| `src/test/java` | Testy jednostkowe (JUnit Jupiter) |
| `pom.xml` | Konfiguracja Mavena (kompilacja, JAR, maven-enforcer) |
| `jenkins/Jenkinsfile` | Pipeline: `Build` → `Test` → `Deliver` |
| `jenkins/scripts/deliver.sh` | Skrypt etapu `Deliver` (instalacja i uruchomienie JAR-a) |

## Uruchomienie lokalne

```shell
mvn -B verify                              # kompilacja + testy
java -jar target/my-app-1.0-SNAPSHOT.jar   # Hello World!
```

## Jenkins

`Jenkinsfile` wymaga agenta z etykietą `ubuntu` oraz skonfigurowanego narzędzia Maven o nazwie
`maven-apache-3.8.4` (*Manage Jenkins → Tools*). Jeśli używasz nowszego Mavena, zmień nazwę
w sekcji `tools` – projekt wymaga Mavena 3.9+ (sprawdza to `maven-enforcer-plugin`).

## CI

Workflow [`ci.yml`](.github/workflows/ci.yml) uruchamia `mvn verify` (JDK 21) oraz `shellcheck` skryptów.
