.. _php/configuration/software/multi_contexts:

Multi-Contexts
##############

Configuration
*************

To change the contexts of your Novius OS instance, edit the :file:`local/config/contexts.config.php` file.

Default configuration
=====================

After installation, Novius OS is configured with three contexts, one site in three languages:

.. code-block:: php

	<?php
	return array(
		'sites' => array(
			'main' => array(
				'title' => 'Main site',
				'alias' => 'Main',
			),
		),

		'locales' => array(
			'fr_FR' => array(
				'title' => 'Français',
				'flag' => 'fr',
			),
			'en_GB' => array(
				'title' => 'English',
				'flag' => 'gb',
			),
			'ja_JP' => array(
				'title' => '日本語',
				'flag' => 'jp',
			),
		),

		'contexts' => array(
			'main::en_GB' => array(),
			'main::fr_FR' => array(),
			'main::ja_JP' => array(),
		),
	);

Multi-sites / multi-languages
=============================

Here is an example configuration with five contexts across three sites and three languages:

.. code-block:: php

	<?php
	return array(
		'sites' => array(
			'main' => array(
				'title' => 'Main site',
				'alias' => 'main',
			),
			'mobile' => array(
				'title' => 'Mobile site',
				'alias' => 'Mobile',
			),
			'event' => array(
				'title' => 'Event site',
				'alias' => 'Event',
			),
		),

		'locales' => array(
			'en_GB' => array(
				'title' => 'English',
				'flag' => 'gb',
			),
			'fr_FR' => array(
				'title' => 'Français',
				'flag' => 'fr',
			),
			'es_ES' => array(
				'title' => 'Español',
				'flag' => 'es',
			),
		),

		'contexts' => array(
			'main::en_GB' => array(),
			'main::fr_FR' => array(),
			'main::es_ES' => array(),
			'mobile::fr_FR' => array(),
			'event::en_GB' => array(),
		),
	);


One site in one language
========================

Here is an example configuration for just one site in one language:

.. code-block:: php

	<?php
	return array(
		'sites' => array(
			'main' => array(
				'title' => 'Main site',
				'alias' => 'main',
			),
		),

		'locales' => array(
			'en_GB' => array(
				'title' => 'English',
				'flag' => 'gb',
			),
		),

		'contexts' => array(
			'main::en_GB' => array(),
		),
	);


Domain Names
************

By default, the first context will answer to the root of your domain, the following contexts in a
:file:`site_code/language_code/` subdirectory (e.g.: :file:`main/es_ES/`).

But for each context, you can choose the URI (including a domain and optionally a directory) it will answer to, by
specifying it the the associated configuration array.

Contexts on subdirectory
========================

.. code-block:: php

	<?php

    'contexts' => array(
        'main::en_GB' => array(), // Uses the default domain
        'main::fr_FR' => array(
            'http://www.mysite.com/fr/',
        ),
        'main::es_ES' => array(
            'http://www.mysite.com/es/',
        ),
        'mobile::fr_FR' => array(
            'http://www.mysite.com/mobile/',
        ),
        'event::en_GB' => array(
            'http://www.mysite.com/event/',
        ),
    ),

.. warning::

	If your main context (the first) has a :file:`fr/example.html` page and your ``main::fr_FR`` context has an
	:file:`example.html` page, their URLs are identical (ie: :file:`http://www.mysite.com/fr/example.html`). In this
	situation, only the page of your main context will be accessible.

Contexts on domains
===================

.. code-block:: php

    <?php

    'contexts' => array(
        'main::en_GB' => array(
            'http://www.monsite.com/',
        ),
        'main::fr_FR' => array(
            'http://www.mysite.fr/',
        ),
        'main::es_ES' => array(
            'http://www.monsite.es/',
        ),
        'mobile::fr_FR' => array(
            'http://mobile.monsite.fr/',
        ),
        'event::en_GB' => array(
            'http://event.monsite.com/',
        ),
    ),

.. note::

	Of course, your domains should also be properly configured in :program:`Apache`.

Contexts with multiple URLs
===========================

.. code-block:: php

	<?php
	'contexts' => array(
		'main::en_GB' => array(
			'http://www.monsite.com/',
		),
		'main::fr_FR' => array(
			'http://www.mysite.fr/',
		),
		'main::es_ES' => array(
			'http://www.monsite.es/',
		),
		'mobile::fr_FR' => array(
			'http://mobile.monsite.fr/',
			'http://www.monsite-mobile.fr/',
			'http://www.mysite.com/mobile/',
		),
		'event::en_GB' => array(
			'http://event.monsite.en/',
		),
	),

Going live
**********

You will probably need to define, for each of your contexts, different URLs between your local (development) and
production instances.
You can do that using :term:`environment-specific config files <Environments>`.
