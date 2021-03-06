## Using locallang.xlf in your Flux/VHS Provider Extension

### Foreword

To prepare your Provider-Extension to use it with different languages, you need to move all visible labels and descriptions from
your Template, Partials and Layout files into a locallang-file. So TYPO3 can take care of which locallang should be loaded, both
for back- and frontend.

If you dont use labels or descriptions in your Page- or Content templates, Flux will look into the ``Resources/Private/Language``
folder of your extension and will recognize if there is a label/description (or translation) available for the label key. If
present, Flux will add this label/description in the backend-view for these elements. So there is basically no need for these
attributes in your template-files.

### A note about default languages

**You should work in English first, you can always change the default language later using TYPO3's language configuration.** Doing
this makes it much easier to share your examples, get support, avoid confusion with label names and of course it makes your work
suitable for use with translation software like Pootle (see fx http://translation.typo3.org). Remember: English is the official
language of TYPO3.

### Working with locallang.xlf

Gernerally you should take a look at this article:

> http://docs.typo3.org/TYPO3/CoreApiReference/Internationalization/Introduction/Index.html

If you want to work with ``locallang.xlf`` you need to create it in the following folder:
``typo3conf/ext/**YOUREXT**/Resources/Private/Language/``

The file ``locallang.xlf`` is used for the default language of your web site and should be in English.

For other languages simply create a new file with the ISO code in front of the filename like this:

- For German use ``de.locallang.xlf``
- For French use ``fr.locallang.xlf``
- ...

For a list of ISO language codes you can visit http://www.loc.gov/standards/iso639-2/php/code_list.php

All Languagefiles should at least contain the following:

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<xliff version="1.0">
        <file source-language="en" datatype="plaintext" original="messages" date="2012-10-17T17:55:17Z" product-name="**YOUREXT**">
                <header/>
                <body>
                </body>
        </file>
</xliff>
```

## Translate labels and description in the backend ##

In this example, we will translate the following Flux form element:
(Please notice, that this is a Configuration section for a Page template. Content- and Plugin templates require an additional
``flux:form.content`` tag in ``flux:grid.column``)

```
<f:section name="Configuration">
    <flux:form id="settings.defaultpage" >
        <flux:form.sheet name="settings.basics">
            <flux:form.field.checkbox name="settings.includenavi" />
            <flux:grid>
                <flux:grid.row>
                    <flux:grid.column colPos="0" name="content"/>
                </flux:grid.row>
            </flux:grid>
        </flux:form.sheet>
    </flux:form>
</f:section>
```

So we need to add labels and/or description for

- the form itself
- the sheet called "basic"
- the checkbox called "includenavi"
- the grid.colum called "content"

To achieve that, we place this code in the ``locallang.xlf`` in the ``body`` tag for each element:
```xml
<trans-unit id="ID.and.path.of.the.element">
      <source>Label or description to be shown</source>
</trans-unit>
```
So basically it always is ``flux.formID.type.name-of-the-element``

In our example, we add the following to the default xlf-file (``locallang.xlf``):

```xml
<trans-unit id="flux.defaultpage">
<source>Default Pagelayout</source>
</trans-unit>
<trans-unit id="flux.defaultpage.sheets.basics">
<source>Basic Configuration</source>
</trans-unit>
<trans-unit id="flux.defaultpage.fields.includenavi">
<source>Include navigation</source>
</trans-unit>
<trans-unit id="flux.defaultpage.columns.content">
<source>Content-Area</source>
</trans-unit>
```

As you can find in ``typo3conf/ext/flux/Classes/Form/AbstractFormComponent.php`` --> ``public function getLabel()`` these types
are available:

- sheets (flux.sheets.id)
- sections
- grids
- columns
- objects
- areas
- containers
- fields

### The whole file is now looking like this: ###

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<xliff version="1.0">
    <file source-language="en" datatype="plaintext" original="messages"
          date="2012-10-17T17:55:17Z" product-name="**YOUREXT**">
        <header/>
        <body>
            <trans-unit id="flux.defaultpage">
				<source>Default Pagelayout</source>
			</trans-unit>
			<trans-unit id="flux.defaultpage.sheets.basics">
				<source>Basic Configuration</source>
			</trans-unit>
			<trans-unit id="flux.defaultpage.fields.includenavi">
				<source>Include navigation</source>
			</trans-unit>
			<trans-unit id="flux.defaultpage.columns.content">
				<source>Content-Area</source>
			</trans-unit>
        </body>
    </file>
</xliff>
```

## Working with other (additional) languages ##

To add translations for further languages we need to create the ``locallang.xlf`` for each languages and name it this way:
``iso.locallang.xlf`` (for example ``de.locallang.xlf``). This file also contains this structure:

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<xliff version="1.0">
    <file source-language="en" datatype="plaintext" original="messages"
          date="2012-10-17T17:55:17Z" product-name="**YOUREXT**">
        <header/>
        <body>
        </body>
    </file>
</xliff>
```

To tell TYPO3 which language this is for, it is not enough to name the file. We need to extend the ``<file>`` tag within the
``iso.locallang.xlf`` with the target language like this:

```xml
<file source-language="en" datatype="plaintext" original="messages"
date="2012-10-17T17:55:17Z" product-name="ext-name" target-language="de">
```

As you can see we added the language target "de" by adding **target-language="de"**

The next thing to do is to add the translation like we did in the default language-file - with one difference: instead of the
```xml
<source>my translation</source>
```

we use

```xml
<target>my translation</target>
```

The German file looks like this now (``de.locallang.xlf``):

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes" ?>
<xliff version="1.0">
	<file source-language="en" datatype="plaintext" original="messages"
	      date="2012-10-17T17:55:17Z" product-name="**YOUREXT**" target-language="de">
		<header/>
		<body>
			<trans-unit id="flux.defaultpage">
				<target>Standard-Seitenlayout</target>
			</trans-unit>
			<trans-unit id="flux.defaultpage.sheets.basics">
				<target>Basis Konfiguration</target>
			</trans-unit>
			<trans-unit id="flux.defaultpage.fields.includenavi">
				<target>Navigation einbinden</target>
			</trans-unit>
			<trans-unit id="flux.defaultpage.columns.content">
				<target>Inhaltsbereich</target>
			</trans-unit>
		</body>
	</file>
</xliff>
```

## Using the language-file for the frontend ##

If you want to use labels or descriptions in the frontend output, you should also place them in the ``locallang.xlf`` of the
target language. To display the label ``contactperson`` you can add this to your Template, Layout or Partial file:

```
<f:translate key="contactperson" extensionName="YOUREXT"/>
```

As an alternative you can use this tag inline like this:

```
{f:translate(key: 'contactperson', extensionName: 'YOUREXT')}
```

In the ``locallang.xlf`` place this within the body-tag:

```xml
<trans-unit id="contactperson">
	<source>Contactperson</source>
</trans-unit>
```

Again, to use it in a different language, place this in your ``iso.locallang.xlf`` (in this example in ``de.locallang.xlf``):

```xml
<trans-unit id="contactperson">
	<target>Ansprechpartner</target>
</trans-unit>
```
