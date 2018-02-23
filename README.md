This NPM package allows you to easily self-host the Karmilla webfont, a fork of Karla.

[Karmilla](https://ms-studio.net/notes/karmilla-a-friendly-fork-of-karla/) is a friendly fork of
[Karla](https://fonts.google.com/specimen/Karla), an open source grotesque sans serif typeface by
[Jonathan Pinhorn](https://twitter.com/jonpinhorn_type).
It has been maintained by [Manuel Schmalstieg](https://github.com/ms-studio) and the community since 2012.
The modifications done to the original typeface are small.
The fork has been renamed to Karmilla to respect the OFL license requirement
(modified versions need to use a different reserved font name).


## How to use

This setup is similar to the one used in the [typefaces](https://github.com/KyleAMathews/typefaces) project.
It assumes you are using webpack with loaders for CSS and font files.
Many tools such as [Create React App](https://github.com/facebookincubator/create-react-app)
and [Gatsby](https://github.com/gatsbyjs/gatsby) will work without any changes to your configuration.

Simply install this package with:

```
npm install github:dmfrancisco/typeface-karmilla
```

Then in your entry file:

```js
import "typeface-karmilla";
```

Finally, in your CSS file you can use it like this:

```css
body {
  font-family: 'Karmilla', sans-serif;
}
```

## Importing specific font styles

Browsers usually only download the font files that are necessary.
This means if your page does not use bold or italics for example, those font files won't be downloaded.
However, in some situations you may want to use one of these styles but don't want to trigger an additional download.

Imagine that in your entire page you only have a couple italicized words.
In that case, you may prefer to let the browser create the italic style instead (referred to as faux-italics and faux-bold).
You can import specific styles like this:

```js
import "typeface-karmilla/regular.css";
import "typeface-karmilla/bold.css";
import "typeface-karmilla/italic.css";
import "typeface-karmilla/bold-italic.css";
```

## Supporting old browsers

If you still need to support old browsers (marked as red in [this list](https://caniuse.com/?browserset=since%202001#feat=woff))
you can import the following files instead:

```js
import "typeface-karmilla/regular-best.css";
import "typeface-karmilla/bold-best.css";
import "typeface-karmilla/italic-best.css";
import "typeface-karmilla/bold-italic-best.css";
```

These files follow the same structure defined by the [Google Webfonts Helper](https://google-webfonts-helper.herokuapp.com)
app when the "Best Support" option is activated. Keep in mind that while these files include multiple formats,
the browser will only download the ones needed.

## Additional instructions

### Why are some files named Karmilla and others Karla?

Karmilla [doesn't offer italic styles](https://github.com/ms-studio/karmilla/issues/15) at the moment.
As a fallback, the Karla files are used instead, which you can opt out from. This means "ç" for example won't be displayed correctly in this style.

### I only need the extra cedilla

[According to Font Squirrel](https://fontsquirrel.com/fonts/karla), the original Karla fonts supports the following languages:

> Alsatian, Arapaho, Arrernte, Aymara, Bislama, Breton, Cebuano, Chamorro, Corsican, English, Fijian, French Creole (Saint Lucia), Frisian, Galician, Gilbertese (Kiribati), Haitian Creole, Hiligaynon, Hmong, Hopi, Ibanag, Iloko (Ilokano), Indonesian, Interglossa (Glosa), Interlingua, Irish (Gaelic), Italian, Lojban, Lombard, Luxembourgian, Malagasy, Mohawk, Norfolk/Pitcairnese, Oromo, Pangasinan, Papiamento, Piedmontese, Potawatomi, Rhaeto-Romance, Romansh (Rumantsch), Rotokas, Scots (Gaelic), Seychellois Creole (Seselwa), Shona, Somali, Southern Ndebele, Swahili, Swati/Swazi, Tagalog (Filipino/Pilipino), Tetum (Tetun), Tok Pisin, Uyghur (Latinized), Volapük, Warlpiri, Xhosa, Yapese and Zulu.

You can check the changes that were done for Karmilla in the [official repository](https://github.com/ms-studio/karmilla#changes).
This package also includes a subset of Karmilla that should contain all glyphs necessary for the additional following languages:

> Portuguese, Spanish, French, German and Dutch.

These files were created by applying the same
[FontSquirrel Webfont Generator settings](https://github.com/ms-studio/karmilla/blob/master/webfontkit/karmilla-016/generator_config.txt)
that are specified in the Karmilla repository to the [TTF files](https://github.com/ms-studio/karmilla/tree/master/ttf)
with a custom subsetting (Western Languages).

You can use it by importing the following files:

```js
import "typeface-karmilla/regular-subset.css";
import "typeface-karmilla/bold-subset.css";
import "typeface-karmilla/italic.css";
import "typeface-karmilla/bold-italic.css";
```

These files are half the size of Karmilla, but around 1.6x bigger than Karla.

### I want the cedilla while still using Google Fonts or the `typeface-karla` package

Google Fonts allows users to import specific glyphs from a font by specifying a `text` parameter.
For example, you could import the "ç" and "Ç" letters from Arimo, and then use it with Karla,
using the `typeface-karla` package, or also from Google Fonts with the following CSS:

```css
@import url(https://fonts.googleapis.com/css?family=Arimo&text=çÇ);
@import url(https://fonts.googleapis.com/css?family=Karla);

body {
  font-family: 'Arimo', 'Karla', sans-serif;
}
```

Because we only important the two letters from Arimo, the rest of the alphabet will fallback to Karla.
The **big caveat** with this approach is that your visitors may have Arimo installed on their machines,
which will cause the browser to use it instead, and so all your text will be rendered with Arimo.

A better solution would be to still host the fonts yourself by downloading them from the
the [Google Webfonts Helper](https://google-webfonts-helper.herokuapp.com) and removing `local('Arimo')` from the `src` properties.

### Other languages

Google Fonts also offers a Tamil script part of the familly with inclined and upright styles in two weights, Regular and Bold.
These are part of the early access program.

```css
@import url(//fonts.googleapis.com/earlyaccess/karlatamilinclined.css);
@import url(//fonts.googleapis.com/earlyaccess/karlatamilupright.css);
```

```css
body {
  font-family: 'Karla Tamil Inclined', sans-serif;
  font-family: 'Karla Tamil Upright', sans-serif;
}
```

## Credits

All credits go to the original authors.  
Read more about Karmilla here: https://github.com/ms-studio/karmilla  
Read more about typefaces here: https://github.com/KyleAMathews/typefaces
