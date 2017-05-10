# Workflow

[Account, Session, Device, Emailaddress](https://docs.google.com/drawings/d/1-QnX8rlFUci4HFzOHGL82krMHvPAlO8wqFM7jyKxHGQ/edit?usp=sharing)


## Account erstellen

Man kann einen Account erstellen (1), diesem wird eine aktuell gültige Session erstellt (2) von welcher der `sessionhash` zurückgegeben wird:

http://2x.dragonjsonserver.de/?namespace=Account&method=createAccount&data=%7B%7D


## Authentifizierung verknüpfen

Mit dem `sessionhash` kann man den Account verschiedenen Authentifizierungsarten verknüpfen.


### Device

`device` wäre ein Smartphone oder eine Setop Box, je nach Device können unterschiedliche Credentials herangezogen werden um ein Device eindeutig identifizieren zu können (im einfachsten Fall ein eindeutiger token wie im Beispiel mit `platform browser` und `credential browser_id`) (3):

http://2x.dragonjsonserver.de/?namespace=Device&method=createDevice&data=%7B%22platform%22%3A%22browser%22%2C%22credentials%22%3A%7B%22browser_id%22%3A%22token%22%7D%2C%22sessionhash%22%3A%2214d93820d172931a7efe4d26d32064d8%22%7D


Und darüber auch später wieder einloggen wodurch man einen neuen `sessionhash` bekommt:

http://2x.dragonjsonserver.de/?namespace=Device&method=loginDevice&data=%7B%22platform%22%3A%22browser%22%2C%22credentials%22%3A%7B%22browser_id%22%3A%22token%22%7D%7D

(also theoretisch, da gibts wohl einen Bug ^^)


### E-Mail Adresse / Passwort

oder dem klassischem E-Mail Adresse / Passwort (4):

http://2x.dragonjsonserver.de/?namespace=Emailaddress&method=createEmailaddress&data=%7B%22emailaddress%22%3A%22example%40example.com%22%2C%22password%22%3A%22example%22%2C%22sessionhash%22%3A%2214d93820d172931a7efe4d26d32064d8%22%7D

Und darüber auch später wieder einloggen wodurch man einen neuen `sessionhash` bekommt:

http://2x.dragonjsonserver.de/?namespace=Emailaddress&method=loginEmailaddress&data=%7B%22emailaddress%22%3A%22example%40example.com%22%2C%22password%22%3A%22example%22%7D

## Fazit

Man hat einen Account losgelöst von den Authentifizierungsmethoden und kann weitere (oAuth, Google, Facebook, ...) beliebig hinzufügen. Einzig die Authentifizierungsart E-Mail Adresse / Passwort ist ein klein wenig besonders, da die E-Mail Adresse auch herangezogen werden kann, wenn es um das Zusenden von Informationen geht. Das wäre aber kein Muss, man kann die E-Mail Adresse auch als Information an den Account hängen.
