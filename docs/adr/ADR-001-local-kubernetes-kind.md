# ADR-001: Lokalny klaster Kubernetes — kind

## Kontekst
Chciałem utworzyć lokalny klaster k8s w celu nauki. Nie posiadam fizycznego sprzętu, na którym mógłbym to testować z dowolnego miejsca, więc wybór padł na pracę z VM Ubuntu w Azurze. Technologie które rozważałem: kind, minikube i k3d. Minikube odrzuciłem ze względu na wysokie zużycie RAM (wymaga VM). K3d rozważałem jako alternatywę, ale kind jest używany do testowania samego Kubernetesa.

## Decyzja
Wybieram kind.

## Konsekwencje
✓ Lekki — nie obciąża Azure VM
✓ Multi-node support przez config YAML
✓ Używany przez core k8s team — wiarygodny sygnał w CV
✗ Mniej przyjazny dla początkujących niż minikube
✗ Brak wbudowanego dashboardu (używam k9s zamiast)
