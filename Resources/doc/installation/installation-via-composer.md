# Installation via composer
---------------------------------------

[go back to Table of contents][back-to-index]

[back-to-index]: https://github.com/symfony2admingenerator/GeneratorBundle/blob/master/Resources/doc/documentation.md#1-installation

### 1. Download files

#### 1.1 Add Admingenerator to your `composer.json`:

```json
"require": {
    "symfony2admingenerator/generator-bundle": "dev-master"
},
```

### 1.2 Configure components dir in your `composer.json`:

```json
"config": {
    "component-dir": "web/components" 
},
```

Then run `php composer.phar update` command.

> **Note:** If you're getting **no matching package found** error then you must also add `"minimum-stability": "dev"` to your **composer.json** file.
    
### 2. Enable bundles

Admingenerator has a dependency on:
 
 * KnpMenuBundle
 * WhiteOctoberPagerfantaBundle
 * FormBundle
 * JMSSecurityExtraBundle

> **Note:** there are also some optional dependencies, each is described in corresponding feature`s doc. This guide describes only the minimal-setup. 

Enable Admingenerator and its dependencies in your `app/AppKernel.php`:

```php
<?php 
public function registerBundles()
{
    $bundles = array(
        // ...
        new JMS\AopBundle\JMSAopBundle(),
        new JMS\SecurityExtraBundle\JMSSecurityExtraBundle(),
        new JMS\DiExtraBundle\JMSDiExtraBundle($this),
        new Admingenerator\FormBundle\AdmingeneratorFormBundle(),
        new Admingenerator\GeneratorBundle\AdmingeneratorGeneratorBundle(),
        new Knp\Bundle\MenuBundle\KnpMenuBundle(),
        new WhiteOctober\PagerfantaBundle\WhiteOctoberPagerfantaBundle(),
    );
}
?>
```

You also need to configure the JMS Security Extra Bundle:

```yaml
jms_security_extra:
    # Enables expression language
    expressions: true

```

### 3. Basic configuration

Choose your model manager and choose basic admingenerator template - with or without assetic. -- add following lines to `app/config/config.yml`:

```yaml
admingenerator_generator:
    # choose  and enable at least one
    use_propel:           true
    use_doctrine_orm:     true
    use_doctrine_odm:     false
    
    # choose and uncomment only one
#    base_admin_template: AdmingeneratorGeneratorBundle::base_admin.html.twig
#    base_admin_template: AdmingeneratorGeneratorBundle::base_admin_assetic_less.html.twig
```

### (Optional) Configure Assetic to use UglifyCSS and UglifyJS

By default, the `base_admin.html.twig` uses UglifyCSS and UglifyJS to minify assets and combine them into one file (less HTTP requests).

In order to properly install and configure UglifyCSS and UglifyJS follow [this article](http://symfony.com/doc/current/cookbook/assetic/uglifyjs.html)

> See also [Asset Management](http://symfony.com/doc/current/cookbook/assetic/asset_management.html) cookbook entry.

### 4. Install assets

To install assets in your web directory run:

`php app/console assets:install web --symlink`

> **Note:** We recommend installing assets with `--symlink` option, however you may skip this option if you wish to hard copy assets.

### (Optional) Dump assets

If you're useing assetic for asset management dump your assets by running:

`php app/console assetic:dump`

### 5. Specify routes

#### Dashboard route (Optional)
By default brand text ("Dashboard") is disabled. To link it with your Dashboard add `dashboard_welcome_path` under `admingenerator_generator` in your `app/config/config.yml`:

```yaml
admingenerator_generator:
    dashboard_welcome_path:     MyDashboard_path
```
