# Zadatak 5: Tablični kalkulator

Tablični kalkulator sadrži tablicu polja koja mogu sadržavati ili konstantu ili matematički izraz. Matematički izrazi mogu referencirati vrijednosti drugih polja koja pak mogu ovisiti o vrijednostima trećih polja itd. Kad god se sadržaj nekog polja X promijeni potrebno je ponovo izračunati vrijednosti svih polja čiji izrazi neposredno ili posredno ovise o polju X.

Napišite programsko rješenje koje podržava zadavanje tablice s numeričkim konstantama i jednostavnim računskim izrazima (dovoljno je podržati zbrajanje s dva operanda), te ispisivanje njenog sadržaja. Rješenje mora omogućiti automatsko prosljeđivanje izmjena kroz proizvoljno dugačke lance ovisnosti. U slučaju kružnih ovisnosti, program treba baciti iznimku.

Upute:

- Polja tablice modelirajte primjercima razreda `Cell`.
- Neka polje čuva svoj sadržaj u tekstnom podatkovnom članu exp. Primjerice, sadržaj može biti `"5"` ili `"A1+A2"`.
- Neka polje čuva cacheiranu vrijednost sadržaja u numeričkom podatkovnom članu value.
- Neka tablica ima metodu `cell(ref)` koja dohvaća referencu na polje zadano tekstnom adresom ref. Npr. `sheet.cell("A1")` vraća polje na koordinatama `(0,0)`.
- Neka tablica ima metodu `set(ref, content)` koja sadržaj polja na adresi `ref` postavlja na tekst `content`.
- Neka tablica ima metodu `getrefs(cell)` koja vraća listu svih polja koja zadano polje referencira. Npr. ako vrijedi `cell.exp === "A3-B4"`, metoda treba vratiti polja na adresama `A3` i `B4`.
  - Uputa: slobodno koristite neku biblioteku koja podržava regularne izraze.
- Neka tablica ima metodu `evaluate(cell)`, koja izračunava numeričku vrijednost zadanog polja.
  - Uputa 1: radi jednostavnosti podržite samo zbrajanje, oduzimanje, množenje i dijeljenje.
  - Uputa 2: slobodno koristite neku biblioteku koja podržava izračunavanje izraza.
- Propagiranje promjena provedite na razini ćelija, bez prozivanja tablice, osim za izračunavanje novih vrijednosti izraza. Kako biste omogućili pozivanje metode evaluate, svaka ćelija treba imati referencu na matičnu tablicu.

Ispravnost vašeg programa možete isprobati sljedećim ispitnim programom:

```typescript
const main = () => {
  const s = new Sheet(5, 5);

  console.log();

  s.set("A1", "2");
  s.set("A2", "5");
  s.set("A3", "A1+A2");
  s.print();
  console.log();

  s.set("A1", "3");
  s.set("A4", "A1+A3");
  s.print();
  console.log();

  try {
    s.set("A1", "A3");
  } catch (e) {
    console.log(e);
    assert(e instanceof SheetRecursionError);
  }

  s.print();
  console.log();
};

main();
```
