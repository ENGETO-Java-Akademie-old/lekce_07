<p align="center">
  <img src="https://engeto.cz/wp-content/uploads/2019/01/engeto-square.png" width="200" height="200">
</p>

# Java - 7. lekce

## Co bychom měli mít hotové

## Co nás čeká

- [GIT Opakování](#git-opakovani)

## GIT Opakování

V minulé lekci jste si prošli základy gitu, jednotlivé koncepty. Ukázali jste si, jak použít git v příkazové řádce. Máte připravený ssh klíč, vyzkoušeli jste si vytvořit vlastní repozitář a v něm sami pracovat.

- Čas na otázky a vysvětlení

## Git a práce v týmu

Verzovací nástroje jsou důležitý nástroj i pro individualní vývojáře, ale jejich hlavní výhody se umocní při týmové práci. 

### Pull Request (nebo také Merge Request)

Důležitou součástí procesu vývoje procesu je review kódu ostatními členy týmu. Možností, jak přesně to provádět je celá řada a záleží na celé řadě faktorů. Co je ale pro všechny společné je to, že je potřeba nástroj, který umožní jednoduše a přehledně řídit celý proces.

Pull request je vytvoření žádosti o `git merge` (nikoliv `git pull`) mezi dvěma vybranými větvema. Daný pull request pak umožní ostatním komentovat jednotlivé změny a případně hlasovat o dané změně.

Práce s Pull Requestem se trochu liší v různých nástrojích na správu git repozitářů, ale princip je pořád stejný. GitHub, GitLab nebo BitBucket nabízejí celou řadu možností, jak s Pull Requesty pracovat.

### GitHub Flow

Git samotný je velice flexibilní nástroj, který nevynucuje určitý způsob práce. Pro koordinovanou a efektivní práci v týmu je ale nutné se domluvit na určitých pravidlech a ta dodržovat. Existuje několik osvědčených metodologií. V této lekci si ukážeme jednu z těch jednodušších - GitHub Flow. Pro zájemce další jsou například Git Flow, GitLab Flow nebo Trunk Based Development.

1. Vytvořte novou větev (např. feature/Ticket123-NejakyPopis nebo bugfix/Bug234-PopisBugu)
2.1 Upravte soubory
2.2 Commit a push souborů do dané větve
3. Vytvořte pull request dané větve do hlavní větve
4. Úprava připomínek
5. Merge pull requestu do hlavní větve
6. Smazání dané větve

## IDE pro GIT

Existuje určitá kontroverze jestli používat jenom příkazovou řádku pro git nebo použít GUI nástroje. Určitě je dobré si oboje vyzkoušet a naučit se základní principy gitu. Jak to pak budete používat v praxi je na vás.

Z mého pohledu některé věci jsou v GUI mnohem přehlednější.

- Zobrazení grafu commitů
- Řešení konfliktů
- Příprava commitu vetšího množství souborů (ale ne všech)

### Github Desktop

Jeden z populárních nástrojů, který je dobře integrovaný s GitHubem je GitHub Desktop. Podporuje i jiné repozitáře než jenom GitHub.

https://desktop.github.com/

Ukázka:

### SourceTree

Další populární nástroj je SourceTree od společnosti Atlassian. Provozují Jiru a Git server BitBucket.

https://www.sourcetreeapp.com/

Ukázka:

### IDEA plugin

Dnes si ještě ukážeme, integrované nástroje pro práci s Gitem v IDE, které používáme v našem kurzu.

Nic dalšího není potřeba stahovat.

Ukázka


### Několik praktických ukázek práce s gitem

1. Vytvoření feature branche a merge do hlavní větve
2. Konflikt a jeho řešení
3. Vytvoření pull requestu

## Maven

V předchozích lekcích jsme ukázali jak program zkompilovat a spustit pomocí IDE. Jak to ale funguje u větších projektů, které mají závislosti na knihovnách třetích stran?



### Artefakty javových projektů

- Jar
- Spustitelný Jar
- War
- Ear
- nebo obyčejný zip

### Bez nástroje

1. Stáhnou Jar nějaké knihovny a přidat na classpath
2. Udělat Jar ručně
3. Spustitelný Jar

Proč ruční řešení po nějaké době přestane fungovat?
- Co když někdo vydá novou verzi knihovny?
- Co když přijde nový vývojář do týmu?
- Jak celou věc nasadíme na server?
- Jakou strukturu ma mit projekt?

### Maven

- Řešení 

#### POM (Project Object Model)

```
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>org.baeldung</groupId>
    <artifactId>org.baeldung</artifactId>
    <packaging>jar</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>org.baeldung</name>
    <url>http://maven.apache.org</url>
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
            //...
            </plugin>
        </plugins>
    </build>
</project>
```

#### Identifikace projektu

groupId - unikátní jméno organizace, které projekt patří (např cz.engeto)
artifactId - unikátní jméno projektu nebo modulu
version - identifikátor verze
packaging - metoda zabalení projektu pro distribuci (JAR, WAR, ZIP)

#### Verze `-SNAPSHOT`

Na release aplikace nebo knihovny se můžeme dívat jako dvou fázový proces. Nejdříve vybereme verzi, kterou chceme releasovat, provedeme celý proces buildu a testování. Pokud všechno projede správně, tak můžeme verzi uložit jako stabilní. Pro první stav je běžné v Mavenu použít připonu `-SNAPSHOT`. Což označuje nestabilní build, který se může ještě změnit.

#### Závislosti

Jak jsme si definovali vlastní projekt, tak jsou definované i jiné projekty, které můžeme použít. Když je potřebujeme do projektu přidat jako závislost, tak je jenom potřebujeme přidat do nodu `<dependencies>`.

Můžeme navíc specifikovat i `scope` pokud potřebujeme závislost pro běh programu nebo jenom unit testy. Možností je víc, ale pro začátek nám stačí vědět, že `compile` je výchozí hodnota a ani není nutné ji explicitně uvádět.

```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-core</artifactId>
    <version>4.3.5.RELEASE</version>
    <scope>compile</scope>
</dependency
```

### Populární public repositáře

https://central.sonatype.org/

https://www.deps.co/guides/public-maven-repositories/

```
<repositories>
    <repository>
        <id>JBoss repository</id>
        <url>http://repository.jboss.org/nexus/content/groups/public/</url>
    </repository>
</repositories>
```

### Proces

`validate` – kontrola projektu
`compile` – zkompiluje projekt a vytvoří požadovaný binární artefakty
`test` – spustí unit testy
`package` – zabalí zkompilovaný kód do balíčku
`integration-test` – spustí další sadu testů, která požaduje kompletní build aplikace
`verify` – zkontroluje validitu balíčku
`install` – uloží vytvořený balíček do lokálního Maven repozitáře (je pak dostupný v dalších projektech)
`deploy` – nahraje vytvořený balíček do vzdáleného Maven repozitáře (pozor může to být veřejně dostupný repozitář)

#### Použití properties

Častá praxe je definovat si na jednom místo verze knihoven a poté je použít jako proměnnou na všech místech. Proměnou definujeme jako `<key>value<key>` v tagu `<properties>`.
```
<properties>
    <spring.version>4.3.5.RELEASE</spring.version>
</properties>
```

a proměnou dále použijeme pomocí `${key}`:
```
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-core</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>
</dependencies>
```
