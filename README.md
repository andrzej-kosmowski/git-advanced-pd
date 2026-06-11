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
--
### Zadanie 2 -- Konflikt na rebase zamiast merge

**1. Jak wygląda git log --graph --oneline --all po rebase? Załącz screenshot.**
<img width="824" height="97" alt="image" src="https://github.com/user-attachments/assets/dd0c227f-dd53-49f4-b4a4-d39ed383ac64" />

**2. Jaka jest różnica w historii między rozwiązaniem przez merge (zad. 1) a rebase (zad. 2)?**

Przy merge historia pokazuje osobne gałęzie oraz merge commit, który łączy zmiany

Przy rebase git przenosi commit jakby był świeży, przez co historia jest prosta i nie ma merge commita.

**3. Dlaczego po rebase trzeba użyć git push --force-with-lease? Co by się stało gdybyś użył zwykłego git push?**

Po rebase zmienia się historia gałęzi, ponieważ Git tworzy nowy commit z nowym hashem. Remote nadal ma starą wersję commita,
więc zwykły git push zostanie odrzucony, ponieważ Git nie pozwala domyślnie nadpisać historii na zdalnym repozytorium.

**4. Czym różni się --force-with-lease od --force? Kiedy używać którego?**

--force nie sprawdza czy ktoś w międzyczasie nie dodał swoich commitów, nadpisą gałąź mimo wszystko // Niebezpieczne!

--force-with-lease - sprawrdza historię i nadpiszę gałąź tylko jeśli historia jest taka sama 

**5. Co robi git rebase --abort? Kiedy chcesz tego użyć?**

Przerywra rebase i przywraca branch do stanu przed jego zaczęciem. Używam go kiedy rozwiązanie poszło w złym kierunku i chce zacząć jeszcze raz od punktu startowego
--
### Zadanie 3 -- Git Stash w sytuacji "pilny hotfix"

**1. Jaka jest różnica między git stash pop a git stash apply? Kiedy chcesz użyć którego?**

 * pop - przywraca zmiany ze stasha i je usuwa z listy - używamy gdy wiemy, że już się nie przyda
 * apply - przywraca zmiany ze stasha i je zostawia w stashu - używamy gdy chce tylko skopiować zmiany albo użyć go jeszcze w przyszłości

**2. Co się dzieje gdy masz 2 stashe i robisz git stash pop? Który zostanie wyciągnięty?**

Jeśli nie podamy konkretnego ID stasha to wyciągnie najnowszy z **stash@{0}**

**3. Dlaczego git stash domyślnie nie chowa untracked files? Kiedy to jest problem?**

Ponieważ nie są śledzone przez gita, zostają one tylko w katalogu roboczym. Może to być problem kiedy chcemy wyczyścić working tree przed zmianą brancha, a zmiany dalej istnieją.

**4. Czy stash idzie na remote po git push? Sprawdź na GitHubie -- czy widzisz tam stashe?**

Nie, ponieważ stash jest lokalny. Nie jest wypychany do remote repo.

**5. Załącz screenshot git stash list z momentu, gdy miałeś 2 stashe.**

<img width="400" height="54" alt="image" src="https://github.com/user-attachments/assets/50d7e186-e36f-47da-8536-b58f233d2fb6" />
