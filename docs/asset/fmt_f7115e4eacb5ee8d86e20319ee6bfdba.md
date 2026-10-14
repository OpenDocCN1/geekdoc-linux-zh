
# Ändern von Eigentumsrechte

Weitere Kommandos, die Eigentumsverhältnisse regeln, sind `chown` (Change Owner) und `chgrp` (Change Group). Der Befehl `chown` dient dazu, einen Benutzer zu ändern. Allerdings darf `root` diese Änderung vornehmen.

Angenommen, die Datei `Roadmap` aus Beispiel 2 soll nicht mehr `tux`, sondern dem Benutzer `geek` gehören, so lautet der entsprechende Befehl:

```
chown geek Roadmap
```

# Wichtige Linux-Befehle im Überblick

In diesem Abschnitt möchten wir Ihnen einen Überblick über die wichtigsten Befehle Ihres Systems geben. Dabei werden wir die Grundbedeutung der einzelnen Kommandos auf einige Parameter eingehen und wenn es sich anbietet, ein typisches Anwendungsbe liefern.

Um über die Details dieses Kommandos zu erfahren, können Sie zusätzliche Informationen mit dem Programm `man` gefolgt von Befehl erhalten z. B.

```
man ls
```

In diesen „Manual Pages“ können Sie sich mit den Bildlauften `↑` `↓` vom Anfang bis Ende der Dokumentation bewegen. Beenden Sie diesen Darstellungsmodus durch Drücken der Taste `Q`. Durch Eingabe von `man` können Sie mehr über `man`-Befehle selbst erfahren.

+   如果某些信息或参数不是绝对必要的，则将它们放在 `[方括号]` 中。

Und natürlich müssen Sie etwaige Angaben Ihren Bedürfnissen anpassen. Es macht keinen Sinn, wie `ls` `Datei(en)` zu schreiben, soweit nicht eine Datei, die sich `Datei(en)` nennt, tatsächlich existiert. Außerdem können Sie mehrere Parameter in aller Regel kombinieren, indem Sie z.B. statt `ls -1 -a` `ls -la` schreiben.

# 文件命令

## Dateiververwaltung

```
ls [Option(en)] [Datei(en)]
```

Wird `ls` ohne weitere Angaben und Parameter aufgerufen, listet es den Inhalt des Verzeichnisses, in dem Sie sich gerade befinden, in Kurzform auf.

Optionen:
+   `-l` detaillierte Liste,
+   `-a` zeigt versteckte Dateien an.

```
cp [Option(en)] Quelldatei Zieldatei
```

Erstellt eine Kopie der Quelldatei in Zieldatei.

Optionen:
+   `-i` Wartet ggf. auf Bestätigung, bevor eine existierende Zieldatei überschrieben wird.
+   `-r` Kopiert rekursiv (mit Unterverzeichnissen)

```
mv [Option(en)] Quelldatei Zieldatei
```

Legt eine Kopie der Quelldatei in Zieldatei an und löscht anschließend die ursprüngliche Datei.

Optionen:
+   `-b` Erstellt vor dem Verschieben eine Sicherungskopie der Quelldatei
+   `-i` Wartet ggf. auf Bestätigung, bevor eine existierende Zieldatei überschrieben wird.

```
rm [Option(en)] Datei (en)
```

Entfernt die angegebenen Datei (en) aus dem Dateystem. Verzeichnisse werden außer durch explizite Angabe des Parameters `-r` nicht durch `rm` gelöscht.

Optionen:
+   `-r` Löscht evtl. vorhandene Unterverzeichnisse
+   `-i` Wartet vor Löschen angegebene Datei auf Bestätigung

```
ln [Option(en)] Quelldatei Zieldatei
```

Legt in Zieldatei einen internen Querverweis („Link“) auf die Quelldatei unter anderem Namen an. Normalerweise zeigt dieser weist direkt auf die Position der Datei innerhalb eines Dateisystems. `ln` hingegen mit der Option `-s` aufgerufen, wird ein sogenannter „symbolischer Link“ angelegt, der lediglich auf den Pfad der Datei zeigt und deswegen über Dateystem-grenzen hinweg funktioniert.

Optionen:
+   `-s` Legt einen symbolischen Link an.

```
cd [Option(en)] Verzeichnis
```

Wechselt das aktuelle Verzeichnis. Wenn nur `cd` eingegeben wird, wird in das Homeverzeichnis gesprungen.

```
mkdir [Option(en)] Verzeichnisname
```

Legt ein neues Verzeichnis an.

```
rmdir [Option(en)] Verzeichnisname
```

Löscht das Verzeichnis, allerdings nur, wenn dieses bereits leer ist.

```
chown [Option(en)] Benutzername.Gruppe Datei
```

Ändert den Besitzer einer Datei auf den angegebenen Benutzernamen.

# Optionen:
+   `-R` Ändern der Dateien und Verzeichnisse in allen Unterverzeichnissen.

```
chgrp [Option(en)] Gruppename Datei (en)
```

Ändert den Namen der Gruppe, die eine gegebene Datei besitzt Gruppename. Der Datei-Besitzer darf diesen Wert nicht ändern, wenn er sowohl Mitglied der bisherigen als auch der Eigentümergruppe ist.

```
chmod [Optionen] modus Datei (en)
```
