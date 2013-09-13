.. _docutils: http://docutils.sourceforge.net/
.. _Django: https://www.djangoproject.com/
.. _django-crispy-forms: https://github.com/maraujop/django-crispy-forms
.. _Foundation: http://github.com/zurb/foundation
.. _Foundation Grid: http://foundation.zurb.com/docs/grid.php

Introduction
============

This is a `Django`_ application to add `django-crispy-forms`_ layout objects for `Foundation`_.

Actually this is only to use specific templates and changing some CSS class names.

This app does not embed a `Foundation`_ release, you will have to install it yourself.

Links
*****

* Download his `PyPi package <http://pypi.python.org/pypi/crispy-forms-foundation>`_;
* Clone it on his `Github repository <https://github.com/sveetch/crispy-forms-foundation>`_;

Requires
========

* `django-crispy-forms`_ = 1.2.x;

Installation
============

Just register the app in your project settings like this :

.. sourcecode:: python

    INSTALLED_APPS = (
        ...
        'crispy_forms',
        'crispy_forms_foundation',
        ...
    )

Then append this part to specify usage of the Foundation set :

.. sourcecode:: python

    # Default layout to use with "crispy_forms"
    CRISPY_TEMPLATE_PACK = 'foundation'

All other `django-crispy-forms`_ settings option apply, see its documentation for more details.

Usage
=====

Import **crispy-forms-foundation** then you can use the layout object in your forms :
    
.. sourcecode:: python

    from crispy_forms_foundation.layout import Layout, Fieldset, Field, SplitDateTimeField, RowFluid, Column, Div, ButtonHolder, Submit, HTML

    class YourForm(forms.ModelForm):
        """
        *Page* form
        """
        def __init__(self, *args, **kwargs):
            self.helper = FormHelper()
            self.helper.form_action = '.'
            self.helper.layout = Layout(
                Fieldset(
                    ugettext('Content'),
                    'title',
                    'content',
                ),
                Fieldset(
                    ugettext('Display settings'),
                    RowFluid(
                        Column('template', css_class='small-6'),
                        Column('order', css_class='small-3'),
                        Column('visible', css_class='small-3'),
                    ),
                ),
                Fieldset(
                    ugettext('Publish settings'),
                    'parent',
                    RowFluid(
                        Column(SplitDateTimeField('published'), css_class='small-6'),
                        Column('slug', css_class='small-6'),
                    ),
                ),
                ButtonHolder(
                    Submit('submit_and_continue', ugettext('Save and continue')),
                    Submit('submit', ugettext('Save')),
                ),
            )
            
            super(YourForm, self).__init__(*args, **kwargs)

The embedded templates are in ``crispy_forms_foundation/templates/foundation``.

Layout items
************

For now there are only two layout items dedicated to Foundation (Row and Column), other embedded items are cloned from the **uni_form** layout items from `django-crispy-forms`_.

Row
---

Act as a div container row, it will embed his items in a div like this : ::

    <div class"row">Your stuff</div>


Column
------

This is the column from the `Foundation Grid`_, all columns should be contained in a `Row`_ and you will have to define the column type in the ``css_class`` attribute.

With a ``css_class`` attribute defined to ``twelve``, it will embed his items in a div like this : ::

    <div class"columns twelve">Your stuff</div>
