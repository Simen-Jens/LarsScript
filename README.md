## Hvordan bruke LarsScript?
https://discordapp.com/oauth2/authorize?client_id=353241122593832962&scope=bot&permissions=0
</br>
</br>
Botten reagrer på mentions (@LarsScript) etterfulgt av en kodeblokk:</br></br>

@LarsScript#3640
```
si("hei")
```

</br>
</br>

Man kan også tilordne nøkkelord til botten:</br></br>
@LarsScript#3640 assign to si hei
```
si("hei")
```
Med dette vil botten evaluere nøkkelordet hvergang det blir nevnt i guilden:</br>
<img align="center" src="https://puu.sh/xpHCk/828a407070.png"/>

## Hvordan skrive LarsScript?
* Ingen desimaltall, Lars er ikke så punktelig.</br>
*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; lovelig eksempel:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`kontobalanse er 1` </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  ulovelig eksempel:&nbsp;&nbsp;&nbsp;`kontobalanse er 1.1`*</br>

* Import setninger er ikke lovelig, Lars bruker kun sin egen kode. </br>
* Lars bruker ikke `True` eller `False` han bruker `tja` og `nei` (`tja` vil tilfeldig bli satt til `True` eller `False` (**OBS!** dette gjelder forøverig ALLE evalueringen som evaluerer til `True`, de vil ha en 50% sjansje for å bli `False`))</br>
*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; lovelig eksempel:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`EØS er tja` </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  ulovelig eksempel:&nbsp;&nbsp;&nbsp;`EØS er True`*</br>

* Feilmeldinger er oppskryt, Lars vet ikke hva han gjorde feil derfor finnes ikke dette. (Dersom man ønsker å la brukeren skape feil kan man bruke den innebygde avtalen `KlikkIVinkel(melding)`)</br>

* Istedenfor `return` bruker vi `gi unnskyldning:`, når Lars har sagt han skal gjøre en avtale kan han komme opp med en unnskyldning for å bryte ut av avtalen.</br>
*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; lovelig eksempel:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`gi unnskyldning: tja` </br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  ulovelig eksempel:&nbsp;&nbsp;&nbsp;`return True`*</br>

* En funksjonsdefinisjon starter med nøkkelordet `avtale`, alle funksjoner fungerer som avtaler for Lars. De er derfor også primitive verdier og kan byttes ut med andre primitive verdier slik som tall og tekst når som helst. </br>
*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; lovelig eksempel:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*
```
avtale spilleLeague(medVenner){
    dersom ikke medVenner er ingenting?{
        KlikkIVinkel("Brukerfeil! avtalen spilleLeague() ble tilsendt venner, dette stemmer ikke. Lars har ingen venner")
    } ellers{
        gi unnskyldning: "Kan ikke spille uansett, må vaske bilen til dama"
    }
}
```
</br>

## Gramatikk
Gyldige primitive verdier:
* nøkkeordet `ingenting`, dette er den atomære verdien for ingenting altså `null`
* boolskeverdier, `tja` og `nei`
* heltallsverdier, altså  ℤ {..., -3, -2, -1, 0, 1, 2, 3, ...}
* tekststrenger, **MERK:** tekstnotasjon benytter dobbelt anførselstegn (`"Nettet er helt Afrika atm"`)
* lister, definieres ved bruk av `[]` - *eks: `fagBestått er []`*
* hashmaps, definieres ved bruk av `{}` - *eks: `myAccomplishments er {"å ha dame": tja, "å ha venner": nei}`*
* avtaler (funksjoner)


Aritmetiske operasjoner:
* `+` gjør addisjon
* `-` gjør substraksjon
* `*` gjør multiplikasjon
* `/` gjør divisjon
* `>` / `større` evaluerer to uttrykk mot hverandre med `greater than` utsagnet
* `<` / `mindre` evaluerer to uttrykk mot hverandre med `lesser than` utsagnet
* `%` gjør modulo

Flyt i språket:
* `()` definerer sammensatte setninger
* `{}` definerer skop, slik som i Java
</br></br>
* `ikke` evaluerer til det samme som `not`
* `og` evaluerer til det samme som `and`
* `eller` evalueres til det samme som `or`
</br></br>
* `dersom` / `ellerkanskje` / `ellers` evalueres respektivt til `if` / `else if` / `else`
* `mens` evalueres til `while` (`do while`, `for` og `for each` finnes ikke ettersom disse løkkene er for vanskelig for Lars)
</br></br>
* `er` fungerer både for sammenligning og tilordning (både `==` og `=`)
* for sammenligning skal man som nevnt bruke `er`, men et sammenligningsuttrykk må ende med `?` (dette gjelder forøvering alle sammenligningsuttrykk `>=` / `<` osv.)</br>
*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; lovelig eksempel:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;*
```
antallVenner er 0
dama er "alt jeg har"
dersom antallVenner er 0 og dama er "alt jeg har"?{
    si("alt er ok")
} ellers {
    KlikkIVinkel("?????")
}
```
</br>

* for å oppnå prosedyrebasert objektorientering i LarsScript trenger vi en måte å få skrivetilgang til ikkelokale variabler (`nonlocal` i python `.` i Java). Dette løses elegant ved at Lars hadde tilgang til variabelen når den var i `pre-alpha`, vi kan dermed få skrivetilgang til variabler utenfor vårt eget skop med å bruke `pre-alpha` nøkkelordet.</br>
*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; eksempel:*
```
avtale vaskeBilenTilDama(){
    såpemerke er "den dama liker best"
    avtale byttSåpe(){
        pre-alpha såpemerke er "dama fant en hun likte bedre"
    }
}
```
</br>

## Innebygd bibliotek i LarsScript
* **tenke(String)** - ber om input fra bruker og gir dette tilbake som en unnskyldning
* **si(String)** - printer informasjon til skjermen
* **antall(val)** - returnerer lengden av en tekststreng eller antall elementer i en liste
* **teksten(val)** - gir tilbake `.toString()` av verdien
* **KlikkIVinkel(String)** - kaster en feilmelding (Lars lager ikke egne feilmeldinger)
