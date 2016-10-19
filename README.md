Swiftmailer Manipulator for Symfony
===================================

[![Build Status](https://travis-ci.org/pixelart/swiftmailer-manipulator-bundle.svg?branch=master)](https://travis-ci.org/pixelart/swiftmailer-manipulator-bundle)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/pixelart/swiftmailer-manipulator-bundle/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/pixelart/swiftmailer-manipulator-bundle/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/pixelart/swiftmailer-manipulator-bundle/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/pixelart/swiftmailer-manipulator-bundle/?branch=master)
[![Code Style](https://styleci.io/repos/70606516/shield?style=flat)](https://styleci.io/repos/70606516)

Sometimes you have staging systems, where you can't install [MailHog] and
using `delivery_address` or `disable_delivery` on the SwiftmailerBundle is
not enough. For example your customer wants the mail to be really delivered.

But maybe the crafted mail goes to a partner, retailer, user, whatever and now
they are worried why they got them (for example notification systems).

This bundle can help you! It provides a plugin into Swiftmailer, which allows
you to modify the subject or body or the from address of every message before
delivery.

Installation
------------

### Step 1: Download the Bundle

Open a command console, enter your project directory and execute the
following command to download the latest stable version of this bundle:

```console
$ composer require pixelart/swiftmailer-manipulator-bundle ^1.0
```

This command requires you to have Composer installed globally, as explained
in the [installation chapter][composer global install] of the Composer
documentation.

### Step 2: Enable the Bundle

Then, enable the bundle by adding it to the list of registered bundles
in the `app/AppKernel.php` file of your project:

```php
<?php
// app/AppKernel.php

// ...
class AppKernel extends Kernel
{
    public function registerBundles()
    {
        $bundles = array(
            // ...

            new Pixelart\Bundle\SwiftmailerManipulatorBundle\PixelartSwiftmailerManipulatorBundle(),
        );

        // ...
    }

    // ...
}
```

### Step 3: Configure the Bundle

Now, configure your wanted manipulations. You have the option to prepend
the subject with an string, to prepend the body with the content of a
template or change the message's from address.

If you are using the default swiftmailer configuration, the config is:

```yaml
# app/config_stage.yml

pixelart_swiftmailer_manipulator:
    prepend_subject: '[TESTSYSTEM!]'
    prepend_body: 'swiftmailer/prepend_body.txt.twig'
    from_address: 'impersonated@example.com'
```

The bundle supports multiple swiftmailer mailers too. You only need to add
the mailers you want to manipulate. For example if you have three configured
mailers, `first_mailer`, `secondary_mailer` and `third_mailer`, but you don't
want to prepend `third_mailer`:

```yaml
# app/config_stage.yml

pixelart_swiftmailer_manipulator:
    mailers:
        first_mailer:
            prepend_subject: '[TESTSYSTEM 1!]'
            prepend_body: 'swiftmailer/prepend_body_1.txt.twig'
        secondary_mailer:
            prepend_subject: '[TESTSYSTEM 2!]'
            prepend_body: 'swiftmailer/prepend_body_2.txt.twig'
```

Contributing
------------

The [contributing](CONTRIBUTING.md) guidelines contains all the information
about contributing to the bundle.

Bug tracking
------------

We use [GitHub issues](https://github.com/pixelart/swiftmailer-manipulator-bundle/issues)
and [waffle.io board](https://waffle.io/pixelart/swiftmailer-manipulator-bundle)
to track issues. If you have found bug, please create an issue.

MIT License
-----------

License can be found [here](LICENSE).

Code of Conduct
---------------

This project adheres to the Contributor Covenant [code of conduct](CODE_OF_CONDUCT.md).
By participating, you are expected to uphold this code.

[MailHog]: https://github.com/mailhog/MailHog
[composer global install]: https://getcomposer.org/doc/00-intro.md
