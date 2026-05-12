# ADR-002: Helm
 
## Kontekst
 
Usprawnienie procesu deploymentu → uniknięcie wywoływania komendy `kubectl apply -f` dla każdego pliku osobno. Do wyboru miałem narzędzia typu Helm, Kustomize lub surowy YAML. Helm wybrałem z powodu jego popularności względem Kustomize, który bardziej odpowiada do deploymentu jednej aplikacji na wiele platform. Dodatkowo znacznie przyspiesza on pracę w porównaniu z pisaniem YAMLi ręcznie.
 
## Decyzja
 
Wybieram Helm.
 
## Konsekwencje
 
- ✓ Jedna komenda zamiast wielu `kubectl apply`
- ✓ Parametryzacja przez `values.yaml`
- ✓ `helm rollback` przy błędach
- ✗ Nowa składnia `{{ }}` do nauki
