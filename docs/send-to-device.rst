.. This Source Code Form is subject to the terms of the Mozilla Public
.. License, v. 2.0. If a copy of the MPL was not distributed with this
.. file, You can obtain one at http://mozilla.org/MPL/2.0/.

.. _sendtodevice:

=====================
Send to Device widget
=====================

The *Send to Device* widget is a single macro form which facilitates the sending of a download link for either Firefox for iOS, Firefox for Android, or both. The form allows sending via SMS or Email, although the SMS copy & messaging is shown only to those in the US. Geo-location is handled in JavaScript using `GeoDude <https://github.com/mozilla/geodude>`_. For users without JavaScript, the widget falls back to a standard Email form.

.. important:: This widget should only be shown to a limited set of locales who are set up to receive the emails. For those locales not in the list, direct links to the respective app stores should be shown instead. If a user is on iOS or Android, CTA buttons should also link directly to respective app stores instead of showing the widget. This logic should be handled on a page-by-page basis to cover individual needs.

.. note:: A full list of supported locales can be found in ``settings/base.py`` under ``SEND_TO_DEVICE_LOCALES``, which can be used in the template logic for each page to show the form.

Usage
-----

1. Include this macro::

    {% from "macros.html" import send_to_device with context %}

2. Add the appropriate lang file to the page template::

    {% add_lang_files "firefox/sendto" %}

3. Make sure necessary files are in your CSS/JS bundles:

  - ``'css/base/send-to-device.less'``

  - ``'js/base/send-to-device.js'``

4. Include the macro in your page template::

    {{ send_to_device() }}

  The macro defaults to sending links for both Android and iOS apps. You can also pass a 'platform' to specify different configuration options::

      {{ send_to_device(platform='select') }}

  * ``select`` shows a drop down so the user can choose their platform.
  * ``ios`` sends the user a link to Firefox for iOS only.
  * ``android`` sends the user a link to Firefox for Android only.

  If the page requires a custom title for the widget, you can also pass an optional heading::

      {{ send_to_device(title_text='Foo Bar') }}

  If you do not want to show a title, you can pass ``include_title=False`::

      {{ send_to_device(include_title=False) }}

  To add a logo and rounded corners to the widget for display in a modal::

      {{ send_to_device(include_logo=True) }}

5. Initialize the widget:

  In your page JS, initialize the widget using::

    var form = new Mozilla.SendToDevice();
    form.init();

Example
-------

You can view a simple example by navigating to ``/styleguide/docs/send-to-device/`` in your local development environment (not available in production).
