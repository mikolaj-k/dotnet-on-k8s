# ADR-003: Argo CD for Gitops
## Status
Accepted (maj 2026)
## Kontekst
Usprawnienie deploymentu aplikacji oraz uspójnienie procesu tak, aby posiadł tylko jedno źródło prawdy w kodzie. Dotychczas ręczne wywoływanie helm upgrade było mało optymalne, czasochłonne i przy rozroście aplikacji podatne na błędy. Rozważałem Flux (bardziej CLI-first, używany przez GitLab) oraz Argo CD (UI, popularny w enterprise, dojrzały).
## Decyzja
Wybieram Argo CD.
## Konsekwencje
✓ UI
✓ Dojrzały produkt
✓ Repozytorium jako jedyne źródło prawdy
✗ Dodatkowe komponenty w klastrze do utrzymania
✗ Dla małego projektu nadmiarowe
