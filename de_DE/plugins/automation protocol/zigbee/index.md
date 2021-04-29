# ZigBee Plugin

**Das ZigBee-Plugin für Jeedom** baut auf der hervorragenden Arbeit auf **die Open-Source-Zigpy-Bibliothek** ein anbieten **Allgemeine Kompatibilität mit verschiedenen ZigBee-Hardware**. Es ermöglicht die Kommunikation mit den folgenden ZigBee-Controllern :

-	**Deconz** : Vom Jeedom-Team getestet und validiert. *(Es ist nicht erforderlich, die deCONZ-Anwendung zu installieren)*
-	**EZSP (Silicon Labs)** : Vom Jeedom-Team getestet und validiert.
-	**XBee** : Nicht vom Jeedom-Team getestet.
-	**Zigate** : Nicht vom Team getestet. *(im Experiment in Zigpy)*
-	**ZNP (Texas Instruments, Z-Stapel 3.X.X)** : Nicht vom Team getestet. *(im Experiment in Zigpy)*
-	**CC (Texas Instruments, Z-Stapel 1.2.X)** : Nicht vom Team getestet. *(im Experiment in Zigpy)*

Darüber hinaus enthält das Plugin viele Tools, die dies ermöglichen :

- die Verantwortung übernehmen **mehrere Controller gleichzeitig**,
- das **sichern und Wiederherstellen** eine Steuerung,
- das **Firmware Update** eine Steuerung,
- das **Aktualisierung der Module** in OTA,
- Visualisierung von Knoten und **Netzwerkgraph**,
- Management von **Gruppen**,
- die Geschäftsführung von **Bindung**,
- die Verantwortung übernehmen **Touchlink**,
- oder sogar um seine eigenen Konfigurationen für die erfahrensten zu integrieren...

# Configuration

## Plugin Konfiguration

**Das ZigBee-Plugin** verwendet Abhängigkeiten, die zuerst installiert werden müssen. Sobald die Abhängigkeiten installiert sind, können Sie einen oder mehrere ZigBee-Controller durch Eingabe konfigurieren **den Typ des Controllers, den Controller-Port und den zu verwendenden Kanal**, Starten Sie dann den Daemon (neu).     

![Aufbau contrôleur Zigbee](./images/zigbee_controllerConfig.png)

>**Wichtig**
>
>Jeder Kanalwechsel erfordert einen Neustart des Dämons. Ein Kanalwechsel kann auch die Wiedereingliederung bestimmter Module erfordern.

### Erweiterte Zigpy-Konfiguration (für Experten reserviert !)

Es ist möglich, bestimmte Parameter für das ZigBee-Subsystem einzurichten *(Zigpy)*. Dieser Teil ist ausschließlich Experten vorbehalten, weshalb das Jeedom-Team keine Liste möglicher Parameter bereitstellt *(Je nach Controller-Typ gibt es Hunderte davon)*.

Das Eingabefeld akzeptiert Code im json-Format dieses Typs :

````````
{
    "ezsp": {
        "CONFIG_ADDRESS_TABLE_SIZE": "16"
    }
}
````````

>**Wichtig**
>
>Jede Supportanfrage wird automatisch abgelehnt, wenn dieses Feld ausgefüllt wird.

## Gerätekonfiguration

### Aufnahme eines ZigBee-Moduls

Inklusion ist der komplexeste Teil von Zigbee. Obwohl einfach, wird der Vorgang oft mehrmals wiederholt, um dies zu erreichen. Jeedom Plugin Seite ist es einfach, klicken Sie einfach auf die Schaltfläche **Einschlussmodus** Danach haben Sie 3 Minuten Zeit, um die Ausrüstung einzuschließen.

Das Einschlussverfahren ist für jedes Modul spezifisch. Bitte beachten Sie die Dokumentation des Herstellers, um dies zu erreichen.

>**TRICK**
>
>Vergessen Sie nicht, einen Reset durchzuführen *(reset)* des Moduls vor jeder Aufnahme.

### Einrichten eines ZigBee-Moduls

Nach der Aufnahme soll Jeedom das Modul automatisch erkennen und die entsprechenden Befehle erstellen. Ist dies nicht der Fall, lesen Sie den folgenden Absatz : **Modul nicht erkannt**.

>**Wichtig**
>
>Aufgrund eines Fehlers in einer Firmware *(Ikea, Sonoff, etc)*, Manchmal muss der Modultyp direkt aus der Liste ausgewählt werden **Gerät** Speichern Sie dann, damit die Bestellungen korrekt erstellt werden.

Wie gewohnt können Sie Ihrem Gerät einen Namen geben, eine Kategorie oder ein übergeordnetes Objekt eingeben und es aktivieren oder sichtbar machen.

Andere spezifischere Parameter sind ebenfalls verfügbar :

- **Identifizierung** : eindeutige Kennung des Geräts. Auch während einer Wiedereingliederung oder wenn Sie den Typ des ZigBee-Controllers ändern.
- **ZigBee-Controller** : wird verwendet, um den ZigBee-Controller in Kommunikation mit dem Gerät auszuwählen.
- **Kommunikationssteuerung** : Mit dieser Option können Sie den Modus zur Überprüfung der guten Kommunikation zwischen der Steuerung und dem Modul auswählen.
- **Ausführungsbestätigung ignorieren** : Aktivieren Sie das Kontrollkästchen, um die korrekte Ausführung des Befehls zu ignorieren. Auf diese Weise können Sie die Kontrolle schneller wiedererlangen, können jedoch nicht garantieren, dass die Bestellung erfolgreich aufgegeben wurde.
- **Warteschlangen zulassen** : Aktivieren Sie das Kontrollkästchen, um das Einreihen von Bestellungen zu ermöglichen. Auf diese Weise können Sie es erneut versuchen, falls der Auftrag nicht ausgeführt wurde.

Das Teil **Information** ermöglicht die manuelle Auswahl von Hersteller und Ausrüstung. Es gibt auch die Anzeige des Geräts sowie zwei Tasten, mit denen die Befehle neu generiert oder auf die Konfigurationsoptionen des Moduls zugegriffen werden kann.

In der Registerkarte **Aufträge**, Wir finden wie üblich die Befehle, die die Interaktion mit dem Modul ermöglichen.

### Modul nicht erkannt

Wenn Ihr Modul von Jeedom nicht automatisch erkannt wird *(Es wurden keine Bestellungen erstellt)* aber gut enthalten, so dass Sie darum bitten müssen, dass es dem Jeedom-Team hinzugefügt wird.

>**INFORMATION**
>
>Das Jeedom-Team behält sich das Recht vor, Integrationsanfragen abzulehnen. Es ist immer vorzuziehen, sich für Geräte zu entscheiden, deren Kompatibilität bereits bestätigt ist.

Um die Hinzufügung neuer Geräte anzufordern, müssen die folgenden Elemente angegeben werden :

- **das genaue Modell** des Moduls mit einem Link zur Kaufseite,
- Klicken Sie auf der Ausrüstungsseite auf die blaue Schaltfläche **Modulkonfiguration** dann tab **Rohdaten**. Kopieren Sie den Inhalt, um ihn an das Jeedom-Team zu übertragen,
- Setzen Sie den Daemon auf der Plugin-Konfigurationsseite in "Debug" und starten Sie ihn neu. Führen Sie Aktionen am Gerät aus *(Wenn es sich um einen Temperatursensor handelt, ändern Sie beispielsweise die Temperatur. Wenn es sich um ein Ventil handelt, ändern Sie den Sollwert usw...)* und senden Sie das ZigBee-Protokoll *(nicht "Zigbeed")*.

>**INFORMATION**
>
>Jede unvollständige Anfrage wird ohne Antwort des Jeedom-Teams abgelehnt.

### Wie Kontrollen für Experten funktionieren

Im Folgenden wird erläutert, wie die Befehle im Plugin für die fortgeschrittensten Benutzer funktionieren :

- ````attributes::ENDPOINT::CLUSTER_TYPE::CLUSTER::ATTRIBUT::VALUE```` Mit dieser Option können Sie den Wert eines Attributs schreiben *(Achten Sie darauf, dass nicht alle Attribute geändert werden können)* mit :
  - ````ENDPOINT```` : Endpunktnummer,
  - ````CLUSTER_TYPE```` : Clustertyp *(IM \| OUT)*,
  - ````CLUSTER```` : Clusternummer,
  - ````ATTRIBUT```` : Attributnummer,
  - ````VALUE```` : Wert zu schreiben.

**Beispiel** : ````attributes::1::in::513::18::#slider#*100```` Dadurch wird das Attribut in den Endpunkt "1" des eingehenden Clusters geschrieben (````in````) `513`, Attribut` 18` mit dem Wert von ````slider*100````.

- ````ENDPOINT::CLUSTER:COMMAND::PARAMS```` ermöglicht es Ihnen, einen Serverbefehl mit auszuführen :
  - ````ENDPOINT```` : Endpunktnummer,
  - ````CLUSTER```` : Clustername,
  - ````COMMAND```` : Name der Bestellung,
  - ````PARAMS```` Parameter in der richtigen Reihenfolge durch `getrennt::``.

**Beispiel** : ````1::on_off::on````, Führen Sie den Befehl aus ````on```` auf dem Endpunkt "1" des Clusters ````on_off```` ohne Parameter.        
**Beispiel** : ````1::level::move_to_level::#slider#::0````, Führen Sie den Befehl aus ````move_to_level```` auf dem Endpunkt "1" des Clusters ````level```` Mit Parametern ````#slider#```` und ````0````.

# Outils

Auf verschiedene Tools, die eine bessere Interaktivität mit dem ZigBee-Netzwerk bieten, kann über die Plugin-Konfigurationsseite zugegriffen werden :

![Werkzeuge contrôleur Zigbee](./images/zigbee_controllerTools.png)

## Sichern / Wiederherstellen eines Controllers

Es ist möglich, ein Backup des ZigBee-Netzwerks von Controllern vom Typ EZSP zu erstellen *(Elelabs zum Beispiel)* und ZNP. Diese Sicherung kann auf einem anderen Controller desselben Typs wiederhergestellt werden.

>**Wichtig**
>
> Auf EZSP-Schlüsseln *(Elelabs)*, Es ist nur möglich, während der gesamten Lebensdauer des Schlüssels eine einzige Sicherungswiederherstellung für alle und für alle durchzuführen.

Das Backup enthält nicht die Liste der Module, sondern nur die Basisinformationen des ZigBee-Netzwerks. Es ist daher nicht erforderlich, es regelmäßig durchzuführen. Eine einzelne Sicherung ist häufig ausreichend, da sich diese Informationen während der Lebensdauer des Controllers nicht ändern.

>**INFORMATION**
>
>ZigBee-Dämonen werden während des Sicherungs- oder Wiederherstellungsprozesses gestoppt.

## Aktualisieren der Controller-Firmware

Es ist möglich, die Firmware des ZigBee-Controllers von Jeedom aus zu aktualisieren *(gilt derzeit nur für Elelabs-Controller)*. Da die Firmware in Zigbee unverzichtbar ist, weil sie unter anderem das Routing verwaltet, ist es wichtig, sie zu aktualisieren.

>**INFORMATION**
>
>ZigBee-Daemons werden während eines Firmware-Updates gestoppt.

## Aktualisieren von OTA-Modulen

OTA-Updates *(Over-The-Air)* sind die Firmware-Updates der Module. Der Vorgang kann eine bestimmte Zeit dauern (mehrere Stunden, abhängig von der Anzahl der Module), ermöglicht jedoch im Allgemeinen eine bessere Zuverlässigkeit des ZigBee-Netzwerks. Um ein Modul aktualisieren zu können, muss der Hersteller die Firmware mitteilen :

- Hinsichtlich **Ikea** und **Der Fortschritt**, Die Firmwares werden direkt online zur Verfügung gestellt, wo das Plugin sie abruft.
- Für andere (siehe [Hier](https://github.com/Koenkk/zigbee-OTA/tree/master/images)), In einigen Fällen stellt der Hersteller informell ein Update zur Verfügung.
- Für alle anderen ist es nicht möglich, das Modul über das Plugin zu aktualisieren.

Um von OTA-Updates zu profitieren, müssen Sie das entsprechende Kontrollkästchen auf der Plugin-Konfigurationsseite aktivieren und dann speichern. Sie müssen dann auf die Schaltfläche klicken **Aktualisieren Sie die Moduldateien** um die neuesten aktualisierten Dateien abzurufen und den ZigBee-Daemon neu zu starten.

Aktualisierungen werden bei Verfügbarkeit oder auf Anforderung des Moduls automatisch durchgeführt. Es ist möglich, die Aktualisierung eines Moduls über die Registerkarte zu erzwingen **Aktionen** aus dem Modulkonfigurationsfenster auf der Geräteseite.

Leider gibt es keinen einfachen Indikator, um den Fortschritt des Updates zu verfolgen. Die einzige Lösung besteht darin, auf die "zigbee_X" -Protokolle im Debug zu verweisen und nach dem Begriff "OTA" zu suchen. Sie können diesen Protokolltyp sehen, wenn ein Modul aktualisiert wird :

````````
2020-02-27 15:51:10 [DEBUG][0x7813:1:0x0019] OTA query_next_image handler for 'IKEA of Sweden TRADFRI control outlet': field_control=1, manufacture_id=4476, image_type=4353, current_file_version=536974883, hardware_version=60
2020-02-27 15:51:10 [DEBUG][0x7813:1:0x0019] OTA image version: 537011747, size: 204222. Update needed: True
2020-02-27 15:51:18 [DEBUG][0x7813:1:0x0019] OTA image_block handler for 'IKEA of Sweden TRADFRI control outlet': field_control=0, manufacturer_id=4476, image_type=4353, file_version=537011747, file_offset=0, max_data_size=63, request_node_addr=Noneblock_request_delay=None
2020-02-27 15:51:18 [DEBUG][0x7813:1:0x0019] OTA upgrade progress: 0.0
````````

# Touchlink

**Touchlink** *(oder Lightlink)* ist eine spezielle Funktion von Zigbee, die es dem Controller ermöglicht, Verwaltungsaufträge an ein Modul zu senden, sofern es sich sehr nahe daran befindet *(weniger als 50 Zentimeter)*. Dies ist beispielsweise nützlich, um Lampen zurückzusetzen, die keine physische Taste haben.

Diese Funktion ist bei ZigBee-Lampen verfügbar **Philips Hue, Ikea, Osram, Icasa und viele mehr...** Das Prinzip ist sehr einfach. Um diesen Modultyp einem ZigBee-Netzwerk zuordnen zu können, müssen Sie zuerst einen Reset durchführen. Beim Neustart versucht das Modul automatisch, eine Verbindung mit dem ersten verfügbaren ZigBee-Netzwerk herzustellen.

## In Touchlink zurücksetzen

Wie so oft in Zigbee können während des Zurücksetzens oder des Zuordnungsprozesses Schwierigkeiten auftreten. Um dies zu erreichen, stehen Ihnen verschiedene Methoden zur Verfügung :

- **Führen Sie schnell 5/6 Ein / Aus-Zyklen durch** *(an aus)*. Die Lampe sollte am Ende des Vorgangs blinken, um die korrekte Erkennung anzuzeigen.
- **Verwenden Sie eine ZigBee-Fernbedienung**, und :
  - **für Philips Hue Fernbedienungen**, Drücken Sie gleichzeitig die EIN- und AUS-Tasten 5 bis 10 Sekunden lang in der Nähe der Glühbirne *(Manchmal muss bei einigen Modellen die Glühbirne kurz zuvor ein- und ausgeschaltet werden)*,
  - **für Ikea-Fernbedienungen**, Drücken Sie die Reset-Taste" *(neben der Batterie)* für 5 bis 10 Sekunden in der Nähe der Glühbirne *(Manchmal muss bei einigen Modellen die Glühbirne kurz zuvor ein- und ausgeschaltet werden)*.
- Über die **Philips Hue Glühbirnen**, Sie können sie auch in die Hue Bridge aufnehmen und dann daraus entfernen.

# Binding

Die Bindung ermöglicht es Ihnen, 2 Module direkt miteinander zu verknüpfen, ohne dass die Befehle durch Jeedom gehen. Die Verknüpfung wird von einem Cluster zu demselben Cluster eines anderen Moduls hergestellt. Die Verbindung muss immer von der Steuerung (Fernbedienungstyp) zum Stellantrieb hergestellt werden.

Sie finden die Bindungsverwaltungselemente, sofern sie von Ihrem Modul unterstützt werden, auf der Registerkarte **Information** aus dem Modulkonfigurationsfenster.

Einige Module sind nicht mit der Bindung kompatibel, andere *(wie Ikea-Module)* Unterstützen Sie nur die Bindung des Befehls an eine Gruppe. Daher müssen Sie zunächst eine Gruppe erstellen, in die Sie den Aktuator einfügen müssen.

# ZigBee-Netzwerk

Der Aufbau eines qualitativ hochwertigen ZigBee-Netzwerks wird durch die im Plugin bereitgestellten Tools erheblich unterstützt. Gehen Sie zur allgemeinen Seite des Plugins, in der alle Geräte aufgelistet sind, und klicken Sie auf die Schaltfläche **ZigBee-Netzwerke** Zugriff auf verschiedene Informationen und Aktionen rund um das ZigBee-Netzwerk sowie deren repräsentative Grafik.

## Netzwerkdiagramm

Das Netzwerkdiagramm bietet einen Überblick über das ZigBee-Netzwerk und die Qualität der Kommunikation mit den verschiedenen Modulen.

>**INFORMATION**
>
>Das ZigBee-Netzwerkdiagramm ist indikativ und basiert auf den Nachbarn, die die Module deklarieren. Dies stellt nicht unbedingt das tatsächliche Routing dar, sondern ein mögliches Routing.

## Das Netzwerk optimieren

Um die Zuverlässigkeit Ihres ZigBee-Netzwerks zu optimieren, wird mehr als empfohlen, mindestens 3 Routermodule permanent mit Strom zu versorgen und ein Herausziehen des Netzsteckers zu vermeiden. Tatsächlich haben wir bei unseren Tests eine deutliche Verbesserung der Zuverlässigkeit und Ausfallsicherheit des ZigBee-Netzwerks beim Hinzufügen von Routermodulen festgestellt. Es ist auch ratsam, sie zuerst einzuschließen, da es sonst zwischen 24 und 48 Stunden für das "Endgerät" dauert" *(Nicht-Router-Module)* entdecke sie.

Ein weiterer wichtiger Punkt ist, dass beim Entfernen eines Routermoduls dieser Teil des "Endgeräts" möglich ist" *(Nicht-Router-Module)* entweder für eine längere oder kürzere Zeit verloren *(in zehn Stunden oder mehr)* oder sogar definitiv und Sie müssen sie wieder einschließen.
Leider liegt dies an der Art und Weise, wie der Hersteller die Integration seiner Geräte in ein ZigBee-Netzwerk geplant hat und daher nicht durch das Plugin korrigiert werden kann, das den Routing-Teil nicht verwaltet.

Schließlich und auch wenn es einigen offensichtlich erscheint, erinnern wir Sie daran, dass ZigBee-Gateways in Wifi weniger zuverlässig sind als USB-Gateways. Das Jeedom-Team empfiehlt daher die Verwendung eines ZigBee-Gateways in USB.  

# FAQ

>**LQI oder RSSI ist N / A**
>
>Normalerweise werden die Werte nach dem Neustart des ZigBee-Netzwerks geleert. Sie müssen warten, bis das Modul erneut kommuniziert, damit die Werte eingegeben werden können.


>**Ich habe Einschlussprobleme oder Fehler in den Typprotokollen ````TXStatus.MAC_CHANNEL_ACCESS_FAILURE````**
>
>Sie müssen versuchen, die USB-Erweiterung zu entfernen oder zu ändern, wenn Sie eine verwenden, oder eine, wenn Sie keine verwenden.


>**Ich habe Fehler ````can not send to device```` oder ````send error```` oder ````Message send failure````**
>
>Dies ist normalerweise auf ein Routing-Problem zurückzuführen. Das Routing ist in ZigBee mehr oder weniger fest und nicht symmetrisch. Ein Modul kann eine andere Route verwenden, um zu antworten, als die, mit der es gesprochen hat. Oft die elektrische Abschaltung *(zum Beispiel Batterien entfernen)* und schalten Sie den Strom ein *(oder Austausch von Batterien)* ist genug, um das Problem zu lösen.


>**Ich habe seltsame Fehler bei Batteriemodulen oder Einschlussprobleme**
>
>Wir haben festgestellt, dass ein großer Teil der ZigBee-Probleme bei Batteriemodulen auf die Batterien oder möglicherweise auf Probleme beim Zurücksetzen der Module vor der Aufnahme zurückzuführen ist. Auch wenn diese neu erscheinen, ist es ratsam, mit neuen Batterien zu testen, um diese Hypothese auszuschließen.


>**Ich habe Bedenken, die Werte der Ausrüstung zu aktualisieren**
>
> 2 Möglichkeiten :
> - Dies ist ein "altes Modul" in ZLL *(Siehe die Konfiguration der Jeedom-Ausrüstung, die angibt, ob es sich um ZHA oder ZLL handelt)*. In diesem Fall benötigen Sie unbedingt einen Befehl "Aktualisieren", damit Sie oder Jeedom die Aktualisierung der Werte erzwingen. Wenn dieser Befehl im Gerät nicht vorhanden ist, müssen Sie sich an den Jeedom-Support wenden, damit er in der nächsten stabilen Version hinzugefügt wird. Sobald Sie fertig sind, klicken Sie auf die Schaltfläche **Befehle neu erstellen** ohne Löschung.
> -	Das Modul befindet sich in ZHA, daher ist es ein Anliegen der Inklusion. In der Registerkarte **Aktion** In der Modulkonfiguration befindet sich eine Schaltfläche **Modul zurücksetzen** Erlauben, Aktionen nach der Aufnahme zu erzwingen. Es muss darauf geachtet werden, dass das Modul wach bleibt, wenn es im Akkubetrieb ist.