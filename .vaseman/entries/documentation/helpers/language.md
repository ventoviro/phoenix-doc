layout: documentation.twig
title: Language Helper

---

# Google Translate

``` php
echo \Windwalker\Helper\LanguageHelper::translate('飛', 'zh-tw', 'en');

// Result is: fly
```

We can set the 4th params (eg: 500) to separate long text (Google translate API has some limit on text length).

# Load Language Files of any Component

``` php
\Windwalker\Helper\LanguageHelper::loadLanguage('com_content', 'site' or 'admin');
```

This code will include all language files of content component.
