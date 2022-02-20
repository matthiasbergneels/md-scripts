---
title: Programmieren - Exkurse
theme: simple
data-separator-notes: '^Note:'
center: false
---

# Programmieren - Exkurse
### Matthias Berg-Neels

----
## Inhalt

* Naming conventions
* Implizite Typisierung mittels ```var```
* Unit Tests
* (Optionals)
* (Programming Principals)

---
# Naming conventions
> Naming conventions sind, in (großen) Projekten / Firmen, Bestandteil der "Code Style Guidelines". Firmen bzw. Community basiert gibt es unterschiedliche Code Style Guidelines nach denen man sich richten kann. Die folgenden Konventionen basieren auf den [Google Style Guidelines für Java](https://google.github.io/styleguide/javaguide.html#s5-naming).

----
## Allgemeine Regeln für Bezeichner und Namen (1/2)

**Regeln**
* erlaubte Zeichen
  * Buchstaben (Case sensitive): a, b, c, ..., x, y, z, A, B, ..., Y, Z
    * Landespezifische Zeichen sind erlaubt (z.B. ä, ü, ö) - sollten aber vermieden werden! (Stichwort: Kompatibilität zwischen Rechnern - betrifft NUR Quellcode, nicht den Bytecode!)
  * Unterstrich: _
  * Dollarzeichen: $
  * Zahlen: 0, 1, 2, ..., 9
* nicht erlaubte Zeichensatz
  * Sonderzeichen

----
## Allgemeine Regeln für Bezeichner und Namen (2/2)
**weitere Regeln**
* keine Leerzeichen
* dürfen nicht mit Zahlen beginnen
* dürfen nicht gleich mit reservierten Schlüsselwörtern sein

**Empfehlungen**
<div>

* sprechende Namen -> man kann beim Lesen verstehen was eine Variable, Klasse, Methode für eine Aufgabe hat.
* **Merksatz**: Wenn man einen Namen lesen kann ohne "grammatikalische" Bauchschmerzen zu bekommen, ist es die richtige Richtung.
* **Anmerkung**: Namen sollten immer die tatsächliche Funktion einer Entität widerspiegeln, daher stehen sie in hoher Abhängigkeit zum Quellcode. Eine Variable mit dem Namen "WindowCount" (vom Typ Boolean), eine Methode "saveToDatabase" (die nichts Speichert) oder eine Klasse "Student" (die Funktionen einer Vorlesung enthält) sollten namentlich noch einmal überdacht werden, auch wenn diese sich "rein vom Namen" korrekt lesen.

</div><!-- .element style="font-size: 0.8em;" -->

----
## Packagenamen

**Guideline**
* klein geschrieben

```Java
de.mbn.myapp.lecture
lecture.objectorientation.trainstation
```

----

## Klassennamen

**Guideline**
* beginnen mit einem Großbuchstaben
* UpperCamelCase - beginnen mit Großbuchstaben und jedes neue Wort beginnt mit einem Großbuchstaben
* Zusatz: Der Dateiname muss sich nach dem Namen der Hauptklasse (first level) in der Datei richten

```Java
Car
Student
TrainDriver
```

----

## Variablen / Attribute

**Guideline**
* lowerCamelCase - beginnen mit einem Kleinbuchstaben und jedes neue Wort beginnt mit einem Großbuchstaben

```Java
familyName
children
studentId
```

----

## Konstanten

**Guideline**
* UPPER_CASE - werden vollständig mit Großbuchstaben geschrieben, neue Wörter werden durch Unterstrich getrennt

```Java
ALLOWED_COLOR_RED
MEANING_OF_LIFE
```
----
## Methoden

**Guideline**
* lowerCamelCase - beginnen mit einem Kleinbuchstaben und jedes neue Wort beginnt mit einem Großbuchstaben
* beginnen mit einem Verb (bzw enthalten mindestens ein Verb)
  * eine Methode "spiegelt" eine Tätigkeit, Geschehen, Vorgang wieder --> es passiert etwas

```Java
accelerate();
persistData();
```

**Getter- / Setter**
* Attributname wird mit get bzw. set vorangestellt in lowerCamelCase

```Java
setFamilyName();
getFamilyName();
```

----

## Spezialfall: Boolen Attribute / Getter-Methoden
* sprechende Definition von Boolean-Attribute
  * z.B. enabled, isTired (VS tired), hasFlatRoof (VS flatRoof), canFly (VS fly), ...
* Boolean Getter-Methoden werden nicht mit get, sondern mit dem passenden Verb (is, has, can) gebildet
  * isEnabled(), isTired(), hasFlatRoof(), canFly()
* anhängig vom Attributnamen können in diesem Fall die Setter-Namen doch komisch wirken
  * setEnabled, setIsTired (VS setTired), setHasFlatRoof (VS setFlatRoof), setCanFly (VS setFly)


----

## Ein Beispiel aus dem echten Leben (/ produktiven Code)

<div>
```Java

package com.sap.iot.rules.ruleprocessorstream.cache.repository;

import // ...

public class ThingModelBasedDataObjectRepository extends HashOperationsRepository<ThingModelBasedDataObject> {

    private static final String KEY_PREFIX = "do_by_rsid_tt_ps";

    private static final String NAME = "name";
    private static final String TYPE = "type";
    private static final String IS_RESULT = "isResult";
    private static final String THING_TYPE = "thingType";
    private static final String PROPERTY_SET = "propertySet";
    private static final String PROPERTY_SET_TYPE = "propertySetType";
    private static final String SENSITIVITY_LEVEL = "sensitivityLevel";
    private static final String LIST_SIZE_SUFFIX = "size";
    private static final String USED_ATTRIBUTES_PREFIX = "usedAttributes.";
    private static final String WILDCARD = "*";

    public ThingModelBasedDataObjectRepository(@Qualifier("ruleCache") RedisTemplate<String, String> redisTemplate, TenantContext tenantContext) {
        // ...
    }

    @Override
    public String getUniqueCachingKeyPrefix() {
        // ...
    }

    @Override
    public void save(@NotBlank String ermRuleServiceId, @Valid ThingModelBasedDataObject dataObject) {
        // ...
    }

    public Optional<ThingModelBasedDataObject> find(@NotBlank String ermRuleServiceId, String thingType, String propertySet) {
        // ...
    }

    public List<ThingModelBasedDataObject> findAll(@NotBlank String ermRuleServiceId, String thingType) {
        // ...
    }

    public Optional<ThingModelBasedDataObject> find(@NotBlank String ermRuleServiceId, String propertySetType) {
        // ...
    }

    public Boolean delete(@NotBlank String ermRuleServiceId, String thingType, String propertySet, String propertySetType) {
        // ...
    }

    @Override
    public long deleteAll(@NotBlank String ermRuleServiceId) {
        // ...
    }

    @Override
    protected Map<String, String> serialize(ThingModelBasedDataObject dataObject) {
        // ...
    }

    @Override
    protected ThingModelBasedDataObject deserialize(Map<String, String> map) {
        // ...
    }

    protected String getCachingKeySuffix(@NotBlank String ermRuleServiceId, String thingType, String propertySet, String propertySetType) {
        // ...
    }

}
```
</div><!-- .element style="font-size: 0.5em;" -->

---
# implizite Typisierung mittels ```var```

> Ermittlung des Datentyps einer Variable ohne spezifische Angabe des Typs mittels der Initialisierung - Schlüsselwort ```var``` (seit Java 10) <sub>some evil stuff</sub>

----
## Verwendung

**Voraussetzung**
* Deklaration mit ```var``` UND sofortiger Initialisierung der Variable.

**Beispiele**
```Java
var numberA = 10;                     // numberA wird zu Integer Variable deklariert
var numberB = 42.0;                   // numberB wird zu Double Variable deklariert
var textA = "Herzlich Willkommen";    // textA wird zu String Variable deklariert
var myAnimal = new Dog(...);          // myAnimal wird zu Dog Variable deklariert

var test;                             // Compiler Fehler!

int numberC = 100;

var numberD = numberC;                // numberD wird zu Integer Variable deklariert
```

**Besser lesbarer (kürzerer) Code** durch Vermeidung von Redundanzen
<div>

```Java
// vorher:
ThingModelBasedDataObjectRepository myThingModelRepo =
      new ThingModelBasedDataObjectRepository(myChacheTemplate, customerTenant);

// neu:
var myThingModelRepo = new ThingModelBasedDataObjectRepository(myChacheTemplate, customerTenant);
```

</div><!-- .element style="font-size: 0.85em;" -->

----

## ABER...

Falsch eingesetzt, wird der Code unverständlicher / komplizierter zu lesen:

```Java
var somethingOne = (farm.hasAnimal()) ? new Dog(...) : "Kein Tier";
var somethingTwo = ("Ergebnis ist " + (numberA + numberB * 50.1)).length() / (double)10;
var somethingThree = Something.returnSomething();
// ...
```

---
# Unit Testing

> Unit Testing in Java mit JUnit5.

----
## Einordnung von Unit Tests

<div align="center">
<img src="img/0x_junit_02testpyramide.svg" width=60% /><!-- .element style="border: 0px; box-shadow: 0 0 0 0; align="center"" -->
</div>

----
## JUnit5 - Basis Annotationen

<div>

| Annotation | Beschreibung | 
|:----------:|:-------------|
| ```@Test``` | kennzeichnet eine Methode als Test | 
| ```@Tag("<tag>")``` | definiert einen Tag zur Filterung von Tests | 
| ```@BeforeEach``` | kennzeichnet eine Methode die **vor jedem** Test läuft (JUnit4 --> ```@Before```) | 
| ```@AfterEach``` | kennzeichnet eine Methode die **nach jedem** Test läuft (JUnit4 --> ```@After```) | 
| ```@BeforeAll``` | kennzeichnet eine Methode die **einmal vor allen** Tests läuft (JUnit4 --> ```@BeforeClass```) | 
| ```@AfterAll``` | kennzeichnet eine Methode die **einmal nach allen** Tests läuft (JUnit4 --> ```@AfterClass```) | 

</div><!-- .element style="font-size: 0.7em;" -->

----

## Assertion

<div>

* Zusicherung / Sicherstellung / Assertion (lat. Aussage / Behauptung)
  * Definition einer Erwartungshaltung zum Vergleich gegen den tatsächlichen Zustand
* JUnit Tests:
  * Klasse: ```Assertions``` (```org.junit.jupiter.api.Assertions```)
  * statische Methoden zur Definition eines erwartenden Ergebnisses (expected) zum Vergleich mit dem tatsächlichen Ergebnis (actual)
  * überladene Methoden mit zusätzlichem Parameter ```Message``` für eigene Meldungen
  * automatische Validierung der "Behauptung" durch das JUnit Test-Framework
  * beliebt als statischer Import zur direkten Nutzung der Methoden:

  ```Java
  import static org.junit.jupiter.api.Assertions.*;
  ```

  * Beispiele:

  ```Java
    Assertions.assertEquals(<expected>, <actual>[, <Message>]);
    Assertions.assertNotEquals(<expected>, <actual>[, <Message>]);
    Assertions.assertTrue(<actual>[, <Message>]);
    Assertions.assertFalse(<actual>[, <Message>]);
    Assertions.assertTimeout(<expected Duration>, <Executable>[, <Message>]);
    Assertions.assertThrows(<expected Exception-Class>, <Executable>[, <Message>]);
    ```

</div><!-- .element style="font-size: 0.8em;" -->

----
## JUnit5 - neue Annotationen

<div>

| Annotation | Beschreibung | 
|:----------:|:-------------|
| ```@DisplayName("descriptive name")``` | definiert den Anzeigename für den jeweiligen Test / die Testklasse |
| ```@Nested``` | markiert eine innere (geschachtelte) Testklasse -> Strukturierung |
| ```@RepeatedTest(count)``` | sich wiederholender Testfall |
| ```@ParameterizedTest``` | Testfall Parametrisierung -> siehe nächste Slide |

</div><!-- .element style="font-size: 0.7em;" -->

----
## ```@ParameterizedTest```

* Separierung von Test-Code und Testfall
* verschiedene Quellen für Testfälle
  * ```@ValueSource```
  * ```@EmptySource``` / ```@NullSource``` / ```@NullAndEmptySource```
  * ```@EnumSource```
  * ```@CsvSource``` / ```@CsvFileSource```
  * ```@MethodSource```

----
## JUnit5 - Nützliches

### Testen von Ausnahmen
```Java
Exception assertThrows(ExceptionClass, Executable)
```

### Testen von mehrer Annotationen auf einmal
```Java
void assertAll(Executable ...);
```

### Testen der Laufzeit
```Java
void assertTimeout(Duration, Executable);
```

----
## Beispiel: Einfache Test-Klasse
```Java
import excercises.exkurs.junit.Calculator;
import org.junit.jupiter.api.*;

class CalculatorTest {

    Calculator myCalculator;
    double result = 0;

    @BeforeEach
    void setUp() {
        myCalculator = new Calculator();
        result = 0;
    }

    @Test
    @DisplayName("adding two numbers")
    void add() {
        result = myCalculator.add(5.0, 10.0);
        Assertions.assertEquals(15.0, result);
    }
}

```

----
## F.I.R.S.T. Principal
* **Fast**: Die Testausführung soll schnell sein, damit man sie möglichst oft ausführen kann. Je öfter man die Tests ausführt, desto schneller bemerkt man Fehler und desto einfacher ist es, diese zu beheben.
* **Independent**: Unit-Tests sind unabhängig voneinander, damit man sie in beliebiger Reihenfolge, parallel oder einzeln ausführen kann.
* **Repeatable**: Führt man einen Unit-Test mehrfach aus, muss er immer das gleiche Ergebnis liefern.
* **Self-Validating**: Ein Unit-Test soll entweder fehlschlagen oder gut gehen. Diese Entscheidung muss der Test treffen und als Ergebnis liefern. Es dürfen keine manuellen Prüfungen nötig sein.
* **Timely**: Man soll Unit-Tests vor der Entwicklung des Produktivcodes schreiben.



---
# Optionals

> TODO... :-)


--- 
# Programming Principals

> DRY, KISS, ... TODO... :-)
