# cv09: Sessions a prihlásenie (nepovinné)

Stránka týždňa: https://beata.stehlikova.website.tuke.sk/ti/10.html
Prijať zadanie: https://classroom50.org/tuke-fberg-stehlikova/technologie-internetu-5k/assignments/cv09/accept?k=tcc8jmx0

Téma je nepovinná a na cvičení sa nepreberá. Vysvetlenie, ukážky s náhľadmi a otázky na obhajobu sú na stránke týždňa. Prompty toto zadanie nemá, ukážky na stránke sú len časti files a zvyšok kódu dopĺňa autor aplikácie.

**Odovzdávaš** (v repository a vo svojom webovom priestore na sigma.tuke.sk v `ti/cv09/`; do `ti/projekt/` sa cv09 nenahráva):

- aplikáciu z cv08 doplnenú o registráciu, prihlásenie, odhlásenie a ochranu files, ktoré menia dáta
- `sql/schema.sql` s table `users`

**Hodnotenie:** téma je nepovinná, body sú za obhajobu. Aplikácia s registráciou, prihlásením, odhlásením a ochranou files, ktoré menia dáta, funguje vo svojom webovom priestore na sigma.tuke.sk v `ti/cv09/`, kód je v repository. Po push sa spustia testy (10 kontrol); zelený výsledok znamená, že files a požadované časti kódu sú na mieste, body udeľuje učiteľka po obhajobe.

## Files a ich roly

| File | Rola | Na čo nadväzuje |
|---|---|---|
| `db.php` | spoločný file: pripojenie k databáze a `session_start()` | cv07 |
| `signup.php` + `content/signup.php` | používatelia, formulár na nového používateľa, INSERT do `users` | `add-ENTITY.php` |
| `login.php` + `content/login.php` | používatelia, formulár na prihlásenie | |
| `login-check.php` | file bez stránky: overí heslo, zapíše do `$_SESSION`, redirect | `delete-LOOKUP.php` |
| `logout.php` | file bez stránky: zmaže údaje session, redirect | `delete-LOOKUP.php` |
| `login-required.php` | spoločný file: neprihláseného pošle na `login.php` | `header()` a `exit` |
| `template.php` | v menu meno a button Odhlásiť, alebo odkazy Prihlásiť a Registrácia | `$messages` |

## Úlohy

**10.1** `git clone` repository cv09 a prekopíruj aplikáciu z cv08:

```bash
rsync -a --exclude .git --exclude README.md cv08/ cv09/
```

Commit.

**10.2** Table `users` (ukážka 1): doplň ju do `sql/schema.sql` a spusti `schema.sql` a `seed.sql` v Adminer.

**10.3** `db.php` (ukážka 2): doplň `session_start()` pred vytvorenie `$pdo` a uprav komentár `// ROLA:`. Do `index.php` a `contact.php` doplň `require 'db.php';` ako prvý riadok. Over: v nástrojoch pre vývojárov je cookie `PHPSESSID`.

**10.4** `signup.php` s `content/signup.php` (ukážka 3): formulár meno, e-mail, heslo. Kontrola povinných hodnôt, kontrola, či e-mail už existuje, `password_hash`, INSERT, správa nad formulárom. Použi vymyslené heslo a e-mail s doménou `example.com`. Over v Adminer: v column `password_hash` je hash, heslo tam nie je. Commit.

**10.5** `login.php` s `content/login.php` (ukážka 4): formulár e-mail a heslo, `method="post"`, `action="login-check.php"`.

**10.6** `login-check.php` (ukážka 4): kontrola, že request je POST, SELECT používateľa podľa e-mailu, `password_verify`, pri neúspechu redirect na `login.php?msg=wrong`, pri úspechu `session_regenerate_id(true)`, zápis do `$_SESSION` a redirect na `index.php?msg=welcome`.

**10.7** `template.php` (ukážka 5): doplň keys `wrong`, `login`, `welcome` a `bye` do `$messages`. V menu vpravo meno a button Odhlásiť pre prihláseného, odkazy na `login.php` a `signup.php` pre neprihláseného. Over: prihlásenie so správnym heslom, s nesprávnym heslom, s neregistrovaným e-mailom. Commit.

**10.8** `logout.php` (ukážka 7): kontrola, že request je POST, zmazanie údajov session, redirect na `index.php?msg=bye`.

**10.9** `login-required.php` (ukážka 6). Pripoj ho hneď za `require 'db.php';` v `add-ENTITY.php`, `edit-ENTITY.php`, `delete-ENTITY.php`, `data.php`, `edit-LOOKUP.php` a `delete-LOOKUP.php`. Každý nový file má na začiatku komentár `// ROLA:`.

**10.10** Over bez prihlásenia: adresa `add-ENTITY.php` napísaná do prehliadača otvorí `login.php`. Over to isté po odhlásení. Commit a push. Upload Folder: `cv09` do `ti/cv09/`. Do `ti/projekt/` sa cv09 nenahráva.

## Obhajoba

Otázky a úlohy na obhajobu (Vysvetli, Uprav, Zdôvodni) a Definition of Done sú na stránke týždňa.

---

# cv09: Sessions and login (optional)

Week page: https://beata.stehlikova.website.tuke.sk/ti/10.html
Accept the assignment: https://classroom50.org/tuke-fberg-stehlikova/technologie-internetu-5k/assignments/cv09/accept?k=tcc8jmx0

The topic is optional and is not covered in the lab. The explanation, examples with previews and defence questions are on the week page. This assignment has no prompts; the examples on the page are only parts of files and the author of the application writes the rest of the code.

**You submit** (in the repository and in your web space on sigma.tuke.sk in `ti/cv09/`; cv09 is not uploaded to `ti/projekt/`):

- the application from cv08 extended with registration, login, logout and protection of the files that change data
- `sql/schema.sql` with the table `users`

**Grading:** the topic is optional, points are awarded for the defence. The application with registration, login, logout and protection of the files that change data works in your web space on sigma.tuke.sk in `ti/cv09/`, and the code is in the repository. Tests run after the push (10 checks); a green result means the files and the required parts of the code are in place, points are awarded by the teacher after the defence.

## Files and their roles

| File | Role | Builds on |
|---|---|---|
| `db.php` | shared file: database connection and `session_start()` | cv07 |
| `signup.php` + `content/signup.php` | users, form for a new user, INSERT into `users` | `add-ENTITY.php` |
| `login.php` + `content/login.php` | users, login form | |
| `login-check.php` | file without a page: verifies the password, writes into `$_SESSION`, redirect | `delete-LOOKUP.php` |
| `logout.php` | file without a page: deletes the session data, redirect | `delete-LOOKUP.php` |
| `login-required.php` | shared file: sends a user who is not logged in to `login.php` | `header()` and `exit` |
| `template.php` | in the menu the name and the button Odhlásiť (Log out), or the links Prihlásiť (Log in) and Registrácia (Sign up) | `$messages` |

## Tasks

**10.1** `git clone` the repository cv09 and copy the application from cv08:

```bash
rsync -a --exclude .git --exclude README.md cv08/ cv09/
```

Commit.

**10.2** The table `users` (example 1): add it to `sql/schema.sql` and run `schema.sql` and `seed.sql` in Adminer.

**10.3** `db.php` (example 2): add `session_start()` before `$pdo` is created and update the comment `// ROLA:`. Add `require 'db.php';` as the first line of `index.php` and `contact.php`. Verify: the developer tools show the cookie `PHPSESSID`.

**10.4** `signup.php` with `content/signup.php` (example 3): a form with name, e-mail and password. A check of required values, a check whether the e-mail already exists, `password_hash`, INSERT, a message above the form. Use a made-up password and an e-mail with the domain `example.com`. Verify in Adminer: the column `password_hash` holds a hash, the password is not there. Commit.

**10.5** `login.php` with `content/login.php` (example 4): a form with e-mail and password, `method="post"`, `action="login-check.php"`.

**10.6** `login-check.php` (example 4): a check that the request is POST, SELECT of the user by e-mail, `password_verify`, on failure a redirect to `login.php?msg=wrong`, on success `session_regenerate_id(true)`, writing into `$_SESSION` and a redirect to `index.php?msg=welcome`.

**10.7** `template.php` (example 5): add the keys `wrong`, `login`, `welcome` and `bye` to `$messages`. On the right of the menu the name and the button Odhlásiť for a logged-in user, links to `login.php` and `signup.php` otherwise. Verify: login with the correct password, with a wrong password, with an e-mail that is not registered. Commit.

**10.8** `logout.php` (example 7): a check that the request is POST, deleting the session data, a redirect to `index.php?msg=bye`.

**10.9** `login-required.php` (example 6). Include it right after `require 'db.php';` in `add-ENTITY.php`, `edit-ENTITY.php`, `delete-ENTITY.php`, `data.php`, `edit-LOOKUP.php` and `delete-LOOKUP.php`. Every new file starts with the comment `// ROLA:`.

**10.10** Verify without logging in: the address `add-ENTITY.php` typed into the browser opens `login.php`. Verify the same after logging out. Commit and push. Upload Folder: `cv09` to `ti/cv09/`. cv09 is not uploaded to `ti/projekt/`.

## Defence

The defence questions and tasks (Explain, Modify, Justify) and the Definition of Done are on the week page.
