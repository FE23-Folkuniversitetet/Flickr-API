![poster](poster.png)

# Introduktion
Att förstå hur man jobbar mot API:er är en väsentlig kunskap för frontendutvecklare! Bemästrar man den tekniken finns det ingen hejd på coola tjänster som kan byggas :smiley:

## Detta ska ni göra
Ni ska med hjälp av Flickrs API utveckla en webbapp med *html*, *css* och *vanilla JS* där ni kan ```söka fram``` och ```på ett snyggt sätt``` presentera bilder.


## Om Flickrs API

### API nyckel
För att få tillgång till Flickers servrar behövs en API-nyckel. Den är gratis, men kräver att ni registrerat ett flickr-konto. Ni skaffar en API-nyckel [här](https://www.flickr.com/services/api/misc.api_keys.html).

### Metoder och argument
Flickrs API är gigantiskt och innehåller många *resurser*. Ni kommer endast använda metoden ```flickr.photos.search``` i denna examination.

Flickr API utgår ifrån denna basURL: 
```https://api.flickr.com/services/rest```

Således blir hela *basURL:en* ( sen tillkommer params ):

```
https://api.flickr.com/services/rest?method=flickr.photos.search
```

### Query Params

**Query params** kallas de förfrågningar man skickar med till servern. Dessa bestämmer **vad** och **hur** du får svar från servern. Varje förfrågan kallas för ett *argument* i sökningen. Argumenten skickas oftast med i [själva adressen](https://en.wikipedia.org/wiki/Query_string) och formateras enligt följande:

```
https://url.to.api?paramName=paramValue&paramName=paramValue...
```

Flickrs metod **flickr.photos.search** har [många valbara argument](https://www.flickr.com/services/api/flickr.photos.search.html), men endast ett är obligatoriskt och det är ```api_key```, d.v.s själva nyckeln för att få svar från servern. 

Det finns ingen standarisering vilka argument som finns vid en API-resurs utan detta är något man måste [läsa sig till i dokumentationen](https://www.flickr.com/services/api/flickr.photos.search.html).

Ett argument som *bör* vara med är ```format=json```då Flickrs API stödjer ett gäng fler andra format. Detta gör att ni får tillbaka JSON som en callback. Detta blir lite meckigt att jobba med, så lägg även på argumentet ```&nojsoncallback=1```. 


En adress kan innehålla ett eller flera argument och kan bli väldigt lång!

En hel förfrågan kan se ut såhär:

```
https://api.flickr.com/services/rest?method=flickr.photos.search&api_key=abc12378asdashdjsah8sds&text=banana&per_page=20&sort=date-taken-asc&format=json&nojsoncallback=1
```

Och såhär kan det se ut i er JS-kod:

```
  let url = `${baseUrl}?api_key=${apiKey}&method=${method}&text=${text}&page=${currentPage}&format=json&nojsoncallback=1`;
```

### Flickrs bild URL:er
JSON kan inte innehålla bilder, så den datan ni får tillbaka använder några olika parametrar för att *bygga ihop* en url till bilden. Detta beskrivs väldigt tydligt [i dokumentationen](https://www.flickr.com/services/api/misc.urls.html).

Bildadresser byggs ihop enligt följande:

```
https://farm{farm-id}.staticflickr.com/{server-id}/{id}_{secret}_[mstzb].jpg
```

```farm-id```, ```server-id```, ```id``` och ```secret```, är alla params du får tillbaka från servern. Det du bestämmer själv är storlek ( ```size``` ) på bilden samt ev. annat bildformat ( default är jpg vilket är bäst i 99% av fallen).

En hel bildadress ser ut så här:

```
https://farm1.staticflickr.com/2/1418878_1e92283336_m.jpg
```

Och det kan se ut såhär i er JS-kod: 

```
let url = `https://farm${img.farm}.staticflickr.com/${img.server}/${img.id}_${img.secret}_${imgSize}.jpg`;
```

## Bedömning
### Godkänt
En webbapp byggd på Flickrs API där ni:
- använt HTML, CSS ( inkl flexbox ) och vanilla JS
- kan söka efter bilder med hjälp av textsök
- visar sökresultatet på ett snyggt sätt i ett galleri
- kan presentera klickad bild i större storlek ( ex. [lightbox effekt](https://en.wikipedia.org/wiki/Lightbox_(JavaScript)) )

### Level-up
- pagnation-funktionalitet där det går att bläddra mellan olika sidor av sökresultaten
- felhantering där felkoden meddelas användaren

