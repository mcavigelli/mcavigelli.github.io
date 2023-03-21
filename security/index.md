
## Rollen und Bezeichnungen


### Authentication


Pass Check an der Reception
Resultat: Schlüssel mit welchem ich mein Zimmer und das Hallenbad öffnen kann.

#### Claims

Persönliche Informationen
Auch im Pass drin, vom Rezeptionisten überprüft


### Architektur

- viele Web APIs
- Identityprovider: enthält Claims zum User implementiert
  OAuth2 und OpenIdConnect
  z.B. Google Applications, Microsoft Applications

Verschiedene Anwendungen **trauen** dem Identityprovider. SSO

#### Provider (die Regierung)

* Produkte Azure AD, Google selber machen.
* Für spezielle Anforderungen => selber machen


Pass ist gesichert mit Hologramm, Stempel. Damit Hotelangestellter von der Regierung die Vertrauenswürdigkeit des Passes überprüfen kann.

Hotel und ich vertrauen der Regierung.

Ich vertraue der Regierung und die Frontendanwendung ebenfalls.

min 12:
ID Provider schützt Resourcen und stellt diese bereit.
2 Formen
- Identifty Resource (Claims)
- API Resource in meinem Namen
  Ich stimme zu, dass in meinem Namen Daten gelesen werden.
   

Ich logge mich beim ID Provider ein, es gibt ein Token zurück. Client kann Token verifizieren.

2 Tokens, synonym mit Resourcetypen
- Identity mit Claims: wer das ist, User
- Access Token Hotelschlüssel

jwt Token
- header
- body
    - iss: issuer des Tokens (Identity Provider)
    - sub: Subject Identityprovider, identifiziert mich als User
-

OAuth: spezifiert ausschliesslich Access Tokens
OpenIdConnect: hängt Identity Tokens dran

Wenn Frontend Application einen Zugriff ohne Token entdeckt, gibt es eine Umleitung zum Identity Provider.

Client hat auch eine Identifikation mit einem Secret

Scopes: bundles of claims, was ich versuche zu erhalten
        Identityprovider überprüft das: habe ich die Admin Rolle, zb.?

18:54
Redirect URI: dorthin soll Anwendung weitergeleitet werden. Wird konfiguriert beim ID-Provider, sicherheit.
ResponseType sagt, was der ID Provider zurückgeben soll.

2 Bildschirme: login, Disclosure zum client

Demo: 20min

Client-app localhost:5001

   => Umleitung localhost:5000 (IdentityServer4)
      weil net eingeloggt
   => Einloggen
   => Consent screen (ConfArch fragt bei IDServer4 an, ob Daten weitergegeben werden dürfen) API von ConfArch wird persönliche Informationen erhalten.




Begriffe

 * Authentication: Wer bin ich, wird mit OpenIdConnect
   abgedeckt (AuthN)
   Ich melde mich an der Rezeption mit meinem Pass.

 * Authorization: Welche Rechte habe ich und welche Daten
   darf ich lesen. (AuthZ)
   Mit dem Hotelschlüssel kann ich in mein Zimmer und in das Hallenbad eintreten.

* Claims: Name, EmployeeNo
  Im Pass steht mein Geburtsdatum. Es wird vom Rezeptionisten überprüft.

* Identity Provider: ein neues Kind in der API Umwelt
  Speichert persönliche Informationen zu einem User.

* SSO: Ich melde mich 1x an bei Google und kann diese Daten für Kalender und E-Mail verwenden.

* Clients hat Users, brauchen Authentication.


## Vertrauen

Die Regierung gibt ausschliesslich einen Pass heraus, wenn ich ihr das erlaube. Andere Leute dürfen bei der Regierung nicht nach Daten von Benutzer "Roland" nachfragen, ausser Roland hat die Regierung dazu ermächtigt.

Das Hotel vertraut der Regierung, dass die Daten im Pass korrekt sind.

## ZF

OpenIdConnect mit Authentication basiert auf OAuth
OpenIdConnect ist aber logisch gesehen der erste Schritt


## Demo

Der Client fragt um Erlaubnis, ein API in meinem Namen anzufragen. Das API wird meine persönlichen Informationen erhalten.

## Sources


https://app.pluralsight.com/course-player?clipId=9070dc42-d038-491f-a7a5-eae904549ec9

Roland Gujit

https://de.wikipedia.org/wiki/OAuth#/media/Datei:Authorization-Code-Grant-Flow.png