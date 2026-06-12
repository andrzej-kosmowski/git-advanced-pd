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

---
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

---

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

---

### Zadanie 4 -- Cherry-pick: przeniesienie commita między gałęziami

**1. Jaki był hash oryginalnego commita na feature/A? Jaki na main po cherry-pick? Załącz oba git log --oneline.**

 * main po cherry-pick: 943df06
 * oryginalny z feature/A: 9887cc8

**2. Dlaczego hash jest różny, jeśli treść (diff) jest identyczna? (Wskazówka: parent commit, timestamp.)**

Cherry-pick tworzy nowy commit na aktualnej gałęzi, dlatego otrzymuje nowy hash. Git traktuje go jako nowy obiekt, mimo że zawartość zmian jest identyczna.

**3. Co zawiera app.txt na main po cherry-pick (która sekcja jest wypełniona, a które mają nadal [TODO ...])? Czego tam nie ma?**

Po wykonaniu cherry-pick na gałęzi main wypełniona jest tylko sekcja B:

```
Linia 1: początek

=== Sekcja A ===
[TODO A]

=== Sekcja B ===
Sekcja B: ważna zmiana w feature/A (commit 2)

=== Sekcja C ===
[TODO C]
```

Na gałęzi main nie ma zmian z:

* commita 1 (Sekcja A)
* commita 3 (Sekcja C)

**4. Co się dzieje, gdy cherry-pick wywoła konflikt? Jak go rozwiązać (analogia do merge/rebase)? Eksperyment: spróbuj cherry-pickować trzeci commit (zmiana sekcji C) -- czy też przejdzie bezkonfliktowo? Dlaczego?**

Procedura rozwiązania jest bardzo podobna do merge lub rebase:
1. Otworzyc edytor
2. usunąc markery
3. Poprawić wersje
4. dodac pliki - git add
5. cherry-pick --continue

**5. Kiedy używać cherry-pick zamiast merge?**

Wtedy kiedy chcemy przenieść tylko konkretny commit bez łączenia całej gałęzi

---

### Zadanie 5 -- In teractive Rebase: porządkowanie historii przed PR

**1. Jaka jest różnica między squash a fixup? (Wskazówka: co dzieje się z wiadomością commit?)**

* squash - łączy commit z poprzednim oraz pozwala edytować wiadomość commita
* fixup - też łączy ale odrzuca edytowanie wiadomości commita

**2. Dlaczego po git rebase -i musisz użyć git push --force-with-lease? Co by się stało gdybyś użył zwykłego git push?**

Ponieważ tworzy nową historię brancha, mogą być różne wiadomości commitów etc. 
Git push zostanie odrzucony, ponieważ historia lokalna różni się od tej na gh

**3. Co zrobi się złego, jeśli zrobisz rebase -i na main współdzielonym z zespołem?**

Można przepisać historię całego brancha przez co inni będą mieli różne hashe lokalnie i remota. Git push może przestać działać, mogą powstać duplikaty. Repo będzie ciężkie do uporządkowania

**4. Załącz screenshot git log --oneline przed rebase i po rebase.**

 * Przed:

   <img width="942" height="136" alt="image" src="https://github.com/user-attachments/assets/29fd55e6-9ef1-4386-ab24-fc0bf4a4463c" />
   
 * Po:

   <img width="449" height="90" alt="image" src="https://github.com/user-attachments/assets/5dcae519-d147-43d5-929e-ab50464dce42" />

**5. Co robi drop -- usuwa zmiany z plików czy tylko z historii? Sprawdź zawartość NOTES.txt po rebase.**

drop usuwa zmiany oraz historię, w tym przypadku po rebase plik NOTES.txt nie istnieje

---

### Zadanie 6 -- Reflog: odzyskanie po reset --hard

**1. Jak długo żyją wpisy reflog? (Wskazówka: zobacz git config gc.reflogExpire.)**

Domyślnie wpisy reflog ok 90 dni, a wpisy dot. commitów nieosiągalnych ok 30 dni.

**2. Czy reflog idzie na remote po git push? Sprawdź: zaloguj się na GitHubie i sprawdź, czy widzisz tam reflog.**

Nie. Reflog jest lokalny i nie idzie na GH po pushu

**3. Jak rozpoznać w git reflog, który HEAD@{N} to "przed pomyłkowym resetem"?**

Po błędnym resecie w reflogu pojawia się wpis podobny do: HEAD@{0}: reset: moving to HEAD~2

Stan sprzed resetu jest zwykle jeden wpis niżej, np.: HEAD@{1}: commit: Commit C

**4. Czy reflog uratuje Cię, gdy: (a) przypadkowo rm -rf na całym katalogu repo? (b) przypadkowo git reset --hard ale jeszcze przed pushem? (c) usunąłeś gałąź lokalnie, ale była tylko lokalnie?**

a) Nie, jeśli usunięty został cały katalog repozytorium razem z folderem .git.

b) Tak. To jest typowy przypadek użycia reflog.

c) Tak, jeżeli commit tej gałęzi nadal znajduje się w reflogu i nie został jeszcze usunięty przez garbage collection.

**5. Załącz screenshot git reflog po reset i po recovery.**

 * Po reset

   <img width="536" height="83" alt="image" src="https://github.com/user-attachments/assets/2145a52f-ef77-4330-8874-39bcaa7ae57e" />

* Po recovery

  <img width="547" height="137" alt="image" src="https://github.com/user-attachments/assets/dac29aa6-6c35-477f-86fb-eacd7a129238" />

---

### Zadanie 7 -- Bisect: binarne polowanie na buga

**1. Ile kroków potrzebował bisect, żeby znaleźć buga? Jak ta liczba ma się do log₂(8) = 3?**

Około 3 więc, zgadza się z teorią działania wyszukiwania binarnego.

**2. Hash i wiadomość złego commita -- skopiuj z konsoli.**

```
5da57be6ea60c457b3f64de5cf652668e20411c9 is the first bad commit
commit 5da57be6ea60c457b3f64de5cf652668e20411c9
Author: Andrzej <bazylek11@gmail.com>
Date:   Thu Jun 11 15:00:06 2026 +0200

    feat: multiply method

 Calc.java | 4 ++++
 1 file changed, 4 insertions(+)

```

**3. Kiedy bisect jest lepszy niż git log + git diff?**

git log oraz git diff są przydatne, gdy znamy przybliżone miejsce problemu lub chcemy ręcznie przeanalizować historię zmian.

git bisect jest lepszy, gdy:

* repozytorium zawiera dużo commitów
* nie wiadomo, który commit wprowadził błąd
* można łatwo określić, czy dany commit jest „good” czy „bad”
* chcemy szybko znaleźć regresję

**4. Co robi git bisect run <skrypt>? Jakie kody wyjścia ma rozumieć skrypt?**

automatyzuje proces oznaczania commitów jako dobrych lub złych. Git uruchamia skrypt dla kolejnych commitów i na podstawie kodu wyjścia decyduje, czy commit jest poprawny.

```
0 -> good
1-127 (poza 125) -> bad
125 -> skip
```

**Co zrobić, jeśli któryś commit się nie kompiluje podczas bisect i nie da się ocenić? (Wskazówka: git bisect skip + exit 125 w bisect run.)**

należy go pominąć.

Ręcznie:
```
git bisect skip
```
Automatycznie w git bisect run:
```
exit 125
```
Przykład:
```
javac Calc.java 2>/dev/null || exit 125
```

---

### Zadanie 8 -- Reset (3 tryby) vs Revert

**1. Wypełnij tabelę:**

| Tryb	| git status po reset |	Zawartość pliku w working dir |	Czy zmiany w staging? |
| --- | --- | --- | --- |
| --soft	| Changes to be committed	| Wersja C	| Tak |
| --mixed	| Changes not staged for commit	| Wersja C	| Nie |
| --hard	| nothing to commit, working tree clean	| Wersja B	| Nie |

**2. Dlaczego git revert jest bezpieczny dla zespołu, a git reset --hard na pushowanym branchu nie?**

git revert nie usuwa historii. Tworzy nowy commit, który odwraca zmiany z wcześniejszego commita.

**3. Po git reset --hard -- czy stracone commity są usunięte z dysku? Jak je odzyskać?**

Nie od razu. Commity zwykle nadal istnieją lokalnie przez jakiś czas, tylko branch już na nie nie wskazuje.
Można je odzyskać przez reflog

**4. Kiedy chcesz zrobić --soft zamiast --mixed?**

--soft jest przydatny, gdy chcę cofnąć commit, ale zostawić jego zmiany od razu przygotowane do kolejnego commita.

**5. Załącz screenshot git log --oneline po git revert HEAD -- czy oryginalny Commit C jest jeszcze w historii?**

<img width="379" height="86" alt="image" src="https://github.com/user-attachments/assets/549fcb07-d651-43c6-8422-4250fd37a86b" />

---

### Zadanie 9 -- Feature branch + PR z konfliktem (GitHub flow)

**1. Po co w ogóle pracować na osobnej gałęzi feature/... zamiast commitować bezpośrednio na main?**

Osobna gałąź pozwala pracować nad zmianą bez psucia stabilnej wersji projektu na main.

**2. Kiedy używasz git fetch origin + git merge origin/main, a kiedy git fetch origin + git rebase origin/main? Jak to wpływa na historię?**

**3. Jaka jest różnica między Squash and merge, Create a merge commit i Rebase and merge w UI GitHuba?**

**4. Dlaczego po lokalnym git rebase origin/main musisz pushować --force-with-lease (zamiast zwykłego --force)?**

Po rebase Git tworzy nowe wersje commitów z nowymi hashami. Lokalna historia gałęzi feature/dodaj-todo różni się wtedy od tej, która jest już na GitHubie.

**5. Wymień 3 dobre praktyki przy zgłaszaniu PR (commit messages, opis, rozmiar PR, code review).**

 * Pisać czytelne wiadomości commitów i tytuł PR-a, np. feat: oznacz zadanie 1 jako zrobione.
 * Dodać opis PR-a: co zostało zmienione, dlaczego i jak to sprawdzić.
 * Robić małe PR-y, które łatwo przejrzeć w code review.

---

### Zadanie 10 -- Śledztwo: kombinacja technik (samodzielne)

1. Problem (a) -- "stracone" commity:

 * Jakie narzędzie użyłeś?
   - git reflog
 * Co dokładnie zaobserwowałeś (jaki output)?
   - git log --oneline pokazywał tylko Commit 1, Commit 2 oraz późniejsze commity, a Commit 3 i Commit 4 zniknęły z aktualnej historii
 * Jak rozwiązałeś (pełna komenda CLI lub opis kliknięć w IntelliJ)?
   - git reset --hard HEAD@{12}

2. Problem (b) -- bug w jednym z 8 commitów:

 * Jakie narzędzie użyłeś?
   - git bisect
 * Ile kroków potrzebowałeś?
   - 3 
 * Hash złego commita.
   - a789fa7 feat: dodaj absoluteValue (commit B5)
 * Jak rozwiązałeś?
   - git bisect start
   - git bisect bad
   - git bisect good 

3. Problem (c) -- niedokończone zmiany + merge gałęzi kolegi:

 * Jakie narzędzie użyłeś?
   - git stash -u
 * Co stało się z wip.txt po Twoich akcjach?
    - git stash -u / Dzięki temu wip.txt został tymczasowo schowany razem z untracked files.
 * Jak wyglądała kolejność komend?
    - git status
    - git stash push -u -m "WIP: moja niedokończona praca"
    - git merge colleague/finished-feature
    - git stash pop
    - git add wip.txt
    - git commit -m "feat: add saved WIP note"
    - git push

