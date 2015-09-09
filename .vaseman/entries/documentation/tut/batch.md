---

layout: documentation.twig
title: Batch

---

# Add Category Batch

Open `Form/Articles/BatchDefinition.php` and add new configuration.

``` php
// src/Blog/Admin/Form/Articles/BatchDefinition.php

// ...

class BatchDefinition implements FieldDefinitionInterface
{
	public function define(Form $form)
	{
		$form->wrap(null, 'batch', function (Form $form)
		{
			// Add Category field
			$form->add('category_id', new CategoryListField)
				->label('Category')
				->addOption(new Option('-- Select Category --'));

			// Language
			$form->add('language', new ListField)
				->label('Language')
				->set('class', 'col-md-12')
				->addOption(new Option('-- Select Language --', ''))
				->addOption(new Option('English', 'en-GB'))
				->addOption(new Option('Chinese Traditional', 'zh-TW'))

				// Add FR-fr language
				->addOption(new Option('French', 'FR-fr'));

				// ...
		});
	}
}
```

Then we can batch move articles items to other category or language.

![Imgur](http://i.imgur.com/azcMe62.jpg)

![Imgur](http://i.imgur.com/mZARv5f.jpg)

Or copy it.

![Imgur](http://i.imgur.com/Rfag9OT.jpg)

The title will auto increment.

![Imgur](http://i.imgur.com/2fzbOY8.jpg)

