---

layout: documentation.twig
title: Start A Blog

---

# Introduction

In this chapter, we'll step by step to create a simple blog system, that helps you understand how to use phoenix.

# Create Admin Package

First, we have to create a basic blog admin package. please type this command:

``` bash
php bin/console muse init Blog/Admin category.categories
php bin/console muse add-subsystem Blog/Admin article.articles
php bin/console muse add-subsystem Blog/Admin comment.comments
```

After package created, register package and add assets link.

``` php
// src/Windwalker/Windwalker.php

class Windwalker extends \Windwalker\Core\Windwalker
{
	public static function loadPackages()
	{
		return array(
			'system' => new SystemPackage,
			'phoenix' => new PhoenixPackage,
			'admin' => new \Blog\Admin\AdminPackage,
		);
	}

	// ...
```

``` bash
$ php bin/console asset sync admin
```

And add routing to `/etc/routing.yml`.

``` yaml
# /etc/routing.yml

# ...

admin:
    pattern: /admin
    package: admin
```

# Migration

Open `src/Blog/Admin/*.php` files, change migration like below:

``` php
// src/Blog/Admin/xxxxxxxxxxxxxx_CategoryInit.php

// ...

class CategoryInit extends AbstractMigration
{
	public function up()
	{
		$this->db->getTable(Table::CATEGORIES, true)
			->addColumn(new Column\Primary('id'))
			->addColumn(new Column\Varchar('title'))
			->addColumn(new Column\Varchar('alias'))
			->addColumn(new Column\Datetime('created'))
			->addColumn(new Column\Integer('created_by'))
			->addColumn(new Column\Datetime('modified'))
			->addColumn(new Column\Integer('modified_by'))
			->addColumn(new Column\Integer('ordering'))
			->addColumn(new Column\Tinyint('state'))
			->addColumn(new Column\Char('language', 7))
			->addColumn(new Column\Text('params'))
			->addIndex(Key::TYPE_INDEX, 'idx_categories_alias', 'alias')
			->addIndex(Key::TYPE_INDEX, 'idx_categories_alias', 'language')
			->addIndex(Key::TYPE_INDEX, 'idx_categories_created_by', 'created_by')
			->create(true);
	}

	public function down()
	{
		$this->db->getTable(Table::CATEGORIES, true)->drop(true);
	}
}
```

``` php
// src/Blog/Admin/xxxxxxxxxxxxxx_ArticleInit.php

class ArticleInit extends AbstractMigration
{
	public function up()
	{
		$this->db->getTable(Table::ARTICLES, true)
			->addColumn(new Column\Primary('id'))
			->addColumn(new Column\Integer('category_id'))
			->addColumn(new Column\Varchar('title'))
			->addColumn(new Column\Varchar('alias'))
			->addColumn(new Column\Text('introtext'))
			->addColumn(new Column\Text('fulltext'))
			->addColumn(new Column\Integer('version'))
			->addColumn(new Column\Datetime('created'))
			->addColumn(new Column\Integer('created_by'))
			->addColumn(new Column\Datetime('modified'))
			->addColumn(new Column\Integer('modified_by'))
			->addColumn(new Column\Integer('ordering'))
			->addColumn(new Column\Tinyint('state'))
			->addColumn(new Column\Char('language', 7))
			->addColumn(new Column\Text('params'))
			->addIndex(Key::TYPE_INDEX, 'idx_articles_alias', 'alias')
			->addIndex(Key::TYPE_INDEX, 'idx_articles_alias', 'language')
			->addIndex(Key::TYPE_INDEX, 'idx_articles_created_by', 'created_by')
			->addIndex(Key::TYPE_INDEX, 'idx_articles_category_id', 'category_id')
			->create(true);
	}

	public function down()
	{
		$this->db->getTable(Table::ARTICLES, true)->drop(true);
	}
}
```

``` php
// src/Blog/Admin/xxxxxxxxxxxxxx_CommentInit.php

class CommentInit extends AbstractMigration
{
	public function up()
	{
		$this->db->getTable(Table::COMMENTS, true)
			->addColumn(new Column\Primary('id'))
			->addColumn(new Column\Integer('article_id'))
			->addColumn(new Column\Varchar('name'))
			->addColumn(new Column\Varchar('email'))
			->addColumn(new Column\Text('text'))
			->addColumn(new Column\Datetime('created'))
			->addColumn(new Column\Integer('ordering'))
			->addColumn(new Column\Tinyint('state'))
			->addColumn(new Column\Text('params'))
			->addIndex(Key::TYPE_INDEX, 'idx_comments_article_id', 'article_id')
			->create(true);
	}

	public function down()
	{
		$this->db->getTable(Table::COMMENTS, true)->drop(true);
	}
}
```

Run migration:

``` bash
php bin/console migration migrate -p=admin
```

Now you can open `http://{your_site}/admin/categories` to see your admin page.

# Fake Data

We must add some fake data to help us developing. Use seeder to do this work, please modify `src/Blog/Admin/Seed/*.php` files.

First check that the seeder ordering is `CategorySeeder` -> `ArticleSeeder` -> `CommentSeeder` in `DatabaseSeeder`.

``` php
// src/Blog/Admin/DatabaseSeeder.php

// ...

class DatabaseSeeder extends AbstractSeeder
{
	/**
	 * doExecute
	 *
	 * @return  void
	 */
	public function doExecute()
	{
		$this->execute(new CategorySeeder);

		$this->execute(new ArticleSeeder);

		$this->execute(new CommentSeeder);

		// @muse-placeholder  seeder-execute  Do not remove this.
	}

	// ...
```

Then add modify all other seeder class to:

``` php
// src/Blog/Admin/Seed/CategorySeeder.php

// ...

class CategorySeeder extends AbstractSeeder
{
	public function doExecute()
	{
		$faker = Factory::create();

		$mapper = new CategoryMapper;

		foreach (range(1, 7) as $i)
		{
			$data = new Data;

			$data['title']       = $faker->word;
			$data['alias']       = OutputFilter::stringURLSafe($data['title']);
			$data['version']     = rand(1, 50);
			$data['created']     = $faker->dateTime->format(DateTime::FORMAT_SQL);
			$data['created_by']  = rand(20, 100);
			$data['modified']    = $faker->dateTime->format(DateTime::FORMAT_SQL);
			$data['modified_by'] = rand(20, 100);
			$data['ordering']    = $i;
			$data['state']       = $faker->randomElement(array(1, 1, 1, 1, 0, 0));
			$data['language']    = 'en-GB';
			$data['params']      = '';

			$mapper->createOne($data);

			$this->command->out('.', false);
		}

		$this->command->out();
	}

	public function doClean()
	{
		$this->db->getTable(Table::CATEGORIES)->truncate();
	}
}
```

``` php
// src/Blog/Admin/Seed/ArticleSeeder.php

// ...

class ArticleSeeder extends AbstractSeeder
{
	public function doExecute()
	{
		$faker = Factory::create();

		$categories = with(new CategoryMapper)->findAll();

		$mapper = new ArticleMapper;

		foreach ($categories as $category)
		{
			foreach (range(1, rand(3, 5)) as $i)
			{
				$data = new Data;

				$data['title']       = $faker->sentence(rand(3, 5));
				$data['alias']       = OutputFilter::stringURLSafe($data['title']);
				$data['category_id'] = $category->id;
				$data['introtext']   = $faker->paragraph(5);
				$data['fulltext']    = $faker->paragraph(5);
				$data['version']     = rand(1, 50);
				$data['created']     = $faker->dateTime->format(DateTime::FORMAT_SQL);
				$data['created_by']  = rand(20, 100);
				$data['modified']    = $faker->dateTime->format(DateTime::FORMAT_SQL);
				$data['modified_by'] = rand(20, 100);
				$data['ordering']    = $i;
				$data['state']       = $faker->randomElement(array(1, 1, 1, 1, 0, 0));
				$data['language']    = 'en-GB';
				$data['params']      = '';

				$mapper->createOne($data);

				$this->command->out('.', false);
			}
		}

		$this->command->out();
	}

	public function doClean()
	{
		$this->db->getTable(Table::ARTICLES)->truncate();
	}
}
```

``` php
// src/Blog/Admin/Seed/CommentSeeder.php

// ...

class CommentSeeder extends AbstractSeeder
{
	public function doExecute()
	{
		$faker = Factory::create();

		$articles = with(new ArticleMapper)->findAll();

		$mapper = new CommentMapper;

		foreach ($articles as $article)
		{
			foreach (range(1, rand(1, 7)) as $i)
			{
				$data = new Data;

				$data['article_id'] = $article->id;
				$data['name']       = $faker->name;
				$data['email']      = $faker->email;
				$data['text']       = $faker->paragraph(5);
				$data['created']    = $faker->dateTime->format(DateTime::FORMAT_SQL);
				$data['ordering']   = $i;
				$data['state']      = $faker->randomElement(array(1, 1, 1, 1, 0, 0));
				$data['params']     = '';

				$mapper->createOne($data);

				$this->command->out('.', false);
			}
		}

		$this->command->out();
	}

	public function doClean()
	{
		$this->db->getTable(Table::COMMENTS)->truncate();
	}
}
```

Run seeder import

``` bash
$ php bin/console seed import -p=admin
```

If migration and seeder works fine, open the admin page, you will see sample data to test.

![Imgur](http://i.imgur.com/qhyCxmp.jpg)

The first `Categories` menu item is a placeholder, you can delete it in `src/Blog/Admin/Templates/_global/admin/submenu.blade.php`.

