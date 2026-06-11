# Praca domowa: Git zaawansowany

### Zadanie 1 -- Pierwszy konflikt merge (CLI + IntelliJ + GitHub)

**1. Jaki był hash merge commitu w wariancie A (CLI)? A w wariancie B (IntelliJ)? Czy są takie same?**
  * Wariant A: 167924b
  * Wariant B: c8cc6809

    Są różne, ponieważ każdy merge commit powstaje osobno i ma inny hash, to są dwie różne rzeczy.
    
**2. Jaką domyślną wiadomość commit wygenerował Git w wariancie A (CLI)? A IntelliJ w wariancie B?**
  * Wariant A: Merge branch 'feature/add-salad'
  * Wariant B: Merge branch 'main' into feature/add-pasta

**3. Kiedy najwygodniej rozwiązywać konflikt w UI GitHuba (wariant C), a kiedy lepiej zrobić to lokalnie?**

Najlepiej używać UI gitHuba wtedy kiedy konflikt jest niewielki, dotyczy małej liczby plików oraz gdy nie trzeba otiwerać projektu.
Lokalnie lepiej rozwiązywać konflikty, gdy zmian jest więcej, potrzeba jest uruchomienie projektu, odpalenie testów po zmianach.

**4. Wymień 2 powody, dla których IntelliJ 3-panel jest wygodniejszy niż edycja markerów ręcznie.**
  1. IntelliJ pokazuje 3 widoki (wersję lokalną, wersję z mergowanej gałęzi oraz wyniki końcowy) więc łatwiej jest zrozumieć konflikt. 
  2. Można wprowadzać zmiany używając przycisków IntelliJ'a zamiast ręcznie usuwać markery, co może powodować dalsze błędy.

**5. Załącz screenshot 3-panelowego narzędzia IntelliJ podczas rozwiązywania konfliktu.**
<img width="2012" height="854" alt="image" src="https://github.com/user-attachments/assets/0bb7a57c-5ade-4067-b7fe-b7059e314622" />
