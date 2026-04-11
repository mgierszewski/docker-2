# Instrukcja prezentacji i omówienia projektu Product Dashboard

## 1. Struktura projektu

```
docker/
├── backend/         # kod serwera Node.js/Express
│   ├── Dockerfile
│   ├── package.json
│   ├── server.js
├── public/          # statyczny frontend (HTML, CSS, JS)
│   ├── Dockerfile
│   ├── index.html
│   ├── products.html
│   ├── stats.html
│   ├── products.js
│   ├── stats.js
│   ├── style.css
│   ├── nginx.conf
├── docker-compose.yml
```

## 2. Omówienie architektury

- **public/** – statyczny frontend serwowany przez Nginx (HTML, CSS, JS)
- **backend/** – API Node.js/Express (GET/POST /items, GET /stats)
- **docker-compose.yml** – uruchamia oba serwisy w osobnych kontenerach, łączy je w jednej sieci

## 3. Budowanie i uruchamianie

1. Budowanie obrazów:
   ```
   docker compose build
   ```
2. Uruchamianie środowiska:
   ```
   docker compose up -d
   ```
3. Sprawdzenie działania:
   - http://localhost/ (strona główna)
   - http://localhost/products.html (lista produktów)
   - http://localhost/stats.html (statystyki)
   - http://localhost/api/stats (API statystyk)

## 4. Funkcjonalności

- **Frontend:**
  - 3 podstrony: index.html, products.html, stats.html
  - Lista produktów pobierana z API, możliwość dodania produktu
  - Statystyki: liczba produktów, ID instancji backendu, producenci, kategorie
- **Backend:**
  - REST API: GET/POST /items, GET /stats
  - Dane trzymane w pamięci (na potrzeby demo)
- **Nginx:**
  - Serwuje pliki statyczne
  - Proxy /api/ do backendu
  - Cache na /api/stats (30s), nagłówek X-Cache-Status

## 5. Konteneryzacja i rejestr

- Oba obrazy można otagować jako latest i v1, wypchnąć do Docker Hub
- Po usunięciu lokalnych obrazów i zmianie docker-compose.yml na image: myuser/docker-frontend:latest itd., środowisko uruchamia się wyłącznie z rejestru

## 6. Typowe pytania i odpowiedzi

- **Dlaczego public i backend osobno?**
  - Rozdzielenie kodu serwera i plików statycznych to dobra praktyka (bezpieczeństwo, porządek, łatwiejsze wdrożenia)
- **Jak działa cache w Nginx?**
  - Endpoint /api/stats jest cache'owany na 30s, nagłówek X-Cache-Status pokazuje HIT/MISS
- **Jak dodać nową funkcję?**
  - Frontend: edytuj pliki w public/
  - Backend: edytuj pliki w backend/, przebuduj obraz backendu
- **Jak uruchomić projekt na czysto?**
  - Usuń lokalne obrazy, pobierz z rejestru, uruchom docker compose up -d

## 7. Przykładowy przebieg prezentacji

1. Pokazanie struktury katalogów
2. Omówienie plików Dockerfile, docker-compose.yml, nginx.conf
3. Budowanie i uruchamianie środowiska
4. Pokazanie działania aplikacji (strony, dodawanie produktu, statystyki, cache)
5. Odpowiedzi na pytania

---

Masz gotowy przewodnik do prezentacji projektu krok po kroku!
