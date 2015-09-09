---

layout: documentation.twig
title: Form & Edit

---

# Category Edit Page

Click Any category item, you will see edit page with a form and inputs.

We must modify this form to fit `categories` table.

Please open `src/Blog/Admin/Form/Category/EditDefinition.php` and change code to below.

``` php
// src/Blog/Admin/Form/Category/EditDefinition.php

namespace Blog\Admin\Form\Category;

use Phoenix\Field\CalendarField;
use Windwalker\Core\Language\Translator;
use Windwalker\Form\Field\HiddenField;
use Windwalker\Form\Field\RadioField;
use Windwalker\Form\Field\TextField;
use Windwalker\Form\FieldDefinitionInterface;
use Windwalker\Form\Form;
use Windwalker\Html\Option;

/**
 * The CategoryEditDefinition class.
 *
 * @since  {DEPLOY_VERSION}
 */
class EditDefinition implements FieldDefinitionInterface
{
	/**
	 * Define the form fields.
	 *
	 * @param Form $form The Windwalker form object.
	 *
	 * @return  void
	 */
	public function define(Form $form)
	{
		// Basic fieldset
		$form->wrap('basic', null, function(Form $form)
		{
			// ID
			$form->add('id', new HiddenField);

			// Title
			$form->add('title', new TextField)
				->label(Translator::translate('admin.category.field.title'))
				->required(true);

			// Alias
			$form->add('alias', new TextField)
				->label(Translator::translate('admin.category.field.alias'));
		});

		// Delete the Text Group...

		// Created fieldset
		$form->wrap('created', null, function(Form $form)
		{
			// No change...
		});
	}
}
```

# Article Edit Form

Then modify the article form.

Note we use `CategoryListField` for `category_id`.

``` php
// src/Blog/Admin/Form/Article/EditDefinition.php

namespace Blog\Admin\Form\Article;

use Blog\Admin\Field\Category\CategoryListField;
use Phoenix\Field\CalendarField;
use Windwalker\Core\Language\Translator;
use Windwalker\Form\Field\HiddenField;
use Windwalker\Form\Field\RadioField;
use Windwalker\Form\Field\TextareaField;
use Windwalker\Form\Field\TextField;
use Windwalker\Form\FieldDefinitionInterface;
use Windwalker\Form\Form;
use Windwalker\Html\Option;

class EditDefinition implements FieldDefinitionInterface
{
	/**
	 * Define the form fields.
	 *
	 * @param Form $form The Windwalker form object.
	 *
	 * @return  void
	 */
	public function define(Form $form)
	{
		// Basic fieldset
		$form->wrap('basic', null, function(Form $form)
		{
			// ID
			$form->add('id', new HiddenField);

			// Title
			$form->add('title', new TextField)
				->label(Translator::translate('admin.article.field.title'))
				->required(true);

			// Alias
			$form->add('alias', new TextField)
				->label(Translator::translate('admin.article.field.alias'));

			// Category
			$form->add('category_id', new CategoryListField)
				->label('Category')
				->addOption(new Option('Uncategorised', ''));
		});

		// Text Fieldset
		$form->wrap('text', null, function(Form $form)
		{
			// No change...
		});

		// Created fieldset
		$form->wrap('created', null, function(Form $form)
		{
			// No change...
		});
	}
}
```

Then we can choose category in article edit page.

![Imgur](http://i.imgur.com/eCT61tS.jpg)

# Comment Form

Same as article and category, but we use `ArticleModalField` to select article.

``` php
// src/Blog/Admin/Form/Comment/EditDefinition.php

namespace Blog\Admin\Form\Comment;

use Blog\Admin\Field\Article\ArticleModalField;
use Phoenix\Field\CalendarField;
use Windwalker\Core\Language\Translator;
use Windwalker\Form\Field\EmailField;
use Windwalker\Form\Field\HiddenField;
use Windwalker\Form\Field\RadioField;
use Windwalker\Form\Field\TextareaField;
use Windwalker\Form\Field\TextField;
use Windwalker\Form\FieldDefinitionInterface;
use Windwalker\Form\Form;
use Windwalker\Html\Option;

class EditDefinition implements FieldDefinitionInterface
{
	/**
	 * Define the form fields.
	 *
	 * @param Form $form The Windwalker form object.
	 *
	 * @return  void
	 */
	public function define(Form $form)
	{
		// Basic fieldset
		$form->wrap('basic', null, function(Form $form)
		{
			// ID
			$form->add('id', new HiddenField);

			// Name
			$form->add('name', new TextField)
				->label('Name')
				->required(true);

			$form->add('email', new EmailField)
				->label('Email')
				->required(true);

			// Article
			$form->add('article_id', new ArticleModalField)
				->label('Article');
		});

		// Text Fieldset
		$form->wrap('text', null, function(Form $form)
		{
			// Introtext
			$form->add('text', new TextareaField)
				->label('Text')
				->set('rows', 10);
		});

		// Created fieldset
		$form->wrap('created', null, function(Form $form)
		{
			// State
			$form->add('state', new RadioField)
				->label(Translator::translate('admin.comment.field.state'))
				->set('class', 'btn-group')
				->set('default', 1)
				->addOption(new Option(Translator::translate('phoenix.grid.state.published'), '1'))
				->addOption(new Option(Translator::translate('phoenix.grid.state.unpublished'), '0'));

			// Created
			$form->add('created', new CalendarField)
				->label(Translator::translate('admin.comment.field.created'));
		});
	}
}
```

You will see a Model select field, if you click the `Select an Item` button, will open a modal for select article.

![Imgur](http://i.imgur.com/AvKB3xf.jpg)

![Imgur](http://i.imgur.com/yOsuRgx.jpg)
