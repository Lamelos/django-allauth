Forked from: https://github.com/pennersr/django-allauth

In this fork I've added a setting for ALLAUTH

.. code-block::

    ALLAUTH_AUTO_SETUP_PROVIDERS = True

which when enabled automatically creates a SocialApp model when needed with client_id and secret settings specified in the provider settings. I use environment files for my deployment needs so I don't want to go meddling in the Django admin to create a new SocialApp for each deployed site. This way I can use the site specific environment file (which already has super-secret stuff, such as database password, secret_key and other api settings).

Example usage:

.. code-block::

    import environ
    env = environ.Env()     # get environment

    ALLAUTH_AUTO_SETUP_PROVIDERS = True     # enable automatic creation of SocialApp for providers
    SOCIALACCOUNT_PROVIDERS = {
        'office365': {
          'client_id': env('OFFICE365_APPLICATION_ID'),
          'secret': env('OFFICE365_SECRET')
        }
    }
