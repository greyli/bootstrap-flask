Use Macros
==========

These macros will help you to generate Bootstrap-markup codes quickly and easily.

render_nav_item()
------------------
Render a Bootstrap nav item.

Example
~~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/nav.html' import render_nav_item %}

    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="navbar-nav mr-auto">
            {{ render_nav_item('index', 'Home') }}
            {{ render_nav_item('explore', 'Explore') }}
            {{ render_nav_item('about', 'About') }}
        </div>
    </nav>

API
~~~~

.. py:function:: render_nav_item(endpoint, text, badge='', use_li=False, **kwargs)

    Render a Bootstrap nav item.

    :param endpoint: The endpoint used to generate URL.
    :param text: The text that will displayed on the item.
    :param badge: Badge text.
    :param use_li: Default to generate ``<a></a>``, if set to ``True``, it will generate ``<li><a></a></li>``.
    :param kwargs: Additional keyword arguments pass to ``url_for()``.


render_breadcrumb_item()
--------------------------
Render a Bootstrap breadcrumb item.

Example
~~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/nav.html' import render_breadcrumb_item %}

    <nav aria-label="breadcrumb">
        <ol class="breadcrumb">
            {{ render_breadcrumb_item('home', 'Home') }}
            {{ render_breadcrumb_item('users', 'Users') }}
            {{ render_breadcrumb_item('posts', 'Posts') }}
            {{ render_breadcrumb_item('comments', 'Comments') }}
        </ol>
    </nav>

API
~~~~

.. py:function:: render_breadcrumb_item(endpoint, text, **kwargs)

    Render a Bootstrap breadcrumb item.

    :param endpoint: The endpoint used to generate URL.
    :param text: The text that will displayed on the item.
    :param kwargs: Additional keyword arguments pass to ``url_for()``.

render_field()
----------------

Render a form field create by Flask-WTF/WTForms.

Example
~~~~~~~~
.. code-block:: jinja

    {% from 'bootstrap/form.html' import render_field %}

    <form method="post">
        {{ form.csrf_token() }}
        {{ render_field(form.username) }}
        {{ render_field(form.password) }}
        {{ render_field(form.submit) }}
    </form>

API
~~~~

.. py:function:: render_field(field, form_type="basic", horizontal_columns=('lg', 2, 10), button_style="", button_size="", button_map={})

    Render a single form field.

    :param field: The form field (attribute) to render.
    :param form_type: One of ``basic``, ``inline`` or ``horizontal``. See the
                     Bootstrap docs for details on different form layouts.
    :param horizontal_columns: When using the horizontal layout, layout forms
                              like this. Must be a 3-tuple of ``(column-type,
                              left-column-size, right-column-size)``.
    :param button_style: Accpet Bootstrap button style name (i.e. priamry, secondary, outline-success, etc.),
                    default to ``secondary`` (e.g. ``btn-secondary``). This will overwrite config ``BOOTSTRAP_BTN_STYLE``.
    :param button_size: Accept Bootstrap button size name: sm, md, lg, block, default to ``md``. This will 
                    overwrite config ``BOOTSTRAP_BTN_SIZE``.
    :param button_map: A dictionary, mapping button field name to Bootstrap button style names. For example, 
                      ``{'submit': 'success'}``. This will overwrite ``button_style`` and ``BOOTSTRAP_BTN_STYLE``.

.. tip:: See :ref:`button_customization` to learn how to customize form buttons.

render_form()
---------------
Render a form object create by Flask-WTF/WTForms.

Example
~~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/form.html' import render_form %}

    {{ render_form(form) }}

API
~~~~

.. py:function:: render_form(form,\
                    action="",\
                    method="post",\
                    extra_classes=None,\
                    role="form",\
                    form_type="basic",\
                    horizontal_columns=('lg', 2, 10),\
                    enctype=None,\
                    button_style="",\
                    button_size="",\
                    button_map={},\
                    id="",\
                    novalidate=False,\
                    render_kw={})

    Outputs Bootstrap-markup for a complete Flask-WTF form.

    :param form: The form to output.
    :param action: The URL to receive form data.
    :param method: ``<form>`` method attribute.
    :param extra_classes: The classes to add to the ``<form>``.
    :param role: ``<form>`` role attribute.
    :param form_type: One of ``basic``, ``inline`` or ``horizontal``. See the
                     Bootstrap docs for details on different form layouts.
    :param horizontal_columns: When using the horizontal layout, layout forms
                              like this. Must be a 3-tuple of ``(column-type,
                              left-column-size, right-column-size)``.
    :param enctype: ``<form>`` enctype attribute. If ``None``, will
                    automatically be set to ``multipart/form-data`` if a
                    :class:`~wtforms.fields.FileField` or :class:`~wtforms.fields.MultipleFileField` is present in the form.
    :param button_style: Accpet Bootstrap button style name (i.e. priamry, secondary, outline-success, etc.),
                    default to ``secondary`` (e.g. ``btn-secondary``). This will overwrite config ``BOOTSTRAP_BTN_STYLE``.
    :param button_size: Accept Bootstrap button size name: sm, md, lg, block, default to ``md``. This will 
                    overwrite config ``BOOTSTRAP_BTN_SIZE``.
    :param button_map: A dictionary, mapping button field name to Bootstrap button style names. For example, 
                      ``{'submit': 'success'}``. This will overwrite ``button_style`` and ``BOOTSTRAP_BTN_STYLE``.
    :param id: The ``<form>`` id attribute.
    :param novalidate: Flag that decide whether add ``novalidate`` class in ``<form>``.
    :param render_kw: A dictionary, specifying custom attributes for the
                     ``<form>`` tag.

.. py:function:: form_errors(form, hiddens=True)

    Renders paragraphs containing form error messages. This is usually only used
    to output hidden field form errors, as others are attached to the form
    fields.

    :param form: Form whose errors should be rendered.
    :param hiddens: If ``True``, render errors of hidden fields as well. If
                   ``'only'``, render *only* these.

.. tip:: See :ref:`button_customizatoin` to learn how to customize form buttons.

render_form_row()
------------------

Render a row of a grid form.

Example
~~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/form.html' import render_form_row %}

    <form method="post">
        {{ form.csrf_token() }}
        {{ render_form_row([form.username, form.password]) }}
        {{ render_form_row([form.remember]) }}
        {{ render_form_row([form.submit]) }}
        {# Custom col which should use class col-md-2, and the others the defaults: #}
        {{ render_form_row([form.title, form.first_name, form.surname], col_map={'title': 'col-md-2'}) }}
        {# Custom col which should use class col-md-2 and modified col class for the default of the other fields: #}
        {{ render_form_row([form.title, form.first_name, form.surname], col_class_default='col-md-5', col_map={'title': 'col-md-2'}) }}
    </form>

API
~~~~

.. py:function:: render_form_row(fields,\
                                 row_class='form-row',\
                                 col_class_default='col',\
                                 col_map={},\
                                 button_style="",\
                                 button_size="",\
                                 button_map={})

    Render a bootstrap row with the given fields.

    :param fields: An iterable of fields to render in a row.
    :param row_class: Class to apply to the div intended to represent the row, like ``form-row`` 
                      or ``row``
    :param col_class_default: The default class to apply to the div that represents a column
                                if nothing more specific is said for the div column of the rendered field.
    :param col_map: A dictionary, mapping field.name to a class definition that should be applied to 
                            the div column that contains the field. For example: ``col_map={'username': 'col-md-2'})``
    :param button_style: Accpet Bootstrap button style name (i.e. priamry, secondary, outline-success, etc.),
                    default to ``secondary`` (e.g. ``btn-secondary``). This will overwrite config ``BOOTSTRAP_BTN_STYLE``.
    :param button_size: Accept Bootstrap button size name: sm, md, lg, block, default to ``md``. This will 
                    overwrite config ``BOOTSTRAP_BTN_SIZE``.
    :param button_map: A dictionary, mapping button field name to Bootstrap button style names. For example, 
                      ``{'submit': 'success'}``. This will overwrite ``button_style`` and ``BOOTSTRAP_BTN_STYLE``.                      

.. tip:: See :ref:`button_customizatoin` to learn how to customize form buttons.

render_pager()
-----------------

Render a pagination object create by Flask-SQLAlchemy.

Example
~~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/pagination.html' import render_pager %}

    {{ render_pager(pagination) }}


API
~~~~

.. py:function:: render_pager(pagination,\
                      fragment='',\
                      prev=('<span aria-hidden="true">&larr;</span> Previous')|safe,\
                      next=('Next <span aria-hidden="true">&rarr;</span>')|safe,\
                      align='',\
                      **kwargs)

    Renders a simple pager for query pagination.

    :param pagination: :class:`~flask_sqlalchemy.Pagination` instance.
    :param fragment: Add url fragment into link, such as ``#comment``.
    :param prev: Symbol/text to use for the "previous page" button.
    :param next: Symbol/text to use for the "next page" button.
    :param align: Can be 'left', 'center' or 'right', default to 'left'.
    :param kwargs: Additional arguments passed to ``url_for``.


render_pagination()
--------------------

Render a pagination object create by Flask-SQLAlchemy.

Example
~~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/pagination.html' import render_pagination %}

    {{ render_pagination(pagination) }}

API
~~~~

.. py:function:: render_pagination(pagination,\
                     endpoint=None,\
                     prev='«',\
                     next='»',\
                     ellipses='…',\
                     size=None,\
                     args={},\
                     fragment='',\
                     align='',\
                     **kwargs)

    Render a standard pagination for query pagination.

    :param pagination: :class:`~flask_sqlalchemy.Pagination` instance.
    :param endpoint: Which endpoint to call when a page number is clicked.
                    :func:`~flask.url_for` will be called with the given
                    endpoint and a single parameter, ``page``. If ``None``,
                    uses the requests current endpoint.
    :param prev: Symbol/text to use for the "previous page" button. If
                ``None``, the button will be hidden.
    :param next: Symbol/text to use for the "next page" button. If
                ``None``, the button will be hidden.
    :param ellipses: Symbol/text to use to indicate that pages have been
                    skipped. If ``None``, no indicator will be printed.
    :param size: Can be 'sm' or 'lg' for smaller/larger pagination.
    :param args: Additional arguments passed to :func:`~flask.url_for`. If
                ``endpoint`` is ``None``, uses :attr:`~flask.Request.args` and
                :attr:`~flask.Request.view_args`
    :param fragment: Add url fragment into link, such as ``#comment``.
    :param align: The align of the paginationi. Can be 'left', 'center' or 'right', default to 'left'.
    :param kwargs: Extra attributes for the ``<ul>``-element.


render_static()
----------------
Render a resource reference code (i.e. ``<link>``, ``<script>``).

Example
~~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/utils.html' import render_static %}

    {{ render_static('css', 'style.css') }}

API
~~~~

.. py:function:: render_static(type, filename_or_url, local=True)

    Render a resource reference code (i.e. ``<link>``, ``<script>``).

    :param type: Resources type, one of ``css``, ``js``, ``icon``.
    :param filename_or_url: The name of the file, or the full url when ``local`` set to ``False``.
    :param local: Load local resources or from the passed URL.


render_messages()
------------------

Render flashed messages send by ``flask.flash()``.

Example
~~~~~~~~

Flash the message in your view function with ``flash(message, category)``:

.. code-block:: python

    from flask import flash

    @app.route('/test')
    def test():
        flash('a info message', 'info')
        flash('a danger message', 'danger')
        return your_template

Render the messages in your base template (normally below the navbar):

.. code-block:: jinja

    {% from 'bootstrap/utils.html' import render_messages %}

    <nav>...</nav>
    {{ render_messages() }}
    <main>...</main>

API
~~~~

.. py:function:: render_messages(messages=None,\
                    container=False,\
                    transform={...},\ 
                    default_category='primary',\
                    dismissible=False,\
                    dismiss_animate=False)

    Render Bootstrap alerts for flash messages send by ``flask.flash()``.

    :param messages: The messages to show. If not given, default to get from ``flask.get_flashed_messages(with_categories=True)``.
    :param container: If true, will output a complete ``<div class="container">`` element, otherwise just the messages each wrapped in a ``<div>``.
    :param transform: A dictionary of mappings for categories. Will be looked up case-insensitively. Default maps all Python loglevel names to Bootstrap CSS classes.
    :param default_category: If a category does not has a mapping in transform, it is passed through unchanged. ``default_category`` will be used when ``category`` is empty.
    :param dismissible: If true, will output a button to close an alert. For fully functioning dismissible alerts, you must use the alerts JavaScript plugin.
    :param dismiss_animate: If true, will enable dismiss animate when click the dismiss button.

When you call ``flash('message', 'category')``, threre are 8 category options available, mapping to Bootstrap 4's alerts type:

primary, secondary, success, danger, warning, info, light, dark.

If you want to use HTML in your message body, just warpper your message string with ``flask.Markup`` to tell Jinja it's safe:

.. code-block:: python

    from flask import flash, Markup

    @app.route('/test')
    def test():
        flash(Markup('a info message with a link: <a href="/">Click me!</a>'), 'info')
        return your_template


render_table()
--------------
Render a Bootstrap table

Example
~~~~~~~

.. code-block:: jinja

    {% from 'bootstrap/table.html' import render_table %}
    {{ render_table(titles, data) }}


API
~~~~

.. py:function:: render_table(titles,\
                              data,\
                              primary_key='id',\
                              caption=None,\
                              table_classes=None,\
                              header_classes=None,\
                              is_responsive=False,\
                              responsive_class='table-responsive')

    Render a bootstrap tables

    :param titles: An iterable of tuples of the format (prop, label) e.g ``[('id', '#')]``
    :param data: An iterable of data objects to render. Can be dicts or class objects.
    :param primary_key: Primary key identifier for a single row
    :param caption: A caption to attach to the table
    :param table_classes: A string of classes to apply to the table e.g ``'table-small table-dark'``
    :param header_classes: A string of classes to apply to the table header e.g ``'thead-dark'``
    :param is_responsive: Whether to enable/disable table responsiveness
    :param responsive_class: The responsive class to apply to the table. Default is ``'table-responsive'``