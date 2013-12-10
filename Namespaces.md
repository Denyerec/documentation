## GIT Master & 6.1 6.0

Using 6.2-dev: You are fine, dont worry.


If you are upgrading flux to the current git master on typo3 6.0 or 6.1 you will currently break your installation. This is because of a bug in typo3:

http://forge.typo3.org/issues/54115

You have 2 ways to fix this:

### Core Hack:

Change 1 line of code:

https://review.typo3.org/#/c/25814/9/typo3/sysext/fluid/Classes/Core/Parser/TemplateParser.php

You are pretty safe to do that, as the change will be backported to 6.0 and 6.1 on the next release.

### Change Templates (Preferred):

Change every occurence of 

* ``{namespace flux=Tx_Flux_ViewHelpers}`` to ``{namespace flux=FluidTYPO3\Flux\ViewHelpers}``
* ``flux:flexform`` to ``flux:form``
* ``flux:flexform.grid`` to ``flux:grid``
* ``flux:flexform.grid.column`` to ``flux:grid.column``
* ``flux:flexform.grid.row`` to ``flux:grid.row``
* ``flux:flexform.container`` to ``flux:form.container``
* ``flux:flexform.data`` to ``flux:form.data``
* ``flux:flexform.object`` to ``flux:form.object``
* ``flux:flexform.section`` to ``flux:form.section``
* ``flux:flexform.sheet`` to ``flux:form.sheet``
* ``flux:flexform.field.wizard.add`` to ``flux:wizard.add``
* ``flux:flexform.field.wizard.colorPicker`` to ``flux:wizard.colorPicker``
* ``flux:flexform.field.wizard.edit`` to ``flux:wizard.edit``
* ``flux:flexform.field.wizard.link`` to ``flux:wizard.link``
* ``flux:flexform.field.wizard.list`` to ``flux:wizard.list``
* ``flux:flexform.field.wizard.select`` to ``flux:wizard.select``
* ``flux:flexform.field.wizard.slider`` to ``flux:wizard.slider``
* ``flux:flexform.field.wizard.suggest`` to ``flux:wizard.suggest``
* ``flux:flexform.field.checkbox`` to ``flux:field.checkbox``
* ``flux:flexform.field.controllerActions`` to ``flux:field.controllerActions``
* ``flux:flexform.field.custom`` to ``flux:field.custom``
* ``flux:flexform.field.file`` to ``flux:field.file``
* ``flux:flexform.field.inline`` to ``flux:field.inline``
* ``flux:flexform.field.inline.fal`` to ``flux:field.inline.fal``
* ``flux:flexform.field.input`` to ``flux:field.input``
* ``flux:flexform.field.relation`` to ``flux:field.relation``
* ``flux:flexform.field.select`` to ``flux:field.select``
* ``flux:flexform.field.text`` to ``flux:field.text``
* ``flux:flexform.field.tree`` to ``flux:field.tree``
* ``flux:flexform.field.userFunc`` to ``flux:field.userFunc``
* ``flux:flexform.content`` to ``flux:form.content``