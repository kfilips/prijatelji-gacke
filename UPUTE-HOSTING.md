# Upute za objavu stranice i uređivanje sadržaja

Stranica se sastoji od statičnih HTML/CSS datoteka plus panela za uređivanje
(`/admin`) preko kojeg tajnik može mijenjati vijesti, statistike i vremensku
crtu aktivnosti bez ikakvog znanja programiranja.

Da bi panel za uređivanje radio, stranica mora biti na **GitHubu i Netlifyju
zajedno** (Netlify se spaja na GitHub repozitorij i preko njega provjerava
tko smije uređivati sadržaj). Netlify Drop (samo povlačenje datoteka) ovdje
nažalost ne radi jer tada nema GitHub repozitorija na koji se spremaju izmjene.

## Korak 1 — GitHub repozitorij
1. Napravi besplatan račun na github.com.
2. Novi repozitorij, npr. `prijatelji-gacke`.
3. Ubaci SVE datoteke i mape iz ovog paketa (uključujući `data/` i `admin/`) u repozitorij (Add file → Upload files).

## Korak 2 — Netlify hosting
1. Besplatan račun na netlify.com, poveži ga s GitHub računom.
2. "Add new site" → "Import an existing project" → odaberi repozitorij `prijatelji-gacke`.
3. Nema potrebe za posebnim build naredbama (ostavi prazno) — objavi.
4. Netlify da adresu tipa `prijatelji-gacke.netlify.app` (može se kasnije zamijeniti pravom domenom).

## Korak 3 — Uključi Identity i Git Gateway (jednom, u Netlify sučelju)
1. U Netlify sučelju za tu stranicu: **Site configuration → Identity → Enable Identity**.
2. **Identity → Registration preferences** → postavi na "Invite only" (da se stranica ne otvori bilo kome).
3. **Identity → Services → Git Gateway** → Enable Git Gateway.
4. **Identity → Invite users** → upiši e-mail tajnika. Tajnik dobije e-mail s pozivnicom i postavi lozinku.

## Korak 4 — Tajnik uređuje sadržaj
1. Tajnik otvori `https://<adresa-stranice>/admin/`.
2. Prijavi se e-mailom i lozinkom iz pozivnice.
3. Vidi tri jednostavne forme:
   - **Naslovna – aktualne vijesti** (dvije kartice na početnoj stranici)
   - **Vremenska crta aktivnosti** (dodavanje/uređivanje/brisanje događaja)
   - **Brojke na naslovnici** (tri statistike)
4. Uredi tekst, klikne "Publish" (Objavi) — promjena je vidljiva na stranici za par minuta.

Ostale stranice (O nama, Rijeka Gacka, Uključi se) trenutno nisu povezane na
ovaj panel jer je njihov sadržaj rjeđe promjenjiv. Ako ih tajnik treba često
mijenjati, mogu se naknadno dodati u isti panel na isti način — javi pa se
proširi `admin/config.yml` i pripadajuće `data/*.json` datoteke.

## Alternativa bez panela — izravno uređivanje na GitHubu
I bez CMS panela, tekst na bilo kojoj stranici (npr. `o-nama.html`) može se
promijeniti tako da se datoteka otvori na github.com, klikne ikona olovke
("Edit this file"), promijeni tekst unutar HTML oznaka i spremi (commit).
Ovo zahtijeva malo pažnje da se ne obrišu HTML oznake `<...>` oko teksta.

## Pristupnica (učlanjenje)
Dugme "Postani član" na stranici "Uključi se" vodi na
`pristupnica-udruga-prijatelji-gacke.pdf` — pravi ispunjivi PDF obrazac
(polja za ime, adresu, OIB, kontakt, izjavu i potpis). Zainteresirani ga
preuzmu, ispune u PDF čitaču ili rukom nakon ispisa, i pošalju e-mailom ili
donesu osobno. Nema potrebe za dodatnim servisom. Ako se polja trebaju
promijeniti, javi pa se PDF prilagodi.

## Kontakt forma
Forma na stranici "Uključi se" već radi bez ikakve registracije — koristi
besplatnu uslugu **FormSubmit.co**, koja šalje poruke izravno na
`info@prijateljigacke.hr`. Ništa dodatno nije potrebno postaviti.

Jedino što treba znati:
- Prva poruka poslana s obrasca aktivira adresu — FormSubmit će na
  `info@prijateljigacke.hr` poslati jedan potvrdni e-mail (potrebno je
  kliknuti poveznicu u njemu jednom, nakon čega sve buduće poruke stižu
  automatski).
- Ako se e-mail udruge ikad promijeni, potrebno je u `ukljuci-se.html`
  zamijeniti adresu na dva mjesta: u `action="https://formsubmit.co/..."`
  i u skrivenom polju `_next` (poveznica na koju se korisnika vrati nakon
  slanja).

## Prije objave provjeriti
- E-mail `info@prijateljigacke.hr` u svim stranicama — zamijeni stvarnim ako nije aktivan.
- Poveznica na Facebook stranicu i na peticiju (peticijeonline.com).
- `data/*.json` datoteke već sadrže trenutne, stvarne podatke — tajnik ih samo ažurira ubuduće preko `/admin`.
