# ldap

'''was ist LDAP?'''

Das "Lightweight Directory Access Protocol" (LDAP) ist ein Netzwerkprotokoll zur Durchführung von Abfragen und Änderungen in einem   verteilten Verzeichnisdienst. Das Protokoll aus dem TCP/IP-Protokollstapel ist in den RFCs 4510, 4511 und 4532 spezifiziert.

Eines gleich vorweg: LDAP selbst ist kein Verzeichnis, sondern das Protokoll, über das es mit einer bestimmten Syntax möglich ist, Informationen eines LDAP-Verzeichnisses abzufragen. Für eine fehlerlose Zusammenarbeit ist es bei LDAP erforderlich, dass alle beteiligten Systeme auf Port 389 für eine ungesicherte Übertragung und auf Port 636 in einer TLS gesicherten Verbindung Daten austauschen können. Historisch betrachtet geht die Entwicklung von LDAP auf die Universität von Michigan zurück. Dort wurde im Jahr 1993 erstmals ein Vorschlag für die vereinfachte Variante des DAP (Directory Access Protocol) als RFC definiert.

'''WO für braucht man LDAP?'''

Die Idee hinter LDAP ist einfach: Ein über verschiedene Server verteiltes Verzeichnis in einer Baumstruktur soll einfach durchsucht werden können.

Die wohl bekannteste Implementierung von LDAP ist das Active Directory von Microsoft. Hilfsprogramme wie der LDAP Admin erleichtern die Suche nach den passenden Attributbezeichnungen. Mit der PowerShell ist eine Verarbeitung von AD-Daten, die über LDAP ermittelt wurden, sehr leicht möglich.

Die Baumstruktur des Verzeichnisses ist in groben Zügen vorgegeben: Der Ursprung ist stets das "Root Directory" und dieses verzweigt in Länder, Organisationen, Organisationseinheiten und Individuen. Bei den letzteren kann es sich um Benutzer, Personen, Drucker, Scanner, Computer, Server oder dergleichen handeln kann. Obwohl das System eine hohe Flexibilität bei der Abbildung von Strukturen erlaubt, ist die Definition der Elemente im Schema eher strikt.

Mögliche Anwendungsfälle für LDAP können sein:

   - Benutzerverwaltung
   - Systemverwaltung
   - Protokollzuordnung
   - RFC-Zuordnungen
   - NIS-Informationen
   - Boot-Informationen
   - Verwaltung von Mountpoints im Dateisystem
   - Organisation von Alias-Namen in E-Mail-Systemen
   - Verwaltung von DNS Zonendaten
   - Organisation von DHCP-Servern
'''
Wie ist LDAP Aufgebaut ?'''

Der grundlegende Aufbau im LDAP-Datenmodell ist einfach. LDAP besteht aus Objekten und folgt weitgehend dem Ansatz der objektorientierten Programmierung mit Klassen, Vererbung, Polymorphie und den Objekten selbst. Ein Verzeichnisdiensteintrag besteht aus einer Liste von Attributen und einem "Pflichtobjekt" – der Bezeichnung des Objekts selbst, dem "Distinguished Name".

Diese Bezeichnung entspricht ein wenig einem Dateinamen und teilt sich eine Eigenschaft mit der Dateinamenkonvention: In derselben Ebene ist kein gleichlautendes Objekt mit demselben Namen möglich. Objekte mit der Bezeichnung "OU" stellen Container dar, in denen weitere Objekte erzeugt sein können. Sie bilden das Grundgerüst beim Aufbau der Struktur. Gemäß dem Standard RFC 2253 mit dem Titel "UTF-8 String Representation of Distinguished Names" existieren unter anderem folgende Attributtypen:

  -CN: commonName
  -L: localityName
  -ST: stateOrProvinceName
  -O: organizationName
  -OU: organizationalUnitName
  -C: countryName
  -STREET: streetAddress
  -DC: domainComponent
  -UID: userid

'''ein Beispiel!'''

Man stelle sich ein Active Directory mit dem Namen CCT.local vor. Es wird ein neuer Benutzer mit dem Namen "Mustermann, Hans" während die Auswahl auf dem Wurzelverzeichnis CCT.local stand angelegt. In der Darstellung als distinguished Name:

CN=Hans Mustermann,DC=CCT,DC=local

Nun wird das Objekt in einen OU mit dem Titel "Personen" verschoben und der DN noch einmal betrachtet:

CN=Hans Mustermann,OU=Personen,DC=CCT,DC=local

Innerhalb der OU Personen erstellt der Administrator nun eine weitere OU, um eine bessere Orientierung zu haben. Diese soll "Mitglieder" heißen und das Benutzerobjekt von Herrn Mustermann wird dieser neuen OU zugeordnet. Somit lautet der DN:

CN=Hans Mustermann,OU=Mitglieder,OU=Personen,DC=CCT,DC=local

Nun ergibt es sich die Logik fast schon von allein. Der commonName, die Bezeichnung des Objekts selbst, steht auf der linken Seite, während die Zuordnung von der rechten Seite ausgehend mit der Domänenstruktur local, gefolgt von CCT beginnt. Wieder von rechts gelesen findet der Administrator das Benutzerobjekt für Herrn Mustermann in der OU "Mitglieder", die sich in der OU "Personen" befindet, die in der Wurzelstruktur der Domäne zu finden ist.
