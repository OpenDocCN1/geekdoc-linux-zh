![](bbox=[0.22, 0.16, 0.77, 0.48])

Figure 7.20 – The output of the application

# 7.6.2 Exercise 2 - Desktop application to translate text

In this exercise, let’s create a desktop widget that translates words in English to a language of your choice and at the same time practice using HTTPService calls.

For translation purposes, you can use the Google Ajax Language API which is an open source API used commonly by developers. You can have a look at this API at http://code.google.com/apis/ajaxlanguage/ to extend it further or to add additional languages to the application. Follow these steps:

+   1. Create a new Flex Project as a Desktop application.

+   2. Add two text inputs, one for the English word to be translated and the other for the translated text. You can add a Combo Box that lists the languages to which you want the text to be translated and a button which when clicked will cause the translation to take place. Listing 7.24 shows the code you can use.

```
<mx:TextInput x="157" y="59" id="textToTranslate"/> <mx:Button x="116" y="200" label="Translate" click="callGoogleLanguageTranslator()" width="104"/> <mx:Label x="10" y="61" text="Text to be translated" width="128" height="47"/> <mx:Label x="10" y="105" text="Translated text" width="119"/> <mx:TextInput x="157" y="103" id="translatedText"/>
```