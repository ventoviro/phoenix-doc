layout: documentation.twig
title:  Modal Tools

---

# Original Bootstrap Modal

Please see [Bootstrap Document](http://getbootstrap.com/2.3.2/javascript.html#modals).

# Choose A DIV as Modal Box

Please write this HTML first:

``` html
<div id="myModal" class="modal hide fade">
    <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-hidden="true">&times;</button>
        <h3>Modal header</h3>
    </div>

    <div class="modal-body">
        <p>One fine body…</p>
    </div>

    <div class="modal-footer">
        <a href="#" class="btn">Close</a>
        <a href="#" class="btn btn-primary">Save changes</a>
    </div>
</div>
```

Then we add this code to PHP:

``` php
\Windawlker\Helper\ModalHelper::modal('myModal');
```

Joomla Will generate modal init JS in `<head>`:

``` javascript
$('#myModal').modal(options);
```

It only effect on `#myModal` div.

# Generate Modal Launch Link

If we need a link or button to call this modal, using:

``` php
echo \Windwalker\Helper\ModalHelper::modalLink('Link title', 'myModal');
```

This code will generate a link to launch `#myModal`. We can set some style, for example, add class in option params:

``` php
echo \Windwalker\Helper\ModalHelper::modalLink('Link title', 'myModal', array('class' => 'btn btn-mini'));
```

The result:

``` html
<a data-toggle="modal" data-target="#myModal" class="btn btn-mini">Link Title</a>
```

## Available options

``` php
$option = array(
    'tag'       => 'a' ,
    'id'        => 'myModal_link',
    'class'     => '',
    'onclick'   => '',
    'icon'      => ''
);
```

# Add Modal Link to Toolbar

``` php
\Windwalker\Helper\ToolbarHelper::modal( 'COM_FLOWER_MODAL_LINK', 'myModal');
```

# Dynamic Modal Content

We can wrap our content in a modal box:

``` php
$content = 'Some text or HTML.' ;
echo \Windwalker\Helper\ModalHelper::renderModal('myModal', $content, $option);
```

This will generate a modal box HTML link the begin of this page.

## Title & Footer

``` php
$option = array(
    'title'     => '',
    'footer'    => ''
);
```

If we don't add these two option, the reault will link below:

``` html
<div class="modal hide fade" id="myModal">
    <div id="myModal-container" class="modal-body">
        Some text or HTML.
    </div>
</div>
```

But we can add title and footer to modal box:

``` php
$content = '<input name="number" />' ;
$option['title'] = 'Choose A Number' ;
$option['footer'] = '<a href="#" class="btn">Close</a>
                    <a href="#" class="btn btn-primary">Save changes</a>' ;

echo \Windwalker\Helper\ModalHelper::renderModal('myModal', $content, $option);
```

The new result:

``` html
<div class="modal hide fade" id="myModal">
    <div class="modal-header">
        <button type="button" role="presentation" class="close" data-dismiss="modal">x</button>
        <h3>Choose A Number</h3>
    </div>

    <div id="myModal-container" class="modal-body">
        <input name="number" />
    </div>

    <div class="modal-footer">
        <a href="#" class="btn">Close</a>
        <a href="#" class="btn btn-primary">Save changes</a>
    </div>
</div>
```

