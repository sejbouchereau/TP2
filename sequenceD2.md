### Diagramme séquence: suggéré

```mermaid
sequenceDiagram
actor Bibliothécaire
    Bibliothécaire->>+Frontend: Enter code
    Frontend->>+Backend: Verify code

    alt
        Backend-->>Frontend: Valid code
        Frontend->>Backend: Verify if exists
        Backend->>+MongoDB: Verify similarities

        alt
        MongoDB-->>Backend: No similarities
        Backend-->>Frontend: Book doesn't exist
        Frontend->>Bibliothécaire: Request book info

        else
        MongoDB-->>-Backend: Similarities
        Backend-->>Frontend: Book exists
        Frontend->>Bibliothécaire: Error "Livre déjà existant"
        end
    else
        Backend-->>Frontend: Invalid code
        Frontend->>Bibliothécaire: Request book name
    end

    Bibliothécaire-->>Frontend: Enter book name
    Frontend->>Backend: Verify if exists
    Backend->>+MongoDB: Verify similarities

        alt
        MongoDB-->>Backend: No similarities
        Backend-->>Frontend: Book doesn't exist
        Frontend->>Bibliothécaire: Request book info

        else
        MongoDB-->>-Backend: Similarities
        Backend-->>Frontend: Book exists
        Frontend->>Bibliothécaire: Error "Livre déjà existant"
        end

    Bibliothécaire-->>Frontend: Enter book info
    Frontend->>Backend: Send book infos
    Backend->>+MongoDB: Add book to DataBase
    MongoDB-->>-Backend: Request succesful
    Backend-->>-Frontend: DataBase updated
    Frontend->>-Bibliothécaire: "Livre ajouté avec succès"
```
